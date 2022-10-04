# Dynamic Programming

Goals:
1. Understand conceptually how each of them work.
2. Learn how to implement them and any operations involved with them. 
3. Understand how they interact with the algorithms and data structures above.
4. Learn what each is good and bad at and when to use them

## How it Works

- Primarily an optimization over plain recursion's repeated calls for the same inputs
- Simply store results of subproblems so we do not have to recompute them later
- Reduces time complexities from exponential to polynomial

### Main Properties of DP Problem
- These are the properties that suggest a problem can be solved with DP

#### 1) Overlapping Subproblems

- Similar to Divide and Conquer, DP combines subproblem solutions
	- Solutions are stored in a table for quick access
- If no common subproblems, DP is not effective
	- e.g. Binary Search has none, Fibonacci has many

##### Ways to Store Values

###### 1. Memoization (Top Down)

- Similar to recursive version of program with small modification looking into lookup table before computing solutions
- Uses recursion

###### Steps
1. Init lookup structure 
	1. Can be max array but should prob be hash map
2. When solution to subproblem is needed, first look into lookup table
	1. If precomputed value there, return it
	2. Otherwise, calculate value and put result in lookup table

###### Advantages
1. Subproblems are solved lazily, only computations needed are carried out as called

###### Disadvantages
1. Slower than tabulation by a constant factor
2. Less space efficient as recursion requires call stack for first computation though it will release after this
	1. Additionally must use dynamically allocated data structure instead of preallocated

###### 2. Tabulation (Bottom Up)

- Builds table in bottom-up fashion and returns last entry from table
	- E.g. calculate fib(0), then fib(1), etc.
- Literally build solutions bottom-up
- Iterative solution

###### Steps
1. Allocate data structure (often array)  with appropriate size
2. Save base cases
3. Iteratively build up to size needed based on input from these base cases

###### Advantages

1. Faster than memoization by a constant factor
2. More space efficient as data structure is preallocated and iterative instead

###### Disadvantages
1. Subproblems are all solved first, so will often do extra constant time work

###### Example: Fibonacci Numbers

Memoization
1. Init lookup table
2. Check for input in lookup table
	1. If not there, return base case or recursively call fib(n-1) + fib(n-2)
	2. Else return from lookup table

Tabulation
1. Init lookup table to size n+1
2. Set base cases at 0 and 1 index of lookup
3. Iteratively build up using table[n] = table[n-1] + table[n-2]
4. Return value at n

##### HOW TO PICK
1. Do all subproblems need to be solved?

Use tabulation, more space efficient and slightly faster.

2. Do only some need to be solved?

Use memoization, lazy solving so will compute less.

##### 2) Optimal Substructure

- This property means the **optimal solution** can be obtained using the **optimal solution to its subproblems** rather than trying **every possible way** to solve the subproblems

###### Example: Shortest Path
- If a node x lies in the shortest path from a source node **U** to destination node **V** then the shortest path from **U** to **V** is a combination of the shortest path from **U** to **X** and the shortest path from **X** to **V**