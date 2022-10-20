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
Hashing is a technique or process of mapping keys and values into a hash table using a hash function.
- Done for faster access to elements
	- Search, insert, and delete all O(1)
- Efficiency of mapping itself depends on hash function used

### 2) Implementation

#### Hash Table
An array that stores pointers to records
- An entry is null if no existing value has hash function value equal to index for entry

#### Hash Function
Converts a large value into a small practical integer value used as index in hash table
Should be:
1.  Efficiently computable. 
2.   Should uniformly distribute the keys (Each table position equally likely for each).
3.  Should minimize collisions.
4.  Should have a low load factor(number of items in table divided by size of the table).

#### Collision Handling
It is possible two keys result in the same value given the hash function. 
If a new key maps to an occupied slot, we can do the following:
1. Chaining
	- The idea is to make each cell of hash table point to a linked list of records that have same hash function value
	- Chaining is simple, but requires additional memory outside the table.
2. Open Addressing
	- In open addressing, all elements are stored in the hash table itself. Each table entry contains either a record or null
	- When searching for an element, we examine the table slots one by one until the desired element is found or it is clear that the element is not in the table.


### 3) Basic Operations

#### Get
###### O(1) time and space
Hash function converts input key into hash index and checks at index.
- If found, the value at the index will be returned, otherwise will return -1

#### Put
###### O(1) time and space
Hash function converts input key into hash index and places value at index.
- If value already exists, will typically be replaced or add as node to linked list if separate chaining

#### Delete
###### O(1) time and space
Hash function converts input key into hash index and looks for value there
- If found, will delete and replace with null

### 4) Other Operations

#### Rehashing
Basically, when the load factor increases to more than its pre-defined value (default value of load factor is 0.75), the time complexity to carry out operations increases.
- To overcome this, the size of the array is increased (doubled) and all the values are hashed again and stored in the new double sized array to maintain a low load factor and low complexity.
- Call insert on each element in original on new larger hash array


### 5) Advantages, Disadvantages, Applications

##### +++
- O(1) insert, delete, search

##### ---
- Need for rehashing
- If many collisions problematic

##### Applications
- Any kind of repeated lookup or search operations on well-defined set of values