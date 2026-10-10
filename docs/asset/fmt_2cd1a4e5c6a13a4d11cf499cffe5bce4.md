
语句执行成功了吗？这意味着什么？

**答：** 语句没有执行成功。`username` 没有对表空间 `DMS04` 的使用（USE）权限。

### 11. 作为 `username`，你请求你拥有 `DBADM` 权限的好朋友（一个企业间谍）向你授予 `DMS04` 的 USE 权限。

换上你企业间谍的化身，在你的 `instnn` 会话中，授予 `username` `DMS04` 的 USE 权限。

```
db2 connect to musicdb user instnn using instnn

db2 grant use of tablespace dms04 to user username
```

## 练习

12. 作为 `usernn`，尝试再次创建你的测试表。执行以下 SQL 语句创建你的测试表。

`db2 "create table test1 (partno integer, subpart integer) in DMS04"`
SQL 语句执行成功了吗？这意味着什么？

**答：** SQL 语句执行成功。有了表空间的 USE 权限，拥有 `CREATAB` 权限的用户可以在该表空间中创建表。

13. 假设 `usernn` 使用 `test1` 一段时间。你现在应该扮演系统管理员的角色（好人，不是企业间谍）。你一直在分析一个关于 `DMS04` 表空间可用空间的问题。作为分析的一部分，你需要知道 `DMS04` 的表空间 ID。`DMS04` 的表空间 ID 是什么？请记录下来。

**提示：**

| 本地 (Local) | `db2 "list tablespaces"` | more |
|---|---|---|
| n| GUI | 在 DB2 Control Center 中，在 `MUSICDB` 数据库选择其下的 Views（视图）。用右键选择 Views。选择 Sample Contents。完成后，点击 Close。 |

**答：** `DMS04` 表空间的 ID 是 6。

14. 你现在决定找出 `DMS04` 中创建了哪些表。执行以下语句显示。

| 本地 (Local) | `db2 connect to musicdb` |
| --- | --- |
| `db2 select * from syscat.tables where tablespace = 'DMS04'` | |

15. 你发现了什么？最初估计 `DMS04` 大大时，预测到这一点了吗？

**答：** `DMS04` 表空间包含三个表：`ALB`、`CONCERTS` 和 `TEST1`。

16. 作为 `instnn`，删除 `username.TEST1` 以将其从数据库中移除。

| 本地 (Local) | GUI |
| --- | --- |
| `db2 connect to musicdb` `db2 drop username.test1` | 在 DB2 Control Center 中，选择 `MUSICDB` 数据库下的 Tables。向下滚动内容面板找到 `TEST1` 表。如果它不在列表中：* 用右键点击 `MUSICDB` 数据库下的 Tables。* 选择 Refresh（刷新）。用右键点击 `TEST1` 表并选择 Drop（删除）。点击 OK。 |

| 本地 (Local) | GUI |
| --- | --- |
| `db2 connect to musicdb` `db2 drop username.test1` | |

17. 为什么你能够删除非自己模式下的表？
**答：** 执行删除操作的是系统管理员。`SYSADM` 对实例中的每个数据库拥有最高级别的权限。拥有 `DBADM` 权限的用户也可以删除该表，所有者 ID 也可以。

18. 显然，你不希望你的生产系统暴露给用户创建测试对象。列出为了开始保护生产环境你应该采取的步骤。
**答：** 在这个特定案例中，我们看到最初由于没有授予表空间的 USE 权限，`username` 无法在 `DMS04` 中创建对象。USE 权限允许你控制谁有使用表空间的能力，对于 `username`，他们仍然可以在 `USERSPACE1` 中创建表。但是，如果企业间谍没有向 `username` 授予 USE 权限（`PUBLIC` 默认拥有 USE 权限），这会对我们系统的存储产生影响，而我们可能希望保持控制。
生产系统通常需要显式控制。为了开始保护环境，通常需要撤销 `PUBLIC` 的 `CONNECT`、`CREATAB` 和 `BINDADD` 权限。你可能还希望撤销 `USERSPACE` 的 USE 权限。

# 548 练习题

19. 撤销授予 `PUBLIC` 的默认数据库权限。

| 本地 | `db2 "revoke bindadd, connect, creatatab on database from public"` |
|---|---|
| GUI | 在 DB2 控制中心中，选择对象树中 `MUSICDB` 数据库下“用户和组对象”（User and Group Objects）左侧的 + 号。在“用户和组对象”下选择“数据库组”（DB Groups）。在内容面板中用右键点击 `PUBLIC` 组，从弹出的菜单中选择“更改”（Change）。勾选“连接数据库”（Connect to database）、“创建表”（Create tables）和“创建包”（Create packages）左侧的复选框以取消选中。点击“确定”（OK）。 |

21. 用户能够创建表吗？

答。用户无法创建表，因为 `CREATAB` 权限已被撤销。

22. 用户 `usernn` 仍然连接到数据库吗？这是否意味着撤销 `CONNECT` 权限的操作未完成？

答。`usernn` 的连接仍然处于状态，否则相关的错误消息将与不具备 connect 权限有关。然而，撤销操作确实从 `PUBLIC` 中移除了 connect 授权。

连接授权在用户建立连接时进行检查。在 `usernn` 连接到数据库时，连接的授权已授予了 `PUBLIC`。

23. 假设你有业务理由撤销某个用户的 connect 权限，并确保该用户建立的所有连接都已断开。你已经完成了撤销操作。请记录并完成所需的剩余步骤。（如果不确定操作流程，请参考解决方案。）

提示：

| 本地 | `db2 list applications` |
|---|---|
| | 注意与 `usernn` 应用程序关联的应用程序句柄（application handle） |
| | `db2 "force application (nnn)"` |
| | 其中 "nnn" 是与 `usernn` 应用程序关联的应用程序句柄 |

GUI | 从控制中心列出当前连接的应用程序。
在 DB2 控制中心，在对象面板（Objects Pane）的对象树中用右键点击 `instnn` 实例，从弹出的菜单中选择“应用程序”（Applications）。
用右键选择与 `usernn` 关联的应用程序。
点击“强制”（Force）。
点击“关闭”（Close）。

- 24. 从你的 `usernn` 再次尝试提交 CREATE TABLE 语句。
`db2 "create table test1 (partno integer, subpart integer) in DMS04"`

- 25. 尝试结果让你认为连接已丢失或已终止。在 `usernn` 会话中提交以下命令。
`db2 connect to musicdb usernn using usernn`

- 26. 连接成功了吗？
答。连接未成功。`USERnn` 拥有 `CONNECT` 权限。因此，系统管理员成功撤销了 connect 权限并断断了 `usernn` 会话。

- 27. 退出 `usernn` 窗口。

# DB2 权限

- 1. 作为 `instnn`，自实例创建以来你一直在执行 sysadm 任务。
假设你现在决定将 `usernn2` 设为 sysadm。
从你的 telnet 会话中，查看数据库管理器配置文件并记录 sysadm 组名。

提示：`db2 get dbm cfg | more`
当前的 sysadm 组是 `ADMnn`。

注意：该组名在 DBM CFG 文件中以大写显示，但在 UNIX 系统中实际上是小写。

- 2. 要添加新的组名和用户，你需要作为 UNIX root 用户。在你的 telnet 会话中：

```
su - root

(输入 root 密码)
```
