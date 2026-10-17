
# 网络与互联网服务

## 第二部分

最后，要测试你的 `.netrc` 文件，请在命令行上配合远程计算机的主机使用 `ftp`：

```
# ftp aptiva
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
331 Password required for bball
230 User bball logged in.
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,26,35,0)
150 Opening ASCII mode connection for happy2.jpg (34636 bytes).
100% !******************************************* 34718 00:00 ETA
226 Transfer complete.
34718 bytes received in 0.05 seconds (698.5 KB/s)
221 Goodbye.
```

如你所示，`.netrc` 文件建立了连接、检索了文件并退出了连接。你可以使用这种方法定期从远程计算机检索文件（例如地图）；定期向远程站点上传文件（例如 Web 页面目录）；或者自动化其他文件传输任务（例如使用 `crontab` 条目定期远程传输系统日志）。

## autoexpect

工具丰富的 Linux 环境具有许多不同的软件工具（例如 `expect`），你可以使用它们来完成复杂的任务。自动化文件传输（和其他任务）的另一种方法是使用 `autoexpect` 命令。`autoexpect` 命令（随 `expect` rpm 包安装）会创建一个 `expect` 脚本，以完成在 `autoexpect` 会话期间执行的任务。

要自动化 FTP 传输，使用 `autoexpect` 命令的 `-f` 命令行选项，后跟所需的命令名称以及一个初始命令行：

```
# expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.
```

# FTP CHAPTER 10 351

Password:mypassword

```
230 User bball logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> get happy2.jpg

get happy2.jpg

local: happy2.jpg remote: happy2.jpg

227 Entering Passive Mode (192,168,23,6,54)

150 Opening Binary mode data connection for happy2.jpg (34636 bytes).

100%

****************************************************

-! 34636 00:00 ETA

226 Transfer complete.

34636 bytes received in 0.03 seconds (1.10 MB/s)

ftp> bye

bye

221 Goodbye.

autexpect done, file is eftp
```

此会话创建一个名为 `eftp` 的可执行文件，它连接到远程计算机、登录、检索文件 `happy2.jpg` 然后断开。要执行自动 FTP 会话，请在命令行输入 `eftp`：

```
# ./eftp
```
