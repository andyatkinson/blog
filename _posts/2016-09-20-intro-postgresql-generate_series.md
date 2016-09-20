---
layout: post
title: "Intro to PostgreSQL generate_series"
date: 2016-09-20 17:00
comments: true
categories: [SQL, Tips]
---


For a recent project, we wanted to efficiently present a week's worth of data, grouped by day, from a data structure where we have rows of hourly summarized data.

The solution was to use the [generate_series](https://www.postgresql.org/docs/8.0/static/functions-srf.html) function in PostgreSQL, with a step value of 1 day, then do a `LEFT OUTER JOIN` to the hourly data, grouping by day, and finally doing a `sum` on the day's values. The outer join gives us summarized data by day, whether there were earnings that day or not.

The output we wanted looked like this:

``` bash
    date    |  sum
------------+-------
 2016-09-20 | 148.3
 2016-09-21 | 112.6
 2016-09-22 |
```

#### Basic series example

Let's say you wanted to to look at a couple of days worth of data, from today, until 1 day from now. The syntax for a series that would express that could look like this:

``` sql
select * from generate_series(now()::date, now()::date + interval '1 day', '1 day')                                                                                                                            ;
   generate_series
---------------------
 2016-09-01 00:00:00
 2016-09-02 00:00:00
```

#### Real-world usage example

To better understand how things are working, let's set up a table and some rows of data, as a simplified version of the real-world usage mentioned above.

In this example, we'll have a table that summarizes earnings for each employee, by hour. We can put this into a test database.

``` sql
CREATE DATABASE test_db;

CREATE TABLE earnings (employee_id integer NOT NULL, hour timestamp NOT NULL, total numeric NOT NULL);
```

Let's insert some records for employee "1". This employee earned some money on September 20 and 21, but none on the 22nd.

``` sql
insert into earnings (employee_id, hour, total) VALUES (1, '2016-09-20 08:00:00', 25.0);
insert into earnings (employee_id, hour, total) VALUES (1, '2016-09-20 09:00:00', 70.3);
insert into earnings (employee_id, hour, total) VALUES (1, '2016-09-20 10:00:00', 53.0);

insert into earnings (employee_id, hour, total) VALUES (1, '2016-09-21 08:00:00', 11.5);
insert into earnings (employee_id, hour, total) VALUES (1, '2016-09-21 09:00:00', 39.7);
insert into earnings (employee_id, hour, total) VALUES (1, '2016-09-21 10:00:00', 61.4);
```

Now that the data is in place, we can extract the date part of each record, and group on that, then `SUM()` the total for each date.

``` sql
SELECT to_char(hour, 'YYYY-MM-DD') as day, sum(total)
FROM earnings
GROUP BY day
ORDER BY day ASC;
    day     |  sum
------------+-------
 2016-09-20 | 148.3
 2016-09-21 | 112.6
```

What if we want to include extra days in the query result though, like September 22? We don't have earnings on those days. That's where `generate_series` comes in!

Let's imagine a user wanted to see earnings from September 20 to 22. Putting everything together, we generate a series with a step value of 1 day, for those start and end dates. We then do a left outer join on the earnings table by date, which allows us to see the earnings for days where we have data, and an empty value where we don't.


``` sql
SELECT
    series.date,
    sum(e.total)

FROM (
    select to_char(day, 'YYYY-MM-DD') as date FROM
    generate_series('2016-09-20'::date, '2016-09-22'::date, '1 day') as day
) series

LEFT OUTER JOIN (
    SELECT * from earnings
    WHERE hour >= '2016-09-20' AND hour <= '2016-09-22') AS e
    ON (series.date = to_char(e.hour, 'YYYY-MM-DD')
)

GROUP BY series.date
ORDER BY series.date;
```


The result should look like this.


``` bash
    date    |  sum
------------+-------
 2016-09-20 | 148.3
 2016-09-21 | 112.6
 2016-09-22 |
```

Thanks for checking this out!