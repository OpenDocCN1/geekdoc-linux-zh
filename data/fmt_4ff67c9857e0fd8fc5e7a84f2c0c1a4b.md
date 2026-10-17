
是的，你可以这样做。但你记得必须先定义一些表，所以可能会再次退出。你决定需要一个存储个人信息的表、一个存储项目信息的表、一个存储项目成员的表以及一个用户信息的表。

![](img/74418f52d5d454acca60721059dbdc99_419_0.png)

这位程序员试图提供帮助。这里的数据库示例非常针对系统管理员可能想要的操作。在不深入探讨数据库设计哲学的情况下，你希望将表中的数据保持在离散相关的集合中。用户信息包括用户及其主目录等内容。用户恰好（通常）是人，并具有姓名和地址等特征。虽然所有这些信息可能关联同一个人，但良好的设计要求你为这两种信息创建单独的表并将它们“关联”起来。此外，“用户信息”是关于你机器上的账户，而“个人信息”是关于真实的人。一个人拥有一条 `userid` 记录，但有一个共享的 `userid` 字段将这两张表的数据关联起来。

这里设计的数据库形式包含了关于人的信息和关于 UNIX 用户账户的信息。为了让示例变得有趣，它让你注意到，可能有一组用户拥有账户是因为他们正为了某个项目共同工作。因此，数据库还包含了关于项目的信息以及参与每个项目的人的信息。

你在目录中创建了文件，其中包含你将使用的每个 SQL 表的 SQL 定义。你选择将它们命名为 `mysql.tablename.def`，以便于查找。这还允许你使用文件中的定义从命令行直接创建数据库表，而无需手动输入。

（注：后续文本为大量重复内容，已按要求处理）

# 其他有用软件：实用工具

```
mysql INSERT INTO projectinfo
-> SET supervisorfirstname='Henry',
-> supervisorlastname='James',
-> projectname='Wine Tasting 101',
-> description='关于葡萄产量的一项重要实验',
-> termination=2020-01-01
-> -
Query OK, 1 row affected (0.00 sec)
```

你决定逐行输入的方法产生了瓶颈。这次你选择使用更具一次性的方法。你先处理计划定义的字段表，然后处理这些字段对应的对应值列表（值表）。

```
mysql INSERT INTO projectinfo
-> (supervisorfirstname,supervisorlastname,
-> projectname,description,termination)
-> VALUES ('Martin', 'Dooley', 'Hydroponics'),
-> '水培系统中的散热,2020-04-01'
Query OK, 1 row affected (0.00 sec)
```

你向 `projectinfo` 表中添加了另一行：

```
mysql INSERT INTO projectinfo
-> (supervisorfirstname,supervisorlastname,
-> projectname,description,termination)
-> VALUES ('Burt', 'Dunmer', 'Negative Space Phenomena'),
-> '埋入容器包装氛围下的密封剂寿命',
-> '0001-06-06'
Query OK, 1 row affected (0.00 sec)
```

现在是时候检查打字是否有什么用处了。尽管你的信息包含了导师的姓、名，以及每个项目的名称、描述和终止日期，但它们无法整齐地显示在一页上。为了方便将结果放入窄小的书页中，而不是你的 UIX 监视器，你决定目前只查看项目名称和导师信息：

```
mysql SELECT projectname,
-> supervisorfirstname,supervisorlastname
-> FROM projectinfo;
```

| projectname | supervisorfirstname | supervisorlastname |
|---|---|---|
| Wine Tasting 101 | Henry | James |
| Hydroponics | Martin | Dooley |
| Negative Space Phenomena | Burt | Dunler |

3 rows in set (0.00 sec)

信息确实在那里！你对结果很满意，决定暂时停用 `mysql`。

![](img/74418f52d5d454acca60721059dbdc99_422_0.png)

当你坐在椅子上，思考你那兴奋的 `mysql` 体验时，你看到一个用户拿着他的 Perl 书走了进来。这时你突然想起了你的 Perl 和 Perl 模块安装。“我打赌我可以写一个脚本来和 `mysql` 通信，这样我就不用记得给我的值加上引号了！”

于是你决定玩玩 Perl。现在你写好了一个与 `mysql` 通信的 Perl 脚本。你知道它还不完全完善，但你迫不及待想要试一下了：

`soyakaze testdb 201>` `./adduser`

`usage adduser.pl <username>`

> 与 MySQL 通信并生成此界面的 Perl 程序实际代码将在今天晚些时候在“使用 Perl”部分介绍，届时那位无畏的程序员会对他的代码进行注释。它作为不连续的列表包含在附录 C，“示例配置文件”中，如果你感兴趣将其输入并在你的机器上使用部分内容的话。现在，如果你想看 MySQL 和你的脚本之间是如何工作的，你需要在接下来的几页中来回翻看。

在你尝试脚本的兴奋中，你忘记了为脚本提供它所需的数据库名称！但你认为记得让脚本告诉你你做了什么是很聪明的。无论如何，你再次尝试了一次，这次使用了正确的语法：

```
soyakaze testdb 202> ./adduser.pl usertrack
User's first name: Henry
User's last name : James
User's street address : use the form
address line 1
address line 2
City, State Zip code
134 Bayard St.
Room 1214
Clifton, OK 13754
User's phone number : (614)-555-1322
Built hjames
Is this OK? (Y/N) : Y
Is user attached to a project? (Y/N) : Y
Project 0 Wine Tasting 101
Supervised by Henry James
Project 1 Hydroponics
Supervised by Martin Dooley
Project 2 Negative Phenomena
Supervised by Burt Dunler
Please pick a project (0-2) : 0
User Added. Exiting
```

院长必须想要这些！你刚刚才将所有这些数据输入到数据库中仅作为测试。你决定，列出 Henry 项目成员的姓名和电话号码应该就能为院长提供足够的信息。

那么，你需要什么呢？

- 你需要通过 `projectinfo` 表关联出哪个项目是 Henry 的项目。不过，你除了该项目属于一个名为“Henry”的人之外，并一无所知，所以这可以作为该项目的搜索标准。
- 你必须从 `projectmembers` 表中将该项目名称与属于该项目的所有成员匹配。
- 你需要 `personinfo` 表中的姓名和号码。
- 然而，`personinfo` 表不包含任何特定于项目的信息，因此你必须使用 `userid` 关联到 `projectinfo` 表中的项目名称，从而从 `personinfo` 表中获取个人信息。

你尝试执行：

```mysql
mysql> SELECT personinfo.userid, personinfo.firstname,
  -> personinfo.lastname, personinfo.phone, projectinfo.projectname
  -> FROM projectinfo, projectinfo, projectmembers
  -> WHERE projectinfo.supervisorfirstname LIKE '%en%' AND
  -> projectmembers.projectname = projectinfo.projectname AND
  -> personinfo.userid = projectmembers.userid;
```

| userid | firstname | lastname | phone | projectname |
|---|---|---|---|---|
| hjames | Henry | James | (614)-555-1322 | Wine Tasting 101 |
| awolsch | Alice | Walsach | (800)-432-1111 | Wine Tasting 101 |
