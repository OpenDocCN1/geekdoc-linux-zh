
```sql
DECLARE
  -- 用户定义数据类型
TYPE MY_STRING_TYPE IS RECORD (
  str_len INTEGER := 0, -- 在声明变量时初始化
  str VARCHAR(32767)); -- 默认为 NULL
TYPE MY_ARRAY_TYPE IS TABLE OF CHAR(8) INDEX BY BINARY_INTEGER;
  -- 变量
  str MY_STRING_TYPE; -- 一个新的复合变量
  arr MY_ARRAY_TYPE; -- 一个新的 D-数组
```

## 创建你的 RECORD 类型

`RECORD`类型定义了一个可以包含任意数量、任意数据类型成员的结构，包括之前定义的`RECORD` `TABLE`类型。类似于某些类型的`%ROWTYPE`记录变量，单个成员使用点符号符号（dot notation）进行引用。成员的任何初始化定义都在运行时针对基础变量执行的。

你可以嵌套`RECORD`类型：

```sql
DECLARE
TYPE ZIP_TYPE IS RECORD (
zip5 VARCHAR(5),
DASH CONST VARCHAR2(1) := '-', -- 可能是为了显示目的
plus4 VARCHAR(4) := '0000'); -- 在运行时初始化
TYPE ADD_TYPE IS RECORD (
line1 VARCHAR(30),
line2 VARCHAR(30),
city VARCHAR(20),
state VARCHAR(2),
zip_code ZIP_TYPE);
TYPE EMPLOYEE_TYPE IS RECORD (
ssn VARCHAR(9),
dob DATE;
address ADD_TYPE);
employee_rec EMPLOYEE_TYPE; -- 实际定义的存储
BEGIN
employee_rec.ssn := '123456789'; -- 某人的社会安全号
employee_rec.address.city := 'Pittsburgh';
employee_rec.address.zip.zip5 := '15210'; -- 匹兹堡的邮政编码
employee_rec.address.zip.code.plus4 := '3702'; -- 匹兹堡的 M. Olive
```

注意使用点符号来引用此嵌套记录的任何子组件。这样做的主要优势是可以更方便地管理不同数据类型的相关数据。一组数据可以通过单个参数传递给子程序或从子程序返回。这比替代方案更整洁、更紧凑。记录允许开发者以紧密相关的数据块来进行思考。

只有当它们被声明为相同的数据类型时，才能将一个记录变量赋值给另一个。基于数据库表`ROWTYPE`的变量与定义为记录类型的变量始终是不兼容的，即使它们的成员完全匹配：

```sql
DECLARE
  TYPE ORDERS_TYPE IS RECORD ( -- 看起来像数据库表
  ord_num orders.ord_num%TYPE,
  quantity orders.quantity%TYPE,
  ...
  discount orders.discount%TYPE);
  orders_rec%ROWTYPE; -- 基于数据库表
  new_orders_rec ORDERS_TYPE;
  old_orders_rec ORDERS_TYPE;
BEGIN
  -- 执行操作
  old_orders_rec := new_orders_rec; -- 这是正确的
  new_orders_rec := orders_rec; -- 这是错误的！
```

在向数据库表插入行时，`VALUES`子句必须指定每个成员：

```sql
INSERT INTO orders_rec;      -- 错误！

INSERT INTO old_orders_rec;  -- 错误！

INSERT INTO orders (ord_num, qty, ..., discount) VALUES

(new_orders_rec.ord_num, new_orders_rec.quantity, ...

new_orders_rec.discount); -- 正确！
```

## 创建你的数组

`PL/SQL` `TABLE`是任何标量类型的一维数组。对于 7.3 之前的 Oracle 服务器，`TABLE`不能包含`RECORD`或另一个`TABLE`。对于 Oracle 7.3 及以上版本，`TABLE`可以包含用户定义的记录，但不能包含另一个`TABLE`。在 Oracle 8 中，`TABLES`只是几种类型的集合。

`PL/SQL` `TABLE`不像 Oracle 数据库。它是一个无界数组，其元素在赋值之前不存在。它始终通过`BINARY_INTEGER`索引，因此其元素索引范围为 -2,147,483,647（好吧，并不完全无界）。程序员可以选择在偏移量 0、1 或任何有意义的地方对数组进行索引。因为未赋值的元素不存在，数组可以包含稀疏分布的值，而对内存使用产生产生额外影响。每个元素通过括号中的偏移量进行引用。你通过先声明表类型，然后基于它创建一个变量来创建`PL/SQL`变量。例如，以下代码仅使用内存存储这些值：

```sql
DECLARE
  TYPE STR_TYPE IS TABLE OF VARCHAR2(8)
  INDEX BY BINARY_INTEGER;
  arr STR_TYPE;
  BINARY_INTEGER := 17; -- 不确定性通用常数
BEGIN
  arr(-2,147,483,647) := 'smallest';
  arr(0) := 'zero';
  arr(2,147,483,647) := 'biggest';
  arr(1) := 'UCU'; -- 索引变量适合循环
```

在声明长字符串变量时，考虑到`PL/SQL`总是为`VARCHAR2`变量分配声明大小的缓冲区是明智的。你也可以像这样指定表为`NULL`：

```sql
TYPE STR_TYPE IS TABLE OF VARCHAR2(8) NOT NULL
INDEX BY BINARY_INTEGER;
arr STR_TYPE;
```

### 表 28.4 使用 PL/SQL 表属性

| 属性 | 描述 | 返回值 | 用法 |
| :--- | :--- | :--- | :--- |
| EXISTS | 测试表元素是否存在值 | TRUE/FALSE | `tableName.EXISTS(offset)` |
| COUNT | 返回表中的项数 | BINARY_INTEGER | `tableName.COUNT` |
| FIRST | 返回第一个元素的偏移量 | BINARY_INTEGER | `tableName.FIRST` |
| LAST | 返回最后一个元素的偏移量 | BINARY_INTEGER | `tableName.LAST` |
| PRIOR | 返回上一个元素的偏移量 | BINARY_INTEGER | `tableName.PRIOR(offset)` |
| NEXT | 返回下一个元素的偏移量 | BINARY_INTEGER | `tableName.NEXT(offset)` |
| DELETE | 删除指定的元素、范围或所有 | 无 | `tableName.DELETE([off_m, off_n])` |

当已经处于`FIRST`或`LAST`元素时，`PRIOR`和`NEXT`分别返回`NULL`。
`DELETE`可以使用任何一种形式删除指定的元素、元素范围或所有元素：

- `tableName.DELETE(m);` 仅删除一个元素
- `tableName.DELETE(m, n);` 删除范围 `[m..n]` 内的所有元素（包含边界）
- `tableName.DELETE;` 删除表中的所有元素

如果指定范围内的偏移量不存在项，则直接跳过（不抛出异常）。范围必须是降序的；`m > n`，而`DELETE`不需要。

变长数组和嵌套表 Oracle 定义了两种类数组结构或集合：变长数组（或数组）和嵌套表。它们与`PL/SQL`表（现在称为“索引表”）的区别在于其使用方式和主要关注点。虽然索引表构造属于`PL/SQL`，但变长数组和嵌套表侧重于数据库本身。例如，它们可以像其他任何数据列一样存储在数据库表中，但不能绑定到主机变量。

创建变长数组创建一个变量与创建`PL/SQL` `TABLE`类似，即声明一个类型并创建该类型的变量。然而，与`PL/SQL` `TABLE`不同，`varray`是“密集的”而非“稀疏的”——你不会像`TABLE`那样在没有数据的地方出现“空隙”。此外，`PL/SQL` `TABLE`几乎是无边界，而`varray`有非常具体的限制。当创建`varray`时，它是`NULL`，且无法进行测试。要使用它，必须先使用构造函数对其初始化，如下代码所示：

# 第 28 章 PL/SQL 基础
