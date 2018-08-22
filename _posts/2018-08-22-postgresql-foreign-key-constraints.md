---
layout: post
title: "A look at PostgreSQL Foreign Key Constraints"
date: 2018-08-22 13:00
comments: true
categories: [Database, SQL]
---

Foreign key constraints enforce that a referenced thing exists on a table it is referencing.

These can be browsed under `Foreign-key constraints` with a `REFERENCES` indicating the local and referenced table, or it can also show up on the column-level when the referenced table has a primary key.

Constraints are not deferrable by default. From my investigation, deferring constraint enforcement seems mainly useful within transactions. Constraints can be set as deferrable per transaction as long as the deferrable attribute was originally specified, i.e. `deferrable initially immediate`.

A foreign key constraint may be altered later with [ALTER CONSTRAINT](https://www.postgresql.org/docs/9.4/static/sql-altertable.html) although to change this behavior with other constraints, I believe the constraint would need to be removed and then added again with the deferrable attribute set.

#### SET CONSTRAINTS

> SET CONSTRAINTS sets the behavior of constraint checking within the current transaction.

[SET CONSTRAINTS docs](https://www.postgresql.org/docs/9.1/static/sql-set-constraints.html)

Immediate constraints are checked after each statement while deferred constraints are not checked until the transaction commits.

For example, within one transaction, there may be be multiple `INSERT` statements. The author has the choice to have constraints like uniqueness, enforced after every statement, or deferred until the end of the statements, when the transaction will be committed.


*Why would the difference be significant?*

This excellent [Hashrocket blog post on deferring constraints](https://hashrocket.com/blog/posts/deferring-database-constraints) goes in depth into an example with a list where each list item has a unique position.

To briefly summarize the article, when re-ordering a list of items where each re-order generates a an update statement per list item within a transaction, two list items would have the same position value at a certain point in execution. This would break because it would violate the uniqueness constraint. The solution was to defer enforcement of the unique constraint until the end of the transaction where each list item has a new position value.

If a transaction is deferrable, it can have 3 classes. The class of deferred constraint the project I'm working on used `DEFERRABLE INITIALLY DEFERRED`, which is not the default, which is that enforcement is not deferred.

Specifying deferrable this way would be more surprising than `INITIALLY IMMEDIATE` which would be the default. For that reason it makes sense as a default either to not specify deferrable, or to specify deferrable initially immediate, to preserve the default behavior, but allow an individual transaction to opt in to the deferred behavior (this was the recommendation from the Hashrocket article that I agree with and am echoing here).

#### ON DELETE and ON UPDATE

Another attribute to specify on foreign key constraints is how to handle when deletes or updates happen on referenced data. The [Postgres constraints documentation](https://www.postgresql.org/docs/9.5/static/ddl-constraints.html) has an example with products, orders, and order items that is helpful.

For example, `ON DELETE RESTRICT` restricts deleting a product that an order item references.

`NO ACTION` is the default behavior when no nothing is specified. `NO ACTION` allows the check to be deferred until later in the transaction. However, specifying `RESTRICT` as an initial setting makes sense to me, as a safeguard from deleting rows unintentionally.

In the event, the cascade delete is desired, the constraint could be modified later.


#### Summary

 * Foreign key constraints ensure data in a referenced table exists
 * Enforcement of constraints can be applied per statement in a batch of statements within a transaction, or deferred until the transaction commits
 * Deletes or updates on referenced tables can be propagated or restricted

