
6. 再次查看 `admnn` 组的成员。

``` 
| lsgroup admnn | |
|---|---|
```

7. 查看 `usernn2` 的主组 ID。

``` 
| HP-UX, Linux, Solaris | more /etc/passwd |
|---|---|
```

8. 你已经将 `usernn2` 设为 `sysadm` 吗？该用户现在可以完成哪些类型的任务？
**答。** ID `usern2` 现在是一个 `sysadm`。该 ID 可以完成所有与数据库管理器相关的任务，包括查询和更改所有数据、创建和删除任何对象、运行任何实用程序、控制授权等。

9. 退出 `su` 到 `root` 返回你的 `instnn` telnet 会话。

10. 建立一个会话，并在其中作为 `usernn2` 连接到数据库。

| 本地 | Telnet 到 UNIX 数据库服务器并登录 |
|---|---|
| GUI | 在 DB2 控制中心中，选择对象树中 `MUSICDB` 数据库下“用户和组对象”（User and Group Objects）左侧的 + 号。在“用户和组对象”下选择“数据库组”（DB Groups）。在内容面板中用右键点击 `PUBLIC` 组，从弹出的菜单中选择“更改”（Change）。勾选“连接数据库”（Connect to database）、“创建表”（Create tables）和“创建包”（Create packages）左侧的复选框以取消选中。点击“确定”（OK）。 |

- 11. 从 `usernn` 会话中通过执行以下命令确定你的权限：
`db2 get-auth`（注：此处 OCR 乱码，已重构逻辑命令）

（注：提供的源第 568-569 页 OCR 文本严重乱码。我保留了可读的片段并清理了格式。）

# 练习题 | 553

22. 通过你的 `usernn2` 会话完成以下操作以使更改生效。
`db2 terminate`
`db2stop force`
`db2start`

23. `force` 命令是否影响了由 `instnn` 用户 ID 建立的连接？（`instnn` 通过 telnet 会话和/或 DB2 控制中心以及 DB2 命令中心连接）。
答。`force` 命令要求强制终止所有应用程序。这也会强制终止系统管理员的连接。

24. 检查 `dbm cfg` 的当前内容，以查看 `usernn2` 对 `SYSCTRL_GROUP` 和 `SYSMAINT_GROUP` 的更新是否生效。
`db2 get dbm cfg | more`
检查 `systctrl` 和 `sysmaint_group` 参数。
答。是的，更新已完成。`systctrl` 和 `sysmaint_group` 参数分别显示 `CTRLnn` 和 `MAINTnn`。

25. 建立两个会话，一个用于 `usernn3`，另一个用于 `usernn4`。

| 本地 | GUI |
| :--- | :--- |
| 向 UNIX 数据库服务器建立两个 telnet 会话，并以 `usernn3` 和 `usernn4` 身份登录。 | 打开两个 DB2 命令窗口，并将每个窗口标题命名为用户名称。 |

26. 从 `usernn3` 会话开始，确定你的权限。
`db2 connect to musicdb user usernn3 using usernn3`
`db2 get authorizations`

27. `SYSCTRL` 权限意味着你有能力连接到任何数据库吗？
答。由于 `connect` 执行成功，且连接的直接或间接权限未列为该用户拥有的权限之一，因此意味着 `SYSCTRL` 权限提供了连接能力。正如课程所示，`SYSCTRL` 还有其他功能。

28. 从 `usernn4` 会话开始，确定你的权限。
`db2 connect to musicdb user usernn4 using usernn4`
`db2 get authorizations`

29. `SYSMAINT` 权限意味着你有能力连接到任何数据库吗？
答。由于 `connect` 执行成功，且连接的直接或间接权限未列为该用户拥有的权限之一，因此意味着 `SYSMAINT` 权限提供了连接能力。正如课程所示，`SYSMAINT` 还有其他功能。

# 554 练习题

30. 从你的 `usernn3` 会话 (`SYSCTRL`) 开始，确定与 `usernn4` 会话相关的代理（agent）。你可能需要先附加到你的实例。
`db2 attach to instnn user usernn3 using usernn3`
`db2 list applications`

31. 作为 `SYSCTRL`，尝试强制终止与 `usernn4` (`SYSMAINT`) 相关的代理。
`db2 "force application (n)"`
其中 `n` 代表你从上一个命令中确定的 `appl.handle`。

32. 你观察到了什么？`SYSCTRL` 还是 `SYSMAINT` 似乎拥有更高的权限？
答。命令执行成功。但仅仅因为 `usernn3` 强制终止了 `usernn4`，并证明 `usernn3` (`SYSCTRL`) 拥有更高级别的权限。记住 `usernn2` 能够强制断开 `instnn`，它们它们是平级的。然而，从“权限与特权”主题中你已经学到 `SYSCTRL` 的权限级别高于 `SYSMAINT`。事实上，必须是 `SYSADM` 或 `SYSCTRL` 才能发布 `FORCE APPLICATION` 命令。

33. 从你的 `usernn3` 会话开始，尝试提交一些 SQL 语句。
`db2 "create table testi (coll char(1))"`
`db2 drop table instnn.reorder`
`db2 "select * from instnn.music"`

34. 有任何语句执行成功了吗？此时不要进行其他授权！你认为如果从 `sysmaint` 权限的 ID 尝试相同的语句，情况会一样吗？
答。没有任何 SQL 语句执行。均遇到了权限错误。`syscl` 权限提供了许多特权，但这些特权并不延伸到访问数据对象。`sysm` 权限作为 `syscl` 权限的真正子集，无法执行任何操作。

35. 从 `usernn3` 的 `syscl` 权限再次尝试一次 `SELECT` 语句。
`db2 select name from instnn.artists`

36. 为什么这个 SQL 语句可以执行？`syscl` 权限针对表访问是特定的吗？
答。`SELECT` 语句有效是因为从 `Instnn.ARTISTS` 表选择的权限已授予 `PUBLIC`。

与 `syscl` 权限相关的特权不是特定于表的——它们是面向实例的。

37. 在 `usernn3` 中输入以下内容，说明之前的 `SELECT` 语句成功的原因：
`db2 "select grantee from syscat.tabauth where tabname = 'ARTISTS'"`

38. 在 `usernn3` 和 `usernn4` 会话中均执行 `db2 terminate`。

39. 你决定在你的安装中让 `usernn5` `DBADM`。
从你的 `instnn` 会话中，让 `usernn5` `DBADM`。

# 提示

| 本地 | GUI |
| :--- | :--- |
| 在你的 `instnn` 会话中：
`db2 connect to musicdb`
`db2 grant dbadm on database to user usernn` | 从 DB2 控制中心，在 Objects 面板的对象树中用右键点击 `MUSICDB` 数据库。<br>- 从弹出菜单中选择 Authorities（权限）。<br>- 点击 Add（添加）按钮。<br>- 从下拉列表中选择 `useridusernn`。<br>- 点击 OK 按钮。<br>- 在 User 选项卡上，选择 `user usernn`。<br>- 点击 `DBADM` 权限框右侧的下拉箭头，并在下拉列表中选择 Yes。<br>- 点击 OK 按钮。 |

40. 检查数据库授权目录视图，以查看你的授予结果。
`db2 "select * from sysatc.dbauth" | more`

注意 `usernn5` 如何拥有 `DBADM` 权限，以及它是由 `INSTnn` 授予的。

41. 你如何区分授予数据库创建者的内部 `DBADM` 授予与其他 `DBADM` 授予区分开来，因为权限列表是相同的？
答。数据库创建时完成的内部授予是由授予者列包含 `SYSDIM` 来识别的。

42. 为 `usernn5` 建立新会话。

| 本地 | GUI |
| :--- | :--- |
| 为 `usernn5` 建立 telnet 会话 | 打开一个 DB2 命令窗口，并将其命名为用户名称。 |

43. 从 `usernn5` 会话开始，连接数据库 `musicdb`。
`db2 connect to musicdbusernn5 using usernn`

44. 作为新的 `dbadm`，尝试执行以下系列 SQL 语句。
`db2 select name from instnn.artists`
`db2 "create table test1 (coll char(1))"`
`db2 "create table test instnn.dlc (coll char(1))"`
`db2 drop table instnn.dlc`

45. 有任何 SQL 语句失败了吗？注意你在另一个用户的模式（schema）中创建并删除了对象。任何具有创建表权限的用户都能完成此类任务吗？
答。没有任何 SQL 语句失败，因为授予 `usernn` 的 `dbadm` 权限允许 `usernn5` ID 执行所有请求的功能。在另一个用户模式中创建和删除对象的能力仅限于 `dbadm` 和 `sysadm` 权限。

# 练习

46. `SELECT` 语句只是授予 `DBADM` 的简单数据操作语言（DML）语句权限示例。你能对 `DBADM` 和 `DML` 做出更广泛的陈述吗？

答。作为示例的 `SELECT` 语句只是 `DBADM` 可以执行的 DML 语句之一。拥有此类权限的用户可以在数据库中的任何任意表上执行任何 DML 语句（`SELECT`、`INSERT`、`UPDATE` 和 `DELETE`）。此外，他们对数据库中的每个表具有控制权。因此，他们可以带 `GRANT OPTION` 将权限授予其他用户，删除对象并修改对象。

47. 除了广泛的 SQL 权限外，`dbadm` 还有能够针对数据库运行某些实用程序的能力，例如 `REORG` 和 `RUNSTATS`。然而，你现在不需要演示这些能力。

回想 `sysctl` 拥有发布 `force` 命令的权限，但没有与数据访问相关的权限。如果你希望在拥有 `sysctl` 权限之外创建一个具有 `dbadm` 权限的 ID——你会如何实现这一结果？

答。可以将用户 ID 放入 `sysctl` 组，然后也授予该 ID `DBADM` 权限。

# DB2 用户和组权限

- 1. Asusernn 作为一个 `DBADM`，在 `INSTnn.ARTISTS` 表中插入以下行。

```
