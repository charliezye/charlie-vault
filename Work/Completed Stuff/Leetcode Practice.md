
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
4. Sol was O(m^2) and O(m), with heap and binary search could reduce to O(n log n)

##### 7) Two Sum
1. Did everything almost correct but when solution did not work properly overthought
2. Did not initially consider that should not look at self so should not put value into hashtable for lookup until after looking up
3. If doing double access like sum of every pair and want to use hashtable:
	1. Check against hashtable first then put into table
	2. This way for each value we are comparing against all values before in an efficient way
		1. No need to make sure not checking against self, no need to worry about duplicates
	2. Simply need to make sure that in answer, returning correct index because i when answer is found is technically higher index

##### 8) Add Two Numbers
1. Solution seems correct at first but when writing code need to make a lot of small adjustments
	1. Think more through algo before writing out
2. Failed submission twice because of small mistakes (forget sections of code)
	1. Consider edge cases one by one running example through code written
2. Could have avoided head null checks by adding empty node in front and returning next

##### 9) Longest Substring
1. Had right idea to use a map here rather than set, should have stored index as I initially thought
	1. Actually did not need to store indexes could still have used set!!
2. Also had right idea for two pointers
	1. Should have considered early on if I needed to actually store substring
		1. If not should have further considered if I just need to store two integers, which was the case
4. Can use Math.max(i,j) when changing max rather than using operators
5. Use i++ operator within functions if going to be written on next line anyways

##### 1578. Minimum Time to Make Rope Colorful
1. Overthought the hell out of the problem which threw me completely off track
2. Slightly more complex solution than needed
	1. Iterating comparing 2 at a time instead of just getting sum of all but highest in group
2. Better when comparing pairs to compare to one behind and increment by 1


---
---

#### Study Plans

##### Programming Skills II
###### 896. Monotonic Array
- Easy does it, only critique is making sure if checking index i and i+ or -1 I don't index past beg/end of array
- Also don't feel bad about using two var to check if it will make it easier

###### 28. Index of First Occurrence
- Missed two edge cases:
	- Needle larger than haystack (index out of bounds)
	- Checking needle goes after 
- If want to run operation at end of array/string without running outside of loop can check if iterator equal to last index
- Can add AND/OR operators within for loop statement next to i \< length

---

##### Dynamic Programming I
###### 509. Fibonacci Number
- First time ran failed as did not account for edge/base cases again

###### 1137. N-th Tribonacci Number
- Overthought how large array needed to be (still only n+1 size needed)

---

##### SQL I

###### 595. Big Countries
- Fucked it using AND instead of OR, read problem more carefully

###### 1757. Recyclable and Low Fat Products
- Ezpz

###### 584. Find Customer Referee
- WHERE will ignore null values if compared, even if using <> comparison
	- Use IFNULL(column, \<valid val\>) to account for this

###### 183. Customers Who Never Order
- Make sure to double check return values/column name in example
- Make sure selecting correct fields

###### 1873. Calculate Special Bonus
- Can use % instead of MOD
- Can use '%' in string as 
- Can use CASE WHEN __ THEN __ ELSE __ END

##### Data Structure II

###### 136. Single Number
- Bit manipulation, easy but didn't know wtf I was doing

###### 169. Majority Element
- Panicked, didn't know where to start
- Didn't see clever solution of knowing must have 2 consecutive same number and must have more consecutive than any other if greater than half

###### 15. Three Sum
- Nested arraylist can just have list inside
- To use set iteration:
	- Iterator itr = set.iterator()
	- while(itr.hasNext())
	- itr.next()
- On right track with picking first two, but wrong about searching for third
	- Could have just picked then did internal loop for third