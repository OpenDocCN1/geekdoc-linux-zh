

# 176 数据库

从第二行开始的所有内容取决于 aspell 的显示。当 aspell 发现一个拼写错误的单词（任何不在其字典中的单词）时，它会显示包含拼写错误单词（consensus）的句子，并用一对星号将该单词突出显示。在该句子下方，aspell 会列出可能的修正建议，并从 i 开始顺序编号。在这种情况下，aspell 将 consensus（正确的选择）作为 consensus 的第一个修正建议。

句子之后，aspell 显示一个包含 16 个选项的列表——通过 1 到 9 的数字编号，以及 6 个用单个字母 i, r, I, R 和 x 标记的选项——后面跟着问号提示符。你必须按下输出显示的数字或字母之一来告诉 aspell 你想让做什么。数字选项显示了拼写单词的 10 种可能替换词。以下是字母选项的含义：

- + 空格接受当前单词。
- i 忽略该拼写错误的单词。
- I 忽略该单词的所有出现处。
- r 替换此处（你必须输入一个替换词）。
- R 替换所有出现处（你必须输入一个替换词）。
- a 接受该单词并添加到你的字典。
- x 表示保存剩余文件并退出，忽略拼写错误。

这些选项是敏感的。确保你没有开启大写锁定。img/d9230b719dc0ef80851f363d8c6f571.png

Fedora Core 带有两个关系型数据库——PostgreSQL 和 MySQL。简单介绍如何使用 PostgreSQL（读作 Postgres），这是一个强大且流行的关系型数据库（作为表格集合工作的数据库类型）。你可以使用结构化查询语言 (SQL) 与数据库进行交互。

PostgreSQL 由一个开发人员开发，并根据 BSD 开源许可证发布。该许可证对源代码的使用没有限制。要获取最新进展，请访问 PostgreSQL.org。

要检查系统中是否安装了 PostgreSQL，输入 `rpm -qa`。至少会看到三个 RPM 包——postgresql、postgresql-libs 和 postgresql-server。如果消息提示未安装这些包，你可以按照以下步骤进行安装：

1. 以 root 身份登录并将 DVD 插入驱动器。如果你使用的是 GNOME 或 KDE，DVD 会自动挂载。如果没有，在终端输入以下命令来挂载 DVD：
```
mount /mnt/cdrom
```
如果你有一个主 CD-ROM 驱动器并添加了第二个 DVD/CD 驱动器，输入 `mount /mnt/cdrom` 进行挂载。

2. 输入以下命令安装 PostgreSQL：
```
cd /mnt/cdrom
rpm -ivh postgresql*
```
要使用 PostgreSQL，必须首先以 root 身份登录并使用以下命令启动数据库服务器：
```
service postgresql start
```
PostgreSQL 服务器进程启动，名为 postmaster。服务器是一个守护进程（持续运行的后台进程），它接受客户端的数据库查询并执行数据库任务（如添加表）。如果你希望在每次启动系统时都启动数据库服务器，输入以下命令将其开启：
```
chkconfig postgresql on
```
现在你必须设计数据库、在 PostgreSQL 中创建数据库并从中加载数据。为了说明如何创建和加载数据库，请设置一个简单的目录数据库。

PostgreSQL 有它自己的用户概念，与 Linux 账户分开。为了让用户能够访问系统上的 PostgreSQL 数据库，你将该用户名作为 PostgreSQL 用户添加。img/d9230b719dc0ef80851f363d8c6f571.png

要添加 PostgreSQL 用户，请遵循以下步骤：

1. 以 root 身份登录。然后在在终端窗口中输入以下命令：
```
su - postgres
```
你以 postgres 身份登录——这是 PostgreSQL 数据库服务器运行的用户名。在此用户名下执行 PostgreSQL 管理任务。

2. 在终端窗口中输入以下命令：
```
createuser
```
此实用程序允许你添加 PostgreSQL 用户。程序会提示输入要添加的用户名名称：
Enter name of user to add:

3. 输入你赋予数据库权限的用户的 Linux 用户名。例如，若要将我自己添加为用户，输入我的 Linux 用户名 `naba`。

4. 回答两个提示问题：
```
Shall the new user be allowed to create databases?
(y/n)
Shall the new user be allowed to create more new users?
(y/n)
```
通常情况下，你不希望用户能够创建数据库或添加新用户，因此对这些提示按 N。你可以使用此过程运行 `createuser` 并根据需要添加任意数据库用户。

遵循以下基本步骤序列来构建数据库：

- 1. 设计数据库。这一步涉及定义用于存储信息的表和属性。
- 2. 创建一个空数据库。在添加表之前，数据库系统要求你构建一个空数据库。
- 3. 在数据库中创建表。在此步中，你使用 SQL 的 `CREATE TABLE` 语句定义表。
- 4. 加载任何固定数据。例如，如果你有一个制造商名称或出版商名称表（针对书籍），你希望将已知信息加载到该表中。
- 5. 备份初始数据库。这一步对于确保你可以从头创建数据库是必要的。
- 6. 将数据加载到表中。你可以从早期的数据库转储加载数据，也可以通过表单主动加载。
- 7. 使用数据库。进行查询、更新记录或使用 SQL 命令插入新记录。

构建数据库并不遵循所有可能的步骤。对于示例，数据库设计步骤是简易的，因为我的目录数据库只包含一张表。该表的属性如下：

- 书名（50个字符）
- 第一作者姓名（最多20个字符）
- 第二作者姓名（如有，20个字符）
- 出版商名称（30个字符）
- 页数（数字）
- 出版年份（数字，如2002）
- 国际标准书号（ISBN），10位文本（如07645634）

我在表中以不带连字符的形式存储 ISBN。并将 ISBN 作为表的主键，因为 ISBN 是书籍的全球识别系统。这意味着每个书籍条目必须有一个唯一的 ISBN，这对于书籍是成立的。要在 PostgreSQL 中创建空数据库，使用 `createdb` 命令。你必须登录 root 然后变为 postgres 用户以运行 `createdb` 程序。输入以下命令切换用户：
```
su
(输入 root 密码)
- postgres
```
变为 postgres 后，你可以创建数据库。例如，创建一个名为 books 的数据库，由 naba 所有，我输入以下命令：
```
createdb -0 naba books
```
当你不再需要某个数据库时，在 postgres 用户下运行 `dropdb` 命令将其删除。要了解更多关于 `createdb` 和 `dropdb` 命令的信息，输入以下命令：
```
man createdb
man dropdb
```

创建空数据库后，你与数据库的所有交互都通过 `psql` 程序进行——PostgreSQL 交互终端作为数据库服务器的客户端。你必须带上名称作为参数运行 `psql`。`psql` 程序会提示你输入。这是一个示例（第一行是你输入的）：

```
psql books
Welcome to psql 7.4, the PostgreSQL interactive terminal.

\copyright 查看分发条款
\h 获取 SQL 命令的帮助
\? 获取关于内部斜杠命令的帮助
\g 或以分号结束以执行查询
\q 退出
```

```
books=>
```

在创建表或将数据加载到表中时，一种典型方法是将 SQL 语句（以及 `\g` 等 psql 命令）放在文件中。

