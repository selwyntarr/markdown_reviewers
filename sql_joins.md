# SQL Joins

>Compiled by: Selwyn Zack Tarriela
>Date: 03/08/2023
>Github: [selwyntarr](https://github.com/selwyntarr)

## Sample Data
Create **table_one** query:
```
CREATE TABLE table_one (
    num INT
);

INSERT INTO table_one (num)
VALUES (1), (1), (1), (2), (3), (3), (3);
```
Create **table_two** query:
```
CREATE TABLE table_two (
    num INT
);

INSERT INTO table_two (num)
VALUES (1), (1), (2), (2), (4), (null);
```
**Output Dataset**
| table_one | table_two|
| --- | --- |
| 1 | 1 |
| 1 | 1 |
| 1 | 2 |
| 2 | 2 |
| 3 | 4 |
| 3 | null |
| 3 | |

## Inner Join

- **Question:** How do inner join works?
    - It will try to match value of the record of your left table to all the values in the right table; 
    - and then it will proceed on the next record of your left table and try to match it again with all values in the right table; 
    - until all there no records left on your left table.   
