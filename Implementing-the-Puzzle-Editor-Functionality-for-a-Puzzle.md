# Enable Puzzle File Creation for your New Puzzle (WIP page and functionality)
1. [Enabling puzzle file creation](#enable-puzzle-file-creation)
2. [Specifying valid board dimensions](#specifying-valid-board-dimensions)
3. [Creating Tiles](#creating-tiles)
4. Initializing an Empty Puzzle (CHOOSE ONE)
    * [From Row and Column Input](#initializing-an-empty-puzzle-from-row-and-column-input)
    * [From Text Input](#initializing-an-empty-puzzle-from-text-input)
5. [Implementing Cell Modification Functionality](#implementing-cell-modification-functionality)

## Enabling Puzzle File Creation
Navigate to `bin/main/edu/rpi/legup/legup/config` and change the corresponding `fileCreationDisabled` parameter to `false`. For example, if we want to enable file creation for Nurikabe, and the configurations file looked like this...
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
...then it should be changed to this:
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

## Creating Tiles
For each puzzle, you will need to create two types of tiles: ones that support placeable elements and ones that support non-placeable elements. A placeable element is any element a user can place down on the board while working in the proof editor. A non-placeable element is any element a user cannot place down on the board while working in the proof editor. For example, in Nurikabe specifically, `BlackTile` and `WhiteTile` will be placeable elements while `NumberTile` will be a non-placeable element.

All tiles must go in the corresponding `elements` folder for the corresponding puzzle (`src/main/java.edu/rpi/legup/puzzle/<PUZZLE_NAME>/elements`). For each tile, the following steps must be completed:
1. The class must inherit from `PlaceableElements` or `NonPlaceableElement`.
2. An ID must be assigned to the tile and specified in the `<PUZZLE_NAME>_elements_reference_sheet.txt` (which should be located at `src/main/java.edu/rpi/legup/puzzle/<PUZZLE_NAME>/elements`).
3. An icon for the tile must be created and stored in the folder located at `edu/rpi/legup/images/<PUZZLE_NAME>/tiles`.
4. A name and description for the tile must be passed into the constructor.

### Example: Creating the `BlackTile` Class
For Nurikabe, we will create the `BlackTile` class in the following folder: `src/main/java.edu/rpi/legup/puzzle/nurikabe/elements`.

Here is what `BlackTile.java` should look like:
```java
package edu.rpi.legup.puzzle.nurikabe.elements;

import edu.rpi.legup.model.elements.PlaceableElement;

public class BlackTile extends PlaceableElement {
    public BlackTile() {
        super("NURI-PLAC-0001", "Black Tile", "The black tile", "edu/rpi/legup/images/nurikabe/tiles/BlackTile.png");
    }
}
```
Note that `BlackTile.png` is an image file containing the icon that will be used for this element.

Next, this is what `nurikabe_elements_reference_sheet.txt` should look like after we created `BlackTile.java`:
```
NURI-PLAC-0001 : BlackTile
```

Note that each puzzle must have a `UnknownTile.java` class, which allows users to clear cells on the board in the puzzle editor. For an example, see `src/main/java.edu/rpi/legup/puzzle/nurikabe/elements/UnknownTile.java`.

## Initializing an Empty Puzzle From Row and Column Input
For this step, all sample code excerpts will use Nurikabe.

First, verify that the puzzle's importer class has `acceptsRowsAndColumnsInput()` return true and `acceptsTextInput()` return false. Change these methods to return the corresponding values if they do not already.

Next, verify that the puzzle's importer class throws an `UnsupportedOperationException` for `initializeBoard(String[] statements)`. To keep all error messages consistent, please have the `UnsupportedOperationException`'s error message read "<PUZZLE_NAME> cannot accept text input".

Finally, we implement `initializeBoard(int rows, int columns)` in the puzzle's importer class to create an empty puzzle board. This can be done by creating a new board object and then adding cells to it in a double for loop.

```java
public class NurikabeImporter extends PuzzleImporter {
    public NurikabeImporter(Nurikabe nurikabe) {
        super(nurikabe);
    }

    @Override
    public boolean acceptsRowsAndColumnsInput() {
        return true;
    }

    @Override
    public boolean acceptsTextInput() {
        return false;
    }

    @Override
    public void initializeBoard(String[] statements) throws UnsupportedOperationException {
        throw new UnsupportedOperationException("Nurikabe cannot accept text input");
    }

    /**
     * Creates an empty board for building
     *
     * @param rows    the number of rows on the board
     * @param columns the number of columns on the board
     * @throws RuntimeException
     */
    @Override
    public void initializeBoard(int rows, int columns) {
        NurikabeBoard nurikabeBoard = new NurikabeBoard(columns, rows);

        for (int y = 0; y < rows; y++) {
            for (int x = 0; x < columns; x++) {
                NurikabeCell cell = new NurikabeCell(NurikabeType.UNKNOWN.toValue(), new Point(x, y));
                cell.setIndex(y * columns + x);
                cell.setModifiable(true);
                nurikabeBoard.setCell(x, y, cell);
            }
        }
        puzzle.setCurrentBoard(nurikabeBoard);
    }

    // Rest of implementation not shown
}
```

## Initializing an Empty Puzzle From Text Input
***For most puzzles, you will never need to and should not implement this functionality.*** This functionality was created as a result of needing a more intuitive way for users to create Short Truth Table puzzle files. Short Truth Table puzzles are special, as it is not intuitive for the user to create a puzzle file by entering row and column values. Current implementation only allows puzzles to support either row and column input or text input. If you determine that your puzzle would work better with text input rather than row and column input, then continue on with this section. Otherwise, skip to the next section.

General note regarding text input: all input will be broken up by new lines. If you want a different way to break up the text input, further modification to the code will be necessary. These modifications will not be covered in this tutorial.

For this step, all sample code excerpts will use Short Truth Table.

### Setting Proper Defaults
First, verify that the puzzle's importer class has `acceptsRowsAndColumnsInput()` return false and `acceptsTextInput()` return true. Change these methods to return the corresponding values if they do not already.

Next, verify that the puzzle's importer class throws an `UnsupportedOperationException` for `initializeBoard(int rows, int columns)`. To keep all error messages consistent, please have the `UnsupportedOperationException`'s error message read "<PUZZLE_NAME> cannot accept row and column input".

```java
public class ShortTruthTableImporter extends PuzzleImporter {
    public ShortTruthTableImporter(ShortTruthTable stt) {
        super(stt);
    }

    @Override
    public boolean acceptsRowsAndColumnsInput() {
        return false;
    }

    @Override
    public boolean acceptsTextInput() {
        return true;
    }

    @Override
    public void initializeBoard(int rows, int columns) {
        throw new UnsupportedOperationException("Short Truth Table cannot accept row and column input");
    }

    // Rest of implementation not shown
}
```

### Checking for Valid Statements
`GameBoardFacade`'s `validateTextInput(String game, String[] statements)` method validates text input by calling a puzzle's `isValidTextInput(String[] statements)` method. By default in `Puzzle.java`, `isValidTextInput(String[] statements)` returns true if there are more than 0 statements:
```java
public abstract class Puzzle implements IBoardSubject, ITreeSubject {
    public boolean isValidTextInput(String[] statements) {
        return statements.length > 0;
    }

    // Rest of implementation not shown
}
```
However, this may not always be sufficient. In your puzzle's class, you can override this method to include stricter checks. An example from `ShortTruthTable.java` is shown below. Note that you will not be able to reuse this code, as the `validGrammar` method is Short Truth Table-specific. Look around at your puzzle's methods to see if a similar method has already been implemented.
```java
public class ShortTruthTable extends Puzzle {
    /**
     * Determines if the given statements are valid for Short Truth Table
     *
     * @param statements
     * @return true if the statements are valid for Short Truth Table, false otherwise
     */
    public boolean isValidTextInput(String[] statements) {
        if (statements.length == 0)
            return false;

        ShortTruthTableImporter importer = (ShortTruthTableImporter) this.getImporter();
        for (String s : statements)
            if (!importer.validGrammar(s))
                return false;
        return true;
    }

    // Rest of implementation not shown
}
```

### Accepting Text Input on the Create Puzzle Dialog
First, you will need to modify the action performed by `gameBoxListener` when the puzzle is selected. Add your puzzle to the if statement checking to see if `puzzleName` equals your puzzle.

```java
private ActionListener gameBoxListener = new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        JComboBox comboBox = (JComboBox) e.getSource();
        String puzzleName = (String) comboBox.getSelectedItem();
        if (puzzleName.equals("ShortTruthTable")) {
            // Show text input area (implementation not shown)
        }
        else {
            // Show row and column input area (implementation not shown)
        }
    }
};
```
Note this also will need to be changed in the `CreatePuzzleDialog` constructor. This makes sure that the dialog shows the correct input when it is initially opened.
```java
public class CreatePuzzleDialog extends JDialog {

    // Implementation not shown

    public CreatePuzzleDialog(JFrame parent, HomePanel homePanel) {
        super(parent, true);

        // Rest of implementation not shown

        if (Objects.equals(this.gameBox.getSelectedItem(), "ShortTruthTable")) {
            // Show text input area (implementation not shown)
        }
        else {
            // Show row and column input area (implementation not shown)
        }

        // Rest of implementation not shown
    }

    // Rest of implementation not shown
}
```
Finally, modify the `okButtonListener` so that it checks if the field is unfilled if the current selected puzzle is the puzzle accepting text dialog. Also modify the action event so that `homePanel` opens the puzzle with the text input.
``` java
private ActionListener okButtonListener = new ActionListener() {
    /**
     * Attempts to open the puzzle editor interface for the given game with the given dimensions
     * @param ae the event to be processed
     */
    @Override
    public void actionPerformed(ActionEvent ae) {
        String game = Config.convertDisplayNameToClassName((String) gameBox.getSelectedItem());

        // Check if all 3 TextFields are filled
        if (game.equals("ShortTruthTable") && textArea.getText().equals("")) {
            System.out.println("Unfilled fields");
            return;
        }
        if (!game.equals("ShortTruthTable") && (game.equals("") || rows.getText().equals("") || columns.getText().equals(""))) {
            // Game does not accept text input (implementation is not shown)
        }

        try {
            if (game.equals("ShortTruthTable")) {
                homePanel.openEditorWithNewPuzzle("ShortTruthTable", textArea.getText().split("\n"));
            }
            else {
                // Open edit with row and column input (implementation not shown)
            }
            setVisible(false);
        }
        catch (IllegalArgumentException e) {
            System.out.println("Failed to open editor with new puzzle");
            e.printStackTrace(System.out);
        }
    }
};
```

### Initializing an Empty Board
The last thing that needs to be done is implementing `initializeBoard(String[] statementInput)` in the puzzle's importer class. This is puzzle-specific. An example with Short Truth Table is shown below. Note that you will not be able to reuse this code, as the code is Short Truth Table-specific. If you are unsure where to begin, consider looking at the importer's `initializeBoard(Node node)` method for ideas.

```java
class ShortTruthTableImporter extends PuzzleImporter {

    public ShortTruthTableImporter(ShortTruthTable stt) {
        super(stt);
    }

    // Rest of implementation not shown

    /**
     * Creates the board for building using statements
     *
     * @param statementInput
     * @throws UnsupportedOperationException
     * @throws IllegalArgumentException
     */
    public void initializeBoard(String[] statementInput) throws UnsupportedOperationException, IllegalArgumentException {
        List<String> statementsList = new LinkedList<>();
        for (String s : statementInput) {
            if (s.strip().length() > 0) {
                statementsList.add(s);
            }
        }
        String[] statementData = statementsList.toArray(new String[statementsList.size()]);

        if (statementData.length == 0) {
            throw new IllegalArgumentException("short truth table Importer: no statements found for board");
        }

        // Store all cells and statements
        List<List<ShortTruthTableCell>> allCells = new ArrayList<>();
        List<ShortTruthTableStatement> statements = new ArrayList<>();

        // Parse the data
        int maxStatementLength = parseAllStatementsAndCells(statementData, allCells, statements);

        // Generate and set the board - don't set given cell values since none are given
        ShortTruthTableBoard sttBoard = generateBoard(allCells, statements, maxStatementLength);
        puzzle.setCurrentBoard(sttBoard);
    }
}
```

## Implementing Cell Modification Functionality
In the puzzle's cell class, you will need to implement `setType(Element e, MouseEvent m)`. You should use `getElementByID()` when you are referencing an element.
```java
public class NurikabeCell extends GridCell<Integer> {
/**
     * Sets the type of this NurikabeCell
     *
     * @param e element to set the type of this nurikabe cell to
     */
    @Override
    public void setType(Element e, MouseEvent m) {
        if (e.getElementName().equals("Black Tile")) {
            this.data = -1;
        }
        else {
            if (e.getElementName().equals("White Tile")) {
                this.data = 0;
            }
            else {
                if (e.getElementName().equals("Number Tile")) {
                    if (m.getButton() == MouseEvent.BUTTON1) {
                        if (this.data <= 0 || this.data > 8) {
                            this.data = 1;
                        }
                        else {
                            this.data = this.data + 1;
                        }
                    }
                    else {
                        if (m.getButton() == MouseEvent.BUTTON3) {
                            if (this.data > 1) {
                                this.data = this.data - 1;
                            }
                            else {
                                this.data = 9;
                            }
                        }
                    }
                }
                else { // unknown tile
                    this.data = -2;
                }
            }
        }
    }

    // Rest of implementation not shown
}
```

# End of Tutorial
Congratulations! You now know the basics for how to implement puzzle editor functionality for a puzzle!