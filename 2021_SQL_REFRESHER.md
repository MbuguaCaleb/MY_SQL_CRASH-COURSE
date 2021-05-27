**Relational Database**

```
Mutiple tables are related to each other using a relationship


```

**Views**

```
Views are like virtual tables.

We can combine data from different tables and put them in a view.

This is especially powerful  for creating reports.

```

**Stored Procedures and Functions**

```
These are little programmes we store inside of our database for quering data

We can have a procedure for getting all the customers in a given city.

```

**SELECT STATEMENT**

```
1. Line spaces and white tabs are ignored when executing SQL statements,

2.When Queries get more complex it is better to put each on a new line

```

```
(a)
When ever we use mutiple sql statements we need to terminate each with a colon.

USE sql_store;

SELECT * FROM customers


```

```
(b)
TO filter data even more we can add the WHERE and the ORDER BY CLAUSE

SELECT *
FROM customers
-- WHERE customer_id = 1
ORDER BY first_name;

```

```
(c)

Arithmetic Operations

SELECT
      last_name
      ,first_name,
      points,
      (points + 10)  *100
FROM customers


Adding an alias to the column name

SELECT
      last_name
      ,first_name,
      points,
      (points + 10)  *100  AS discount_factor
FROM customers


including a space on my alias name

SELECT
      last_name
      ,first_name,
      points,
      (points + 10)  *100  AS 'discount factor'
FROM customers


Removing duplicates from my data

I use the distinct key word

SELECT DISTINCT state from customers;

```

**SELECT STATEMENT EXERCISE**

```

SELECT name, unit_price, (unit_price*1.1) as new_price FROM products;

```

**THE WHERE CLAUSE**

```
It is mainly used to filter data.

Arithmetic operators in SQL

>------->greater than
>=------>greater than or equal to
<------>Less than/Equal to
<=----->Less than or equal to
=----->Equal to operator
!=--->Not Equal Operator
<>--->Not Equal Operator

```

```
SELECT *
FROM customers
WHERE (points>3000)

Equals sign is in the right most side

```

```
When dealing with strings, we must enclose our data in either
single or double quotes

SELECT *
FROM customers
WHERE state='VA'

It does not matter whether my string values are uppercase or lower case

```

```

SELECT *
FROM customers
WHERE state <>'va'

```

```
Default date format in MYSQL is YYYY-MM-DD

SELECT * FROM customers
WHERE birth_date > '1990-01-01'

Exercise

Getting the orders placed in the current year

SELECT * FROM
orders
WHERE
order_date >= '2019-01-01'


```

**AND OR AND NOT OPERATORS**

```

AND Operator-When using and, both conditions must be true

OR-At least one has to be true



SELECT *
FROM customers
WHERE birth_date > '1990-01-01' AND points > 1000


More complex condition

SELECT *
FROM customers
WHERE birth_date > '1990-01-01' OR points > 1000
AND state='VA'

```

```
-- AND OR AND NOT OPERATORS

-- These enforce Mutiple search conditions

-- SELECT *
-- FROM customers
-- WHERE birth_date > '1990-01-01' OR
--       (points > 1000 AND state='VA')

-- AND HAS GOT HIGHER PRECEDENCE

-- NOT IS USED TO NEGATE THE CONDITION

SELECT *
FROM customers
WHERE NOT (birth_date > '1990-01-01' OR points>1000)

-- This query returns the opposite
-- It is going to return customers born before 1990 aand whose points are
-- less than one thousand

```

**Exercise**

```
SELECT *FROM order_items
WHERE order_id = 6
AND (quantity*unit_price) > 30;

```

**IN OPERATOR**

```

Used to compare an attribute with a list of values


```

```
SQL examples

-- A where clause always expects a condition that will evaluate to either
-- true or false

SELECT * FROM
customers
WHERE state='FL' OR state = 'VA' OR state='GA';

SELECT * FROM
customers
WHERE state IN ('VA','FL','GA');

SELECT * FROM
customers
WHERE state NOT IN ('VA','FL','GA');

SELECT * FROM
products
WHERE quantity_in_stock IN(49,38,72);

```

**BETWEEN**

```
Used when comparing an attribute with a range of
values.

It makes your SQL MORE CLEANER

SELECT *
FROM customers
WHERE points BETWEEN 1000 AND 3000;

Remember the date format

SELECT * FROM
customers WHERE birth_date
BETWEEN '1990-01-01' AND '2000-01-01'

```

**LIKE AND UNLIKE**

```
Returns values marching a particular pattern.

(a)Start with letter b
SELECT * FROM
customers WHERE
last_name LIKE 'b%';

b% means that it does not matter any other characters after the b..

(b)have a be either at the beginning or the end

SELECT * FROM
customers WHERE
last_name LIKE '%b%';

(c)Ends with a particular letter
SELECT * FROM
customers WHERE
last_name LIKE '%y';

Alternative for % is marching with an underscore.
Each underscore represents the exact number of characters.

Case 1
Must have exactly 2 characters and end with a y

SELECT * FROM
customers WHERE
last_name LIKE '_y';

case2

5 underscores and a y

It means that it has exactly 6 characters and ends with a
y.

SELECT * FROM
customers WHERE
last_name LIKE '_____y';

example2
SELECT * FROM
customers WHERE
last_name LIKE 'b____y';

will return data marching exactly this pattern


%(Percent)-------->repserents any number of characters.
_(underscore)------->represents anyy number of characters.

```

**REGEXP**

```

SELECT * FROM
customers
-- WHERE last_name LIKE '%FIELD%'
WHERE last_name REGEXP 'FIELD'

^--------->(represents the beginning of a string)

SELECT * FROM
customers
-- WHERE last_name LIKE '%FIELD%'
WHERE last_name REGEXP '^FIELD'

Means the last name must begin with field.


$---------->(represents end of the field)

SELECT * FROM
customers
-- WHERE last_name LIKE '%FIELD%'
WHERE last_name REGEXP 'FIELD$'

(Last name must end with field)
```

```

-- Last has field or Mac or rose
SELECT * FROM
customers
WHERE last_name REGEXP 'field|mac|rose';


-- Last must start with the given names

SELECT * FROM
customers
WHERE last_name REGEXP '^field|mac|rose';

```

```
More examples


SELECT * FROM
customers
WHERE last_name REGEXP '[gim]e';

-- customer may have ge,ie,and me
-- ge
-- ie
-- me


SELECT * FROM
customers
WHERE last_name REGEXP 'e[gim]';


-- Marching against a range of characters
SELECT * FROM
customers
WHERE last_name REGEXP '[a-h]e';


```

**_Summary_**

```
--^ ---->beginning

--$ ----->end

---| ----->or

[abcd]-Matches either of the charatcers in brackets

--[a-f]--->marches a range of characters.


```

**Exercise**

```
-- GET CUSTOMERS WHOSE FIRST NAME ARE ELKA OR AMBUR
SELECT * FROM customers
WHERE first_name REGEXP 'ELKA|AMBUR' ;

-- LAST NAME ENDS WITH EY OR ON
SELECT * FROM customers
WHERE last_name REGEXP 'EY$|0N$';

-- start with MY AND CONTAINS SE
SELECT * FROM customers
WHERE last_name REGEXP '^MY|SE';


-- Last name contains b followed by r or u
SELECT
    *
FROM
    customers
WHERE
    last_name REGEXP 'B[RU]'


```

**Fetching Null records**

```

SELECT * FROM customers
WHERE phone IS NULL;


NEGATING

SELECT * FROM customers
WHERE phone IS NOT NULL


SELECT * FROM orders
WHERE shipper_id IS NULL;

```

**SORTING COLUMNS VIA ORDER BY**

```
SELECT *
FROM customers
ORDER BY first_name;

-- SORT IN DESCENDING ORDER

SELECT *
FROM customers
ORDER BY first_name
DESC;

-- SORT BY TWO COLUMNS
SELECT *
FROM customers
ORDER BY state ,first_name
DESC;

-- The above will fisrst order by the state and then
-- the first_name

-- In MySQL you can order by a column thats not in your
-- select query unlike other databases which thrown an error cause
-- of this

SELECT first_name,last_name
FROM customers
ORDER BY birth_date
DESC;

-- We can as well order data from an ALIAS
SELECT first_name,last_name, 10*3 AS points
FROM customers
ORDER BY points, birth_date
DESC;

-- We may as well order from an arithmetic expression

SELECT order_id,product_id,quantity,unit_price,
(quantity*unit_price) as total_price
FROM order_items
WHERE order_id=2
ORDER BY total_price DESC;

SELECT order_id,product_id,quantity,unit_price
FROM order_items
WHERE order_id=2
ORDER BY (quantity*unit_price)
DESC;


SELECT * ,
(quantity*unit_price) as total_price
FROM order_items
WHERE order_id=2
ORDER BY total_price DESC;

```

```

SELECT * FROM customers
LIMIT 3;

-- IF LIMIT IS GREATER THAN THE NO OF RECORDS
-- RETURNED THE QUERY RETURNS ALL ROCORDS
SELECT * FROM customers
LIMIT 300;

-- aDDING AN OFFSET
-- SKIP THE FIRST 6 RECORDS THEN PICK NEXT THREE
SELECT * FROM customers
LIMIT 6,3;

-- NOTICE THE LIMIT CLAUSE MUST ALWAYS COME AT THE END
SELECT * FROM customers
ORDER BY points DESC
LIMIT 3;

```

**Inner JOins**

```
Help us select data from mulitple tables

```

```
-- JOIN AS THE WORD SUGGESTS JOINS THE TABLES
SELECT order_id,orders.customer_id, first_name,last_name FROM orders
INNER
JOIN customers
	 ON orders.customer_id = customers.customer_id;

-- I MAY OMIT INNER ANFD JUST WRITE JOIN
SELECT order_id,orders.customer_id, first_name,last_name FROM orders
JOIN customers
	 ON orders.customer_id = customers.customer_id;

--IF A COLUMN HAS THE SAME NAME IN BOTH TABLES I MUST PREFIX IT WITH
THE TABLE NAME WHEN MAKING SELECT

-- --ADDING AN ALIAS
SELECT order_id,o.customer_id, first_name,last_name
FROM orders o
JOIN customers c
	 ON o.customer_id = c.customer_id;


```

```
SELECT order_id,p.name,oi.quantity,oi.unit_price FROM
order_items oi
JOIN products p
     ON oi.order_id = p.product_id
ORDER BY order_id DESC;



```

**Joining Across Databases**

```
-- JOINING ACROSS DATABASES
USE sql_inventory;

SELECT *
FROM sql_store.order_items oi
JOIN products p
ON oi.product_id = p.product_id;


```

**Self Joins**

```
I query a table from Itself if there is related data

-- Helps me Join data from the same table
USE sql_hr;

SELECT * FROM
employees e
JOIN employees m
     ON e.reports_to =m.employee_id;


SELECT
e.employee_id,
e.first_name,
m.first_name as manager
FROM
employees e
JOIN employees m
     ON e.reports_to =m.employee_id

Joining a table by itself is JUST Like the other joins.
The only difference being i call the same tables twice
but with a differenct prefix.



```

**JOINING WITH MORE THAN ONE TABLE**

```
-- //I am Joining Orders to the statuses and customer tables
-- When Joining tables i must join them by virtue of the key relationships
-- When i JOin everything becomes like one table.The only place i must referene
-- with table alias on select is when i have duplicate columns
use sql_store;

SELECT
   o.order_id,
   o.order_date,
   c.first_name,
   c.last_name,
   os.name AS status
FROM orders o
JOIN customers c
     ON o.customer_id = c.customer_id
JOIN order_statuses os
     ON o.status = os.order_status_id;


USE sql_invoicing;

SELECT c.name as client_name,pm.name as payment_method
FROM payments p
JOIN clients c
ON p.client_id = c.client_id
JOIN payment_methods pm
ON p.payment_method = pm.payment_method_id

```

**Compoud Join Conditions**

```
There tables that lack  a primary key
and can uniquely be queried by a combination of two keys.

A table that has two primary keys is known as a composite primary key.

Tables that can be idenfied/related by two unique columns and not only one.

Sample SQL

SELECT *
FROM order_items oi
JOIN order_item_notes oin
     ON oi.order_id=oin.order_id
     AND oi.product_id=oin.product_id


Tables that may be related by 2 keys


```

**Implicit Join Syntax**

```
-- Traditional way to write a Join
SELECT *
FROM orders o
JOIN customers c
     ON o.customer_id=c.customer_id;

-- Implicit Join SYNTAX
-- This is another way to write a join
-- I begin by declaring my tables first

SELECT *
FROM orders o,customers c
WHERE o.customer_id=c.customer_id

The implicit join should however be avoided because it
leads to a cross join should one forget to include the WHERE clause

A cross join is where data from one table is appended onto another
regardless of the condition.


```

**REMEBER!!!!!!!Important**

```

Whenever you write join without stating whether its an inner or outer join,
it is automatucally regarded as an inner join....

Its is adivsable to exlpicitly do your selects,


SELECT
  c.customer_id,
  c.first_name,
  o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id



```

**Outer Joins**

```
-- Innerjoin exculudes all data that does not meet the condition

SELECT
  c.customer_id,
  c.first_name,
  o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id;

-- The above will excude any customer who does not have an order

-- What if i  want to return all the customers regardless to whether or
-- not they have an order?

-- I use an outer join


-- There are two types of outer joins:

-- (a)Left JOIN(shortcut of LEFT OUTER JOIN)

  --   RETURNS ALL DATA FROM THE TABLE ON THE LEFT REGARDLESS OF THE CONDITION
-- (b)RIGHT JOIN(shortcut of right Inner Join)
--   RETURNS ALL DATA FROM THE TABLE ON THE RIGHT REGARDLESS OF THE CONDITION

SELECT
  c.customer_id,
  c.first_name,
  o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id;

-- THE ABOVE RETURNS ALL THE CUSTOMERS EVEN IF THEY DO NOT HAVE AN ORDER

SELECT
  c.customer_id,
  c.first_name,
  o.order_id
FROM customers c
RIGHT JOIN orders o
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id;

-- THE ABOVE WILL RETURN ALL THE ORDERS REGARDLESS


SELECT
  c.customer_id,
  c.first_name,
  o.order_id
FROM  orders o
RIGHT JOIN customers c
    ON c.customer_id = o.customer_id
ORDER BY c.customer_id;

-- Table on the right is table 2 always
-- table on left is table one always


```

**Outer Join exercise**

```
-- products name,id and quanity
-- return a product with no quantiteis as well

SELECT
  p.product_id,
  p.name,
  oi.quantity
FROM products p
LEFT JOIN order_items oi
     ON p.product_id = oi.product_id;



SELECT
  p.product_id,
  p.name,
  oi.quantity
FROM order_items oi
RIGHT JOIN products p
     ON p.product_id = oi.product_id;


```

**Outer Joins From Multiple tables**

```

SELECT
  c.customer_id,
  c.first_name,
  o.order_id,
  sh.name as shipper_name
FROM  orders o
RIGHT JOIN customers c
    ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
    ON sh.shipper_id = o.shipper_id
ORDER BY c.customer_id;

-- As best practice it is good to use the left join
-- It is easier to interpret

SELECT
  c.customer_id,
  c.first_name,
  o.order_id,
  sh.name as shipper_name
FROM  customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
    ON sh.shipper_id = o.shipper_id
ORDER BY c.customer_id;


```

**OUTER JOIN EXERCISE**

```
SELECT
   o.order_date,
   o.order_id,
   c.first_name,
   sh.name AS shipper,
   st.name AS status
FROM orders o
JOIN customers c
   ON o.customer_id = c.customer_id
JOIN order_statuses st
   ON st.order_status_id=o.status
LEFT JOIN shippers sh
   ON o.shipper_id =sh.shipper_id


-- Whenever i have no null data it means i have made an inner join
-- Whenever i have null data it means i have made an outer join.

```

**Self Outer Join**

```

USE sql_hr;

SELECT
   e.employee_id,
   e.first_name,
   e.job_title,
   m.first_name as manager
FROM employees e
LEFT JOIN employees m
     ON e.reports_to = m.employee_id

WITH A INNER JOIN IT WILL ONLY RETURN EMPLOYEES WITH A MANANAGER

```

**USING CLAUSE**

```

Whenever the column names you are joining are the same you
may replace ON condition with USING in your join.

USE sql_store;

SELECT
    o.order_id,
    c.first_name
FROM orders o
JOIN customers c
--     ON o.customer_id=c.customer_id
	USING(customer_id)

USE sql_store;

SELECT
    o.order_id,
    c.first_name,
    sh.name as shipper
FROM orders o
JOIN customers c
	USING(customer_id)
LEFT JOIN shippers sh
    USING(ship



Simlifying a table with a composite primary key with Using

SELECT *
FROM order_items oi
JOIN order_item_notes oin
     ON oi.order_id=oin.order_id AND
        oi.product_id=oin.product_id;

        SELECT *
FROM order_items oi
JOIN order_item_notes oin
      USING(order_id,product_id);

```

**USING EXERCISE**

```
wheh i am using the USING CLAUSE I MUST
Make sure that the tables i am relation share
the same column name,Otherwise i must use ON

USE sql_invoicing;

SELECT
     p.date,
     c.name as client,
     p.amount
FROM payments p
JOIN clients c
     USING(client_id)
JOIN payment_methods pm
     ON pm.payment_method_id = p.payment_method

```

**NATURAL JOINS**

```
Easier to code but not recommended because it at times produces unexpected results.

IN a NATURAL JOin you do not have to manaully write the condition but the database
will examine which columns are similar on you behalf and do a JOIN for you.

USE sql_store;


SELECT
  o.order_id,
  c.first_name
FROM
orders o
NATURAL JOIN customers c


```

**CROSS JOINS**

```
We use a CROSS JOIN TO JOIN EVERY RECORD FROM THE FIRST TABLE TO EVERY RECORD IN THE SECOND TABLE

A cross Join therefore does not have a condition

It gives me a result with all the combnations for instance.


USE sql_store;

SELECT
  c.first_name AS customer,
  p.name AS product
FROM customers c
CROSS JOIN products p
ORDER BY c.first_name;

-- The above query will bring all the combinations
-- of customers with products
-- The above is the explicit syntax of a cross JOIN

-- WE MAY ALSO WRITE A JOIN IMPLICITLY AS SHOWN
-- BELOW WHICH IS NOT RECOMMENDED

SELECT
  c.first_name AS customer,
  p.name AS product
FROM customers c, products p
ORDER BY c.first_name

```

**CROSS JOIN EXERCISE**

```
-- Implicit cross JOIN (UNRECOMMEDNED)
SELECT
  sh.name as shipper,
  p.name as  product
FROM shippers sh, products p
ORDER BY sh.name;

-- expicit(Recommended)

SELECT
  sh.name as shipper,
  p.name as  product
 FROM shippers sh
CROSS JOIN products p
ORDER BY sh.name

```

**UNIONS**

```
JOINS HELP US COMBINE COLUMNS FROM MULTIPLE TABLES

UNIONS ON THE OTHER HAND HELP US COMBINE ROWS FROM MULTIPLE TABLES

THROUGH UNION OPERATOR WE ARE ABLE TO COMBINE RECORDS FROM MULTIPLE QUERIES
INTO ONE RESULT SET.


USE sql_store;

RESULT SET ONE

SELECT
    order_id,
    order_date,
    'Active' as status
FROM orders
WHERE order_date >='2019-01-01';


RESULT SET TWO

SELECT
    order_id,
    order_date,
    'Archived' as status
FROM orders
WHERE order_date <'2019-01-01';


A UNION COMES IN WHEN I WANT TO COMBINE DATA FROM TWO RESULT SETS

USE sql_store;

SELECT
    order_id,
    order_date,
    'Active' as status
FROM orders
WHERE order_date >='2019-01-01'
UNION
SELECT
    order_id,
    order_date,
    'Archived' as status
FROM orders
WHERE order_date <'2019-01-01';


We may as well combine data  from different tables into one result set.

N.B

FOR A UNION to work the number of rows returned by each query should
be the same otherwise MYSQL will not know how to combine this data.


The table columns name in returned from a union are the column
names of the first result set.

The second result set takes those names to the the names of their
columns.

I may therore rename the columns via an alias to make them agreeable to
my dataset


```

**EXERCISE**

```
UNIONS MOSTLY COMBINE DATA FROM A DIFFERENT RESULT SET.


-- <2000 points=bronze
-- 2000-3000-Silver
-- 3000 POINTS > GOLD CUSTOMERS

SELECT 
 customer_id,
 first_name,
 points,
 'Bronze' AS type
FROM customers 
WHERE points <2000
UNION
SELECT 
 customer_id,
 first_name,
 points,
 'Silver'
FROM customers 
WHERE points BETWEEN 2000 AND 3000
UNION
SELECT 
 customer_id,
 first_name,
 points,
 'Gold'
FROM customers 
WHERE points > 3000
ORDER BY first_name  ASC


```
