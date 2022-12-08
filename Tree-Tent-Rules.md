# Tree Tent
Tree Tent is a puzzle with unfilled squares shown in gray. Your task is to place tents in such a way that the number tents in each row and column is satisifed, and that each tree has a tent next to it.

Clicking on a unfilled tile places a grass tile.

Clicking on a grass tile replaces it with a tent tile.

Clicking on a tent tile returns it to being unfilled.

# Rules
### Here are the basic rules of the puzzle

1) Each tent is attached to one tree (so there are as many tents as there are trees).

2) The numbers across the top and down the side show how many tents are in the respective row or column.

3) A tent can only be found horizontally or vertically adjacent to a tree.

4) Tents are never adjacent to each other, neither vertically, horizontally, nor diagonally.

# LEGUP Proof rules
## Basic rules


### Empty Field

[![H9o9yk7.th.jpg](https://iili.io/H9o9yk7.th.jpg)](https://freeimage.host/i/H9o9yk7)

Rule comes directly from Rule #3. Use this rule to place grass tiles on any tile that isn't horizontally or vertically adjacent to a tree.


### Finish with Grass

[![H9oHX44.th.jpg](https://iili.io/H9oHX44.th.jpg)](https://freeimage.host/i/H9oHX44)

Rule ccomes directly from Rule #2. Use this rule to place grass tiles on any tile in a row/column that has the required number of tents.

### Finish with Tents

[![H9oHvje.th.jpg](https://iili.io/H9oHvje.th.jpg)](https://freeimage.host/i/H9oHvje)

Rule ccomes directly from Rule #2. Use this rule to place tent tiles on any tile in a row/column that has the same number of unfilled tiles as there are tents required.  


### Last Camping Spot

[![H9oHr6x.th.jpg](https://iili.io/H9oHr6x.th.jpg)](https://freeimage.host/i/H9oHr6x)

Derivation of Rule #1. Use this rule to place a tent next to a tree which currently has no tents and is suroonded by grass/tree tiles.

### Surrond Tent with Grass

[![H9oHsyP.th.jpg](https://iili.io/H9oHsyP.th.jpg)](https://freeimage.host/i/H9oHsyP)

Rule ccomes directly from Rule #4. Use this rule to place grass tiles on any tile that is vertically, horizontally, or diagonally adjacent to a tent.

### Tent for Tree

[![H9oHp6v.th.jpg](https://iili.io/H9oHp6v.th.jpg)](https://freeimage.host/i/H9oHp6v)

Rule comes directly from Rule #1.

### Tree for Tent

[![H9oJqns.th.jpg](https://iili.io/H9oJqns.th.jpg)](https://freeimage.host/i/H9oJqns)

Rule comes directly from Rule #1.

## Contradiction rules

### No Tent for Tree

[![H9oJoF4.th.jpg](https://iili.io/H9oJoF4.th.jpg)](https://freeimage.host/i/H9oJoF4)

Rule comes directly from Rule #1. Use this rule if a derivation leads to a situation where no place for a tent to be placed vertically or horizontally adjacent to a tree.

### No Tree for Tent

[![H9oJlKx.th.jpg](https://iili.io/H9oJlKx.th.jpg)](https://freeimage.host/i/H9oJlKx)

Rule comes directly from Rule #1. Use this rule if a derivation leads to a situation where there is a tent that isn't placed vertically or horizontally adjacent to a tree.

### Too few Tents

[![H9oJMAP.th.jpg](https://iili.io/H9oJMAP.th.jpg)](https://freeimage.host/i/H9oJMAP)

Rule comes directly from Rule #2. Use this rule if a derivation leads to a row/column having not enough tents to fufill the requirements.

### Too many Tents

[![H9oJjVa.th.jpg](https://iili.io/H9oJjVa.th.jpg)](https://freeimage.host/i/H9oJjVa)

Rule comes directly from Rule #2. Use this rule if a derivation leads to a row/column having more tents than the requirements state.



### Touching Tents

[![H9oJSRI.th.jpg](https://iili.io/H9oJSRI.th.jpg)](https://freeimage.host/i/H9oJSRI)

Rule comes directly from Rule #4. Use this rule if a derivation leads to a two tents being placed vertically, horizontally, or diagonally adjacent.



## Case rules

### Fill in Row

[![H9oJtJ2.th.jpg](https://iili.io/H9oJtJ2.th.jpg)](https://freeimage.host/i/H9oJtJ2)

Use this rule to create a branch in the proof of all possible combinations of tents and grass tiles of a particular row 


### Links from Tent

[![H9oJbO7.th.jpg](https://iili.io/H9oJbO7.th.jpg)](https://freeimage.host/i/H9oJbO7)

Use this rule to select a tent and create a branch in the proof where each branch contains a possible link beteween that tent in a tree.


### Links from Tree

[![H9odHib.th.jpg](https://iili.io/H9odHib.th.jpg)](https://freeimage.host/i/H9odHib)

Use this rule to select a tree and create a branch in the proof where each branch contains a possible link beteween that tree to any ajacent tents.


### Tent or Grass

[![H9odHib.th.jpg](https://iili.io/H9odHib.th.jpg)](https://freeimage.host/i/H9odHib)

Use this rule to create a split in the tree where the tile selected is a tent in one branch, and a grass tile in another branch



