
SQL> create type employee_type as object (
1 ssn number(9),
2 name varchar2(35),
3 address varchar2(70),
4 resume CLOB );

# 列表 12.2 将对象类型作为关系表中的列

```sql
SQL> create table manager_candidates (
1 position varchar2(40),
2 vacancy CLOB,
3 employee_type );
SQL> insert into manager_candidates values (
1 'Technical Manager',empty_clob()),
2 employee_type(123456789,'John Doe','123 Maple St '
3 Metropolis - NY : 12762,empty_clob()) );
SQL> select mc.employee.name from manager_candidates mc
1 where mc.employee.ssn = 123456789;
```

# III 第 12 章

注意你必须使用别名和点符号语法来检索表内对象的属性值。还要注意当你执行插入操作时，你为名为 `employee_type` 的对象类型调用了名为 `employee_type` 的构造器方法。所有构造器的名称都与其对应的对象类型相同。列表 12.3 提供了你可以对对象类型所做的另一个示例。

# 列表 12.3

```sql
SQL> create table employee of employee_type;
```

创建此表也会包含对象 ID (`OID`) 或 `REF` 的列，用于对象实例（行）。这与具有对象类型（列）的关系表形成对比。

# REF 属性

Oracle8 世界中的关系与 Oracle 关系世界中的并无不同：它指定了对象之间如何关联。Oracle 仅支持单向一对关系，这可能不足以建模你的业务。当你将对象类型中的属性声明为 `REF` 时，这本质上是一种关系。`REF` 本质上也是指针，或对象的“句柄”。你可以限制 `REF` 引用的范围。范围的概念被包含 SQL3（ANSI 标准的最新修订），它包含了一些面向对象的特性。

就像 RMT（关系模型二）中的代理键一样，Oracle8 中的对象 (`REF`) 是系统生成的值，在所有对象中是唯一的，并指向持久对象。`REF` 实际上引用对象表中的行，而不是对象类型。对于给定的对象，`REF` 是该对象的 `OID` 与对象表的 ID 的组合。列表 12.4 显示了如何创建一个包含 `REF` 属性的对象类型，基于该类型创建对象表，并插入行（实例化对象）。

# 列表 12.4

```sql
SQL> create type insured_employee_type as object (
1 control_number number(9),
2 contract CLOB,
3 employee_ref ref employee_type );
SQL> create table insured_employee (
1 of insured_employee_type
2 scope for (employee_ref) is employee);
SQL> insert into insured_employee
1 select control_sequence.nextval,
2 empty_clob(),
3 ref(e) from employee e
4 where e.ssn=123456789;
```

# 方法

对象类型可以有零或多个 `MEMBER` 方法。`MEMBER` 方法（或简称“方法”）是一种可以操作任何对象类型内部数据（即属性）的子程序，而不仅仅是定义它所在的类型。当然，方法是一个 `PL/SQL` 过程或函数。

就像任何 `PL/SQL` 封装子程序一样，你为每个方法创建一个接口（规范规范）和一个实现（包体）。当你访问方法时，使用点符号语法。

`(object.method)`。列表 12.5 展示了对象类型内方法创建（规范和正体）的示例，随后是调用该方法的某些 `PL/SQL` 代码。。

# 列表 12.5

```sql
SQL> create type auto_type as object (
1 vin varchar2(80),
2 make varchar2(30),
3 model varchar2(40),
4 member function getcost
5 return number;
6 pragma restrict_references
7 (getcost, WNPS) );
SQL> create type body auto_type (
1 member function getcost
2 return number is
3 begin
4 return (cost);
5 end;
/* create object table and insert some data */
SQL> declare
1 a auto_type;
2 c number;
3 begin
4 select value(a)
5 into a
6 from auto a
7 where a.vin='1VWF673FB9093871AF21';
8 c:=a.getcost();
9 /* do not something with c */
10 end;
```

注意，该函数通过 `pragma` 指令设置为 `WNPS`。`WNPS` 代表“不写包阶段”，意味着该函数被设定为不能修改其内部的参数（否则会产生副作用）。若要比较或排序对象类型，你可以定义一个 `MAP` 或 `ORDER` 函数来比较两个对象。当你使用这些比较函数时，你是在指定用于条件和排序的排序语义（即排序对序列）。有关更详细的实现细节，请参考 Oracle8 或 Oracle8i CD-ROM 文档。

# 集合（VARRAY 和嵌套表）

集合是事物的有序或无序组。`VARRAY` 是有序的，而嵌套表（nested TABLE）属于 ANSI 标准，但 `VARRAY` 是非标准的。任何主从（即一对多）关系都可以帮助对比这两种集合。按某种顺序排列的项目主列表可以使用 `VARRAY`，而每个主列表的每个行项目详情可以使用其内部的嵌套表。

# 第 12 章 对象化特性

## 注意

集合不支持并行查询、`DML`、复制和分布式数据库功能。

Oracle `VARRAY` 像数组一样，具有隐式顺序。数组中的每个元素都有相对于数组起始位置的偏移位置，可以通过该偏移量直接访问（也称为下标或索引）。`VARRAY` 数据存储在行内（表行内），除非单元存储超过 4KB（此时存储在数据库外部）。每个 `VARRAY` 像大多数数组一样，都有一个计数（`count`）和一个限制（`limit`）。计数是能够存储的最大元素数量。在 `VARRAY` 中，限制是可以存储的最大元素数量。你可以通过 `PL/SQL` 和 3GL 中的订阅来访问单个元素，但在纯 SQL 中不行。

如前所述，嵌套表非常适合主从（即一对多）关系。Oracle 中的嵌套表实际上是一种用户定义类型，或 `TABLE` 类型，它可以作为列用在表中，并将对象类型作为属性，或作为 `PL/SQL` 子句。嵌套表使用 `STORE AS` 子句存储在主表之外的存储表中。嵌套表具有一些优缺点。优点包括可以对其建立索引（与对象表不同），并且不需要连接（类似于簇）。缺点之一是你具有某种形式的级联删除（删除主行将删除所有详情行），无法实现引用完整性约束。

# 列表 12.6 创建和使用 VARRAY 和嵌套表（TABLE）

```sql
/* VARRAY */
SQL> create type tax_type as object (
  1 year date,
  2 taxes_paid number);
SQL> create type tax_array_type as VARRAY(3)
  1 of tax_type;
SQL> create type client_type as object (
  1 cid number,
  2 name varchar2(35),
  3 address varchar2(80),
  4 taxes_array_type);
SQL> create table clients of client_type;
/* NESTED TABLE */
SQL> create type child_type as object (
  1 child_id number,
  2 child_name varchar2(35));
SQL> create type child_nest_type as TABLE
  1 of child_type;
```

```sql
SQL> create table parent (
  1 parent_id number,
  2 parent_name varchar2(35),
```
