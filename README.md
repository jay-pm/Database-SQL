
## SQL

    1. Selecting columns
    2. Filtering rows
    3. Aggregate functions
    4. Sorting and grouping

*SQL*, which stands for Structured Query Language, is a language for interacting with data stored in something called a relational database.

Relational database are a collection of tables.  
A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or record, of a table contains information about a single entity.  
For example, in a table representing employees, each row represents a single person. Each column, or field, of a table contains a single attribute for all rows in the table.

A query is a request for data from a database table (or combination of tables). 

### 1. Selecting columns

**SELECTing single columns**

In SQL, we can select data from a table using a SELECT statement. For example, the following query selects the name column from the people table:

    SELECT name
    FROM people;

In this query, SELECT and FROM are called keywords. In SQL, keywords are not case-sensitive, which means we can write the same query as:

    select name
    from people;*

It's good practice to make SQL keywords uppercase to distinguish them from other parts of your query, like column and table names.  
It's also good practice to include a semicolon at the end of your query. This tells SQL where the end of your query is!

**SELECTing multiple columns**

In the real world, we often want to select multiple columns. Luckily, SQL makes this really easy. To select multiple columns from a table, simply separate the column names with commas!

    SELECT name, birthdate
    FROM people;
 
**SELECTing all columns**

    SELECT *
    FROM people;
    
**Limiting query result**

If we only want to return a certain number of results, we can use the LIMIT keyword to limit the number of rows returned:

    SELECT *
    FROM people
    LIMIT 10;
    
**SELECTing DISTINCT values**

    SELECT DISTINCT language
    FROM films;

**COUNTing number of rows**

If you want to count the number of employees in your employees table, the COUNT statement lets us do this by returning the number of rows in one or more columns.  
For example, this code gives the number of rows in the people table:

    SELECT COUNT(*)
    FROM people;
 
 Below query gives count of non missing values in a single column.
 
    SELECT COUNT(birthdate)
    FROM people;
    
It's also common to combine COUNT with DISTINCT to count the number of distinct values in a column.
For example, this query counts the number of distinct birth dates contained in the people table:

    SELECT COUNT(DISTINCT birthdate)
    FROM people;

###  2. Filtering

In SQL, the **WHERE** keyword allows us to filter based on both text and numeric values in a table.  
Note: WHERE clause always comes after the FROM statement.
    
The following code returns all films with the title 'Metropolis':

    SELECT title
    FROM films
    WHERE title = 'Metropolis';

We can combine WHERE multiple conditions using **AND** or **OR** operator.  
We need to specify the column name separately for every AND and OR condition, so "WHERE release_year > 2000 AND < 2010 would be invalid.  
Below query displays all details for Spanish language films released after 2000, but before 2010.

    select *
    from films
    where language = 'Spanish'
    and release_year > 2000
    and release_year < 2010

Below is OR query.

    SELECT title
    FROM films
    WHERE release_year = 1994
    OR release_year = 2000;

Below query is a combination of AND and OR and will get the title and release year of films released in the 90s which were in French or Spanish and which took in more than $2M gross.

    SELECT title, release_year
    FROM films
    WHERE (release_year >= 1990 AND release_year < 2000)
    AND (language = 'French' OR language = 'Spanish')
    AND gross > 2000000

In SQL the **BETWEEN** keyword provides a useful shorthand for filtering values within a specified range.  
BETWEEN is inclusive, meaning the beginning and end values are included in the results!

    SELECT title
    FROM films
    WHERE release_year
    BETWEEN 1994 AND 2000;
    
One more example with AND, OR, BETWEEN:

    SELECT title, release_year
    FROM films
    WHERE release_year BETWEEN 1990 AND 2000
    AND budget > 100000000
    AND (language = 'Spanish' OR language = 'French')

**WHERE IN*

**LIKE, NOT LIKE**
