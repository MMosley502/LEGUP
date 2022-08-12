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
