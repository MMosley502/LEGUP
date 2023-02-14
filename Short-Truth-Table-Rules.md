# Short Truth table
Short Truth table is a visual representation of logic expressions that you need to assign values for

Red means the block represents "false", and green means the block represents "True"

Clicking on a gray block will color it green.

Clicking on a green block will color it red.

Clicking on a red block will color it gray.



# Rules
### Here are the basic rules of the puzzle

'And' Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       F       |
|       F           |       T           |       F       |
|       F           |       F           |       F       |

'Conditional' Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       F       |
|       F           |       T           |       T       |
|       F           |       F           |       T       |

'Biconditional' Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       F       |
|       F           |       T           |       F       |
|       F           |       F           |       T       |

'Or' Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       T       |
|       F           |       T           |       T       |
|       F           |       F           |       F       |

'Not' Expression Truth Table

|  Expression       | Truth State   |
| :----:            |    :----:     | 
|       T           |       F       |   
|       F           |       T       |   



# LEGUP Proof rules
## Basic rules


### True or False Rule

[![Hn3hHZu.jpg](https://iili.io/Hn3hHZu.jpg)](https://freeimage.host/)

The same variable must hold it's truth value in all cases, Use this rule to assign all of a given variable the same value


### 'And' Elimination

[![Hn3hnu1.jpg](https://iili.io/Hn3hnu1.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'And' State

### 'Biconditonal' Elimination 

[![Hn3h5ap.jpg](https://iili.io/Hn3h5ap.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'Biconditional'  State


### 'Conditonal' Elimination 

[![Hn3h5ap.jpg](https://iili.io/Hn3h5ap.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'Conditional' State


### 'Not' Elimination 

[![Hn3h8Mb.jpg](https://iili.io/Hn3h8Mb.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'Not' State

### 'Or' Elimination 

[![Hn3hSPj.jpg](https://iili.io/Hn3hSPj.jpg)](https://freeimage.host/)

Use this rule to color an expression green or red depending on the 'conditional' State

### 'And' Introduction

[![Hn3hiAP.jpg](https://iili.io/Hn3hiAP.jpg)](https://freeimage.host/)

Use this rule to Assign the 'And' a truth value on the the surronding expressions

### 'Biconditonal' Introduction

[![Hn3hLDF.jpg](https://iili.io/Hn3hLDF.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Bicontional' a truth value on the the surronding expressions

### 'Conditonal' Introduction 

[![Hn3hLDF.jpg](https://iili.io/Hn3hLDF.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Condtional' a truth value on the the surronding expressions

### 'Not' Introduction 

[![Hn3jFxn.jpg](https://iili.io/Hn3jFxn.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Not' a truth value on the the surronding expressions

### 'Or' Introduction 

[![Hn3jFxn.jpg](https://iili.io/Hn3jFxn.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Or' a truth value on the the surronding expressions



## Contradiction rules

### Contradicting 'And'

[![Hn3jTb9.jpg](https://iili.io/Hn3jTb9.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'And' is incorrect based on the surronding expressions

### Contradicting 'Variable'

[![Hn3ja0x.jpg](https://iili.io/Hn3ja0x.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value a variable in two locations has two different states

### Contradicting 'Bicondtional'

[![Hn3ja0x.jpg](https://iili.io/Hn3ja0x.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Bicondtional' is incorrect based on the surronding expressions

### Contradicting 'Condtional'

[![Hn3jEOP.jpg](https://iili.io/Hn3jEOP.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Condtional' is incorrect based on the surronding expressions

### Contradicting 'Negation'

[![Hn3jw0v.jpg](https://iili.io/Hn3jw0v.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Not' is incorrect based on the surronding expression

### Contradicting 'Or'

[![Hn3jveI.jpg](https://iili.io/Hn3jveI.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Or' is incorrect based on the surronding expressions

## Case rules

### 'And' Case

[![Hn3jig4.jpg](https://iili.io/Hn3jig4.jpg)](https://freeimage.host/)

Use this case on a known 'And' to create a split in the branch where the surronding expressions will satisfy the condition

### 'Atomic' Case

[![Hn3w9qb.jpg](https://iili.io/Hn3w9qb.jpg)](https://freeimage.host/)

Use this case on a unknown variable to create a split in the branch where the variable is true in one branch, and false in another

### 'Biconditional' Case

[![Hn3wqI1.jpg](https://iili.io/Hn3wqI1.jpg)](https://freeimage.host/)

Use this case on a known 'Biconditional' to create a split in the branch where the surronding expressions will satisfy the condition

### 'Conditional' Case

[![Hn3w7It.jpg](https://iili.io/Hn3w7It.jpg)](https://freeimage.host/)

Use this case on a known 'Conditional' to create a split in the branch where the surronding expressions will satisfy the condition

### 'Or' Case

[![Hn3wVv2.jpg](https://iili.io/Hn3wVv2.jpg)](https://freeimage.host/)

Use this case on a known 'Or' to create a split in the branch where the surronding expressions will satisfy the condition
