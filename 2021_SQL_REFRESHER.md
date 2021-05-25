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
