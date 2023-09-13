
# Table of Contents

1.  [Sample Database](#org1e19c7d)
2.  [General Commands](#orgdab65e3)
3.  [WEEK #1](#org6fb0fac)
    1.  [keywords](#orgdc31245)
    2.  [installation](#org885e8e1)
    3.  [commands](#org0559671)
    4.  [articles](#org2b54f9a)
4.  [WEEK #2](#org41e5ec0)
    1.  [Introduction](#orgfc56c28)
    2.  [Basics of Filtering with SQL](#orgef09101)
    3.  [Advanced Filtering: IN, OR, and NOT](#org2d482fb)
    4.  [Using Wildcards in SQL](#orgea02d14)
    5.  [ORDER BY](#org7c7d107)
    6.  [Math Operations](#org1f09c93)
    7.  [Aggregate Functions](#org270bd79)
    8.  [Grouping Data with SQL](#org693b44a)
5.  [WEEK #3](#org3b25922)
    1.  [Using Subqueries](#org32da0c5)
    2.  [Subquery Best Practices and Considerations](#org0f8a994)
    3.  [Joins](#orga2a0e84)
    4.  [JOIN vs Subquery](#orgd4c578f)
6.  [WEEK #4](#orgf7a4981)
    1.  [Working with Text Strings](#org06b89f5)
    2.  [Date and Time Strings](#org9c0db81)
    3.  [Case Statements](#orgcddc9e0)
    4.  [Create View](#orge04b208)
    5.  [Data Governance and Profiling](#orgc771516)
    6.  [links](#orgee94fa6)

This file includes notes and summary of the course [SQL for Data
Science](https://www.coursera.org/learn/sql-for-data-science) from University of California, Davis available in Coursera
as well as additional information that I find useful to learn but it's
missing in the course. You can use it as a supplementary material if
you're taking the course or as an standalone summary of basics of SQL
for data science.

You are encouraged to download the README.org and open it inside Emacs
if you're familiar with org mode. It has the same content.


<a id="org1e19c7d"></a>

# Sample Database

Download the sample database called chinook from this [link](https://www.sqlitetutorial.net/sqlite-sample-database/).


<a id="orgdab65e3"></a>

# General Commands

Some general commands you can use to inspect your sample database:

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


<a id="org6fb0fac"></a>

# WEEK #1


<a id="orgdc31245"></a>

## keywords

-   data modeling
-   NoSQL
-   primary keys, foreign keys
-   ER diagrams: Chen notation, Crow's foot notation, UML class diagram notation


<a id="org885e8e1"></a>

## installation

-   for Linux: install sqlite3 from terminal


<a id="org0559671"></a>

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


<a id="org2b54f9a"></a>

## articles

-   [AWS and SQL](https://aws.amazon.com/what-is/sql/)
-   [Sqlite toturials](https://www.w3resource.com/sqlite/index.php)
-   [SQL vs. NoSQL – Know the Difference](https://dataconomy.com/2014/07/01/sql-vs-nosql-need-know/)
-   [NoSQL keeps rising, but relational databases still dominate big data](https://www.techrepublic.com/article/nosql-keeps-rising-but-relational-databases-still-dominate-big-data/)
-   


<a id="org41e5ec0"></a>

# WEEK #2

Filtering, sorting, and calculating data with SQL


<a id="orgfc56c28"></a>

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


<a id="orgef09101"></a>

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


<a id="org2d482fb"></a>

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


<a id="orgea02d14"></a>

## Using Wildcards in SQL


### LIKE operator(predicate)

Used for only string data not numerical data. 

-   %: '%string', 'st%g', 'st%'
    it does not match NULL value
-   \_: is not supported in DB2 but most other system support it.
    
        WHERE val LIKE '_string'
-   []: not supported in SQLite
-   Wildcards are slower than filtering operators


<a id="org7c7d107"></a>

## ORDER BY

-   It should be the last clause in an statement
-   Different columns can be used for sorting
-   Column position can be used
    
        ORDER BY 1,5
-   DESC: descending
-   ASC: ascending
-   DESC and ASC should be repeated for each column


<a id="org1f09c93"></a>

## Math Operations

Creating new column in the output from math operations on other
columns:

    SELECT col1,col2, col1*col2 AS new_col
           FROM my_table;

new<sub>col</sub> is as alias for the new column 


<a id="org270bd79"></a>

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


<a id="org693b44a"></a>

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


<a id="org3b25922"></a>

# WEEK #3


<a id="org32da0c5"></a>

## Using Subqueries

They are used to create queries inside queries.

    select country, company from customers
    where customerid in
    (select customerid from invoices where billingstate like 'a%');


<a id="org0f8a994"></a>

## Subquery Best Practices and Considerations

Format your code using [poorsql.com](https://poorsql.com/)


<a id="orga2a0e84"></a>

## Joins


### selecting from different tables

    SELECT orders.order_id, customers.customer_name
    FROM orders
    INNER JOIN customers ON orders.customer_id = customers.customer_id;

The dot (.) in orders.order<sub>id</sub> and customers.customer<sub>name</sub> is used to
specify the table from which each column should be retrieved. This
notation is often referred to as "table.column" notation, and it's
necessary when you are selecting columns from multiple tables that
have columns with the same name.


### INNER join

    SELECT orders.order_id, customers.customer_name
    FROM orders
    INNER JOIN customers ON orders.customer_id = customers.customer_id;

1.  \`SELECT orders.order<sub>id</sub>, customers.customer<sub>name</sub>\`: This part of the SQL statement specifies the columns you want to retrieve in the result set. It's saying that you want to retrieve two columns:
    -   \`orders.order<sub>id</sub>\`: This is the \`order<sub>id</sub>\` column from the \`orders\` table.
    -   \`customers.customer<sub>name</sub>\`: This is the \`customer<sub>name</sub>\` column from the \`customers\` table.

2.  \`FROM orders\`: This part of the statement specifies the source table from which you want to retrieve data. In this case, it's the \`orders\` table.

3.  \`INNER JOIN customers ON orders.customer<sub>id</sub> = customers.customer<sub>id</sub>\`: This is where the actual join operation occurs. Let's break it down further:
    -   \`INNER JOIN\`: This specifies that you want to perform an inner join between the \`orders\` table and the \`customers\` table. An inner join returns only the rows where there is a match in both tables.
    -   \`customers\` is the name of the table you're joining with.
    -   \`ON orders.customer<sub>id</sub> = customers.customer<sub>id</sub>\`: This part of the statement specifies the join condition. It tells the database how to match rows between the two tables. Specifically, it's saying that you want to join rows where the \`customer<sub>id</sub>\` column in the \`orders\` table is equal to the \`customer<sub>id</sub>\` column in the \`customers\` table. This condition establishes the relationship between the two tables based on the \`customer<sub>id</sub>\` column.

So, when you execute this SQL statement, SQLite will retrieve data from both the \`orders\` and \`customers\` tables and combine it into a single result set. The result will include pairs of \`order<sub>id</sub>\` and \`customer<sub>name</sub>\` where the \`customer<sub>id</sub>\` values in the \`orders\` and \`customers\` tables match.

For example, if you have the following data:

**orders table:**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">order<sub>id</sub></th>
<th scope="col" class="org-right">customer<sub>id</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-right">101</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-right">102</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-right">103</td>
</tr>
</tbody>
</table>

**customers table:**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">customer<sub>id</sub></th>
<th scope="col" class="org-left">customer<sub>name</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">101</td>
<td class="org-left">Alice</td>
</tr>


<tr>
<td class="org-right">102</td>
<td class="org-left">Bob</td>
</tr>


<tr>
<td class="org-right">104</td>
<td class="org-left">Carol</td>
</tr>
</tbody>
</table>

The result of the SQL query will be:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">order<sub>id</sub></th>
<th scope="col" class="org-left">customer<sub>name</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-left">Alice</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-left">Bob</td>
</tr>
</tbody>
</table>

As you can see, only the rows with matching \`customer<sub>id</sub>\` values (1
and 2) are included in the result, and it combines the relevant data
from both tables.


### LEFT JOIN (or LEFT OUTER JOIN)

-   A LEFT JOIN returns all rows from the left table and the matched rows

from the right table.

-   If there's no match in the right table, NULL

values are filled in for the columns from the right table.

Example:

    SELECT customers.customer_name, orders.order_id
    FROM customers
    LEFT JOIN orders ON customers.customer_id = orders.customer_id;


### RIGHT JOIN (or RIGHT OUTER JOIN)

-   A RIGHT JOIN is similar to a LEFT JOIN, but it returns all rows

from the right table and the matched rows from the left table.

-   If there's no match in the left table, NULL values are filled in for

the columns from the left table.

Example:

    SELECT customers.customer_name, orders.order_id
    FROM customers
    RIGHT JOIN orders ON customers.customer_id = orders.customer_id;


### LEFT or RIGHT

In SQL joins, particularly when discussing LEFT JOIN and RIGHT JOIN,
the terms "left" and "right" refer to the order of the tables being
joined and the direction of the inclusion of rows in the result
set. These terms help describe which table's data is preserved fully
and which table's data may have missing values (NULLs) in the result
set. Let's clarify the differences:

1.  LEFT JOIN (or LEFT OUTER JOIN):
    -   The "left" table is the table listed on the left side of the JOIN
        clause.
    -   All rows from the left table are included in the result set,
        regardless of whether there is a match in the right table.
    -   If there is a match in the right table, the corresponding data is
        included in the result set.
    -   If there is no match in the right table, NULL values are used for
        the columns from the right table.

2.  RIGHT JOIN (or RIGHT OUTER JOIN):
    -   The "right" table is the table listed on the right side of the
        JOIN clause.
    -   All rows from the right table are included in the result set,
        regardless of whether there is a match in the left table.
    -   If there is a match in the left table, the corresponding data is
        included in the result set.
    -   If there is no match in the left table, NULL values are used for
        the columns from the left table.

In summary, the primary difference between LEFT JOIN and RIGHT JOIN is
the direction in which they include rows from the tables involved in
the join. LEFT JOIN keeps all rows from the left table, while RIGHT
JOIN keeps all rows from the right table. The choice of whether to use
LEFT JOIN or RIGHT JOIN depends on your specific data and query
requirements. Most often, LEFT JOIN is used because it retains all
records from the "left" or main table and includes matching data from
the "right" or related table when available.


### CROSS join

A CROSS JOIN, also known as a Cartesian join, is a type of join operation in SQL where every row from one table is combined with every row from another table, resulting in a Cartesian product of the two tables. In other words, it creates all possible combinations of rows from the two tables, without any specific condition or criteria for matching rows. As a result, the size of the result set can grow rapidly, especially if the tables being joined are large.

Here's the basic syntax for a CROSS JOIN:

    SELECT *
    FROM table1
    CROSS JOIN table2;

In this syntax:

-   \`table1\` and \`table2\` are the names of the two tables you want to combine.
-   \`\*\` is used to select all columns from both tables in the Cartesian product.

Here's an example to illustrate a CROSS JOIN:

Assume you have two tables:

**table1 (colors):**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">color</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">Red</td>
</tr>


<tr>
<td class="org-left">Green</td>
</tr>


<tr>
<td class="org-left">Blue</td>
</tr>
</tbody>
</table>

**table2 (sizes):**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">size</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">Small</td>
</tr>


<tr>
<td class="org-left">Medium</td>
</tr>


<tr>
<td class="org-left">Large</td>
</tr>
</tbody>
</table>

If you perform a CROSS JOIN between these two tables:

    SELECT *
    FROM colors
    CROSS JOIN sizes;

The result will be the Cartesian product of all color and size combinations:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">color</th>
<th scope="col" class="org-left">size</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">Red</td>
<td class="org-left">Small</td>
</tr>


<tr>
<td class="org-left">Red</td>
<td class="org-left">Medium</td>
</tr>


<tr>
<td class="org-left">Red</td>
<td class="org-left">Large</td>
</tr>


<tr>
<td class="org-left">Green</td>
<td class="org-left">Small</td>
</tr>


<tr>
<td class="org-left">Green</td>
<td class="org-left">Medium</td>
</tr>


<tr>
<td class="org-left">Green</td>
<td class="org-left">Large</td>
</tr>


<tr>
<td class="org-left">Blue</td>
<td class="org-left">Small</td>
</tr>


<tr>
<td class="org-left">Blue</td>
<td class="org-left">Medium</td>
</tr>


<tr>
<td class="org-left">Blue</td>
<td class="org-left">Large</td>
</tr>
</tbody>
</table>

As you can see, every color is combined with every size, resulting in
a total of 9 rows in the result set.

CROSS JOINs are relatively rare in practice because they tend to
generate large result sets and can be computationally expensive. They
are typically used in specific scenarios where you need to generate
all possible combinations, such as when creating test data or
performing certain types of mathematical calculations. In most cases,
other types of joins (e.g., INNER JOIN, LEFT JOIN) with appropriate
conditions are more commonly used to retrieve meaningful data from
related tables.


### FULL UTER JOIN

Here's a brief overview of the key characteristics of a FULL OUTER
JOIN:

Returns All Rows: Unlike INNER JOIN, which only returns matching
rows, a FULL OUTER JOIN returns all rows from both the left and
right tables.

NULL Values: When there is no match for a row in one of the
tables, the columns from that table will contain NULL values in
the result set.

Combines Data: A FULL OUTER JOIN combines data from two tables
based on a specified join condition, creating a unified result
set.

Useful for Comparisons: FULL OUTER JOINs are often used when you
need to compare data from two tables comprehensively, such as
identifying records that exist in one table but not in the other
or finding matching records while also including non-matching
ones.

Here's the basic syntax for a FULL OUTER JOIN:

    SELECT *
    FROM table1
    FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;


### multiple columns

In this scenario, we have three tables: \`orders\`, \`customers\`,
and \`products\`. We want to retrieve a list of orders that includes the
customer name and the product name for each order.

Assuming the following table structures:

****orders:****

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">order<sub>id</sub></th>
<th scope="col" class="org-right">customer<sub>id</sub></th>
<th scope="col" class="org-right">product<sub>id</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-right">101</td>
<td class="org-right">201</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-right">102</td>
<td class="org-right">202</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-right">103</td>
<td class="org-right">201</td>
</tr>


<tr>
<td class="org-right">4</td>
<td class="org-right">104</td>
<td class="org-right">203</td>
</tr>
</tbody>
</table>

**customers:**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">customer<sub>id</sub></th>
<th scope="col" class="org-left">customer<sub>name</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">101</td>
<td class="org-left">Alice</td>
</tr>


<tr>
<td class="org-right">102</td>
<td class="org-left">Bob</td>
</tr>


<tr>
<td class="org-right">103</td>
<td class="org-left">Carol</td>
</tr>


<tr>
<td class="org-right">104</td>
<td class="org-left">David</td>
</tr>
</tbody>
</table>

**products:**

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">product<sub>id</sub></th>
<th scope="col" class="org-left">product<sub>name</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">201</td>
<td class="org-left">Laptop</td>
</tr>


<tr>
<td class="org-right">202</td>
<td class="org-left">Smartphone</td>
</tr>


<tr>
<td class="org-right">203</td>
<td class="org-left">Tablet</td>
</tr>
</tbody>
</table>

We can use an INNER JOIN to combine these tables to get the desired result:

    SELECT orders.order_id, customers.customer_name, products.product_name
    FROM (orders
    INNER JOIN customers ON orders.customer_id = customers.customer_id)
    INNER JOIN products ON orders.product_id = products.product_id;

In this query:

1.  The first INNER JOIN combines the \`orders\` and \`customers\` tables
    based on the \`customer<sub>id</sub>\` column, linking each order to its
    respective customer.

2.  The second INNER JOIN combines the result of the first join (which
    includes order and customer information) with the \`products\` table
    based on the \`product<sub>id</sub>\` column, linking each order to its
    corresponding product.

The result of this query will be a list of orders with the customer
name and the product name for each order:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">order<sub>id</sub></th>
<th scope="col" class="org-left">customer<sub>name</sub></th>
<th scope="col" class="org-left">product<sub>name</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-left">Alice</td>
<td class="org-left">Laptop</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-left">Bob</td>
<td class="org-left">Smartphone</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-left">Carol</td>
<td class="org-left">Laptop</td>
</tr>


<tr>
<td class="org-right">4</td>
<td class="org-left">David</td>
<td class="org-left">Tablet</td>
</tr>
</tbody>
</table>

This query demonstrates how you can use INNER JOINs to combine data
from three tables to create a comprehensive result set that includes
information from all three tables based on specified join conditions.


### using alias

    SELECT c.customer_name, o.order_date
    FROM customers c
    INNER JOIN orders o ON c.customer_id = o.customer_id
    WHERE c.city = 'New York';

    SELECT o.order_id, c.customer_name
    FROM orders AS o
    INNER JOIN customers AS c ON o.customer_id = c.customer_id;


### self-join

A self-join is a specific type of join operation in SQL where a table
is joined with itself. In other words, it's a way to combine rows from
the same table based on a related column. Self-joins are commonly used
when you have hierarchical or recursive data stored within a single
table, and you need to retrieve relationships or data from different
rows within the same table.

Here's how a self-join works:

1.  **Table with Self-Reference**: In a self-join scenario, the table
    must contain a column or columns that establish a relationship
    between rows within the same table. This typically involves having
    a foreign key column that references the primary key column of the
    same table. This creates a self-referencing relationship.

2.  **Join Condition**: You specify a join condition that defines how the
    rows in the table should be matched with other rows in the same
    table. This condition typically involves comparing the values in
    the self-referencing columns.

3.  **Result Set**: The result of the self-join is a new table that
    combines data from the original table based on the specified join
    condition.

Here's a simple example to illustrate a self-join. Suppose you have an
"employees" table with the following structure:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">employee<sub>id</sub></th>
<th scope="col" class="org-left">employee<sub>name</sub></th>
<th scope="col" class="org-right">manager<sub>id</sub></th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-left">Alice</td>
<td class="org-right">NULL</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-left">Bob</td>
<td class="org-right">1</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-left">Carol</td>
<td class="org-right">1</td>
</tr>


<tr>
<td class="org-right">4</td>
<td class="org-left">David</td>
<td class="org-right">2</td>
</tr>


<tr>
<td class="org-right">5</td>
<td class="org-left">Eve</td>
<td class="org-right">2</td>
</tr>
</tbody>
</table>

In this table:

-   \`employee<sub>id</sub>\` is the primary key.
-   \`employee<sub>name</sub>\` stores the names of employees.
-   \`manager<sub>id</sub>\` is a foreign key that references the \`employee<sub>id</sub>\` of the employee's manager. It establishes a self-referencing relationship.

You can use a self-join to retrieve the names of employees along with the names of their managers:

    SELECT e.employee_name AS employee, m.employee_name AS manager
    FROM employees e
    LEFT JOIN employees m ON e.manager_id = m.employee_id;

In this query:

-   \`e\` is an alias for the "employees" table, representing employees.
-   \`m\` is an alias for the same "employees" table, representing managers.
-   The self-join condition \`e.manager<sub>id</sub> = m.employee<sub>id</sub>\` connects each
    employee with their respective manager.

The result of the self-join will be:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">employee</th>
<th scope="col" class="org-left">manager</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">Alice</td>
<td class="org-left">NULL</td>
</tr>


<tr>
<td class="org-left">Bob</td>
<td class="org-left">Alice</td>
</tr>


<tr>
<td class="org-left">Carol</td>
<td class="org-left">Alice</td>
</tr>


<tr>
<td class="org-left">David</td>
<td class="org-left">Bob</td>
</tr>


<tr>
<td class="org-left">Eve</td>
<td class="org-left">Bob</td>
</tr>
</tbody>
</table>

As you can see, the self-join allows you to retrieve the names of
employees along with the names of their respective managers from the
same table, creating a hierarchical relationship. Self-joins are
particularly useful in scenarios involving organizational hierarchies,
bill-of-materials structures, and other situations where data has a
parent-child or recursive relationship within a single table.


### UNIONs

In SQL, the UNION operator is used to combine the result sets of two
or more SELECT statements into a single result set. It allows you to
merge rows from different tables or even from the same table based on
common columns or data types. The UNION operator removes duplicate
rows by default, but you can also use UNION ALL if you want to include
duplicate rows in the result.

-   **Column Compatibility**: The SELECT statements within a UNION must have
    the same number of columns, and the corresponding columns in each
    SELECT statement must have compatible data types. The column names
    from the first SELECT statement are used as the column names in the
    result.

-   **Duplicate Removal**: By default, UNION removes duplicate rows from the
    combined result set. If you want to keep duplicate rows, you can use
    UNION ALL instead.

    SELECT column1, column2, ...
    FROM table1
    UNION
    SELECT column1, column2, ...
    FROM table2;


<a id="orgd4c578f"></a>

## JOIN vs Subquery

In JOIN you can call different columns from different tables but in
subquery, the table that is called inside the subquery is not
accessible outside the subquery. 


<a id="orgf7a4981"></a>

# WEEK #4


<a id="org06b89f5"></a>

## Working with Text Strings

-   Concatenating
    
        select col1 || '(' || col2 || ')' from tab1;
-   Trimming
    
        select trim('      you the best     ') as trim_str;

Removes trailing spaces from both sides. There is RTRIM and LTRIM also.

-   Substring
    
        select substr(col1, num1, num2) from tab1;

num1 is the beginning of the trimming and num2 is the length of the
trim. num1 starts with 1.

-   Case
    
        select upper(col1) from tab1;
        select lower(col1) from tab1;
        select ucase(col1) from tab1;


<a id="org9c0db81"></a>

## Date and Time Strings


### strfmt

The \`strftime\` function in SQLite is used to format date and time
values as strings. It allows you to specify a format string with
various modifiers to control how the date and time should be
displayed. The basic syntax of the \`strftime\` function is as follows:

    strftime(format, timestamp)

-   \`format\`: This is a required argument and specifies the format you
    want the date and time to be displayed in. It is a string containing
    format codes and optional text.

-   \`timestamp\`: This is the timestamp or date and time value that you
    want to format.

Here are some common format codes and modifiers you can use with the
\`strftime\` function in SQLite:

**Date Format Codes**:

-   \`%Y\`: Four-digit year (e.g., 2023).
-   \`%m\`: Month as a zero-padded decimal number (01-12).
-   \`%d\`: Day of the month as a zero-padded decimal number (01-31).
-   \`%W\`: Week number of the year as a decimal number (00-53).

**Time Format Codes**:

-   \`%H\`: Hour (00-23).
-   \`%M\`: Minute (00-59).
-   \`%S\`: Second (00-59).

**Other Format Codes**:

-   \`%a\`: Abbreviated weekday name (Sun, Mon, Tue, etc.).
-   \`%A\`: Full weekday name (Sunday, Monday, Tuesday, etc.).
-   \`%b\`: Abbreviated month name (Jan, Feb, Mar, etc.).
-   \`%B\`: Full month name (January, February, March, etc.).
-   \`%c\`: Preferred date and time representation (usually the same as \`%a %b %d %H:%M:%S %Y\`).
-   \`%p\`: AM or PM designation (AM/PM).

**Modifiers**:

-   \`-\`: A hyphen \`-\` before a modifier (e.g., \`%-d\`) removes leading zeros.
-   \`\_\`: An underscore \`\_\` before a modifier (e.g., \`\_%d\`) pads with spaces instead of zeros.
-   \`0\`: A zero \`0\` before a modifier (e.g., \`%0d\`) pads with zeros (default behavior).

Examples of using the \`strftime\` function with modifiers and format codes:

    -- Format a timestamp as "YYYY-MM-DD HH:MM:SS"
    SELECT strftime('%Y-%m-%d %H:%M:%S', '2023-09-06 15:30:00');

    -- Format a timestamp without leading zeros in the day and month
    SELECT strftime('%Y-%-m-%-d %H:%M:%S', '2023-09-06 15:30:00');

    -- Format a timestamp with abbreviated month and day names
    SELECT strftime('%A, %B %d, %Y', '2023-09-06 15:30:00');

    -- Format a timestamp as "hh:MM AM/PM"
    SELECT strftime('%I:%M %p', '2023-09-06 15:30:00');

\`\`\`


### Now

To retrieve the current date:

    select date('now');


<a id="orgcddc9e0"></a>

## Case Statements

In SQLite, the CASE statement is a conditional expression that allows
you to perform conditional logic within SQL queries. It's useful for
making decisions and returning different values or performing
different actions based on specific conditions. The CASE statement can
be used in both SELECT statements and UPDATE statements.

The basic syntax of the CASE statement in SQLite is as follows:

    CASE
        WHEN condition1 THEN result1
        WHEN condition2 THEN result2
        ...
        ELSE else_result
    END

Example:

    SELECT
        name,
        CASE
    	WHEN age >= 18 THEN 'Adult'
    	ELSE 'Minor'
        END AS age_group
    FROM people;

In this example, we use a CASE statement to categorize people as
either 'Adult' or 'Minor' based on their age.


<a id="orge04b208"></a>

## Create View

In SQLite, a view is a virtual table created from the result of a
SELECT query. Unlike physical tables, views do not store data
themselves; instead, they provide a way to access and manipulate data
from one or more underlying tables or other views. Views are often
used to simplify complex queries, encapsulate logic, and provide a
consistent interface to users or applications.

To create a view in SQLite, you use the CREATE VIEW statement. Here's
the basic syntax:

    CREATE VIEW view_name AS
    SELECT columns
    FROM tables
    WHERE conditions;

Once a view is created, you can query it just like a regular table
using the SELECT statement:

    SELECT * FROM top_customers;


### drop the view

    drop view my_view;


### ETL

ETL stands for Extract, Transform, Load, and it is a concept related
to data integration and database management, often associated with SQL
databases. ETL is a process used to collect, clean, and move data from
various sources into a destination database or data warehouse for
analysis, reporting, or other purposes. Each phase of the ETL process
serves a specific purpose.


<a id="orgc771516"></a>

## Data Governance and Profiling

Data profiling in SQL is a process used to analyze and understand the
characteristics, structure, and quality of a dataset or a database. It
involves examining the data to gain insights into its content,
distribution, completeness, accuracy, and potential issues. Data
profiling is an essential step in data analysis, data cleansing, and
data integration processes. Here are the key concepts related to data
profiling in SQL:

-   Data Exploration: Data profiling begins with exploring the data to
    get a high-level understanding of its contents. Analysts or data
    professionals use SQL queries to retrieve sample data, count
    records, and examine the data types of columns.

-   Column Profiling: Data profiling often involves profiling individual
    columns within a dataset or database table. This includes:
    Determining data types (e.g., integer, string, date). Calculating
    statistics such as minimum, maximum, mean, median, and standard
    deviation. Identifying unique values and their
    frequencies. Detecting missing values and calculating the percentage
    of missing data. Checking for data patterns, formats, and
    distributions.


<a id="orgee94fa6"></a>

## links

SQL puzzles

[SQL Authority: SQL Puzzles](https://blog.sqlauthority.com/category/sql-puzzle/)

Recommended by many recruiters to practice SQL for a data science interview.

[SQLZOO](https://sqlzoo.net/)

