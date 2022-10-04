### SQL Concepts

###### Syntax
SELECT *columns*
FROM *table_name*
WHERE *conditional*

#### Important Calls

###### EXISTS
- Conditional used to see if a certain value exists in a table column
- Can be used in the following form:
```
SELECT columns
FROM table_1
WHERE 
(SELECT 1
FROM table_1
WHERE table_1_id = table_2_id)
```
- This will return values from table 1 where some column matches another from table 2
	- Despite this, using a join or selecting just id from subquery are more efficient

###### JOIN
- There are several types of join, all following the below general syntax
```
Table_1 JOIN Table_2 ON Table_1.table_1_field = Table_2.table_2_field
```
1. Inner JOIN (**JOIN**)
	- Basic join that returns all rows that match **ON** conditional
2. Full (outer) JOIN (**FULL JOIN**)
	- Join that returns rows that match AND rows from **BOTH** tables that do not with null in other columns
3. Left (outer) JOIN (**LEFT JOIN**)
	- Join that returns rows that match AND rows from the **LEFT** table that do not with null in other columns
4. Right (outer) JOIN (**RIGHT JOIN**)
	- Join that returns rows that match AND rows from **RIGHT** tables that do not with null in other columns

###### NULL
- Null values behave differently
- Cannot assert any comparisons on null, can only use 
	- **IS NULL**
	- **IS NOT NULL**
- Additional way to work null check into a **WHERE** clause:
	- **IFNULL**(column, \<valid val\>) 
	- Most useful when using comparison with NOT and nulls may exist
		- e.g. if checking if id <> 1, change null to 0 and will give null as well

###### % and _
- Used in string as wildcards
- % is wildcard of any length, _ is wildcard length one char

###### CASE WHEN \<condition\> THEN __ ELSE __ END
- In place of IF statement

###### IF(\<condition\>, if true;, if false)
- 