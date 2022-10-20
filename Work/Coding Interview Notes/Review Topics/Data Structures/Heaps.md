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
### 1) Structure/Function

Heaps are a special tree-based data structure that is a complete binary tree.

There are two specific types of heaps:
1. Max-Heap
	- Key at root node must be greatest among all of its children
	- Must be recursively true for all sub-trees
2. Min-Heap
	- Key at root node must be smallest among all of its children
	- Must be recursively true for all sub-trees

The time complexity to build a binary heap is O(n)
```
BUILD-HEAP(A) 

    heapsize := size(A); 

    for i := floor(heapsize/2) downto 1 

        do HEAPIFY(A, i); 

    end for 

END
```

### 2) Implementation

Binary heaps are typically represented as arrays
- The root element is at arr[0]
``` java
Arr[(i-1)/2]	Returns the parent node 
Arr[(2*i)+1]	Returns the left child node
Arr[(2*i)+2]	Returns the right child node
```

To build a heap from an array, first consider it as a binary tree with the values as shown 
- Start with the middle element (the root in array-impl tree) and call the heapify operation on that index and continue down to 1

### 3) Basic Operations

#### Heapify
1. Start by locating root element and left/right children
2. Compare root value to children
	- If either is smaller/larger swap root with the smallest/largest child
	- Recursive call on affected subtree (where root value was just swapped)

###### Code
``` java
// To heapify a subtree rooted with node i which is
// an index in arr[]. n is size of heap
void heapify(int arr[], int N, int i)
{
	int largest = i; // Initialize largest as root
	int l = 2 * i + 1; // left = 2*i + 1
	int r = 2 * i + 2; // right = 2*i + 2

	// If left child is larger than root
	if (l < N && arr[l] > arr[largest])
		largest = l;

	// If right child is larger than largest so far
	if (r < N && arr[r] > arr[largest])
		largest = r;

	// If largest is not root
	if (largest != i) {
		int swap = arr[i];
		arr[i] = arr[largest];
		arr[largest] = swap;

		// Recursively heapify the affected sub-tree
		heapify(arr, N, largest);
	}
}
```

#### Decrease Key
###### O(log n)
To decrease the value of a certain key inside the min-heap, we need to reach it first
- Keep map beside original array storing index of every key to determine index

1. Use map to locate index of certain key
2. Change value and move up the tree if needed for min-heap, or down for max-heap (call heapify)

#### Extract Max/Min
###### O(log n)
1. Remove the root and replace with the last element in the heap
2. Restore heap property by comparing with children and moving new root down until children both smaller than or equal to element (call heapify)

#### Insertion
###### O(log n)
At most one swap on each level of heap from inserted node to root, and heap is complete tree

1. Append new value to the end of the heap (last element in array)
2. Compare added element with parent and move element up unntil parent is larger than or equal to inserted element

``` python
public void insert(Comparable x)
{
	if(size == heap.length - 1) doubleSize();

	//Insert a new item to the end of the array
	int pos = ++size;

	//Percolate up
	for(; pos > 1 && x.compareTo(heap[pos/2]) < 0; pos = pos/2 )
		heap[pos] = heap[pos/2];

	heap[pos] = x;
}
```

#### Deletion

1. Call decrease key until max negative
2. Call extract min as must be minimum value now

#### 4) Other Operations

##### Priority Queue

Queue with following properties:
1. Every item has a priority associated with it
2. Element with high priority is dequeued before element with low
3. If two have same priority, served according to order in the queue

Quite literally implemented as a binary heap with priority as keys.

#### 5) Advantages, Disadvantages, Applications

##### +++
- Binary heap supports insert, delete, extract max, and decrease key operations in O(log n) time
- No extra space for pointers as implementation with array
- Created in O(n) time

##### ---
- Searching is O(n)
- Finding a successor or predecessor of an element takes O(n)

##### Applications
1. Priority queues
	- Binary heap supports insert, delete, extract max, and decrease key operations in O(log n) time
2. Binomial and Fibonacci heap
	- Perform union in O(log n) which is O(n) in binary heap
3. Order statistics
	- Efficiently finding kth smallest or largest element in array
4. Graph algorithms with priority queue
	- Dijkstra's shortest path and Prim's minimum spannning tree