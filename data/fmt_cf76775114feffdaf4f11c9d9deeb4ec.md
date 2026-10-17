
## Select tableid,tbpace,substr(definer,1,18) as definer,substr(tbpace,1,18) as tbpace,tbodytype from syscat.tables order by 1,2,3

| TABLEID | DEFINER | TBSPACE | TBPSYTYPE |
|---|---|---|---|
| 0 | SYSISM | SYSSCATCH1 | S |
| 1 | SYSISM | TMPSPACE1 | S |
| 2 | SYSISM | USERSPACE1 | D |
| 4 | IN101 | DBMS02 | D |
| 5 | IN101 | DBMS03 | D |
| 6 | IN101 | DBMS04 | D |
| 7 | IN101 | DBMS05 | D |
| 8 | IN101 | DBMS06 | D |
| 9 | IN101 | DBMS01 | S |

图 4.3 表与表之间的关联。

这些信息中需要注意的几点：首先是图 4.4 中高亮的行。你可以看到有 4 个 `TABLEID` 为“4”的表，但它们位于 4 个不同的空间中。`SYSISM.SYSINDEXES` 位于 `TBPACE` 0，或者（查看图的底部），`SYSCAT.INST101.ARTISTS` 位于 `TBPACE` 3，或 `DBMS01`；`INST101.ALB` 位于 `TBPACE` 6，或 `DBMS04`。

第二点注意的是表的 `TYPE`——即显示的“V”表示视图（View），“T”表示表（Table）。你也可以在这一列中看到 `A`。对于表来说，`TBSPACEID` 有意义，而对于视图，`TBSPACEID` 始终显示为“0”。但想一下——视图的数据存储位置与基础表数据存储的位置相同。因此，不要看到 `TBSPACE` 列就认为在 `SYSCAT` 表空间中有用于视图的行和列。

以下 SQL 语句连接了信息：

```sql
select tableid, tbchema, tablename, type, b.tbpace, b.definer, b.tbpace, btbodytype from syscat.tables t, syscat.tables b
where b.tbpace = t.tbpace and t.type = 'T' order by 1, 4
```

## DB2 对象

在本节中，学生将学习如何创建 DB2 对象——表、视图、索引、别名、引用完整性、检查约束和触发器。

## 创建 Schema—GUI

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_131_0.png)

图 4.4 创建 Schema—GUI。

从控制中心（Control Center）访问创建 Schema GUI（图 4.4）：

- 选择 Schemas（右鼠标点击）
- 选择 Create（创建）

创建 Schema GUI 包含以下内容：

- Schema 名称（Schema name）
- 授权名称（Authorization name）
- 注释（Comment）

所有生成 SQL 或 DB2 命令的控制中心对话框都提供了“显示 SQL”或“显示命令”按钮。你可以显示 SQL 语句或命令并将其保存为脚本。

当使用 `CREATE SCHEMA` 语句显式创建 schema 时，schema 所有者将获得该 schema 的 `CREATEIN`、`DROPIN`、`ALTERIN` 权限，并具有将这些权限授予其他用户的能力。schema 名称不能以 `SYS` 开头。

让我们创建 schema 的语句。

## 创建 Schema—语句

图 4.5 所示的语句（`CREATE SCHEMA AND COMMENT ON`）如果你在图 4.4 所示的 GUI 上点击 `SHOW STATEMENT` 时会看到的语句。

## 创建对象 | 115

```sql
CREATE SCHEMA PAYROLL AUTHORIZATION KEITH;
COMMENT ON Schema PAYROLL IS
'schema for payroll application';
```

图 4.5 创建 Schema—语句。

在将数据组织成表时，将表（以及其他相关对象）组合在一起可能也有益。这是通过定义一个 schema 实现的。关于 schema 的信息保存在你所连接的数据库的系统目录表中。随着其他对象的创建，它们可以被放在此 schema 中。

持有 `SYSADM` 或 `DBADM` 权限的授权 ID 可以用任何有效的 schema 名称或授权名称创建 schema。任何 ID 都可以显式创建一个与语句授权 ID 匹配的 schema。授予授权名称的权限将在安全章节中详细介绍。

schema 名称或授权名称不能以 `SYS` 开头。

当使用 `CREATE SCHEMA` 语句显式创建 schema 时，schema 所有者将获得该 schema 的 `CREATEIN`、`DROPIN`、`ALTERIN`、`GRANTIN` 权限，并具有将这些权限授予其他用户的能力。你可以创建一个 schema 并在其中包含某些 SQL 语句（`CREATE TABLE`，排除类型表和物化视图；`CREATE VIEW` 语句，排除类型视图；`CREATE INDEX` 语句；`COMMENT` 语句；`GRANT` 语句）。例如，以下是单个语句：

```sql
CREATE SCHEMA PERS
CREATE TABLE PERS (DEPTNUM SMALLINT NOT NULL,
DEPTNAME VARCHAR(14),
MANAGER SMALLINT,
DIVISION VARCHAR(10),
LOCATION VARCHAR(13),
CONSTRAINT PKKEY PRIMARY KEY (DEPTNUM),
CONSTRAINT FKEYMGR
FOREIGN KEY (MANAGER) 
REFERENCES STAFF (ID) )
CREATE TABLE STAFF (ID SMALLINT NOT NULL,
NAME VARCHAR(9),
DEPT SMALLINT,
JOB VARCHAR(5),
YEARS SMALLINT,
SALARY DECIMAL(7,2),
COMM DECIMAL(7,2)),
```

## 116 DB2 通用数据库：Linux、Unix 和 Windows 管理

```sql
CONSTRAINT PKEYID
PRIMARY KEY (ID) ),
CONSTRAINT FKEYNO
FOREIGN KEY (DEPT)
REFERENCES (DEPTNUM ) );
```

因此，你可以使用单个语句创建两个相互依赖的表，而无需先创建主键表，再创建带外键表，最后修改第一个以添加外键。`CREATE SCHEMA` 语句中的任何未限定对象名通过创建的 schema 名称进行隐式限定。

## 设置当前 Schema

在这里，我们将识别如何使用 `CURRENT SCHEMA` 寄存器。

```sql
connect to mydbdb user Keith
select * from employee

select from KEITH.EMPLOYEE

set current schema = 'PAYROLL'
select * from employee

select from PAYROLL.EMPLOYEE Current Schema.
```

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_133_0.png)

当使用 `CREATE SCHEMA` 语句显式创建 schema 时，schema 所有者将获得该 schema 的 `CREATEIN`、`DROPIN`、`ALTERIN`、`GRANTIN` 权限，并具有将这些权限授予其他用户的能力。你可以创建一个 schema 并在其中包含某些 SQL 语句（`CREATE TABLE`，排除类型表和物化视图；`CREATE VIEW` 语句，排除类型视图；`CREATE INDEX` 语句；`COMMENT` 语句；`GRANT` 语句）。例如，以下是单个语句：

## 创建对象 | 119

```sql
connect to musicdb;
create table artists
(
artno    smallint not null,
name            varchar(50) with default 'abc',
classification    char(1) not null,
bio               clob(100K) logged,
picture           blob(10M) not logged compact)

in dms01
index in dms02
long in dms03;
```
