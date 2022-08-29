- **Category:** note
- **Title:** SQL Basics 
- **Created date:**
- **Updated date:** 22/05/2022
- **Tag:** [[Data Analyst]] [[Relational Database]]
- **Main refs:**
---
## Tasks
- [Window Function Questions](https://www.windowfunctions.com/)
- Practice page: https://www.w3resource.com/sql-exercises/
	- [ ] Join and Subqueries
		- [ ] Soccer DB (Stop at SUBQUERIES 8)
- [ ] [SQL LeetCode problems](https://github.com/shawlu95/Beyond-LeetCode-SQL)
---
```ad-resources
- [Advanced SQL](https://mode.com/sql-tutorial/intro-to-advanced-sql/) in Mode
```
## [[Database Fundamental Concepts]]
## [[Design an SQL Database]]
## SQL Basics
### Special attributes (column) of RDB table
- *Primary key*: the **unique identifying key for each entity** in the table
	- Normal primary key: 
		- ![[Pasted image 20211218105041.png|300]] 
		- **student_id is the primary key** which help to distinguish 2 diff student have the same name (Jack) and major.
	-  Composite primary key: the primary key is a composite of 2 or more attributes
		- ![[Pasted image 20211219101537.png|300]]
		- 2 foreign keys **branch_id** and **supplier_name** make the primary key for the Branch Supplier table
- *Foreign key*: an attributes that **store a primary key of a row** (in another or the same DB table)
	- e.g.: ![[Pasted image 20211219101109.png]]
		- **branch_id** is a foreign key pointing to the primary key of Branch table 
			- ![[Pasted image 20211219101153.png|300]]
		- **super_id** is another foreign key pointing to the primary key of the same table (Employee)
### Basics data types in SQL
```ad-resources
[SQL datatypes - w3schools](https://www.w3schools.com/sql/sql_datatypes.asp)
```
#### Numeric data types 
- *BOOLEAN or BOOL*: 0 = FALSE, non-0 = TRUE.
- *INTEGER(size) or INT(size)*: a medium integer => *BIGINT(size)*: a large integer; *TINYINT(size)*; *SMALLINT(size)*
- *DECIMAL(size,d) or DEC(size,d)*: an exact fixed-point number[^1] (size = total number of digits and d =number of digits after the decimal point)
- *DOUBLE(size,d)*: a normal-size floating point number[^2] (size = total number of digits and d =number of digits after the decimal point)
#### Date and Time data types
- *DATE*: a date (format: YYYY-MM-DD)
- *YEAR*: a year in four-digit format.
- *TIMESTAMP(fsp[^3])*: a timestamp (format: YYYY-MM-DD hh:mm:ss)
	- using *DEFAULT CURRENT_TIMESTAMP*: Automatic initialization the current date and time
	- using *ON UPDATE CURRENT_TIMESTAMP*: Automatic updating to the current date and time
#### String data types
- *VARCHAR(size)*: A **variable length** string (size = max number of characters in string)
- *BLOB(size)*: for **B**inary **L**arge **OB**jects, a collection of binary data stored as a single entity (e.g. images, audio or other multimedia objects...)
### Basic Commands in SQL
#### Working with DB
- Create DB: [CREATE DATABASE](https://www.w3schools.com/sql/sql_create_db.asp)
- Use DB: [USE DATABASE](https://beginner-sql-tutorial.com/sql-use-database.htm)
- Delete DB: [DROP DATABASE](https://www.w3schools.com/sql/sql_drop_db.asp)
- Backup DB: [BACKUP DATABASE](https://www.w3schools.com/sql/sql_backup_db.asp)
#### Working with Table
- **Working with table structure (attributes):**
	- Create Table: [CREATE TABLE](https://www.w3schools.com/sql/sql_create_table.asp) (including new creation and creation using another table's data)
	- Modify Table (attributes and their constraints): [ALTER TABLE](https://www.w3schools.com/sql/sql_alter.asp) can perform ADD COLUMN, DROP COLUMN and ALTER COLUMN
	- Delete Table: [DROP TABLE](https://www.w3schools.com/sql/sql_drop_table.asp)
	- Using [Constraints](https://www.w3schools.com/sql/sql_constraints.asp) (with CREATE TABLE and ALTER TABLE): 
		- Contraints used to specify rules for data in table. Constraints can be column level or table level.
		- Commonly used constraints:
			- [NOT NULL](https://www.w3schools.com/sql/sql_notnull.asp) - Ensures that a column cannot have a NULL value
			- [UNIQUE](https://www.w3schools.com/sql/sql_unique.asp) - Ensures that all values in a column are different
			- [PRIMARY KEY](https://www.w3schools.com/sql/sql_primarykey.asp) - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
			- [FOREIGN KEY](https://www.w3schools.com/sql/sql_foreignkey.asp) - Prevents actions that would destroy links between tables
				- [ON DELETE SET NULL](https://askinglot.com/what-is-the-difference-between-on-delete-set-null-and-on-delete-cascade): having this constraint, if the row in the source table linked to foreign key value is deleted, the value of that foreign key is set to NULL.
				- [ON DELETE SET CASCADE](https://askinglot.com/what-is-the-difference-between-on-delete-set-null-and-on-delete-cascade): having this constraint, if the row in the source table linked to foreign key value is deleted, the rows contain that foreign value in the current table will also be deleted.
			- [CHECK](https://www.w3schools.com/sql/sql_check.asp) - Ensures that the values in a column satisfies a specific condition
			- [DEFAULT](https://www.w3schools.com/sql/sql_default.asp) - Sets a default value for a column if no value is specified
			- [CREATE INDEX](https://www.w3schools.com/sql/sql_create_index.asp) - Used to create and retrieve data from the database very quickly
- **Working with data in table:**
	- Add new records (entities or rows) to a table: 
		- Basics syntax: [INSERT INTO](https://www.w3schools.com/sql/sql_insert.asp)
		- Add new records to a table using other tables' data: [INSERT INTO SELECT](https://www.w3schools.com/sql/sql_insert_into_select.asp)
	- Update old records in a table: [UPDATE](https://www.w3schools.com/sql/sql_update.asp)
	- Delete records in a table: [DELETE](https://www.w3schools.com/sql/sql_delete.asp)
#### Query 
##### Select/Query from a DB
```ad-definition
[SELECT](https://www.w3schools.com/sql/sql_select.asp) statement is used to select data from a database, the data returned is stored in a result table, called the result-set.
```
- **Syntax diagram of SELECT statement**
	- ![[Pasted image 20220104112120.png|600]]
- [SELECT DISTINCT](https://www.w3schools.com/sql/sql_distinct.asp) is used to return only distinct (different) values
- [SELECT TOP](https://www.w3schools.com/sql/sql_top.asp) is used to specify the number of records to return.
- [SELECT INTO](https://www.w3schools.com/sql/sql_select_into.asp) statement copies data from one table into a new table
- [Nesting SELECT in FROM](https://stackoverflow.com/questions/4629979/nested-select-statement-in-sql-server) using Alias
- **Clauses (mệnh đề) used with SELECT**
	- [WHERE](https://www.w3schools.com/sql/sql_where.asp) clause is used for filter record.
		- WHERE condition can be built using [SQL OPERATORS](https://www.w3schools.com/sql/sql_operators.asp)
			- Special Case: `> ALL (inner query)` means the greater than the biggest value in the inner query
		- [LIKE](https://www.w3schools.com/sql/sql_like.asp) operator is used in a WHERE clause to search for a specific pattern in a column 
			- Two [wildcards](https://www.w3schools.com/sql/sql_wildcards.asp) often used with LIKE:
				- The percent sign (%) represents zero, one or multiples characters (e.g. "%a" can be any value end with "a")
				- The underscore sign (_) represents a single character.
				- [ESCAPE](https://media.datadirect.com/download/docs/openaccess/alloa/index.html#page/sqlref/escape-clause-in-like-operator.html) clause to indicate escape character. A escape character will indicate that any wildcard character after it will be treated as a regular character.
			- We can use NOT LIKE to exclude data with a specific pattern too.
		- [IN](https://www.w3schools.com/sql/sql_in.asp) operator allow to specify multiple values in WHERE clause (can also use another SELECT in IN)
			- We can use [IN for two and more variables at the same time](https://docs.oracle.com/cd/B19306_01/server.102/b14200/conditions013.htm) -> just need parenthesis surrounding these variables.
				- Syntax: WHERE (column_name1, column_name2) IN (SELECT...);
		- [BETWEEN](https://www.w3schools.com/sql/sql_between.asp) operator selects values with in a given range, value can be numbers, text, or dates.
		- [UNION](https://www.w3schools.com/sql/sql_union.asp) operator is used to combine the result-set of two or more SELECT statements (*vertical*)
		- [EXISTS](https://www.w3schools.com/sql/sql_exists.asp) operator is used to test for the existence of any record in a subquery => returns TRUE if the subquery returns one or more records.
	- [ORDER BY](https://www.w3schools.com/sql/sql_orderby.asp) clause is used to sort the result-set in ascending or descending order.
	- Aggregate Functions such as:
		- [MIN() and MAX()](https://www.w3schools.com/sql/sql_min_max.asp) functions return the min and max value of the selected column (used as input)
		- [COUNT(), AVG() and SUM()](https://www.w3schools.com/sql/sql_count_avg_sum.asp) function a correspondent value of a selected value (used as input)
		- [HAVING](https://www.w3schools.com/sql/sql_having.asp) clause has the same filter function as WHERE clause but used exclusively with aggregate functions (WHERE clause cannot be used with aggregate functions)
		- [GROUP BY](https://www.w3schools.com/sql/sql_groupby.asp) statement groups row that have the same (column) value into summary row (e.g. GROUP BY country -> group row by the same country). GROUP BY is often used with aggregates functions MIN(), MAX(), COUNT(), SUM(), AVG().
	- [JOIN](https://www.w3schools.com/sql/sql_join.asp) clause is used to combine rows from two or more table (*horizontal*), based on a related column between them.
		- JOIN or [(INNER) JOIN](https://www.w3schools.com/sql/sql_join_inner.asp): Returns records that have matching values in both tables
		- [LEFT (OUTER) JOIN](https://www.w3schools.com/sql/sql_join_left.asp): Returns all records from the left table, and the matched records from the right table
		- [RIGHT (OUTER) JOIN](https://www.w3schools.com/sql/sql_join_right.asp): Returns all records from the right table, and the matched records from the left table
		- [FULL (OUTER) JOIN](https://www.w3schools.com/sql/sql_join_full.asp): Returns all records when there is a match in either left or right table
		- Differences between [ON and USING](https://stackoverflow.com/questions/11366006/mysql-join-on-vs-using) in JOIN clause
		- ![[Pasted image 20211219174009.png]]
	- [CASE](https://www.w3schools.com/sql/sql_case.asp) an if-then-else statement
	- [NULL values](https://www.w3schools.com/sql/sql_null_values.asp)
		- IS NULL
		- IS NOT NULL
	- [NULL functions](https://www.w3schools.com/sql/sql_isnull.asp):
		- IFNULL()
		- ISNULL()
##### Subquery in SQL
```ad-definition
[Subquery](https://www.w3resource.com/sql/subqueries/understanding-sql-subqueries.php) is a SQL query nested inside a larger query
```
##### Working with String in SQL
```ad-resources
[SQL string functions for cleaning](https://mode.com/sql-tutorial/sql-string-functions-for-cleaning/)
```
- [CONCAT()](https://www.w3schools.com/sql/func_mysql_concat.asp): Add several strings together.
	- [|| operator](https://www.sqlines.com/oracle-to-sql-server/string_concat) as alternative to CONCAT() function
- [REPLACE()](https://www.w3schools.com/sql/func_mysql_replace.asp): Replace (case-sensitive) all occurrences of a substring within a string with a new substring.
##### [[Window Functions in SQL]]
#### Misc.
- **Better syntax**:
	- using *table_name.attribute_name* instead of only *attribute_name* to distinguish between table and know where is the attribute belong to (help memory)
	- NEW.attribute_name = get the value of <attribute_name> attribute in the latest added row or entity
- [Indexes](https://www.tutorialspoint.com/sql/sql-indexes.htm) are special lookup tables that database search engine can use to find rows with specific column values quickly, but it will slows down data input (more detail [why we use Indexes](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html))
		- CREATE INDEX (or CREATE UNIQUE INDEX)
		- DROP INDEX
- [Comments](https://www.w3schools.com/sql/sql_comments.asp):
	- Single lines comment: `--`
	- Multi-line comments start with `/*` and end with `*/`
- **Aliases**: give a table, or a column in a table, a temporary (in the duration of the query) readable name using [AS](https://www.w3schools.com/sql/sql_alias.asp) keyword 
- [Wildcard](https://www.w3schools.com/sql/sql_wildcards.asp) character (e.g. % or _ or \[]...) used to substitute one or more characters in a string, often use with LIKE operators in WHERE clause.
- [Stored Procedure](https://www.w3schools.com/sql/sql_stored_procedures.asp): use procedure to reuse save code in SQL, need to execute using EXEC commands (different from function)
	- CREATE PROCEDURE
	- EXEC
	- ALTER PROCEDURE
	- DROP PROCEDURE
- [Triggers](https://www.geeksforgeeks.org/sql-trigger-student-database/): is a stored procedure in DB which automatically invokes whenever a special event (that we define) in the DB occurs
	- For Triggers which operates more than 1 code lines we need to [use DELIMITER](https://www.w3resource.com/mysql/mysql-triggers.php). DELIMITER have to be executed in the SQL command line or MySQL workbench (not in code editor).
	- In Triggers, we use [IF..THEN..ELSEIF..THEN..ELSE..END IF;](https://stackoverflow.com/questions/27647420/if-statement-inside-trigger-clause)
- [Stored Function](https://www.mysqltutorial.org/mysql-stored-function/): a **reusable** special kind of program that **returns a single value**, can **be used in SQL statements wherever an expression is used** (no need EXEC like stored procedure)
	- CREATE FUNCTION
	- ALTER FUNCTION
	- DROP FUNCTION

[^1]: A fixed point number has **a specific number** of bits (or digits) reserved for the integer part (left of demical point) and **a specific number** of bits reserved for the fractional part (right of decimal point). No matter how big or small the number (of this data type), the computer always use the same number of bits for each portion. (e.g. the format `IIIII.FFFFF` has max number `99999.99999` and min non-zero number `00000.00001`)
[^2]: A floating point number **does not reserve a specific number** of bits for each part of the number. Instead, it reserves a certain number of bits for the number (called the *mantissa*) and a certain number of bits to say *where* within that number the decimal place sits (called the *exponent*). (e.g. a floating point number takes 10 digits with 2 digits reserved for exponent might have max as `9.999999e+50` and min non-zero as `0.0000001e-49` ) 
[^3]: fractional seconds precision
