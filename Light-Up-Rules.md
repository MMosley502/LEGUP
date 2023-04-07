# Light Up
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
## Case Rules
### Satisfy Number

[![bklHqN.th.jpg](https://iili.io/bklHqN.th.jpg)](https://freeimage.host/i/bklHqN)

Relative to a black numbered square: Any placement of light bulbs around that number which satisfies the number (takes into account already placed lightbulbs, and makes all other cells white). 

### Light or Empty

[![bkctea.th.jpg](https://iili.io/bkctea.th.jpg)](https://freeimage.host/i/bkctea)

Relative to an unlit cell, at least one of the unknown (and unlit, to reduce the number) cells that can light up that cell (this could include itself) contains a lightbulb

## Contradiction Rules
### Bulb in Path

[![bkcdAb.th.jpg](https://iili.io/bkcdAb.th.jpg)](https://freeimage.host/i/bkcdAb)

Rule comes directly from Rule #2. There is no derivation to avoid a light bulb to be placed in a lit path.

### Cannot Light Cell

[![bkcOg9.th.jpg](https://iili.io/bkcOg9.th.jpg)](https://freeimage.host/i/bkcOg9)

Rule is a derivation of rule #2 and the goal state. There is no possible way for a bulb to be placed to light a particular cell. All cells that can possibly light that cell (including itself) are empty. 

### Too Few Bulbs

[![bkcSbj.th.jpg](https://iili.io/bkcSbj.th.jpg)](https://freeimage.host/i/bkcSbj)

Rule comes directly from Rule #3. There is no way to satisfy a number in a black square

### Many Bulbs

[![bkc4sV.th.jpg](https://iili.io/bkc4sV.th.jpg)](https://freeimage.host/i/bkc4sV)

Rule comes directly from Rule #3. There is no way to lower the number of bulbs to match the black square that they surround

## Direct Rules
### Empty Cells in Light

[![bkcqiB.th.jpg](https://iili.io/bkcqiB.th.jpg)](https://freeimage.host/i/bkcqiB)

Rule comes directly from Rule #2. Any unknown lit cell must be empty

### Empty Corners

[![bkczHg.th.jpg](https://iili.io/bkczHg.th.jpg)](https://freeimage.host/i/bkczHg)

This rule is a derivation of Rules #1 and #3. The diagonal corners of a numbered square are empty (Rule #3 forces those corners to be empty in each possible case)

### Finish with Bulbs

[![bkcTOJ.th.jpg](https://iili.io/bkcTOJ.th.jpg)](https://freeimage.host/i/bkcTOJ)

Rule comes directly from Rule #3. If the sum of a block’s unknown cells and its light bulb cells equals its number, then the unknown cells must contain bulbs 

### Finish with Empty

[![bkcERs.th.jpg](https://iili.io/bkcERs.th.jpg)](https://freeimage.host/i/bkcERs)

Rule comes directly from Rule #3. If a block with a number has as many light bulbs around it as its number, the other cells around it must not contain a light bulb and therefore be empty

### Must Light

[![bkchs2.th.jpg](https://iili.io/bkchs2.th.jpg)](https://freeimage.host/i/bkchs2)

Rule is a derivation of the goal. If there is only cell from which an unlit cell can be lit from, then that cell must have a bulb 