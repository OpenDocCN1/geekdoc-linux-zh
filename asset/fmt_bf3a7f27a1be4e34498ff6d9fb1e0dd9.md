
通过使用 System V habitat 脚本来修改 `PATH` 环境变量，可以在不让管理员更新每个用户的 `.profile`、`.login` 和 `.cshrc` 文件的情况下更改 System V habitat 路径。管理员只需更新 `/etc/svid2path` 和 `/etc/svid3path` 文件即可启用全局定义。

为了进一步说明 System V habitat 脚本如何设置 `PATH`，请看下面指定了 SVID 2 的 System V habitat 脚本的 `.profile` 文件：

```
stty erase DEL kill ^U intr ^C quit ^X echo
TERM=vt100
PATH=$HOME/bin:/usr/lib:/bin
MAIL=/usr/mail/$LOGNAME
EDITOR=vi
export MAIL PATH TERM EDITOR
if [ -f /etc/svid2_profile ]
then
    . /etc/svid2_profile
fi
```

在此示例中，假设 System V habitat 的路径为 `/usr/opt/s5`，如 `/etc/svid2path` 的内容所示，并且你的登录目录为 `/usr/users/xxx`。当你使用上述 `.profile` 文件登录后显示 `PATH` 时，结果会显示 System V habitat 的路径已被添加到 `.profile` 文件第三行设置的 `PATH` 之前，如下所示：

```
% echo $PATH  Return
/usr/opt/s5/bin:/usr/opt/s5/sbin:/usr/users/xxx/bin:/usr/lib:/bin
```

因此，当你发出 shell 命令时，会首先搜索 System V habitat。如果未找到该命令，则会搜索指定的路径。

### 9.3 Shell 脚本的兼容性

通过修改 shell 的 `PATH` 环境变量来实现 shell 脚本的兼容性（见第 9.1 节所述）。因此，System V habitat 会在默认系统位置之前被搜索。如果你的 `PATH` 变量已设置为 System V habitat，则无论你使用 C shell 还是 Bourne、Korn 或 POSIX shell，你的脚本都是 System V 兼容的。

### 9.4 System V Habitat 命令摘要

表 9-1 总结了 System V habitat 中用户命令的行为，这些命令的选项或功能与默认系统版本不同。如需完整了解 habitat 中的命令，请参阅每个命令的参考页。

**表 9-1：用户命令摘要**

| Command | System V Behavior |
|---|---|
| `chmod(1)` | 当省略 who 字符串时，会忽略 `umask` 值，使用符号形式时表现得好像 a 是 who 值。 |
| `df(1)` | 接受 `-t` 选项，可打印空间总量，并接受可选的文件系统名称或设备名称。 |
| `ln(1)` | 接受 `-f` 选项，可在创建指定链接前静默删除已存在的目标路径名。 |
| `ls(1)` | 仅在指定 `-C` 选项时才产生多列输出。此外，`-s` 选项会导致文件大小以 512 字节单位报告，而非 1024 字节单位。 |
| `mailx(1)` and `Mail(1)` | 包含 System V `mailx` 命令的功能。 |
| `sum(1)` | 默认使用按词算法；指定 `-r` 选项时使用按字节算法。System V `sum` 命令校验和算法的默认使用与 `sum` 命令的默认系统版本相反。 |
| `tr(1)` | 只要指定 `-c` 选项，就会包含 `-A` 选项。`-A` 选项会导致仅在八进制范围 1 到 377 内的字符被取反。 |

## 10 获取有关网络用户和主机的信息

本章介绍如何在开始通信或文件传输任务之前查找有关本地和远程用户和主机的信息。本章所述的命令将使你能够：

- 了解你自己的网络连接（`who am i` 命令，第 10.1 节）
- 确定当前谁已登录到本地系统以及他们从何处登录（`who` 命令，第 10.1 节）
- 查找有关另一用户的附加信息（如有）；例如，全名、办公地点、电话号码、项目或计划（`finger` 命令，第 10.2.1 节）
- 确定用户是否可通过 `talk` 或 `write` 命令联系（`finger` 命令，第 10.2.1 节和第 10.2.2 节）
- 分析和排序有关远程主机使用的信息（`uptime` 命令，第 10.3 节）
- 确定谁当前已登录到远程主机（`rwho` 命令，第 10.4 节）
- 确定远程主机是否在线（`ping` 命令，第 10.5 节）

#### Note

> 本章所述的命令与所有 TCP/IP 操作一样，受本地和远程主机的安全功能限制。如果它们的工作方式与此处或相关参考页所述不同，请咨询你的系统管理员。

### 10.1 在本地主机上识别用户

当你通过提供用户名和密码登录到主机计算机时，你具有唯一的身份。要验证你自己的网络连接的此信息，你可以使用名为 `who am i` 的 `who` 命令版本来显示有关你的以下信息：

- 登录名
- 终端名（行）
- 登录时间
- 网络连接来源计算机

例如，用户 lennon 可能在系统提示符（$）下输入 `who am i` 命令，并看到以下输出：

```
% who -M am i
lennon     tty p0     Jul 15 14:17     (walrus)
```

在此示例中，用户 lennon 于 7 月 15 日下午 2:17 从主机 walrus 登录。该行是 tty p0，而 walrus 是该行的名称，网络连接来自该行。

`who am i` 命令可帮助您跟踪在工作站上运行的会话。某些会话可能是您自己或与您合作的人对另一主机的远程登录。有关 `who am i` 命令的更多信息，请参阅 `who(1)` 参考手册页。

若要了解是否有其他用户登录到同一本地主机，请使用 `who` 命令。在以下示例中，lennon 在本地主机 london 的提示符下输入 `who` 命令，得知当前有三个其他用户从不同节点登录到 london：

```
london$ who -M
lennon     tty p0     Jul 15 08:17     (walrus)
elvis      tty p2     Jul 15 07:55     (velvet)
burdon     tty p1     Jul 15 09:02     (animal)
sarjan     tty p4     Jul 14 16:47     (pepper)
```

`who` 命令的输出与 `who am i` 命令的输出相同。

### 10.2 获取有关网络用户的信息

`finger` 命令及其选项使您可以显示在本地或远程主机上拥有帐户的用户的信息。指定的主机必须运行 `fingerd` 守护进程服务器，或者配置了 `inetd` 守护进程以启动 `fingerd`。如果 `finger` 命令不能像 `finger(1)` 参考手册页中描述的那样工作，请咨询您的系统管理员。

`finger` 命令具有以下语法：

```
finger [ [ option... ] [ user... ] [ user@host_name... ] ]
```

如果在使用 `finger` 命令时不指定选项或用户名，它将列出您所登录的本地主机上所有用户的以下信息（如果这些信息在给定用户的 `/etc/passwd` 文件中）：

- 登录名
- 全名
- 终端行名称，以及它是否可以通过 `write`（参见第 11.8 节）或 `talk`（参见第 11.9 节）接收来自其他用户的消息
- 空闲时间
- 登录时间
- 用户的办公室位置

#### 10.2.1 获取有关特定用户的信息

如果在本地主机上指定了用户的登录名，那么 `finger` 命令显示的信息比不指定用户名时更多。将显示有关该用户的以下附加信息：

- 用户的主目录和登录 Shell
- 用户主目录中的 `.plan` 和 `.project` 文件的内容（如果有）

以下示例演示了如何使用 `finger` 命令查找在本地主机上拥有帐户的用户 smith 的信息：

```
% finger smith
Login name: smith      (messages off)  In real life: John Smith
Office: LV05-3/724
Directory: /usr/netd/r2/smith             Shell: /bin/csh
On since Apr 9 16:20:56 on ttypb from wombat-lv5.dec.c
18 seconds Idle Time
Project: book "Communicating with Network Users"
Plan:
```

在输出的第一行中，messages off 表示用户 smith 已在他的 `.login` 文件中放置了 `mesg n` 命令，以防止他的终端通过 `write` 或 `talk` 命令接收来自其他用户的消息，这些消息可能会分散注意力。
