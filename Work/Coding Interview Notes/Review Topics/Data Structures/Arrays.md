Arrays

Goals:
1) Understand the structure of each and how they conceptually function
2) Learn how to implement the data structure itself
3) Understand how basic operations function/Learn how to implement them and their space/time complexity
  a) Traversal
  b) Insertion
  c) Deletion
  d) Searching
  e) Sorting
  f) Reversal
  g) Rotation
  h) Rearranging
  i) Merging
4) Other factors to consider
5) Understand what they are good and bad at and when to use them

https://www.geeksforgeeks.org/introduction-to-arrays/

1) Structure/Function:

- Arrays are a linear data structure
- "An array is a collection of items of the same data type stored at contiguous memory locations."
- Arrays have data of the same datatype placed in incremented indexes starting at 0
- They store elements at contiguous locations in memory
  - Are all stored successively, so all next to each other evenly spaced based on size of datatype in each element
  - Difference between two indexes is known as the offset
- A basic array has a fixed size, meaning size cannot be shrunk or expanded
  - Memory is statically allocated

2) Implementation:

Arrays can be implemented in several different ways:

a) Initializing with no values
  - Size is defined but no values are passed, making an empty array
b) Initializing with specific values
  - Can define size and pass values
 
3) Basic Operations Function

a) Traversal (O(1))
  - Arrays allow random access, meaning we can easily use the index to specifically access any element by position that we want

b) Insertion (O(n))
  - To replace a value to a particular array index position, can just access and directly assign using index (O(1))
  - However, if wanting to insert value at position without replacing, would take O(n) time as all other elements after must be shifted right
    - This is slightly worse if array is full and new array must be created, as this would take O(n) time to copy best case (in Java may not be the case)
    - If inserting at end, O(1) in either case

c) Deletion (O(n))
  - To delete a value, access using index, then reassign to next value and continue until end of array, essentially shifting left
  - Set last element in array to empty/null value
  - If given element to delete rather than index, must search then delete (same complexity regardless of search used)

d) Searching
  There are many different ways to search using arrays but the basic most efficient are below:
  1) Unsorted - Basic search over elements (O(n))
    - Must access all array elements and look for particular value
    - This is the only efficient way to search in an unsorted array
  2) Sorted - Binary search (O(log n)) (O(log n) space for recursive calls)
    - Refer to binary search file for implementation

e) Sorting
  Merge and quick sort are good ones. Refer to file for reference.

f) Reversal
  This essentially swaps the outermost elements and moves inwards until the whole array is reversed. 
  1) Using start and end index, loop while incrementing start index and decrementing end index until they meet
  2) For each step of the loop, swap the start index element with the end index element

g) Rotation
  1) Using temp array: (O(n) time/space)
    After rotating d positions to the left, the first d elements become the last d elements of the array
    a) Keep track of index of temp array
    b) Store elements from index d to N-1 into the temp array
    c) Store first d elements of original array into temp array
    d) Copy back elements of temp array into original array

  2) Rotate by one (O(n * d) time, O(1) space)
    a) For each iteration, shift elements by one position to left circularly (first element becomes last)
    b) Perform d times to rotate elements to left by d position

  3) Juggling method (extension of 2) (O(n) time, O(1) space)
    Instead of moving one at a time, divide array into different sets where number of sets is equal to GCD of N and d (say X. so elements x distance apart are part of a set) and rotate elements within sets by one position to left
    a) Calculate GCD between length and the distance to be moved
    b) Elements are only shifted within sets
    c) Start with temp = arr[0], keep moving arr[l+d] to arr[l] and finally store temp at the right place

  Official steps:

  1) Perform d%n in order to keep the value of d within the range of the array where d is the number of times the array is rotated and N is the size of the array.
  2) Calculate the GCD(N, d) to divide the array into sets.
  3) Run a for loop from 0 to the value obtained from GCD.
    a) Store the value of arr[i] in a temporary variable (the value of i denotes the set number).
    b) Run a while loop to update the values according to the set.
  4) After exiting the while loop assign the value of arr[j] as the value of the temporary variable (the value of j denotes the last element of the ith set).

Other rotation methods to consider:
  - Block swap
  - Reversal algorithm

  4) Reversal algorithm for rotation (O(n) time, O(1) space)
    a) Reverse first 'd' elements
    b) Reverse last (N-d) elements
    c) Reverse whole array

  5) Block swap reversal (O(n) time, O(1) space)
    Initialize A = arr[0..d-1] and B = arr[d..n-1]
    1) Do following until size of A is equal to size of B
      a)  If A is shorter, divide B into Bl and Br such that Br is of same length as A. Swap A and Br to change ABlBr into BrBlA. Now A is at its final place, so recur on pieces of B with n-d size. 
       b)  If A is longer, divide A into Al and Ar such that Al is of same length as B Swap Al and B to change AlArB into BArAl. Now B is at its final place, so recur on pieces of A with n-d size. 
    2)  Finally when A and B are of equal size, block swap them.

h) Rearranging
  Rearranging in arrays requires some form of navigation and swapping/replacement operation. e.g:
  
Rearrange an array such that arr[i] = i

  1) Naive Approach (O(n^2))
    a) Navigate the numbers from 0 to n-1.
    b) Now navigate through array.
    c) If (i=a[j]) , then replace the element at i position with a[j] position.
    d) If there is any element in which -1 is used instead of the number then it will be replaced automatically.
    e) Now, iterate through the array and check if (a[i]!=i) , if it s true then replace a[i] with -1.

  2) Another (O(n))
    a) Navigate through the array. 
    b) Check if a[i] = -1, if yes then ignore it. 
    c) If a[i] != -1, Check if element a[i] is at its cor­rect posi­tion (i=A[i]). If yes then ignore it. 
    d) If a[i] != -1 and element a[i] is not at its cor­rect posi­tion (i!=A[i]) then place it to its correct position, but there are two conditions:  
      - Either A[i] is vacate, means A[i] = -1, then just put A[i] = i .
      - OR A[i] is not vacate, means A[i] = x, then int y=x put A[i] = i. Now, we need to place y to its correct place, so repeat from step c.

  3) Set implementation (O(n) time and space)
    a) Store all the numbers present in the array into a Set 
    b) Iterate through the length of the array, if the corresponding position element is present in the Set, then set A[i] = i, else A[i] = -1 

  4) Swap in array (O(n))
    Using cyclic sort
    a) Iterate through elements in an array 
    b) If arr[i] >= 0 && arr[i] != i, put arr[i] at i ( swap arr[i] with arr[arr[i]])

i) Merging
  Merge two sorted arrays (No regard for space)
  1) Brute force (O((m+n)log(m+n)) time, O(1) space)
    a) Take all elements of arr1 and arr2 and place in arr3.
    b) Simply sort arr3
  2) Merge sort style (O(n1 + n2) Time and O(n1 + n2) Extra Space) 
    a) Create arr3 size n1+n2
    b) Simultaneously traverse arr1 and arr2
      - Pick smaller of current, add to arr3 then step forward in that array
      - Stop when reached end of one array
    c) Add remaining of other array not finished to end of arr3
  3) Maps (O(n log(n) + m log(m)) time, O(N) space)
    a) Insert elements of both arrays in map as keys
    b) Print keys of map

  The following are all O(1) space
  4) O(m\*n) 
  Iterate through every element of ar2[] starting from last element. Do following for every element ar2[i]
    a) Store last element of ar1[i]: last = ar1[i]
    b) Find smallest element greater than ar2[i]
    c) Move all elements one position ahead until smallest greater element is not found
    d) If there was a greater element, place last of ar1 in ar2[i] and ar2[i] in position found

  Actual implementation:
    a) Store last element of ar1[i]: last = ar1[i]
    b) Loop from last element of ar1[] while element ar1[j] is 
       greater than ar2[i].
          ar1[j+1] = ar1[j] // Move element one position ahead
          j--
    c) If any element of ar1[] was moved
          ar1[j+1] = ar2[i] 
          ar2[i] = last

  Worst case when all elements of ar1 are greater than all elements of ar2.

  5) Optimized of 4 - Traversing both parallely O((n+m)log(n+m)
    If encounter jth second array element is smaller than ith first array element, jth element should be included and replace some kth element in first array
    a) Initialize i,j,k as 0,0,n-1 where n is size of arr1 
    b) Iterate through every element of arr1 and arr2 using two pointers i and j respectively
      if arr1[i] is less than arr2[j]
        increment i
      else
        swap the arr2[j] and arr1[k]
        increment j and decrement k

    c) Sort both arr1 and arr2 
    Worst case traversal is O(n+m), worst case sorting is O(nlog(n)+m(logm))

  6)  Simple and efficient (O(n*m))
    a) Initialize i with 0
    b) Iterate while loop until last element of array 1 is greater than first element of array 2
          if arr1[i] greater than first element of arr2
              swap arr1[i] with arr2[0]
              sort arr2
          incrementing i 

  7) Partitioning arrays (O(min(nlogn, mlogm)))
  Let the length of the shorter array be ‘m’ and the larger array be ‘n’
    a) Select shorter array and find index at which partition should be done
      1. Partition shorter array at median (l1) 
      2. Select first n-l1 elements from second array
      3. Compare border elements
        - If l1 < r2 and l2 < r2 we have found index
        - else if l1 > r2 we have to search left subarray
        - else have to search right
  NOTE : This step will store all the smallest elements in the shorter array.
    b) Swap all elements right of index(i) of shorter array with first n-i elements of larger array
    c) Sort both of the arrays
    - if len(arr1) > len(arr2) all the smallest elements are stored in arr2 so we have to move all the elements in arr1 since we have to print arr1 first.
      d) Rotate larger array (arr1) m times counter clockwise
      e) Swap the first m elements of both the arrays

  8) Insertion sort w/ simultaneous merge (O(m*n))
    a) Sort list 1 by always comparing first element of list 2 and swapping if required
    b) After each swap, perform insertion of swapped element into correct position in list 2 which will eventually sort list 2 at the end.
      - For every swapped element from list 1, perform insertion sort in list 2 to find its correct position so that when list 1 is sorted, list 2 is also sorted.

  9) Euclidean Division Lemma (O(m+n))
    Just merge the two arrays as we do in merge sort, while simultaneously using Euclidean Division Lemma, i.e. (((Operation on array) % x) * x). And at least after merging divide both the arrays with x. Where x needs to be a number greater than all elements of array. Here in this case x, (according to the constraints) can be 10e7 + 1.
  Refer back to this later: https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/

Others to consider:
- Merge k sorted arrays
  - https://www.geeksforgeeks.org/merge-k-sorted-arrays/
  - Minheap solution

4) Other factors

a) Multi-dimensional arrays
  - Stored in memory in row-major order
  - Accessing elements
    - Access is still using indexes, with a separate index for each dimension to find a specific element
  - To output all elements, need number of nested loops equal to number of dim.
b) Jagged array
  - Array of arrays s.t. member arrays can be of different sizes
  - Syntax: data_type array_name[][] = new data_type[n][];  //n: no. of rows
             array_name[] = new data_type[n1] //n1= no. of columns in row-1
             array_name[] = new data_type[n2] //n2= no. of columns in row-2
             array_name[] = new data_type[n3] //n3= no. of columns in row-3
                                   .
                                   .
                                   .
             array_name[] = new data_type[nk]  //nk=no. of columns in row-n

5) Advantages/Disadvantages:

+++
1) Good at random access
2) Better cache locality as memory blocks are contiguous
  - When computer goes to memory to access data, other members of array are already loaded into cache and have faster access
  - In another data structure like a linked list, the other members can be stored anywhere in memory, so often takes multiple trips to memory to find multiple members
3) Represent multiple data items of same type using single name

---
1) Size of array cannot be changed after declaration because of static memory allocation
2) Bad at insertion/deletion (O(n))
  - Especially at beginning
  - Works by shifting all elements right of index if adding then filling empty index, if deleting shifting all elements right to left to fill empty index
3) Bad at memory usage for many applications
  - e.g. stack as array, POPing an element simply changes pointer/view
    - Element stays taking up memory space, even if changed to null
  - Less of an issue for primitive data type but bigger for objects

7) Good Uses/Applications:

Good uses:
a) Good when size of data set is known
b) Used in solving matrix problems. 
c) Helps in implementing sorting algorithm.
d) The different variables of the same type can be saved under one name. 
e) Used to Implement other data structures like Stacks, Queues, Heaps, Hash tables, etc.

Real life applications:
- Applied as a lookup table in computer.
- Databases records are also implemented by the array.