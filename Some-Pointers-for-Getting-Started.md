**Note: if you are reading this and have not followed the [developer setup guide](https://github.com/Bram-Hub/Legup/wiki/Programming-Setup-Guide) yet, please do that first.**

The Legup repository can be daunting at first glance. Here is some general starting information as well as some basics on how to navigate the repository:

## Puzzle Status
### Fully Functioning
These are the puzzles that are fully functioning. If you are new to Legup and want to get used to the software, you should first take a look at these puzzles:
* Light Up
* Nurikabe
* Short Truth Table

### Actively In Development
These are the puzzles that are currently actively being developed for Legup. They are at various points in development. 
#### Significantly through development
* Tree Tent
#### Just started
* Battleship

While you can use these puzzles to get acquainted with the software, expect there to be bugs (documenting these bugs would be greatly appreciated).

### Not Currently In Development
These are the puzzles that are not actively being developed for Legup. They are at various points in development. 
* Fillapix
* Hey Awake
* Masyu
* Skyscrapers
* Sudoku

While you can use these puzzles to get acquainted with the software, expect there to be bugs (documenting these bugs would be greatly appreciated). However, since they are not actively being worked on, work on these bugs will not be prioritized by the Legup development team. Please feel free to contribute any bug fixes yourself; they will be greatly appreciated by the Legup development team.

## Where exactly is the code?
Most likely, the path for the code you are looking for from the repository root is located in `src/main/java/edu/rpi/legup`. 

If you are working on puzzles, you go to `src/main/java/edu/rpi/legup/puzzle`. In here, you will find the code for the rules and board for each of the different puzzles. If you are creating a new puzzle, you would create your new puzzle within this directory.

If you are working on UI, you go to `src/main/java/edu/rpi/legup/ui`. If you are creating any new views, you would create your new view within this directory.

## What is the general structure of a puzzle?
To simplify, each puzzle consists of a board, multiple rules, importer, and exporter.
### The Board
The board is the grid that is manipulated for the puzzle. While a board class will exist for each puzzle, there are also other components (such as cells) that will also make up the board. What each of these classes does is out of the scope of this getting started guide.

### The Rules
There are 3 types of rules: basic rules, contradiction rules, and case rules. Basic rules are just "A leads to B because of X rule". Contradiction rules are just "A is invalid because of X contradiction". Case rules branch off multiple possibilities. For example, in Nurikabe, each cell can be black or white. Therefore, the Black or White case rule will create 2 branches: one where the selected cell is black and one where the selected cell is white.

Each rule has its own corresponding ID, which can be found within the class or within a text file called `puzzlename_reference_sheet.txt` in the corresponding `rules` package. The implementation of each rule will require you to look at the information on the board and interpret it.

### Importer and Exporter
The importer imports data from a proof/puzzle file. The exporter saves a proof to a proof file. When you open file, you use the importer. When you save a file, you use the exporter.