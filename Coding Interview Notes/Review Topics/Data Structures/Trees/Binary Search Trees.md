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
###### O(h) time, O(h) space
- Worst case O(n)

Base Case: Tree is empty
Recursive Step: Left and right child are set to recursive call

###### Steps
1. Starting at head, search for deletion node recursively
	1. If deletion value is less than root, recur down left subtree
	2. If greater, recur down right subtree
3. If deletion value same as current node value
	1. If only one child or no child, return that child or null
	2. If two children, get inorder successor (smallest in right subtree) and set root value to this
		1. Traverse as far left in right subtree and deepest child is smallest
	2. Delete inorder successor by calling delete on right subtree with successor value

 ##### Improvement (Less Calls)

- Keep track of parent node of successor to make child of that parent null to delete
	- Successor will always be leaf node
- Only different step is during 3.2.
	- Instead of calling delete (extra call stack calls), delete successor from saved parent
	- Can safely replace successor with parent's right child as it is always left child of parent
	- If no succ, assign parent's right child to successor's right child 

#### 4) Other Operations

##### Construction from Preorder Traversal (All Recursive)

##### Brute ForceMethod
###### O(n<sup>2</sup>) time, O(n) space
- Go through traversal list and recur to set left and right subtrees

Base Case: If node pointer is null, create new node with data
Recursive Step: Call on left and right child

###### Steps
1. If node is null then create new node with given data
2. If node data is greater than given data, recur on left subtree
3. If node data less than given data, recur on right subtree
4. Return node

##### Split Method
###### O(n<sup>2</sup>) time, O(n) space
- Split traversal akin to binary search based on values with respect to root and recur down left/right subtree

- Pass into recursive call: traversal array, current index, low and high as index range of recursive step
Base Case: Step called on single element (low = high)
Recursive Step: Called on left and right subtrees divided by index found i and low/high

###### Steps
1. Construct root from first element
2. Find index of first element greater than group
	1. Values between first (root) and this index are left subtree
	2. Values after index are right subtree
3. Divide traversal at index i from 2 and recur for left and right

##### Range Method (Recursive)
###### O(n) time, O(n) space
- Set a range {min, max} for each node
- Construct nodes based on where they fall within range
	- Left subtree range should be between INT_MIN and current node value
	- Right subtree between current node value and INT_MAX\

- Pass into recursive call: traversal array, current index, current node value, min, and max, and size
Base case: Reached end of traversal array
Recursive Step: Called on right and left subtree 

###### Steps
1. Call method passing in INT_MIN, INT_MAX as range values and root values
	1. This will create the root node
2. If element falls within range
	1. Create new node and increment current index first
	2. Recur on left subtree (set root.left with call) using previous min and setting max as value of the current node
	3. Recur on right subtree (set root.right with call) setting min as value of current node and using previous max
3. Return root

#### Binary Tree to BST Conversion

##### Basic Implementation
###### O(n log n) time, O(n) space

1. Create temp array to store [inorder traversal](obsidian://open?vault=Obsidian%20Vault&file=Coding%20Interview%20Notes%2FReview%20Topics%2FData%20Structures%2FTrees%2FGeneral%20%2B%20Binary%20Trees)of tree
	1. O(n) time
2. Sort temp array
	1. With [[Sorting#Quick Sort | heap]]/[[Sorting#Merge Sort | merge]] sort would take O(n log n)
	2. Can easily do with Arrays.sort for O(n<sup>2</sup>)
2. Do inorder traversal again and copy array elements to tree nodes one by one
	1. O(n) time


##### +++
###### Advantages over Hash Table
- Hash Table O(1) time operations
	- Search
	- Insert
	- Delete
- In BST these are all O(log n)

1. Can get all keys in sorted order with an inorder traversal (O(n))
	1. O(n log n) for hash table, much less simple operation
2. Easier Operations
	1. [Order statistics](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)
	2. [Find closest lower and greater elements](https://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/)
	3. [Range queries](https://www.geeksforgeeks.org/print-bst-keys-in-the-given-range/)
		1. This is important to remember
		2. To do a range search in hash table must iterate every bucket space O(n) or worse
		3. BST will not search subtrees that cannot have answer
3. Easy to implement custom BST
	1. Hash table requires hashing generally relying on libraries
4. With self balancing BSTs, operations guaranteed in O(log n time)
	1. For hash tables O(1) is average time, some are costly O(n<sup>2</sup>)  esp. with table resizing
5. BST are more memory efficient than hash tables
	1. Hash function range forces larger arrays to be made even if not used, not dynamic

##### Applications

- Using for various searching sorting
- Value of left node is always less than parent, right is always greater
- Examples are AVL trees, red-black trees
