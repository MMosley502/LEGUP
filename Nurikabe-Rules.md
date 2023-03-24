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
## Direct Rules
### Black Between Regions 
[![DwSKnp.th.jpg](https://iili.io/DwSKnp.th.jpg)](https://freeimage.host/i/DwSKnp)

This rule comes directly from Rule #3. If there are two white areas with a different number, and there is an unknown cell that is adjacent to both areas, then the unknown should be made black. 

### Black Bottle Neck
[![DweMG9.th.jpg](https://iili.io/DweMG9.th.jpg)](https://freeimage.host/i/DweMG9)

This rule is a derivation of Rule #4. Use this rule to place black tiles when a black square is surrounded by white tiles to help ensure all the black tiles are connected

### Can't Reach Cell
[![DwvLBI.th.jpg](https://iili.io/DwvLBI.th.jpg)](https://freeimage.host/i/DwvLBI)

This rule is a derivation of Rule #3. Use this rule to place black tiles if a square is not within reach of any number cells to color it black

### Corners Black
[![Dw8uEP.th.jpg](https://iili.io/Dw8uEP.th.jpg)](https://freeimage.host/i/Dw8uEP)

This rule is a derivation of Rule #4. Use this rule to place black tiles next to any black tile that is surrounded by white tiles 

### Fill in Black
[![Dw8ayJ.th.jpg](https://iili.io/Dw8ayJ.th.jpg)](https://freeimage.host/i/Dw8ayJ)

This rule is a derivation from Rule #4. Use this rule to place black tiles if a unfilled square is surrounded by black tiles 

### Fill in White
[![Dw8han.th.jpg](https://iili.io/Dw8han.th.jpg)](https://freeimage.host/i/Dw8han)

This rule is a derivation from Rule #4. Use this rule to place white tiles if a unfilled square is surrounded by white tiles

### Prevent Black Square
[![DwSWoQ.th.jpg](https://iili.io/DwSWoQ.th.jpg)](https://freeimage.host/i/DwSWoQ)

This rule is a derivation from Rule #5. If three out of four cells of a 2x2 block of cells are black, and the fourth is unknown, then the unknown should be made white.

### Surround Region
[![DwSgxR.th.jpg](https://iili.io/DwSgxR.th.jpg)](https://freeimage.host/i/DwSgxR)

This rule is a derivation of Rule #2. All the unknown cells that are adjacent to a white area that contains exactly the right number of cells should be made black 

### White Bottle Neck
[![DwSPfI.th.jpg](https://iili.io/DwSPfI.th.jpg)](https://freeimage.host/i/DwSPfI)

This rule is a derivation of Rule #2. If there is only one unknown adjacent to a white area, and that area does not contain any number, then the unknown should be made white 

## Contradiction Rules
### Black Square
[![Dwvrmv.th.jpg](https://iili.io/Dwvrmv.th.jpg)](https://freeimage.host/i/Dwvrmv)

This rule comes directly from Rule #5. Use this rule when following a derivation that leads to a black square being formed

### Isolated Black
[![DwUJ07.th.jpg](https://iili.io/DwUJ07.th.jpg)](https://freeimage.host/i/DwUJ07)

This rule comes directly from Rule #4. Use this rule when following a derivation that leads to the black wall being unable to meet

### Multiple Numbers
[![DwUBzx.th.jpg](https://iili.io/DwUBzx.th.jpg)](https://freeimage.host/i/DwUBzx)

This rule comes directly from Rule #3. Use this rule when following a derivation that leads to a white region containing multiple numbers is formed

### No Number
[![DwUIg1.th.jpg](https://iili.io/DwUIg1.th.jpg)](https://freeimage.host/i/DwUIg1)

This rule comes directly from Rule #3. Use this rule when following a derivation that leads to a white region that contains no numbers

### Too Few Spaces
[![DwU5mJ.th.jpg](https://iili.io/DwU5mJ.th.jpg)](https://freeimage.host/i/DwU5mJ)

This rule comes directly from Rule #2. Use this rule when following a derivation that leads to a white region containing too few white tiles

### Too Many Spaces
[![DwUeB2.th.jpg](https://iili.io/DwUeB2.th.jpg)](https://freeimage.host/i/DwUeB2)

This rule comes directly from Rule #2. Use this rule when following a derivation that leads to a white region containing too many white tiles

### Unreachable Cell
[![DwULBV.th.jpg](https://iili.io/DwULBV.th.jpg)](https://freeimage.host/i/DwULBV)

Rule is a combination of Rule #2 and Rule #3. If an unknown cell cannot be reached from any area by any path while making sure that the number of cells in the area don’t exceed the number, then the unknown should be black

## Case Rules

### Black or White

[![DwvEge.th.jpg](https://iili.io/DwvEge.th.jpg)](https://freeimage.host/i/DwvEge)

If a tile can be colored either white or black based on the current state of the board, use this rule to create a split in the tree where the tile is black in one path, and white in the other

# Tutorial
## Here are the general steps you can take to solve the Nurikabe puzzle

### Step 1: Close cells adjacent to 1s

![image](https://user-images.githubusercontent.com/96987732/226740844-4a2deefe-e2a8-4f87-8b14-5e9cf5b6e6a2.png)

### Step 2: Close any cell between two numbers

![image](https://user-images.githubusercontent.com/96987732/226740957-5a5dd5b9-4653-4ce4-abdb-ff2130ef1b55.png)

### Step 3: Identify "Realms"
* Realms are cells with reach on the board. 
* It is recommended to start with cells that have the Maximum reach. 
* When considering reach, disregard open and closed cells

![image](https://user-images.githubusercontent.com/96987732/226741528-ef59a733-4fa7-416e-91b6-31bee71fd27e.png)

### Step 4: Overlay all Realms

![image](https://user-images.githubusercontent.com/96987732/226742026-2738a873-58cd-497a-94a9-3320be7429c1.png)

### Step 5: Close any cell not covered by any of the Realms 

![image](https://user-images.githubusercontent.com/96987732/226742226-17de951f-77f9-4563-9bb8-3ae434163c95.png)

### Step 6: Check for cells that are forced open. 
* If any realm contains the number of cells as the contained number make them all open

![image](https://user-images.githubusercontent.com/96987732/226743107-3523436f-6002-4e9e-83e0-df26dfa4ca0d.png)

### Step 7: Reduce maximum reach
* If an open cell is only covered by one realm, it belongs to that number
* Because of this, the coverage of the realms will shrink to be able to connect to the open cell
* Repeat from step 5

### Step 8: Remove cells adjacent to open cells
* Any cell adjacent to an open cell that belongs to a different realms should be closed
* Repeat from step 5 again

### Step 9: Check for blocks of 3 closed, and check what block is forced open

![image](https://user-images.githubusercontent.com/96987732/226745145-438aca2e-722e-4a77-a00e-52c74f6452f4.png)

### Step 10: Check for blocks of 2 closed
* A block of 2 indicates that at least one of the other 2 must be open. If the 2 unmarked are in only one realm, at least one of the 2 must be connected to that number. If one cell must be Open for the other to be, then the first cell must be Open. This will reduced the maximum reach of the realm (Step 7).
* If each of the unmarked cells is in only 1 realm and the realms are not the same, one of the cells must be closed

