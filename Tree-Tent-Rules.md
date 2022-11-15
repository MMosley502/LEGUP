# Tree Tent
Tree Tent is a puzzle with unfilled squares shown in gray. Your task is to place tents in such a way that the number tents in each row and column is satisifed, and that each tree has a tent next to it

Clicking on a unfilled tile places a grass tile

Clicking on a grass tile replaces it with a tent tile

Clicking on a tent tile returns it to being unfilled

# Rules
### Here are the basic rules of the puzzle

1) Each tent is attached to one tree (so there are as many tents as there are trees).

2) The numbers across the top and down the side show how many tents are in the respective row or column.

3) A tent can only be found horizontally or vertically adjacent to a tree.

4) Tents are never adjacent to each other, neither vertically, horizontally, nor diagonally

# LEGUP Proof rules
## Basic rules


### Empty Field

Rule ccomes directly from Rule #3. Use this rule to place grass tiles on any tile that isn't horizontally or vertically adjacent to a tree.


### Finish with Grass

Rule ccomes directly from Rule #2. Use this rule to place grass tiles on any tile in a row/column that has the required number of tents

### Finish with Tents

Rule ccomes directly from Rule #2. Use this rule to place tent tiles on any tile in a row/column that has the same number of unfilled tiles as there are tents required.  


### Last Camping Spot

Derivation of Rule #1. Use this rule to place a tent next to a tree which currently has no tents and is suroonded by grass/tree tiles.

### Surrond Tent with Grass

Rule ccomes directly from Rule #4. Use this rule to place grass tiles on any tile that is vertically, horizontally, or diagonally adjacent to a tent

### Tent for Tree

Rule comes directly from Rule #1.

### Tree for Tent

Rule comes directly from Rule #1.

## Contradiction rules

### No Tent for Tree


### No Tree for Tent



### Too few Tents



### Too many Tents


### Touching Tents




## Case rules

### Fill in Row

### Links from Tent

### Links from Tree

### Tent or Grass



