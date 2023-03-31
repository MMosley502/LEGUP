# Strategy to solve puzzles
## Here are the general steps you can take to solve the Nurikabe puzzle

### Step 1: Close cells adjacent to 1s

![image](https://user-images.githubusercontent.com/96987732/226740844-4a2deefe-e2a8-4f87-8b14-5e9cf5b6e6a2.png)

### Step 2: Close any cell between two numbers

![image](https://user-images.githubusercontent.com/96987732/226740957-5a5dd5b9-4653-4ce4-abdb-ff2130ef1b55.png)

### Step 3: Identify "Realms"
* Realms are cells with reach on the board. 
* It is recommended to start with cells that have the Maximum reach. 
* When considering reach, disregard open and closed cells

![image](https://user-images.githubusercontent.com/96987732/226741528-ef59a733-4fa7-416e-91b6-31bee71fd27e.png)

### Step 4: Overlay all Realms

![image](https://user-images.githubusercontent.com/96987732/226742026-2738a873-58cd-497a-94a9-3320be7429c1.png)

### Step 5: Close any cell not covered by any of the Realms 

![image](https://user-images.githubusercontent.com/96987732/226742226-17de951f-77f9-4563-9bb8-3ae434163c95.png)

### Step 6: Check for cells that are forced open. 
* If any realm contains the number of cells as the contained number make them all open

![image](https://user-images.githubusercontent.com/96987732/226743107-3523436f-6002-4e9e-83e0-df26dfa4ca0d.png)

### Step 7: Reduce maximum reach
* If an open cell is only covered by one realm, it belongs to that number
* Because of this, the coverage of the realms will shrink to be able to connect to the open cell
* Repeat from step 5

### Step 8: Remove cells adjacent to open cells
* Any cell adjacent to an open cell that belongs to a different realms should be closed
* Repeat from step 5 again

### Step 9: Check for blocks of 3 closed, and check what block is forced open

![image](https://user-images.githubusercontent.com/96987732/226745145-438aca2e-722e-4a77-a00e-52c74f6452f4.png)

### Step 10: Check for blocks of 2 closed
* A block of 2 indicates that at least one of the other 2 must be open. If the 2 unmarked are in only one realm, at least one of the 2 must be connected to that number. If one cell must be Open for the other to be, then the first cell must be Open. This will reduced the maximum reach of the realm (Step 7).
* If each of the unmarked cells is in only 1 realm and the realms are not the same, one of the cells must be closed