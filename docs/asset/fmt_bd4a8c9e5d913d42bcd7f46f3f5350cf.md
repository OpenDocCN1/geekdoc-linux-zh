
## WHILE (x < 10) LOOP -- While 循环

...

`x := x + 1`;

END LOOP; -- 完成

## LOOP -- 模拟 Repeat-Until（或 Do-While）循环

...

EXIT WHEN -- 完成

END LOOP; -- 完成

始终记住循环的开头和结尾是一个良好的习惯，特别是对于长循环，这样你就知道它的用途了。

PL/SQL 不支持像 FORTRAN 那样的使用 `CONTINUE` 语句来跳转到循环末尾并跳过中间的所有代码。在这种情况下，有些人会建议你使用条件逻辑将代码模块化，这会导致你的代码变得缩进非常离谱且更难以维护。然而，这有一个解决方案。使用 `goto` 语句来模拟 `CONTINUE` 语句。`CONTINUE` 是 SQL 中的关键字，所以你不能在语句或标签中使用它。

### 列表 28.11 模拟 continue (Simulating)

```sql
DECLARE

j NUMBER := 0;

BEGIN

DBMS_OUTPUT.enable;

LOOP

 -- 打印 0 到 20 之间的偶数

IF MOD(j,2) = 1 THEN -- 跳过奇数

GOTO CONTINUE; -- 拼写错误是一个内部梗

END IF; -- 跳过奇数

DBMS_OUTPUT.put_line(TO_CHAR(j) || ' is even');

n<<CONTINUE>>

EXIT WHEN j = 20; -- 完成

j := j + 1; -- 不要忘记增加循环计数器！

END LOOP; -- 打印 0 到 20 之间的偶数

END;
```

服务器响应如下：

```
0 is even

2 is even

4 is even

6 is even

8 is even

10 is even

12 is even

14 is even

16 is even

18 is even

20 is even
```

## 使用游标迭代

游标可以返回一个或多行，或者一个都不返回。通常的操作序列是：
1. 声明游标，以及用于存储数据的数据结构
2. 打开游标
3. 反复从游标获取数据到数据结构中，直到数据集耗尽
4. 关闭游标

### 使用游标迭代

对于 `FOR` 循环，不支持像 FORTRAN 那样的 `CONTINUE` 语句来跳转到循环末尾并跳过中间的所有代码。在这种情况下，有些人会建议你使用条件逻辑将代码模块化，这会导致你的代码变得缩进非常离谱且更难以维护。然而，这有一个解决方案。使用 `goto` 语句来模拟 `CONTINUE` 语句。`CONTINUE` 是 SQL 中的关键字，所以你不能在语句或标签中使用它。

## 获取循环变量的值

`FOR` 循环的语法意味着你无法在作用范围之外引用它，它在循环完成后消失。如果你需要循环变量，必须将其复制（参见 28.12）。

### 列表 28.12 lastodd.sql

```sql
DECLARE

  j NUMBER;

BEGIN

  DBMS_OUTPUT.enable; -- 输出

  FOR i IN 1..100 LOOP -- 100 次迭代

    IF MOD(i,2) = 1 THEN -- 奇数

      j := i;                -- 捕捉变量

    END IF;

  END LOOP;                -- 什么都不做

  DBMS_OUTPUT.put_line('last number was ' ||TO_CHAR(j));

END;
```

服务器显示：

```
last number was 99
PL/SQL 过程完成。
```

`IN` 子句必须指定一个范围。你也可以反向迭代，以倒计时的方式（参见 28.13）。

### 列表 28.13 countdown.sql——使用 IN

```sql
BEGIN

FOR j IN REVERSE 1..10 LOOP -- 倒计时

  DBMS_OUTPUT.put(TO_CHAR(j) || '- ');

END LOOP; -- 倒计时

  DBMS_OUTPUT.put_line('Blastoff!');

END/
```

你得到：
`10-9-8-7-6-5-4-3-2-1-Blastoff!`
PL/SQL 过程完成。

## 定义游标

在定义游标时，你会注意到几种基于相同主题的变体：

```sql
DECLARE

  -- 获取数据库中的所有订单

  CURSOR get_orders IS

    SELECT * FROM orders;

  -- 根据指定的订单号获取几列

  CURSOR get_orditem(Pord_num orders.ord_num%TYPE) IS

    SELECT seq_num, quantity, unit_price, extended_price
    FROM orders
    WHERE ord_num = Pord_num;

  -- 获取特定项目#的整行

  CURSOR get_items(Pitem_no items.item_no%TYPE) RETURN items%ROWTYPE IS

    SELECT * FROM items WHERE item_no = Pitem_no;

  -- 获取特定项目#的名称

  CURSOR get_item_name(Pitem_no items.item_no%TYPE)
    RETURN items.item_name%TYPE
  SELECT item_name FROM items WHERE item_no = Pitem_no;
```

尽管有很多变体，但只有两种基本模式。游标可以带有参数，也可以不带。你在打开游标时提供参数的值。你可以定义返回类型，也可以不定义。返回类型可以是用户定义的记录、数据库行类型或单个变量。无论何种方式，`SELECT` 子句中定义的列必须与你用于接收返回值的任何内容匹配。

一旦声明，游标就可以打开、获取（FETCH）行、检查其状态并在不再需要时关闭。

游标可以有任何名称；在这些情况下，惯例是在游标名称后面加上 `_cur`（或）或 `_loop`，或者以 `get_` 作为前缀（取决于我的心情）。在游标名称中使用表名，或者尝试使其具有意义（不要太长），例如 `get_addresses` 或 `employee_by_dept_cursor`。

请注意，参数列表只能包含输入值，不能包含输出值。这就是为什么不需要也不允许参数流。输入参数也必须是标量值。

当游标打开时，会执行 SQL 并计算相应的数据集。然而，并没有实际返回行到程序。你使用 `FETCH` 每次获取一行。获取的行将保持为当前行，直到执行下一次 `fetch`。你只能向正方向获取；没有控制可以在数据集中向后移动。

## 游标属性

游标具有表 28.7 所示的属性。

### 表 28.7 游标属性

| 属性 | 返回值 | 说明 |
| --- | --- | --- |
| ISOPEN | TRUE/FALSE | 表示游标是否已打开或关闭 |
| FOUND | TRUE/FALSE | 表示是否找到了行 |
| NOTFOUND | TRUE/FALSE | 表示是否未找到行 |
| ROWCOUNT | NUMBER | 获取的每行的序号（第 1 行、第 2 行、第 3 行...） |

以下是它们的一些用法示例：

```sql
IF (orders_cur%FOUND) THEN -- 获取了一个订单

  OPEN items_cur(orders_cur.orderno); -- 打开一个相关的游标

  LOOP

    FETCH items_cur into order_item;

    EXIT WHEN items_cur%NOTFOUND; -- 完成后退出

    -- 显示目前为止处理的许多行
    DBMS_OUTPUT.PUT_line('On Row #' || TO_CHAR(items_cur%ROWCOUNT));

  END LOOP;

END IF; -- 获取了一个订单
```

```sql
IF (items_cur%ISOPEN) THEN -- 关闭游标

  CLOSE items_cur;

END IF; -- 关闭已打开的游标
```

## 游标 FOR 循环

游标 `FOR` 循环是使用游标的最简单方法。游标的打开、获取和关闭都在 `FOR` 循环的作用范围内自动处理。返回记录变量也为你为你隐式地定义，并且不能在循环范围之外引用。游标可以带有参数。你可以在声明部分中声明游标，也可以在 `FOR` 循环体本身中声明（见列表 28.14）。

### 列表 28.14 cfort.sql—游标循环的简单用法

```sql
DECLARE

  CURSOR get_tables IS

    SELECT * FROM user_tables;

BEGIN

  FOR get_tables_cur IN get_tables LOOP
```
