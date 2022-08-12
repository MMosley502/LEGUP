For this tutorial, we will be demonstrating how to implement a puzzle in order to allow proofs of your puzzle to be solved. We will be implementing Nurikabe as an example in this tutorial.

# Implementing a New Puzzle
This page aims to be a straightforward guide for developers in creating a new puzzle for Legup.
In this example, we will create <a href="https://en.wikipedia.org/wiki/Nurikabe_(puzzle)">Nurikabe</a>,
a simple puzzle game played on a rectangular grid.
## Organization and Classes
We begin by creating a new directory under `src/main/java/edu/rpi/legup/puzzle` called `nurikabe`.
Every puzzle in Legup extends the abstract class `edu.rpu.legup.model.Puzzle`. The constructor and
the following abstract methods must be implemented:
* `public void initializeView()`
* `public Board generatePuzzle(int difficulty)`
* `public boolean isBoardComplete(Board board)`
* `public void onBoardChange(Board board)`

Although all of these methods need to be overridden, not all of them need to do something. For example,
puzzle generation is not a feature required for every puzzle, so this method may do nothing. Also, there
may be no need to do anything on board change. With all of this known, we can create a basic `Nurikabe`

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
with a few helper methods to be overridden by subclasses. Nurikabe is a grid-based puzzle, so we can use
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
}
```
## Adding Rules
Legup allows a user to find a solution by applying simple axioms, or rules. There are
three types of rules in Legup: basic, case, and contradiction. Basic rules represent a
logical continuation of the puzzle solution; case rules represent two possible paths on
which the solution may go, and create a branch in the proof tree; contradiction rules
show that a contradiction with the rules of the puzzle have been derived.

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

All rules go into a subpackage called `rules`. We divide the first rule into two&mdash;
the first having no numbers, the second having more than one[^1].
```java
package edu.rpi.legup.puzzle.nurikabe.rules;

import edu.rpi.legup.model.gameboard.Board;
import edu.rpi.legup.model.gameboard.GridBoard;
import edu.rpi.legup.model.gameboard.PuzzleElement;
import edu.rpu.legup.model.rules.ContradictionRule;
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
        GridBoard<Integer> nurikabeBoard = (GridBoard<Integer>) board;

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
## GUI
Our Nurikabe implementation is not of much use if there is no graphical interface!
## Puzzle Files, Importing, and Exporting

[^1]: *Note.* To ease implementing the rules, we use a few utilities defined in the `NurikabeUtilities` class,
  which the reader can find along with the other Nurikabe files in the main repository. Implementing these
  features is outside the scope of this tutorial.

[//]: --------------------------------------------------------------------------------------------------------------------------------------------------

# Enable Puzzle File Creation for your New Puzzle
1. [Temporarily disabling puzzle file creation](#temporarily-disabling-puzzle-file-creation)
2. [Specifying valid board dimensions](#specifying-valid-board-dimensions)


## Temporarily Disabling Puzzle File Creation
We will disable puzzle file creation for your new puzzle temporarily. This will allow us to work on the puzzle file creation functionality while preventing users within Legup from accidentally accessing this in-progress functionality.

Navigate to `bin/main/edu/rpi/legup/legup/config` and add the following under the last puzzle:

```xml
<puzzle name="Nurikabe"
            qualifiedClassName="edu.rpi.legup.puzzle.nurikabe.Nurikabe"
            fileType=".xml"
            fileCreationDisabled="false"/>
```
So, for example, if `config` looked like this previously...

```xml
<Legup version="3.0">
    <puzzles>
        <puzzle name="Battleship"
            qualifiedClassName="edu.rpi.legup.puzzle.battleship.Battleship"
            fileType=".xml"
            fileCreationDisabled="true"/>
        <puzzle name="TreeTent"
            qualifiedClassName="edu.rpi.legup.puzzle.treetent.TreeTent"
            fileType=".xml"
            fileCreationDisabled="true"/>
    </puzzles>
</Legup>
```
...it should now look like this:

```xml
<Legup version="3.0">
    <puzzles>
        <puzzle name="Battleship"
            qualifiedClassName="edu.rpi.legup.puzzle.battleship.Battleship"
            fileType=".xml"
            fileCreationDisabled="true"/>
        <puzzle name="TreeTent"
            qualifiedClassName="edu.rpi.legup.puzzle.treetent.TreeTent"
            fileType=".xml"
            fileCreationDisabled="false"/>
        <puzzle name="Nurikabe"
            qualifiedClassName="edu.rpi.legup.puzzle.nurikabe.Nurikabe"
            fileType=".xml"
            fileCreationDisabled="true"/>
    </puzzles>
</Legup>
```
`qualifiedClassName` is the name of the class of the puzzle, `fileType` is the file format of the puzzle file, and `fileCreationDisabled` specifies whether or not you want to disable file creation for the puzzle. `fileType` should, for the most part, always be `.xml`.

## Specifying Valid Board Dimensions
In the `Puzzle` class (found at `src/main/java/edu/rpi/legup/model/Puzzle.java`), we find the following method:

```java
/**
 * Checks if the given height and width are valid board dimensions for the given puzzle
 *
 * @param rows    the number of rows on the board
 * @param columns the number of columns on the board
 * @return true if the given dimensions are valid for the given puzzle, false otherwise
 */
 public boolean isValidDimensions(int rows, int columns) {
     return rows > 0 && columns > 0;
 }
```
This, by default, makes any m by n board valid, where m and n are positive integers. 

However, we want to set our own custom validator for Nurikabe. Nurikabe only allows m by n boards where m and n are at least 2. In order to implement this and override the `Puzzle` class' method, we navigate to the `Nurikabe` class (found at `src/main/java/edu/rpi/legup/puzzle/nurikabe/Nurikabe.java`) and add the following method:

```java
@Override
/**
 * Determines if the given dimensions are valid for Nurikabe
 *
 * @param rows      the number of rows
 * @param columns   the number of columns
 * @return true if the given dimensions are valid for Nurikabe, false otherwise
 */
public boolean isValidDimensions(int rows, int columns) {
    return rows >= 2 && columns >= 2;
}
```

......More steps in between......

## Enabling Puzzle File Creation
Now, you are ready to enable the puzzle file creation! Navigate back to `bin/main/edu/rpi/legup/legup/config` and change the corresponding `fileCreationDisabled` parameter to `false`.

```xml
<Legup version="3.0">
    <puzzles>
        <puzzle name="Battleship"
            qualifiedClassName="edu.rpi.legup.puzzle.battleship.Battleship"
            fileType=".xml"
            fileCreationDisabled="true"/>
        <puzzle name="TreeTent"
            qualifiedClassName="edu.rpi.legup.puzzle.treetent.TreeTent"
            fileType=".xml"
            fileCreationDisabled="false"/>
        <puzzle name="Nurikabe"
            qualifiedClassName="edu.rpi.legup.puzzle.nurikabe.Nurikabe"
            fileType=".xml"
            fileCreationDisabled="false"/>
    </puzzles>
</Legup>
```

# End of Tutorial
Congratulations! You now know the basics for how to implement a new puzzle in Legup and how to set up file creation for that new puzzle within Legup.