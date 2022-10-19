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
```
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
```
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
```
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
```
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
Another D&C algorithm. Picks an element as a pivot and partitions the given array around the picked pivot.
- Different versions
	- Always pick the first element as a pivot.
	- Always pick the last element as a pivot (implemented below)
	- Pick a random element as a pivot.
	- Pick median as the pivot.
- Partition
	- Given an array and an element x of it as the pivot, put x  at its correct position in a sorted array, and put all smaller elements before x and greater after x, all in linear time

1. Start with left-most element and keep track of index of smaller or equal elements as i
2. If we find a smaller element, swap current element with i
3. Otherwise, ignore current element

```

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
###### O(n<sup>2</sup>) time, O(1) space
