# SQL Joins

>Compiled by: Selwyn Zack Tarriela <br> Date: 03/08/2023 <br> Github: [selwyntarr](https://github.com/selwyntarr)

## Table of Contents
- [Sample Data](#Sample-Data)
- [Inner Join](#Inner-Join)
- [Left Join](#Left-Join)
- [Right Join](#Right-Join)
- [Full Join](#Full-Join)
- [Natural Join (Not Recommended)](#Natural-Join-(Not-Recommended))
- [Cross Join](#Cross-Join)
- [Self Join](#Self-Join)

---


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

`Beware: null is not equal to null (they are representation only of no value) cannot be a match when joining`

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

## Self Join

- **Question:** How to do a self join?
    - Reference the table to itself by using a common table expression or a temporary result set

- **Example:** What query to get the output table?

<table>
  <tr>
    <th>Source Table</th>
    <th>Output</th>
  </tr>
  <tr>
    <td>
        <table>
            <tr>
                <th>Source</th>
                <th>Destination</th>
                <th>Travel Time (mins)</th>
            </tr>
            <tr>
                <td>Marikina</td>
                <td>San Mateo</td>
                <td>60</td>
            </t>
            <tr>
                <td>San Mateo</td>
                <td>Marikina</td>
                <td>60</td>
            </t>
            <tr>
                <td>Marikina</td>
                <td>Cainta</td>
                <td>60</td>
            </t>
            <tr>
                <td>Cainta</td>
                <td>Marikina</td>
                <td>60</td>
            </t>
            <tr>
                <td>San Mateo</td>
                <td>Montalban</td>
                <td>60</td>
            </t>
            <tr>
                <td>Montalban</td>
                <td>San Mateo</td>
                <td>60</td>
            </tr>
        </table>
    </td>
    <td>
        <table>
            <tr>
                <th>Source</th>
                <th>Destination</th>
                <th>Travel Time (mins)</th>
            </tr>
            <tr>
                <td>Marikina</td>
                <td>San Mateo</td>
                <td>60</td>
            </tr>
            <tr>
                <td>Marikina</td>
                <td>Cainta</td>
                <td>60</td>
            </tr>
            <tr>
                <td>San Mateo</td>
                <td>Montalban</td>
                <td>60</td>
            </t>
        </table>
    </td>
  </tr>
</table>

- **Solution:**
    - Match the table to itself with source and its destination
    - Add a condition where the `id_1` should be less than `id_2`, this will remove any duplicates 
```
WITH cte AS (
    SELECT * 
    , ROW_NUMBER() OVER() AS id --to generate row_id
    from source_table
)
SELECT cte T1 -- create first instance
SELECT cte T2 -- create second instance
    ON T1.source = T2.destination
    AND T1.id < T2.id --this will remove the duplicate matches
```
    
## References:
`Different Types of Joins` -> https://www.youtube.com/watch?v=xUsY2jWQa1w <br>
`Self Join` -> https://www.youtube.com/watch?v=WhkNQ3g0U64
