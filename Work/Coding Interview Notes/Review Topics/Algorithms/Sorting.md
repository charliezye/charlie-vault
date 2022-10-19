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


`void` `bubbleSort(``int` `arr[])`

    `{`

        `int` `n = arr.length;`

        `for` `(``int` `i =` `0``; i < n -` `1``; i++)`

            `for` `(``int` `j =` `0``; j < n - i -` `1``; j++)`

                `if` `(arr[j] > arr[j +` `1``]) {`

                    `// swap arr[j+1] and arr[j]`

                    `int` `temp = arr[j];`

                    `arr[j] = arr[j +` `1``];`

                    `arr[j +` `1``] = temp;`

                `}`

    `}`
#### Merge Sort
###### O(n<sup>2</sup>) time, O(1) space

#### Quick Sort
###### O(n<sup>2</sup>) time, O(1) space


#### Heap Sort
###### O(n<sup>2</sup>) time, O(1) space
