# Implementing a New Puzzle
This page aims to be a straightforward guide for developers in creating a new puzzle for LEGUP.
In this example, we will create <a href="https://en.wikipedia.org/wiki/Nurikabe_(puzzle)">Nurikabe</a>,
a simple puzzle game played on a rectangular grid.

*Note.* All project files can be found in the [tutorial repository](https://github.com/armendbm/Legup/tree/master/src/main/java/edu/rpi/legup/puzzle/nurikabe).

## Organization and Classes
We begin by creating a new directory under `src/main/java/edu/rpi/legup/puzzle` called `nurikabe`.
Every puzzle in LEGUP extends the abstract class `edu.rpi.legup.model.Puzzle`. The constructor and
the following abstract methods must be implemented:
* `public void initializeView()`
* `public Board generatePuzzle(int difficulty)`
* `public boolean isBoardComplete(Board board)`
* `public void onBoardChange(Board board)`

Although all of these methods need to be overridden, not all of them need to do something. For example,
puzzle generation is not a feature required for every puzzle, so this method may do nothing. Also, there
may be no need to do anything on board change. With all of this known, we can create a basic `Nurikabe`
class.
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.model.Puzzle;
import edu.rpi.legup.model.gameboard.Board;

public class Nurikabe extends Puzzle {
    public Nurikabe() {
        super();
    }

    @Override
    public void initializeView() {
    }

    @Override
    public Board generatePuzzle(int difficulty) {
        return null;
    }

    @Override
    public boolean isBoardComplete(Board board) {
        return true;
    }

    @Override
    public void onBoardChange(Board board) {
    }
}
```
This code will compile, but it clearly does nothing. The first thing to analyze here is the
`edu.rpi.legup.model.gameboard.Board` class. Every puzzle has its own requirements for the board,
and we implement this by extending `Board`. At a high level, a `Board` is a list of `PuzzleElement`s,
with a few helper methods to be overridden by subclasses. Nurikabe is a grid-based puzzle, so we can extend
the helper class `edu.rpi.legup.model.gameboard.GridBoard`, which holds an array of `GridCell`s.
In this game, each cell is either unset (gray), white, black, or a number. The first three cell types
are mutable, while number cells are immutable.

We start by creating a simple enum of the cell types, in `NurikabeType.java`. For conversion to
`int` we subtract 2 from the ordinal value: this way we can assume that any cell with a value
greater than 0 is a number cell.
```java
package edu.rpi.legup.puzzle.nurikabe;

public enum NurikabeType {
    UNKNOWN, BLACK, WHITE, NUMBER;

    public int toValue() {
        return this.ordinal() - 2;
    }
}
```
Then we can extend `GridCell`:
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.model.gameboard.GridCell;

import java.awt.Point;

public class NurikabeCell extends GridCell<Integer> {
    public NurikabeCell(int valueInt, Point location) {
        super(valueInt, location);
    }

    public NurikabeType getType() {
        switch (data) {
            case -2:
                return NurikabeType.UNKNOWN;
            case -1:
                return NurikabeType.BLACK;
            case 0:
                return NurikabeType.WHITE;
            default:
                if (data > 0) {
                    return NurikabeType.NUMBER;
                }
        }
        return null;
    }

    @Override
    public NurikabeCell copy() {
        NurikabeCell copy = new NurikabeCell(data, (Point) location.clone());
        copy.setIndex(index);
        copy.setModifiable(isModifiable);
        copy.setGiven(isGiven);
        return copy;
    }
}
```
Finally, we create our `NurikabeBoard`:
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.model.gameboard.GridBoard;
import edu.rpi.legup.model.gameboard.PuzzleElement;

public class NurikabeBoard extends GridBoard {
    public NurikabeBoard(int width, int height) {
        super(width, height);
    }

    public NurikabeBoard(int size) {
        super(size, size);
    }

    @Override
    public NurikabeCell getCell(int x, int y) {
        return (NurikabeCell) super.getCell(x, y);
    }
}
```

*Note.* In this case, extending `GridBoard` does very little. But some puzzles add
extra convenience methods to their boards, and uniformity justifies making a `NurikabeBoard`.

## Adding Rules
LEGUP allows a user to find a solution by applying simple axioms, or rules. There are
three types of rules in LEGUP: basic, case, and contradiction. Basic rules represent a
logical continuation of the puzzle solution; case rules represent two possible paths on
which the solution may go, and create a branch in the proof tree; contradiction rules
show that a contradiction with the rules of the puzzle has been derived, and kill the
current branch of the proof tree.

In general, basic rules are *not* required to solve a puzzle, since they can be derived
from the other two types. For example, one such basic rule for Nurikabe may be the following:
> If a cell is surrounded by white squares, the cell must be white.

However, if we apply the case rule (that the cell can be either black or white), in the case
where the cell is black, we can apply the contradiction rule:
> All black cells must be connected.

This kills the branch, and we have proven that the cell is white.

Thus, for brevity's sake, we will implement every contradiction rule in Nurikabe
and the one case rule since they are necessary, but only one basic rule as an example.
The following rules make up Nurikabe:
> Each connected set of white cells must contain exactly one numbered cell.

> The size of a connected set of white cells must be the number given in its numbered cell.

> All black cells must be connected.

> There may not be a 2x2 area of black cells.

All rules go into a subpackage called `rules`.

### Contradiction Rules
We divide the first rule into two&mdash;
the first having no numbers, the second having more than one. We begin in `NoNumberContradictionRule.java`.

*Note.* To ease implementing the rules, we use a few utilities defined in the `NurikabeUtilities` class, which the reader can find along with the other Nurikabe files in the `main` branch. Implementing these features is outside the scope of this tutorial.
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.puzzle.nurikabe.NurikabeBoard;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;
import edu.rpi.legup.puzzle.nurikabe.NurikabeUtilities;
import edu.rpi.legup.utility.DisjointSets;

import java.util.Set;

public class NoNumberContradictionRule extends ContradictionRule {
    private final String NO_CONTRADICTION_MESSAGE = "Does not contain a contradiction at this index";
    private final String INVALID_USE_MESSAGE = "Contradiction must be a white cell";
    private final String NOT_SURROUNDED_BY_BLACK_MESSAGE = "Must be surrounded by black cells";

    public NoNumberContradictionRule() {
        super("No Number",
                "All enclosed white regions must have a number.",
                "edu/rpi/legup/images/nurikabe/contradictions/NoNumber.png");
    }

    @Override
    public String checkContradictionAt(Board board, PuzzleElement puzzleElement) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board;

        NurikabeCell cell = (NurikabeCell) nurikabeBoard.getPuzzleElement(puzzleElement);
        if (cell.getType() != NurikabeType.WHITE) {
            return super.getInvalidUseOfRuleMessage() + ": " + this.INVALID_USE_MESSAGE;
        }
        DisjointSets<NurikabeCell> regions = NurikabeUtilities.getNurikabeRegions(nurikabeBoard);
        Set<NurikabeCell> whiteRegion = regions.getSet(cell);
        for (NurikabeCell c : whiteRegion) {
            if (c.getType() == NurikabeType.NUMBER) {
                return super.getNoContradictionMessage() + ": " + this.NO_CONTRADICTION_MESSAGE;
            }
        }
        for (NurikabeCell c : whiteRegion) {
            NurikabeCell top = nurikabeBoard.getCell(c.getLocation().x, c.getLocation().y+1);
            NurikabeCell left = nurikabeBoard.getCell(c.getLocation().x-1, c.getLocation().y);
            NurikabeCell right = nurikabeBoard.getCell(c.getLocation().x+1, c.getLocation().y);
            NurikabeCell bottom = nurikabeBoard.getCell(c.getLocation().x, c.getLocation().y-1);

            if (isEmptyCell(top) || isEmptyCell(left) || isEmptyCell(right) || isEmptyCell(bottom))
                return super.getInvalidUseOfRuleMessage() + ": " + this.NOT_SURROUNDED_BY_BLACK_MESSAGE;
        }
        return null;
    }

    private boolean isEmptyCell(NurikabeCell cell)
    {
        if (cell == null)
            return false;
        NurikabeType cellType = cell.getType();
        return cellType != NurikabeType.BLACK && cellType != NurikabeType.WHITE;
    }
}
```
As you can see from the above, in defining `checkContradictionAt()`, we are given a `PuzzleElement`.
In general, LEGUP tests for a contradiction *at every cell in the puzzle.* Thus, at a minimum, we only need
to write code to detect the contradiction for one cell involved. The purpose of the parameter, however, is
actually to allow LEGUP to find the proper error message for each cell when the rule is
applied incorrectly, to report a mistake to the user.
For example, if the above rule is applied when the region still has empty squares adjacent and
the user hovers one of the cells, they will see the error "Must be surrounded by black cells".
Hence it is important for developers to handle every type of `PuzzleElement` in this method and
properly write error messages for them.

Here, we make sure that the cell in question is white, that its region contains no numbers, and that
its region is surrounded by black cells. In this way, we prove the contradiction, and handle every error.

*Note.* In the `checkContradictionAt()` method, returning `null` signifies that the rule
can be correctly applied. Any other return value is considered to be an error message.

Now we continue with the `MultipleNumbersContradictionRule`.
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.puzzle.nurikabe.NurikabeBoard;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;
import edu.rpi.legup.puzzle.nurikabe.NurikabeUtilities;
import edu.rpi.legup.utility.DisjointSets;

import java.util.Set;

public class MultipleNumbersContradictionRule extends ContradictionRule {
    private final String NO_CONTRADICTION_MESSAGE = "Does not contain a contradiction at this index";
    private final String INVALID_USE_MESSAGE = "Contradiction must be a numbered cell";

    public MultipleNumbersContradictionRule() {
        super("Multiple Numbers",
                "All white regions cannot have more than one number.",
                "edu/rpi/legup/images/nurikabe/contradictions/MultipleNumber.png");
    }

    @Override
    public String checkContradictionAt(Board board, PuzzleElement puzzleElement) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board;

        NurikabeCell cell = (NurikabeCell) nurikabeBoard.getPuzzleElement(puzzleElement);
        if(cell.getType() != NurikabeType.NUMBER) {
            return super.getInvalidUseOfRuleMessage() + ": " + INVALID_USE_MESSAGE;
        }
        DisjointSets<NurikabeCell> regions = NurikabeUtilities.getNurikabeRegions(nurikabeBoard);
        Set<NurikabeCell> numberedRegion = regions.getSet(cell);
        for (NurikabeCell c : numberedRegion) {
            if (c != cell && c.getType() == NurikabeType.NUMBER) {
                return null;
            }
        }
        return super.getNoContradictionMessage() + ": " + NO_CONTRADICTION_MESSAGE;
    }
}
```
This rule is simpler&mdash;we only allow it to be applied to numbered cells, and we just verify
that there is at least one more number in the region.

Next, we similarly divide the second rule from above into two&mdash;the first having too
few white cells in a region, the second having too many.
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.puzzle.nurikabe.NurikabeBoard;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;
import edu.rpi.legup.puzzle.nurikabe.NurikabeUtilities;
import edu.rpi.legup.utility.DisjointSets;

import java.util.Set;

public class TooFewSpacesContradictionRule extends ContradictionRule {
    private final String NO_CONTRADICTION_MESSAGE = "Does not contain a contradiction at this index";
    private final String INVALID_USE_MESSAGE = "Contradiction must be a white or a numbered cell";

    public TooFewSpacesContradictionRule() {
        super("Too Few Spaces",
                "A region cannot contain less spaces than its number.",
                "edu/rpi/legup/images/nurikabe/contradictions/TooFewSpaces.png");
    }

    @Override
    public String checkContradictionAt(Board board, PuzzleElement puzzleElement) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board;

        NurikabeCell cell = (NurikabeCell) nurikabeBoard.getPuzzleElement(puzzleElement);
        if (cell.getType() != NurikabeType.WHITE && cell.getType() != NurikabeType.NUMBER) {
            return super.getInvalidUseOfRuleMessage() + ": " + this.INVALID_USE_MESSAGE;
        }

        DisjointSets<NurikabeCell> regions = NurikabeUtilities.getPossibleWhiteRegions(nurikabeBoard);
        Set<NurikabeCell> whiteRegion = regions.getSet(cell);
        NurikabeCell numberedCell = null;
        for (NurikabeCell c : whiteRegion) {
            if (c.getType() == NurikabeType.NUMBER) {
                numberedCell = c;
                break;
            }
        }

        if (numberedCell != null && whiteRegion.size() < numberedCell.getData()) {
            return null;
        }
        return super.getNoContradictionMessage() + ": " + this.NO_CONTRADICTION_MESSAGE;
    }
}
```
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.puzzle.nurikabe.NurikabeBoard;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;
import edu.rpi.legup.puzzle.nurikabe.NurikabeUtilities;
import edu.rpi.legup.utility.DisjointSets;

import java.util.ArrayList;
import java.util.Set;

public class TooManySpacesContradictionRule extends ContradictionRule {

    private final String NO_CONTRADICTION_MESSAGE = "Does not contain a contradiction at this index";
    private final String INVALID_USE_MESSAGE = "Contradiction must be a white or a numbered cell";

    public TooManySpacesContradictionRule() {
        super("Too Many Spaces",
                "A region cannot contain more spaces than its number.",
                "edu/rpi/legup/images/nurikabe/contradictions/TooManySpaces.png");
    }

    @Override
    public String checkContradictionAt(Board board, PuzzleElement puzzleElement) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board;

        NurikabeCell cell = (NurikabeCell) nurikabeBoard.getPuzzleElement(puzzleElement);
        if (cell.getType() != NurikabeType.WHITE && cell.getType() != NurikabeType.NUMBER) {
            return super.getInvalidUseOfRuleMessage() + ": " + this.INVALID_USE_MESSAGE;
        }

        DisjointSets<NurikabeCell> regions = NurikabeUtilities.getNurikabeRegions(nurikabeBoard);
        Set<NurikabeCell> whiteRegion = regions.getSet(cell);
        ArrayList<NurikabeCell> numberedCells = new ArrayList<>();
        for (NurikabeCell c : whiteRegion) {
            if (c.getType() == NurikabeType.NUMBER) {
                numberedCells.add(c);
            }
        }

        for (NurikabeCell number : numberedCells) {
            if (whiteRegion.size() > number.getData()) {
                return null;
            }
        }
        return super.getNoContradictionMessage() + ":" + this.NO_CONTRADICTION_MESSAGE;
    }
}
```
Now, we define the third rule from the introduction to this section, which stated that *all black cells
must be connected.*
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.puzzle.nurikabe.NurikabeBoard;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;
import edu.rpi.legup.puzzle.nurikabe.NurikabeUtilities;
import edu.rpi.legup.utility.DisjointSets;

import java.util.Set;

public class IsolateBlackContradictionRule extends ContradictionRule {

    private final String NO_CONTRADICTION_MESSAGE = "Contradiction applied incorrectly. No isolated Blacks.";
    private final String INVALID_USE_MESSAGE = "Contradiction must be a black cell";

    public IsolateBlackContradictionRule() {
        super("Isolated Black",
                "There must still be a possibility to connect every Black cell",
                "edu/rpi/legup/images/nurikabe/contradictions/BlackArea.png");
    }

    @Override
    public String checkContradictionAt(Board board, PuzzleElement puzzleElement) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board;
        NurikabeCell cell = (NurikabeCell) nurikabeBoard.getPuzzleElement(puzzleElement);
        if (cell.getType() != NurikabeType.BLACK) {
            return super.getInvalidUseOfRuleMessage() + ": " + this.INVALID_USE_MESSAGE;
        }

        DisjointSets<NurikabeCell> blackRegions = NurikabeUtilities.getPossibleBlackRegions(nurikabeBoard);
        boolean oneRegion = false;
        for (Set<NurikabeCell> region : blackRegions.getAllSets()) {
            for (NurikabeCell c : region) {
                if (c.getType() == NurikabeType.BLACK) {
                    if (oneRegion) {
                        return null;
                    } else {
                        oneRegion = true;
                        break;
                    }
                }
            }
        }
        return super.getNoContradictionMessage() + ": " + this.NO_CONTRADICTION_MESSAGE;
    }
}
```
To verify the preceding, we first find all possible black regions (defined as
all regions that are black, assuming that any empty cells are black). Then, we loop through them,
discarding regions made up solely of empty cells (since these may all be white and cause no contradiction),
and if we discover two such regions, we have proven the contradiction.

The final contradiction rule is the restriction against 2x2 regions of black squares. We implement it
as follows:
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.puzzle.nurikabe.NurikabeBoard;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;

public class BlackSquareContradictionRule extends ContradictionRule {

    private final String NO_CONTRADICTION_MESSAGE = "No 2x2 square of black exists.";
    private final String INVALID_USE_MESSAGE = "Does not contain a contradiction at this index";

    public BlackSquareContradictionRule() {
        super("Black Square",
                "There cannot be a 2x2 square of black.",
                "edu/rpi/legup/images/nurikabe/contradictions/BlackSquare.png");
    }

    @Override
    public String checkContradictionAt(Board board, PuzzleElement puzzleElement) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board;
        int height = nurikabeBoard.getHeight();
        int width = nurikabeBoard.getWidth();

        NurikabeCell cell = (NurikabeCell) nurikabeBoard.getPuzzleElement(puzzleElement);
        if (cell.getType() != NurikabeType.BLACK) {
            return super.getInvalidUseOfRuleMessage() + ": " + this.INVALID_USE_MESSAGE;
        }

        for (int x = cell.getLocation().x - 1; x >= 0 && x < cell.getLocation().x + 1 && x < width - 1; x++) {
            for (int y = cell.getLocation().y - 1; y >= 0 && y < cell.getLocation().y + 1 && y < height - 1; y++) {
                if (nurikabeBoard.getCell(x, y).getType() == NurikabeType.BLACK &&
                        nurikabeBoard.getCell(x + 1, y).getType() == NurikabeType.BLACK &&
                        nurikabeBoard.getCell(x, y + 1).getType() == NurikabeType.BLACK &&
                        nurikabeBoard.getCell(x + 1, y + 1).getType() == NurikabeType.BLACK) {
                    return null;
                }
            }
        }

        return super.getNoContradictionMessage() + ": " + this.NO_CONTRADICTION_MESSAGE;
    }
}
```

### Case Rule(s)
In Nurikabe, there is only one case rule: a cell can be white or black. We implement it by extending
`CaseRule`.
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.CaseBoard;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.CaseRule;
import edu.rpi.legup.model.tree.TreeTransition;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;

import java.util.ArrayList;
import java.util.List;

public class BlackOrWhiteCaseRule extends CaseRule {

    public BlackOrWhiteCaseRule() {
        super("Black or White",
                "Each blank cell is either black or white.",
                "edu/rpi/legup/images/nurikabe/cases/BlackOrWhite.png");
    }

    @Override
    public String checkRuleRaw(TreeTransition transition) {
        List<TreeTransition> childTransitions = transition.getParents().get(0).getChildren();
        if (childTransitions.size() != 2) {
            return super.getInvalidUseOfRuleMessage() + ": This case rule must have 2 children.";
        }

        TreeTransition case1 = childTransitions.get(0);
        TreeTransition case2 = childTransitions.get(1);
        if (case1.getBoard().getModifiedData().size() != 1 ||
                case2.getBoard().getModifiedData().size() != 1) {
            return super.getInvalidUseOfRuleMessage() + ": This case rule must have 1 modified cell for each case.";
        }

        NurikabeCell mod1 = (NurikabeCell) case1.getBoard().getModifiedData().iterator().next();
        NurikabeCell mod2 = (NurikabeCell) case2.getBoard().getModifiedData().iterator().next();
        if (!mod1.getLocation().equals(mod2.getLocation())) {
            return super.getInvalidUseOfRuleMessage() + ": This case rule must modify the same cell for each case.";
        }

        if (!((mod1.getType() == NurikabeType.WHITE && mod2.getType() == NurikabeType.BLACK) ||
                (mod2.getType() == NurikabeType.WHITE && mod1.getType() == NurikabeType.BLACK))) {
            return super.getInvalidUseOfRuleMessage() + ": This case rule must an empty white and black cell.";
        }

        return null;
    }

    @Override
    public CaseBoard getCaseBoard(Board board) {
        NurikabeBoard nurikabeBoard = (NurikabeBoard) board.copy();
        CaseBoard caseBoard = new CaseBoard(nurikabeBoard, this);
        nurikabeBoard.setModifiable(false);
        for (PuzzleElement element : nurikabeBoard.getPuzzleElements()) {
            if (((NurikabeCell) element).getType() == NurikabeType.UNKNOWN) {
                caseBoard.addPickableElement(element);
            }
        }
        return caseBoard;
    }

    @Override
    public ArrayList<Board> getCases(Board board, PuzzleElement puzzleElement) {
        ArrayList<Board> cases = new ArrayList<>();
        Board case1 = board.copy();
        PuzzleElement data1 = case1.getPuzzleElement(puzzleElement);
        data1.setData(NurikabeType.WHITE.toValue());
        case1.addModifiedData(data1);
        cases.add(case1);

        Board case2 = board.copy();
        PuzzleElement data2 = case2.getPuzzleElement(puzzleElement);
        data2.setData(NurikabeType.BLACK.toValue());
        case2.addModifiedData(data2);
        cases.add(case2);

        return cases;
    }

    @Override
    public String checkRuleRawAt(TreeTransition transition, PuzzleElement puzzleElement) {
        return null;
    }
}
```
Although the rule itself is simpler than many of the contradiction rules, its implementation is
complex since (1) the proof tree must be split into two branches and (2) the board must enter a
special state in which the user can select the cell to which the rule should be applied.

In general, for case rules, we have to implement four methods: `checkRuleRaw()`, `checkRuleRawAt()`,
`getCaseBoard()`, and `getCases()`. The first two make much more sense in the context of basic
and contradiction rules, and for this reason, one or both may just return `null`. In this case,
we use `checkRuleRaw()` to make sure the rule has been applied correctly to the board. The `CaseBoard`
that we use in `getCaseBoard()` is the special-state board from above, and its use is rather simple.
Finally, the `getCases()` method duplicates the board for each branch
of the proof tree, setting the cell to white in one, and black in the other.

### Basic Rule(s)
Many basic rules, for the reason given in the introduction to this section, are simply shortcuts
to avoid branches and contradictions.
We will implement the one basic rule mentioned earlier:
> If a cell is surrounded by white squares, the cell must be white.

In `FillinWhiteBasicRule.java`:
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.BasicRule;
import edu.rpi.legup.model.rules.ContradictionRule;
import edu.rpi.legup.model.tree.TreeNode;
import edu.rpi.legup.model.tree.TreeTransition;
import edu.rpi.legup.puzzle.nurikabe.NurikabeCell;
import edu.rpi.legup.puzzle.nurikabe.NurikabeType;

public class FillinWhiteBasicRule extends BasicRule {

    public FillinWhiteBasicRule() {
        super("Fill In White",
                "If there an unknown region surrounded by white, it must be white.",
                "edu/rpi/legup/images/nurikabe/rules/FillInWhite.png");
    }

    @Override
    public String checkRuleRawAt(TreeTransition transition, PuzzleElement puzzleElement) {
        NurikabeBoard board = (NurikabeBoard) transition.getBoard();
        NurikabeBoard origBoard = (NurikabeBoard) transition.getParents().get(0).getBoard();
        ContradictionRule contraRule = new IsolateBlackContradictionRule();

        NurikabeCell cell = (NurikabeCell) board.getPuzzleElement(puzzleElement);

        if (cell.getType() != NurikabeType.WHITE) {
            return "Only white cells are allowed for this rule!";
        }
        NurikabeBoard modified = (NurikabeBoard) origBoard.copy();
        modified.getPuzzleElement(puzzleElement).setData(NurikabeType.BLACK.toValue());
        if (contraRule.checkContradictionAt(modified, puzzleElement) != null) {
            return "white cells must be placed in a region of white cells!";
        }
        return null;
    }

    @Override
    public Board getDefaultBoard(TreeNode node) {
        return null;
    }
}
```
Most basic rules need only override `checkRawRuleAt()`, which functions similarly to the
`checkContradictionAt()` method we saw earlier. The implementation here demonstrates the principle
above: we use a contradiction rule to implement the corresponding basic rule.

**WARNING:** `checkRawRuleAt()` should never reference the parameter `transition` or its respective `board` in `checkContradictionAt`. Doing so will likely cause self-validation issues. 

*Note.* `BasicRule` also requires you to implement `getDefaultBoard()`, which is a method used for
default-rule applications. This feature is, however, experimental, and it is not implemented in
many puzzles.

Now that we have completed all the necessary rules, we can finally revisit our `Nurikabe` class,
and finish one of the methods.
```java
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.model.rules.ContradictionRule;

@Override
public boolean isBoardComplete(Board board) {
    NurikabeBoard nurikabeBoard = (NurikabeBoard) board;

    for (ContradictionRule rule : contradictionRules) {
        if (rule.checkContradiction(nurikabeBoard) == null) {
            return false;
        }
    }
    for (PuzzleElement data : nurikabeBoard.getPuzzleElements()) {
        NurikabeCell cell = (NurikabeCell) data;
        if (cell.getType() == NurikabeType.UNKNOWN) {
            return false;
        }
    }
    return true;
}
```
To check for board completion, we make sure that all cells are filled, and that there
are no contradictions. The `contradictionRules` variable is set automatically by
the superclass, which detects any `ContradictionRule` subclasses found within the package.

## GUI
Our Nurikabe implementation is not of much use if there is no graphical interface!
LEGUP follows the model-view-controller architecture, and we just finished creating
our model; now we need a view and a controller to interact with it. We begin by
creating a view for each cell, which we will then aggregate into a larger view for
the entire board.

*Note.* Much of the following code makes heavy use of the Java AWT library, which is outside
the purview of this guide. There is, though, no shortage of examples online and within LEGUP
for its usage, to which we direct the reader.

LEGUP comes with two classes which will be especially useful here: `edu.rpi.legup.ui.boardview.GridElementView`
and `edu.rpi.legup.ui.boardview.GridBoardView`. We will extend these classes for Nurikabe.
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.ui.boardview.GridElementView;

import java.awt.*;

public class NurikabeElementView extends GridElementView {

    private static final Font FONT = new Font("TimesRoman", Font.BOLD, 16);
    private static final Color FONT_COLOR = Color.BLACK;

    public NurikabeElementView(NurikabeCell cell) {
        super(cell);
    }

    @Override
    public NurikabeCell getPuzzleElement() {
        return (NurikabeCell) super.getPuzzleElement();
    }

    @Override
    public void drawElement(Graphics2D graphics2D) {
        NurikabeCell cell = (NurikabeCell) puzzleElement;
        NurikabeType type = cell.getType();
        if (type == NurikabeType.NUMBER) {
            graphics2D.setStroke(new BasicStroke(1));
            graphics2D.setColor(Color.WHITE);
            graphics2D.fillRect(location.x, location.y, size.width, size.height);

            graphics2D.setColor(Color.BLACK);
            graphics2D.drawRect(location.x, location.y, size.width, size.height);

            graphics2D.setColor(FONT_COLOR);
            graphics2D.setFont(FONT);
            FontMetrics metrics = graphics2D.getFontMetrics(FONT);
            String value = String.valueOf(puzzleElement.getData());
            int xText = location.x + (size.width - metrics.stringWidth(value)) / 2;
            int yText = location.y + ((size.height - metrics.getHeight()) / 2) + metrics.getAscent();
            graphics2D.drawString(String.valueOf(puzzleElement.getData()), xText, yText);
        } else if (type == NurikabeType.BLACK) {
            graphics2D.setStroke(new BasicStroke(1));
            graphics2D.setColor(Color.BLACK);
            graphics2D.fillRect(location.x, location.y, size.width, size.height);
        } else if (type == NurikabeType.WHITE) {
            graphics2D.setStroke(new BasicStroke(1));
            graphics2D.setColor(Color.WHITE);
            graphics2D.fillRect(location.x, location.y, size.width, size.height);
            graphics2D.setColor(Color.BLACK);
            graphics2D.drawRect(location.x, location.y, size.width, size.height);
        } else if (type == NurikabeType.UNKNOWN) {
            graphics2D.setStroke(new BasicStroke(1));
            graphics2D.setColor(Color.LIGHT_GRAY);
            graphics2D.fillRect(location.x, location.y, size.width, size.height);
            graphics2D.setColor(Color.BLACK);
            graphics2D.drawRect(location.x, location.y, size.width, size.height);
        }
    }
}
```
Any subclass of `GridElementView` must override `getPuzzleElement()` and return the corresponding
`PuzzleElement`, and override `drawElement()`, where it can draw the cell appropriately.

Now, we implement the general `NurikabeView`:
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.controller.BoardController;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.ui.boardview.GridBoardView;

import java.awt.*;

public class NurikabeView extends GridBoardView {

    public NurikabeView(NurikabeBoard board) {
        super(new BoardController(), new NurikabeController(), board.getDimension());

        for (PuzzleElement puzzleElement : board.getPuzzleElements()) {
            NurikabeCell cell = (NurikabeCell) puzzleElement;
            Point loc = cell.getLocation();
            NurikabeElementView elementView = new NurikabeElementView(cell);
            elementView.setIndex(cell.getIndex());
            elementView.setSize(elementSize);
            elementView.setLocation(new Point(loc.x * elementSize.width, loc.y * elementSize.height));
            elementViews.add(elementView);
        }
    }
}
```
All we have to do in this subclass is get every `PuzzleElement` from the board, create their views,
and position them relatively within this larger view. Notice that the superclass requires a controller
for the puzzle, which handles user interaction with the board. Next, the `NurikabeController`:
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.controller.ElementController;
import edu.rpi.legup.model.gameboard.PuzzleElement;

import java.awt.event.MouseEvent;

public class NurikabeController extends ElementController {

    @Override
    public void changeCell(MouseEvent e, PuzzleElement data) {
        NurikabeCell cell = (NurikabeCell) data;
        if (e.getButton() == MouseEvent.BUTTON1) {
            if (e.isControlDown()) {
                this.boardView.getSelectionPopupMenu().show(boardView, this.boardView.getCanvas().getX() + e.getX(), this.boardView.getCanvas().getY() + e.getY());
            } else {
                if (cell.getData() == -2) {
                    data.setData(0);
                } else if (cell.getData() == 0) {
                    data.setData(-1);
                } else {
                    data.setData(-2);
                }
            }
        } else if (e.getButton() == MouseEvent.BUTTON3) {
            if (cell.getData() == -2) {
                data.setData(-1);
            } else if (cell.getData() == 0) {
                data.setData(-2);
            } else {
                data.setData(0);
            }
        }
    }
}
```
This class simply defines what happens to a given cell on the board when it is clicked. For Nurikabe,
we just cycle between the cell types (excluding numbered, of course).

And we are done! Now we just register our `NurikabeView` in the `Nurikabe` class:
```java
@Override
public void initializeView() {
    boardView = new NurikabeView((NurikabeBoard) currentBoard);
    addBoardListener(boardView);
}
```

## Puzzle Files, Importing, and Exporting
The final stage in adding our puzzle to LEGUP is specifying how we will
store these puzzles in files, and import/export them. Puzzles in LEGUP are stored as XML
files, and we specify the precise rules in our importer. Here is an example of a basic Nurikabe
file:
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Legup version="2.0.0">
    <puzzle name="Nurikabe">
        <board height="5" width="5">
            <cells>
                <cell value="4" x="4" y="0"/>
                <cell value="1" x="0" y="2"/>
                <cell value="1" x="2" y="2"/>
                <cell value="1" x="4" y="2"/>
                <cell value="4" x="0" y="4"/>
            </cells>
        </board>
    </puzzle>
</Legup>
```
To read these files, we extend the `edu.rpi.legup.model.PuzzleImporter` class, and override
the `initializeBoard()` method.
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.model.PuzzleImporter;
import edu.rpi.legup.save.InvalidFileFormatException;
import org.w3c.dom.Element;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;

import java.awt.*;

public class NurikabeImporter extends PuzzleImporter {
    public NurikabeImporter(Nurikabe nurikabe) {
        super(nurikabe);
    }

    @Override
    public void initializeBoard(Node node) throws InvalidFileFormatException {
        try {
            if (!node.getNodeName().equalsIgnoreCase("board")) {
                throw new InvalidFileFormatException("nurikabe Importer: cannot find board puzzleElement");
            }
            Element boardElement = (Element) node;
            if (boardElement.getElementsByTagName("cells").getLength() == 0) {
                throw new InvalidFileFormatException("nurikabe Importer: no puzzleElement found for board");
            }
            Element dataElement = (Element) boardElement.getElementsByTagName("cells").item(0);
            NodeList elementDataList = dataElement.getElementsByTagName("cell");

            NurikabeBoard nurikabeBoard = null;
            if (!boardElement.getAttribute("size").isEmpty()) {
                int size = Integer.valueOf(boardElement.getAttribute("size"));
                nurikabeBoard = new NurikabeBoard(size);
            } else if (!boardElement.getAttribute("width").isEmpty() && !boardElement.getAttribute("height").isEmpty()) {
                int width = Integer.valueOf(boardElement.getAttribute("width"));
                int height = Integer.valueOf(boardElement.getAttribute("height"));
                nurikabeBoard = new NurikabeBoard(width, height);
            }

            if (nurikabeBoard == null) {
                throw new InvalidFileFormatException("nurikabe Importer: invalid board dimensions");
            }

            int width = nurikabeBoard.getWidth();
            int height = nurikabeBoard.getHeight();

            for (int i = 0; i < elementDataList.getLength(); i++) {
                NurikabeCell cell = (NurikabeCell) puzzle.getFactory().importCell(elementDataList.item(i), nurikabeBoard);
                Point loc = cell.getLocation();
                if (cell.getData() != NurikabeType.UNKNOWN.toValue()) {
                    cell.setModifiable(false);
                    cell.setGiven(true);
                }
                nurikabeBoard.setCell(loc.x, loc.y, cell);
            }

            for (int y = 0; y < height; y++) {
                for (int x = 0; x < width; x++) {
                    if (nurikabeBoard.getCell(x, y) == null) {
                        NurikabeCell cell = new NurikabeCell(NurikabeType.UNKNOWN.toValue(), new Point(x, y));
                        cell.setIndex(y * height + x);
                        cell.setModifiable(true);
                        nurikabeBoard.setCell(x, y, cell);
                    }
                }
            }
            puzzle.setCurrentBoard(nurikabeBoard);
        } catch (NumberFormatException e) {
            throw new InvalidFileFormatException("nurikabe Importer: unknown value where integer expected");
        }
    }
}
```
LEGUP also supports saving partially complete proofs, and we extend `PuzzleExporter` to save the
current state of the board.
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.model.PuzzleExporter;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import org.w3c.dom.Document;

public class NurikabeExporter extends PuzzleExporter {

    public NurikabeExporter(Nurikabe nurikabe) {
        super(nurikabe);
    }

    @Override
    protected org.w3c.dom.Element createBoardElement(Document newDocument) {
        NurikabeBoard board = (NurikabeBoard) puzzle.getTree().getRootNode().getBoard();

        org.w3c.dom.Element boardElement = newDocument.createElement("board");
        boardElement.setAttribute("width", String.valueOf(board.getWidth()));
        boardElement.setAttribute("height", String.valueOf(board.getHeight()));

        org.w3c.dom.Element cellsElement = newDocument.createElement("cells");
        for (PuzzleElement puzzleElement : board.getPuzzleElements()) {
            NurikabeCell cell = (NurikabeCell) puzzleElement;
            if (cell.getData() != -2) {
                org.w3c.dom.Element cellElement = puzzle.getFactory().exportCell(newDocument, puzzleElement);
                cellsElement.appendChild(cellElement);
            }
        }

        boardElement.appendChild(cellsElement);
        return boardElement;
    }
}
```
In both of the above classes we make use of a helper class to create `NurikabeCell`s from XML data,
and to export `NurikabeCell`s to XML data through the `Puzzle.getFactory()` method.
The `NurikabeCellFactory` is written as follows:
```java
package edu.rpi.legup.puzzle.nurikabe;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.ElementFactory;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpi.legup.save.InvalidFileFormatException;
import org.w3c.dom.Document;
import org.w3c.dom.NamedNodeMap;
import org.w3c.dom.Node;

import java.awt.*;

public class NurikabeCellFactory extends ElementFactory {
    @Override
    public NurikabeCell importCell(Node node, Board board) throws InvalidFileFormatException {
        try {
            if (!node.getNodeName().equalsIgnoreCase("cell")) {
                throw new InvalidFileFormatException("nurikabe Factory: unknown puzzleElement puzzleElement");
            }

            NurikabeBoard nurikabeBoard = (NurikabeBoard) board;
            int width = nurikabeBoard.getWidth();
            int height = nurikabeBoard.getHeight();

            NamedNodeMap attributeList = node.getAttributes();
            int value = Integer.valueOf(attributeList.getNamedItem("value").getNodeValue());
            int x = Integer.valueOf(attributeList.getNamedItem("x").getNodeValue());
            int y = Integer.valueOf(attributeList.getNamedItem("y").getNodeValue());
            if (x >= width || y >= height) {
                throw new InvalidFileFormatException("nurikabe Factory: cell location out of bounds");
            }
            if (value < -2) {
                throw new InvalidFileFormatException("nurikabe Factory: cell unknown value");
            }

            NurikabeCell cell = new NurikabeCell(value, new Point(x, y));
            cell.setIndex(y * height + x);
            return cell;
        } catch (NumberFormatException e) {
            throw new InvalidFileFormatException("nurikabe Factory: unknown value where integer expected");
        } catch (NullPointerException e) {
            throw new InvalidFileFormatException("nurikabe Factory: could not find attribute(s)");
        }
    }

    public org.w3c.dom.Element exportCell(Document document, PuzzleElement puzzleElement) {
        org.w3c.dom.Element cellElement = document.createElement("cell");

        NurikabeCell cell = (NurikabeCell) puzzleElement;
        Point loc = cell.getLocation();

        cellElement.setAttribute("value", String.valueOf(cell.getData()));
        cellElement.setAttribute("x", String.valueOf(loc.x));
        cellElement.setAttribute("y", String.valueOf(loc.y));

        return cellElement;
    }
}
```

We can finish the `Nurikabe` class!
```java
public Nurikabe() {
    super();

    this.name = "Nurikabe";

    this.importer = new NurikabeImporter(this);
    this.exporter = new NurikabeExporter(this);

    this.factory = new NurikabeCellFactory();
}
```

Finally, we need to add the new puzzle to LEGUP's list, so that it recognizes the files.
In `src/main/resources/edu/rpi/legup/legup` in the file `config`, we add the line
```xml
<puzzle name="Nurikabe" qualifiedClassName="edu.rpi.legup.puzzle.nurikabe.Nurikabe" fileType=".xml"/>
```

Congratulations, you've added a puzzle to LEGUP!

## Next Steps
This tutorial was intended to give a simple overview of the anatomy of a puzzle in LEGUP. For
this reason, certain features were not implemented and comments were removed.
However, this will (hopefully) have given the reader enough information
to be able to read and navigate the source code independently, where the wealth of
examples and comments will help to explain the minutia of puzzles and the application in general.

Interested developers should view the full source code for [Nurikabe](https://github.com/Bram-Hub/Legup/tree/master/src/main/java/edu/rpi/legup/puzzle/nurikabe)
and [other puzzles](https://github.com/Bram-Hub/Legup/tree/master/src/main/java/edu/rpi/legup/puzzle).
Particularly helpful for understanding Legup's backend are the [models](https://github.com/Bram-Hub/Legup/tree/master/src/main/java/edu/rpi/legup/model)
and [controllers](https://github.com/Bram-Hub/Legup/tree/master/src/main/java/edu/rpi/legup/controller),
which are extended by every puzzle.
