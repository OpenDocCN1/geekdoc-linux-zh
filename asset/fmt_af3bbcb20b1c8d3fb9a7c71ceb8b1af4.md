
# 仅允许上传到 incomming 目录...

```
# <Directory>
#   Umask 017
#   # ...禁止读/写
#   <Limit READ WRITE>
#     DenyAll
#   </Limit>
#   # ...允许存储文件，但不允许其他写入
#   <Limit STOR>
#     AllowAll
#   </Limit>
# </Directory>
#</Anonymous>
```

# 网络与互联网服务 第二部分

一旦完成配置，你需要识别 `inet` 守护进程进程。
可以使用以下命令找到它：

```
humf2:/etc # ps aux | grep inetd

root      146 0.0 1440 296 ? S 17:32 0:00 /usr/sbin/inetd

root      1564 0.0 1208 416 ? S 22:38 0:00 grep inetd
```

进程 ID `PID` `146` 是一个示例——它在你的系统上可能不同。
一旦对 `inetd.conf` 文件进行了修改，你需要获取配置文件。这是通过使用 `kill -1` 向进程发送 `HUP` 信号完成的。

```
humf2:/etc # kill -1 146
```

如果你运行 `ftp` 连接到 `localhost`，你应该看到 `proptfd` 的横幅。例如，该用户是之前创建的且有效的登录。运行 `ls` 命令时使用了 `-Ca`，以列显示输出并列出隐藏文件。

```
humf2:/etc # ftp localhost

Connected to localhost.

220 ProFTPD 1.2.0 (by SuSE Linux)

Name (localhost): root

331 Password required.

230 User logged in. Remote system type is UNIX. Using binary mode to transfer files.

ftp > -Ca

150 Opening ASCII data connection for list.

226 Transfer complete.

ftp > exit
```

# FTP 第 10 章

#### 注意

SUSE 6.2 Linux 发行版附带 ProFTPD 1.2 服务器。在本书出版时，ProFTPD 1.2 解决了在旧版本中发现的重要安全问题。建议从 `http://www.proftpd.org/` 更新到 ProFTPD 的最新版本。

# FTP 管理工具

有几个工具可以帮助管理 FTP 服务器。这些工具在安装服务器时已作为软件包的一部分自动安装。以下实用程序帮助你查看服务器的当前状态并控制其关闭程序：

- `ftpshut`
- `ftpwho`
- `ftpcount`

# ftpshut

`ftpshut` 命令简化了 FTP 服务器的关闭程序。此功能仅适用于你一直运行服务器——而不是让其留由 `inetd` 调用。`ftpshut` 的格式如下：

```
ftpshut -l <login-minutes> -d <drop-minutes> <time> <warning message>
```

`<login-minutes>` 是服务器关闭前拒绝新事务的分钟数。`<drop-minutes>` 是服务器关闭前断开现有连接的分钟数。`<login-minutes>` 的默认值为 10，`<drop-minutes>` 的默认值为 5。

`<time>` 是服务器关闭的时间。你可以指定军事时间格式（例如，`0312` 表示凌晨 3:12）。第二个选项是指定等待的分钟数（例如 `+60` 表示 60 分钟后关闭）。最后一个选项是最剧烈的；如果你现在指定字符串，`<warning message>` 是向所有 FTP 客户端显示的的消息，告知服务器将关闭。有关关闭消息格式的详情见本文前面的 `ftpass` 文件。

# FTP

# 网络与互联网服务 第二部分

# ftpwho

`ftpwho` 显示系统上所有的活动 FTP 用户。该命令的输出格式类似于 `/bin/ps` 命令。其格式如下：

`<pid> <tty> <stat> <time> < connection details >`

`<pid>` 是处理传输的 FTP 守护进程 ID；`<tty>` 总是问号 (?) 因为连接来自 FTP 而不是 Telnet；`<stat>` 是该实例的状态，`S` 表示睡眠，`Z` 表示已崩溃（僵尸），`R` 表示运行。`<time>` 表示该 FTP 实例占用的 CPU 时间。最后，`<connection details>` 告诉连接来自哪里、用户是谁以及该用户的功能。

以下是 `ftpwho` 输出的示例：

```
Service class all:
10440 7 S 0:00 ftppd: vestax.domain.com: anonymous/ssah@domain.com: IDLE
10501 7 ? 0:00 ftppd: toybox.domain.com: heidi: RETR mklinux-ALL.sit.bin
2 users (-1 maximum)
```

# ftpcount

`ftpcount` 是 `ftpwho` 的简化版本，显示 `ftpass` 中定义的每个类的当前用户总。`ftpcount` 的示例输出所示：

```
Service class all - 2 users (-1 maximum)
```

# 使用 FTP 客户端

本节介绍了随 SuSE 6.2 几个 FTP 客户端。虽然古老的 `ftp` 命令一直是全球数百万用户首选的网络文件传输工具，但仍有改进空间。然而，`ftp` 命令有许多许多用户可能不知道的功能。大多数新手和资深 Linux 用户都已如何在命令行中使用 `ftp` 配合远程计算机名称访问 FTP（如在本章开头所述）。你还可以使用 FTP 的 `-a` 命令行选项加速匿名登录。

用户可能对 `wget` 包感兴趣。`wget` 能够通过单条命令行命令使用 FTP 或 HTTP 下载软件，例如：
`get ftp://aptiva.home.org/home/bball/happy2.jpg`

> 注意
> SuSE 用户可以使用 SuSE `ftp` 客户端对 FTP 服务器实现相同的效果：
> `ftp://aptiva.home.org/home/bball/happy.jpg`

注意，尽管这些实用程序某些允许在命令行上指定密码，但这样做可能会带来安全风险，因此不建议。

另一个 `ftp` 命令功能是 `.netrc`。你可以使用它完成与上述命令行示例相同的任务。首先，使用你喜欢的文本编辑器在主目录中创建 `.netrc` 文件；然后输入一系列类似下方的自动登录行：

```
machine aptiva.home.org

login bball

password mypassword

macdef init

get happy2.jpg

bye
```

> 警告
> `.netrc` 的一个缺点是密码以明文形式留在系统中。这会带来重大的安全风险。`.netrc` 文件的权限应设置为 `600`。

文件的第一行使用 `machine` 关键字来指定远程计算机。接下来的两行指定你的远程登录和密码。`macdef` 和 `init` 关键字指定自动执行宏的开始。放置在这些关键字和两个空行之后的任何 FTP 命令都将被执行。在之前的示例中，使用 `get` 命令来检索文件 `happy2.jpg`，使用 `bye` 命令来退出连接。

保存 `.netrc` 文件并退出编辑器。接下来，使用 `chmod` 命令赋予该文件 600 的读写权限：

```
# chmod 600 .netrc
```
