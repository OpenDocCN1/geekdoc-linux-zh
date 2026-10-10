
17. 默认表空间的表空间定义者的授权 ID 是什么？
答。不是，如果使用 SMS。

18. 输入以下内容数据库。

| 本地 | db2 connect |
| GUI | 从 |

# 配置你的数据库

如果你意外取消了绑定，可以手动在 Windows 上绑定文件：

- 打开 DB2 命令行窗口。
- 切换目录到 `sqllib\bnd`
- 使用以下命令绑定 `db2ubind.lst` 和 `db2cli.lst`：

1. 添加数据库：
2. 展开实例并点击 Views 探索你可以做什么
**注意：** 第一次访问数据库需要几分钟。DB Center。如果你想检查，执行：
`db2 connect to musicdb`
`db2 list packages`

你会看到包的数量在增加。在 bind 结束时，包的总数应该是 80。

**注意：** 执行 list 会减慢 bind 的整体进度。

# 练习题 45

如果你意外取消了绑定，可以手动在 Windows 上绑定文件：

- 打开一个 DB2 命令行窗口。
- 切换目录到 `sqllib\bnd`
- 使用以下命令绑定 `db2ubind.lst` 和 `db2cli.lst`：
  `db2 connect to musicdb user instnn using instnn`
  `db2 bind @db2ubind.lst`
  `db2 bind @db2cli.lst`

实验结束

# 创建对象 3

## 本练习关于什么

本练习是一个在线创建练习。完成练习后，你将能够：

- 创建表
- 创建索引
- 创建视图
- 创建别名
- 为表添加引用性约束
- 为表添加检查约束
- 为表添加触发器
- 访问对象的系统目录信息

## 引言

现在已经有了数据库和表空间，需要创建 MUSICDB 数据库对象。使用 DB2 Control Center（GUI 练习）或 DB2 语句来创建每种类型的第一个对象，作为第一个表。当有多个相同类型的对象需要创建时，将使用脚本文件创建所有剩余对象。

## 练习说明

在整个练习过程中，如果出现 DB2 消息窗口，或者你正在查看 Show SQL 或 Show Command 窗口，在很多情况下，练习说明不会特别告诉你关闭窗口。阅读消息，查看 SQL 或命令，然后点击关闭窗口。

命令通常在 Command Center（命令中心）的 Interactive（交互）选项卡中输入。如果你想在 Command Center 的 Script（脚本）选项卡或 DB2 命令行窗口（以 db2 为前缀）中输入，通常也是可以的。

在某些情况下，可能需要滚动窗口以访问窗口上的 Action（操作）按钮（如 OK、Cancel 或 Apply）。如果你看不到操作按钮，请向下滚动窗口查看它们。

在练习过程的任何时候，当你将新脚本导入到 Command Center 的 Script 选项卡时，如果系统提示你是否要丢弃当前脚本，请点击 Yes。

主要使用你的 telnet 会话和命令的练习解决方案标记为 Local（本地）。主要使用 GUI 工具的练习解决方案标记为 GUI。

## Setup

在 DB2 Control Center 中执行以下步骤，以启用工作站与数据库服务器之间的通信。

- 1. 如果你正在进行 DB2 远程管理练习，请连接到你的 `instnn` 实例（如果尚未连接）。然后连接到你的 MUSICDB 数据库（如果尚未连接）。
同时，打开 DB2 命令行窗口，并连接到你的 MUSICDB 数据库：
Start -> Programs -> IBM DB2 -> Command Line Tools -> Command Window
`db2 connect to musicdb user instnn using instnn`
- 2. 对于两种练习环境，请与你的 UNIX 数据库服务器建立 TELNET 会话并使用你的实例名称登录。

## Create Tables

在本节中，你将为 MUSICDB 数据库创建所需的表。

- 1. 创建你的 ARTISTS 表。该表应具有以下特征：
- 表模式 (schema) `instnn`
- 表名 `artists`
- 位于表空间 `dms01` 的普通数据
- 位于表空间 `dms02` 的索引
- 位于表空间 `dms03` 的长数据
- 列 `artno` 应该定义为主键
- 定义如下的列：
(`artno smallint null`,
`name varchar (50)`,
`classification char (1) not null`,
`bio clob (100K) logged compact`,
`picture blob (500k) not logged compact`)

## 462 | Exercises

## Local

`db2 connect to musicdb`

在键入完整语句之前，不要按回车键。按回车键会将语句发送到 DB2 执行。

```
db2 "create table artists

(artno smallint not null,

name varchar (50),

classification char (1) not null,

bio clob (100K) logged compact,

picture blob (500k) not logged compact,

primary key (artno)

in in dms01

index in dms02

long in dms03"
```
