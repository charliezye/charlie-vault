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

------------------------------------------------------------------------

1) Structure/Function

- "A tree is non-linear and a hierarchical data structure consisting of a collection of nodes such that each node of the tree stores a value and a list of references to other nodes (the “children”)."
- Recursive definition: "A tree consists of a root, and zero or more subtrees T1, T2, … , Tk such that there is an edge from the root of the tree to the root of each subtree."

- Non-linear data structure, instead a hierarchal data structure

- Trees have entries known as nodes, starting with a single root node with each node having zero or more "child" nodes that are linked to them, represented below the parent nodes like branches
  - Each node has a value and pointers to each of its leaf nodes in memory
- Important terms for trees
  - Parent node: Predecessor of a node
  - Root node: The single node at the top of the tree (no parents)
  - Child nodes: Nodes linked directly below a specific parent node
  - Leaf nodes: Nodes that have no children, meaning all pointers are null
  - Ancestor: Any predecessor nodes on path of root to that node
  - Depth/Level: Number for each node signifying number of edges from root to that node
  - Height: Number of edges from node to the furthest leaf, for tree aka maximum node depth
  - Degree: Number of children for node, degree of tree is arity
  - Arity: Max degree of any node in the tree

- A tree with N nodes has N-1 edges

------------------------------------------------------------------------

Binary Tree

- Most commonly used tree form
- Every node in the tree has at most two children, known as a left and right child node

- Types of binary trees:  
  a. Full binary trees
    - Every node has exactly 0 or two children
  b. Perfect binary trees
    - All internal nodes have two children, all leaf nodes are at same level
    - No room for adding nodes without adding height
  c. Complete binary tree
    - Perfect binary tree but may be missing nodes on last level/max depth
    - Must be filled starting at left of last level
    - Heaps are these
  d. Balanced binary trees
    - Height is O(log n)
    - Looks full, no missing chunks or branches ending much earlier than others
    - Types:
      - AVL Tree
        - Height of left and right sub-tree differing at most by 1
      - Red-black Tree
        - Number of black nodes on every root to leaf paths is same and no adjacent red nodes
    - O(log n) for search, insert, and delete
  e. Degenerate tree
    - Every internal node has only one child
    - Performance equivalent to linked list
    - Skewed tree
      - Degen tree with all left or all right nodes

- In a perfect binary tree, can easily calculate height as function of number of nodes
  - Each level has 2^i nodes in it
  - Thus, can factor to find that with n nodes:
  - h = log(n+1) where n is num nodes

Binary Search Tree

- Using for various searching sorting
- Value of left node is always less than parent, right is always greater
- Examples are AVL trees, red-black trees

------------------------------------------------------------------------

Binary Tree Properties

1. The maximum number of nodes at level 'l' of a binary tree is 2^l.

2. The maximum number of nodes in a binary tree of height 'h' is 2^h - 1 where height of root is 1.

3. In a binary tree with N nodes, the minimum possible height or levels is log(N+1)

4. A binary tree with L leaves has at least log(L) + 1 levels

5. In a binary tree where every node has 0 or 2 children (full), the number of leaf nodes is always one more than nodes w/ two children.

6. In a non-empty binary tree, the total number of edges is exactly 1 less than the number of nodes

------------------------------------------------------------------------
------------------------------------------------------------------------

2) Data Structure Implementation

Linked List Representation

- A tree is represented as a pointer to the topmost node of the tree, known as the root.
  - If it is empty, the value of the root is null
- A tree node contains:
  - Data
  - Pointer to left child
  - Pointer to right child

  1. Create tree node class
  2. Create root node with value and save pointer
  3. Create new nodes and assign to left and right pointers of root and future nodes to populate

------------------------------------------------------------------------

Array Representation (Sequential)

- Array indexes are values in tree nodes and array values give parent node of particular index or node
  - Value of root node index is always -1 as no parent for root

Construct linked from array representation:

- Recursive (O(n) time, O(n) space)
An array created [0..n-1] is used to keep track of created nodes.

1. Create an array of pointers of size n, created[]
  - The value of created[i] is NULL if node for index i is not created, else value is pointer to the created node.
2. Do following for every index i of given array:
  a. If created[i] is not NULL, then node is already created and return.
  b. Create a new node with value equal to index i.
  c. If parent[i] is -1 (i is root), make created node as root and return.
  d. Check if parent of ‘i’ is created (We can check this by checking if created[parent[i]] is NULL or not.
  e. If parent is not created, recur for parent and create the parent first.
  f. Let the pointer to parent be p. If p->left is NULL, then make the new node as left child. Else make the new node as right child of parent.

- Iterative (O(n) time, O(n) space)

1. Create n new nodes
2. Store in a data structure to keep track of which node is created for which value
3. Traverse parent array and build tree by setting parent-child relationship
  a. If parent (value at index of array) is -1, set root to current node with value i (current index)
  b. Else check if parent's left child is Null (node with value at index of array has no left child), then map left child to its parent (map current index node to parent)
    - If left child not null then map to right of parent

------------------------------------------------------------------------

For String representation (multiple of same value):
  1. Set root value char at index 0 of string
  2. If creating left node to a current node at index i:
    a. Input value and parent index
    b. Value is placed at (2 * i) + 1 index (assuming 0 start)
  3. If creating right node to a current node at index i:
    a. Input value and parent index
    b. Value is placed at (2 * i) + 2 index (assuming 0 start)

  - For each node, 2 more spots for left/right allocated at end of string


------------------------------------------------------------------------
------------------------------------------------------------------------

3) Basic Operations

a) Traversal

- Breadth First Search (BFS)
  - First explore nodes one step away, then two steps, etc.
  - Ripple effect like throwing stone in pond
  - Always finds shortest path (but less efficient)

- Depth First Search (DFS)
  - Go as deep down one path before backing up and trying another
  - Corn maze explore path until hitting dead end
  - Sometimes will not find shortest path (more efficient)
  - Implemented with recursion
  - Generally requires less memory than BFS


Ordered Traversals (O(n) time, O(h) space)
  - Space considers functional call stack
  - For space, if skewed tree will be O(n), if balanced tree will be O(log n)

- Pre-Order Traversal (C,L,R)
  - Visit current node, then left subtree, then right subtree
  - Typically same order as DFS
  - Used to create copy of tree or get prefix expression on expression tree

- In-Order Traversal (L,C,R)
  - Visit left subtree, then current node, then right subtree
  - In binary search tree, this gives nodes in increasing (non-decreasing) order of values
- Post-Order Traversal (L,R,C)

  - Visit left subtree, then right subtree, then current node
  - "Bottom up"
  - Used to delete tree
  - Also useful for postfix expression of expression tree

------------------------------------------------------------------------

b) Insertion    

------------------------------------------------------------------------

c) Deletion

------------------------------------------------------------------------

d) Searching

------------------------------------------------------------------------

e) Sorting

------------------------------------------------------------------------

f) Merging

------------------------------------------------------------------------

g) Height of Tree

------------------------------------------------------------------------

h) Level of tree

------------------------------------------------------------------------

i) Size of entire tree

------------------------------------------------------------------------
------------------------------------------------------------------------

4) Basic Operation Implementation

a) Traversal

Breadth First Search (BFS)
Depth First Search (DFS)
- Both have own separate documents

1. Recursive implementation

- Pre-Order Traversal (O(n) time, O(n) space)
  1. Visit the root/current node
  2. Traverse left subtree recursively (call Preorder(left-subtree))
  3. Traverse right subtree recursively (call Preorder(right-subtree))

- In-Order Traversal (O(n) time, O(n) space)
  1. Traverse left subtree recursively (call Inorder(left-subtree))
  2. Visit the root/current node
  3. Traverse right subtree recursively (call Inorder(right-subtree))

- Post-Order Traversal (O(n) time, O(n) space)
  1. Traverse left subtree recursively (call Postorder(left-subtree))
  2. Traverse right subtree recursively (call Postorder(right-subtree))
  3. Visit the root/current node

2. Iterative implementations

- In-Order (with stack) (O(n) time, O(n) space)
  1. Create an empty stack S.
  2. Initialize current node as root
  3. Push the current node to S and set current = current->left until current is NULL
  4. If current is NULL and stack is not empty then
    a. Pop the top item from stack.
    b. Print the popped item, set current = popped_item->right
    c. Go to step 3.
  5. If current is NULL and stack is empty then we are done.

- Pre-Order (with stack) (O(n) time, O(n) space)
  1. Create an empty stack
  2. Initialize current node as root
  3. Push the current node to S
  4. If stack is not empty then
    a. Pop top item from the stack
    b. Push right child of a popped item to stack
    c. Push left child of a popped item to stack
  Right pushed first to ensure left subtree traversed first

- Post-Order (2 stacks) (O(n) time, O(n) space)
  1. Push root to first stack.
  2. Loop while first stack is not empty
    a. Pop a node from first stack and push it to second stack
    b. Push left and right children of the popped node to first stack
  3. Pop contents of second stack that are now in postorder
 
- Morris In-Order Traversal (No recursion or stack) (O(n) time, O(1) Space)
  - Based on threaded binary tree
  1. Initialize current as root
  2. While current is not NULL
    If the current does not have left child
      a. Print current’s data
      b. Go to the right, i.e., current = current->right
    Else
      a. Make the right child of the inorder predecessor point to the current node.
      (Find rightmost node in current left subtree)
      Two cases arise:
        a) The right child of the inorder predecessor already points to the current node.  
        (reverting changes to restore original tree and fix right child of predecessor)
          1. Set right child to NULL (currently current)
          2. Print current node’s data
          3. Move to right child of current node.
        b) The right child is NULL.
        (restructuring considering the right-most as the inorder predecessor to current)
          1. Set it to current node.
          2. Move to left child of current node.

  - Tree is modified but reverted back to original shape after

- Morris Pre-Order Traversal (No recursion or stack) (O(n) time, O(1) Space)
  1. Initialize current as root
  2. While current is not NULL
    If the current does not have left child
      a. Print current’s data
      b. Go to the right, i.e., current = current->right
    Else
      a. Make the right child of the inorder predecessor point to the current node.
      (Find rightmost node in current left subtree)
      Two cases arise:
        a) The right child of the inorder predecessor already points to the current node.  
        (reverting changes to restore original tree and fix right child of predecessor)
          1. Set right child to NULL (currently current)
          2. Move to right child of current node.
        b) The right child is NULL.
        (restructuring considering the right-most as the inorder predecessor to current)
          1. Set it to current node.
          2. Print current node’s data
          3. Move to left child of current node.

  - Difference is printing when in-order predecessor is NOT pointing instead of IS pointing, meaning before it is ordered hence pre-ordered

------------------------------------------------------------------------

b) Insertion    

Level Order Insertion (First position available by level)

1.

------------------------------------------------------------------------

c) Deletion

------------------------------------------------------------------------

d) Searching

------------------------------------------------------------------------

e) Sorting

------------------------------------------------------------------------

f) Merging

------------------------------------------------------------------------

g) Height of Tree

------------------------------------------------------------------------

h) Level of tree

------------------------------------------------------------------------

i) Size of entire tree

------------------------------------------------------------------------

j) Deepest Node

------------------------------------------------------------------------
------------------------------------------------------------------------

5) Other factors

Handshaking Lemma

- In every finite undirected graph, an even number of vertices will always have an odd degree (number of vertices that touch an odd number of edges is even)
- Consequence of degree sum formula
  - sum(u in v) deg(v) = 2|E|
  - Sum of degrees (number of times each vertex is touched) equals twice number of edges in graph

Uses for trees

a) In a k-ary tree where every node has either 0 or k children, the following property is always true.

  L = (k - 1)*I + 1
Where L = Number of leaf nodes
      I = Number of internal nodes  

b) In a Binary tree, the number of leaf nodes is always one more than nodes with two children.
------------------------------------------------------------------------

Specific important binary trees

a) AVL

b) Red and black

------------------------------------------------------------------------
------------------------------------------------------------------------

6) Advantages/Disadvantages/Applications

+++
- Trees are useful for storing information naturally forming a hierarchy, like the file system on a computer
- Trees with ordering provide moderate access/search (quicker than linked list, slower than array)
- Trees provide moderate insertion and deletion (quicker than array, slower than unordered linked list)
- Trees don't have upper limit on number of nodes like LL and unlike arrays, as linked w/ pointers

Applications:
- Manipulate hierarchical data.
- Make information easy to search (see tree traversal).
- Manipulate sorted lists of data.
- As a workflow for compositing digital images for visual effects.
- Router algorithms
- Form of multi-stage decision-making (see business chess).
- Priority queue for searching max/min in O(1) time