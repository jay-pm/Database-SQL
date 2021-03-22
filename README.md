
## SQL

### 1. Selecting columns
### 2. Filtering rows
### 3. Aggregate functions
### 4. Sorting and grouping

*SQL*, which stands for Structured Query Language, is a language for interacting with data stored in something called a relational database.

Relational database are a collection of tables.  
A table is just a set of rows and columns, like a spreadsheet, which represents exactly one type of entity. For example, a table might represent employees in a company or purchases made, but not both.

Each row, or record, of a table contains information about a single entity.  
For example, in a table representing employees, each row represents a single person. Each column, or field, of a table contains a single attribute for all rows in the table.

A query is a request for data from a database table (or combination of tables).   
For adding comment in SQL, use --

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

**WHERE IN**  
When number of conditions increases, using where clause might get unwieldy. Here comes IN operator.
Check below example with WHERE and WHERE IN

With WHERE:  

    SELECT name
    FROM kids
    WHERE age = 2
    OR age = 4
    OR age = 6
    OR age = 8
    OR age = 10;
    
With WHERE IN:  
    
    SELECT name
    FROM kids
    WHERE age IN (2, 4, 6, 8, 10);
    
**IS NULL, IS NOT NULL**

In SQL, NULL represents a missing or unknown value. You can check for NULL values using the expression IS NULL. For example, to count the number of missing birth dates in the people table:  

    SELECT COUNT(*)
    FROM people
    WHERE birthdate IS NULL;
    
to find out not NULL values we can use IS NOT NULL.  

    SELECT name
    FROM people
    WHERE birthdate IS NOT NULL;


**LIKE, NOT LIKE**

In SQL, the LIKE operator can be used in a WHERE clause to search for a pattern in a column. To accomplish this, we use something called a wildcard as a placeholder for some other values. There are two wildcards you can use with LIKE:

- The % wildcard will match zero, one, or many characters in text.
- The _ wildcard will match a single character.  
You can also use the *NOT LIKE* operator to find records that don't match the pattern you specify.

Examples:
1. Below will display all names which begin with 'B'. 

        SELECT name
        FROM people
        WHERE name LIKE 'B%'

2. Below will display people whose names have 'r' as the second letter.

        SELECT name
        FROM people
        WHERE name LIKE '_r%'
3. Below will display names of people whose names don't start with A

        SELECT name
        FROM people
        WHERE name NOT LIKE 'A%'    
        
### 3. Aggregate functions:  
Often, we want to perform some calculation on the data in a database. SQL provides a few functions, called aggregate functions.  
Example: AVG, SUM, MIN, MAX  

Below will fetch average duration for films from films table

    SELECT AVG(duration)
    FROM films

Aggregate functions can be combined with the WHERE clause to gain further insights from your data.  
Example:
Get the amount grossed by the best performing film between 2000 and 2012, inclusive.

    SELECT MAX(gross)
    FROM films
    WHERE release_year >= 2000 AND release_year <=2012 
    
In addition to using aggregate functions, we can perform basic arithmetic with symbols like +, -, *, and /.

    SELECT(4+5) -- will result in 9
SQL assumes that if you divide an integer by an integer, you want to get an integer back. So be careful when dividing!  
    
    SELECT(4/3) -- will result in 1

If you want more precision when dividing, you can add decimal places to your numbers. For example,
    
    SELECT(4.0/3.0) //result in 1.333333..

**Aliasing**  
When you have two columns with same name, This will be confusing.  
To avoid situations like this, SQL allows us to do something called aliasing. Aliasing simply means we assign a temporary name to something. To alias, we use the AS keyword.

    SELECT MAX(budget), MAX(duration) -- here two columns will be creeated with name MAX
    FROM films;

in the above example we could use aliases to make the result clearer:

    SELECT MAX(budget) AS max_budget,
    MAX(duration) AS max_duration
    FROM films;
Example: Get the number of decades the films table covers. Alias the result as number_of_decades

    SELECT (MAX(release_year) - MIN(release_year))/10 AS number_of_decades
    FROM films
    
### 4. Sorting and grouping

In SQL, the **ORDER BY** keyword is used to sort results in ascending or descending order according to the values of one or more columns.  
By default ORDER BY will sort in ascending order. If you want to sort the results in descending order, you can use the DESC keyword. For example,

    SELECT title
    FROM films
    ORDER BY release_year DESC;
gives you the titles of films sorted by release year, from newest to oldest.

few more example:  
1. Get the title of films released in 2000 or 2012, in the order they were released.

        SELECT title
        FROM films
        WHERE release_year IN (2000, 2012)
        ORDER BY release_year;
    
2. Get all details for all films except those released in 2015 and order them by duration.

        SELECT *
        FROM films
        WHERE release_year <> 2015
        ORDER BY duration;
    
3. Get the title and gross earnings for movies which begin with the letter 'M' and order the results alphabetically.

        SELECT title, gross
        FROM films
        WHERE title LIKE 'M%'
        ORDER BY title;

*Make sure to always put the ORDER BY clause at the end of your query. You can't sort values that you haven't calculated yet!*

**GROUP BY**

In SQL, GROUP BY allows you to group a result by one or more columns. Commonly, GROUP BY is used with aggregate functions like COUNT() or MAX(). GROUP BY always goes after the FROM clause.

    SELECT sex, count(*)
    FROM employees
    GROUP BY sex;
    
Example: 
Get the release year and average duration of all films, grouped by release year.

    SELECT release_year, AVG(duration), count(*)
    FROM films
    GROUP BY release_year;    
