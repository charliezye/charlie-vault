# Breadth First Search (BFS)

- Also known as Level Order Traversal for [binary trees](obsidian://open?vault=Obsidian%20Vault&file=Work%2FCoding%20Interview%20Notes%2FReview%20Topics%2FData%20Structures%2FTrees%2FGeneral%20%2B%20Binary%20Trees)

### Recursive Method
###### O(n<sup>2</sup>) time, O(n) space
- O(log n) space, or height, for a balanced tree 

##### General Idea
- Use the recursive function to traverse all nodes of a level
- Find the height of the tree and run depth first search and maintain current height
- Print nodes for every height from root and for 1 to height 
	- Match if the current height is equal to the height of the iteration then print that node's data

##### Steps
1. Calculate [height]([[General + Binary Trees#Height of Tree]]) of the tree
2. Run a loop for current height from 1 to h
3. Use [DFS](obsidian://open?vault=Obsidian%20Vault&file=Work%2FCoding%20Interview%20Notes%2FReview%20Topics%2FAlgorithms%2FDepth%20First%20Search) to traverse the tree and maintain height for the current node
	1. If Node is NULL then return
	2. If level is 1 (leaf node) print node data
	3. If level greater than 1
		1. Recursive call on node's left child and decrement the height counter
		2. Recursive call on node's right child and decrement height counter

###### Code

```
/* function to print level order traversal of tree*/

void printLevelOrder()
{
	int h = height(root);
	int i;
	for (i = 1; i <= h; i++)
		printCurrentLevel(root, i);
}

/* Print nodes at the current level */

void printCurrentLevel(Node root, int level)
{
	if (root == null)
		return;
	if (level == 1)
		System.out.print(root.data + " ");
	else if (level > 1) {
		printCurrentLevel(root.left, level - 1);
		printCurrentLevel(root.right, level - 1);
	}
}
```

### Iterative Method
###### O(n) time, O(n) space

- Uses a queue similar to a lot of other binary tree methods

##### General Idea
- For each node, first, the node is visited and its child nodes and put into a queue
- Then pop a node from the queue and put its children in the queue
- Continue until the queue is empty

##### Steps
1. Create an empty queue and push the root node into it
2. While queue is not empty:
	1. Dequeue node and print
	2. Enqueue node's children

###### Code
```
/* Given a binary tree. Print
     its nodes in level order
     using array for implementing queue  */
     
    void printLevelOrder()
    {
        Queue<Node> queue = new LinkedList<Node>();

        queue.add(root);

        while (!queue.isEmpty()) {
            Node tempNode = queue.poll();
            System.out.print(tempNode.data + " ");
            
            /*Enqueue left child */
            if (tempNode.left != null) {
                queue.add(tempNode.left);
            }
            
            /*Enqueue right child */
            if (tempNode.right != null) {
                queue.add(tempNode.right);
            }
        }
    }
```

