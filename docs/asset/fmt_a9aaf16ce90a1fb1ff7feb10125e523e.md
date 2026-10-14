
为了进行此真实测试，首先完全退出你的 SQL*Plus 会话，然后重新进入。这将确保你的会话是全新的。然后，执行 `SET SERVEROUTPUT ON`，并运行列表 29.11 所示的匿名块。注意，该块并没有启用输出；该功能是在包初始化代码中执行的。调试标志（其值通常默认为 `NULL`）在初始也会被重置。服务器响应如下：

`DEBUG status is initially: FALSE`
`DEBUG status is now: TRUE`
`DEBUG status is now: FALSE`
`DEBUG status is finally: TRUE`

`PL/SQL procedure successfully completed.`
现在再次运行。
`DEBUG status is initially: TRUE`
`DEBUG status is now: TRUE`
`DEBUG status is now: FALSE`
`DEBUG status is finally: TRUE`

`PL/SQL procedure successfully completed.`

注意初始调试标志的值为 `TRUE`。该值从上一次程序运行传递到下一次。如果你重新连接，你实际上拥有一个新的会话，包初始化将再次执行。记住，代码在内存中是静态的，但每个用户都会获得一组全新的本地的私有变量。运行第二个 SQL*Plus 会话并验证这一点。

# 关于提供的 Oracle8i 数据库包

除了为 Oracle8i 服务器提供基本功能（作为你的基本子类型声明和数据类型转换程序）的 `STANDARD` 包外，还有一组供 DBA 和开发者使用的包。这些包通过它们的名称进行区分，名称以 `DBMS_` 或 `STL_` 开头，意味着它们与数据库或通用实用程序进行交互。首先，你将快速浏览这些包，之后对其进行详细检查。

## 服务器内部的交互

大多数提供的 Oracle8i 包在服务器环境内的数据工作：数据字典项、用户数据库对象，或仅存在于系统全局区域（`SGA`，共享内存池）的对象。通过这些包，你可以管理快照、重新编译程序单元、在数据库条目更改时生成异步警报、运行作业等。

许多此类包与数据库应用程序内置的功能衔接，或者通过可加载的外部模块（如 `DLL`）扩展数据库环境。并不要求、也没有必要你理解或使用这些模块入口点。我甚至可以说，你不应该尝试直接使用它们，而是应该通过所提供的 `PL/SQL` 编程接口来使用。

## 服务器外部的交互

某些包向调用上下文提供反馈，或其他向外部过程提供接口。例如，Oracle8i 的管道（pipe）功能被设计为会话间通信的方法，严格基于内存——不使用数据库对象进行中间存储。另一个例子是 `DBMS_OUTPUT` 包允许在 `SQL*Plus` 中运行 `PL/SQL` 程序时显示打印语句。

## 从服务器获取更多信息

多个包程序允许你获取有关数据库服务器的额外调优信息，例如共享内存池使用、段空间信息、运行跟踪、获取通用数据库信息等。当你习惯使用它们后，它们将成为你工具箱的标准部分。

## 描述提供的包

表 29.2 是一些重要的提供的 Oracle8i 包的方便快速参考，以及它们包含内容的简要描述。

### 表 29.2 提供的包摘要

| 包名 | 包头文件 | 描述 |
| --- | --- | --- |
| `DBMS_ALERT` | `dbmsalt.sql` | 数据库事件的异步处理。 |
| `DBMS_APPLICATION_INFO` | `dbmsutil.sql` | 注册当前运行的应用程序名称（性能监控）。 |
| `DBMS_AQADM` | `dbmsaqad.sql` | 与高级队列选项配合。 |
| `DBMS_DDL` | `dbmsutil.sql` | 重新编译存储子程序和包；分析数据库对象。 |
| `DBMS_DEBUG` | `dbmspb.sql` | `PL/SQL` 调试器的接口。 |
| `DBMS_DEFER` | `dbmsdefr.sql` | 远程过程调用设施的用户界面。 |
| `DBMS_DESCRIBE` | `dbmsdesc.sql` | 描述存储子程序的参数。 |
| `DBMS_JOB` | `dbmsjob.sql` | 在指定的时间或间隔运行用户定义的作业。 |
| `DBMS_LOCK` | `dbmslock.sql` | 管理数据库锁。 |
| `DBMS_OUTPUT` | `dbmsout.sql` | 在 `SQL*Plus` 中运行 `PL/SQL` 程序时显示打印语句。 |
| `DBMS_PIPE` | `dbmspipe.sql` | 会话间通信的方法。 |
| `DBMS_PROFILER` | `dbmsprof.sql` | `PL/SQL` 执行性能剖析。 |
| `DBMS_REFRESH` | `dbmsref.sql` | 刷新化视图。 |
| `DBMS_SESSION` | `dbmsssn.sql` | 管理会话特定信息。 |
| `DBMS_SHARED_POOL` | `dbmspool.sql` | 管理共享内存池使用。 |
| `DBMS_SNAPSHOT` | `dbmssnap.sql` | 管理数据快照。 |
| `DBMS_SPACE` | `dbmspace.sql` | 获取段空间信息。 |
| `DBMS_SYSTEM` | `dbmsys.sql` | 管理系统级操作。 |
| `DBMS_TRANSACTION` | `dbmstrans.sql` | 管理数据库事务。 |
| `DBMS_UTILITY` | `dbmsutil.sql` | 通用实用程序。 |

# 开始使用 ORACLE8i 提供的包

## 确保包已正确安装

你需要验证两点内容：

- 包存在且且有效（如上一个查询所示）。
- 用户对这些包或他们想要使用的包具有 `EXECUTE`（执行）权限。

用户可以通过以下查询检查他们是否拥有对 Oracle8i 提供的包的 `EXECUTE` 权限：

```
SELECT table_name, grantee
FROM all_tab_privs
WHERE grantor='SYS' and privilege='EXECUTE'
ORDER BY table_name;
```

典型的响应可能如下：

| TABLE_NAME | GRANTEE |
|---|---|
| `DBMS_APPLICATION_INFO` | `PUBLIC` |
| `DBMS_DBA` | `PUBLIC` |
| `DBMS_DESCRIBE` | `PUBLIC` |
| `DBMS_JOB` | `PUBLIC` |
| `DBMS_OUTPUT` | `PUBLIC` |
| `DBMS_PIPE` | `PUBLIC` |
| `DBMS_SESSION` | `PUBLIC` |
| `DBMS_SNAPSHOT` | `PUBLIC` |
| `DBMS_SPACE` | `PUBLIC` |
| `DBMS_SQL` | `PUBLIC` |
| `DBMS_STANDARD` | `PUBLIC` |
| `DBMS_TRANSACTION` | `PUBLIC` |
| `DBMS_UTILITY` | `PUBLIC` |
| `DBMS_REFRESH` | `PUBLIC` |
| `UTL_FILE` | `PUBLIC` |

所有 Oracle8i 提供的包都应该已经向 `PUBLIC` 授予了 `EXECUTE` 权限。我以前使用数据字典的所有视图来验证这一点。如果缺少任何你想要使用的包，DBA 可以以 `SYS` 身份重新编译。如果某个包存在但无效，DBA 可以使用以下命令重新编译：

```
ALTER PACKAGE SYS.<name> COMPILE PACKAGE;
```

`<name>` 是无效包的名称。`COMPILE PACKAGE` 子句告诉 Oracle8i 重新编译包规范和包体。如果包体需要重新编译，请运行对应的：

```
ALTER PACKAGE SYS,<name> COMPILE BODY;
```
