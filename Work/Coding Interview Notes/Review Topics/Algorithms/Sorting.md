## Sorting

##### Stability
A sorting algorithm is said to be stable if two objects with equal keys appear in the same order in sorted output as they appear in the input data set.

##### In Place
A sorting algorithm is said to be in place if it does not require extra space.

#### Selection Sort
###### O(n<sup>2</sup>) time, O(1) space
Repeatedly find the minimum element from the unsorted part and put it at the beginning.
- Maintains two subarrays:
	- The subarray already sorted
	- The remaining unsorted subarray
- In place
- Not stable

###### Code
``` java
	// One by one move boundary of unsorted subarray
	for (int i = 0; i < n-1; i++)
	{
		// Find the minimum element in unsorted array
		int min_idx = i;
		
		for (int j = i+1; j < n; j++)
			if (arr[j] < arr[min_idx])
				min_idx = j;
		// Swap the found minimum element with the first element
		int temp = arr[min_idx];
		arr[min_idx] = arr[i];
		arr[i] = temp;
	}
```

#### Bubble Sort
###### O(n<sup>2</sup>) time, O(1) space
Works by repeatedly swapping adjacent elements if they are in the wrong order.
- Pass through array looking at pairs, swap any that are out of order
- Now can pass through again and ignore last element as must be in correct place
- If on pass no elements are swapped, know it is sorted
- In place
- Stable

###### Code
``` java
// An optimized version of Bubble Sort
    static void bubbleSort(int arr[], int n)
    {
        int i, j, temp;
        boolean swapped;
        for (i = 0; i < n - 1; i++)
        {
            swapped = false;
            for (j = 0; j < n - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    // swap arr[j] and arr[j+1]
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
 
            // IF no two elements were
            // swapped by inner loop, then break
            if (swapped == false)
                break;
        }
```

#### Insertion Sort
###### O(n<sup>2</sup>) time, O(1) space
Array is virtually split into sorted and unsorted part. Values of unsorted are picked and place at correct position in sorted
- Iterate through entire array
- Compare current key to predecessor
	- If smaller, compare to elements before, moving any greater up to make space for current key to be swapped

###### Code
```java
/*Function to sort array using insertion sort*/
    void sort(int arr[])
    {
        int n = arr.length;
        for (int i = 1; i < n; ++i) {
            int key = arr[i];
            int j = i - 1;
 
            /* Move elements of arr[0..i-1], that are
               greater than key, to one position ahead
               of their current position */
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }
```

#### Merge Sort
###### O(n log n) time, O(n) space
Based on Divide and Conquer. The array is initially divided into two equal halves and then they are combined in a sorted manner.
- Recursive algorithm that continuously splits array in half until it cannot be divided
	- Base case when one element or empty
	- Recursive call merge sort on halves
	- When both halves sorted, merge operation is applied, combining two smaller sorted arrays
- Not in place
- Stable

##### Steps
1. declare array and left, right, mid variable
2. perform merge function.
    1. if left > right
        1. return
    2. mid= (left+right)/2
    3. mergesort(array, left, mid)
    4. mergesort(array, mid+1, right)
    5. merge(array, left, mid, right)

###### Code
```java
 void merge(int arr[], int l, int m, int r)
    {
        // Find sizes of two subarrays to be merged
        int n1 = m - l + 1;
        int n2 = r - m;
 
        /* Create temp arrays */
        int L[] = new int[n1];
        int R[] = new int[n2];
 
        /*Copy data to temp arrays*/
        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];
 
        /* Merge the temp arrays */
 
        // Initial indexes of first and second subarrays
        int i = 0, j = 0;
 
        // Initial index of merged subarray array
        int k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            }
            else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }
 
        /* Copy remaining elements of L[] if any */
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }
 
        /* Copy remaining elements of R[] if any */
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }
 
    // Main function that sorts arr[l..r] using
    // merge()
    void sort(int arr[], int l, int r)
    {
        if (l < r) {
            // Find the middle point
            int m = l + (r - l) / 2;
 
            // Sort first and second halves
            sort(arr, l, m);
            sort(arr, m + 1, r);
 
            // Merge the sorted halves
            merge(arr, l, m, r);
        }
    }
```


#### Quick Sort
###### O(n<sup>2</sup>) time, O(1) space
- Despite being O(n^2) worst case, faster in practice O(n log n) than merge sort and heap sort as worst case rarely happens for any use cases less than nhuge

Another D&C algorithm. Picks an element as a pivot and partitions the given array around the picked pivot.
- Different versions
	- Always pick the first element as a pivot.
	- Always pick the last element as a pivot (implemented below)
	- Pick a random element as a pivot.
	- Pick median as the pivot.
- Partition
	- Given an array and an element x of it as the pivot, put x  at its correct position in a sorted array, and put all smaller elements before x and greater after x, all in linear time
- In place as only use space for recursive calls

##### Steps
1. Start with left-most element and keep track of index of smaller or equal elements as i
2. If we find a smaller element, swap current element with i
3. Otherwise, ignore current element

```java

    // A utility function to swap two elements
    static void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    
    /* This function takes last element as pivot, places
       the pivot element at its correct position in sorted
       array, and places all smaller (smaller than pivot)
       to left of pivot and all greater elements to right
       of pivot */
    static int partition(int[] arr, int low, int high)
    {
  
        // pivot
        int pivot = arr[high];
  
        // Index of smaller element and
        // indicates the right position
        // of pivot found so far
        int i = (low - 1);
  
        for (int j = low; j <= high - 1; j++) {
  
            // If current element is smaller
            // than the pivot
            if (arr[j] < pivot) {
  
                // Increment index of
                // smaller element
                i++;
                swap(arr, i, j);
            }
        }
        swap(arr, i + 1, high);
        return (i + 1);
    }
  
    /* The main function that implements QuickSort
              arr[] --> Array to be sorted,
              low --> Starting index,
              high --> Ending index
     */
    static void quickSort(int[] arr, int low, int high)
    {
        if (low < high) {
  
            // pi is partitioning index, arr[p]
            // is now at right place
            int pi = partition(arr, low, high);
  
            // Separately sort elements before
            // partition and after partition
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }
```

#### Heap Sort
###### O(n log n) time, O(1) space
A comparison-based sorting technique based on the Binary Heap data structure.
- Similar to selection sort where we first find the minimum element and place it at the beginning
- Repeat the same process for the remaining elements
- In place
- Typically not stable
- 2-3x slower than well-implemented quick sort

###### Heapify
- Process of creating a heap data structure from a binary tree represented using an array using recursion
- Starts from first index of non-leaf node whose index is given by n/2 - 1

Pseudocode
```java
heapify(array)  
 Root = array[0]

   Largest = largest( array[0] , array [2 * 0 + 1]/ array[2 * 0 + 2])  
if(Root != Largest)  
 Swap(Root, Largest)
```

###### Algorithm
1. Build complete binary tree from array
2. Convert tree into max heap using heapify
3. Perform heap sort
	1. Delete root node of max-heap and replace with the last node in the heap (swap and remove last node)
	2. Heapify the root of the heap
	3. Repeat while size of heap is greater than 1

Note: Heapify can only be applied if node's children are heapified, so must be performed in bottom up order

###### Code
```java
public void sort(int arr[])
    {
        int N = arr.length;
 
        // Build heap (rearrange array)
        for (int i = N / 2 - 1; i >= 0; i--)
            heapify(arr, N, i);
 
        // One by one extract an element from heap
        for (int i = N - 1; i > 0; i--) {
            // Move current root to end
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
 
            // call max heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }
 
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

###### Iterative Heapify
```java
// function build Max Heap where value
  // of each child is always smaller
  // than value of their parent
  static void buildMaxHeap(int arr[], int n)
  {
    for (int i = 1; i < n; i++)
    {
      // if child is bigger than parent
      if (arr[i] > arr[(i - 1) / 2])
      {
        int j = i;
 
        // swap child and parent until
        // parent is smaller
        while (arr[j] > arr[(j - 1) / 2])
        {
          swap(arr, j, (j - 1) / 2);
          j = (j - 1) / 2;
        }
      }
    }
  }
 
  static void heapSort(int arr[], int n)
  {
    buildMaxHeap(arr, n);
 
    for (int i = n - 1; i > 0; i--)
    {
      // swap value of first indexed
      // with last indexed
      swap(arr, 0, i);
 
      // maintaining heap property
      // after each swapping
      int j = 0, index;
 
      do
      {
        index = (2 * j + 1);
 
        // if left child is smaller than
        // right child point index variable
        // to right child
        if (index < (i - 1) && arr[index] < arr[index + 1])
          index++;
 
        // if parent is smaller than child
        // then swapping parent with child
        // having higher value
        if (index < i && arr[j] < arr[index])
          swap(arr, j, index);
 
        j = index;
 
      } while (index < i);
    }
  }
 
  public static void swap(int[] a, int i, int j) {
    int temp = a[i];
    a[i]=a[j];
    a[j] = temp;
  }
```