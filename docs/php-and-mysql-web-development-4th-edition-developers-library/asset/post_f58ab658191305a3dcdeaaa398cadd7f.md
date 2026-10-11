
This chapter uses the following terminology:

- **“Stored programs”** refers collectively to stored objects of all types (functions, procedures, triggers, and events).

- **“Stored routines”** is a more limited term that refers only to stored functions and procedures. Both types of objects are defined using very similar syntax, so it is often natural to discuss them together. In fact, the term “stored procedures” is frequently used to refer both to procedures and functions. However, I find this unhelpfully ambiguous and will not use the term that way.

Later sections in this chapter discuss how to write and use each type of stored program. However, before getting into the details of any particular type of stored program, we’ll begin with a discussion of an issue common to all of them: how to write compound statements.

## 4.1 Compound Statements and Statement Delimiters

A simple stored program that has a body consisting of a single SQL statement can be written without any special treatment. The following procedure uses a `SELECT` statement that displays the names of the tables in the `sampdb` database:

```sql
CREATE PROCEDURE sampdb_tables ()
  SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_SCHEMA = 'sampdb'
    ORDER BY TABLE_NAME;
```

However, a stored program need not be limited to a single simple statement. The code can contain multiple SQL statements, and it can use constructs such as local variables, conditional statements, loops, and nested blocks. To write a stored program that uses these features, use a compound statement, which consists of `BEGIN` and `END` to form a block within which an arbitrary number of statements can be written. The following procedure displays a greeting with your username, or “earthing” if you are an anonymous user:

```sql
CREATE PROCEDURE greetings ()
BEGIN
  # 77 = 16 for username + 60 for hostname + 1 for '@'
  DECLARE user CHAR(77) CHARACTER SET utf8;
  SET user = (SELECT CURRENT_USER());
  IF INSTR(user,'@') > 0 THEN
    SET user = SUBSTRING_INDEX(user,'@',1);
  END IF;
  IF user = '' THEN       # anonymous user
    SET user = 'earthing';
  END IF;
  SELECT CONCAT('Greetings, ',user, '!') AS greeting;
END;
```

An issue that arises in the use of compound statements is that the statements within a block must be separated semicolon (`;`) characters as delimiters. That also is the default statement delimiter for the **mysql** program, so there is a conflict if you try to define stored programs using **mysql**. To deal with this, use the **delimiter** command to redefine **mysql**'s statement delimiter to a character or string that does not appear in the routine definition. That causes **mysql** not to interpret semicolons as terminators and to pass the entire object definition to the server as a single statement. You can redefine the terminator to semi-colon again after defining the stored program. The following example temporarily changes the **mysql** delimiter to $ while a stored procedure is being defined, and then executes the procedure after restoring the default delimiter:

```sql
mysql> delimiter $
mysql> CREATE PROCEDURE show_times()
   -> BEGIN
   ->  SELECT 'Local time is:', CURRENT_TIMESTAMP;
   ->  SELECT 'UTC time is:', UTC_TIMESTAMP;
   -> END$
mysql> delimiter ;
mysql> CALL show_times();
+----------------+-------------------------+
| Local time is: | CURRENT_TIMESTAMP   |
+----------------+-------------------------+
| Local time is: | 2008-05-15 18:20:13  |
+----------------+-------------------------+
| UTC time is: | UTC_TIMESTAMP   |
+----------------+-------------------------+
| UTC time is: | 2008-05-15 23:20:13  |
+----------------+-------------------------+
```

The delimiter need not be $, and it need not be a single character:

```sql
mysql> delimiter EOF
mysql> CREATE PROCEDURE show_times()
   -> BEGIN
   ->  SELECT 'Local time is:', CURRENT_TIMESTAMP;
   ->  SELECT 'UTC time is:', UTC_TIMESTAMP;
   -> END EOF
mysql> delimiter ;
```

The principle to keep in mind is this: If a stored program's body contains any internal semicolons, you should redefine the delimiter while defining the program.

A compound statement need not be used only for complex stored programs. You can use one even if a program body consists of a single statement, or even no statements:

```sql
CREATE PROCEDURE do_little ()
BEGIN
    DO SLEEP(1);
END;

CREATE PROCEDURE do_nothing ()
BEGIN
END;
```

For stylistic consistency, you might prefer to use `BEGIN` and `END` for all stored program definitions.

## 4.2 Stored Functions and Procedures

Stored functions calculate a value to be returned to the caller for use in expressions, just like built-in functions such as `COS( )` or `HEX( )`. Stored procedures are executed as stand-alone operations using the `CALL` statement rather than in expressions. Use a procedure if you need only to perform a computation to produce an effect or action without returning a value, or if the computation produces result sets (which a function is not allowed to do). These are guidelines, not hard and fast rules. For example, if you need to return more than one value, you cannot use a function. But you may be able to use a procedure, because procedures support parameter types that can have their values set when the procedure executes, such that those values can be accessed by the caller after the procedure finishes.

To create a stored function or procedure, use a `CREATE FUNCTION` or `CREATE PROCEDURE` statement. The following example creates a function that takes an integer-valued parameter representing a year. (Use `p_` as a prefix to distinguish parameter names from other names such as those of tables or columns.) The function uses a subquery to determine how many presidents were born in that year and returns the count:

```sql
mysql> delimiter $
mysql> CREATE FUNCTION count_born_in_year(p_year INT)
      -> RETURNS INT
      -> READS SQL DATA
      -> BEGIN
      ->   RETURN (SELECT COUNT(*) FROM president WHERE YEAR(birth) = p_year);
      -> END$
mysql> delimiter ;
```

The function has a `RETURNS` clause to indicate the data type of its return value and a body that computes that value. The function body must include at least one `RETURN` statement to return a value to the caller. By defining a calculation as a function, you have a simple way to execute it without specifying all the logic each time, and it can be invoked just like a built-in function:

```sql
mysql> SELECT count_born_in_year(1908);
+------------------------+
| count_born_in_year(1908) |
+------------------------+
|                        1 |
+------------------------+
mysql> SELECT count_born_in_year(1913);
+-------------------------+
| count_born_in_year(1913) |
+-------------------------+
|                       2 |
+-------------------------+
```

Here, the function is invoked by itself, but stored functions can be used within arbitrarily complex expressions.

You cannot return multiple values from a given function. You could write multiple functions and invoke them all from within a single statement, but another approach is to use a stored procedure that "returns" values via OUT parameters. The procedure should compute the desired values and assign them to the parameters, which then can be accessed by the caller after the procedure returns. For details, see Section 4.2.2, “Stored Procedure Parameter Types.”

If you define a stored function with the same name as a built-in function, you should qualify the function name with the database name when you invoke it. For example, if you define a stored function named PI() in the sampledb database, invoke it as sampledb.PI() to make clear that you do not mean the built-in function. (To avoid this ambiguity, it's best not to use names of built-in functions.)

A stored procedure is similar to a stored function, but it doesn't return a value. Therefore, it does not have a RETURNS clause or any RETURN statements. The following simple stored procedure is similar to the count_born_in_year() function, but instead of calculating a count as a return value, it displays a result set containing a row of information for each president born in the given year.

```sql
mysql> DELIMITER $
mysql> CREATE PROCEDURE show_born_in_year(p_year INT)
    -> BEGIN
    ->   SELECT first_name, last_name, birth, death
    ->     FROM president
    ->     WHERE YEAR(birth) = p_year;
    -> END$
mysql> DELIMITER ;
```

Unlike stored functions, stored procedures are not used in expressions. They are invoked using the CALL statement:

```sql
mysql> CALL show_born_in_year(1908);
+----------+----------+------------+------------+
| first_name | last_name | birth      | death      |
+----------+----------+------------+------------+
| Lyndon B. | Johnson  | 1908-08-27 | 1973-01-22 |
+----------+----------+------------+------------+
mysql> CALL show_born_in_year(1913);
+----------+----------+------------+------------+
| first_name | last_name | birth      | death      |
+----------+----------+------------+------------+
```
