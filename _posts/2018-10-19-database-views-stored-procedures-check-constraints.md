---
layout: post
title: "A Quick Look at Views, Stored Procedures, and Check Constraints"
date: 2018-10-19 13:00
comments: true
categories: [Databases]
---

This post will take a quick look at views, stored procedures, and check constraints. What are they and what are their use cases? This post is specific to PostgreSQL.

#### Database Views

A database view is kind of a virtual table, based on a `SELECT` query to an existing table. How are they used? One use case would be when a particular user only needs read only access to a subset of rows in a table. This would be achieved by creating a view, and then granting only that permission to that user (role).

##### Basic View Example

For a quick demonstration, we'll put together a table for storing earnings by hour. Each earnings record belongs to an employee. We'll insert some records with `employee_id` values between 1 and 5. We'll call the employees with IDs of 3 or less "special". [Views are currently read only](https://www.postgresql.org/docs/9.2/static/sql-createview.html).

```
test# insert into earnings (employee_id, hour, total) VALUES (1, date_trunc('hour', now()), 10);
test# insert into earnings (employee_id, hour, total) VALUES (1, date_trunc('hour', now() + interval '1 hour'), 10);
...
(insert some more and change the ID)
```

Now we'll create the view for the special employees. The view will be called `special_employee_earnings` and it limits the results using a SELECT query against the earnings table.

```sql
CREATE VIEW special_employee_earnings AS SELECT * from earnings where employee_id <= 3;
```


#### Stored Procedures

> "The stored procedures define functions for creating triggers or custom aggregate functions." [article](http://www.postgresqltutorial.com/introduction-to-postgresql-stored-procedures/) PL/pgSQL is a safe choice. One of the advantages is re-use across various applications (by moving logic to the database) as well as performance by having the logic execute in the database as opposed to the application layer.

Stored procedures are functions to use with data, within queries. I made a repo called [db-stuff](https://github.com/andyatkinson/db-stuff) with like `get_sum(a,b)` from the [Stored Procedures Tutorial](http://www.postgresqltutorial.com/postgresql-stored-procedures/).

Why have these in the database versus an application? As the quote above indicates, perhaps it's useful to share this function across applications, potentially with a variety of programming language stacks.


#### Check constraints

Check constraints are a way to do some data validations.

A check constraint might be part of a column definition. The [documentation](https://www.postgresql.org/docs/9.4/static/ddl-constraints.html) has an example for a `price` column  of `numeric` type, where we want to check that the price is greater than zero.

```
CREATE TABLE products (
    price numeric CHECK (price > 0)
);
```

Violating this constraint produces a descriptive error message:

```
INSERT INTO PRODUCTS (price) VALUES (-1);
ERROR:  new row for relation "products" violates check constraint "products_price_check"
DETAIL:  Failing row contains (-1).
```
