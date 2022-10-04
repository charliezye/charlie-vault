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