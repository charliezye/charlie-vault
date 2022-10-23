Goals:
1) Understand the structure of each and how they conceptually function
2) Learn how to implement the data structure itself
3) Understand how basic operations function
4) Learn how to implement basic operations and their space/time complexity
a) Traversal
b) Insertion    
c) Deletion
d) Searching
e) Sorting
f) Merging
5) Other factors to consider
  - Input: How data will be received
  - Processing: How data is manipulated in the structure (how it's changed to accomodate other data)
  - Maintaining: How data is organized within structure
  - Retrieving: Accessing and returning data
6) Understand what they are good and bad at and when to use them

References:

Stack:
https://www.geeksforgeeks.org/stack-data-structure-introduction-program/

Queue:
https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/


2) Structure/Function

a) Stack

- A linear data structure following LIFO for operations, last in first out.
  - In other words, insertion and deletion must happen at same end (top)
- Real life example of this would be a stack of plates. The plate put on last is the top, and since we can only remove the plate at the top, it can be said that the last plate put on comes out first.

Other Types of Stacks:

- Register stack
  - A memory element present in the memory unit and can handle a small amount of data only. Height is always limited as much smaller than memory.
- Memory stack
  - Can handle large amount of memory data, flexible as occupies large amount of memory data

b) Queue

- A linear data structure following FIFO for operations, first in first out.
  - Insertion and deletion occur at opposite ends (rear and front)
- A real life example is people waiting in line to receive something, first customer who came is served first.

Other Types of Queues:
- Circular queue
  - Elements act as circular ring
  - Working is same except last element connected to first
  - Better utilizes memory as if there is an empty position an element can easily be added there
- Priority queue
  - Arranges elements based on some priority such that highest priority is at end of queue
- Dequeue
  - Elements can be inserted or removed from both ends of the queue (not necessarily FIFO)


----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

2) Implementations

Stack

a) Using array

  1. Create array of maximum size (or as needed)
  2. Store counter starting at zero to keep track of top index
  3. Implement operations as shown below

Importantly, in this implementation can save several lines of code by using ++top and top-- operations to increment and decrement top while returning or setting values.

+++
- Easy to implement
- Less memory as no pointers needed

---
- Not dynamic
- Doesn't grow and shrink based on needs at runtime
- Total size of stack must be defined before

b) Using linked list

Only singly linked list is required and new nodes are added at the head.

  1. Create stack node class
  2. Implement operations as shown below

+++
- Can grow and shrink according to needs at runtime
- Used in many virtual machines such as JVM
- More secure and reliable as they do not get corrupted easily
- Cleans up objects automatically

---
- Requires additional memory due to pointers
- Random accessing not possible
- If the stack falls outside the memory it can lead to abnormal termination.

c) Using queues

Can be implemented using two queues or in final case one. 

1. Push costly

  This method ensures that the newly entered element is always at the front of ‘q1’ so that pop operation dequeues from ‘q1’. ‘q2’ is used to put every new element in front of ‘q1’.

  - push(s, x) operation’s steps are described below: 
    - Enqueue x to q2
    - One by one dequeue everything from q1 and enqueue to q2.
    - Swap the names of q1 and q2
  - pop(s) operation’s function is described below: 
    - Dequeue an item from q1 and return it.
  
  Push: O(n), Pop: O(1), Space: O(n) b/c two queues

2. Pop costly

  In a push operation, the new element is always enqueued to q1. In pop() operation, if q2 is empty then all the elements except the last, are moved to q2. Finally, the last element is dequeued from q1 and returned.

  - push(s, x) operation: 
    - Enqueue x to q1 (assuming size of q1 is unlimited).
  - pop(s) operation: 
    - One by one dequeue everything except the last element from q1 and enqueue to q2.
    - Dequeue the last item of q1, the dequeued item is result, store it.
    - Swap the names of q1 and q2
    - Return the item stored in step 2.

  Push: O(1), Pop: O(n), Space: O(n) b/c two queues=

3. One queue

  - The idea behind this approach is to make one queue and push the first element in it. 
  - After the first element, we push the next element and then push the first element again and finally pop the first element. 
  - So, according to the FIFO rule of the queue, the second element that was inserted will be at the front and then the first element as it was pushed again later and its first copy was popped out. 
  - So, this acts as a stack and we do this at every step i.e. from the initial element to the second last element, and the last element will be the one which we are inserting and since we will be pushing the initial elements after pushing the last element, our last element becomes the first element.

  Push: O(n), Pop: O(1), Space: O(n) b/c two queues
  Functionally, works the same as 1. but dequeue and enqueuing to itself.

----------------------------------------------------------------------------------

Queue


a) Using Array

  1. Keep track of two indices of array: Front and Rear
  2. Enqueue at rear, dequeue at front
  3. To avoid front reaching end of array, increase front and rear in a circular manner instead of incrementing both
    a. This is accomplished by increment index of front/rear and using modulus with capacity of queue array to move index back to front whenever past maximum index of array

+++
- Easy to implement
- Large amount of data managed efficiently with ease
- Insertion and deletion performed easily

---
- Static data structure with fixed size
- (fixed by circular queue implementation above) If large number of enqueue and dequeue operations, at some point may not be able to insert even if queue is empty

b) Using Linked List
  
  1. Keep track of two pointers to nodes, front and rear
  2. To enqueue, add new node to next of rear and move rear to next (new) node
  3. To dequeue, remove front node and return and move front pointer to next node
    a. If front ever becomes null, also set rear to null. This means the queue is empty.

+++
- Can grow and shrink according to needs at runtime

---
- Requires additional memory due to pointers
- Random accessing not possible
- If the stack falls outside the memory it can lead to abnormal termination.


----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

3) Basic Operations

There is no traversal in these as you can only access the one element at a time. Importantly, these operations below are the default basic built in operations for each. Others detailed at the top are in part 4).

Stack

a) push (insertion) (O(1))
  - Adds an item to the stack. If it is full, then it is an overflow condition
  1. Check if stack is full
  2. If not, increment top and assign value at new top

b) pop (deletion/removal) (O(1))
  - Removes item from stack in reverse order of pushed. If empty, underflow condition
  1. Check if stack is empty
  2. Store value at top, decrement top, return value

c) peek/top (access) (O(1))
  1. Return value at top

d) isEmpty (O(1))
  1. Check if top is 0, if it is then empty

e) size (O(1))
  1. Return top 

----------------------------------------------------------------------------------

Queue

a) enqueue (insertion) (O(1))
  - Adds an item to the queue. If it is full, then it is an overflow condition
  1. Check if queue is full
  2. If not, increment tail and add element
b) dequeue (deletion/removal) (O(1))
  - Removes item from queue in order of enqueued. If empty, underflow condition
  1. Check if queue is empty
  2. If not, return  
c) front (access) (O(1))
  1. Return value at front
d) rear (access) (O(1))
  1. Return value at rear
e) empty
  1. If size is 0, then empty
f) size
  1. Kept track of as a field of queue

----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

4) Other operations

d) Searching

Stack

- Recursion (O(n) time, O(n) space)
  1. If stack is empty then return error based on type of search
  2. Hold all values in function call stack and pop until have reached index or matched search value
  3. Return either value or index or boolean if not found
  4. Push all held items back one by one

- Iterative is same as above but with second stack instead of function call stack

----------------------------------------------------------------------------------

Queue

- Can simply dequeue and re-enqueue going through entire queue and save index/value at index when found, or if not return error
  1. If stack is empty then return error based on type of search
  2. Dequeue and re-enqueue elements one by one until gone through entire queue
  3. Save either value or index or boolean if not found while going through, and return


e) Sorting

Stack

- Recursion (O(n^2) time, O(n) space)
  1. Hold all values in function call stack until stack empty (first recursive call)
  2. Insert all held items one by one in sorted order (second recursive call)
    a. If next item in function call stack is greater than top or there is no top, simply push
    b. If top is greater, pop/store and recur
    c. Push back top item removed earlier, essentially finding right spot in sorted stack and pushing there

- Iterative (O(n^2) time, O(n) space)
  1. Create second stack 
  2. While first stack is not empty, pop/store top element of first stack
  3. While second stack is not empty and top of first is greater that top of second, pop from second stack and push into first stack
  4. Push stored top element of first stack into second stack
  5. Return second stack once first is empty

Essentially this is taking the next element from the first stack, moving elements from the second back to the first until we find the correct spot for the new one, then putting them all back in the second and repeating with the second stack

----------------------------------------------------------------------------------

Queue

- Iterative (O(n log n) time, O(n) space)
  1. Dequeue and add all items to array
  2. Sort array using merge sort
  3. Enqueue sorted elements in order back into queue

- No extra space (O(n^2) time, O(1) space)
  1. Dequeue, store, and re-enqueue entire queue until maximum index is found  
  2. Dequeue, store, and re-enqueue entire queue until minimum index is found
  3. Repeat except don't enqueue minimum index element at original spot and instead enqueue last (at rear)
  4. Repeat 1 and 2 n times, looking at all elements but the last i elements being the current iteration and thus number of elements at rear in correct position

f) Merging

Stack

- Must decide which is on top first (O(n), O(1)/O(n))
  1. Pop and push all elements of stack to put on top into another temp stack
  2. Pop and push from other stack into the stack to merge with, essentially reversing twice 
    - Can also do recursively with call stack in same manner of other operations

Queue
- Super easy (O(n), O(1))
  1. Dequeue from queue to merge at back then enqueue elements into queue to merge with

----------------------------------------------------------------------------------


Queue


g) Reversing

Stack

- Using Recursion (O(n^2) time, O(n) space)
  1. Hold all values in function call stack until original stack becomes empty
    - Peek to hold values then pop with each recursive call until stack size is 0
  2. Insert elements back into original stack at bottom one by one
    - Hold/pop all items in original stack in function call stack, insert next element in function call stack above, then reinsert held ones in this step on top during each step of adding a new one 

- No extra space (O(n) time, O(1) space)
  1. Internally represent as linked list and reverse linked list
  2. At end, top becomes prev being last node, fully reversing stack
  
----------------------------------------------------------------------------------

Queue

- Iterative (O(n) time, O(n) space)
  1. Dequeue all elements in queue and insert into stack
    - Now top of stack is end of queue
  2. Pop elements in stack and enqueue one by one back into queue

- Recursive (O(n) time, O(n) space)
  1. If queue is empty (size = 0), return
  2. Dequeue and store element and recur
  3. Enqueue stored element into queue

h) Delete middle element

Stack

- Recursion (O(n) time, O(n) space)
  1. Store current counter to know how many elements have been removed
  2. Remove items one by one storing in function call stack
  3. Return all items except middle item

- Iterative (O(n) time, O(n) space)
  1. Create new temporary stack
  2. Push first n/2 elements of original stack into temp stack
  3. Pop and delete middle element
  4. Push temp stack elements back into original stack


----------------------------------------------------------------------------------

Queue

- O(n) time, O(1) space
  1. Dequeue and enqueue elements one by one until middle element is reached
  2. Dequeue and do not enqueue middle element
  3. Continue until end of queue


----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

5) Other factors

Queue

a) Dequeue extra info

- Can dequeue/enqueue on rear or front (both ways)
- Clockwise/anti-clockwise rotations are performed in O(1)
 - Dequeue from one side, enqueue on other
- Less memory efficient than normal queue


6) Advantages/Disadvantages and Applications

Stack
+++
- Stack helps in managing data that follows the LIFO technique.
- Stacks are be used for systematic Memory Management.
- It is used in many virtual machines like JVM.
- When a function is called, the local variables and other function parameters are stored in the stack and automatically destroyed once returned from the function. Hence, efficient function management.
- Stacks are more secure and reliable as they do not get corrupted easily.
- Stack allows control over memory allocation and deallocation.
- Stack cleans up the objects automatically.

---
- Stack memory is of limited size.
- The total of size of the stack must be defined before.
- If too many objects are created then it can lead to stack overflow.
- Random accessing is not possible in stack.
- If the stack falls outside the memory it can lead to abnormal termination.


Applications

- Infix to Postfix/Prefix conversion
- Redo-undo features at many places like editors, photoshop.
- Forward and backward features in web browsers
- Used in many algorithms like Tower of Hanoi, tree traversals, stock span problems, and histogram problems.
- Backtracking is one of the algorithm designing techniques. Some examples of backtracking are the Knight-Tour problem, N-Queen problem, find your way through a maze, and game-like chess or checkers in all these problems we dive into someway if that way is not efficient we come back to the previous state and go into some another path. To get back from a current state we need to store the previous state for that purpose we need a stack.
- In Graph Algorithms like Topological Sorting and Strongly Connected Components
- In Memory management, any modern computer uses a stack as the primary management for a running purpose. Each program that is running in a computer system has its own memory allocations
- String reversal is also another application of stack. Here one by one each character gets inserted into the stack. So the first character of the string is on the bottom of the stack and the last element of a string is on the top of the stack. After Performing the pop operations on the stack we get a string in reverse order.


----------------------------------------------------------------------------------

Queue
+++
- A large amount of data can be managed efficiently with ease.
- Operations such as insertion and deletion can be performed with ease as it follows the first in first out rule.
- Queues are useful when a particular service is used by multiple consumers.
- Queues are fast in speed for data inter-process communication.
- Queues can be used in the implementation of other data structures.
---
- The operations such as insertion and deletion of elements from the middle are time consuming.
- Limited Space.
- In a classical queue, a new element can only be inserted when the existing elements are deleted from the queue.
- Searching an element takes O(N) time.
- Maximum size of a queue must be defined prior.

Applications

Queue
- Multi programming: Multi programming means when multiple programs are running in the main memory. It is essential to organize these multiple programs and these multiple programs are organized as queues. 
- Network: In a network, a queue is used in devices such as a router or a switch. another application of a queue is a mail queue which is a directory that stores data and controls files for mail messages.
- Job Scheduling: The computer has a task to execute a particular number of jobs that are scheduled to be executed one after another. These jobs are assigned to the processor one by one which is organized using a queue.
- Shared resources: Queues are used as waiting lists for a single shared resource.
- When things don't need to be processed immediately but instead FIFO, like breadth first search
- When a resource is shared among multiple consumers. Examples include CPU scheduling, Disk Scheduling. 
- When data is transferred asynchronously (data not necessarily received at same rate as sent) between two processes. Examples include IO Buffers, pipes, file IO, etc. 
- Key press sequence
- Ticket counter line
- ATM booth line
- Queue can be used as an essential component in various other data structures.