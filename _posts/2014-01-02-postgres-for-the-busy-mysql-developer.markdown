---
layout: post
title: "Postgres for the busy MySQL developer"
date: 2014-01-02 14:50
comments: true
categories: [PostgreSQL, Productivity, Databases]
---
For a new project I will be using PostgreSQL. I have more experience with MySQL at this point so I wanted to quickly learn about PostgreSQL and port over some of the skills I have.

## Roles
Permissions are managed with "roles". To see all roles, type `\du`. A Superuser is created that is the same as my login user. To see the privileges for all tables, run `\l`. Here is a [list of privileges](http://www.postgresql.org/docs/9.0/static/sql-grant.html).

## Working with rails
For a Rails application, create a `rails` role and make it the owner:

``` bash
createdb -O rails app_name_development
```

From a psql prompt, type `\list` to see all databases, and `\c database` to connect to a database by name. `\dt` will show all the tables.

If the rails user did not have create database privileges, there will be an error running `rake` in a rails project when the database is dropped. To add the permission to the rails user using psql:

``` sql
alter role rails createdb
```

To verify this role as added run the following query. A [role full list](http://www.postgresql.org/docs/9.1/static/sql-alterrole.html) is here.

``` sql
select rolcreatedb from pg_roles where rolname = 'rails';
 rolcreatedb
-------------
 t
```

## Working with CSV data
Like Mysql, Postgres supports loading data from, and dumping data to CSV files. The following example shows an example of working with CSV files with a simple `company_stuff` database and `customers` table. First we need to create the database, connect to it, and create the table.

``` sql
create database company_stuff;
\c company_stuff;
create table customers 
    (id serial not null primary key, 
    email varchar(100), 
    full_name varchar(100)); 
```

Type `\d customers` to verify the table is set up correctly.

Now assuming we have the same CSV text file from the previous article when I covered how to work with CSV files using MySQL, we can load it into postgres using the `copy` command. This example specifies the column names, and note that the primary key column value is populated automatically.

``` bash
% cat customers.txt
bob@example.com,Bob Johnson
jane@example.com,Jane Doe
```

``` sql
copy customers(email, full_name) 
from '/tmp/customers.txt' 
delimiter ',' CSV;
```

Verify the contents of the customers table.

``` sql
select * from customers;
 id |      email       |  full_name
----+------------------+--------------
  1 | bob@example.com  |  Bob Johnson
  2 | jane@example.com |  Jane Doe
```

Now we can insert a new record, then dump all the records out again as new CSV file.

``` sql
copy customers(email, full_name) 
to '/tmp/more_customers.csv' 
with delimiter ',';
```

Verify the output of the CSV file:

``` bash
~ $ cat /tmp/more_customers.csv
bob@example.com, Bob Johnson
jane@example.com, Jane Doe
andy@example.com,andy
```

# Running one-off queries
Running a query from the command line then combining it with `grep` or other command line tools is very useful. Here is quick search in the "customers" database for columns named something like "email", using grep:

``` bash
~ $ psql -U andy -d company_stuff -c "\d customers" | grep email
     email     | character varying(100) |
```

## More Mysql to Postgres articles
 * [Useful guide on equivalent commands in postgres from mysql](http://granjow.net/postgresql.html)
 * [PostgreSQL quick start for people who know MySQL](http://clarkdave.net/2012/08/postgres-quick-start-for-people-who-know-mysql/)
 * [PostgreSQL for MySQL users](http://www.coderholic.com/postgresql-for-mysql-users/)
 * [How To Use Roles and Manage Grant Permissions in PostgreSQL on a VPS](https://www.digitalocean.com/community/articles/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps--2)
