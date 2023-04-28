# Short Truth Table
Short Truth Table is a visual representation of logic expressions for which you need to assign values in the Short Truth Table Method.

## Short Truth Table Method

The Short Truth Table Method assigns truth values to the involved atomic and complex statements in order to obtain a desired combination of truth values. The Short Truth Table Method thus tries to generate one row of the truth table that has the combination of truth values in which you are interested. The Truth Table Method systematically exhausts all possible truth value combinations of the involved statements. In the truth table, we look for a row that reflects a certain possibility, and that will tell us the answer to whatever question we had. The Short Truth Table Method shortens this process by focusing the search.

As you assign truth values to certain statements, the truth values of other statements can be forced. For example, if you are forced to make a statement both true and false, then you know that the combination of truth values you are looking for does not exist (this is called Contradiction, and you can see its rules in later sections, as well as other rules that will help you solve given exercises). The Short Truth Table Method is therefore often a kind of proof by contradiction or indirect proof. 

There are different final evaluations of logical arguments (collections of premises and conclusions) that you can reach as a result of the Short Truth Table Method:
* Valid Argument: It is not possible to have true premises and a false conclusion. To prove this, you can suppose the premises of an argument are true and the conclusion is false, and derive a contradiction.
* Invalid Argument: It is possible to have true premises and a false conclusion. To prove this, you can suppose the premises of an argument are true and the conclusion is false, and that all statements can be evaluated in that case with no contradictions.
* Tautology: It is not possible for the statement in question to be false. To prove this, you can suppose the statement in question is false and derive a contradiction.
* Contradiction: It is not possible for the statement to be true. To prove this, you can suppose the statement in question is true and derive a contradiction (which, in this sense, means that if the statement is true then some other statement or variable is assigned both true and false according to the Contradiction Rules later on).

## Puzzle Instructions

In LEGUP Short Truth Table, rather than annotating statements with truth values, we’ll turn the statements green (True) or red (False). The truth value of a statement is indicated by the truth value of its outermost operator. The truth values of operators and variables are linked to one another according to the rules in the following sections.

In order to complete a proof in this Puzzle, you will change the undetermined truth values of each block in each statement in a systematic way, supporting each change with a logical rule from the list below. The truth values of the blocks can be changed in the following ways:
* Clicking on a gray block will color it green (True).
* Clicking on a green block will color it red (False).
* Clicking on a red block will color it gray (Undetermined).

# LEGUP Proof rules

## Case Rules

### AND Case

[![Hn3jig4.jpg](https://iili.io/Hn3jig4.jpg)](https://freeimage.host/)

Use this case on a known 'And' to create a split in the branch where the surronding expressions will satisfy the condition

### Atomic Case

[![Hn3w9qb.jpg](https://iili.io/Hn3w9qb.jpg)](https://freeimage.host/)

Use this case on a unknown variable to create a split in the branch where the variable is true in one branch, and false in another

### Biconditional Case

[![Hn3wqI1.jpg](https://iili.io/Hn3wqI1.jpg)](https://freeimage.host/)

Use this case on a known 'Biconditional' to create a split in the branch where the surronding expressions will satisfy the condition

### Conditional Case

[![Hn3w7It.jpg](https://iili.io/Hn3w7It.jpg)](https://freeimage.host/)

Use this case on a known 'Conditional' to create a split in the branch where the surronding expressions will satisfy the condition

### OR Case

[![Hn3wVv2.jpg](https://iili.io/Hn3wVv2.jpg)](https://freeimage.host/)

Use this case on a known 'Or' to create a split in the branch where the surronding expressions will satisfy the condition


## Contradiction Rules

### AND Contradiction

[![Hn3jTb9.jpg](https://iili.io/Hn3jTb9.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'And' is incorrect based on the surronding expressions

### Variable Contradiction

[![Hn3ja0x.jpg](https://iili.io/Hn3ja0x.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value a variable in two locations has two different states

### Biconditional Contradiction

[![Hn3ja0x.jpg](https://iili.io/Hn3ja0x.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Bicondtional' is incorrect based on the surronding expressions

### Conditional Contradiction

[![Hn3jEOP.jpg](https://iili.io/Hn3jEOP.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Condtional' is incorrect based on the surronding expressions

### NOT Contradiction

[![Hn3jw0v.jpg](https://iili.io/Hn3jw0v.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Not' is incorrect based on the surronding expression

### OR Contradiction

[![Hn3jveI.jpg](https://iili.io/Hn3jveI.jpg)](https://freeimage.host/)

Use this rule to end a line of reasoning if the value of the 'Or' is incorrect based on the surronding expressions


## Basic rules

### True or False Rule

[![Hn3hHZu.jpg](https://iili.io/Hn3hHZu.jpg)](https://freeimage.host/)

The same variable must hold it's truth value in all cases, Use this rule to assign all of a given variable the same value

### AND Elimination

[![Hn3hnu1.jpg](https://iili.io/Hn3hnu1.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'And' State

### Biconditional Elimination 

[![Hn3h5ap.jpg](https://iili.io/Hn3h5ap.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'Biconditional'  State

### Conditional Elimination 

[![Hn3h5ap.jpg](https://iili.io/Hn3h5ap.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'Conditional' State

### NOT Elimination 

[![Hn3h8Mb.jpg](https://iili.io/Hn3h8Mb.jpg)](https://freeimage.host/)

Use this rule to assign an expression a truth value depending on the 'Not' State

### OR Elimination 

[![Hn3hSPj.jpg](https://iili.io/Hn3hSPj.jpg)](https://freeimage.host/)

Use this rule to color an expression green or red depending on the 'conditional' State

### AND Introduction

[![Hn3hiAP.jpg](https://iili.io/Hn3hiAP.jpg)](https://freeimage.host/)

Use this rule to Assign the 'And' a truth value on the the surronding expressions

### Biconditional Introduction

[![Hn3hLDF.jpg](https://iili.io/Hn3hLDF.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Bicontional' a truth value on the the surronding expressions

### Conditional Introduction 

[![Hn3hLDF.jpg](https://iili.io/Hn3hLDF.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Condtional' a truth value on the the surronding expressions

### NOT Introduction 

[![Hn3jFxn.jpg](https://iili.io/Hn3jFxn.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Not' a truth value on the the surronding expressions

### OR Introduction 

[![Hn3jFxn.jpg](https://iili.io/Hn3jFxn.jpg)](https://freeimage.host/)

Use this rule to Assign the 'Or' a truth value on the the surronding expressions


# Truth Table Rules
### Here are the basic rules of the puzzle

AND Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       F       |
|       F           |       T           |       F       |
|       F           |       F           |       F       |

Conditional Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       F       |
|       F           |       T           |       T       |
|       F           |       F           |       T       |

Biconditional Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       F       |
|       F           |       T           |       F       |
|       F           |       F           |       T       |

OR Expression Truth Table

| Left Expression     | Right Expression    | Truth State   |
| :----:            |    :----:         |     :----:    |
|       T           |       T           |       T       |
|       T           |       F           |       T       |
|       F           |       T           |       T       |
|       F           |       F           |       F       |

NOT Expression Truth Table

|  Expression       | Truth State   |
| :----:            |    :----:     | 
|       T           |       F       |   
|       F           |       T       |   

