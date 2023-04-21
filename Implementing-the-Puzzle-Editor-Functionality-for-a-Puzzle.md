# Enable Puzzle File Creation for your New Puzzle (WIP page and functionality)
1. [Temporarily disabling puzzle file creation](#temporarily-disabling-puzzle-file-creation)
2. [Specifying valid board dimensions](#specifying-valid-board-dimensions)
3. [Creating Tiles](#creating-tiles)
4. [Initializing an Empty Puzzle From Row and Column Input](#initializing-an-empty-puzzle-from-row-and-column-input)
5. [Initializing an Empty Puzzle From Text Input](#initializing-an-empty-puzzle-from-text-input)

## Temporarily Disabling Puzzle File Creation
We will disable puzzle file creation for your new puzzle temporarily. This will allow us to work on the puzzle file creation functionality while preventing users within LEGUP from accidentally accessing this in-progress functionality.

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
***For most puzzles, you will never need to and should not implement this functionality.*** This functionality was created as a result of needing a more intuitive way for users to create Short Truth Table puzzle files. Short Truth Table puzzles are special, as it is not intuitive for the user to create a puzzle file by entering row and column values. Most puzzles will only need to be initialized with a row and column input. Current implementation only allows puzzles to support either row and column input or text input. If you determine that your puzzle would work better with text input rather than row and column input, then continue on with this section. Otherwise, skip to the next section.

TODO:
-
If the puzzle only accepts row and column input:
- In the puzzle importer's class (e.g. `NurikabeImporter.java`):
    - Make sure that `initializeBoard(String[] statements)` immediately throws an UnsupportedOperationException
    - Implement `initializeBoard(int rows, int columns)` to create an empty puzzle board (add NurikabeImporter example)
    - Make sure `acceptsRowsAndColumnsInput()` returns true and `acceptsTextInput()` returns false

If the puzzle only accepts text input:
- In the puzzle importer's class (e.g. `ShortTruthTable.java`)
    - Make sure that `initializeBoard(int rows, int columns)` immediately throws an UnsupportedOperationException
    - Implement `initializeBoard(String[] statementInput)` however is fit for the puzzle
    - Make sure `acceptsTextInput()` returns true and `acceptsRowsAndColumnsInput()` returns false
    - Implement `isValidTextInput(String[] statements)` in the puzzle class (e.g. `ShortTruthTable.java`) if the default behavior in `Puzzle.java` is not sufficient

- Create a new method `setType()` in the puzzle class (e.g. `Nurikabe.java`, `ShortTruthTable.java`) that deals with how to handle these element IDs

- There may also be other incompatibilities that should be easy to track down through errors that tell you something is null. This is usually caused by the puzzle editor not creating all the proof editor stuff (like the proof tree) from the proof solver.

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
Congratulations! You now know the basics for how to implement puzzle editor functionality for a puzzle!