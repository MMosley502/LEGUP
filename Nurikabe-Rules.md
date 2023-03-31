# Nurikabe
Nurikabe is a puzzle with unfilled squares shown in gray. Your task is to color all the cells white or black according to the rules of the game

Clicking on a gray tile first makes it white

Clicking on a white tile makes it black

Clicking on a black tile returns it to gray

### Definitions specific to Nurikabe
1) White Area: an adjacency region of white cells
2) Area’s number: The number of the (one!) cell that is part of that area that has a number


# Rules
### Here are the direct rules of the puzzle

1) You cannot fill in cells containing numbers black.
2) A number cell tells the number of continuous white cells it is connected to INCLUDING itself. 
3) Each area of white cells contains exactly one number in it, and they are separated by black cells.
4) The black cells are linked to form a single continuous wall.
5) Black cells cannot be linked to be 2×2 square or larger.

# LEGUP Proof Rules

## Case Rules

### Black or White

[![DwvEge.th.jpg](https://iili.io/DwvEge.th.jpg)](https://freeimage.host/i/DwvEge)

If a tile can be colored either white or black based on the current state of the board, create a split in the tree where the tile is black in one path, and white in the other to show the different cases

## Contradiction Rules
### Black Square
[![Dwvrmv.th.jpg](https://iili.io/Dwvrmv.th.jpg)](https://freeimage.host/i/Dwvrmv)

This rule comes directly from Rule #5. If a black 2x2 square is formed and there is no derivation around forming said square, the board is in a state of contradiction.

### Isolated Black
[![DwUJ07.th.jpg](https://iili.io/DwUJ07.th.jpg)](https://freeimage.host/i/DwUJ07)

This rule comes directly from Rule #4. If a black wall is unable to meet when following a derivation of a board, there is a contradiction and the board is in a state of contradiction.

### Multiple Numbers
[![DwUBzx.th.jpg](https://iili.io/DwUBzx.th.jpg)](https://freeimage.host/i/DwUBzx)

This rule comes directly from Rule #3. If a white region containing multiple numbers is formed, place a wall between the regions to avoid a contradiction

### No Number
[![DwUIg1.th.jpg](https://iili.io/DwUIg1.th.jpg)](https://freeimage.host/i/DwUIg1)

This rule comes directly from Rule #3. If a derivation leads to a white region that contains no numbers, the board is in a state of contradiction

### Too Few Spaces
[![DwU5mJ.th.jpg](https://iili.io/DwU5mJ.th.jpg)](https://freeimage.host/i/DwU5mJ)

This rule comes directly from Rule #2. If a derivation that leads to a white region containing too few white tiles is unable to be fixed by expanding the region, the board case is in a state of contradiction

### Too Many Spaces
[![DwUeB2.th.jpg](https://iili.io/DwUeB2.th.jpg)](https://freeimage.host/i/DwUeB2)

This rule comes directly from Rule #2. If a derivation that leads to a white region containing too many white tiles is unable to be fixed without placing illegal black tiles, the board is in a state of contradiction.

### Unreachable Cell
[![DwULBV.th.jpg](https://iili.io/DwULBV.th.jpg)](https://freeimage.host/i/DwULBV)

Rule is a combination of Rule #2 and Rule #3. If an unknown cell cannot be reached from any area by any path while making sure that the number of cells in the area don’t exceed the number, then the unknown should be black.

## Direct Rules
### Black Between Numbers
[![DwSKnp.th.jpg](https://iili.io/DwSKnp.th.jpg)](https://freeimage.host/i/DwSKnp)

This rule comes directly from Rule #3. If there are two white areas with a different number, and there is an unknown cell that is adjacent to both areas, then the unknown should be made black. 

### Black Bottle Neck
[![DweMG9.th.jpg](https://iili.io/DweMG9.th.jpg)](https://freeimage.host/i/DweMG9)

This rule is a derivation of Rule #4. If there is only one unknown adjacent to a black adjacency region, and there are other black cells that don’t belong to that region, then the unknown should be made black.

### Can't Reach Cell
[![DwvLBI.th.jpg](https://iili.io/DwvLBI.th.jpg)](https://freeimage.host/i/DwvLBI)

This rule is a derivation of Rule #3. If an unknown square is not within reach of any number cells to color it black, color the unknown square black.

### Corners Black
[![Dw8uEP.th.jpg](https://iili.io/Dw8uEP.th.jpg)](https://freeimage.host/i/Dw8uEP)

This rule is a derivation of Rule #4. If a white area needs only one more white cell, and there are two unknown adjacent to that area, and a third unknown adjacent to both of these two unknowns, then the third unknown must be black.

### Fill in Black
[![Dw8ayJ.th.jpg](https://iili.io/Dw8ayJ.th.jpg)](https://freeimage.host/i/Dw8ayJ)

This rule is a derivation from Rule #4. If a unfilled square is surrounded by black tiles, then the unknown square should be filled in black 

### Fill in White
[![Dw8han.th.jpg](https://iili.io/Dw8han.th.jpg)](https://freeimage.host/i/Dw8han)

This rule is a derivation from Rule #4. If there is only one unknown adjacent to a white area, and that area’s number is higher than the number of cells currently in that area, then the unknown should be made white. 

### Prevent Black Square
[![DwSWoQ.th.jpg](https://iili.io/DwSWoQ.th.jpg)](https://freeimage.host/i/DwSWoQ)

This rule is a derivation from Rule #5. If three out of four cells of a 2x2 block of cells are black, and the fourth is unknown, then the unknown should be made white.

### Surround Region
[![DwSgxR.th.jpg](https://iili.io/DwSgxR.th.jpg)](https://freeimage.host/i/DwSgxR)

This rule is a derivation of Rule #2. All the unknown cells that are adjacent to a white area that contains exactly the right number of cells should be made black 

### White Bottle Neck
[![DwSPfI.th.jpg](https://iili.io/DwSPfI.th.jpg)](https://freeimage.host/i/DwSPfI)

This rule is a derivation of Rule #2. If there is only one unknown adjacent to a white area, and that area does not contain any number, then the unknown should be made white 

### Block Connection
![image](https://user-images.githubusercontent.com/96987732/229222784-86dc1e87-1fde-4641-a0b3-e2452df9f0fa.png)

This rule is a derivation of Rule #2. If there is an area with a number, and a second area without a number, and an unknown adjacent to both areas, then if the sum of the number of cells of the two areas plus 1 is larger than the first area’s number, then the unknown should be made black