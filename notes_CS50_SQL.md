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
# Lecture 2 Relating
## Relationships

* one to one one author writes one book
* one to many one author writes many books
* many to many many authors write books together

### Crows foot Notation
![alt text](p17.jpg)
One to One would look like
![alt text](p19.jpg)

## subqueries
```sql
SELECT "name"
FROM "authors"
WHERE "id" = (
    SELECT "author_id"
    FROM "authored"
    WHERE "book_id" = (
        SELECT "id"
        FROM "books"
        WHERE "title" = 'Flights'
    )
);
```
always run form the most inside parenthesis first
* each nesting gets indentation
### IN
```sql
SELECT "title"
FROM "books"
WHERE "id" IN (
    SELECT "book_id"
    FROM "authored"
    WHERE "author_id" = (
        SELECT "id"
        FROM "authors"
        WHERE "name" = 'Fernanda Melchor'
    )
);
```
### JOIN
```sql
SELECT *
FROM "sea_lions"
JOIN "migrations" ON "migrations"."id" = "sea_lions"."id";
```
* standart in sqlite is an inner *JOIN*
    * only rows that have the identifier in both tables are joined
* *LEFT JOIN* - the data in the table first named is prioritised, the the data from the first table is kept even if there are no corresponding values in the right table, only matching rows have entries in all columns
* *RIGHT JOIN* - the data in the table secondly named is prioritised, the the data from the second table is kept even if there are no corresponding values in the left table, only matching rows have entries in all columns
* *FULL JOIN* - all Data is kept only matching rows have entries in all columns
* *NATURAL JOIN* - omits the notation for id columns if there are both named **exactly** the same
```sql
-- Left Join
SELECT *
FROM "sea_lions"
LEFT JOIN "migrations" ON "migrations"."id" = "sea_lions"."id";
-- Natural Join
SELECT *
FROM "sea_lions"
NATURAL JOIN "migrations";
```
## Sets
### INTERSECT
* the intersection of values in two groups eg being both an author an a translator - Authores INTERSECT translators
```sql
SELECT "book_id" FROM "translated"
WHERE "translator_id" = (
    SELECT "id" from "translators"
    WHERE "name" = 'Sophie Hughes'
)
INTERSECT
SELECT "book_id" FROM "translated"
WHERE "translator_id" = (
    SELECT "id" from "translators"
    WHERE "name" = 'Margaret Jull Costa'
);
```

### UNION
* the combination of values of two groups, removes duplicates, eg being either authors or translators, but ensuring each person appears only once in the result - Authores UNION translators
```sql
SELECT 'author' AS "profession", "name" 
FROM "authors"
UNION
SELECT 'translator' AS "profession", "name" 
FROM "translators";
```
### UNION ALL
* the combination of values of two groups, keeps duplicates, eg Listing all occurrences of people being authors or translators, even if they appear in both groups - Authores UNION ALL translators

### EXCEPT
* the exclusion of values from another set in the current set, eg being only an author not a translater - Authores EXCEPT translators
```sql
SELECT "name" FROM "authors"
EXCEPT
SELECT "name" FROM "translators";
```
## GROUP BY
```sql
SELECT "book_id", ROUND(AVG("rating"), 2) AS "average rating"
FROM "ratings"
GROUP BY "book_id"
HAVING "average rating" > 4.0; -- having is where for grouped data
```
grouping data in chunks the apply a function AVG to each chunk, since the data points are no longer addressed individually HAVING is used to address the chunks instead of WHERE