
# Table of Contents

1.  [WEEK #1](#org8c36237)
    1.  [keywords](#org24d69ba)
    2.  [installation](#orgb741df2)
    3.  [commands](#orgdc2e514)
    4.  [articles](#org96ca956)
2.  [WEEK #2](#org686d6a2)
    1.  [Introduction](#org6dc424d)
    2.  [Basics of Filtering with SQL](#org4672fc5)
    3.  [Advanced Filtering: IN, OR, and NOT](#org6620a36)
    4.  [Using Wildcards in SQL](#orgb7d44c2)
    5.  [ORDER BY](#orgedad785)
    6.  [Math Operations](#orgeb698c5)
    7.  [Aggregate Functions](#orge0a8cd8)
    8.  [Grouping Data with SQL](#orge80e814)
3.  [Sample Database](#org2912447)
    1.  [see columns in a sample table](#org9fbb669)
4.  [GENERAL COMMANDS](#org6863ced)

This file includes notes and summary of the course [SQL for Data
Science](https://www.coursera.org/learn/sql-for-data-science) from University of California, Davis available in Coursera
as well as additional information that I find useful to learn but it's
missing in the course. You can use it as a supplementary material if
you're taking the course or as an standalone summary of basics of SQL
for data science.

You are encouraged to download the README.org and open it inside Emacs
if you're familiar with org mode. It has the same content.


<a id="org8c36237"></a>

# WEEK #1


<a id="org24d69ba"></a>

## keywords

-   data modeling
-   NoSQL
-   primary keys, foreign keys
-   ER diagrams: Chen notation, Crow's foot notation, UML class diagram notation


<a id="orgb741df2"></a>

## installation

-   for Linux: install sqlite3 from terminal


<a id="orgdc2e514"></a>

## commands


### select

simple select query

    select col1, col2, col3 from my_table limit number_of_lines;

limit the number of rows

    select col1, col2, col3 from my_table where col4 = 'value';

sum of a column

    select sum(col1) from my_table;


### create table

    create table my_table
           (col1 char(20) null,
           col2 char(20) not null,
           col3 char(20) primary key);


### insert into table

    	/* It's a good practice to first
    	identify columns that the values
    	 are going to get there */
    insert into my_table
           (col1, col2, )
           values
           (value1, value2,);		


### create temporary table

    	-- create a subset from a table
    create temporary table my_tmp_table as
           (
           select *
           from my_table
           where col1 = 'value')


### adding comments by &#x2013; and *\*\**


<a id="org96ca956"></a>

## articles

-   [AWS and SQL](https://aws.amazon.com/what-is/sql/)
-   [Sqlite toturials](https://www.w3resource.com/sqlite/index.php)
-   [SQL vs. NoSQL – Know the Difference](https://dataconomy.com/2014/07/01/sql-vs-nosql-need-know/)
-   [NoSQL keeps rising, but relational databases still dominate big data](https://www.techrepublic.com/article/nosql-keeps-rising-but-relational-databases-still-dominate-big-data/)
-   


<a id="org686d6a2"></a>

# WEEK #2

Filtering sorting and calculating data with SQL


<a id="org6dc424d"></a>

## Introduction


### Clauses and operators

-   WHERE
-   BETWEEN AND
-   IN
-   OR
-   NOT
-   LIKE
-   ORDER BY
-   GROUP BY


### Wildcards


### Math operators

-   AVERAGE
-   COUNT
-   MAX
-   MIN


<a id="org4672fc5"></a>

## Basics of Filtering with SQL


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


### BETWEEN AND

    select city from customers where customerid between 4 and 10;	


<a id="org6620a36"></a>

## Advanced Filtering: IN, OR, and NOT


### IN

-   use parentheses for more than one condition with comma between them
    
        select country from customers where city in ('Paris', 'Rome', 'Oslo');


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


### IN or OR

-   IN is faster
-   OR: order is important
-   IN: order is not important
-   IN: making sub-queries


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


<a id="orgb7d44c2"></a>

## Using Wildcards in SQL


### LIKE operator(predicate)

Used for only string data not numerical data. 

-   %: '%string', 'st%g', 'st%'
    it does not match NULL value
-   \_: is not supported in DB2 but most other system support it.
    
        WHERE val LIKE '_string'
-   []: not supported in SQLite
-   Wildcards are slower than filtering operators


<a id="orgedad785"></a>

## ORDER BY

-   It should be the last clause in an statement
-   Different columns can be used for sorting
-   Column position can be used
    
        ORDER BY 1,5
-   DESC: descending
-   ASC: ascending
-   DESC and ASC should be repeated for each column


<a id="orgeb698c5"></a>

## Math Operations

Creating new column in the output from math operations on other
columns:

    SELECT col1,col2, col1*col2 AS new_col
           FROM my_table;

new<sub>col</sub> is as alias for the new column 


<a id="orge0a8cd8"></a>

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


### DISTINCT

It recognizes duplicates in a column

    SELECT count(DISTINCT col1)
           FROM my_table


<a id="orge80e814"></a>

## Grouping Data with SQL


### GROUP BY

In the following example we are counting the number of cities each
country has in our table customers:

    select country, count(city) from customers group by country ;	


### HAVING

It filters the result of group by like where. In the following
example, the result is filtered to those countries with customers
having a special email patter: 

    select country, count(city) from customers group by country having  email like '%com';	

We can use multiple columns for group by. If there are more columns
in the group by, these groups need to be in the select part
too. NULL is categorized separately.

WHERE is used before grouping and HAVING is used after it. 


<a id="org2912447"></a>

# Sample Database

Download the sample database called chinook from this [link](https://www.sqlitetutorial.net/sqlite-sample-database/).


<a id="org9fbb669"></a>

## see columns in a sample table

    select * from genres; 


<a id="org6863ced"></a>

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

