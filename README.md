
# Table of Contents

1.  [WEEK #1](#org2644863)
    1.  [keywords](#org7e61123)
    2.  [installation](#org4daf85f)
    3.  [commands](#org9894645)
        1.  [select](#org489ab3b)
        2.  [create table](#org81db404)
        3.  [insert into table](#orgbcc3706)
        4.  [create temporary table](#orgdbfbb68)
        5.  [adding comments by &#x2013; and *\*\**](#orgd290b67)
    4.  [articles](#orgb635bdd)
2.  [WEEK #2](#org5b87e73)
    1.  [Introduction](#orge3c85aa)
        1.  [Clauses and operators](#orgb5f9953)
        2.  [Wildcards](#orgc2e83c0)
        3.  [Math operators](#org7873520)
    2.  [Basics of Filtering with SQL](#org97a8343)
        1.  [where clause operator](#org12b919e)
        2.  [BETWEEN AND](#org874b8d1)
    3.  [Advanced Filtering: IN, OR, and NOT](#orgb5517ec)
        1.  [IN](#orgf4488ef)
        2.  [OR](#org59865b7)
        3.  [IN or OR](#orga400383)
        4.  [OR  AND](#orgc0157d3)
    4.  [Using Wildcards in SQL](#org9545250)
        1.  [LIKE operator(predicate)](#org7e8e323)
    5.  [ORDER BY](#org332adc7)
    6.  [Math Operations](#org983a3b7)
    7.  [Aggregate Functions](#org749b08c)
        1.  [DISTINCT](#orgf0e19fb)
    8.  [Grouping Data with SQL](#org49700bb)
        1.  [GROUP BY](#orgc174399)
        2.  [HAVING](#orgf331523)
3.  [Sample Database](#orgb2dab07)
    1.  [see columns in a sample table](#org022f6c7)
4.  [GENERAL COMMANDS](#org62cd1f8)

This file includes notes and summary of the course [SQL for Data
Science](https://www.coursera.org/learn/sql-for-data-science) from University of California, Davis available in Coursera
as well as additional information that I find useful to learn but it's
missing in the course. You can use it as a supplementary material if
you're taking the course or as an standalone summary of basics of SQL
for data science.

You are encouraged to download the README.org and open it inside Emacs
if you're familiar with org mode. It has the same content.


<a id="org2644863"></a>

# WEEK #1


<a id="org7e61123"></a>

## keywords

-   data modeling
-   NoSQL
-   primary keys, foreign keys
-   ER diagrams: Chen notation, Crow's foot notation, UML class diagram notation


<a id="org4daf85f"></a>

## installation

-   for Linux: install sqlite3 from terminal


<a id="org9894645"></a>

## commands


<a id="org489ab3b"></a>

### select

simple select query

    select col1, col2, col3 from my_table limit number_of_lines;

limit the number of rows

    select col1, col2, col3 from my_table where col4 = 'value';

sum of a column

    select sum(col1) from my_table;


<a id="org81db404"></a>

### create table

    create table my_table
           (col1 char(20) null,
           col2 char(20) not null,
           col3 char(20) primary key);


<a id="orgbcc3706"></a>

### insert into table

    	/* It's a good practice to first
    	identify columns that the values
    	 are going to get there */
    insert into my_table
           (col1, col2, )
           values
           (value1, value2,);		


<a id="orgdbfbb68"></a>

### create temporary table

    	-- create a subset from a table
    create temporary table my_tmp_table as
           (
           select *
           from my_table
           where col1 = 'value')


<a id="orgd290b67"></a>

### adding comments by &#x2013; and *\*\**


<a id="orgb635bdd"></a>

## articles

-   [AWS and SQL](https://aws.amazon.com/what-is/sql/)
-   [Sqlite toturials](https://www.w3resource.com/sqlite/index.php)
-   [SQL vs. NoSQL – Know the Difference](https://dataconomy.com/2014/07/01/sql-vs-nosql-need-know/)
-   [NoSQL keeps rising, but relational databases still dominate big data](https://www.techrepublic.com/article/nosql-keeps-rising-but-relational-databases-still-dominate-big-data/)
-   


<a id="org5b87e73"></a>

# WEEK #2

Filtering sorting and calculating data with SQL


<a id="orge3c85aa"></a>

## Introduction


<a id="orgb5f9953"></a>

### Clauses and operators

-   WHERE
-   BETWEEN AND
-   IN
-   OR
-   NOT
-   LIKE
-   ORDER BY
-   GROUP BY


<a id="orgc2e83c0"></a>

### Wildcards


<a id="org7873520"></a>

### Math operators

-   AVERAGE
-   COUNT
-   MAX
-   MIN


<a id="org97a8343"></a>

## Basics of Filtering with SQL


<a id="org12b919e"></a>

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


<a id="org874b8d1"></a>

### BETWEEN AND

    select city from customers where customerid between 4 and 10;	


<a id="orgb5517ec"></a>

## Advanced Filtering: IN, OR, and NOT


<a id="orgf4488ef"></a>

### IN

-   use parentheses for more than one condition with comma between them
    
        select country from customers where city in ('Paris', 'Rome', 'Oslo');


<a id="org59865b7"></a>

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


<a id="orga400383"></a>

### IN or OR

-   IN is faster
-   OR: order is important
-   IN: order is not important
-   IN: making sub-queries


<a id="orgc0157d3"></a>

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


<a id="org9545250"></a>

## Using Wildcards in SQL


<a id="org7e8e323"></a>

### LIKE operator(predicate)

Used for only string data not numerical data. 

-   %: '%string', 'st%g', 'st%'
    it does not match NULL value
-   \_: is not supported in DB2 but most other system support it.
    
        WHERE val LIKE '_string'
-   []: not supported in SQLite
-   Wildcards are slower than filtering operators


<a id="org332adc7"></a>

## ORDER BY

-   It should be the last clause in an statement
-   Different columns can be used for sorting
-   Column position can be used
    
        ORDER BY 1,5
-   DESC: descending
-   ASC: ascending
-   DESC and ASC should be repeated for each column


<a id="org983a3b7"></a>

## Math Operations

Creating new column in the output from math operations on other
columns:

    SELECT col1,col2, col1*col2 AS new_col
           FROM my_table;

new<sub>col</sub> is as alias for the new column 


<a id="org749b08c"></a>

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


<a id="orgf0e19fb"></a>

### DISTINCT

It recognizes duplicates in a column

    SELECT count(DISTINCT col1)
           FROM my_table


<a id="org49700bb"></a>

## Grouping Data with SQL


<a id="orgc174399"></a>

### GROUP BY

In the following example we are counting the number of cities each
country has in our table customers:

    select country, count(city) from customers group by country ;	


<a id="orgf331523"></a>

### HAVING

It filters the result of group by like where. In the following
example, the result is filtered to those countries with customers
having a special email patter: 

    select country, count(city) from customers group by country having  email like '%com';	

We can use multiple columns for group by. If there are more columns
in the group by, these groups need to be in the select part
too. NULL is categorized separately.

WHERE is used before grouping and HAVING is used after it. 


<a id="orgb2dab07"></a>

# Sample Database

Download the sample database called chinook from this [link](https://www.sqlitetutorial.net/sqlite-sample-database/).


<a id="org022f6c7"></a>

## see columns in a sample table

    select * from genres; 


<a id="org62cd1f8"></a>

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

