
输出如下：

```
+   [rick@gw psql]$ ./sel15
Connected OK
About to execute BEGIN rows affected
Command executed OK, no rows affected
About to execute DECLARE age_fname_cursor CURSOR FOR SELECT age, fname FROM
children WHERE age = '6';
Command executed OK, no rows affected
About to execute FETCH 1 IN age_fname_cursor
Select executed OK, 1 rows found
About to execute NEXT IN age_fname_cursor
Select executed OK, 1 rows found
About to execute NEXT IN age_fname_cursor
Select executed OK, 1 rows found
About to execute NEXT IN age_fname_cursor
Select executed OK, 0 rows found
About to execute COMMIT WORK
Command executed OK, no rows affected
```

如你所见，一次一次地检索我们的数据实际上非常简单。唯一的缺点（通常无关紧要）是，我们不知道是否检索了所有数据，也不知道总共有多少行。这是因为 `PQtuples(result)` 的结果，对于单行的 `FETCH` 来说是合理的，当检索到行时它的值为 1。

现在我们以更易于管理的格式检索了数据，可以继续访问这些信息的各个部分了。

## 获取列信息

从返回的数据中提取非常有用的第一条信息是列信息（包括列名和数据类型）。通过三个函数可以很容易地实现这一点：一个用于发现有多少列，一个用于获取每个列的名称，另一个用于获取列的大小。当然，你可以通过名称指定你想要的列，但这样的话，理论上你预先知道了将返回的每个列的类型。

通常情况下，按名称指定你需要的每个列是一个好主意。这样做的原因是为了防止当数据库添加了新列时，你的代码产生“意外”。如果需要删除某些列，至少在代码中进行 `grep` 搜索就能显示出代码中待删除的列名。假设代码中的列类型没有那么明确——即在运行时确定类型意味着你的代码可以自动考虑到列类型的任何变化。相反，你将编写更多的代码，这会增加出现 Bug 的风险并略微降低性能。

我们通过 `PQnfields` 找到返回结果中的列数：

```c
int PQnfields(PGresult *result);
```

## 第四章

我们使用 `PQfname` 函数获取单个列的名称，并传入 `field_index`，第一列的索引为 0：

```c
char *PQfname(PGresult *result, int field_index);
```

我们可以通过 `PQsize` 获取数据大小的想法。我们使用“idea（想法）”这个词是因为它只返回 PostgreSQL 内部使用的空间，即使如此，对于 `VARCHAR` 等变长字段，它也会返回 -1。

```c
int PQsize(PGresult *result, int field_index);
```

这里明显遗漏了返回的列的类型。遗憾的是，看起来执行此任务的程序 `PQtype` 返回的是一个 `Oid`（实际上是一个无符号整数的类型定义）。这只提供了类型的内部表示，并且在任何地方都没有文档说明，使得它几乎毫无用。出于这个原因，我们在这里不会使用它，但希望在以后版本的 PostgreSQL 中，或者至少在 libpq 库中，开发出一个更有用的函数来发现返回的类型。

我们现在利用这些知识将我们的 `sel5.c` 程序扩展为 `sel6.c`，通过检索列信息。使用检索到的数据中的某一行来提取列头信息并不重要，事实上，即使 `SELECT` 语句没有返回行，我们仍然可以访问列信息。

这些非常微小，所以我们在这里只显示新增，而不是重复所有代码。

首先，我们为新函数添加原型声明：

```c
void show_column_info(PGresult *result);
```

我们在检索数据时调用它。我们允许在每次返回数据时都调用它，以证明这是有效的，尽管我们我们在生产环境代码中不会这样做。

```c
if (stmt_ok) {
    PQclear(result);
    stmt_ok = execute_one_statement("FETCH 1 IN name age_fname_cursor",
                                    &result);
    if (stmt_ok) {
        show_column_info(result);
    }
    while (stmt_ok && PQtuples(result) > 0) {
        show_one_row_data(result);
    }
    PQclear(result);
}
```

## PostgreSQL 接口

```c
stmt_ok = execute_statement("BEGIN WORK", &result);
if (stmt_ok) {
    Pclear(result);
    stmt_ok = execute_statement("DECLARE age_fname_cursor CURSOR FOR
        SELECT age, fname FROM children WHERE
        age < '65*'", &result);
    if (stmt_ok) {
        Pclear(result);
        stmt_ok = execute_statement("FETCH 1 IN age_fname_cursor",
            &result);
        if (stmt_ok) show_column_info(result);
        while (stmt_ok & Pntuples(result) > 0) {
            show_row_data(result);
            Pclear(result);
            stmt_ok = execute_statement("FETCH NEXT IN age_fname_cursor",
                &result);
        }
    }
    stmt_ok = execute_statement("COMMIT WORK", &result);
}
if (stmt_ok) Pclear(result);
Pfinish(conn);
return EXIT_SUCCESS;
```

```c
int execute_one_statement(const char *stmt_to_exec
retcode = 0;
break;
return retcode;
/* execute_one_statement * */
void show_column_info(PGresult *result) {
    int num_columns = 0;
    int i;
    if (!result) return;
    num_columns = PQfields(result);
    printf("%d columns in the result set\n", num_columns);
    for(i = 0; i < num_columns; i++) {
        printf("Field %d, Name %s. Internal size %d\n",
            i,
            PQfname(result, i),
            PQsize(result, i));
    }
}
/* show_column_info * */
void show_one_row_data(PGresult *result) {
    int col;
    for(col = 0; col < PQfields(result); col++) {
        printf("DATA: %s\n", PQgetisnull(result, col) ? "NULL" :
            PQgetvalue(result, col));
    }
} /* show_one_row_data * */
void tidyup_and_exit(PGconn *conn) {
```
