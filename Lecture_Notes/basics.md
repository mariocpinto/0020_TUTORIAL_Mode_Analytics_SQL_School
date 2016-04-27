### Basics:

* To select a set of columns from a table, use:
```sql
SELECT * FROM table_name
SELECT col1, col2, col3 FROM table_name
```
* SQL is not sensitive to spaces and line breaks.
* Avoid spaces in column names, else you will need to reference column names by enclosing them in double quotes.
* If you want to display results with a different column name, use the `AS` clause. e.g.
```sql
SELECT col1 AS "New Column Header"
  FROM table_name
```
* Note that the capitalization in column names used with `AS` will only appear if the new name is enclosed in double quotes. 
Otherwise, the new name will be turned into lowercase. e.g.
The following query will return results with the column name new_column (without capitalization).
```sql
SELECT col1 AS New_Column
  FROM table_name
```
* The `LIMIT` clause can be used to limit the number of rows returned by a query:
```sql
  SELECT col1 AS New_Column
  FROM table_name
  LIMIT 15
```
* The `WHERE` clause can be used to filter rows based on certain criteria for column values. 
Note, however, that this will also filter out NULL values. e.g.
```sql
SELECT *
  FROM table_name
 WHERE criteria
 ```
* The `SELECT`, `FROM` and `WHERE` clauses must be in this order.
* The comparison operators that can be used are `=`, `!=`, `>`, `<`, `>=`, `<=`.
 These can be used both with numeric and non-numeric data.
 For non-numeric data, the values need to be included in single quotes and operators such as `<` will operate based on alphabetic order. Further, note that 'An' is considered > 'A'.
* One can use `+`, `-`, `*`, `/` and `()` to operate on values from the same row.
 (For values from different rows, aggregation functions need to be used).
These columns are called derived columns". e.g.
```sql
SELECT col1, col2,
       2*col1 - col2/4 as My_Calculated_Column
FROM table_name
```
* It is a convention to usually put double quotes around column names.
* The `LIKE` (case sensitive) and `ILIKE` (not case sensitive) clauses can be used in conjunction with `WHERE`
to filter based on a partial string match.
The `%` symbol is used as a wildcard character and the `_` symbol is used as a single character wildcard.
* The `IN` clause can be used in conjunction with `WHERE` to filter based on values being present in a list.
The list is represented by multiple values separated by a comma and included in round brackets.
* The `BETWEEN` clause in conjunction with `AND` can be used along with the `WHERE` clause to filter values in a range. 
Note that the end values are included. e.g.
```sql
SELECT *
  FROM table_name
 WHERE column_name BETWEEN val1 AND val2
```
* One cannot perform arithmatic with NULL values. i.e. column_name = NULL does **not** work.
Instead, use the `IS NULL` clause along with `WHERE`. Note that a column that contains blank spaces is not considered NULL.
To get non-NULL columns, use `IS NOT NULL`.
* The `AND`, `OR` and `NOT` clauses can be used to combine conditions used with `WHERE`.
* The `ORDER BY` clause can be used to sort results by a particular order. 
The `DESC` clause can be used to sort in descending order. 
One can sort by multiple columns by passing column names separated by a comma e.g.
```sql
SELECT * 
  FROM table_name
 ORDER BY col_1 DESC, col_2
```
* In some flavors of SQL, one can pass column numbers (starting from 1) instead of column names to `ORDER BY`.
The name to number mapping is defined by the order of columns in the `SELECT` clause.
* When the `LIMIT` clause is used along with `ORDER BY`, the ordering is applied before the limit is applied.
* To comment out a single line, sue `--`. For multiple lines, use `/* */`.

<br>

[Back to course notes](../Course_Notes.md)
