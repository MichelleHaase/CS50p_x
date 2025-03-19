# Lecture 1 Querying
General Order of Keywords <br>
* SELECT – Specifies which columns to retrieve.
* DISTINCT (optional) – Removes duplicate rows from the result.
* FROM – Specifies the table(s) to retrieve data from.
* JOIN – Combines data from multiple tables.
* ON – Defines the condition for the JOIN operation.
* WHERE – Filters rows before grouping.
* GROUP BY – Groups rows that have the same values in specified columns.
* HAVING – Filters grouped rows based on a condition.
* WINDOW (optional) – Defines a window for window functions (used in advanced queries).
* ORDER BY – Sorts the result set by specified columns.
* LIMIT / FETCH – Restricts the number of rows returned.
* OFFSET – Skips a specified number of rows before returning results.

## wildcards with LIKE
% can match any char <br>
_ can match any single char <br>
when searching strings 'LIKE' is Case insensitive '=' is Case sensitive <br>
```sql
SELECT "title" FROM "list" WHERE "title" LIKE '%love%'; -- selects everything that has love in it 
SELECT "title" FROM "list" WHERE "title" LIKE 'love %'; -- selects everything that starts with love
SELECT "title" FROM "list" WHERE "title" LIKE 'p_re'; -- searches for words that start with p have one more letter than re, usefull if spelling is unclear can be used several times in row like p___
```
## Ranges with BETWEEN AND
```sql
SELECT "title", "year" FROM "list" WHERE "year" BETWEEN 2019 AND 2022; -- selects titles from the years 2019 to 2022
SELECT "title", "rating" FROM "list" WHERE "rating" > 4.0; 
```
## ORDER BY
by default Ascending tags ASC DESC <br>
## Aggregate functions
* COUNT AVG MIN MAX SUM
```sql
SELECT ROUND(AVG("rating"),2) AS "Avarage rating" FROM "list"; -- calcs the average rating and rounds it to two decimal points and names the column "Avarage rating"
SELECT COUNT(DISTINCT "publisher") FROM "list";
```
# Lecture 2