## Study Topics Completed

----------------------------------------------------------------

### Data Structures:

1) Linked Lists
 - [x] 1. Notes ✅ 2022-09-26
 - [ ] 2. Implementation Practice
2) Trees, Tries, & Graphs
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
3) Stacks & Queues
  - [x] 1. Notes (DONE) ✅ 2022-09-26
  - [ ] 2. Implementation Practice
4) Heaps
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
5) Vectors/ArrayLists
  - [x] 1. Notes (DONE) ✅ 2022-09-26
  - [ ] 2. Implementation Practice
6) Hash Tables
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice

----------------------------------------------------------------

### Algorithms:

1) BFS
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
2) DFS
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
3) Binary Search
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
4) Merge Sort
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
5) Quick Sort
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice

----------------------------------------------------------------

### Concepts:

1) Bit Manipulation
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
2) Memory (Stack vs) Heap)
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
3) Recursion
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
4) Dynamic Programming
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice
5) Big O Time & Space
  - [ ] 1. Notes (DONE)
  - [ ] 2. Implementation Practice
6) Generics 
  - [ ] 1. Notes
  - [ ] 2. Implementation Practice

----------------------------------------------------------------
----------------------------------------------------------------

## Leetcode Practice Problems Completed

----------------------------------------------------------------

##### 1) Roman numerals to integers (String)
  1. Problems/Takeaways
    1. Considered error checking too early and wrote too complex algorithm
      - Takeaway: Write algorithms FIRST then consider error checking.
    2. Abandoned my brute force idea which ended up being pretty close
      - Takeaway: Some problems may be easier than I think, don't assume hard.
    3. Didn't write out algorithm enough on paper or questions
      - Takeaway: Write questions to ask interviewer
      - Takeaway: Fully think through each section of code
    4. My map initialization was pretty long-form and inefficient to write
      - Takeaway: Use Map.of() up to 10, then Map.ofEntries(entry()) for 10+
      - Consider python too because it's as simple as {Key:val}
    5. Working with strings seems much more complex in Java because cannot simply index, .charAt and .subString are a lot more to write

##### 2) Palindrome Linked List (LL)
  1) Problems/Takeaways
    1. Forgetting to use variable type when defining
    2. Forgetting syntax such as ;
    3. Need to use pointers to head not change head itself
    4. Trouble coming to solution
      1. Continue to explore what comes to mind first
      2. Reversal was a good idea but at first dismissed and almost lost optimal solution
    5. Overthought size calc
    6. Don't mess up closing brackets, double check
    7. Midpoint calculation: Optimal is slow/fast pointer?
    8. Slight reversal improvement: move next assignment into loop

##### 3) Ransom Note (Strings)
  1. String.indexOf() checks if char present in string, index of or -1 if not occur
  2. To splice string/remove char can use substring() of before and after and add
    1. No capitals in substring!!
  3. Again, don't forget to use variable types before assigning new!!!!!
  4. Alt sol: use array with indexes representing letters
  5. Don't forget that using storage with FIXED size is fine
    1. Almost had other optimal solution but strayed away because of idea that using data structures makes O(1) space, may be simpler to use storage

##### 4) FizzBuzz
  1. Done it before
  2. Just add directly, no need to build string then add

##### 5) Middle of Linked List
1. Perfect example of why writing code for methods is important
2. NullPointerException
	1. Be very careful to not put self in situation where referencing instance field or method of a null value 
	2. If calling next in repeated fashion more than once, always check if current and next are null

##### 6) K Weakest Rows
1. Didn't know how to use heap/binary search which would be best
2. Overthought using arrays, can't store index and value
	1. Don't need to use arraylist when size needed is known, consider this next time
	2. If feel need to store both and sort (no map), probably doing something wrong
	3. Use other data structure to sort
3. Need to study writing basic methods