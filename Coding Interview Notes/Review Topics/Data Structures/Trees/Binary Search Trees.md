## Binary Search Trees
#### Goals 
The following goals are general goals included as an outline every data structure. Some data structures may have sections that are different than the goals shown here.
1) Understand the structure of each and how they conceptually function
2) Learn how to implement the data structure itself
3) Learn how basic operations function, how to implement them, and their space/time complexity
	1) Traversal
	2) Insertion    
	3) Deletion
	4) Searching
	5) Sorting
	6) Merging
4) More Complex Operations
5) Other factors to consider
6) Understand what they are good and bad at and when to use them

---

### Important Reference Links

[Geeks for Geeks BSTs](https://www.geeksforgeeks.org/introduction-to-binary-search-tree-data-structure-and-algorithm-tutorials/?ref=lbp)

---

### 1) Structure/Function

- A BST is a binary tree with the following properties:
	- The **left** subtree of a node contains only nodes with values **lesser** than the current node's value
	- The **right** subtree contains only nodes with values **greater** than the node's key
	- Left and right subtrees must also be BSTs by definition
	- There must be **no duplicate nodes** in tree
- Ordering makes search, minimum and maximum operations easier

### 2) Implementation

- The implementation of a BST is essentially the same as that of [Binary Trees](obsidian://open?vault=Obsidian%20Vault&file=Coding%20Interview%20Notes%2FReview%20Topics%2FData%20Structures%2FBinary%20Trees), see that file for reference.

### 3) Basic Operations

#### Searching

- This is very similar to [binary search](obsidian://open?vault=Obsidian%20Vault&file=Coding%20Interview%20Notes%2FReview%20Topics%2FAlgorithms%2FBinary%20Search) which is used to search arrays

- Start at the root, comparing its value to the search value
	- If less than, know value must be in left subtree
	- If more than, know value must be in right subtree
- Essentially traverse in this manner and discard a subtree each time
- Assuming a balanced tree, **search space is cut in half** with each step

###### Steps
1. If current node value matches search value, return current node pointer
2. If search value less than current node, recur on left child
3. If search value greater, recur on right child

#### Insertion

- A new value is always inserted at a leaf node
- Search downwards for insertion value until empty child is found
	- Insert new node into that leaf node position

##### Iterative Level Order
- Iteratively traverse the tree using a queue

###### Steps
1. Create a new node with the value to insert and a queue
2. Starting with the head, enqueue 
If find a node w/ left child empty, make new node left child
- If find node w/ right child empty, make new node right child

- Using for various searching sorting
- Value of left node is always less than parent, right is always greater
- Examples are AVL trees, red-black trees
