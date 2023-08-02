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

## Left Join

- **Question:** How do left join works?
    - It will do an inner join;
    - and add records that exist in the left that is not in the right table filling the values with null.

## Right Join

- **Question:** How do right join works?
    - It will do an inner join;
    - and add records that exist in the right that is not in the left table filling the values with null.

## Full Join

- **Question:** How do full join works?
    - It will do an inner join;
    - and add records that exist in the left that is not in the right table filling the values with null;
    - and add records that exist in the right that is not in the left table filling the values with null.

## Cross Join

- **Question:** How do cross join works?
    - It will match every record of the left to the right even though they are not actually equal;
    - The number of records of the results will always be count(left) * count(right).

## Natural Join (Not Recommended)

- **Question:** How do natural join works?
    - no need to write the `ON` keyword and specify a critera;
    - if there are same name column existing on the two tables it will do an inner join;
    - elif there are no identical columns on the tables it will do a cross join;
