
# SQL

*SQL*, which stands for Structured Query Language, is a language for interacting with data stored in something called a relational database.

Relational database are a collection of tables. A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or record, of a table contains information about a single entity. For example, in a table representing employees, each row represents a single person. Each column, or field, of a table contains a single attribute for all rows in the table.

**SELECTing single columns**

A query is a request for data from a database table (or combination of tables). 

In SQL, we can select data from a table using a SELECT statement. For example, the following query selects the name column from the people table:

SELECT name
FROM people;

In this query, SELECT and FROM are called keywords. In SQL, keywords are not case-sensitive, which means we can write the same query as:

select name
from people;

It's good practice to make SQL keywords uppercase to distinguish them from other parts of your query, like column and table names.

It's also good practice to include a semicolon at the end of your query. This tells SQL where the end of your query is!
