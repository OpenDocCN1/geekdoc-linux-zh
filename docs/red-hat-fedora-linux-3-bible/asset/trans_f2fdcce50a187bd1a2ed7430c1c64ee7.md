

要为后台传输选择文件，请使用 `bgget` 命令。以下是示例：

```
ncftp /pub > bgget wireless.doc
*Spooleid: get wireless.doc
ncftp /pub > jobs
--Scheduled--For----Host--Command----
2003-09-01 18:38 maple     GET wireless.doc
ncftp /pub > bgstart
Background process started.
Watch the "/home/br/.ncftp/spool/log" file to see how it is progressing
```

在此示例中，`bgget` 命令将远程当前目录（/pub）中的 `wireless.doc` 文件放入后台队列，并设置将其复制到本地当前目录。输入 `jobs` 命令显示，来自名为 maple 的主机的任务（GET `wireless.doc`）已调度为立即运行（2003 年 9 月 1 日，下午 6:38）。通过运行 `bgstart` 命令，该进程以及其他任何在队列中的任务都会立即运行。

您可以选择不立即开始后台传输，而是稍后执行。对于已在队列中等待传输的后台任务，当您退出 `ncftp`、离开当前 FTP 站点或前往另一个 FTP 站点时，传输才会开始。这样，执行传输的程序（`ncftpbatch`）就可以接管当前的登录会话以执行传输。

如果您希望等待更长时间才执行传输，可以向 `bgget` 命令传递一个选项，使其在特定时间开始传输。以下是示例：

```
ncftp /pub > `bgget -@ 2003090410000 wireless.doc`
```

使用此命令，传输被设置为在 2003 年 9 月 4 日上午 10:00 执行，以传输名为 `wireless.doc` 的文件。同样，您可以检查主目录中的 `.ncftp/spool/.log` 文件，查看传输是否已完成。

## 使用 gFTP 窗口

如果您更喜欢使用图形化界面访问 FTP 服务器，可以使用 gFTP 窗口。您可以通过输入 `gftp` 或在桌面上的 Red Hat 菜单中选择 Internet → gFTP 来打开 gFTP 窗口。图 9-10 展示了 gFTP 窗口的一个示例。

与 `ftp` 命令不同，gFTP 窗口允许您同时查看当前远程和本地目录的内容。要将文件从一侧传输到另一侧，只需双击它或将其拖放到另一个窗格中。（通常，您只是从 FTP 站点复制文件，除非该站点授予您写入权限。）

![](img/b22364e57409c2481ba806e4e6b9309c_375_0.png)

请按照以下步骤连接到 FTP 站点：

- 1. 在 Host 框中输入您想要连接的 FTP 服务器名称（例如，`ftp.redhat.com`）。
- 2. 输入 FTP 服务器上的端口号（您可以留空以使用默认端口号 21）。
- 3. 输入用于登录 FTP 服务器的用户名。如果您没有特定的用户名且服务器是公共访问的，请使用默认的 `anonymous`。
- 4. 输入您输入的用户名对应的密码。匿名 FTP 服务器的惯例是使用电子邮件地址作为密码。
- 5. 点击显示两个小监视器的图标以连接到 FTP 站点。
- 6. 如果信息输入正确，窗口底部窗格应显示传输已完成，右侧窗格应显示 FTP 站点当前目录的内容。连接后，您可以执行以下操作：
    - 移动位置。双击目录以移动到该目录，或双击两个点（. .）以上移一级。您可以对远程和本地目录都执行此操作。
    - 拖放文件。您可以将文件从 FTP 站点拖放到左侧窗格（代表当前本地目录）。
    - 保存此站点。如果您希望稍后返回此站点，请选择 Bookmarks → Add Bookmark。一个弹出窗口允许您为书签列表中的此站点命名。完成后，您可以稍后从列表中选择该条目以连接到该站点。gFTP 窗口不仅保存了主机名，还保存了端口、用户名和密码。因此，您只需单击一下即可连接。这是 gFTP 等图形化 FTP 程序的最佳功能之一。

gFTP 的一个不错功能是它会保存日志信息。选择 Logging → View Log。会出现一个窗口，显示您的计算机与每个 FTP 站点之间已发生的对话。您可以查看这些消息以了解当无法连接到站点时出了什么问题，或者回忆您在某个 FTP 站点上的访问记录和操作。

## 使用 wget 获取文件

如果您已经知道网络中某个文件的位置，那么比打开 FTP 会话、在 FTP 服务器上移动并运行 `get` 命令更高效的方法来下载该文件。`wget` 命令是一个简单、高效的工具，用于通过互联网进行非交互式文件下载。

如果您想从 FTP 服务器或 Web 服务器（HTTP）下载某个文件，并且确切知道文件的位置，`wget` 是一种很好的下载方式。如果您想将整个站点递归地从一台计算机复制到另一台计算机（例如，包含用户主目录），`wget` 命令非常有用。从 FTP 站点下载时，`wget` 可以让您仅作为匿名用户下载，或者在命令行中添加自己的用户名和密码。

以下是使用 `wget` 从 FTP 站点获取文件的示例：

```
$ wget ftp://ftp.redhat.com/pub/contrib/libc6/1386/zsh-4.1.1-1.1386.rpm
--01:53:33--  ftp://ftp.redhat.com/pub/contrib/libc6/1386
            => "zsh-4.1.1-1.1386.rpm"
Resolving ftp.redhat.com ... done.
Connecting to ftp.redhat.com[162.148.218.201]:21 ... connected.
Logging in as anonymous ... Logged in!
=> SYST ... done.    => PWD ... done.
=> TYPE I ... done.  => CWD /contrib/libc6/1386 ... done.
=> PASV ... done.    => RETR zsh-4.1.1-1.1386.rpm ... done.
     Length: 2,541,655 (unauthoritative)

100%[=======================================================================] 2,541,655  50.31K/s  ETA 00:00
05:16:39 (50.31 KB/s) - "zsh-4.1.1-1.1386.rpm" saved [2541655]
```

根据 URL 的第一部分（`ftp://`），`wget` 知道您正在使用 FTP 将文件复制到本地主机上的当前目录（`.`）。解析地址（`ftp.redhat.com`）后，`wget` 连接到该站点，以匿名用户身份登录，更改工作目录（到 `/pub/contrib/libc6/1386`），并传输文件。当文件下载时，`wget` 显示下载进度，然后退出。

如果需要以除匿名以外的用户身份登录，可以将该信息添加到命令行或主目录中的 `.netrc` 文件中（输入 `man netrc` 以查看该文件的格式）。以下是将密码添加到命令行的示例：

```
$ wget ftp://joe:my67chevy@ftp.handsonhistory.com/semol.doc .
```

> 注意：将密码添加到命令行会使密码暴露给旁观者。通常不建议这样做，除非没有人能看到您的监视器或您的历史文件。

在上面的示例中，用户以 joe 的身份登录，密码为 my67chevy。wget 随后从名为 ftp.handsonhistory.com 的主机计算机的当前目录中复制文件 semol.doc。该当前目录很可能是 /home/joe。

使用 wget，您还可以从 Web 服务器下载文件。如果文件地址以 http:// 开头，wget 命令使用 http 协议下载文件。下载单个文件时，您使用的格式与 FTP 文件相同（例如：wget http://host/File.）。HTTP 下载的最佳 wget 选项是 -r（递归）。

递归下载允许您选择 Web 站点上的一个点，并下载该点下方的所有内容。以下是使用递归下载来下载 www.handsonhistory Web 站点内容的示例。

```
$ wget -r www.handsonhistory.com .
```

在此示例中，构成 www.handsonhistory.com Web 站点的目录结构被复制到当前目录下的目录 www.handsonhistory.com 中。如果您想将 Web 站点的内容从一台计算机移动到另一台计算机，这将非常有用。

> 注意：下载整个 Web 站点可能会导致大量数据被下载。如果您只想要 Web 站点的一部分，请从站点结构中较低的一个点开始。因为内容是通过跟踪链接获取的，如果 Web 站点某个目录中有不在链接中的内容，它就不会被下载。

> 备注：另一个您可能感兴趣的类似于 wget 的命令是 curl 命令。与 wget 一样，curl 可以使用 ftp 或 http 协议下载文件。但是，它还支持安全的 http（https）、telnet 和 gopher 协议。Curl 还可以在同一连接上进行多文件传输。

## 使用 ssh 进行远程登录/远程执行

尽管 telnet 和 rlogin 登录命令以及 rsh 远程执行命令存在的时间更长，但 ssh 命令是远程登录和执行的推荐工具。原因是 ssh 提供加密通信，因此您可以在不安全的公共网络上安全地在互不认识的宿主之间使用它。

在以下示例中，ssh 用于登录名为 maple 的计算机。由于未指定用户，ssh 尝试以当前用户身份登录（在此情况下是 root 用户）。

```
# ssh maple
```

