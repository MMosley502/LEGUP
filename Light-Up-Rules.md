# Light Up
Light Up is a puzzle with unfilled squares shown in gray. Your task is to ensure all non-black tiles are lit up with light bulbs.

Clicking on an unfilled tile places a light bulb and colors the area it lights up yellow

Clicking on a light bulb replaces it with an "empty" tile, represented by a black dot

Clicking on a "empty" tile returns it to being unfilled

# Rules
### Here are the direct rules of the puzzle

1) Light bulbs light Up ALL tiles on its row and column unless blocked by a black tile.

2) Light bulbs cannot shine lights on each other

3) Black tiles with numbers (0 to 4) must have that many light bulbs located cardinal adjacent to them (no diagonals)

# LEGUP Proof Rules
## Direct Rules


### Empty Cells in Light

[![bkcqiB.th.jpg](https://iili.io/bkcqiB.th.jpg)](https://freeimage.host/i/bkcqiB)

Rule comes directly from Rule #2. Use this rule to place "empty" tiles on all tiles that are being shined on

### Empty Corners

[![bkczHg.th.jpg](https://iili.io/bkczHg.th.jpg)](https://freeimage.host/i/bkczHg)

This rule is a derivation of Rules #1 and #3. Use this rule to place "empty" tiles on the corner of numbered black squares if placing a light there would make fulfilling Rule #3 impossible for that black tile.

### Finish with Bulbs

[![bkcTOJ.th.jpg](https://iili.io/bkcTOJ.th.jpg)](https://freeimage.host/i/bkcTOJ)

Rule comes directly from Rule #3. Use this rule to place light bulbs on the remaining adjacent tiles to fulfil light bulb requirement

### Finish with Empty

[![bkcERs.th.jpg](https://iili.io/bkcERs.th.jpg)](https://freeimage.host/i/bkcERs)

Rule comes directly from Rule #3. Use this rule to place "empty" tiles on the remaining adjacent tiles to fulfil light bulb requirement

### Must Light

[![bkchs2.th.jpg](https://iili.io/bkchs2.th.jpg)](https://freeimage.host/i/bkchs2)

Rule is a derivation of the goal. Use this rule to place a light bulb if there is an unlighted tile in which all other options for light bulbs are not possible


## Contradiction Rules
### Bulb in Path

[![bkcdAb.th.jpg](https://iili.io/bkcdAb.th.jpg)](https://freeimage.host/i/bkcdAb)

Rule comes directly from Rule #2. Use this rule when following a derivation that requires a light bulb to be placed in a lit tile.

### Cannot Light Cell

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

