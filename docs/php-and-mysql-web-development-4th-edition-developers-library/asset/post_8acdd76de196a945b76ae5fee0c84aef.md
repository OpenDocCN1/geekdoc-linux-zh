
## E.2.1 Control-Flow Statements

The **BEGIN** ... **END** construct creates a block within which multiple statements can be grouped. If a stored program body needs to contain more than one statement, they must be grouped within a **BEGIN** block. Also, if the program contains any **DECLARE** statements, they can appear only at the beginning of a **BEGIN** block.

### CASE

```sql
CASE [expr]
    WHEN expr1 THEN stmt_list1
    [WHEN expr2 THEN stmt_list2] ...
    [ELSE stmt_list]
END IF
```

The **CASE** statement provides a branching flow–control construct. When the initial expression, `expr`, is present, **CASE** compares it to the expression following each **WHEN**. For the first one that is equal, the statement list for the corresponding **THEN** value is executed. This is useful for comparing a given value to a set of values.

When the initial expression, `expr`, is not present, **CASE** evaluates **WHEN** expressions. For the first one that is true, the statement list for the corresponding **THEN** value is executed. This is useful for performing non–equality tests or testing arbitrary conditions.

If no **WHEN** expression matches, the statement list for the **ELSE** clause is executed, if there is one.

Note that the **CASE** statement differs from the **CASE** operator described in Section C.2.1, “Comparison Functions.”

### IF

```sql
IF expr1 THEN stmt_list1
    [ELSIF expr2 THEN stmt_list2] ...
    [ELSE stmt_list]
END IF
```

The **IF** statement provides a branching flow–control construct. If the expression following the **IF** keyword is true, the statement list following the initial **THEN** is executed. Otherwise, expressions for any following **ELSIF** clauses are evaluated. For the first one that is true, the corresponding statement list is executed. If no expression is true, the statement list for the **ELSE** clause is executed, if there is one.

Note that the **IF** statement differs from the `IF()` function described in Section C.2.1, “Comparison Functions.”

### ITERATE

```sql
ITERATE label
```

The **ITERATE** statement is used within looping constructs to begin the next iteration of the loop. It can appear within **LOOP**, **REPEAT**, and **WHILE**.

### LEAVE

```sql
LEAVE label
```

The `LEAVE` statement is used to exit a labeled flow-control construct. The statement must appear within the construct that has the given *label*.

### LOOP

```sql
LOOP stmt_list END LOOP
```

```sql
label : LOOP stmt_list END LOOP [label]
```

This statement sets up an execution loop. The statements within the loop execute repeatedly until control is transferred out of the loop.

### REPEAT

```sql
REPEAT stmt_list UNTIL expr END REPEAT
```

```sql
label : REPEAT stmt_list UNTIL expr END REPEAT [label]
```

This statement sets up an execution loop. The statements within the loop execute repeatedly until the expression *expr* is true.

### RETURN

```sql
RETURN expr
```

The `RETURN` statement is used only within stored functions (not stored procedures, triggers, or events). When executed, it terminates execution of the function, and the value of *expr* becomes the value returned to the statement that invoked the function. There can be multiple `RETURN` statements within a function, but there must be at least one.

### WHILE

```sql
WHILE expr DO stmt_list END WHILE
```

```sql
label : WHILE expr DO stmt_list END WHILE [label]
```

This statement sets up an execution loop. The statements within the loop execute repeatedly as long as the expression *expr* is true.

## E.2.2 Declaration Statements

The `DECLARE` statement is used for declaring local variables, conditions, cursors, and handlers.

### DECLARE

```sql
DECLARE var_name [, var_name] ... type [DEFAULT value]
```

```sql
DECLARE condition_name CONDITION FOR named_condition
named_condition: {SQLSTATE [VALUE] sqlstate_value | mysql_errno}
```

```sql
DECLARE cursor_name CURSOR FOR select_stmt
```

```sql
DECLARE handler_type
HANDLER FOR handler_condition [, handler_condition] ...
statement

handler_type: (CONTINUE | EXIT)

handler_condition:
SQLSTATE [VALUE] sqlstate_value
| mysql_errno
| condition_name
| SQLWARNING
| NOT FOUND
| SQLEXCEPTION
```

Declares local variables, conditions, cursors, and handlers. DECLARE can appear only at the beginning of a BEGIN block. If multiple declarations occur, they must appear in this order:

- Variable and condition declarations
- Cursor declarations
- Handler declarations

DECLARE followed by a list of comma-separated variables declares local variables for use within the routine. A local variable is accessible within the BEGIN block where it is declared and any nested blocks, but not in any outer blocks.

A local variable can be initialized in the DECLARE statement with a DEFAULT clause. If there is no DEFAULT clause, the initial value is NULL. To assign a value to a local variable later in the routine, use a SET statement or a SELECT ... INTO var_name statement.

DECLARE ... CONDITION creates a name for a condition. The name can be referred to in a DECLARE ... HANDLER statement. named_condition can be either an SQLSTATE value represented as a five-character quoted string or a numeric MySQL-specific error number.

DECLARE ... CURSOR declares a cursor to be associated with the given SELECT statement, which should not contain an INTO clause. The cursor can be opened with an OPEN statement, used with FETCH to retrieve rows, and closed with CLOSE.

- An SQLSTATE value represented as a five-character string. The value should not be `00000` because that represents success, not an error.
- A numeric MySQL-specific error number. The value should not be zero because that represents success, not an error.
- A named condition previously declared with DECLARE ... CONDITION.
- SQLWARNING, which catches any SQLSTATE value that begins with 01.
- NOT FOUND, which catches any SQLSTATE value that begins with 02.
- SQLEXCEPTION, which catches any SQLSTATE value not caught by SQLWARNING or NOT FOUND.

## E.2.3 Cursor Statements

The statements in this section enable you to open and close cursors, and to use them for fetching rows while open. Cursors currently are read-only and can be used only to move forward a row at a time within a result set (that is, they are not scrollable).

### CLOSE

```sql
CLOSE cursor_name
```

Closes the given cursor, which must be open. An open cursor is closed automatically when the BEGIN block within which the cursor was declared ends.

### FETCH

```sql
FETCH [NEXT] FROM cursor_name INTO var_name [, var_name] ...
```

Fetches the next row from the given cursor into the named variable or variables. The cursor must be open. If no row is available, an error with a SQLSTATE value of 02000 (No Data) occurs.

### OPEN

```sql
OPEN cursor_name
```

Opens the given cursor so that it can be used with FETCH.

## E.3 Comment Syntax

MySQL allows you to intersperse comments with your SQL code. Comments can be useful for documenting statements that you store in files. This section describes how to write comments in your SQL statements.

The MySQL server understands three types of comments:

- Anything from `#` to the end of the line is treated as a comment. This syntax is the same as is used in most Unix shells and in many scripting languages, such as Perl, PHP, or Ruby.

```sql
# this is a single line comment
```

- Anything between `/*` and `*/` is treated as a comment. This form of comment may span multiple lines. The syntax is the same as is used in the C programming language.

```sql
/* this is a single line comment */
/*
    this
    is a multiple line
    comment
*/
```

- You can begin a comment with two dashes and a space (`-- `), or two dashes and a control character such as a newline. Everything from the dashes to the end of the line is treated as a comment.

```sql
-- this is a comment
```

The MySQL double-dash comment style is somewhat different from the comment style of standard SQL, which begins with just two dashes and does not require the space before any following text. MySQL requires a space after the dashes as an aid for disambiguation. Statements with expressions such as 5--7 might be taken as containing a comment starting sequence otherwise. It's not likely you'd write such an expression as 5--7, so this is a useful heuristic. Still, it is only a heuristic, and you should take care if you import SQL code that contains double-dash comments from other database systems into MySQL.

The server ignores comments when executing statements, with the exception that it gives C-style comments that begin with `/*+` special treatment. You can “hide” MySQL-specific keywords in C-style comments by beginning the comment with `/*+` rather than `/*`. MySQL looks inside this special type of comment and uses the keywords, but other database servers will ignore them as part of the comment. This has a portability benefit, at least for other servers that understand C-style comments: It is possible to write code that takes advantage of MySQL-specific functions when executed by MySQL but that can be used with other database servers without modification. The following two statements are equivalent for database servers other than MySQL, but MySQL will perform an INSERT DELAYED operation for the second:

```sql
INSERT INTO mytbl (id,date) VALUES(13, '2008-09-28');
INSERT /*+ DELAYED */ INTO mytbl (id,date) VALUES(13, '2008-09-28');
```
