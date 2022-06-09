## Gradle

This project uses Gradle for dependency management.

## XML Board Specifications

An example for the Battleship `edu.rpi.legup.puzzle` demonstrates the proper format for XML files to be read in. Puzzles have particular `x` and `y` values associated with a location of each `puzzleElement`. The board size dictates the square size of the board. Legup supports many puzzles, such as Light Up, Nurikabe, Short Truth Table, etc., with others such as Battleship, Skyscrapers, and Tree Tent actively in development.

```
<edu.rpi.legup.Legup>
    <edu.rpi.legup.puzzle qualifiedClassName="edu.rpi.legup.puzzle.battleship.BattleShip">
        <board size="10">
            <puzzleElement>
                <puzzleElement value="1" x="2" y="0"/>
                <puzzleElement value="1" x="6" y="0"/>
                <puzzleElement value="2" x="1" y="1"/>
                <puzzleElement value="-1" x="8" y="1"/>
                <puzzleElement value="-1" x="2" y="2"/>
            </puzzleElement>
        </board>
    </edu.rpi.legup.puzzle>
</edu.rpi.legup.Legup>
```
Element values are dependent on the type of `edu.rpi.legup.puzzle`. This is specified in each `edu.rpi.legup.puzzle`'s documentation.