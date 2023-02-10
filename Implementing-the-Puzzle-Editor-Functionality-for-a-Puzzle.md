# Enable Puzzle File Creation for your New Puzzle (WIP page and functionality)
1. [Temporarily disabling puzzle file creation](#temporarily-disabling-puzzle-file-creation)
2. [Specifying valid board dimensions](#specifying-valid-board-dimensions)


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

......More steps in between......

To support a new puzzle:
- make the tile "Element" classes for that puzzle (`NonPlaceableElements` and `PlaceableElements`)
- These files will go in the `elements` folder of their specified game `src/main/java.edu/rpi/legup/puzzle/gamename(eg: Nurikabe)`
- Base these classes off of the ones from Nurikabe and Tree Tent if you need help
- Make sure they inherit from `NonPlaceableElement` if the element is non-placeable, and from `PlaceableElements` if its placeable (this differs game to game)
- Change the fields passed in to the constructor to describe the puzzle element
- These should get the buttons with the selected images to appear when you open a puzzle Of that type in the editor
- You will also have to change the mouse event methods in the classes `src/main/java.edu/rpi/legup/puzzle/gamename(eg. Nurikabe)`
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