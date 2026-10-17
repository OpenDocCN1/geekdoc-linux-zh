
## DECLARE GLOBAL TEMPORARY TABLE table_name

```
      .-*-,--

V                                                      |

-->--+----------column-definition----------++--)-->

|   '-LIKE--table_name--+------------------+'             |

      '-view-name--+' '-copy-options-'                   |

+LIKE--table_name--+------------------------------------+

|      '-view-name--+' '-copy-options-'                   |

|      '-as-subquery-clause--'                          |

------------------------------------------------------

V                                                      |

-->--WITH REPLACE--+------------------------<

|   '-ON COMMIT DELETE ROWS---. |

+---------------------------------------+

|   '-ON COMMIT PRESERVE ROWS-' |

+------------------------------------------------------+

-->------------------------------------------------------+

|       '-ON ROLLBACK DELETE ROWS---. |

'-NOT LOGGED--+---------------------------------------+'

      '-ON ROLLBACK PRESERVE ROWS-'
```

图 10.9 iSeries 的 `DECLARE GLOBAL TEMPORARY TABLE` 语法。

## 第 10 章 利用 DB2 应用开发特性

```
>>--DECLARE GLOBAL TEMPORARY TABLE--table-name------------------------------------>

------------------------------------------------------------------------------------------------------

V|

--+(+--column-definition--++--COLUMN ATTRIBUTES---

|

|--EXCLUDING IDENTITY--||

|--LIKE----table-name-----||

|   |--view-name-----|       --COLUMN ATTRIBUTES--||

|   |--INCLUDING IDENTITY--||

||--AS--(fullselect)--WITH NO DATA--|

|                   |--copy-options--|

------------------------------------------------------------------------------------------------------

V++--ON COMMIT DELETE ROWS--+--------------------------------->

| |--ON COMMIT PRESERVE ROWS--|

|'--ON COMMIT DROP TABLE----|

|'------CCSID--+ASCII-------+'

|       |--EBCDIC-|

|       '--UNICODE--'|
```

**图 10.10** zSeries 的 `DECLARE GLOBAL TEMPORARY TABLE` 语法。

图 10.11 显示了声明临时表的示例。`tempnewproj projno CHAR(6)`

```sql
DECLARE GLOBAL TEMPORARY TABLE session.tempnewproj 
               projname VARCHAR(24)
               projsdate DATE
               projedate DATE
               category VARCHAR(100) 
               desc VARCHAR(100) )
ON COMMIT PRESERVE ROWS      -- 适用于 LUW 和 iSeries
NOT LOGGED
ON ROLLBACK PRESERVE ROWS  -- 适用于 LUW 和 iSeries
WITH REPLACE                -- 适用于 LUW 和 iSeries
IN usertemspace             -- 适用于 LUW
```

**图 10.11** 声明临时表的示例。

### 全临时表

该示例演示了创建一个名为 `tempnewproj` 的临时表。列和数据类型的显式定义方式与定义标准表的方式相同。

在 LUW 上，临时表不支持 BLOB、DBCLOB、LONG VARCHAR、LONG VARGRAPHIC、DATALINK、引用类型和结构化类型。在 zSeries 上，临时表支持所有内置数据类型，但 BLOB、CLOB、DBCLOB 和 ROWID 类型除。在 iSeries 上，支持 BLOB、DBCLOB、VARCHAR、VARGRAPHIC 和 DATALINK，但有细微限制。

iSeries SQL 参考用于用于为临时表指定临时表空间，且仅适用于 DB2 LUW。如果不指定，DB2 将默认选择一个。适用于 iSeries 的 DB2 UDB 没有表空间的概念，而在 zSeries 上，临时表创建在属于 TEMP 数据库的具有适当页面的表空间中。为了可移植性，请在临时表定义中省略此项。

在同一会话中声明另一个同名的临时表之前，必须先删除现有的临时表。可以通过显式使用 `DROP` 命令来实现。

```sql
DROP TABLE session.tempnewproj
```

在 DB2 LUW 和 iSeries 上，可以使用 `REPLACE` 选项，如图 10.8 所示。使用此选项时，您应该声明一个同名的表（在同一会话中），DB2 将自动删除现有的临时表并用新定义重新创建。`REPLACE` 选项在连接池环境中（连接返回到池中而不是由应用程序释放）特别有用。由于连接池，当连接返回到池中时，之前使用的临时表可能尚未被删除。使用 `REPLACE` 可以确保下次使用该池连接的应用程序不会获取到上一次使用留下的数据。

`COMMIT` 子句允许您指定在提交时是保留还是删除临时表中的数据。默认行为是在提交时刷新临时表的内容。

`NOT LOGGED` 子句用于指示该表中的数据更改不记录（以提高性能）。在 zSeries 上，需要最少日志，且目前不支持 `NOT LOGGED` 子句。

还有其他声明临时表的方法，例如：

```sql
DECLARE GLOBAL TEMPORARY TABLE TEMP_EMPLOYEE LIKE EMPLOY
```

通常，临时表的形式与真实表相同，因为您使用它们来从另一个表中提取子集数据进行处理。图 10.11 展示了如何使用 `LIKE` 子句来轻松地实现这一点。这种简单性的主要优势是不需要为临时表提供列定义。源表定义可以是真实表、另一个临时表、视图或别名（针对远程表）。只有列名、其类型和可空属性会被复制。索引和约束不会被复制。

图 10.12 阐了声明临时表的另一种方法。全选择（full select）的列名和类型决定了临时表的结构。临时表不会通过 `SELECT` 语句填充。

```sql
DECLARE GLOBAL TEMPORARY TABLE TEMP_EMPDEP AS
(SELECT E.FIRSTNAME, E.LASTNAME, D.DEPTNAME
FROM EMPLOYEE E, DEPARTMENT D WHERE E.WORKDEPT=D.DEPTNO)
DEFINITION ONLY
-- 在 Series 和 iSeries 上，这是 WITH NO DATA 的同义词
```

**图 10.12** 使用全选择声明临时表。

### 在 SQL 过程中使用临时表

您可以在 SQL 过程中声明、操纵和删除临时表。图 10.13 展示了在存储过程上下文中声明和使用临时表的基本元素。它还强调了一个并非显而易见的潜在问题。

```sql
CREATE PROCEDURE temp_table_demo()
LANGUAGE SQL
SPECIFIC temp_table_demo -- 适用于 LUW 和 iSeries
-- WLM ENVIRONMENT <env>             -- 适用于 zSeries
DYNAMIC RESULTS 1
BEGIN
DECLARE v_sql VARCHAR(100) DEFAULT 'SELECT * FROM temp_table';
DECLARE GLOBAL TEMPORARY TABLE
session.temp_table (id INT, value VARCHAR(10))
ON COMMIT PRESERVE ROWS;
INSERT INTO session.temp_table VALUES (1,'a');
INSERT INTO session.temp_table VALUES (2,'b');
INSERT INTO session.temp_table VALUES (3,'c');
PREPARE stmt FROM v_sql;
OPEN c_cur;
END
```

**图 10.13** 使用临时表的简单示例。

### 在过程之间共享临时表

本节演示了如何在过程之间共享临时表。示例的设计使其能够在所有平台上运行。

在引用临时表之前，必须先对其声明，以便 DB2 了解其结构。当临时表与其引用的位置不同时会出现复杂情况。考虑以下场景：

- 应用程序想要声明表 `T`，填充它，然后调用过程 `P` 处理数据。应用程序和过程 `P` 如何引用 `T` 而无需重新声明？
- 存储过程 `P1` 可能声明一个临时表 `T`，填充它，并希望过程 `P2` 和 `P3` 引用 `P1` 中的临时表而它们无需重新声明？

在这两种情况下，在同一会话中重新声明临时表都会导致 `SQLSTATE 42710`（对象已存在），或者如果指定了 `REPLACE`，则第一个表会被随后的声明替换。

解决此问题的方法是意识到声明和引用不需要包含在同一个过程体中。唯一的要求是临时表必须在过程构建时在当前会话中声明。在下面的示例中，将演示两个过程共享一个名为 `SESSION.temp` 的临时表。

图 10.14 显示了一个名为 `init_temp` 的过程，它仅封装了临时表 `SESSION.temp` 的声明。

```sql
CREATE PROCEDURE init_temp()
LANGUAGE SQL
SPECIFIC init_temp                -- 适用于 LUW 和 iSeries
-- WLM ENVIRONMENT <env>             -- 适用于 zSeries
it: BEGIN
DECLARE GLOBAL TEMPORARY TABLE
```

## 第 10 章利用 DB2 应用开发特性

```
session.temp (id INT, data VARCHAR(10))  --适用于 LUW 和 iSeries
WITH REPLACE
ON COMMIT PRESERVE ROWS;
```

结束

### 图 10.14 用于封装临时表声明的存储过程。

使用存储过程初始化临时表具有三个主要优势：

- 它允许为 DB2 开发中心所使用的数据库连接轻松地声明临时表。
- 存储过程无需在应用程序代码（可能由他人维护）中查找临时表的 DDL。
- 如果在应用程序代码的多个位置可能实例化同一个临时表，则该表的定义被集中在一个地方。

通过 `init_temp` 过程，可以相对容易地管理一个构建共享临时表的存储过程的环境。只要在当前数据库连接中先执行 `init_temp`，你就可以构建一个引用该临时表的存储过程。

为了与 `init_temp` 互补，如图 10.15 所示，定义一个用于删除临时表的存储过程。这对于 zSeries 来说是必要的，因为该平台目前不支持 `REPLACE` 选项。在 LUW 或 iSeries 上，如果当前会话中存在 `SESSION.temp` 临时表，调用 `init_temp` 会自动删除任何现有表。

```
CREATE PROCEDURE close_temp()
LANGUAGE SQL
SPECIFIC CLOSE_TEMP  --适用于 LUW 和 iSeries
-- WLM ENVIRONMENT <env> --适用于 zSeries
BEGIN
DROP TABLE SESSION.TEMP;
END
```

### 图 10.15 用于封装删除临时表的存储过程。

使用存储过程删除临时表具有以下两个优势：

- 它允许人们在 DB2 开发中心工作时删除会话的临时表。
- 它通过存储过程完成了对临时表声明的封装。

### 声明的全局表

要构建图 10.16 所示的 `insert_to_temp` 过程，请执行 `init_temp` 过程。注意 `insert_to_temp` 静态地引用了 `SESSION.temp`，但其体内并不包含 `DECLARE TEMPORARY TABLE`。

```
CREATE PROCEDURE insert_to_temp()
LANGUAGE SQL
  SPECIFIC insert_to_temp --适用于 LUW 和 iSeries
  --LUW ENVIRONMENT <env> --适用于 zSeries
BEGIN
  INSERT INTO SESSION.TEMP VALUES (1, 'one');
  INSERT INTO SESSION.TEMP VALUES (2, 'two');
  INSERT INTO SESSION.TEMP VALUES (3, 'three');
END
```

**图 10.16** 一个在没有声明的情况下引用临时表的存储过程。

另一个过程图 10.17 所示的 `show_rows` 共享临时表数据。它将临时表的内容返回给应用程序。

```
CREATE PROCEDURE show_rows()
LANGUAGE SQL
  SPECIFIC show_rows --适用于 LUW 和 iSeries
  --LUW ENVIRONMENT <env> --适用于 zSeries
DYNAMIC RESULT SETS 1
BEGIN
  DECLARE cur CURSOR WITH HOLD RETURN TO CALLER FOR
    SELECT * FROM session.temp;
OPEN cur;
