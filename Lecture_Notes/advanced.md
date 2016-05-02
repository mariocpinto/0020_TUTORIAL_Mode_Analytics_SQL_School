### Advanced Topics:

The notes below are from [this section](https://sqlschool.modeanalytics.com/advanced/) of the tutorial.

* **Data Types**:
  * A list of different SQL data types can be found [here](http://www.w3schools.com/sql/sql_datatypes_general.asp).
  * One can cast from one data type to another using either `CAST(column_name AS data_type)` or column_name::data_type.
  * Arithmatic on dates often results in data of type `INTERVAL`.
  * One can add intervales to dates using: `data_var + INTERVAL '1 week'`.
  * Current timestamp canbe accessed using the `NOW()` function.

* **Wrangling Messy Data**:
  * `LEFT(string, n)` returns left n characters from string.
  * `RIGHT(string, n)` returns right n characters from string.
  * `LENGTH(string)` returns length of string.
  * `TRIM(how string_of_characters_to_trim FROM string )` 
  {how = leading, trailing, both} returns string with specified characters removed from specifid characters.
  * `POSITION(substring IN string)` returns first location of substring in string, counting from left.
  * `STRPOS(string, substring)` returns the same result as `POSITION`.
  * `SUBSTR(string, starting_pos, n)` returns n characters of string, starting from starting_pos.
  * `CONCAT(str1, str2, str3, ...)` returns a concatenated string. One can alsu use str1 || str2 || str3 ... for the same result.
  * `UPPER(string)` returns the string in upper case.
  * `LOWER(string)` returns the string in lower case.
  * From a datetime field, one can extract the following variables:
  ```sql
  EXTRACT('year'   FROM date_time_variable) AS year,
  EXTRACT('month'  FROM date_time_variable) AS month,
  EXTRACT('day'    FROM date_time_variable) AS day,
  EXTRACT('hour'   FROM date_time_variable) AS hour,
  EXTRACT('minute' FROM date_time_variable) AS minute,
  EXTRACT('second' FROM date_time_variable) AS second,
  EXTRACT('decade' FROM date_time_variable) AS decade,
  EXTRACT('dow'    FROM date_time_variable) AS day_of_week
  ```
  
  * To truncate a datetime field, one can use the DATETRUNC function as shown below.
 This will return a datetime rounded down e.g. 2014-01-31 17:45:00 along with 'year' will result in 2014-01-01 00:00:00.
 ```sql
  DATE_TRUNC('year'   , date_time_variable) AS year,
  DATE_TRUNC('month'  , date_time_variable) AS month,
  DATE_TRUNC('week'   , date_time_variable) AS week,
  DATE_TRUNC('day'    , date_time_variable) AS day,
  DATE_TRUNC('hour'   , date_time_variable) AS hour,
  DATE_TRUNC('minute' , date_time_variable) AS minute,
  DATE_TRUNC('second' , date_time_variable) AS second,
  DATE_TRUNC('decade' , date_time_variable) AS decade
 ```
  
  * To get the current date and time, the following functions can be used. These do not require a FROM clause.
  ```sql
  CURRENT_DATE AS date,
  CURRENT_TIME AS time,
  CURRENT_TIMESTAMP AS timestamp,
  LOCALTIME AS localtime,
  LOCALTIMESTAMP AS localtimestamp,
  NOW() AS now
  ```
  
  * To change the timezone of a timestamp, use the `AT TIME ZONE` function. e.g.
  ```sql
SELECT CURRENT_TIME AS time,
    CURRENT_TIME AT TIME ZONE 'PST' AS time_pst
  ```  
  
  * The `COALESCE` function can be used to replace null values in a column with some other value: 
 `COALESCE(column_with_nulls, value_to_be_used_to_replace_nulls)`.

* **Subqueries**:
 * Subqueries / inner queries / nested queries allow operations to be broken down into multiple steps.
 * Example of using a subquery in the `FROM` clause. Note that the output of the subquery serves as the input of the main query.
 ```sql
 SELECT my_subquery.*
  FROM (
         SELECT *
          FROM table_name
         WHERE condition
       ) my_subquery
 WHERE my_subquery.column = value
 ```
 * Subqueries can also be used in conjunction with `WHERE`, `JOIN` / `ON` and `CASE`.
 These should typically return a single value, except when used with `IN`. The subqueries should not be named in these cases.
 * One can join a subquery that hits the same table as the outer query rather than filtering in the `WHERE` clause.

* **Window Functions**:
 * One can use an aggregation functions i.e. `SUM()`, `COUNT()`, `AVG()` on a subset of data by applying windowing:
 This is achieved by using the `OVER` clause along with the `PARTITION BY` and `ORDER BY` clause.
 `PARTITION BY` will both group and order by the passed column.
 e.g.
 ```sql
 SELECT col1,
       col2,
       SUM(col2) OVER (PARTITION BY col1 ORDER BY col3)
  FROM table
 ```
 * `ROW_NUMBER()` can be used along with partition functions to get the row number as per the `ORDER BY` part.
 * `ROW_NUMBER()` returns a unique value for each entry. 
 `RANK()` returns the same rank for entries with the same column value,
 but then jumps values depending upon the number of repetitions.
 `DENSE_RANK()` works similar to `RANK()` except that it does not jump values.
 * `NTILE(n)` can be used to know which quar/pen/percen-tile the data referred to by `ORDER BY` lies in.
 If the number of data points is lesser than the number of buckets, the calculations may not be right.
 * `LAG(col_name,  count)` and `LEAD(col_name, count)` can be used to access values from previous / following rows 
 that are count rows away.
 * It is possible to define a window alias using the `WINDOW` clause, which should come after the `WHERE` clause:
 e.g. with bike sharing data:
 ```sql
 SELECT start_terminal,
       duration_seconds,
       NTILE(4) OVER ntile_window AS quartile,
       NTILE(5) OVER ntile_window AS quintile,
       NTILE(100) OVER ntile_window AS percentile
  FROM tutorial.dc_bikeshare_q1_2012
 WHERE start_time < '2012-01-08'
WINDOW ntile_window AS 
         (PARTITION BY start_terminal ORDER BY duration_seconds)
 ORDER BY start_terminal, duration_seconds
 ```

* **Making Queries Run Faster**:
 * General suggestions to make queries run faster can be found [here](https://sqlschool.modeanalytics.com/advanced/faster-queries/).
 * The `EXPLAIN` query can be used at the beginning of any query to get a sense of how long it will take to run the query.

<br>

[Back to course notes](../Course_Notes.md)
