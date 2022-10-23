Goals:
1) Understand the structure of each and how they conceptually function
2) Learn how to implement the data structure itself
3) Understand how basic operations function
4) Learn how to implement basic operations and their space/time complexity
  - Traversal, insertion, deletion, searching, sorting, merging
5) Other factors to consider
6) Understand what they are good and bad at and when to use them

Resources:
https://www.geeksforgeeks.org/linked-list-set-1-introduction/

1) Structure/Function

- Linked lists are made up of a long chain of nodes
  - Each node contains two parts:
    - A data element needed to be stored of the same type
    - A pointer containing the memory address of the next node in the chain
  - There is a head node and a tail node
    - The head node is simply the beginning of the chain 
    - The tail node is simply the end, signified by a pointer to null 
    - Both functionally are the same as any other node
- Nodes are non-contiguous, so can each be anywhere in memory (non-consecutive)
- Singly vs. doubly linked list
  - Above is the singly linked list
  - The doubly linked list is the same but has an additional pointer to previous node's address
    - Thus, stores both head and tail, so can traverse backwards from tail\
    - This means uses even more memory though
  - There are multiple scenarios in which doubly linked list are better as described in part 4

2) How to implement data structure

- This is quite simple
1) Create a Node class/data type
  - Should have two variables:
    - A Data Item (of whatever type)
    - A pointer/reference or address to the next node in the list
  - Should be static if accessed by Main
2) Create nodes and point them to each other
  - In Java, should create empty LinkedList first
    - Gives access to built-in functions
  - After creating will have references, so set node next to reference to next one in list (and prev of next to current if doubly linked)
  - Next address of final node should be null unless circular linked list, in which case should be head

3) Basic Operations

a) Traversal O(n)
  - Singly linked (O(n))
    - Follow next node addresses starting with stored head and maintain index
    - Traversal must start at the head and continue towards tail
      - No way to traverse backwards once at a certain node
  - Doubly linked (O(n/2))
    - Can traverse in either direction, cutting time down in real scenarios in half but not really affecting big O
  - Edge cases
    - Index out of bounds

b) Insertion
  - Singly linked (O(n))
  - Doubly linked (O(n/2))
  - Because you still need to traverse to that particular node, runtime is similar to traversal above with constant operation after

c) Deletion
  - Considering you have a reference/address to the node you want to delete:
  - Singly linked (O(n))
    - Must traverse to previous node by starting at head, taking O(n) time
  - Doubly linked (O(1))
    - Given the node to delete, you can easily access the previous node

d) Searching (O(n))
  - Always involves some traversal and counting/comparisons.

e) Sorting (O(n log n))
  - Merge sort is best way to sort linked lists.
  - There are O(n) and O(log n) space complexity ones, but the solution below is O(1).


f) Reversal (O(n))
  - There are several ways to accomplish this efficiently.

g) Rotation (O(n))
  - Interesting double pointer and circular ways to accomplish this.

h) Rearranging (O(n))
  - Depends on specific case, but example below is O(n).

i) Merging (O(m+n) lengths of both lists)
  - There are several ways to do this but overall concept is the same, compare from front of both lists to add to result. 


4) Basic Operations Implementation

a) Traversal
  Consider you are given the index to traverse to. 
  1) (doubly only) If length of LinkedList is known, if index is in latter half of list, start from tail and use prev node instead of next shown below.
  2) Create temporary pointer to head node (Java). 
  3) Using the node from 2, reassign it to the next node field of itself (traversing one node down the list). 
  4) Repeat step 3 the number of the index given (Or length-index if starting from tail). Now you have traversed to the proper node.

b) Insertion    

Add node to front: O(1)
  1) Allocate and put data into new node.
  2) Make next address of new node the address of head node.
  3) (doubly only) Make prev address of head node the address of new node.
  4) Reassign head to point to new node.

Add node after given node: O(n)
  1) Check if node is at beginning.
  2) (if given index) Traverse to node at index given.
  3) Check if given (prev) node is null.
  4) Allocate and put data into new node.
  5) Make next address of new node the next address of previous node.
  6) Change next address of previous node to address of new node.
  7) (doubly only) Make previous address of new node the address of previous node.
  8) (doubly only) Change previous address of new node's next node to new node's address.

Add node at end: O(n) or O(1) if tail pointer exists (for doubly linked)
  1) Allocate and put data into new node.
  2) If Linked List empty, make new node as head.
  3) Make sure next address if new node is null.
  4) Traverse to end of list (until next is null).
  5) Change next address of last node to address of new node.
    - If tail node is stored (as in doubly linked), this is only step needed.

c) Deletion

Delete from beginning: O(1)
  1) Check if list is empty.
  2) Reassign head to point to head's next address.

Delete from Middle: O(n)
  1) Check if node is at beginning
  2) Traverse to previous node of deletion node.
    - If given node address:
      - For singly, traverse until node is found, storing prev address.
      - For doubly, simply take prev address of given node.
    - If given index, follow steps from traversal above.
  2) Change next address of previous node to next address of deletion node.
  3) (doubly only) Change previous address of deletion node's next node to previous address of deletion node.

Deletion from end: O(n)
  1) Traverse to end of list, storing prev address while traversing.
  2) Once at end, set prev's next address to null.

Recursive method:

Since the current node pointer is derived from the previous node’s next, if the value of the current node pointer is changed, the previous next node’s value also gets changed which is the required operation while deleting a node (i.e points previous node’s next to current node’s (with value or index) next).

  1) Pass Node (node pointer) as a reference to the function (as in Node head).
  2) Create base case for when correct node is reached.
    - Change this node pointer so it points to its next, returning the new pointer.
  3) Make correct recursive call to function to find the node containing the given value (perhaps decrementing int or matching).

Now, when base case is reached, change in value of correct pointer will result in next being changed for all nodes before it.


d) Searching (O(n) / O(1) space complexity if no recursion)

Get Nth node: 

Algorithm 1:
  1) Initialize count = 0
  2) Loop through the link list
     a) if the count is equal to the passed index then return the current
         node
     b) Increment count
     c) change current to point to next of the current.

Algorithm 2 (Recursion): O(n) space complexity too
  1) Initialize count = 0
  2) if count==n
     return node->data
  3) else
    return getnth(node->next,n-1)

Nth from last:

Algo 1: 
  1) Calculate the length of the Linked List.
  2) Traverse to the len - n + 1 node and return.

Algo 2 (2 pointers):
Maintain two pointers starting from the head of the Linked-List.
  1) Move one pointer to the Nth node from the start
  2) Move both together until pointer from 1) reaches last node. Now other is answer.

Find middle:

Algo 1: 
  1) Count length
  2) Traverse to len/2 node and return.

Algo 2 (2 pointer - Tortoise and Hare):
Maintain two points starting from head.
  1) Traverse one pointer one step and the other two steps.
  2) When two step pointer reaches end, one step will be in middle.

Algo 3:
  1) Initialize the mid element as head and initialize a counter as 0.
  2) Traverse the list from the head, while traversing increment the counter and change mid to mid->next whenever the counter is odd. 

Thus, the mid will move only half of the total length of the list. 

e) Sorting

Merge sort is best suited sorting algorithm. O(n log n)

Algorithm: O(n log n) time, O(1) space

In each pass, we are merging lists of size K into lists of size 2K. (Initially K equals 1)) 

  1) Create temporary pointer p to head node.
  2) Create empty list L which we will add elements to.
  3) If p is null, terminate.
  4) Otherwise, there is at least one element in the next pair of length-K lists, so increment the number of merges performed in this pass.
  5) Point another temporary pointer, q, at the same place as p. Step q along the list by K places, or until the end of the list, whichever comes first. Let psize be the number of elements you managed to step q past.
  6) Let qsize equal K. Now we need to merge a list starting at p, of length psize, with a list starting at q of length at most qsize.
  7) So, as long as either the p-list is non-empty (psize > 0) or the q-list is non-empty (qsize > 0 and q points to something non-null):
    a) Choose which list to take the next element from. If either list is empty, we must choose from the other one. (By assumption, at least one is non-empty at this point.)   
    b) If both lists are non-empty, compare the first element of each and choose the lower one. If the first elements compare equal, choose from the p-list. (This ensures that any two elements which compare equal are never swapped, so stability is guaranteed.)
    c) Remove that element, e, from the start of its list, by advancing p or q to the next element along, and decrementing psize or qsize.
    d. Add e to the end of the list L we are building up.
  8) Now we have advanced p until it is where q started out, and we have advanced q until it is pointing at the next pair of length-K lists to merge. So set p to the value of q, and go back to the start of this loop.

As soon as a pass like this is performed and only needs to do one merge, the algorithm terminates, and the output list L is sorted. Otherwise, double the value of K, and go back to the beginning.

This procedure only uses forward links, so it doesn't need a doubly linked list. If it does have to deal with a doubly linked list, the only place this matters is when adding another item to L.

Dealing with a circularly linked list is also possible. You just have to be careful when stepping along the list. To deal with the ambiguity between p==head meaning you've just stepped off the end of the list, and p==head meaning you've only just started, I usually use an alternative form of the "step" operation: first step p to its successor element, and then reset it to null if that step made it become equal to the head of the list.

f) Reversal (O(N))

Iterative Method: ()
  1) Create three pointers prev, curr as head, and next.
  2) Store curr's next address as the next pointer.
  3) Change the next of curr to prev.
  4) Set prev as curr and curr as next.
  5) Repeat steps 2-4 until reaching the end of the linked list. 

Can also store pointer to next within loop instead of outside.

Recusive (weird):
 1) Divide the list in two parts - first node and 
      rest of the linked list.
 2) Call reverse for the rest of the linked list.
 3) Link rest to first.
 4) Fix head pointer

Recursive (better):
Here, we use previous and current node for recursive calls.
  1) If last node, mark it head and update its next to the previous node (base case).
  2) Save next node address for recursive call.
  3) Update next node to the previous node.
  4) Recursively call to function with saved next node address (now curr) and current node (now prev). 

g) Rotation (O(n))

Given k nodes to rotate by (counter-clockwise rotation): 

Algo 1:
Goal is to store 3 nodes: kth, k+1th, and last.
  1) Traverse the list from the beginning and stop at kth node. 
  2) Store pointer to kth node. We can get (k+1)th node from next address.
  3) Keep traversing till the end and store a pointer to the last node also. 
  4) Change next address of kth node to null.
  5) Change next address of last node to head.
  6) Reassign head to k+1th node address.

Algo 2 (Make Circular):
  1) Traverse to end of list.
  2) Set next to head.
  3) Traverse to k-1 position from head (last element of rotated array).
  4) Update head to next address of current node.
  5) Update next address of current node to null.

h) Rearranging (O(N))

Given a singly linked list L0 -> L1 -> … -> Ln-1 -> Ln. Rearrange the nodes in the list so that the new formed list is : L0 -> Ln -> L1 -> Ln-1 -> L2 -> Ln-2 … You are required to do this in place without altering the nodes’ values. 

Efficient solution: O(N)
  1) Find the middle point using tortoise and hare method.
  2) Split the linked list into two halves using found middle point in step 1)
  3) Reverse the second half.
  4) Do alternate merge of first and second halves.

i) Merging (O(m+n) lengths of both lists)

Merge two sorted linked lists:
Refer to https://www.geeksforgeeks.org/merge-k-sorted-linked-lists/?ref=lbp
Uses Divide+Conquer and Heaps, should come back to this.

Cases to deal with: 
  - a or b may be empty
  - One may run out first
  - Starting result list empty and building up is a problem

Algo 1 (Dummy nodes): 
  1) Create dummy node as start of result list and a Tail pointer to this node.
  2) Check to see if either list has ended, in which case you should finish the result by pointing the tail to the head of the remaining list. Terminate.
  3) Compare the head of each list. Whichever is smaller should be added to the tail of the result.
  4) Advance the head of the list chosen to its next node address.
  5) Advance the tail to its next node address. 

Algo 2 (Local References):
  1) Maintain a pointer to the last node of the result list (fixes same issue of result list).
  2) Same steps as above.
  3) Advance the pointer to the next field of itself.

Algo 3 (Recursion): (Bad space complexity)
  1) If either node from a/b are null, return the other (base case).
  2) Compare a and b nodes. Whichever is smaller, set its next address to recursive call with its next address and the b node.

Algo 4 (Reversing lists):
Reverse each list
  1) Initialize result list as empty: head = NULL.
  2) Let 'a' and 'b' be the heads of first and second list respectively.
  3) Reverse both the lists.
  4) While (a != NULL and b != NULL)
    a) Find the larger of two (Current 'a' and 'b')
    b) Insert the larger value of node at the front of result list.
    c) Move ahead in the list of larger node. 
  5) If 'b' becomes NULL before 'a', insert all nodes of 'a' 
   into result list at the beginning.
  6) If 'a' becomes NULL before 'b', insert all nodes of 'b' 
   into result list at the beginning.  


Merge k sorted linked lists:

5) Other factors to consider

Circular linked lists (additional type)
  - This can apply to singly or doubly linked lists.
  - The main difference is that the last node points to the first (head node) so it becomes circular in nature
  - Insertion in beginning is different
    - Need last node address input
    - Set new node address to last's next address and last next address to new node
  - Deletion at last is different
    - Must set next of prev after traversing to head instead of null
  - Advantages: 
    - Any node can be a starting point and can traverse whole list from
    - Useful for queue, don't need front and rear pointer, just last inserted
    - Useful in repeatedly going around list
    - Fibonacci Heap
  - Disadvantages: 
    - More complex
    - Reversing is more complicated
    - Possible for infinite loop
    - Harder to find end of list and control loop

6) Advantages/Disadvantages

+++
1) Dynamic data structure
  - Allocates needed memory while running
  - Facilitates change to size of data structure (don't need to create new one to add new elements)
2) Easy insertion and deletion
  - Runs in O(1) time wherever operation is done
3) No/low memory waste
  - E.g. no garbage collection, no dangling pointers
  - Dynamic structure also matters here, no allocated memory that is empty/useless until filled
4) Expanded in constant time

---
1) Greater memory usage
  - Additional pointer(s) stored in memory as opposed to arrays that only store elements
2) No random access of elements
  - Need to traverse linearly through list
  - No indexes
3) Accessing/searching elements is more time consuming
  - Runs in O(n) time
4) Bad cache locality

7) Good Uses:

1) Implementing Stacks and Queues
  - In fact, LinkedList in Java works with stack and queue calls
    - For stacks, .push() and .pop()
    - For queues, .offer() and .poll()
2) Various representations of trees and graphs
3) Finding paths in networks
4) Arithmetic operations on long integers
5) Representing sparse matrices
4) Dynamic memory allocation (free blocks)

Real life scenarios:

1) GPS navigation
  - Steps or stops are like nodes
  - If you need to add a stop, can easily insert node and recalculate route
2) Music playlist
  - Songs may not be stored in same place in memory, but will be in particular order