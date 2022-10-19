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
