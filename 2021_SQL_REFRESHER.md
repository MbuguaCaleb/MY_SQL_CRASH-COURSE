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

**Exercice**

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
