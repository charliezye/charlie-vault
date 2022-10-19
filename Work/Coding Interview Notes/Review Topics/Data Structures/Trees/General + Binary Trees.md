## Binary Trees
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
---
### Important Reference Links

[Geeks for Geeks Binary Trees](https://www.geeksforgeeks.org/introduction-to-binary-tree-data-structure-and-algorithm-tutorials/?ref=lbp)

---
---

### 1) Structure/Function

#### General Tree 

##### Definition
> A tree is non-linear and a hierarchical data structure consisting of a collection of nodes such that each node of the tree stores a value and a list of references to other nodes (the “children”)

>>**Recursive definition**
>>"A tree consists of a root, and zero or more subtrees T1, T2, … , Tk such that there is an edge from the root of the tree to the root of each subtree."

##### General Information
- Non-linear data structure, instead a hierarchal data structure
- Trees have entries known as nodes, starting with a single root node with each node having zero or more "child" nodes that are linked to them, represented below the parent nodes like branches
	- Each node has a value and pointers to each of its leaf nodes in memory

##### Important terms for trees
- Parent node: Predecessor of a node
- Root node: The single node at the top of the tree (no parents)
- Child nodes: Nodes linked directly below a specific parent node
- Leaf nodes: Nodes that have no children, meaning all pointers are null
- Ancestor: Any predecessor nodes on path of root to that node
- Depth/Level: Number for each node signifying number of edges from root to that node
- Height: Number of edges from node to the furthest leaf, for tree aka maximum node depth
- Degree: Number of children for node, degree of tree is arity
- Arity: Max degree of any node in the tree

##### Tree Properties
- A tree with N nodes has N-1 edges

---

#### Binary Tree

##### General Information
- Most commonly used tree form in practice problems
- Every node in the tree has at most two children, known as a left and right child node

##### Types of binary trees
1. Full binary trees
- Every node has exactly 0 or two children
2. Perfect binary trees
- All internal nodes have two children, all leaf nodes are at same level
- No room for adding nodes without adding height
3. Complete binary tree
- Perfect binary tree but may be missing nodes on last level/max depth
- Must be filled starting at left of last level
- Heaps are these
4. Balanced binary trees
- Height is O(log n)
- Looks full, no missing chunks or branches ending much earlier than others
- Types:
  - AVL Tree
	- Height of left and right sub-tree differing at most by 1
  - Red-black Tree
	- Number of black nodes on every root to leaf paths is same and no adjacent red nodes
- O(log n) for search, insert, and delete
5. Degenerate tree
- Every internal node has only one child
- Performance equivalent to linked list
- Skewed tree
  - Degen tree with all left or all right nodes

#### Binary Tree Properties
1. The maximum number of nodes at level 'l' of a binary tree is 2^l.
2. The maximum number of nodes in a binary tree of height 'h' is 2^h - 1 where height of root is 1.
3. In a binary tree with N nodes, the minimum possible height or levels is log(N+1)
4. A binary tree with L leaves has at least log(L) + 1 levels
5. In a binary tree where every node has 0 or 2 children (full), the number of leaf nodes is always one more than nodes w/ two children.
6. In a non-empty binary tree, the total number of edges is exactly 1 less than the number of nodes

---
---

### 2) Data Structure Implementation

#### Linked List Representation
- A tree is represented as a pointer to the topmost node of the tree, known as the root.
  - If it is empty, the value of the root is null
- A tree node contains:
  1. Data
  2. Pointer to left child
  3. Pointer to right child

###### Steps:
1. Create tree node class
2. Create new nodes and assign to left and right pointers of root and future nodes to populate
3. Create root node with value and save pointer

---

#### Array Representation (Sequential)

- Array indexes are values in tree nodes and array values give parent node of particular index or node
  - Value of root node index is always -1 as no parent for root

##### Constructing linked representation from array representation:

###### Recursive (O(n) time, O(n) space)

An array created [0..n-1] is used to keep track of created nodes.

1. Create an array of pointers of size n, created[]
	  - The value of created[i] is NULL if node for index i is not created, else value is pointer to the created node.
2. Do following for every index i of given array:
	  1. If created[i] is not NULL, then node is already created and return.
	  2. Create a new node with value equal to index i.
	  3. If parent[i] is -1 (i is root), make created node as root and return.
	  4. Check if parent of ‘i’ is created (We can check this by checking if created[parent[i]] is NULL or not.
	  5. If parent is not created, recur for parent and create the parent first.
	  6. Let the pointer to parent be p. If p -> left is NULL, then make the new node as left child. Else make the new node as right child of parent.

###### Iterative (O(n) time, O(n) space)
1. Create n new nodes
2. Store in a data structure to keep track of which node is created for which value
3. Traverse parent array and build tree by setting parent-child relationship
    1. If parent (value at index of array) is -1, set root to current node with value i (current index)
    2. Else check if parent's left child is Null (node with value at index of array has no left child), then map left child to its parent (map current index node to parent)
        1. If left child not null then map to right of parent

##### String Representation of Array (multiple of same value)
  1. Set root value char at index 0 of string
  2. If creating left node to a current node at index i:
	  1. Input value and parent index
	  2. Value is placed at (2 * i) + 1 index (assuming 0 start)
  3. If creating right node to a current node at index i:
	  1. Input value and parent index
	  2. Value is placed at (2 * i) + 2 index (assuming 0 start)

For each node, 2 more spots for left/right allocated at end of string

---
---

### 3) Basic Operations

#### Traversal

##### [Breadth First Search (BFS)](obsidian://open?vault=Obsidian%20Vault&file=Coding%20Interview%20Notes%2FReview%20Topics%2FAlgorithms%2FBreadth%20First%20Search)
  - First explore nodes one step away, then two steps, etc.
  - Ripple effect like throwing stone in pond
  - Always finds shortest path (but less efficient)

##### [Depth First Search (DFS)](obsidian://open?vault=Obsidian%20Vault&file=Coding%20Interview%20Notes%2FReview%20Topics%2FAlgorithms%2FDepth%20First%20Search)
  - Go as deep down one path before backing up and trying another
  - Corn maze explore path until hitting dead end
  - Sometimes will not find shortest path (more efficient)
  - Implemented with recursion
  - Generally requires less memory than BFS

#### DFS Ordered Traversals 
###### (O(n) time, O(h) space)
  - Space considers functional call stack
	  - All algorithms assume O(h) unless otherwise specified
  - For space, if skewed tree will be O(n), if balanced tree will be O(log n)

##### Pre-Order Traversal (C,L,R)
  - Visit current node, then left subtree, then right subtree
  - Typically same order as DFS
  - Used to create copy of tree or get prefix expression on expression tree
  
###### Recursive Steps:
  1. Visit the root/current node
  2. Traverse left subtree recursively (call Preorder(left-subtree))
  3. Traverse right subtree recursively (call Preorder(right-subtree))

###### Iterative Steps (stack):
  1. Create an empty stack
  2. Initialize current node as root
  3. Push the current node to S
  4. If stack is not empty then
    1. Pop top item from the stack
    2. Push right child of a popped item to stack
    3. Push left child of a popped item to stack
  Right pushed first to ensure left subtree traversed first
  
  ###### Morris Pre-Order Traversal (No recursion or stack) (O(n) time, O(1) Space)
  1. Initialize current as root
  2. While current is not NULL
	  1. If the current does not have left child
			1. Print current’s data
			2. Go to the right, i.e., current = current->right    
		2. Else
	      1. Make the right child of the in-order predecessor point to the current node.
	      2. (Find rightmost node in current left subtree)
		      Two cases arise:
		        1. The right child of the in-order predecessor already points to the current node (reverting changes to restore original tree and fix right child of predecessor)
			        1. Set right child to NULL (currently current)
			        2. Move to right child of current node.
		        1. The right child is NULL (restructuring considering the right-most as the inorder predecessor to current)
			          1. Set it to current node.
			          2. Print current node’s data
			          3. Move to left child of current node.

- Difference between this and in-order is printing when in-order predecessor is NOT pointing instead of IS pointing, meaning before it is ordered hence pre-ordered

##### In-Order Traversal (L,C,R)
  - Visit left subtree, then current node, then right subtree
  - In binary search tree, this gives nodes in increasing (non-decreasing) order of values
  
###### Recursive Steps:
  1. Traverse left subtree recursively (call Inorder(left-subtree))
  2. Visit the root/current node
  3. Traverse right subtree recursively (call Inorder(right-subtree))

###### Iterative Steps (stack):
  1. Create an empty stack S.
  2. Initialize current node as root
  3. Push the current node to S and set current = current->left until current is NULL
  4. If current is NULL and stack is not empty then
	  1. Pop the top item from stack.
	  2. Print the popped item, set current = popped_item->right
	  3. Go to step 3.
  5. If current is NULL and stack is empty then we are done.

###### Morris In-Order Traversal (No recursion or stack) (O(n) time, O(1) Space)
Based on threaded binary tree
  1. Initialize current as root
  2. While current is not NULL
		1. If the current does not have left child
	    1. Print current’s data
	    2. Go to the right, i.e., current = current->right
    2. Else
	      1. Make the right child of the in-order predecessor point to the current node.
	      2. (Find rightmost node in current left subtree)
		      Two cases arise:
		        1. The right child of the in-order predecessor already points to the current node (reverting changes to restore original tree and fix right child of predecessor)
			        1. Set right child to NULL (currently current)
			        2. Print current node’s data
			        3. Move to right child of current node.
		        1. The right child is NULL (restructuring considering the right-most as the inorder predecessor to current)
			          1. Set it to current node.
			          2. Move to left child of current node.

  - Tree is modified but reverted back to original shape after


##### Post-Order Traversal (L,R,C)
  - Visit left subtree, then right subtree, then current node
  - "Bottom up"
  - Used to delete tree
  - Also useful for postfix expression of expression tree

###### Recursive Steps:
  1. Traverse left subtree recursively (call Postorder(left-subtree))
  2. Traverse right subtree recursively (call Postorder(right-subtree))
  3. Visit the root/current node

###### Iterative Steps (2 stacks):
  1. Push root to first stack.
  2. Loop while first stack is not empty
	  1. Pop a node from first stack and push it to second stack
	  2. Push left and right children of the popped node to first stack
  3. Pop contents of second stack that are now in postorder

---

#### Insertion    

##### Iterative Level Order 
###### O(V) time, O(B) space
- Where V is num nodes, B is width of tree)

- Traverse nodes in level order, adding to a queue
	- Dequeue and check left and right nodes in level order until an empty spot is found and add node there
- In worst case, we need to hold all vertices of a level in the queue
- This method of insertion will guarantee creation of a complete binary tree

###### Steps:
1. Create new node with value to be inserted and queue
2. Traverse nodes in level order, adding to queue until finding an empty spot
3. With each step dequeue one node from queue until queue is empty
	1. If left child of node is empty, make new node left child of that node
		1. Else add left child to queue
	2. Else if right child is empty, make new node right child of node
		1. Else add right child to queue

---

#### Deletion
##### Replacement with Deepest Node 
###### (O(n) time and space)
- Replace node being deleted with deepest and rightmost node in binary tree
	- No order among elements so can replace with last element
- Use queue to traverse and find nodes given value

###### Steps:
1. Do level order traversal storing non-empty child nodes in a queue and popping to check
	1. Store a pointer to the node containing the value to be deleted
	2. Store a pointer to node most recently added to queue to track parent of rightmost deepest node
2. Once deepest and right-most node is found (queue is empty), replace value in node containing value to delete with value of this node
	1. Remove pointer from parent to rightmost deepest node, effectively deleting it

---

#### Searching
##### Level Order Search
###### (O(n) time and space)
- Same concept as above, using queue to traverse, checking value of each node until found

###### Steps:
1. Do level order traversal storing non-empty child nodes in a queue
	1. Pop to compare value to search value and recursively add children until queue is empty
	2. Stop if value is found


---

#### Summation

##### Recursive Method
###### (O(n) time and space)
- Recursively call left and right subtree sums and add values with current node's value

###### Steps:
1. Recur on left and right children
2. Add sum result of left and right children to value of current node and return

##### Iterative Method
###### (O(n) time and space)
- Do level order traversal like above and add to sum each time node is dequeued

###### Steps:
1. Use a queue and traverse in level order
2. Dequeue nodes with each step, adding child nodes to queue, and adding the value of the node dequeued to a sum

---

### 4) More Complex (Tree-Specific) Operations

#### Height of Tree
##### Recursive Method
###### (O(n) time and space on callstack)
- Recursively call height function on left and right subtrees
	- After heights are found for each subtree, compare and return greater height + 1

###### Steps:
1. Recur on left and children of current node until null
	1. Compare height value of left and right child and return the greater value + 1 to account for the current node in height
---

#### Level of tree
###### (O(n) time and space)
- If finding level of a specific node, level order traverse until node is found
	- Keep track of level, each time children are added increment level
- Can also accomplish this by recursion by recurring on left and right subtrees and including level in function call
	- Each successive call should use level of current call + 1

---

#### Size of entire tree
###### (O(n) time and space)
- Level order traverse using queue and add to count of node with each node dequeued

---
---

### 5) Other factors

#### Handshaking Lemma

- In every finite undirected graph, an even number of vertices will always have an odd degree (number of vertices that touch an odd number of edges is even)
- Consequence of degree sum formula
  - sum(u in v) deg(v) = 2|E|
  - Sum of degrees (number of times each vertex is touched) equals twice number of edges in graph

#### Uses for Binary Trees
1. In a k-ary tree where every node has either 0 or k children, the following property is always true.

  L = (k - 1)\*I + 1
*Where L = Number of leaf nodes*
     *I = Number of internal nodes*

2. In a Binary tree, the number of leaf nodes is always one more than nodes with two children.

---
---

### 6) Advantages/Disadvantages/Applications

#### +++
- Trees are useful for storing information naturally forming a hierarchy, like the file system on a computer
- Trees with ordering provide moderate access/search (quicker than linked list, slower than array)
- Trees provide moderate insertion and deletion (quicker than array, slower than unordered linked list)
- Trees don't have upper limit on number of nodes like LL and unlike arrays, as linked w/ pointers

#### ---


#### Applications:
- Manipulate hierarchical data.
- Make information easy to search (see tree traversal).
- Manipulate sorted lists of data.
- As a workflow for compositing digital images for visual effects.
- Router algorithms
- Form of multi-stage decision-making (see business chess).
- Priority queue for searching max/min in O(1) time
