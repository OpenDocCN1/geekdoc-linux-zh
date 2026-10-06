
键？为什么不呢，例如，直接使用客户名称作为键？这是因为我们无法保证名称不会改变，也无法保证两个人的名字不会相同。但我们可以保证一个任意分配的值（如我们的客户编号）是唯一且不可变的。

## 数据库引擎/服务器

Linux 提供了许多可用的数据库服务器。其中最著名的是 MySQL（及其分支 MariaDB）和 PostgreSQL。这些数据库服务器实现了客户端/服务器架构，这个概念在 20 世纪 90 年变成了一个热门话题。这种类型的数据库服务器作为服务器进程运行，通过网络连接到它们，并发送 SQL 语句到服务器执行。数据库操作的结果将返回给客户端程序进行进一步的处理和展示。许多网站使用这种架构，通过 Web 服务器向独立的数据库发送 SQL 语句，以根据需要动态创建网页。由 Linux、Apache Web 服务器、MySQL 和 PHP 组成的著名 LAMP 堆栈推动了早期的很大发展。

对于这次冒险来说，设置 MySQL 和 PostgreSQL 等数据库服务器太复杂，无法在这里涵盖，因为除了其他之外，它们还支持多个并发用户以及相应的安全控制。这对于我们学习 SQL 来说已经超出了。

## sqlite3

我们将使用的数据库是 SQLite。SQLite 是一个可以与应用程序配合使用提供高级 SQL 功能的库。它在嵌入式系统领域非常受欢迎。它省去了开发者为自己的数据存储和管理任务编写自定义解决方案的麻烦。除了库之外，SQLite 还提供了一个命令行工具直接与 SQLite 数据库交互。此外，它还接受来自标准输入的 SQL（以及自己的命令行界面），并将结果发送到标准输出，它是我们使用 shell 脚本的理想选择。

大多数 Linux 仓库中都有 SQLite。安装非常简单，如下：

```
me@linuxbox:-$ sudo apt install sqlite3
```

## 构建实验场

让我们创建一个包含一些真实数据的实验场。在 LinuxCommand.org 网站上有一个我们可以下载的存档，可以实现这一点。

```
me@linuxbox:-$ cd
me@linuxbox:-$ curl -c http://linuxcommand.org/adventure-sql.tgz
me@linuxbox:-$ tar xzf adventure-sql.tgz
me@linuxbox:-$ cd adventure-sql
```

解压 .tgz 文件将生成一个包含数据集、一些演示代码和一些实用工具的实验场目录。我们将处理的数据集包含 Ubuntu 18.04 系统上安装的软件包列表。这将包含软件包名称、每个软件包的简短描述、每个软件包包含的文件列表以及它们的大小。

```
me@linuxbox:~/adventure-sq$ 
```

所有文件都是人类可读的文本，所以请随意查看。存档中的数据集是 .tsv 文件。这些是制表符分隔的值文件。第一个是 `package_descriptions.tsv` 文件。它包含两列数据：软件包名称和软件包描述。第二个名为 `package_files.txt` 的文件有三列：软件包名称、该软件包安装的文件名称以及文件的大小。

## 启动 sqlite

要启动 SQLite，只需使用 `sqlite3` 命令，后面可选地跟一个用于加载我们数据库的文件名。如果我们不使用文件名，SQLite 将在内存中创建一个临时数据库。

```
me@linuxbox:~/adventure-sq$ sqlite3
SQLite version 3.22.0 2018-01-22 18:45:57
Enter."help" for usage hints.
Connected to a transient in-memory database.
Use ".FILENAME" to reopen on a persistent database.
sqlite>
```

加载完成后，SQLite 将呈现一个提示符让我们可以在其中输入命令。命令可以是 SQL 语句，也可以是控制 SQLite 自身的点命令（dot commands）。要查看可用点命令的列表，我们在提示符处输入 `.help`。

```
sqlite> .help
```

对我们感兴趣的点命令只有几个，它们处理输出的格式化问题。要退出 sqlite3，我们输入点命令 `.quit`。

```
sqlite> .quit
```

虽然我们可以使用 `sqlite>` 提示符直接与 sqlite3 程序交互，但 sqlite3 也可以通过标准输入接受点命令流和 SQL 语句。这通常是 SQLite 的被使用方式。

## 创建表并插入我们的数据

为了开始使用数据库，我们需要将 .tsv 文件转换为 SQL 语句流。我们的数据库最初将包含两个表。第一个名为 `Package_Descriptions`，第二个名为 `Package_Files`。为 `Package_Descriptions` 表创建 SQL 流，我们将使用实验场存档中提供的 `insert_Package_Descriptions.awk` 程序。

```
me@linuxbox:~/adventure-sql$ ./Package_Descriptions.awk 
< package_descriptions.tsv > insert_Package_Descriptions.sql
```

让我们看看生成的 SQL 查询。我们将使用 `head` 命令显示流的前几行。

```
me@linuxbox:~/adventure-sql$ insert_Package_Descriptions.sql
DROP TABLE IF EXISTS Package_Descriptions;
CREATE TABLE Package_Descriptions (
    package_name VARCHAR(60),
    description VARCHAR(120)
);

BEGIN TRANSACTION;
INSERT INTO Package_Descriptions
VALUES ('a2ps', 
'GNU a2ps "Anything to PostScript" converter and pretty-printer\');
INSERT INTO Package_Descriptions
VALUES ('accountservice', 
'query and manipulate user account information');
```

使用 `tail` 命令查看最后几行。

```
me@linuxbox:~/adventure-sql$ tail insert_Package_Descriptions.sql
VALUES ('zlibamd64', 
'compression library - runtime\');
INSERT INTO Package_Descriptions
VALUES ('zlib186', 
'compression library - runtime\');
INSERT INTO Package_Descriptions
VALUES ('zlib-devamd64', 
'compression library - development\');
INSERT INTO Package_Descriptions
VALUES ('zsh', 
'shell with lots of features\');
INSERT INTO Package_Descriptions
VALUES ('zsh-common', 
'architecture independent files for Zsh');

COMMIT;
```

如我们所见，SQL 是冗长的且像英语的。英语规定关键字要大写；但并非强制要求。SQL 是不区分大小写的。空格并不重要，但通常用于使 SQL 语句更易读。语句可以跨多行，但不是必须的。语句以分号字符结束。这次冒险中的 SQL 通常按照下文“延伸阅读”部分由 Simon Holywell 编写的风格指南格式化。由于 SQL 可能变得复杂，编写代码时的视觉化支持 SQL 有两种注释形式。

- 单行注释以破折号开头
- 而多行注释采用类似于编程语言的 `/* */` 风格

在继续之前，我们需要暂时偏离一下讨论一下作为标准的 SQL。虽然有 ANSI 标准，但每个数据库服务器实现 SQL 的方式都不同。早期并没有固定的标准，部分是出于商业考虑。每个供应商都想让客户难以迁移到竞争对手的产品，因此他们都向语言中添加了独特的特性，以促进令人畏惧的“供应商锁定”。

## 创建和删除表

我们 SQL 流的前两行删除了任何名为 `Package_Descriptions` 的现有表，并创建一个同名的新表。`DROP TABLE` 语句删除表。可选的 `IF EXISTS` 子句用于在表不存在时防止错误。SQL 中有很多可选子句。`CREATE TABLE` 语句定义一个新表。正如我们看到的，这将有两个列。第一列 `package_name` 定义为多达 60 个字符的变量字符串 `VARCHAR`。这里是 SQL 数据库支持的一些常用数据类型：

| 数据类型 | 说明 |
| --- | --- |
| INTEGER | 整数 |
| CHAR(n) | 固定长度字符串 |
| VARCHAR(n) | 可变长度字符串 |
| NUMERIC | 数字 |
| REAL | 浮点数 |
| DATETIME | 日期和时间 |

## 数据类型

SQL 数据库支持许多类型。遗憾的是，这取决于供应商。即使在两个数据库共享相同数据类型名称的情况下，数据类型的实际含义也可能不同。SQLite 中的数据类型是动态的。与其他 SQL 数据库不同，SQLite 不是固定的。SQLite 允许其他数据库中的许多常见数据类型，它实际上支持 4 种通用数据存储类型。

| 数据类型 | 说明 |
| --- | --- |
| INTEGER | 根据需要使用 1, 2, 3, 4, 6 或 8 字节的有符号整数 |
| REAL | 8 字节 IEEE 浮点数 |
| TEXT | 字符串 |
| BLOB | 二进制大对象（例如 JPEG 或 MP3 文件） |SQLite 数据类型

在上面的示例中，我们将 `VARCHAR` 指定为列类型。SQLite 对此完全满意，但它实际上将这些列中的值存储为 `TEXT`。它忽略了数据类型规范中的长度限制。SQLite 极其

