### Intermediate:

* Aggregation functions `COUNT`, `MIN`, `MAX`, `SUM`, `AVG` are used to perform operations across entire columns.
* To count the total number of rows in a table, use `COUNT(*)` or `COUNT(1)`.
To count the non-null entries in a column, use `COUNT(column_name)`.
Count can be used both on numeric as well as non-numeric columns.
While using count, since this will return just one value, one must group by the other columns displayed in order to avoid an error.
e.g.
```sql
SELECT COUNT(col_name) AS display_name
  FROM table_name
```
* `SUM` can be used to aggregate numeric columns.
* `MIN` and `MAX` can be used both on numeric and non-numeric columns.
* `AVG` can be used to find the average of numeric quantities, excluding nulls.
* To group results by particular columns, use the `GROUP BY` clause with column names separated by a comma.
e.g.
```sql
SELECT col1,
       col2,
       COUNT(*)
 FROM table_name
 GROUP BY col1, col2
 ORDER BY col1, col2
```
* Limits, when applied, come into play after the grouping is performed.
* If one wants to filter based on aggregated values, `WHERE` won't work. Instead, one must use the `HAVING` clause:
e.g.
```sql
SELECT col1,
       col2,
       MAX(col3)
 FROM table_name
 GROUP BY col1, col2
 HAVING MAX(col3) > cutoff_value
 ORDER BY col1, col2
```
* Order of commands learnt so far:
  * `SELECT`
  * `FROM`
  * `WHERE`
  * `GROUP BY`
  * `HAVING`
  * `ORDER BY`
* `SELECT DISTINCT` can be used to list the distinct values among column(s).
When used on more than one column (separated by commas) all unique combinations of the unique values in each column will be returned.
* To handle if-then-else, SQL uses the `CASE` statement with the `SELECT` clause.
`WHEN`, `THEN`, `END` is compulsory, `ELSE` is optional. e.g.
```sql
SELECT col1,
       col3,
       CASE WHEN col3 = value1 THEN label1
            WHEN col3 = value2 THEN label2
            ELSE NULL END AS My_col_name
  FROM table_name
```
* `CASE` can be used in conjunction with `GROUP BY` for useful complex queries.
* To use an alias for a table name, just add the name after `FROM table_name`.
* To join two tables used the clause `FROM table_1 JOIN table_2 ON table_1_col = table_2_col`.
* The above join is the same as using the clause `INNER JOIN`. The result is an intersection.
i.e. only rows for which there is a match based on the `ON` criteria are included and others are discarded.
* If you have columns with the same name in the two tables being joined, give them a new name while displaying them,
else contents of the two columns will be displayed to be identical even if they are not really identical.
* Outer joins can be of three types:
  * `LEFT JOIN` or `LEFT OUTER JOIN`
  * `RIGHT JOIN` or `RIGHT OUTER JOIN`
  * `FULL JOIN` or `FULL OUTER JOIN`
* A visual representation of the different types of joins can be found [here](http://joins.spathon.com/).
`LEFT JOIN` includes all rows from the `FROM` table in addition to the table intersection.
`RIGHT JOIN` includes all rows from the `RIGHT JOIN` table in addition to the table intersection.
`TOTAL OUTER JOIN` includes all rows from both tables (with the intersecting rows clubbed).
* If one wants to filter _one_ of the tables _before_ a join is performed, 
one can specify the filtering criteria as part of the `ON` clause. 
If however one wants to filter the table resulting out of the join, one can use the `WHERE` clause.
* To stack two tables, use the `UNION` clause. This will skip any rows that are exactly identical.
To stack tables without any deletion of rows, use `UNION ALL`.
To apply a `UNION`, both tables should have the same number of columns and 
should also have the same column data types in the same order (however the column names need not be the same).
* Self joins, inequality joins and joining on multiple keys are all possible.

<br>

[Back to course notes](../Course_Notes.md)
