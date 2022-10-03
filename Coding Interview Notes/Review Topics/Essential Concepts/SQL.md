### SQL Concepts

###### Syntax
SELECT *columns*
FROM *table_name*
WHERE *conditional*

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
	- When 
