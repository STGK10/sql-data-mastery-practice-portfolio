# SQLBolt Practices Repository

Source:  [sqlbolt.com](https://sqlbolt.com)

## Index

00. [SQL into](#00-SQL-intro)
01. [SELECT Queries 101](#01-select-queries-101)
02. [Queries With Constraints](#02-queries-with-constraints
03. [Filtering and Sorting Query Results](#04-filtering-and-sorting-query-results)
04. [Simple SELECT Queries](#05-simple-select-queries)
05. [Multi-table Queries With JOINs](#06-multi-table-queries-with-joins)
06. [OUTER JOINs](#07-outer-joins)
07. [A Short Note on NULLs](#08-a-short-note-on-nulls)
08. [Queries With Expressions](#09-queries-with-expressions)
09. [Queries With Aggregates (Pt. 1)](#10-queries-with-aggregates-pt-1)
10. [Queries With Aggregates (Pt. 2)](#11-queries-with-aggregates-pt-2)
11. [Order of Execution of a Query](#12-order-of-execution-of-a-query)
12. [Inserting Rows](#13-inserting-rows)
13. [Updating Rows](#14-updating-rows)
14. [Deleting Rows](#15-deleting-rows)
15. [Creating Tables](#16-creating-tables)
16. [Altering Tables](#17-altering-tables)
17. [Dropping Tables](#18-dropping-tables)


## 00. SQL intro

Everything generate data, in the era of AI, data becomes the most valuable asset in the world.
SQL (Structured Query Language) is a language that allows to query, manipulate and transform data from a relational database. Therefore it is the language through which we can talk to data.
The most popular SQL data bases are SQLite, MySQL, Postgres, Oracle and Microsoft SQL Server. They all support the common SQL language standard.

A relational database represent a collection of related 2D tables (similar to Excel spreadsheet) with a finite number of named columns (attributes or properties of the table) and any number of rows data. 

For example, if the Department of Motor Vehicles had a database, you might find a table containing all the known vehicles that people in the state are driving. This table might need to store the model name, type, number of wheels, and number of doors of each vehicle for example.

Table: Vehicules

| ID | Model             | # Wheels |  # Doors |  Type  
|----| ----------------- |--------- |--------- |------------
|  1 | Ford Focus        |  4       |   4      | Sedan      
|  2 | Tesla Roadster    |  4       |   2      | Sports     
|  3 | Kawakasi Ninja    |  2       |   0      | Motorcycle 
|  4 | McLaren Formula 1 |  4       |   0      | Race       
|  5 | Tesla S           |  4       |   4      | Sedan      


In such a database, you might find additional related tables containing information such as a list of all registered drivers in the state, the types of driving licenses that can be granted, or even driving violations for each driver.
By learning SQL, the goal is to learn how to answer specific questions about this data, like "What types of vehicles are on the road have less than four wheels?", or "How many models of cars does Tesla produce?", to help us make better decisions down the road.


## 01. SELECT queries 101

We need SELECT statements (refered to as queries) to retrieve data from a SQL database. A query in itself is just a statement which declares what data we are looking for, where to find it in the database, and optionally, how to transform it before it is returned.



```
-- Select query for a specific columns
SELECT 
    column_1, 
    column_2, 
    ... ,
    column_k
FROM mytable

```

This query will display a two-dimensional set of rows and columns from the table, showing only the columns specified immediately after the SELECT clause. However if we wanted to display all the columns from the table we would have use the asterisk (*) instead of listing all the column names individually.

```
-- Select query for all columns
SELECT *
FROM mytable
```

Notice: SQL doesn't require you to write the keywords all capitalized, but as a convention, it helps people distinguish SQL keywords from column and tables names, and makes the query easier to read.

### Exercice

We will be using a database with data about some of Pixar's classic movies for most of our exercises. This first exercise will only involve the Movies table, and the default query below currently shows all the properties of each movie. 


Table: Movies

| id | Title | Director | Year | Length_minutes |
| --:| :--- | :--- | ---: | -------------: |
| 1 | Toy Story | John Lasseter | 1995 | 81 |
| 2 | A Bug's Life | John Lasseter | 1998 | 95 |
| 3 | Toy Story 2 | John Lasseter | 1999 | 93 |
| 4 | Monsters, Inc. | Pete Docter | 2001 | 92 |
| 5 | Finding Nemo | Andrew Stanton | 2003 | 107 |
| 6 | The Incredibles | Brad Bird | 2004 | 116 |
| 7 | Cars | John Lasseter | 2006 | 117 |
| 8 | Ratatouille | Brad Bird | 2007 | 115 |
| 9 | WALL-E | Andrew Stanton | 2008 | 104 |
| 10 | Up | Pete Docter | 2009 | 101 |
| 11 | Toy Story 3 | Lee Unkrich | 2010 | 103 |
| 12 | Cars 2 | John Lasseter | 2011 | 120 |
| 13 | Brave | Brenda Chapman | 2012 | 102 |
| 14 | Monsters University | Dan Scanlon | 2013 | 110 |




Tasks:

1. Find the title of each film
```
SELECT 
    Title
FROM movies;
```


2. Find the director of each film
```
SELECT 
    Director
FROM movies;
```


3. Find the title and director of each film
```
SELECT 
    Title,
    Director
FROM movies;
```

4. Find the title and year of each film
```
SELECT 
    Title,
    Year
FROM movies;
```

5. Find all the information about each film
```
SELECT * FROM movies;
```





## 02. Queries with constraints

To filter certain results from being returned, we need to use a WHERE clause in the query. The clause is applied to each row of data by checking specific column values to determine whether it should be included in the results or not.  

```
--Select query with constraints
SELECT 
    column_1,
    Column_2
    ...,
    column_k
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

More complex clauses can be constructed by joining numerous AND or OR logical keywords (ie. num_wheels >= 4 AND doors <= 2). 
Here are some useful operators that you can use for numerical data (ie. integer or floating point):


| Operator | Condition | SQL Example |
| :--- | :--- | :--- |
| `=`, `!=`, `<`, `<=`, `>`, `>=` | Standard numerical operators | `col_name != 4` |
| `BETWEEN ... AND ...` | Number is within range of two values (inclusive) | `col_name BETWEEN 1.5 AND 10.5` |
| `NOT BETWEEN ... AND ...` | Number is not within range of two values (inclusive) | `col_name NOT BETWEEN 1 AND 10` |
| `IN (...)` | Number exists in a list | `col_name IN (2, 4, 6)` |
| `NOT IN (...)` | Number does not exist in a list | `col_name NOT IN (1, 3, 5)` |


Constraints in clauses allows the query to run faster due to the reduction in unnecessary data being returned.

When writing WHERE clauses with columns containing text data, SQL supports a number of useful operators to do things like case-insensitive string comparison and wildcard pattern matching. We show a few common text-data specific operators below: 

| Operator | Condition | Example |
| :--- | :--- | :--- |
| `=` | Case sensitive exact string comparison (notice the single equals) | `col_name = "abc"` |
| `!=` or `<>` | Case sensitive exact string inequality comparison | `col_name != "abcd"` |
| `LIKE` | Case insensitive exact string comparison | `col_name LIKE "ABC"` |
| `NOT LIKE` | Case insensitive exact string inequality comparison | `col_name NOT LIKE "ABCD"` |
| `%` | Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE) | `col_name LIKE "%AT%"`<br>(matches "AT", "ATTIC", "CAT" or even "BATS") |
| `_` | Used anywhere in a string to match a single character (only with LIKE or NOT LIKE) | `col_name LIKE "AN_"`<br>(matches "AND", but not "AN") |
| `IN (...)` | String exists in a list | `col_name IN ("A", "B", "C")` |
| `NOT IN (...)` | String does not exist in a list | `col_name NOT IN ("D", "E", "F")` |

Note: All strings must be quoted so that the query parser can distinguish words in the string from SQL keywords.

### Exercice
Here's the definition of a query with a WHERE clause again:
```
--Select query with constraints
SELECT 
    column_1,
    Column_2
    ...,
    column_k
FROM mytable
WHERE condition
    AND/OR another_condition
    AND/OR …;
```

Table: movies

### Movies

| Id | Title | Director | Year | Length_minutes |
| --:| :--- | :--- | ---: | -------------: |
| 1 | Toy Story | John Lasseter | 1995 | 81 |
| 2 | A Bug's Life | John Lasseter | 1998 | 95 |
| 3 | Toy Story 2 | John Lasseter | 1999 | 93 |
| 4 | Monsters, Inc. | Pete Docter | 2001 | 92 |
| 5 | Finding Nemo | Andrew Stanton | 2003 | 107 |
| 6 | The Incredibles | Brad Bird | 2004 | 116 |
| 7 | Cars | John Lasseter | 2006 | 117 |
| 8 | Ratatouille | Brad Bird | 2007 | 115 |
| 9 | WALL-E | Andrew Stanton | 2008 | 104 |
| 10 | Up | Pete Docter | 2009 | 101 |
| 11 | Toy Story 3 | Lee Unkrich | 2010 | 103 |
| 12 | Cars 2 | John Lasseter | 2011 | 120 |
| 13 | Brave | Brenda Chapman | 2012 | 102 |
| 14 | Monsters University | Dan Scanlon | 2013 | 110 |
| 87 | WALL-G | Brenda Chapman | 2042 | 97 |


Go ahead and try and write some queries with the operators above to limit the results to the information we need from the Movies table for each task below: 

1. Find the movie with a row id of 6
```
SELECT 
    * 
FROM movies
WHERE id = 6
```


2. Find the movies released in the years between 2000 and 2010
```
SELECT 
    * 
FROM movies
WHERE Year BETWEEN 2000 AND 2010
```

3. Find the movies not released in the years between 2000 and 2010
```
SELECT 
    * 
FROM movies
WHERE Year NOT BETWEEN 2000 AND 2010
```

4. Find the first 5 Pixar movies and their release year
```
SELECT 
    * 
FROM movies
WHERE id BETWEEN 1 AND 5
```

5. Find all the Toy Story movies
```
SELECT 
    * 
FROM movies
WHERE Title LIKE "Toy %"
```

6. Find all the movies directed by John Lasseter
```
SELECT 
    * 
FROM movies
WHERE Director LIKE "John Lasseter"
```

7. Find all the movies (and director) not directed by John Lasseter
```
SELECT 
    Title,
    Director
FROM movies
WHERE Director NOT LIKE "John Lasseter"
```

8. Find all the WALL-* movies
```
SELECT 
   *
FROM movies
WHERE Title LIKE "Wall%"
```


## 03. Filtering and Sorting Query Results