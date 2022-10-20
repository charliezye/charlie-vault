### Bitwise Operations

##### Operators

###### **&** (Bitwise AND)
- Input: Two equal-length bit patterns
1. If bits in compared positions are both 1, resulting bit is 1
2. If either is not, resulting bit is 0

###### | (Bitwise OR)
- Input: Two equal-length bit patterns
1. If bits in compared position both 0, resulting bit is 0
2. If either is not, resulting bit is 1

###### ^ (Bitwise XOR)
- Input: Two equal-length bit patterns
1. If bits in compared position do not match (1 and 0), resulting bit is 1
2. If they match, bit is 0
- Efficient in checking for duplicates

###### ~ (Bitwise NOT)
- Input: Any bit pattern
1. Flips the bits of the a number
	1. If i'th bit is 0, change to 1, and vice versa
- If passed positive value X, returns (-X - 1)

###### << (Left Shift)
- Input: Any bit pattern
- Shifts bits to the left
1. Bits towards the left are removed
2. Zeros are added to the right for every bit removed
- Every bit shift left effectively doubles value of original bits
	- 1 << n = 2<sup>n</sup>

###### >> (Right Shift)
- Input: Any bit pattern
- Shifts bits to the right
1. Adds copies of bit to leftmost end from the left
2. Bits are removed to the right
- Usually halves the value of original bits
	- 1 << n = 2<sup>n</sup>

#### Basic Concepts

###### 1. Get negative of number

**-x = ~x + 1**
- Invert bits and add one

###### 2. Find element that appears once in array that others appear 3 times

- Run a loop for all elements in the array. At the end of every iteration, maintain the following two values.
	1. ones: The bits that have appeared 1st time or 4th time or 7th time .. etc.
	2. twos: The bits that have appeared 2nd time or 5th time or 8th time .. etc.
- Finally, we return the value of ‘ones’

```
 for (int i = 0; i < n; i++) {
            /*"one & arr[i]" gives the bits that are there in
            both 'ones' and new element from arr[]. We
            add these bits to 'twos' using bitwise OR*/
            twos = twos | (ones & arr[i]);
 
            /*"one & arr[i]" gives the bits that are
            there in both 'ones' and new element from arr[].
            We add these bits to 'twos' using bitwise OR*/
            ones = ones ^ arr[i];
 
            /* The common bits are those bits which appear third time
            So these bits should not be there in both 'ones' and 'twos'.
            common_bit_mask contains all these bits as 0, so that the bits can
            be removed from 'ones' and 'twos'*/
            common_bit_mask = ~(ones & twos);
 
            /*Remove common bits (the bits that appear third time) from 'ones'*/
            ones &= common_bit_mask;
 
            /*Remove common bits (the bits that appear third time) from 'twos'*/
            twos &= common_bit_mask;
        }
        return ones;
```

#### Hacks

###### 1. Even/Odd Integer

**n & 1**

- Output: **1*** if n is **odd**, or **0** if n is **even**

###### 2. Two Integers Opposite Signs

**x ^ y**

- Output: Negative if x and y have opposite signs

###### 3. Add 1 to an integer

**-~x**

- Uses concept below

###### 4. Swap two numbers without using any third variable

**x = x ^ y;
y = x ^ y;
x = x ^ y;**

- Use XOR operators to swap using property **x ^ x = 0**