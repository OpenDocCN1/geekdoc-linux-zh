
> 图 B.5 用户定义类型——定义。

`TYPE` 是源于（SOURCED ON）一个现有类型，即使用基础产品定义的类型（如 `INTEGER`）。

一旦定义了类型，在创建或更改表时，列定义可以引用该类型。数据库管理器在使用此类列时将执行强类型检查。例如，图 B.5 底所示 `SELECT` 语句是无效的，因为 `KPH` 和 `MPH` 已定义为唯一类型。它们不能相互比较。

使用 `WITH COMPARISONS` 子句会导致 DB2 创建转换函数，将 UDT 从其源类型转换。这是强制语法，除非基础类型是 `LONG VARGRAPH`、`LONG VARCHAR`、`BLOB`、`CLOB` 或 `DBCLOB`。例如，插图中的 `KPH` 定义显示了将该唯一类型从 `INTEGER` 源类型进行转换的函数。使用 `WITH COMPARISONS` 并自动生成转换函数允许以下语句变得有效：

```
SELECT ROUTE_NUM FROM SPEED_LIMITS
WHERE CANADA_SL > KPH(80)
```

其中 `KPH(80)` 将整数值 80 转换为 `KPH` 类型。

在 DB2 中，还可以使用 `CREATE TYPE` 语句创建结构化类型。用户定义的结构化类型可以包含零个或多个属性。结构化类型可以是子类型，允许从父类类型继承属性。

# 创建唯一类型——GUI

图 B.6 创建唯一类型——GUI。

从控制中心（Control Center）访问创建唯一类型 GUI：

- 应用程序对象（Application Objects）
- 选择用户定义唯一类型（User-Defined Distinct Types）（右鼠标按钮）
- 选择创建（Create）

创建唯一类型 GUI 允许指定以下内容（图 B.6）：

- 选择唯一类型的架构
- 指定唯一类型的名称
- 选择源数据类型
- 非固定源数据类型的数据类型特征
- 注释（Comment）

# 用户定义函数——必要性

使用 DB2 作为数据库管理器的不同业务应用程序广泛且多样，并且数量持续增长。这种多样化的用法要求数据库支持各种标量函数。见图 B.7。

and so forth cubic rating mph yards horsepower UDTs? watts kph feet cups and so forth and so forth

图 B.7 用户定义函数——必要性。

UDTs 的使用也增加了对额外标量函数的需求。例如，可能需要从加仑到升升的转换。引入对用户定义函数（UDFs）的支持允许安装环境定义任意数量的专用函数。这可以被软件开发者利用。

# 用户定义函数——定义

```
CREATE FUNCTION KPH_TO_MPH(KPH) RETURNS MPH EXTERNAL 'conversions.dll'
```

图 B.8 用户定义函数——定义。

`CREATE FUNCTION` 语句可用于定义标量、表或行函数。标量函数在每次被调用时返回单个值。表函数返回

强类型检查定义了数据类型只能以安装环境定义的方式使用。因此，除非定义了此类用法，否则 UDT 不能与数据库管理器提供的函数结合使用。为了帮助安装环境定义常用函数，DB2 允许函数源于之前定义的函数。这些之前定义的函数可以由数据库管理器提供，也可以由用户编写。

对于某些 UDT，**不**为数据库管理器提供的每个函数定义源于它的函数是有益的。例如，假设员工编号被定义为基于 `INTEGER` 类型的唯一类型。安装环境可能不会在此类型上定义 `SUM`、`AVG`、`+`、`-`、`*` 函数，因为此类操作是无效的。

也允许函数名重载，因此同一个名称可以使用多次。例如，考虑图 B.9 中定义的 `AVG_US_SPEED` 函数。该函数可以被定义为 `AVG`，即使该函数名称已经存在。在重载情况下，数据库管理器将调用与传入的输入参数匹配的函数。

## 用户定义函数—隔离（Fencing）

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_442_0.png)

**图 B.10** 用户定义函数—隔离。

DB2 为安装程序提供了确定用户定义函数执行位置的能力。UDF 的执行位置是在实例级别上，因此适用于在该实例内创建的所有数据库。

被隔离的（fenced）函数不会损害数据库管理器存储区域的完整性。如果 UDF 中存在代码错误，数据库将能够免受这些错误的影响。

未被隔离的（not fenced）函数作为数据库管理器代码的一部分执行。这可能会带来性能提升，但必须确保 UDF 不会损坏数据库管理器的存储。创建非隔离函数的能力通过 DB2 权限进行控制。

在 UNIX 系统上，被隔离的 UDF 可以在不同于实例 USERNAME 的用户名下运行。在创建实例时，必须在 `DB2CRT` 命令中指定 UDF USERNAME。

创建 UDF 时可能定义的其他子句还包括：

- `DETERMINISTIC`（确定性）或 `NOT DETERMINISTIC`（非确定性）函数在用相同参数调用时将产生或不会产生不同的结果。例如，随机函数将被定义为 `NOT DETERMINISTIC`。
- `EXTERNAL ACTION`（外部操作）定义数据库管理器，该函数可以执行数据库外部的操作。例如，向开发团队发送消息的函数就具有 `EXTERNAL ACTION`。

## 参考文献

可以在何处获取更多 DB2 信息？
万维网
IBM 互联网连接网站

```
http://www.ibm.net
```

互联网“意见请求”（RFC）编辑器器
http://www.isi.edu/rfc-editor/

IBM 学习服务网站
//www-3.ibm.com/services/learning

```
http://www.isi.edu/rfc-editor/
```

IBM DB2 和商业智能技术会议网站
http://www-3.ibm.com/services/learning/conf/db2
ITSO Redbooks 网站
http://www.redbooks.com

```
//www-3.ibm.com/services/learning
```

DB2 支持网站
http://www-4.cgi-bin/db2www/data/db2/udb/winos2unix/support/index.d2w/report
DB2 信息网站
http://www-4.software.ibm.com/data/db2
DB2 技术库网站
http://www-4.software.ibm.com/data/db2/library
DB2 认证网站
http://www-1.ibm.com/certify
CompuServe
IBM DB2 家族论坛 (GO IBMDB2)
互联网新闻组
comp.databases.ibm-db2
bit.listserv.db2-l

```
http://www-3.ibm.com/services/learning/conf/db2
```

```
http://www.redbooks.com
```

```
http://www-4.cgi-bin/db2www/data/db2/udb/winos2unix/support/index.d2w/report
```

```
http://www-4.software.ibm.com/data/db2
```

```
http://www-4.software.ibm.com/data/db2/library
```

```
http://www-1.ibm.com/certify
```
