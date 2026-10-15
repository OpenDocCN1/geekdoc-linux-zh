
该文件仍然位于 `...admin/rh1dev/pfile`，但它也会出现在 `$ORACLE_HOME/dbs` 中。

注意
来自 `$ORACLE_HOME/admin` 的一些额外脚本提供了附加功能。一个示例将在第 10 章“出现问题时”中讨论。

## 为新数据库配置

一旦创建了数据库，你需要将其包含在网络文件中。具体来说，你需要在 `tnsnames.ora` 和 `listener.ora` 文件中创建条目。然后你需要启动监听器。如果使用 `DBCA` 创建数据库或生成脚本，链接将自动创建。在这种情况下，它们是自动创建的。如果你没有使用 `DBCA` 创建了脚本，则新数据库的唯一 `init.ora` 在 `pfile` 目录中，因此需要为该文件创建一个链接。语法如下：

## 自动配置的文件

如果使用 `DBCA` 创建数据库或生成脚本，链接将自动创建。在这种情况下，它们是自动创建的。如果你没有使用 `DBCA` 创建了脚本，则新数据库的唯一 `init.ora` 在 `pfile` 目录中，因此需要为该文件创建一个链接。

## 配置新数据库

一旦创建了数据库，你需要将其包含在网络文件中。具体来说，你需要在 `tnsnames.ora` 和 `listener.ora` 文件中创建条目。然后你需要启动监听器。

## 自动配置的文件

如果使用 `DBCA` 创建数据库或生成脚本，链接将自动创建。在这种情况下，它们是自动创建的。如果你没有使用 `DBCA` 创建了脚本，则新数据库的唯一 `init.ora` 在 `pfile` 目录中，因此需要为该文件创建一个链接。

## 创建数据库

# 第 5 章

![](img/0735bb12e1d45128c662b4b409eb1bf1_152_0.png)

## 5.15 listener.ora

对于新数据库，你需要复制并修改的关键行设置如下：

```
SID_DESC =

  (GLOBAL_DBNAME = rhitst1.mike.com)

  (ORACLE_HOME = /u01/app/oracle/product/9.1.6)

  (SID_NAME = rhitst1)

)
```

确保你已添加正确的数据库名称，并且拼写正确。接下来，你必须考虑监听器进程本身。

## listener (监听)

监听器进程必须运行，其他机器的连接才能成功。如果监听器进程未运行，你可以本地连接数据库，但外部到数据库的连接将失败。通常，每个服务器上有一个监听器进程，支持该服务器上的所有数据库（无论版本）。要启动监听器进程，只需输入 `lsnrctl start`，如图 5.16 所示。

你可以使用 `ps -ef` 来确定监听器进程是否运行，或者你可以检查监听器本身：

```bash
$ lnrctl status
```

这将告诉你监听器是否正在运行，以及它正在对哪些数据库（服务处理程序）进行监听。

修改 `listener.ora` 文件后，你需要重启监听器以使更改生效。你可以执行 `lsnrctl reload` 命令，也可以直接重启它。要停止监听器，请执行此命令：

## 5

## 创建数据库

# Unix 和 Linux 上的 Oracle DBA

```bash
$ lnrctl stop

LSNRCTRL for Linux: Version 8.1.6.0 - Production on 19-FEB-2001 19:32:17

(c) Copyright 1998, 1999, Oracle Corporation. All rights reserved.

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC) (KEY=EXTPROC)))

The command completed successfully
```

如果你打算重启监听器，在停止它后不要忘记重新启动它。最后，要获取监听器命令的完整列表，请尝试 `lsnrctl help`。

![](img/0735bb12e1d45128c662b4b409eb1bf1_153_0.png)

图 5.16 启动监听器进程。

不要忘记监听器！
有多位 DBA 在早上启动了生产数据库，但忘记了重启监听器。结果就是导致了混乱的询问：“数据库启动了吗？”
在启动数据库后，请确保监听器进程正在运行。

记住连接到数据库有两种方式：本地或远程。当你已经登录到数据库、设置了 `ORACLE_SID` 且未在连接字符串中指定数据库名称时，即建立了本地连接。

```bash
$ sqlplus system
```

## 创建数据库
第 5 章

本地连接将使用 bequeath 协议，不需要监听器运行。通常，这是 DBA 连接到数据库的方式，因为他们已经通过 telnet 或 Windows 登录到了 Unix 服务器。

远程连接涉及用户从客户端机器连接到数据库服务器。这需要使用连接字符串来指定目标数据库，以及其机器上的 `tnames.ora`。数据库服务器上也必须运行监听器进程。这是大多数终端用户使用的连接类型。尝试连接到远程数据库的写法如下：

```bash
$ sqlplus system@rhitdev1
```

这涵盖了设置 Oracle 网络的基础知识。Net8 的高级功能似乎一直在在演进，但这些基础将让你准备好投入生产。现在数据库已设置好并建立了连接，从技术角度来说你已经准备就绪。有些公司有记录新数据库的程序，此外你还需要为新数据库更新自己的电子表格，所以不要忘记这些最后的管理任务。

# 自定义你的 .profile 文件

你创建数据库时使用的 `.profile` 文件可以工作，但可以进行改进。Unix 环境中两种流行的修改是在登录时为数据库 SID 提供提示符，并提供命令行编辑功能。

为了获得 SID 提示并正确设置你的环境，你需要使用 `/usr/local/bin/oraenv` 文件，并拥有一个更新过的 `/etc/oratab` 文件。只需将以下代码添加到你的 `.profile` 文件（位于你的家目录下）的末尾即可：

```bash
echo "The SIDs on this machine are:"
cat /etc/oratab | awk -F: '{print $1}' | grep -v "#"
ORAENV_ASK=$SID
export ORAENV_ASK
/usr/local/bin/oraenv
```

这段代码使用 `awk` 提取并打印 `/etc/oratab` 中列出的数据库。然后你选择一个 SID，`oraenv` 会使用该值设置你的环境。你的下一次登录将显示如下：

```bash
$ su oracle
Password:
The SIDs on this machine are:
demo
rhisti
ORACLE_SID = [rhisti] ? demo
$ echo $ORACLE_SID
demo
```

下一种常见的配置使用的是 Korn shell 的命令行编辑功能和你的历史文件。如果你想重复之前输入过的命令，只需按下 `ESC-K`。然后输入 `K`，你输入的每条命令都会出现在该行。

# 日常活动
第 6 章

数据字典提供了大量的视图，包含数据库中每个对象和统计信息的详情。这些信息以只读（不可更新！）格式提供给用户。这对于任何想要查询的人来说都是非常优质的信息源。事实上，大多数 GUI 管理工具（第 7 章“GUI 管理产品”介绍）都是从这些视图中获取信息，然后将其格式化为彩色的图表和图形展示给用户。

作为一名新入职的 DBA，我做过的最有益的活动之一就是致力于学习一些常用的视图。我完全没有记下所有的视图，但我知道它们有多少个，并且当我不记得某个确切名称时，我知道该去哪里查找。

要获取所有标准视图的列表，请使用以下命令：

```sql
select synonym_name from dba_synonyms where
synonym_name like 'VS%'
synonym_name like 'DBA%'
synonym_name like 'ALL%'
synonym_name like 'USER%'
order by synonym_name;
```

将结果输出到文件中，并进行编辑以删除不需要或冗余的信息。

DBA 常用的视图包括：

```sql
v$database, v$datasource, v$controlfile, v$instance,
v$log, v$logfile, v$recover_file v$ssga, v$session
dba_constraints, dba_data_files, dba_extents, dba_free_space,
dba_ind_columns, dba_indexes, dba_objects, dba_segments,
dba_sequences, dba_synonyms, dba_rollback_segs, dba_role_privs,
```
