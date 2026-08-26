# SQLBolt Practices Repository

Source:  [sqlbolt.com](https://sqlbolt.com).

## Index

00. [SQL into] (#00-SQL-intro)
01. [SELECT Queries 101](#01-select-queries-101)
02. [Queries With Constraints (Pt. 1)](#02-queries-with-constraints-pt-1)
03. [Queries With Constraints (Pt. 2)](#03-queries-with-constraints-pt-2)
04. [Filtering and Sorting Query Results](#04-filtering-and-sorting-query-results)
05. [Simple SELECT Queries](#05-simple-select-queries)
06. [Multi-table Queries With JOINs](#06-multi-table-queries-with-joins)
07. [OUTER JOINs](#07-outer-joins)
08. [A Short Note on NULLs](#08-a-short-note-on-nulls)
09. [Queries With Expressions](#09-queries-with-expressions)
10. [Queries With Aggregates (Pt. 1)](#10-queries-with-aggregates-pt-1)
11. [Queries With Aggregates (Pt. 2)](#11-queries-with-aggregates-pt-2)
12. [Order of Execution of a Query](#12-order-of-execution-of-a-query)
13. [Inserting Rows](#13-inserting-rows)
14. [Updating Rows](#14-updating-rows)
15. [Deleting Rows](#15-deleting-rows)
16. [Creating Tables](#16-creating-tables)
17. [Altering Tables](#17-altering-tables)
18. [Dropping Tables](#18-dropping-tables)


## 00. SQL intro

Everything generate data, in the era of AI, data becomes the most valuable asset in the world.
SQL (Structured Query Language) is a language that allows to query, manipulate and transform data from a relational database. Therefore it is the language through which we can talk to data.
The most popular SQL data bases are SQLite, MySQL, Postgres, Oracle and Microsoft SQL Server. They all support the common SQL language standard.

A relational database represent a collection of related 2D tables (similar to Excel spreadsheet) with a finite number of named columns (attributes or properties of the table) and any number of rows data. 

For example, if the Department of Motor Vehicles had a database, you might find a table containing all the known vehicles that people in the state are driving. This table might need to store the model name, type, number of wheels, and number of doors of each vehicle for example.

Table: Vehicules
| ID | Model             | # Wheels |  # Doors |  Type      |
|  1 | Ford Focus        |  4       |   4      | Sedan      |
|  2 | Tesla Roadster    |  4       |   2      | Sports     |
|  3 | Kawakasi Ninja    |  2       |   0      | Motorcycle |
|  4 | McLaren Formula 1 |  4       |   0      | Race       |
|  5 | Tesla S           |  4       |   4      | Sedan      |


In such a database, you might find additional related tables containing information such as a list of all registered drivers in the state, the types of driving licenses that can be granted, or even driving violations for each driver.
By learning SQL, the goal is to learn how to answer specific questions about this data, like "What types of vehicles are on the road have less than four wheels?", or "How many models of cars does Tesla produce?", to help us make better decisions down the road.
