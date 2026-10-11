+   2.  Salesman B sells two shirts and the register software decrements the shirt count
+   by two:
+   
+       `UPDATE inventory SET quantity = quantity - 2 WHERE item = 'shirt';`
+   
+   With this method, each modification to the database no longer requires multiple state-
+   ments. This eliminates concurrency issues, so there is no need to use explicit table locks. If
+   an operation you want to perform is similar to this, there may be no need for transactions
+   at all.
+   
+   The non-transactional approaches just described can be applied successfully to many
+   types of problems, but they have certain limitations:
+   
+   *   Not every operation can be written in terms of relative updates. Sometimes you
+       must use multiple statements, in which case concurrency issues must be considered
+       and dealt with.
+   *   You may be able to keep clients from interfering with each other by locking tables
+       for the duration of a multiple-statement operation, but what happens if an error oc-
+       curs in the middle of the operation? In this case, you’d want the effects of the earlier
+       statements to be undone so that the database isn’t left in a half-modified and incon-
+       sistent state. Unfortunately, although table locking can help you address concurrency
+       issues, non-transactional tables provide no assistance in recovering from errors.
+   *   The locking strategy requires you to lock and unlock tables yourself. If you
+       revise an operation in such a way that changes the set of tables used, you must
+       remember to modify the `LOCK TABLES` statement accordingly.

If any of these issues are significant for your applications, you should use transaction-
safe tables instead, because transactional capabilities help you deal with each issue. A trans-
action handler executes a set of statements as a unit and manages concurrency issues by
preventing clients from getting in the way of each other. It also enables rollback in the
case of failure to keep half-executed operations from damaging your database, and it de-
termine which locks are necessary and acquires them automatically.

> Can You Mix Transactional and Non-Transactional Tables?
> It is possible to use both transactional and non-transactional tables during the course of a
> transaction, but the result might not be what you expect. Statements for non-transactional
> tables always take effect immediately, even when autocommit is disabled. In effect, non-
> transactional tables are always in autocommit mode and each statement commits immedi-
> ately. As a result, if you change a non-transactional table within a transaction and then
> attempt a rollback, the non-transactional table changes cannot be undone.

# 2.14 Foreign Keys and Referential Integrity

A foreign key relationship enables you to declare that an index in one table is related to
an index in another. It also enables you to place constraints on what may be done to the
tables in the relationship. The database enforces the rules of this relationship to maintain