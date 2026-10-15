
# 第21章

## 管理数据库服务

### 本章内容

- 数据库基础简要回顾
- 选择数据库：MySQL 与 PostgreSQL
- 配置 MySQL
- 配置 PostgreSQL
- 数据库客户端
- 参考

本章是对 MySQL 和 PostgreSQL 的介绍，这两款数据库系统随 Ubuntu 一起提供。你将了解这些系统的作用、两个程序的比较方式，以及如何权衡它们的优缺点。这些信息可以帮助你为组织的数据库需求选择并部署合适的系统。

组织的数据库管理员 DBA 的职责因组织规模和运营情况、支持人员等而有所不同。根据特定组织的架构，如果你是组织的 DBA，你的职责可能包括以下内容：

- 安装和维护数据库服务器——你可能需要安装和维护数据库软件。维护可能涉及在适当时间安装补丁以及升级软件。作为 DBA，你可能需要对系统拥有 root 访问权限，并懂得如何管理软件（参见第 7 章“管理软件”）。你还需要了解内核、文件系统和其他安全问题。
- 安装和维护数据库客户端——数据库客户端是用于访问数据库的程序（你将在本章后面的“数据库客户端”部分了解更多），可在本地或通过网络远程访问。你的职责可能包括在用户系统上安装和维护这些客户端程序。本章讨论了如何从 Linux 命令行以及其图形界面数据库工具安装和使用客户端。
- 管理账户和用户——账户和用户管理包括向数据库添加和删除用户、分配和管理密码等。在本章中，你将学习如何在 Ubuntu 上使用 MySQL 和 PostgreSQL 授予和撤销用户权限和密码。
- 确保数据库安全——为了确保数据库安全，你需要关注诸如访问控制，确保只有授权人员可以访问数据库，以及权限，确保可以访问数据库的人不会做不该做的事情等事项。在本章中，你将学习如何管理通过安全外壳 SSH、Web 和本地 GUI 客户端访问数据库。
- 确保数据完整性——服务器硬盘存储上的所有信息中，数据库中的信息很可能是最重要的。确保数据完整性涉及规划多用户访问，并确保当多个用户同时对数据库进行更改时，更改不会丢失或重复。

### 数据库基础简要回顾

本章讨论的 Linux 下的数据库服务基于客户端/服务器模型。数据库客户端通常用于输入数据以及从服务器查询或显示查询结果。你可以使用命令行或图形客户端访问正在运行的服务器。数据库通常有两种形式：平面文件和关系型。平面文件数据库可以简单到用空格、制表符或其他字符分隔信息不同部分的文本文件。Ubuntu 的 `/etc/passwd` 文件就是一个简单的平面文件数据库的例子。另一个例子可能是类似这样的简单通讯录：

Doe-John-505 Some Street-Anytown-NY-12345-555-555-1212

你可以使用标准的 UNIX 工具如 `grep`、`awk` 和 `perl` 来搜索和从这种原始数据库中提取信息。虽然这对于只有一个人使用的地址簿这样的小型数据库可能效果很好，但这种类型的平面文件数据库有几个局限性：

- 扩展性差——平面文件数据库无法对数据进行随机访问。它们只能进行顺序访问。这意味着它们必须逐行扫描文件中的每一行来查找特定信息。随着数据库规模的增长，访问时间增加，性能下降。
- 平面文件数据库不适合多用户环境——根据数据库的设置方式，它要么一次只允许一个用户访问，要么允许两个用户同时进行更改，而更改可能会相互覆盖并导致数据丢失。

### phonebook

| last_name | first_name | phone |
|---|---|---|
| Doe | John | 555-555-1212 |
| Doe | Jane | 555-555-1212 |
| Palmer | John | 555-123-4567 |
| Johnson | Richard | 555-111-4321 |

### cd_collection

| id | title | artist | year | rating |
|---|---|---|---|---|
| 1 | Mindbomb | The The | 1989 | 4 |
| 2 | For All You've Done | Hillsong | 2004 |  |
| 3 | Trouser Jazz | Mr. Scruff | 2002 | 5 |
| 4 | Natural Elements | Acoustic Alchemy | 1988 | 3 |
| 5 | Combat Rock | The Clash | 1982 | 4 |
| 6 | Life for Rent | Dido | 2003 | 5 |
| 7 | Adiemus 4 | Karl Jenkins | 2000 | 4 |
| 8 | The Two Towers | Howard Shore | 2002 | 5 |

FIGURE 21.2 A single database can contain two tables—in this case, phonebook and cd_collection.

phone number, you want to be able to look up outstanding order and invoice information for any of your customers. You could use three related tables in an RDBMS to store and organize customer data for just those purposes. Figure 21.3 shows an example of such a database.

### customers

| cid | last_name | first_name | shipping_address |
|---|---|---|---|
| 0 | Doe | John | 505 Somestreet |
| 2 | Doe | Jane | 505 Somestreet |
| 3 | Palmer | John | 200 Anystreet |
| 4 | Johnson | Richard | 1000 Another Street |

### orders

| cid | order_num | stock_num | priority | shipped | date |
|---|---|---|---|---|---|
| 0 | 1002 | 100.252.342 | 3 | Y | 8/31/01 |
| 0 | 1221 | 200.352 | 1 | N | 10/2/01 |
| 3 | 1223 | 200.121 | 2 | Y | 10/2/01 |
| 2 | 1225 | 221.152 | 1 | N | 10/3/01 |

### overdue

| cid | order_num | days_overdue | action |
|---|---|---|---|
| 0 | 1002 | 32 | sent letter |

FIGURE 21.3 You can use three related tables to track customers, orders, and outstanding invoices.
