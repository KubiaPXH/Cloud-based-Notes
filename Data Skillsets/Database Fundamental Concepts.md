# Database Fundamental Concepts
## What is a Database (DB)? 
- Database (DB): Any collection of **related** information
	- **related** means that the information here needs to have the same properties (or attributes) in the case of relational database.
- Two type of DB:
	- Relational DB (SQL DB): Organize data into one or more tables
		- Each table (a group) have rows (entities in the group) and columns (attributes of each entities)
		- For each row (entity), there is a **unique key identifies** to distinguish one entity to another. 
	- Non-Relational DB (noSQL, not just SQL): Organize data is anything but a 2D table
		- e.g.: key value stores, documents (JSON?, XML?...), Graphs, Flexible Tables?
## Database Management Systems (DBMS): 
- DBMS: a software program used to manage a DB (CRUD, Design, Security, Backup, Import/Export data, concurrency - multiple parallel computations, interacts with external apps).
- Diagram of the interactions btw app <-> data:
	- ![[Pasted image 20211218102513.png|500]]
- Relational Database Management Systems (RDBMS): a DBMS for relational DB (e.g. mySQL, Oracle, mariaDB...)
## Structured Query Language (SQL)
> SQL is a standardized (even slightly diff depend on diff RDBMS) language for interacting with RDBMS. Saying it the other way, **we command RDBMS (to manage, in a large sense, DB) using SQL language.**
- SQL is a hybrid language, 4 type of language in one:
	- Data Definition Language (DDL): defining DB schemas
	- Data Manipulation Language (DML): inserting, updating, deleting data from DB
	- Data Control Language (DCL): controlling access to DB, user & permissions management
	- Data Query Language (DQL): query the data for information
- Database Queries: 
	- Prob: As the DB structure become more and more complex -> more difficult to get the info we want
	- Solution: **DB Queries which are requests made to DBMS to get a specific info from DB** (e.g. google search is a query)