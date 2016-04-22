## SQL School: Tutorial Notes


These are the [notes I took](Course_Notes.md) as I worked through [Mode Analytics'](https://modeanalytics.com/)
[SQL School](https://sqlschool.modeanalytics.com/):  

#### Basics:
* To select a set of columns from a table, use:
```sql
SELECT * FROM table_name
SELECT col1, col2, col3 FROM table_name
```
* SQL is not sensitive to spaces and line breaks.
* Avoid spaces in column names, else you will need to reference column names by enclosing them in double quotes.
* If you want to display results with a different column name, use the `AS` keyword. e.g.
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
* The LIMIT keyword can be used to limit the number of rows returned by a query:
```sql
SELECT col1 AS New_Column
  FROM table_name
  LIMIT 15





