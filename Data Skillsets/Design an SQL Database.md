# Design an SQL Database
```ad-important
**QUESTION**: How to design a database based having database requirements?

**ANSWER:** Database requirements -> Entity Relationship (ER) diagram -> Database schema (But this is a not linear procedure but have comebacks and feedbacks!!)
```
```ad-tip
**Basic Rule**: When there is one thing in the "real world" there should be one copy of that in the database => **Don't put the same (string) data in twice - use a relationship instead.** 
```
## Entity Relationship Diagrams:
- Entity Relationship Diagrams: describes interrelated things of interest (entities) in a specific domain => ER diagram is composed of **entities** and **relationships exist between entities**. Here, ER diagrams is used to model database.
- Components of a ER diagram:
	- Example and notation (attention on how to notation components):
		- ![[Student_ERDiagram.png]]
		- **Entity**: Object we want to model & store information abt (in a table)
			- *Attribute* (known)
			- *Primary key* (known)
			- *Composite attribute*: an attribute that can be broken up into sub-attributes (only need to define sub-attributes but no need to create composite attribute)
			- *Multi-valued attribute*: an attribute that can have > 1 value (e.g. club - a student can join more than 1 club)
			- *Derived attribute*: an attribute that can be derived from the other attribute (e.g. has_honors). we don't need to keep track (official create) an derived attribute in DB schema since we can derive it every time from other attributes.
		- **Relationship**: defines relationship btw two entities
			- *Partial participation* (single line): not all members of the entity need to participate in the relationship (e.g. a student can take classes but it's also ok if he doesn't take any class)
			- *Total participation* (double line): all members of the entity must participate in the relationship (e.g. all class need to be taken by at least one student)
			- *Relationship attribute* (known)
			- *Relationship cardinality*: the number of instances (members) of an entity from a relation that can be associated with the relation, common cases are 1:1, 1:N, N:1, N:M (e.g. N:M cardinality relationship: a student can take M, any number, of classes and a class can be taken by N, any number, of student).
		- **Weak Entity**: an entity that cannot be uniquely identified by its attributes alone -> it will depend on another entity(s) (e.g. a exam depends on a class and only can exist in a context of a class)
			- *Identifying relationship*: a relationship that serves to uniquely identify the weak entity => the weak entity always need to have a total participation in the identifying relationship.
## Database schemas:
- [Database Schema](https://database.guide/what-is-a-database-schema/): is the organization and structure of a database, we can consider a **DB schema is a blueprint of the database** without needed to have any data in it.
	- More concrete, DB Schema show us all the components and their properties of a database: tables (attributes <- data types in tables), relationships between tables, views and stored procedures...
	- DB schema can be, and should be, represented by a visual diagrams as below:
		- e.g. ![[Pasted image 20211223143108.png|400]]
- Reading a DB schema: Knowing how to read a DB schema = Knowing how the DB is organized and structured.
## Stage 1: From Database Requirements to ER diagram
- [Tutorial](https://www.mikedane.com/databases/sql/designing-an-er-diagram/)
- Free tool for ER Diagram and DB Schema: [ERDplus](https://erdplus.com/documents)
## Stage 2: From ER Diagram to DB Schema
- Basic process and example with [tutorial](https://www.mikedane.com/databases/sql/er-diagram-mapping/):
	- Input as ER Diagrams:
		- ![[Pasted image 20211225115143.png|700]]
	- Step 1: **Mapping of Regular Entity Types** -> for each *regular entity* type create a table that includes *all the simple attributes* of that entity.
	- Step 2: **Mapping of Weak Entity Types** -> for each *weak entity* type create a table includes *all simple attributes* of the weak entity
		- The primary key of the new table (weak entity) should be: the partial key of the weak entity + the primary key of its owner.
		- #question: how to deal with 1:N constraint? 
	- Step 3: **Mapping of Binary 1:1 Relationships Types**  -> include one side of the relationship as a foreign key in the other and favor total participation not partial participation (meaning that foreign key is added in the entity which totally participation, but not partial participation, in the relationship). Other cases -> free to choose the side.
	- Step 4: **Mapping of Binary 1:N Relationships Types** -> include the 1 side's primary key as a foreign key on the N side relation (table)
	- Step 5: **Mapping of Binary M:N Relationships Types** -> create new relation (table), for the relationship, who's primary key is a combination of both entities' primary key's, then include any relationship attributes.
		- #question: for this example, how we can respect the constraint the branch's employees only work on clients handled by their branch but not clients handled by other branches?
	- Output as DB Schema: 
		- ![[Pasted image 20211225123308.png|700]]
- This process using [[SQL Basics#Working with DB|SQL's manipulating database commands]] and [[SQL Basics#Working with Table|SQL's manipulating table commands]]
```ad-resources
For [more details](https://course.ccs.neu.edu/cs3200sp18s3/ssl/lectures/lecture_08_mapping.pdf) and [further more details](http://jcsites.juniata.edu/faculty/rhodes/dbms/ermapping.htm) to mapping the ER Model to DB Schema
```