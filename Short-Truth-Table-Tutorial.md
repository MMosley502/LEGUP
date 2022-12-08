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


### Atomic Rule

The same variable must hold it's truth value in all cases, Use this rule to assign all of a given variable the same value


### 'And' Elimination

Use this rule to assign an expression a truth value depending on the 'And' State

### 'Biconditonal' Elimination 

Use this rule to assign an expression a truth value depending on the 'Biconditional'  State


### 'conditonal' Elimination 

Use this rule to assign an expression a truth value depending on the 'conditional' State


### 'Not' Elimination 

Use this rule to assign an expression a truth value depending on the 'conditional' State

### 'Or' Elimination 

Use this rule to color an expression green or red depending on the 'conditional' State

### 'And' Introduction

Use this rule to Assign the 'And' a truth value on the the surronding expressions

### 'Biconditonal' Introduction

Use this rule to Assign the 'Bicontional' a truth value on the the surronding expressions

### 'conditonal' Introduction 

Use this rule to Assign the 'Condtional' a truth value on the the surronding expressions

### 'Not' Introduction 

Use this rule to Assign the 'Not' a truth value on the the surronding expressions

### 'Or' Introduction 
Use this rule to Assign the 'Or' a truth value on the the surronding expressions


## Contradiction rules

### Contradicting 'And'

Use this rule to end a line of reasoning if the value of the 'And' is incorrect based on the surronding expressions

### Contradicting 'Variable'

Use this rule to end a line of reasoning if the value a variable in two locations has two different states

### Contradicting 'Bicondtional'

Use this rule to end a line of reasoning if the value of the 'Bicondtional' is incorrect based on the surronding expressions

### Contradicting 'Condtional'

Use this rule to end a line of reasoning if the value of the 'Condtional' is incorrect based on the surronding expressions

### Contradicting 'Negation'

Use this rule to end a line of reasoning if the value of the 'Not' is incorrect based on the surronding expression

### Contradicting 'Or'

Use this rule to end a line of reasoning if the value of the 'Or' is incorrect based on the surronding expressions

## Case rules

### 'And' Case

Use this case on a known 'And' to create a split in the branch where the surronding expressions will satisfy the condition

### 'Atomic' Case

Use this case on a unknown variable to create a split in the branch where the variable is true in one branch, and false in another

### 'Biconditional' Case

Use this case on a known 'Biconditional' to create a split in the branch where the surronding expressions will satisfy the condition

### 'Conditional' Case

Use this case on a known 'Conditional' to create a split in the branch where the surronding expressions will satisfy the condition

### 'Or' Case

Use this case on a known 'Or' to create a split in the branch where the surronding expressions will satisfy the condition
