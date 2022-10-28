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

Rule comes directly from Rule #2. Use this rule to place "empty" tiles on all tiles that are being shined on

### Empty Corners
Rule is a derivation of Rule #1 and #3. Use this rule to place "empty" tiles on the corner of numbered black squares if placing a light there would make fufilling Rule #3 impossible for that black tile.


### Finish with Bulbs

Rule comes directly from Rule #3. Use this rule to place lightbulbs on the remaining adjacent tiles to fufill lightbulb requirement

### Finish with Empty

Rule comes directly from Rule #3. Use this rule to place "empty" tiles on the remaining adjacent tiles to fufill lightbulb requirement

### Must Light

Rule is a derivation of the goal. Use this rule to place a lightbulb if there is a unlighted tile in which all other options for lightbulbs are not possible


## Contradiction rules
### Rule #
[INSERT LINK HERE]

### Rule #
[INSERT LINK HERE]
### Rule #
[INSERT LINK HERE]



## Case rules

### Rule #
[INSERT LINK HERE]

### Rule #
[INSERT LINK HERE]
### Rule #
[INSERT LINK HERE]