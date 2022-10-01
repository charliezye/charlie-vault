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
###### O(h) time, O(h) space on call stack
- A new value is always inserted at a leaf node
- Search downwards for insertion value until empty child is found
	- Insert new node into that leaf node position

##### Recursive Method
Base Case: Tree is empty
Recursive Step: Left and right child are set to recursive call
###### Steps
1. Starting at head, compare inserting element with current node
	1. Recur down left subtree if insertion value is less than the current node value
	2. Recur down right subtree if insertion value greater than current node value
2. After reaching null return new node (set child equal to)
3. Return unchanged pointer to current to go back up tree

#### Deletion

##### Three Scenarios
###### 1. Node to delete is leaf
- Simply remove from the tree 
	- Done by setting parent's child to null
###### 2. Node to delete has only one child
- Copy child to deletion node and delete child
###### 3. Node to delete has two children
- Find in-order successor of node
	- If right child is not empty
	- Find minimum value in right child of node
- Copy contents of inorder successor to node and delete successor
- Predecessor can also be used

##### Recursive Method
Base Case: Tree is empty
Recursive Step: Left and right child are set to recursive call
###### Steps
1. Starting at head, search for deletion node recursively
	1. If deletion value is less than root, recur down left subtree
	2. If greater, recur down right subtree
3. If deletion value same as current node value
	1. If only one child or no child, return that child or null
	2. If two children, get inorder successor (smallest in right subtree)

##### Iterative Method


- Using for various searching sorting
- Value of left node is always less than parent, right is always greater
- Examples are AVL trees, red-black trees
