
- The trigger automatically provides a value of `CURRENT_TIMESTAMP` for the DATETIME column. In effect, this works around the limitation that a column's default value must be a constant, and implements TIMESTAMP-like automatic initialization for a DATETIME column.

To see how the trigger works, insert some rows into the table, and then retrieve its contents:

```text
mysql> INSERT INTO t (percent) VALUES(-2); DO SLEEP(2);
mysql> INSERT INTO t (percent) VALUES(30); DO SLEEP(2);
mysql> INSERT INTO t (percent) VALUES(120);
mysql> SELECT * FROM t;
+ -------+---------------------+
| percent |        dt           |
+ -------+---------------------+
|       0 | 2008-05-15 18:38:22 |
|      30 | 2008-05-15 18:38:24 |
|     100 | 2008-05-15 18:38:26 |
+ -------+---------------------+
```

The privilege required to create and drop triggers is version-specific. Before MySQL 5.1.6, you must have the `SUPER` privilege. As of MySQL 5.1.6, access control is more correctly handled: Because a trigger is associated with a table, you must have the `TRIGGER` privilege for that table to be able to create and drop triggers for it.

## 4.4 Events

MySQL 5.1.6 and up has an event scheduler that enables you to perform time-activated database operations. An event is a stored program that is associated with a schedule. The schedule defines the time or times at which the event executes, and optionally when the event ceases to exist. Events are especially useful for performing unattended administrative operations such as periodic updates to summary reports, expiration of old data, or log table rotation. This section demonstrates row expiration. For an example that shows how to perform event-based log table rotation, see Section 12.5.7.4, “Expiring or Rotating Log Tables.”

The event scheduler does not run by default, so you must turn it on if you want to use events. Put the following lines in an option file that the server reads at startup:

```ini
[mysqld]
event_scheduler=ON
```

To check the status of the event scheduler at runtime, use this statement:

```sql
SHOW VARIABLES LIKE 'event_scheduler';
```

To stop or start the scheduler at runtime, change the value of the `event_scheduler` system variable (it is a GLOBAL variable, so you must have the `SUPER` privilege):

If you stop the scheduler, no events run. It is also possible to leave the scheduler running but disable individual events, as discussed later.

# Note

> If you set `event_scheduler` to `DISABLED` at startup, you can check but not change its status at runtime. Also, you can create events, but they will not execute.

The event scheduler writes to the server's error log, which you can check for information about what the scheduler is doing. It logs events as it runs them, as well as errors that occur during event execution. If the event scheduler is not running when you expect it to be, check the error log for a message that indicates the reason why.

The following example shows how to create a simple event that deletes old rows from a table. Suppose that you have a table named `web_session` that holds state information for sessions associated with users who visit your Web site, and that this table has a `DATETIME` column named `last_visit` that indicates the time of each user's most recent visit. To keep this table from accumulating stale rows, you can set up an event that periodically purges them. To execute the event every six hours and have it expire rows more than a day old, write the event definition like this:

```sql
CREATE EVENT expire_web_session
ON SCHEDULE EVERY 4 HOUR
DO
   DELETE FROM web_session
   WHERE last_visit < CURRENT_TIMESTAMP - INTERVAL 1 DAY;
```

The `EVERY n interval` clause specifies periodic execution at fixed intervals. The `interval` values are like those used for the `ADD_DATE()` function, such as `HOUR`, `DAY`, or `MONTH`. Following `EVERY`, you can also include `STARTS datetime` and `ENDS datetime` options that specify the initial and final execution time. By default, an `EVERY` event runs for the first time immediately after it is created and has no final time.

The `DO` clause defines the event body, which is an `SQL` statement that executes when the event runs. As for other stored program types, this can be a simple statement or a compound statement written using `BEGIN` and `END`.

To create an event that runs only one time, use the `AT` scheduling type rather than `EVERY`. A definition such as the following creates an event that executes once, an hour in the future:

```sql
CREATE EVENT one_shot
ON SCHEDULE AT CURRENT_TIMESTAMP + INTERVAL 1 HOUR
DO ...;
```

To disable an event to stop it from executing, or to re-enable a disabled event, use:

```sql
ALTER EVENT event_name DISABLE;
ALTER EVENT event_name ENABLE;
```

An event belongs to a database, so you must have the EVENT privilege for that database to create or drop events for it.

## 4.5 Security for Stored Programs and Views

When you create a stored program, you create an object that is to be executed later. The same is true when you define a view: It sets up a SELECT statement intended for later invocation. This “execute later” aspect of such objects means that the user who causes object execution might not be the user who originally created it, which raises an important question: What security context should the server use for checking access privileges at execution time? That is, which account’s privileges should apply?

By default, the server uses the account of the user who defined the object. Suppose that I define a stored procedure p() that accesses tables belonging to me. If I give you the execute privilege for p(), you can say call p() to invoke the procedure and it will access my tables on your behalf because it runs with my privileges. This type of security context can be good or bad:

- It’s good in the sense that it enables carefully written stored programs to be set up that provide controlled access to tables for users who are not able to access them directly.
- It’s bad if a user creates a stored program that accesses sensitive data but forgets that other people who can invoke the object have the same access to that data as its definer.

The definer for a stored program or view can be specified explicitly by including a definer = account clause in the CREATE statement for the object. This causes the named account to be treated as the definer for purposes of access checking at execution time. For example:

```sql
CREATE DEFINER = 'sampadm'@'localhost' PROCEDURE count_students()
SELECT COUNT(*) FROM student;
```

In a definer clause, the definer value can be an account name in ‘user_name’@‘host_name’ format as used in account-management statements such as CREATE USER. (See Section 12.4.1.1, “Specifying Account Names.”) For this format, user_name and host_name must both be given. Alternatively, the value can be current_user or current_user() to indicate the account of the user who executes the statement (the same account that is used by default if no definer clause is present).

If you have the SUPER privilege, you can give any syntactically legal account name as the definer value; a warning occurs if the account does not exist at the time. If you do not have the SUPER privilege, you can set the definer only to your own account, using either the literal account name or current_user.

For views and stored functions and procedures, you can specify the SQL SECURITY characteristic, which gives you an additional means of control over execution time access-checking. SQL SECURITY takes a value of definer (execute with the definer’s privileges) or invoker (execute with the privileges of the user who invoked the object).

SQL SECURITY INVOKER is preferable for situations when you don’t want a stored program or view to execute with any more privileges than a user already has. The following view accesses a table in the mysql database, but runs with invoker privileges. That way, if the invoker has no access to mysql.user, the view won’t subvert that restriction.

```sql
CREATE SQL SECURITY INVOKER VIEW v
   AS SELECT CONCAT(User, '@',Host) AS Account, Password FROM mysql.user;
```

Triggers and events are invoked automatically by the server, so the concept of “invoking user” does not apply. Thus, they have no SQL SECURITY characteristic and always execute with definer privileges.

If a stored program or view runs with definer privileges at execution time and the definer account does not exist, an error occurs.
