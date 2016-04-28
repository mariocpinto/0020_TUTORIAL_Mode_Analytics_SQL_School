### Advanced Topics:

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
  
  * To truncate a datetime filed, one can use the DATETRUNC function as shown below.
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
  
  * To get the current date and time, the following functiosn can be used. These do not require a FROM clause.
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
<br>

[Back to course notes](../Course_Notes.md)
