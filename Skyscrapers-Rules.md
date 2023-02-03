# Skyscrapers
Skyscrapers is a puzzle with unfilled squares shown in gray. Your task is to fill all the squares with numbers without breaking the rules of the game.

Clicking on a tile increases the number in the square by 1, up to the width of the board.

Clicking on a tile of max height returns it to blank.

# Rules 
### Here are the direct rules of the puzzle

1) Each row and column must contain the numbers 1-N, N being the width of the board.

2) The numbers outside the board indicate the number of buildings visible from that perspective in that row or column. A larger number indicates a taller building, and taller buildings obscure the smaller buildings behind them.

# LEGUP Proof Rules
## Case Rules

### Cell For Number 

![CellForNumber](https://user-images.githubusercontent.com/98851950/202821671-47455459-ac44-47dd-9724-0693d63352d4.png)


Use this rule to create a branch in the proof for each possible location of the given number along the given row of column. Does not branch into cases that create a duplicate contradiction.


### Number For Cell

![NumberForCell](https://user-images.githubusercontent.com/98851950/202821690-a66e8f13-857a-4924-977a-87874ffb961a.png)


Use this rule to create a branch in the proof for each possible value of the given cell. Does not branch into cases that create a duplicate contradiction.

## Contradiction Rules

### Duplicate Number

![DuplicateNumber](https://user-images.githubusercontent.com/98851950/202822278-f6d2f943-4f42-40d4-9bd1-75692b4fab5d.png)


This can be easily derived from Rule #1. Use this when a number appears twice in a row or column

### Unresolved Number

![UnresolvedNumber](https://user-images.githubusercontent.com/98851950/202822254-82d585be-f55d-4041-a257-2d040522975e.png)


Comes from Rule #1. Use this when Cell For Number returns no cases.

### Unresolved Cell

![UnresolvedCell](https://user-images.githubusercontent.com/98851950/202822264-e9e21ef7-91ca-44e0-898c-3f9f6069af25.png)


Comes from Rule #1. Use this when Number For Cell returns no cases.

### Too Few Visible

![InsufficientVisibility](https://user-images.githubusercontent.com/98851950/202822465-b5925c84-97e5-4aeb-b8e6-ac681cdf5e02.png)


Derived from Rule #2. Use this when a full row/col has fewer buildings visible than the rule.

### Too Many Visible

![ExceedingVisibility](https://user-images.githubusercontent.com/98851950/202822483-576203d2-e460-45b2-b7e7-5e25b1ede9e5.png)


Derived from Rule #2. Use this when a full row/col has more buildings visible than the rule.

### Preemptive Visibility

![PreemptiveVisibility](https://user-images.githubusercontent.com/98851950/202822588-cc098bf3-6fe2-4fc1-8e9f-418a35ac2160.png)


Derived Rule #2. Use this when the row/col isn't full yet, but a visibility contradiction is inevitable.

## Direct Rules

### N-Edge

![NEdge](https://user-images.githubusercontent.com/98851950/202823052-366ba057-c863-4f65-a376-6cfee62aac5c.png)


A combination of Rules #1 and #2. Use this when N, the width of the board, appears as a clue. The numbers must appear in order increasing away from that clue.

### Last Non-Duplicate Cell

![LastCell](https://user-images.githubusercontent.com/98851950/202823048-57f768a5-73a3-48a0-9355-fb338fd2d657.png)


From Rule #1. Use this when there is only one Cell For Number that does not create a Duplicate Contradiction.

### Last Non-Duplicate Number

![LastNumber](https://user-images.githubusercontent.com/98851950/202823038-94899ffb-4f38-4305-875e-052369bd0c66.png)


From Rule #1. Use this when there is only one Number For Cell that does not create a Duplicate Contradiction.

### Last Visible Cell

![FixedMax](https://user-images.githubusercontent.com/98851950/202823022-7b011609-749b-49b3-8cf6-39dd5d207bc3.png)


From Rule #2. Use this when there is only one Cell For Number that does not create a Preemptive Visibility Contradiction.

### Last Visible Number

![OneEdge](https://user-images.githubusercontent.com/98851950/202823012-e52a2df3-fa0b-4dbf-b6b9-f2be046d5e8c.png)


From Rule #2. Use this when there is only one Number For Cell that does not create a Preemptive Visibility Contradiction.