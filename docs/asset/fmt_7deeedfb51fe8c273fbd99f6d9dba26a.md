
## O. 实例使用的操作系统

## O. 实例使用的通信配置

## O. DB2 注册

## O. DB2 数据库管理器配置

# 问题 141

用户 `USER1` 想要调用一个动态从表中检索数据的 SQL 存储过程。为了调用该存储过程，`user1` 必须拥有哪两个权限？

☐ A. 存储过程的 `EXECUTE` 权限

☐ B. 存储过程的 `CALL` 权限

☐ C. 存储过程检索数据的表的 `SELECT` 权限

☐ D. 存储过程包的 `EXECUTE` 权限

☐ E. 存储过程的 `SELECT` 权限

## 问题 142

以下语句的作用是什么？

`GRANT ALTER ON SEQUENCE gen_empid TO user1 WITH GRANT OPTION`

- A. 赋予 `USER1` 更改与名为 `GEN_EMPID` 的序列相关的注释的权限，以及向其他用户和组授予该序列的 `CONTROL` 权限的能力。
- B. 赋予 `USER1` 更改与名为 `GEN_EMPID` 的序列关联的 `PREVIOUS_VALUE` 和 `NEXT_VALUE` 表达式返回值的权限，以及向其他用户和组授予该序列的 `CONTROL` 权限的能力。
- C. 赋予 `USER1` 更改与名为 `GEN_EMPID` 的序列相关的注释的权限，以及向其他用户和组授予该权限的能力。
- D. 赋予 `USER1` 更改与名为 `GEN_EMPID` 的序列关联的 `PREVIOUS_VALUE` 和 `NEXT_VALUE` 表达式返回值的权限，以及向其他用户和组授予该权限的能力。

## 问题 143

关于 `DB2` 安全，以下哪种陈述**不**正确？

- A. 如果使用 Microsoft Active Directory 验证用户，则必须创建一个自定义安全插件。
- B. 只有具有 `Security Administrator`（安全管理员）权限的用户才被允许授予和撤销 `SETSESSIONUSERPRIVILEGES`。
- C. 用户和组在授予权限之前必须存在。
- D. 如果一个拥有表 `SELECT` 权限的用户基于该表创建了视图，并且随后其 `SELECT` 权限被撤销，则该视图将仍然可运行。

## 问题 144

以下哪种 SQL 语句允许名为 `USER1` 的用户写入 `LBAC` 保护列，这些列由 `LBAC` 标签保护，且该标签的安全级别低于 `USER1` 所有的级别？

- A. `GRANT EXCEPTION ON RULE DB2LBACWRITEARRAY WRITEDOWN FOR sec.policy TO USER user1`
- B. `GRANT EXCEPTION ON RULE DB2LBACWRITEARRAY WRITEDOWN FOR sec.policy TO USER user1`
- C. `GRANT EXCEPTION ON RULE DB2LBACWRITEARRAY WRITEUP FOR sec.policy TO USER user1`
- D. `GRANT EXCEPTION ON RULE DB2LBACWRITEARRAY WRITEUP FOR sec.policy TO USER user1`

## 附录 B：示例测试

## 问题 145

在创建数据库时，以下哪些数据库权限**没有**自动授予给 `PUBLIC` 组？

A. `CONNECT`

B. `BINDADD`

C. `IMPLICIT_SCHEMA`

D. `CREATE_EXTERNAL_ROUTINE`

## 问题 146

用户名为 `USER1` 被授予了 `DBADM` 权限。假设没有授予其他权限/权利，并且已从 `PUBLIC` 组撤销所有权限，如果执行了以下 SQL 语句：

`REVOKE DBADM ON DATABASE FROM user1`

用户 `USER1` 将拥有哪些权限/权利？

A. 无（None）

B. `CONNECT`

C. `SYSCTRL`

D. `CREATETAB`

## 问题 147

用户 `USER1` 需要从 `SALES` 数据库中删除名为 `ORDERS_V` 的视图，该视图基于名为 `ORDERS` 的表。假设用户 `USER1` 不持有任何权限，在允许用户 `USER1` 删除该视图之前，必须授予哪些权限？

A. `ORDERS_V` 视图的 `DROP` 权限

B. `ORDERS` 表的 `CONTROL` 权限

C. `ORDERS_V` 视图的 `DROP` 权限

D. `ORDERS_V` 视图的 `CONTROL` 权限

## 问题 148

以下哪些权限允许用户为嵌入式 SQL 生成包并将其存储在数据库中？

- A. `BIND`
- B. `BINDADD`
- C. `CREATE_EXTERNAL_ROUTINE`
- D. `CREATE_NOT_FENCED_ROUTINE`

## 问题 149

`USER1` 拥有调用名为 `GEN_RESUME` 的存储过程所需的权限。`User2` 需要能够调用该过程——而用户 `USER1` 和 `PUBLIC` 组的所有成员不应再被允许调用该过程。使用以下哪些语句可以实现这一目标？

- A. `GRANT EXECUTE ON ROUTINE gen_resume TO user2 EXCLUDE user1, PUBLIC`
- B. `GRANT EXECUTE ON PROCEDURE gen_resume TO user2; REVOKE EXECUTE ON PROCEDURE gen_resume FROM user1, PUBLIC;`
- C. `GRANT CALL ON ROUTINE gen_resume TO user2 EXCLUDE user1, PUBLIC`
- D. `GRANT CALL ON PROCEDURE gen_resume TO user2; REVOKE CALL ON PROCEDURE gen_resume FROM user1, PUBLIC;`

## 问题 150

关于基于标签的访问控制 (`LBAC`)，以下哪种陈述**不**正确？

- A. `LBAC` 可用于限制对单行和单列的访问。
- B. 被授予不同 `LBAC` 安全标签的用户在执行相同查询时将获得不同的结果。
- C. 只有具有 `SYSADM` 或 `SECADM` 权限的用户才被允许创建安全策略和安全标签。
- D. 安全标签组件代表可能用于判断用户是否应该访问特定数据的标准。

## 答案

### DB2 服务器管理

#### 问题 1

正确答案是 C。系统的默认实例由 `DB2INSTANCE` 环境变量定义，在许多情况下，该实例是执行所有实例级操作的实例。如果你需要对另一个实例执行操作，必须首先更改分配给 `DB2INSTANCE={InstanceName}` 的值（在 Linux 和 UNIX 上使用 `export DB2INSTANCE={InstanceName}`），其中 `InstanceName` 是分配给你想作为默认实例的实例名称，或者你必须连接到该实例。

#### 问题 2

正确答案是 B。`MAXAGENTS` `DB2` Manager 配置参数用于指定同时存在的最大代理数量。（代理促进了应用程序与数据库之间的操作。）`NUM_AGENTS` 指定 `DB2` Manager 启动时创建的空闲代理数量；`MAX_COORDINENTS` 指定节点上可以存在的协调代理的最大数量；而 `MAXAGENTS` 指定无论使用哪个数据库，其最大数量。

#### 问题 3

正确答案是 C。可以通过执行 `UPDATE DATABASE CONFIGURATION` 命令更改特定数据库配置参数的值。该命令的语法为：

```
UPDATE [DATABASE | DB]
[CONFIGURATION | CONFIG | CFG]
```

其中：

+ `DatabaseAlias` 指定要修改信息的数据库别名。
+ `Parameter` 指定要修改的配置参数（通过关键字）。（许多情况下，参数关键字与参数名称相同。）
+ `Value` 指定分配给指定配置参数的新值。

如果在 `UPDATE DATABASE CONFIGURATION` 命令中使用 `DEFERRED` 子句，对数据库配置的更改将在所有到相应的连接终止并建立新连接之前生效。如果使用 `IMMEDIATE` 子句或未指定任何子句，对数据库配置的所有更改将立即生效——前提是资源可用。

#### 问题 4

正确答案是 C。除了启用远程管理 `DB2` 服务器外，`DAS` 实例启动 `Control Center` 和 `Configuration Assistant`，提供了发现其他 `DAS` 实例配置以及使用 `DB2 Discovery` 的数据库信息的手段。（`Configuration Assistant` 和 `Control Center` 使用此类信息来简化和自动化客户端到 `DB2` 服务器的配置；如果服务器的 `DAS` 实例未运行，这两个工具都无法发现它。）如果 `DAS` 配置参数设置为 `SEARCH`，服务器将响应搜索和已知发现请求；如果此参数设置为 `KNOWN`，则服务器将仅响应已知发现请求；如果设置为 `DISABLE`，则服务器将不响应发现请求。
