# Nurikabe 
Nurikabe is a puzzle with unfilled squares  shown in gray. Your task is to color all the cells white or black according to the rules of the game

Clicking on a gray tile first fills it white

Clicking on a white tile fills it black

Clicking on a black tile returns it to becoming gray

# Rules
### Here are the direct rules of the puzzle

1) You cannot fill in cells containing numbers black.
2) A number cell tells the number of continuous white cells it is connected to INCLUDING itself. 
3) Each area of white cells contains exactly one number in it. and they are separated by black cells.
4) The black cells are linked to be a single continuous wall.
5) Black cells cannot be linked to be 2×2 square or larger.

# LEGUP Proof Rules
## Direct Rules
### Black Between Regions 
[![DwSKnp.th.jpg](https://iili.io/DwSKnp.th.jpg)](https://freeimage.host/i/DwSKnp)

This rule comes directly from Rule #3. Use this rule to place black tiles when differeing regions are close to each other to insert black squares between these regions

### Black Bottle Neck
[![DweMG9.th.jpg](https://iili.io/DweMG9.th.jpg)](https://freeimage.host/i/DweMG9)

This rule is a deriviation of Rule #4. Use this rule to place black tiles when a black square is  surrounded by white tiles to help ensure all the black tiles are connected

### Can't Reach Cell
[![DwvLBI.th.jpg](https://iili.io/DwvLBI.th.jpg)](https://freeimage.host/i/DwvLBI)

This rule is a deriviation of Rule #3. Use this rule to place black tiles if a square is not within reach of any number cells to color it black

### Corners Black
[![Dw8uEP.th.jpg](https://iili.io/Dw8uEP.th.jpg)](https://freeimage.host/i/Dw8uEP)

This rule is a derivation of Rule #4. Use this rule to place black tiles next to any black tile that is  surrounded by white tiles 

### Fill in Black
[![Dw8ayJ.th.jpg](https://iili.io/Dw8ayJ.th.jpg)](https://freeimage.host/i/Dw8ayJ)

This rule is a deriviation from Rule #4. Use this rule to place black tiles if a unfilled square is  surrounded by black tiles 

### Fill in White
[![Dw8han.th.jpg](https://iili.io/Dw8han.th.jpg)](https://freeimage.host/i/Dw8han)

This rule is a deriviation from Rule #4. Use this rule to place white tiles if a unfilled square is  surrounded by white tiles

### Prevent Black Square
[![DwSWoQ.th.jpg](https://iili.io/DwSWoQ.th.jpg)](https://freeimage.host/i/DwSWoQ)

This rule is a deriviation from Rule #5. Use this rule to place white tiles if a a black square would form if the tile was colored black

### Surrond Region
[![DwSgxR.th.jpg](https://iili.io/DwSgxR.th.jpg)](https://freeimage.host/i/DwSgxR)

This rule is a deriviation of Rule #2. Use this rule to place black tiles around a completed white region 

### White Bottle Neck
[![DwSPfI.th.jpg](https://iili.io/DwSPfI.th.jpg)](https://freeimage.host/i/DwSPfI)

This rule is a derivation of Rule #2, Use this rule to place a single white tiles on any region that needs expansion and currently  surrounded by black tiles

## Contradiction Rules
### Black Square
[![Dwvrmv.th.jpg](https://iili.io/Dwvrmv.th.jpg)](https://freeimage.host/i/Dwvrmv)

Rule comes directly from Rule #5. Use this rule when following a deriviation that leads to a black square being formed

### Isolated Black
[![DwUJ07.th.jpg](https://iili.io/DwUJ07.th.jpg)](https://freeimage.host/i/DwUJ07)

Rule comes directly from Rule #4. Use this rule when following a deriviation that leads to  the black wall being unable to meet

### Multiple Numbers
[![DwUBzx.th.jpg](https://iili.io/DwUBzx.th.jpg)](https://freeimage.host/i/DwUBzx)

Rule comes directly from Rule #3. Use this rule when following a deriviation that leads to a white region containing multiple numbers is formed

### No Number
[![DwUIg1.th.jpg](https://iili.io/DwUIg1.th.jpg)](https://freeimage.host/i/DwUIg1)

Rule comes directly from Rule #3. Use this rule when following a deriviation that leads to a white region that contains no numbers

### Too Few Spaces
[![DwU5mJ.th.jpg](https://iili.io/DwU5mJ.th.jpg)](https://freeimage.host/i/DwU5mJ)

Rule comes directly from Rule #2. Use this rule when following a derivation that leads to a white region containing too few white tiles

### Too Many Spaces
[![DwUeB2.th.jpg](https://iili.io/DwUeB2.th.jpg)](https://freeimage.host/i/DwUeB2)

Rule comes directly from Rule #2. Use this rule when following a derivation that leads to a white region containing too many white tiles

### Unreachable Cell
[![DwULBV.th.jpg](https://iili.io/DwULBV.th.jpg)](https://freeimage.host/i/DwULBV)

Rule is a combination of Rule #2 and Rule #3. Use this rule when following a deriviation that leads to a white being placed where no numbered tiles are able to reach it

## Case Rules

### Black or White

[![DwvEge.th.jpg](https://iili.io/DwvEge.th.jpg)](https://freeimage.host/i/DwvEge)

If a tile can be colored either white or black based on the current state of the board, use this rule to create a split in the tree where the tile is black in one path, and white in the other