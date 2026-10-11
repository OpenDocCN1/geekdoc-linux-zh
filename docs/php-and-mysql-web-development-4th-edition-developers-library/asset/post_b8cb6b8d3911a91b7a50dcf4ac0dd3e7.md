
## 2.12 Multiple-Table Deletes and Updates

Sometimes it’s useful to delete rows based on whether they match or don’t match rows in another table. Similarly, it’s often useful to update rows in one table using the contents of rows in another table. This section describes how to perform multiple-table DELETE and UPDATE operations. These types of statements draw heavily on the concepts used for joins, so be sure you’re familiar with the material discussed earlier in Section 2.8, “Performing Multiple-Table Retrievals with Joins.”

To perform a single-table DELETE or UPDATE, you refer only to the columns of one table and thus need not qualify the column names with the table name. For example, to delete all rows in a table t that have id values greater than 100, you’d write a statement like this:

```sql
DELETE FROM t WHERE id > 100;
```

But what if you want to delete rows based not on properties inherent in the rows themselves, but rather on their relationship to rows in another table? Suppose that you want to delete from t those rows with id values that are found in another table t2?

To write a multiple-table DELETE, name all the tables in a FROM clause and specify the conditions used to match rows in the tables in the WHERE clause. The following statement deletes rows from table t1 where there is a matching id value in table t2:

```sql
DELETE t1 FROM t1 INNER JOIN t2 ON t1.id = t2.id;
```

Notice that if a column name appears in more than one of the tables, it becomes ambiguous and must be qualified with a table name.

The syntax also allows for deleting rows from multiple tables at once. To delete rows from both tables where there are matching id values, name them both after the DELETE keyword:

```sql
DELETE t1, t2 FROM t1 INNER JOIN t2 ON t1.id = t2.id;
```

What if you want to delete non-matching rows? A multiple-table DELETE can use any kind of join that you can write in a SELECT, so employ the same strategy that you’d use when writing a SELECT that identifies the non-matching rows. That is, use a LEFT JOIN or RIGHT JOIN. For example, to identify rows in t1 that have no match in t2, you’d write a SELECT like this:

```sql
SELECT t1.* FROM t1 LEFT JOIN t2 ON t1.id = t2.id WHERE t2.id IS NULL;
```

The analogous DELETE statement to find and remove those rows from t1 uses a LEFT JOIN as well:

```sql
DELETE t1 FROM t1 LEFT JOIN t2 ON t1.id = t2.id WHERE t2.id IS NULL;
```

MySQL supports a second multiple-table DELETE syntax. With this syntax, use a FROM clause to list the tables from which rows are to be deleted and a USING clause to join the tables that determine which rows to delete. The preceding multiple-table DELETE statements can be rewritten using this syntax as follows:

```sql
DELETE FROM t1 USING t1 INNER JOIN t2 ON t1.id = t2.id;
DELETE FROM t1, t2 USING t1 INNER JOIN t2 ON t1.id = t2.id;
DELETE FROM t1 LEFT JOIN t2 ON t1.id = t2.id WHERE t2.id IS NULL;
```

The principles involved in writing multiple-table UPDATE statements are quite similar to those used for DELETE: Name all the tables that participate in the operation and qualify column references as necessary. Suppose that the quiz you gave on September 23, 2008, contained a question that everyone got wrong, and then you discover that the reason for this is that your answer key was incorrect. As a result, you want to add a point to every-one's score. With a multiple-table UPDATE, you can do this as follows:

```sql
UPDATE score, grade_event SET score.score = score.score + 1
WHERE score.event_id = grade_event.event_id
AND grade_event.date = '2008-09-23' AND grade_event.category = 'Q';
```

In this case, you could accomplish the same objective using a single-table update and a subquery:

```sql
UPDATE score SET score = score + 1
WHERE event_id = (SELECT event_id FROM grade_event
WHERE date = '2008-09-23' AND category = 'Q');
```

But other updates cannot be written using subqueries. For example, you might want to not only identify rows to update based on the contents of another table, but to copy column values from one table to another. The following statement copies t1.a to t2.a for rows that have a matching id column value:

```sql
UPDATE t1, t2 SET t2.a = t1.a WHERE t2.id = t1.id;
```

To perform multiple-table deletes or updates for InnoDB tables, you need not use the syntax just described. Instead set up a foreign key relationship between tables that includes an ON DELETE CASCADE or ON UPDATE CASCADE constraint. For details, see Section 2.14, “Foreign Keys and Referential Integrity.”

## 2.13 Performing Transactions

A transaction is a set of SQL statements that execute as a unit and that can be canceled if necessary. Either all the statements execute successfully, or none of them have any effect. This is achieved through the use of commit and rollback capabilities. If all of the statements in the transaction succeed, you commit it to record their effects permanently in the database. If an error occurs during the transaction, you roll it back to cancel it. Any statements executed up to that point within the transaction are undone, leaving the database in the state it was in prior to the point at which the transaction began.

Commit and rollback provide the means for ensuring that halfway-done operations don’t make their way into your database and leave it in a partially updated (inconsistent) state. The canonical example of this involves a financial transfer where money from one account is placed onto another account. Suppose that Bill writes a check to Bob for $100.00 and Bob cashes the check. Bill’s account should be decremented by $100.00 and Bob’s account incremented by the same amount:

```sql
UPDATE account SET balance = balance - 100 WHERE name = 'Bill';
UPDATE account SET balance = balance + 100 WHERE name = 'Bob';
```

If a crash occurs between the two statements, the operation is incomplete. Depending on which statement executes first, Bill is $100 short without Bob having been credited, or Bob is given $100 without Bill having been debited. Neither outcome is correct. If transactional capabilities are not available to you, you have to figure out the state of ongoing operations at crash time by examining your logs manually in order to determine how to undo them or complete them. The rollback capabilities of transaction support enable you to handle this situation properly by undoing the effect of the statements that executed before the error occurred. (You may still have to determine which transactions weren’t entered and re-issue them, but at least you don’t have to worry about half-transactions making your database inconsistent.)

Another use for transactions is to make sure that the rows involved in an operation are not modified by other clients while you’re working with them. MySQL automatically performs locking for single SQL statements to keep clients from interfering with each other, but this is not always sufficient to guarantee that a database operation achieves its intended result, because some operations are performed over the course of several statements. In this case, different clients might interfere with each other. A transaction groups statements into a single execution unit to prevent concurrency problems that could otherwise occur in a multi-client environment.

Transactional systems typically are characterized as providing ACID properties. ACID is an acronym for Atomic, Consistent, Isolated, and Durable, referring to four properties that transactions should have:

- **Atomicity**: The statements a transaction consists of form a logical unit. You can’t have just some of them execute.
- **Consistency**: The database is consistent before and after the transaction executes. In other words, the transaction doesn’t make a mess of your database.
- **Isolation**: One transaction has no effect on another.
- **Durability**: When a transaction executes successfully to completion, its effects are recorded permanently in the database.

Transactional processing provides stronger guarantees about the outcome of database operations, but also requires more overhead in CPU cycles, memory, and disk space.
