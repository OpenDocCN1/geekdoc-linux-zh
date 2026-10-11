The analogous DELETE statement to find and remove those rows from t1 uses a LEFT JOIN as well:
DELETE t1 FROM t1 LEFT JOIN t2 ON t1.id = t2.id WHERE t2.id IS NULL;

MySQL supports a second multiple-table DELETE syntax. With this syntax, use a FROM clause to list the tables from which rows are to be deleted and a USING clause to join the tables that determine which rows to delete. The preceding multiple-table DELETE statements can be rewritten using this syntax as follows:
DELETE FROM t1 USING t1 INNER JOIN t2 ON t1.id = t2.id;
DELETE FROM t1, t2 USING t1 INNER JOIN t2 ON t1.id = t2.id;
DELETE FROM t1 LEFT JOIN t2 ON t1.id = t2.id WHERE t2.id IS NULL;

The principles involved in writing multiple-table UPDATE statements are quite similar to those used for DELETE: Name all the tables that participate in the operation and qualify column references as necessary. Suppose that the quiz you gave on September 23, 2008, contained a question that everyone got wrong, and then you discover that the reason for this is that your answer key was incorrect. As a result, you want to add a point to every-one's score. With a multiple-table UPDATE, you can do this as follows:
UPDATE score, grade_event SET score.score = score.score + 1
WHERE score.event_id = grade_event.event_id
AND grade_event.date = '2008-09-23' AND grade_event.category = 'Q';
In this case, you could accomplish the same objective using a single-table update and a subquery:
UPDATE score SET score = score + 1
WHERE event_id = (SELECT event_id FROM grade_event
WHERE date = '2008-09-23' AND category = 'Q');
But other updates cannot be written using subqueries. For example, you might want to not only identify rows to update based on the contents of another table, but to copy column values from one table to another. The following statement copies t1.a to t2.a for rows that have a matching id column value:
UPDATE t1, t2 SET t2.a = t1.a WHERE t2.id = t1.id;
To perform multiple-table deletes or updates for InnoDB tables, you need not use the syntax just described. Instead set up a foreign key relationship between tables that includes an ON DELETE CASCADE or ON UPDATE CASCADE constraint. For details, see Section 2.14, “Foreign Keys and Referential Integrity.”

# ### 2.13 Performing Transactions

A transaction is a set of SQL statements that execute as a unit and that can be canceled if necessary. Either all the statements execute successfully, or none of them have any effect. This is achieved through the use of commit and rollback capabilities. If all of the state-ments in the transaction succeed, you commit it to record their effects permanently in the