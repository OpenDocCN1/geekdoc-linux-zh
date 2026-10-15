
`DBMS_OUTPUT.PUT_line(get_tables_cur.table_name);`

`END LOOP;`

`END;`

如果你以 `scott/tiger` 身份运行此代码，将得到以下结果：

- `BONUS`
- `DEPT`
- `EMP`
- `SALGRADE`
- `PL/SQL` 成功完成。

第 2–3 行定义了游标。

第 5 行定义了与游标配合使用的游标记录变量。

第 6 行使用点符号引用游标中指定的列。

如列表 28.15 所示，你可以做得更加简洁，但仍然可以相同的结果：

# 列表 28.15 cfor2.sql—简单的循环，更简单的循环

```
BEGIN

FOR get_tables_cur IN (SELECT * FROM user_tables) LOOP

  DBMS_OUTPUT.put_line(get_tables_cur.table_name);

END LOOP;

/

```

区别在于游标也被定义在循环局部。这对于简单程序是没问题的。

你也可以带参数并搜索特定的表（见列表 28.16）。

# 列表 28.16 cfor3.sql—带参数的简单循环游标

```
DECLARE

  CURSOR get_tables IS

    SELECT * FROM user_tables;

-- (此处原文代码未完整，但根据逻辑翻译应保持一致)

```

# 使用隐式游标

隐式游标的维护成本相对较低。它们仅在你预期获取恰好一行或多于一行时使用。如果找到零行或多行，会抛出 `NO_DATA_FOUND` 或 `TOO_MANY_ROWS` 异常，导致你无功而获。列表 28.20 展示了隐式游标的作用。

# 列表 28.20 impour.sql—一个简单的隐式游标

```sql
DECLARE

  -- 记录变量定义

  get_tables_rec all_tables%ROWTYPE; -- 基于表

  -- 局部变量

  local_owner all_tables.owner%TYPE := 'DEMO'; -- 搜索标准

  local_table all_tables.table_name%TYPE := 'CUSTOMER';

BEGIN

  SELECT * INTO get_tables_rec -- 查找单行

  FROM ALL_TABLES

  WHERE owner = local_owner AND table_name = local_table;

  DBMS_OUTPUT.put_line(get_tables_rec.tablespace_name);

END;

/

```

你得到以下输出：

`USER_DATA`
`PL/SQL procedure successfully completed.`

如果你没有构造搜索条件以返回恰好一行，就会发生这种情况（列表 28.21）。

# 列表 28.21 gloomy.sql—当发现多行时隐式游标失败

```sql
DECLARE

  -- 记录变量定义

  get_tables_rec all_tables%ROWTYPE; -- 基于表

  -- 局部变量

  local_owner all_tables.owner%TYPE := 'DEMO';

BEGIN

  SELECT * INTO get_tables_rec FROM ALL_TABLES

  WHERE owner = local_owner;

  DBMS_OUTPUT.put_line(get_tables_rec.tablespace_name);

END;

/

```

服务器会给出一个有意义的错误信息：

```
ERROR at line 1:
ORA-01422: exact fetch returns more than requested number of rows
ORA-06512: at line 7
```

实际发生的情况如下：

1. Oracle 打开了游标并抓取了一行。
2. Oracle 并不满意，又尝试另一次抓取并获取了另一行！
3. 由于你无法将十磅的行塞进一个五磅的变量里，Oracle 关闭了游标（实际上它最终也会关闭）并生成了异常。

William Page 的 Oracle 技巧 #81 提到在隐式游标上进行两次抓取，仅仅是为了看它是否会返回另一行（从而不满足隐式游标返回恰好一行的要求）。这是一个 ANSI 标准的要求。

当你只需要一行且不想处理异常异常时，请使用显式游标并由自己执行 `FETCH`。如果你想知道可能存在多个游标（或者完全没有！），并且介意处理异常，那么就使用隐式游标。事实上，正因为这个原因，你可以在单行查找例程中使用隐式游标。你需要知道单行查找是否真的恰好是一行，或者你是否将其视为错误。如果你在乎获取那一行，使用显式游标处理会更高效。

隐式游标不能配合数组来处理额外的行。根据定义，它们应该返回单行。

# 异常

异常是一个非致命事件，它会立即中断程序的正常执行，并无条件地跳转到块的异常处理器。某些异常，如 `NO_DATA_FOUND` 或 `TOO_MANY_ROWS`，可以被视为处理过程正常的一部分。像 `VALUE_ERROR` 这样的异常指示程序错误或某些意外事件。其他异常则指示严重问题，例如内存耗尽。

如果块中没有定义异常处理器，异常将返回给上一层块（如果有的话）。异常会“冒泡”通过嵌套块，直到找到该块的异常处理器，或者控制返回到调用上下文（在我们的例子中是 `SQL+Plus`）。

你的程序会不断遇到异常。你只需要一个异常处理器来处理它们。再次参考上一次导致崩溃的隐式游标（见列表 28.22）。

# 列表 28.22 graceful.sql—使用异常处理器

```sql
DECLARE

-- 记录变量定义

get_tables_rec all_tables%ROWTYPE; -- 基于类型

-- 局部变量

local_owner all_tables.owner%TYPE := 'DEMO'

status NUMERIC := 0; -- 捕获错误代码（初始化为 OK）

BEGIN

  SELECT * INTO get_rec FROM ALL_TABLES

  WHERE owner = local_owner;

  DBMS_OUTPUT.put_line(get_rec.tablespace_name);

EXCEPTION

  WHEN TOO_MANY_ROWS THEN

    status := SQLCODE;

    DBMS_OUTPUT.put_line('get_tables: ' || SQLERRM(status));

    DBMS_OUTPUT.put_line('get_tables: Exiting gracefully.');

END;

/

```
