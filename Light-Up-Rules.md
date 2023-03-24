# Light Up (WIP)
Light Up is a puzzle with unfilled squares shown in gray. The goal is to light up every cell in the grid by placing light bulbs in some of the cells.

Clicking on an unfilled tile places a light bulb and colors the area it lights up yellow

Clicking on a light bulb replaces it with an "empty" tile, represented by a black dot

Clicking on a "empty" tile returns it to being unfilled

### Definitions specific to light up
1. Light bulb: a cell from which light is emitted in straight lines from. A bulb cannot be in another’s light path. This is a cell state.
2. Light path: A direct line of sight to a light bulb. This is not a cell state which the user can directly add; it is automatically added when a light bulb is placed. Light is stopped by black blocks which are fixed on the board.


# Rules
### Here are the direct rules of the puzzle

1. A cell either has a bulb or is empty
2. Each cell must be lit by a light
3. Each numbered black block must have exactly that many bulbs around it
4. No bulb can be in another’s light path.
5. Light is emitted from a straight line from a bulb, stopped by blocks, in the four adjacent directions.(automatic)


# LEGUP Proof Rules
## Direct Rules


### Empty Cells in Light

[![bkcqiB.th.jpg](https://iili.io/bkcqiB.th.jpg)](https://freeimage.host/i/bkcqiB)

Rule comes directly from Rule #2. Any unknown lit cell must be empty

### Empty Corners

[![bkczHg.th.jpg](https://iili.io/bkczHg.th.jpg)](https://freeimage.host/i/bkczHg)

This rule is a derivation of Rules #1 and #3. Use this rule to place "empty" tiles on the corner of numbered black squares if placing a light there would make fulfilling Rule #3 impossible for that black tile.

### Finish with Bulbs

[![bkcTOJ.th.jpg](https://iili.io/bkcTOJ.th.jpg)](https://freeimage.host/i/bkcTOJ)

Rule comes directly from Rule #3. If the sum of a block’s unknown cells and its light bulb cells equals its number, then the unknown cells must contain bulbs 

### Finish with Empty

[![bkcERs.th.jpg](https://iili.io/bkcERs.th.jpg)](https://freeimage.host/i/bkcERs)

Rule comes directly from Rule #3. If a block with a number has as many light bulbs around it as its number, the other cells around it must not contain a light bulb and therefore be empty

### Must Light

[![bkchs2.th.jpg](https://iili.io/bkchs2.th.jpg)](https://freeimage.host/i/bkchs2)

Rule is a derivation of the goal. Use this rule to place a light bulb if there is an unlighted tile in which all other options for light bulbs are not possible


## Contradiction Rules
### Bulb in Path

[![bkcdAb.th.jpg](https://iili.io/bkcdAb.th.jpg)](https://freeimage.host/i/bkcdAb)

Rule comes directly from Rule #2. Use this rule when following a derivation that requires a light bulb to be placed in a lit tile.

### Cannot Light Cell? (Why cant use must light?)

[![bkcOg9.th.jpg](https://iili.io/bkcOg9.th.jpg)](https://freeimage.host/i/bkcOg9)

Rule is a derivation of rule #2 and the goal state. Use this rule when following a derivation that would not let you place a light bulb that could light Up a tile given the rules. Usually this is used when the tile is deemed 'empty' already


### Too Few Bulbs

[![bkcSbj.th.jpg](https://iili.io/bkcSbj.th.jpg)](https://freeimage.host/i/bkcSbj)

Rule comes directly from Rule #3. Use this rule when following a derivation that leads to a black tile being surrounded by fewer light bulbs than required

### Many Bulbs

[![bkc4sV.th.jpg](https://iili.io/bkc4sV.th.jpg)](https://freeimage.host/i/bkc4sV)

Rule comes directly from Rule #3. Use this rule when following a derivation that leads to a black tile being surrounded by more light bulbs than required



## Case Rules

### Satisfy Number

[![bklHqN.th.jpg](https://iili.io/bklHqN.th.jpg)](https://freeimage.host/i/bklHqN)

If a tile can be either an 'empty' tile or have a light bulb, use this rule to create a split where each branch has a valid placement of light bulbs

### Light or Empty

[![bkctea.th.jpg](https://iili.io/bkctea.th.jpg)](https://freeimage.host/i/bkctea)

If a numbered black square has more than one possible arrangement of light bulbs, use this rule to create a split in the tree each branch has a valid combination of light bulbs.

