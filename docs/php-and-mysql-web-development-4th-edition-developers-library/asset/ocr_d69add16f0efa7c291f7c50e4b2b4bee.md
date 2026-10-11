The first thing we do in insert_rows() is prepare an INSERT statement by passing it to mysql_stmt_prepare(). The statement looks like this:

```
INSERT INTO t (i,t,c,dt) VALUES(?, ?,?, ?)
```

The statement contains four placeholders, so it’s necessary to supply four data values each time the statement is executed. Placeholders typically represent data values in VALUES() lists or in WHERE clauses. But there are places in which they cannot be used:

+   - As identifiers such as table or column names. This statement is illegal:

```
SELECT * FROM ?
```

+   - You can use placeholders on one side of an operator, but not on both sides. This statement is legal:

```
SELECT * FROM student WHERE student_id = ?
```

However, this statement is illegal:

```
SELECT * FROM student WHERE ? = ?
```

This restriction is necessary so that the server can determine the data type of parameters.

The next step is to set up an array of MYSQL_BIND structures, one for each placeholder. As demonstrated in insert_rows(), setting these up involves two stages:

+   1. Initialize all parts of the structures that will be the same for each row inserted.
+   2. Perform a row-insertion loop that, for each row, initializes the parts of the structures that vary for each row.

You could actually perform all initialization within the loop, but that would be less efficient.

The first initialization stage begins by zeroing the contents of the param array containing the MYSQL_BIND structures. The program uses memset(), but you could use bzero() if your system doesn’t have memset(). These two statements are equivalent:

```
memset ((void *) param, 0, sizeof (param));
bzero ((void *) param, sizeof (param));
```

Clearing the param array implicitly sets all structure members to zero. Code that follows sets some members to zero to make it explicit what’s going on, but that is not strictly necessary. In practice, you need not assign zero to any structure members after clearing the structures.