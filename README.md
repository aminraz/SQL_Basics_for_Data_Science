
# Table of Contents

1.  [WEEK #1](#org297a915)
    1.  [keywords](#org64c2bb4)
    2.  [installation](#org99c045f)
    3.  [commands](#org39d4c8b)
        1.  [select](#org47c7f57)
        2.  [create table](#orga2d5e68)
        3.  [insert into table](#org3053e9e)
        4.  [create temporary table](#org7be8b18)
        5.  [adding comments by &#x2013; and *\*\**](#orga5965e8)
    4.  [articles](#orgc365f6e)
2.  [WEEK #2](#orgc9c8b73)
    1.  [Introduction](#orgbb28a90)
        1.  [Clauses and operators](#org83749e9)
        2.  [Wildcards](#orgcc3ae54)
        3.  [Math operators](#org5a0255e)
    2.  [Basics of Filtering with SQL](#org5b95ff7)
        1.  [where clause operator](#org56c2b98)
        2.  [BETWEEN AND](#orgd74b268)
    3.  [Advanced Filtering: IN, OR, and NOT](#org290ea22)
        1.  [IN](#org1d3e64a)
        2.  [OR](#org4a21fe3)
        3.  [IN or OR](#org04e3a76)
        4.  [OR  AND](#orgd81155c)
    4.  [Using Wildcards in SQL](#org3682de1)
        1.  [LIKE operator(predicate)](#org08b6deb)
    5.  [ORDER BY](#org92976a4)
    6.  [Math Operations](#org1f1c7d6)
    7.  [Aggregate Functions](#org5fefc0f)
        1.  [DISTINCT](#orgfc6d5bd)
    8.  [Grouping Data with SQL](#org30118fd)
        1.  [GROUP BY](#org204417b)
        2.  [HAVING](#orgd83d176)
3.  [Sample Database](#orgc9bdf26)
    1.  [see columns in a sample table](#orgbf016ad)
4.  [GENERAL COMMANDS](#org197a66e)

This org file includes notes and summary of the course [SQL for Data
Science](https://www.coursera.org/learn/sql-for-data-science) from University of California, Davis available in Coursera
as well as additional information that I find useful to learn but it's
missing in the course. You can use it as a supplementary material if
you're taking the course or as an standalone summary of basics of SQL
for data science.

This document is divided into different headings that you jump into
through these links: [1](#org297a915) [2](#orgc9c8b73)


<a id="org297a915"></a>

# WEEK #1


<a id="org64c2bb4"></a>

## keywords

-   data modeling
-   NoSQL
-   primary keys, foreign keys
-   ER diagrams: Chen notation, Crow's foot notation, UML class diagram notation


<a id="org99c045f"></a>

## installation

-   for Linux: install sqlite3 from terminal


<a id="org39d4c8b"></a>

## commands


<a id="org47c7f57"></a>

### select

simple select query

    select col1, col2, col3 from my_table limit number_of_lines;

limit the number of rows

    select col1, col2, col3 from my_table where col4 = 'value';

sum of a column

    select sum(col1) from my_table;


<a id="orga2d5e68"></a>

### create table

    create table my_table
           (col1 char(20) null,
           col2 char(20) not null,
           col3 char(20) primary key);


<a id="org3053e9e"></a>

### insert into table

    	/* It's a good practice to first
    	identify columns that the values
    	 are going to get there */
    insert into my_table
           (col1, col2, )
           values
           (value1, value2,);		


<a id="org7be8b18"></a>

### create temporary table

    	-- create a subset from a table
    create temporary table my_tmp_table as
           (
           select *
           from my_table
           where col1 = 'value')


<a id="orga5965e8"></a>

### adding comments by &#x2013; and *\*\**


<a id="orgc365f6e"></a>

## articles

-   [AWS and SQL](https://aws.amazon.com/what-is/sql/)
-   [Sqlite toturials](https://www.w3resource.com/sqlite/index.php)
-   [SQL vs. NoSQL – Know the Difference](https://dataconomy.com/2014/07/01/sql-vs-nosql-need-know/)
-   [NoSQL keeps rising, but relational databases still dominate big data](https://www.techrepublic.com/article/nosql-keeps-rising-but-relational-databases-still-dominate-big-data/)
-   


<a id="orgc9c8b73"></a>

# WEEK #2

Filtering sorting and calculating data with SQL


<a id="orgbb28a90"></a>

## Introduction


<a id="org83749e9"></a>

### Clauses and operators

-   WHERE
-   BETWEEN AND
-   IN
-   OR
-   NOT
-   LIKE
-   ORDER BY
-   GROUP BY


<a id="orgcc3ae54"></a>

### Wildcards


<a id="org5a0255e"></a>

### Math operators

-   AVERAGE
-   COUNT
-   MAX
-   MIN


<a id="org5b95ff7"></a>

## Basics of Filtering with SQL


<a id="org56c2b98"></a>

### where clause operator

    SELECT col1, col2 FROM my_table
           WHERE col operator value;

operator can be

-   =
-   <> (not equal !=)
-   <
-   >
-   >=
-   <=
-   BETWEEN AND
-   IS NULL


<a id="orgd74b268"></a>

### BETWEEN AND

    select city from customers where customerid between 4 and 10;	


<a id="org290ea22"></a>

## Advanced Filtering: IN, OR, and NOT


<a id="org1d3e64a"></a>

### IN

-   use parentheses for more than one condition with comma between them
    
        select country from customers where city in ('Paris', 'Rome', 'Oslo');


<a id="org4a21fe3"></a>

### OR

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">WHERE</th>
<th scope="col" class="org-left">X</th>
<th scope="col" class="org-left">or</th>
<th scope="col" class="org-left">Y</th>
<th scope="col" class="org-left">output</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">&#xa0;</td>
<td class="org-left">true</td>
<td class="org-left">or</td>
<td class="org-left">false</td>
<td class="org-left">X</td>
</tr>


<tr>
<td class="org-left">&#xa0;</td>
<td class="org-left">true</td>
<td class="org-left">or</td>
<td class="org-left">true</td>
<td class="org-left">X</td>
</tr>


<tr>
<td class="org-left">&#xa0;</td>
<td class="org-left">false</td>
<td class="org-left">or</td>
<td class="org-left">false</td>
<td class="org-left">nil</td>
</tr>


<tr>
<td class="org-left">&#xa0;</td>
<td class="org-left">false</td>
<td class="org-left">or</td>
<td class="org-left">true</td>
<td class="org-left">Y</td>
</tr>
</tbody>
</table>


<a id="org04e3a76"></a>

### IN or OR

-   IN is faster
-   OR: order is important
-   IN: order is not important
-   IN: making sub-queries


<a id="orgd81155c"></a>

### OR  AND

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">WHERE</th>
<th scope="col" class="org-left">X</th>
<th scope="col" class="org-left">OR</th>
<th scope="col" class="org-left">Y</th>
<th scope="col" class="org-left">AND</th>
<th scope="col" class="org-left">Z</th>
<th scope="col" class="org-left">output</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">&#xa0;</td>
<td class="org-left">T</td>
<td class="org-left">&#xa0;</td>
<td class="org-left">F</td>
<td class="org-left">&#xa0;</td>
<td class="org-left">F</td>
<td class="org-left">X</td>
</tr>
</tbody>
</table>

OR is executed before AND. By using parentheses we can force to check
AND condition:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">WHERE</th>
<th scope="col" class="org-left">(X</th>
<th scope="col" class="org-left">OR</th>
<th scope="col" class="org-left">Y)</th>
<th scope="col" class="org-left">AND</th>
<th scope="col" class="org-left">Z</th>
<th scope="col" class="org-left">output</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">&#xa0;</td>
<td class="org-left">T</td>
<td class="org-left">&#xa0;</td>
<td class="org-left">F</td>
<td class="org-left">&#xa0;</td>
<td class="org-left">F</td>
<td class="org-left">nil</td>
</tr>
</tbody>
</table>


<a id="org3682de1"></a>

## Using Wildcards in SQL


<a id="org08b6deb"></a>

### LIKE operator(predicate)

Used for only string data not numerical data. 

-   %: '%string', 'st%g', 'st%'
    it does not match NULL value
-   \_: is not supported in DB2 but most other system support it.
    
        WHERE val LIKE '_string'
-   []: not supported in SQLite
-   Wildcards are slower than filtering operators


<a id="org92976a4"></a>

## ORDER BY

-   It should be the last clause in an statement
-   Different columns can be used for sorting
-   Column position can be used
    
        ORDER BY 1,5
-   DESC: descending
-   ASC: ascending
-   DESC and ASC should be repeated for each column


<a id="org1f1c7d6"></a>

## Math Operations

Creating new column in the output from math operations on other
columns:

    SELECT col1,col2, col1*col2 AS new_col
           FROM my_table;

new<sub>col</sub> is as alias for the new column 


<a id="org5fefc0f"></a>

## Aggregate Functions

-   AVG()
-   COUNT()
-   MIN()
-   MAX()
-   SUM()

    SELECT AVG(col1) AS col1_avg FROM my_table;
           -- null rows are ignored 

    SELECT count(*) AS total_rows FROM my_table;
           -- it counts null rows
           -- if you count a specific column, it ignores null rows

AS is not mandatory.


<a id="orgfc6d5bd"></a>

### DISTINCT

It recognizes duplicates in a column

    SELECT count(DISTINCT col1)
           FROM my_table


<a id="org30118fd"></a>

## Grouping Data with SQL


<a id="org204417b"></a>

### GROUP BY

In the following example we are counting the number of cities each
country has in our table customers:

    select country, count(city) from customers group by country ;	


<a id="orgd83d176"></a>

### HAVING

It filters the result of group by like where. In the following
example, the result is filtered to those countries with customers
having a special email patter: 

    select country, count(city) from customers group by country having  email like '%com';	

We can use multiple columns for group by. If there are more columns
in the group by, these groups need to be in the select part
too. NULL is categorized separately.

WHERE is used before grouping and HAVING is used after it. 


<a id="orgc9bdf26"></a>

# Sample Database

Download the sample database called chinook from this [link](https://www.sqlitetutorial.net/sqlite-sample-database/).


<a id="orgbf016ad"></a>

## see columns in a sample table

    select * from genres; 


<a id="org197a66e"></a>

# GENERAL COMMANDS

-   open the database
    
        .open chinook.db
-   inspect the tables
    
        .tables
-   .help: show help for dot commands
-   .database: show the connected databases in the session
-   attach a database
    
        attach database "address.db" as db_name;
-   .exit: exit the sqlite
-   showing the structure of a table
    
        .schema tab_name
-   .indexes: show the indexes of the current database or table
-   write query result into a file
    
        .output filename
        	select * from tab_name;

