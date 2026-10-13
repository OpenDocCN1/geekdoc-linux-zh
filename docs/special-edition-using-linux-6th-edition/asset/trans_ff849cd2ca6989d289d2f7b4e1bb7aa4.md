

如果你在命令行中没有使用 `-u` 选项指定用户名，并且尚未设置 `NWCLIENT_DEFAULT_USER` 环境变量，系统会提示你输入用户名，如图 28.2 所示。

**图 28.2**  
NetWare 用户 jsmith 的示例登录会话。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_538_0.png)

如果你以 root 身份登录 Linux，可以使用 `nwlogin` 配合 `-l` 选项为另一个 Linux 用户建立 NetWare 连接。如果要将 Linux 用户 col 以 `OU=ACCTG.O=CALDERA` 上下文中的 NetWare 账户 jsmith 登录到示例树，请执行以下命令：

```
nwlogin -l col -u jsmith.acctg.caldera
```

> **注意**
> 
> 使用 `-l` 选项登录时所使用的客户端首选项是 root 的，而不是 col 的；但是，当 col 用户使用 NDS 资源时，所使用的客户端首选项是 col 的。

当 Linux 用户登录到 NDS 或 bindery 服务器时，该登录会话对该 Linux 用户所登录的任何终端均有效。如果该用户在 OpenLinux 服务器上打开了多个 telnet 会话，则该用户的所有会话都被视为已登录到 NetWare，并且可以使用 NetWare 资源。

> **警告**
> 
> 如果用户登录到 NDS 或 bindery 服务器，然后注销 Linux，Linux 服务器会保持该用户的 NDS 或 bindery 连接处于打开状态：该用户下次登录 Linux 时，该 NDS 或 bindery 连接仍然可用。只要 nwclientd 守护进程未被停止或重启，此情况就成立。因此，如果 Linux 机器由多个用户共享，请确保在注销 Linux 之前已注销 NetWare。

## 查看当前的 NetWare 连接

你可以使用适用于 Linux 的 NetWare 客户端同时登录到多个 NDS 树和 bindery 服务器。`nwwhoami` 实用程序使用户可以查看所有当前的 NetWare 连接。该实用程序没有任何关联的命令行参数。要查看你的 NetWare 连接，请执行以下命令：

```
nwwhoami
```

## 注销

当你不再需要 NetWare 连接时，请注销。要从 NDS 树或 NetWare bindery 服务器注销，可以使用 **nwlogout** 实用程序。其语法如下（表 28.4 显示了 nwlogout 实用程序可能使用的命令行选项）：

```
nwlogout [OPTIONS]
```

**表 28.4 — `nwlogout` 的命令行选项**

| 选项 | 用途 |
|---|---|
| `-a` | 注销所有 NDS 树和 NetWare 服务器 |
| `-h` | 显示命令帮助 |
| `-s <SERVER>` | 从服务器（bindery）注销 |
| `-t <TREE>` | 从树（NDS）注销 |

由于 NetWare 客户端允许你同时登录到多个 NDS 树和 bindery 服务器，因此在注销时，你必须指定要从哪个服务器或树注销。

如果要从 **NW-TREE** NDS 树注销，请执行以下命令：

```
nwlogout -t NW-TREE
```

执行此命令后，你将注销 **NW-TREE** 及其所有关联服务器。但是，你在其他所有 NDS 树和 bindery 服务器上的登录状态仍然保持。

如果要一次注销所有 NDS 树和 bindery 服务器，可以执行以下命令：

```
nwlogout -a
```

此命令将断开你与*所有*已连接的 NetWare 资源（包括基于 NDS 和基于 bindery 的资源）的连接。

## NetWare 自动挂载器

NetWare 客户端（`nwclientd`）使你能够通过 Linux 文件系统访问 NDS 和 bindery 对象。`/NetWare/` 目录称为自动挂载路径。登录后，你可以通过在 `/NetWare/` 目录中使用简单的 `cd` 命令，浏览 NDS 目录树或 NetWare 服务器资源。

如图 28.3 所示，你可以通过在 NetWare 自动挂载路径中更改目录，浏览 NDS 树上下文以及 NetWare 文件系统。你还可以通过切换到 NetWare 自动挂载路径中的 `/NetWare/bindery/` 目录，浏览 bindery 服务器和卷。

**图 28.3**  
使用 NetWare 自动挂载路径浏览 NW-TREE。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_540_0.png)

## 打印到 NetWare 打印队列

本节描述的所有打印实用程序都可以使用环境变量，如前文“配置 NetWare 客户端设置”部分所述。与打印相关的变量如表 28.5 所示。

**表 28.5 — 打印实用程序使用的环境变量**

| 环境变量 | 功能 |
|---|---|
| `NWCLIENT_PREFERRED_SERVER` | 打印实用程序使用此变量指定在未通过 `-s` 选项指定时持有打印队列的 NetWare 服务器 |
| `NWCLIENT_PREFERRED_QUEUE` | 打印实用程序使用此变量指定在未通过 `-q` 选项指定时默认使用的打印队列对象 |

可用于从 OpenLinux 打印到 NetWare 打印队列的两个实用程序是 nwprint 和 xnwprint。其语法如下（表 28.6 显示了 nwprint 和 xnwprint 实用程序可能使用的命令行选项）：

```
nwprint [OPTIONS]

xnwprint [OPTIONS]
```

**表 28.6 — nwprint 和 xnwprint 的命令行选项**

| 选项 | 描述 |
|---|---|
| `-q <QUEUE NAME>` | 要使用的 NetWare 打印队列 |
| `-s <SERVER>` | 队列所在的 NetWare 服务器 |
| `-b <PATH>` | 要打印到的 bindery 队列对象的 NetWare 自动挂载路径 |
| `-n <PATH>` | 要打印到的 NDS 队列对象的 NetWare 自动挂载路径 |
| `-p <PRINTSERVER>` | 将处理打印作业的打印服务器对象 |
| `-# <NUMBER>` | 要打印的份数 |
| `-l <NUMBER>` | 每页可打印的行数 |
| `-t <NUMBER>` | 每个制表符扩展为的空格数 |
| `-w <NUMBER>` | 页面上可打印的列数 |
| `-f <FORMNAME>` | 要使用的 NetWare 打印格式名称（格式必须存在于 NetWare 容器对象中） |
| `-j <JOBNAME>` | 出现在标题页上的作业名称 |
| `-u <NAME>` | 出现在标题页上的用户名 |
| `-c` | 在每个换行符前插入回车符 |
| `-N` | 禁止打印标题页 |
| `-h` | 显示命令帮助 |

要将一份名为 `myfile` 的文件打印三份到 O=CALDERA 上下文中的 Q-HPLASERJET NetWare 打印队列，可以使用以下命令：

```
nwprint -s OPENLINUX -q Q-HPLASERJET.CALDERA -# 3 myfile
```

> **注意：** 你必须指定 NDS 打印队列的 distinguished name。所使用的 distinguished name 可以是全类型格式（如 `.CN=Q-HPLASERJET.O=CALDERA`）或无类型格式（如 `Q-HPLASERJET.CALDERA`）。

你还可以通过执行以下命令，使用示例 NDS 树中 Q-HPLASERJET 打印队列的 NetWare 自动挂载路径进行打印：

```
nwprint -n /NetWare/NDS/NW-TREE/CALDERA/Q-HPLASERJET myfile
```

> **注意：** 使用 NetWare 自动挂载路径时，你可以指定 NDS 打印队列或 NDS 打印机对象。

> **注意：** 在撰写本文时，尚不支持 Novell 分布式打印服务（NDPS）。但是，你可以创建一个由 NDPS 服务的打印队列，并让 Linux 客户端按照上述步骤打印到该队列。

## 检查打印作业状态

可以使用 `nwqstat` 或 `xnwmanageq` 实用程序检查打印作业的状态。其语法如下（表 28.7 显示了 `nwqstat` 和 `xnwmanageq` 实用程序可能使用的命令行选项）：

```
nwqstat [OPTIONS]

xnwmanageq [OPTIONS]
```

**表 28.7 — nwqstat 和 xnwmanageq 的命令行选项**

| 选项 | 描述 |
|---|---|
| `-q <QUEUE>` | 打印队列名称 |
| `-s <SERVER>` | 队列所在的 NetWare 服务器 |
| `-b <PATH>` | bindery 队列对象的 NetWare 自动挂载路径 |
| `-n <PATH>` | NDS 打印机或打印队列对象的 NetWare 自动挂载路径 |
| `-h` | 显示命令帮助 |

要使用 NetWare 自动挂载路径查看 O=CALDERA 上下文中 Q-HPLASERJET 的状态，请执行以下命令：

```
nwqstat -n /NetWare/NDS/NW-TREE/CALDERA/Q-HPLASERJET
```

上述命令将按打印顺序显示当前位于打印队列中的打印作业列表。

xnwmanageq 实用程序使你能够以图形方式查看打印队列中的作业，如图 28.4 所示。如果你拥有适当的 NDS 权限，该实用程序还允许你删除打印作业。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_542_0.png)

### 从打印队列中删除作业

nwdelqjob 实用程序允许用户删除其提交到 NetWare 打印队列的打印作业。默认情况下，用户只能删除自己的打印作业。但是，如果你拥有适当的 NDS 权限，则可以使用此实用程序删除其他用户的打印作业。其语法如下（表 28.8 显示了 nwdelqjob 实用程序可能使用的命令行选项）：

```
nwdelqjob [OPTIONS] <JOB ID>
```

**表 28.8 — nwdelqjob 的命令行选项**

| 选项 | 描述 |
|---|---|
| `-q <QUEUE>` | 打印队列名称 |
| `-s <SERVER>` | 队列所在的 NetWare 服务器 |

