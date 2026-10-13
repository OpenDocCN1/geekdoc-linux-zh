
## 安装 PostgreSQL

输入以下命令来安装 PostgreSQL：

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh postgresql*
```

使用 PostgreSQL 所需的软件包将安装到你的系统上。

要使用 PostgreSQL，你必须首先以 `root` 身份登录，并使用以下命令启动数据库服务器：

```
service postgresql start
```

PostgreSQL 服务器进程启动，称为 `postmaster`。服务器是一个守护进程（一个连续在后台运行的进程），它接受来自客户端进程的数据库查询，并代表客户端执行数据库任务（如添加表）。

如果你希望 PostgreSQL 数据库服务器在系统每次启动时都启动，请输入以下命令来启用它：

```
chkconfig postgresql on
```

现在，你必须设计一个数据库，在 PostgreSQL 中创建该数据库，并将数据加载到其中。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

### 添加数据库用户

PostgreSQL 拥有独立于 Linux 用户账户的自身用户概念。要允许用户访问你系统上的 PostgreSQL 数据库，你必须将该用户名添加为 PostgreSQL 用户。

要添加 PostgreSQL 用户，请遵循以下步骤：

1. 以 `root` 身份登录。然后在终端窗口中输入以下命令：

   ```
   su - postgres
   ```

   你以 `postgres` 身份登录——这是 PostgreSQL 数据库服务器运行的用户名。你必须在此用户名下执行 PostgreSQL 管理任务。

2. 在终端窗口中输入以下命令：

   ```
   createuser
   ```

   此实用程序允许你添加 PostgreSQL 用户。程序会提示输入要添加的用户名：

3. 输入你授予数据库权限的用户的 Linux 用户名。

   例如，要添加我自己作为用户，我输入我的 Linux 用户名 `naba`。

4. 回答接下来的两个提示：

   ```
   Shall the new user be allowed to create databases? (y/n)
   Shall the new user be allowed to create more new users? (y/n)
   ```

   通常，你不希望用户创建数据库或添加新用户，因此你按 N 键来回应这些提示。

   你可以使用此过程运行 `createuser` 并添加任意数量的数据库用户。

### 回顾构建数据库的步骤

遵循以下基本步骤序列来构建数据库：

1. 设计数据库。

   此步骤涉及定义将用于存储信息的表和属性。

2. 创建一个空数据库。

   在你添加表之前，数据库系统要求你构建一个空数据库。

3. 在数据库中创建表。

   在此步骤中，你使用 SQL 的 `CREATE TABLE` 语句定义表。

4. 将固定数据加载到表中。

   例如，如果你有一个制造商名称或出版商名称（对于书籍的情况）的表，你希望将该表加载已知信息。

5. 备份初始数据库。

   如果需要从头创建数据库，此步骤是必要的，以确保你可以做到这一点。

6. 将数据加载到表中。

   你可以从数据库的早期转储中加载数据，或者通过表单交互式加载。

7. 使用数据库。

   使用 SQL 命令进行查询、更新记录或插入新记录。

#### 设计数据库

我的简单示例并未遵循数据库构建的所有可能步骤。对于这个示例，数据库设计步骤很琐碎，因为我的图书目录数据库仅包含一个表。该表的属性如下：

- 书籍标题，最多 50 个字符
- 第一作者姓名，最多 20 个字符
- 第二作者姓名（如果有），最多 20 个字符
- 出版商姓名，最多 30 个字符
- 页数，作为数字
- 出版年份，作为数字（如 2002）
- 国际标准书号（ISBN），作为 10 个字符的文本（如 0764567934）

我将 ISBN 存储为不包含典型书籍 ISBN 中嵌入的破折号。我还将 ISBN 用作表的主键，因为 ISBN 是书籍的全球识别系统。这意味着每个书籍条目必须有一个唯一的 ISBN，这对于书籍来说是真实的。

#### 创建空数据库

要在 PostgreSQL 中创建空数据库，请使用 `createdb` 命令。你必须以 `root` 身份登录，然后切换到 `postgres` 用户以运行 `createdb` 程序。在终端窗口中输入以下命令以获取 `postgres` 用户名权限：

```
su -
```
在提示符处输入 root 密码

```
su - postgres
```

成为 `postgres` 用户后，你可以创建数据库。例如，要创建一个名为 `books` 的空数据库，并且该数据库由数据库用户 `naba` 拥有，我输入以下命令：

```
createdb -O naba books
```

当不再需要某个数据库时，在 `postgres` 用户名下运行 `dropdb` 命令以删除该数据库。要了解有关 `createdb` 和 `dropdb` 命令的更多信息，请输入以下命令：

```
man createdb
man dropdb
```

#### 使用 PostgreSQL 交互式终端

创建空数据库后，你与数据库的所有交互都通过 `psql` 程序进行——该程序是作为数据库服务器客户端的 PostgreSQL 交互式终端。你必须以数据库名称作为参数运行 `psql`。`psql` 程序随后会提示你输入。下面是一个示例（第一行是你输入的内容）：

```
psql books
Welcome to psql 7.4, the PostgreSQL interactive terminal.

Type:  \copyright for distribution terms
       \h for help with SQL commands
       \? for help on internal slash commands
       \g or terminate with semicolon to execute query
       \q to quit

books=>
```

在创建表或向表中加载数据时，一种典型方法是将 SQL 语句（以及如 `\g` 等 `psql` 命令）放在一个文件中，然后运行 `psql`，将标准输入重定向到该文件。例如，假设有一个名为 `sample.sql` 的文件包含一些你想在名为 `books` 的数据库上尝试的 `SQL` 命令。那么，你可以使用以下命令运行 `psql`：

```
psql books < sample.sql
```

我以此方式使用 `psql` 来创建数据库表。

#### 定义表

为了创建一个名为 `books` 的表，我编辑了一个名为 `makedb.sql` 的文本文件，并在该文件中放入以下行：

```
/*
* Table structure for table 'books'
*/
CREATE TABLE books (
  isbn CHAR(10) NOT NULL PRIMARY KEY,
  title CHAR(80),
  author1 CHAR(20),
  author2 CHAR(20),
  pubname CHAR(30),
  pubyear INT,
  pagecount INT
) \g
```

`CREATE TABLE books` 是一个 `SQL` 语句，用于创建名为 `books` 的表。语句末尾的 `\g` 是一个 `psql` 命令。表的属性显示在括号内的行中。

如果表包含固定数据，你还可以包含其他 `SQL` 语句（如 `INSERT INTO`），以便在创建表后立即将数据加载到表中。

要执行创建 `books` 表的 `makedb.sql` 文件中的 `SQL` 语句，我按如下方式运行 `psql`：

```
psql books < makedb.sql
```

现在，`books` 数据库包含一个名为 `books` 的表。（好吧，也许我应该给它们起不同的名字，但给它们起相同的名字似乎很方便。）我现在可以开始向表中加载数据了。

#### 向表中插入记录

向表中加载数据的一种方法是在另一个文件中准备 SQL 语句，然后使用该文件作为输入运行 `psql`。例如，假设我想将以下书籍信息添加到 `books` 表中：

```
isbn = '0764541331'
title = 'Red Hat Linux 9 Professional Secrets'
author1 = 'Naba Barkakati'
author2 = NULL
pubname = 'Wiley Publishing, Inc.'
pubyear = 2003
pagecount = 1070
```

那么，以下 SQL 语句将此信息加载到 `books` 表中：
