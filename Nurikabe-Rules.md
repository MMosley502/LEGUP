# Nurikabe 
Nurikabe is a puzzle, unfilled squares are shown as gray, and your job is to color all the cells white or black according to the rules of the game
Clicking on a gray tile first fills it white, clicking on a white tile fills it black, and clicking on a black tile returns it to becoming gray

# Rules
### Here are the basic rules of the puzzle

1) You cannot fill in cells containing numbers black.
2) A number cell tells the number of continuous white cells it is connected to INCLUDING itself. 
3) Each area of white cells contains exactly one number in it. and they are separated by black cells.
4) The black cells are linked to be a single continuous wall.
5) Black cells cannot be linked to be 2×2 square or larger.

# LEGUP Proof rules
## Basic rules
### Black Between Regions 
 
This rule comes directly from Rule #3. Use this rule to place black tiles when differeing regions are close to each other to insert black squares between these regions

### Black Bottle Neck
 

### Can't Reach Cell
 
This rule is a deriviation of Rule #3. Use this rule to place black tiles if a square is not within reach of any number cells to color it black

### Corners Black
 

This rule is a derivation of Rule #4. Use this rule to place black tiles next to any black tile that is surronded by white tiles 

### Fill In Black
 
This rule is a deriviation from Rule #4. Use this rule to place black tiles if a unfilled square is surronded by black tiles 

### Fill In White
 

This rule is a deriviation from Rule #4. Use this rule to place white tiles if a unfilled square is surronded by white tiles

### Prevent Black Square
 

This rule is a deriviation from Rule #5. Use this rule to place white tiles if a a black square would form if the tile was colored black

### Surrond Region
 
This rule is a deriviation of Rule #2. Use this rule to place black tiles around a completed white region 

### White Bottle Neck
 

This rule is a derivation of Rule #2, Use this rule to place a single white tiles on any region that needs expansion and currently surronded by black tiles

## Contradiction rules
### Black Square
 
Rule comes directly from Rule #5. Use this rule when following a deriviation that leads to a black square being formed

### Isolated Black
 

Rule comes directly from Rule #4. Use this rule when following a deriviation that leads to  the black wall being unable to meet

### Multiple Numbers

Rule comes directly from Rule #3. Use this rule when following a deriviation that leads to a white region containing multiple numbers is formed

### No Number
 

Rule comes directly from Rule #3. Use this rule when following a deriviation that leads to a white region that contains no numbers

### Too Few Spaces
 

Rule comes directly from Rule #2. Use this rule when following a derivation that leads to a white region containing too few white tiles

### Too Many Spaces
 

Rule comes directly from Rule #2. Use this rule when following a derivation that leads to a white region containing too many white tiles

### Unreachable Cell
 

Rule is a combination of Rule #2 and Rule #3. Use this rule when following a deriviation that leads to a white being placed where no numbered tiles are able to reach it

## Case rules

### Black or White

If a tile can be colored either white or black based on the current state of the board, use this rule to create a split in the tree where the tile is black in one path, and white in the other