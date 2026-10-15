
- `GRANT EXEMPTION ON RULE DB2LBACWRITEARRAY WRITEUP FOR sec_policy TO user1`
- `GRANT EXEMPTION ON RULE DB2LBACWRITEARRAY WRITEUP FOR sec_policy TO user1`

## 答案

### 问题 1

正确答案是 C。大多数用户在访问 DB2 实例之前通过的第一个安全门户是身份验证过程。身份验证的目的是验证用户确实是他们所称的。一旦用户通过验证并建立了与数据库的连接，DB2 数据库管理器将评估分配给用户的所有权限和特权，以确定允许用户执行的操作。

### 问题 2

正确答案是 B。类似于系统管理员 `SYSADM`、系统控制 `SYSCTRL` 和系统监控 `SYMON` 权限，系统维护 `SYSMAINT` 权限只能授予 DB2 实例配置中 `sysaint_group` 参数指定的组名。

### 问题 3

正确答案是 D。为了连接并操作特定的数据库，用户必须拥有使用该数据库所需的权限和特权。因此，每创建一个新数据库时，除非另有规定，会自动授予以下权限和特权：

* 数据库管理员 `DBADM` 权限以及 `CONNECT`, `CREATAB`, `BINDADD`, `CREATE_NOT_FENCED`, `IMPLICIT_SCHEMA` 和 `LOAD` 权限授予创建数据库的用户。
* 表空间 `USSPACE1` 的 `USE` 权限授予该组。
* `CONNECT`, `CREATAB`, `BINDADD` 和 `IMPLICIT_SCHEMA` 权限授予 `PUBLIC` 组
* 每个系统目录表的 `SELECT` 权限授予 `PUBLIC` 组。

# 第8 章：安全

- `SYSIBM` 架构中所有过程的 `EXECUTE` 权限授予 `PUBLIC` 组。
- `SYSFUN` 架构中所有函数的 `EXECUTE WITH GRANT` 权限授予 `PUBLIC` 组。
- 每个绑定工具的 `BIND AND EXECUTE` 权限授予 `PUBLIC` 组。

（欲需更多信息，请参阅第 3 章“数据放置”）

### 问题 4

正确答案是 D。`CONTROL` 视图权限为用户提供了所有可用权限，允许用户从数据库中删除 `drop` 视图，并赋予用户向其他用户和组授予或撤销一个或多个视图权限 `CONTROL` 权限除外 的能力。

### 问题 6

正确答案是 C。`GRANT ALL PRIVILEGES` 语句为 `USER1` 赋予了 `EMPLOYEE` 表的以下权限：`ALTER`、`SELECT`、`INSERT`、`UPDATE`、`DELETE`、`INDEX` 和 `REFERENCES`。要删除索引，`USER1` 需要对该索引拥有 `CONTROL` 权限，而不是该索引所基于表；`USER1` 无法向其他用户授予权限，因为在赋予 `USER1` 表权限的 `GRANT ALL PRIVILEGES` 语句没有指定 `WITH GRANT OPTION` 子句；而且为了删除 `EMPLOYEE` 表，`USER1` 必须拥有该表的 `CONTROL` 权限——`GRANT ALL PRIVILEGES` 语句并未授予 `CONTROL` 权限。

### 问题 7

正确答案是 B。当赋予用户特定数据库的数据库管理员 `DBADM` 权限时，他们将自动获得该数据库所有用的数据库权限 `CONNECT`、`QUIESCE`、`IMPLICIT_SCHEMA`、`CREATAB`、`BINDADD`、`CREATE_EXTERNAL_ROUTINE`、`CREATE_NOT_FENCED_ROUTINE` 和 `LOAD`。当撤销数据库管理员权限时，那些在授予 `DBADM` 权限时隐含和自动授予的所有其他数据库权限不会自动撤销。对数据库中对象拥有的权限也是如此。

### 问题 8

正确答案是 A 和 C。在用户调用例例 用户定义函数、存储过程或方法 之前，他们必须拥有该例例的 `EXECUTE` 权限以及该例例所需的任何权限。因此，为了执行查询表的存储过程，用户必须同时拥有该存储过程的 `EXECUTE` 权限以及对查询运行目标表的 `SELECT` 权限。

包权限控制用户对特定包可以做什么和不能做什么。 包是一个包含 DB2 数据库管理器所需的信息的对象，以便代表嵌入式 SQL 应用程序以最高效率处理 SQL 语句。

## 702 第 8 章：安全

## 问题 9

正确答案是 A。`ALTER table` 权限允许用户对表执行 `ALTER TABLE` SQL 语句。换句话说，此权限允许用户向表中添加列、添加或更改与表或其任何列相关的注释、为表创建或删除主键、为表创建或删除唯一约束、为表创建或删除检查约束、为表创建或删除引用约束，以及为表创建或删除触发器 前提是用户拥有触发器所引用的每个对象的相应权限。

`UPDATE` 权限允许用户对表执行 `UPDATE` SQL 语句。换句话说，这允许用户修改表中的数据。`DELETE` 权限允许用户对表执行 `DELETE` SQL 语句。换句话说，它允许用户从表中删除数据行。

## 问题 10

正确答案是 B。`BIND` 数据库权限允许用户在数据库中创建包 通过针对数据库预编译嵌入式 SQL 应用程序源代码文件，或通过将应用程序绑定文件绑定到数据库来实现。

`BIND package` 权限允许用户对已绑定到数据库的包进行重新绑定或添加新的包版本。 除了 `BIND package` 权限外，在包成功重新绑定之前，用户必须拥有执行构成该包的 SQL 语句所需的权限。 `CREATE_EXTERNAL_ROUTINE` 数据库权限允许用户创建外部例例 如用户定义函数 UDFs 和/或过程，并将其存储在数据库中，以便其他用户和应用程序可以使用它们。 `CREATE_NOT_FENCED_ROUTINE` 数据库权限允许用户创建非围栏 unfenced UDF 和/或过程并将其存储在数据库中。 被认为足够“安全”可以在 DB2 数据库管理器运行环境进程或地址空间中运行的非围栏 UDF/过程。除非 UDF/例例被注册为非围栏，否则 DB2 数据库将隔离 UDF/例例的内部资源，使其无法在 DB2 数据库管理地址空间中运行

## 问题 11

正确答案是 C。`GRANT` 语句不会检查要授予权限和权利的用户和/组的名称是否有效。因此，可能向不存在的用户和组授予权限和权利。

## 问题 12

正确答案是 B。授予唯一可用存储过程权限的语法如下：

```
GRANT EXECUTE ON [RoutineName] |
[PROCEDURE <SchemaName.> *]
TO [Recipient, ...]
<WITH GRANT OPTION>
```

用于撤销唯一可用存储过程权限的语法如下：

```
REVOKE EXECUTE ON [RoutineName] |
[PROCEDURE <SchemaName.> BY ALL]
FROM [Forfeiter, ...] <BY ALL>
RESTRICT
```

其中：

- *RoutineName*：通过名称标识与 `EXECUTE` 权限关联的例例 用户定义函数、方法或存储过程。
- *TypeName*：通过名称标识找到特定方法的类型。
- *SchemaName*：通过名称标识所有函数、方法或过程 包括未来可能创建的 将要被授予 `EXECUTE` 权限的模式。
- *Recipient*：标识要接收 `EXECUTE` 权限的用户和/或组的名称。`Recipient` 参数指定的值可以是以下任何组合：`<USER> {Username}`、`<GROUP> {GroupName}` 和 `PUBLIC`。
- *Forfeiter*：标识要接收 `EXECUTE` 权限的用户和/或组的名称 此处应为撤销权限者。`Recipient` 参数指定的值可以是以下任何组合 此处原文有误。

因此，授予存储过程权限的正确方法是使用 `GRANT` 语句。

## 问题 13

正确答案是 A。要使用标签访问控制 `LBAC` 限制行的访问，你必须定义安全标签、定义安全策略，并将安全标签授予相应的 LBAC 配置文件。

## 问题 14

正确答案是 C。安全管理员 `SECADM` 权限是一种特殊的数据库权限，允许特殊用户配置各种标签访问控制 `LBAC` 元素，以限制对表的访问。具有安全管理员权限的用户被允许：

- 创建和删除安全策略。
- 创建和删除安全标签。
- 向用户授予/撤销安全标签 使用 `GRANT SECURITY LABEL` 和 `REVOKE SECURITY LABEL` 语句。
- 授予和撤销 LBAC 规则免权。
- 授予和撤销 `SESSIONUSER` 权限 使用 `GRANT SESSIONUSER` 语句。
- 转移非安全管理员拥的所有对象 使用 `TRANSFER OWNERSHIP` 语句。

没有其他权限为用户提供这些能力。

## 问题 15
