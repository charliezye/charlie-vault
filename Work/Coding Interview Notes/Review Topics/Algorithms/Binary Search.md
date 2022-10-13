# Binary Search
###### O(log n) time
###### Requirements: Array must be sorted

- Basic concept: Repeatedly divide the search interval in half

### Basic Steps
1. Begin with the middle element of the array
2. If the value of the search item is equal to the middle element, then return its index
3. Else if the value of the search item is less than the middle element, narrow the search interval to the lower half
4. Otherwise (if the value is greater), narrow it to the upper half
5. Repeated the first four steps until the value is found or the interval is empty
	1. If empty, this means not found in array

### Implementations

##### Iterative Method
###### O(log n) time, O(1) space
- Repeat until start index is equal to end index
1. Calculate middle index
2. Compare
	1. If middle element equal to search item, return item
	2. If middle element less than search item, set end index to middle - 1
	3. If middle element greater, set start index to middle + 1

###### Code:
```
binarySearch(arr, x, startIndex, endIndex)
	repeat till startIndex = endIndex
	   mid = (startIndex + endIndex)/2
		   if (x == arr[mid])
		   return mid
	
		   else if (x > arr[mid]) // x is on the right side
			   startIndex = mid + 1
	
		   else                  // x is on the left side
			   endIndex = mid - 1
```

##### Recursive Method
###### O(log n) time, O(log n) space
- Base case: If start index is greater than end index, return false
1. Calculate middle index
2. Compare
	1. If middle element equal to search item, return item
	2. If middle element less than search item, recursive call with mid - 1 as start index
	3. If middle element greater, recursive call with mid + 1 as end index

###### Code:
```
binarySearch(arr, x, low, high)
   if low > high
	   return False 

   else
	   mid = (low + high) / 2 
		   if x == arr[mid]
		   return mid

	   else if x > arr[mid]        // x is on the right side
		   return binarySearch(arr, x, mid + 1, high)
	   
	   else                        // x is on the left side
		   return binarySearch(arr, x, low, mid - 1)
```

##### Diagram:
![[Pasted image 20221013091337.png]]