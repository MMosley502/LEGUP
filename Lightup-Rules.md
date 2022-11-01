# Lightup
Lightup is a puzzle with unfilled squares shown in gray. Your task ensure all non-black tiles are lit up with lightbulbs.

Clicking on a unfilled tile places a lightbulb and colors the area it lights up yellow

Clicking on a lightbulb replaces it with a "empty" tile, represented by a black dot

Clicking on a "empty" tile returns it to being unfilled

# Rules
### Here are the basic rules of the puzzle

1) Lightbulbs shines light on ALL tiles on it's row and column unless blocked by a black tile.

2) Lightbulbs cannot shine lights on each other

3) black tiles with numbers (0 -> 4) must have that many lightbulbs cardinally adjacent to them (no diagonols)

# LEGUP Proof rules
## Basic rules


### Empty Cells in Light

[![bkcqiB.th.jpg](https://iili.io/bkcqiB.th.jpg)](https://freeimage.host/i/bkcqiB)

Rule comes directly from Rule #2. Use this rule to place "empty" tiles on all tiles that are being shined on

### Empty Corners

[![bkczHg.th.jpg](https://iili.io/bkczHg.th.jpg)](https://freeimage.host/i/bkczHg)

Rule is a derivation of Rule #1 and #3. Use this rule to place "empty" tiles on the corner of numbered black squares if placing a light there would make fufilling Rule #3 impossible for that black tile.

### Finish with Bulbs

[![bkcTOJ.th.jpg](https://iili.io/bkcTOJ.th.jpg)](https://freeimage.host/i/bkcTOJ)

Rule comes directly from Rule #3. Use this rule to place lightbulbs on the remaining adjacent tiles to fufill lightbulb requirement

### Finish with Empty

[![bkcERs.th.jpg](https://iili.io/bkcERs.th.jpg)](https://freeimage.host/i/bkcERs)

Rule comes directly from Rule #3. Use this rule to place "empty" tiles on the remaining adjacent tiles to fufill lightbulb requirement

### Must Light

[![bkchs2.th.jpg](https://iili.io/bkchs2.th.jpg)](https://freeimage.host/i/bkchs2)

Rule is a derivation of the goal. Use this rule to place a lightbulb if there is a unlighted tile in which all other options for lightbulbs are not possible


## Contradiction rules
### Bulb in Path

[![bkcdAb.th.jpg](https://iili.io/bkcdAb.th.jpg)](https://freeimage.host/i/bkcdAb)

Rule comes directly from Rule #2. Use this rule when following a derivation that requires a lightbulb to be placed in a lit tile.

### Cannot Light Cell

[![bkcOg9.th.jpg](https://iili.io/bkcOg9.th.jpg)](https://freeimage.host/i/bkcOg9)

Rule is a derivation of rule #2 and the goal state. Use this rule when following a derivation that would not let you place a lightbulb that could light up a tile given the rules. Usually this is used when the tile is deemed 'empty' already


### Too Few Bulbs

[![bkcSbj.th.jpg](https://iili.io/bkcSbj.th.jpg)](https://freeimage.host/i/bkcSbj)

Rule comes directly from Rule #3. Use this rule when following a derivation that leads to a black tile being surronded by fewer lightbulbs than required

### Many Bulbs

[![bkc4sV.th.jpg](https://iili.io/bkc4sV.th.jpg)](https://freeimage.host/i/bkc4sV)

Rule comes directly from Rule #3. Use this rule when following a derivation that leads to a black tile being surronded by more lightbulbs than required



## Case rules

### Satisfy Number

[![bklHqN.th.jpg](https://iili.io/bklHqN.th.jpg)](https://freeimage.host/i/bklHqN)

If a tile can be either a 'empty' tile or have a Lightbulb,  use this rule to create a split in the tree where the tile is 'empty' in one path, and has a lightbulb in the other

### Light or Empty

[![bkctea.th.jpg](https://iili.io/bkctea.th.jpg)](https://freeimage.host/i/bkctea)

If a numbered black square has more than 1 possible arrangement of lightbulbs,  use this rule to create a split in the tree each branch has a valid combination of lightbulbs.

