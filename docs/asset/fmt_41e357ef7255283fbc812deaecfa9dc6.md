
其中 `hostname` 是你想要连接的 FTP 服务器名称。如果它是公共系统，请使用你的用户名和密码登录。以用户 `anonymous`（或 `ftp`）身份登录，并将你的电子邮件地址作为密码。在服务器上使用 `ls` 和 `cd` 命令，就像在 shell 中使用相应的工具一样。`get file` 命令将文件从本地系统复制到服务器，`status` 显示 FTP 连接的信息，`help` 显示命令列表。

除 `status` 之外，上述前述的命令在 `sftp`、`ftp` 和 `ncftp` 中也同样可用。

# 教程环节

以下是两个 `ftp` 会话，其中 Sam 向一个名为 `plum` 的 `vsfpd` 服务器传输并从那里下载文件。当 Sam 输入 `ftp plum` 命令时，本地 `ftp` 客户端连接到服务器，服务器会请求用户名和密码。由于他在本地系统中以 `sam` 身份登录，Sam 建议在 `plum` 上也以 `sam` 登录。要以 `sam` 登录，他只需按回车键。然而，由于他在 `plum` 上的用户名是 `sels`，因此他在 `Name (plum:sam):` 提示符处输入了 `sls`。当 Sam 用正常的系统密码响应 `Password:` 提示符后，`vsfpd` 向他表示问候并告知它正在使用二进制模式传输文件。通过 `ftp` 的二进制模式，Sam 可以传输 ASCII 和二进制文件（见第 708 页）。

```
$ ftp plum
Connected to plum (172.16.192.151)
220 (vsFTPD 2.3.4)
Name (plum:sam): sls
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

登录后，Sam 使用 `ftp ls` 命令查看远程工作目录中的内容，这是他在 `plum` 上的主目录。然后他 `cd` 到 `memos` 目录并显示那里的文件。

```
ftp ls 1s
227 Entering Passive Mode (172,16,192,131,249,127)
150 Here comes the directory listing.
drwxrxr-x 2 501 4096 Mar 03 02:52 expenses
drwxrxr-x 2 501 4096 Mar 03 02:54 memos
drwxrxr-x 2 501 4096 Mar 03 02:52 tech
226 Directory send OK.
```

```
ftp cd memos
250 Directory successfully changed.
```

```
ftp ls 1s
227 Entering Passive Mode (172,16,192,131,49,131).
150 Here comes the directory listing.
--rw-rw-r-- 1 501 87499 Mar 03 02:53 memo.0514
--rw-rw-r-- 1 501 58235 Mar 03 02:54 memo.0628
--rw-rw-r-- 1 501 58531 Mar 03 02:53 memo.0905
--rw-rw-r-- 1 501 12846 Mar 03 02:54 memo.0921
--rw-rw-r-- 1 501 76277 Mar 03 02:54 memo.1102
226 Directory send OK.
```

接下来，Sam 使用 `ftp get` 命令将 `memo.1102` 从远程复制到本地系统。他使用二进制模式确保无论文件是二进制还是 ASCII 格式都能获得良好的副本。服务器确认文件已成功复制，并报告其大小和复制所需的时间。然后 Sam 将本地文件 `memo1114` 复制到远程系统。该文件被复制到远程工作目录 `memos`。

```
ftp get memo1102

local: memo1102 remote: memo1102

227 Entering Passive Mode (172,16,192,131,151).

150 Opening BINARY mode connection for memo1102 (76271 bytes).

222 Transfer complete.

76271 bytes received in 0.136 secs (5588.44 Kbytes/sec)
```

```
ftp put memo1114
local: memo1114 remote: memo1114
227 Entering Passive Mode (172,16,192,131,213).
150 OK to send.
222 Transfer complete.
13023 bytes sent in 0.226 secs (5762.09 Kbytes/sec)
```

现在 Sam 决定将 `plum` 的 `memo` 目录中的所有文件复制到他本地系统上的新目录中。他输入 `ls` 以确保复制了正确的文件，但 `ftp` 超时了。他没有退出 `ftp` 并在 shell 中给出另一个命令，而是执行了 `ftp open plum` 来重新连接服务器。登录后，他使用 `ftp cd` 将服务器上的目录切换到 `memos`。

```
ftp ls
Passive mode refused.
ftp open plum
Connected to plum (172.16.192.151).
220 (vsSFTP 2.3.4)
Name (plum:sam): sls
ftp cd memos
250 Directory successfully changed.
```

此时，Sam 意识到他还没有为要下载的文件创建目录。他在 `plum` 上的工作目录中执行 `mkdir` 命令创建一个 `memos.hold` 目录。Sam 使用二进制模式确保无论文件是二进制还是 ASCII 都能切换到他在本地创建的 `memos.hold` 目录。Sam 使用 `lcd` 工作目录切换到 `memos.hold` 目录，以便 Sam 想要的文件放入 `memos.hold` 目录。Sam 使用 `pwd` 报告了 `ftp` 的新工作目录：

```
ftp> mkdir memos.hold
ftp> lcd
Local directory now /home/sam/memos
```

Sam 使用 `mget`（多个获取）命令配合通配符 `*` 将远程的所有文件复制到本地系统的 `memos` 目录中。当 `ftp` 提示第一个文件时，Sam 意识到他忘记关闭提示符，因此他响应 `n` 并按下 `CTRL-C` 停止复制文件。服务器检查他是否继续执行 `mget` 命令。

接下来 Sam 输入 `prompt` 命令，该命令会切换提示符状态（开启时关闭，关闭时开启）。现在当他给出 `mget` 命令时，`ftp` 会在不提示的情况下复制文件。获取所需文件后，Sam 输入 `quit` 命令关闭与服务器的连接，退出 `ftp` 并返回本地 shell 提示符。

```
ftp> mget *
mget memo.0514? n
mget memo.0628? CONTROL-C
Continue with mget? n
```

```
ftp> prompt
Interactive mode off.
```

```
ftp> mget *
local: memo.0514 remote:memo.0514
227 Entering Passive Mode (172,16,192,131,207,88).
150 Opening BINARY mode connection for memo.0514 (87499 bytes).
226 Transfer complete.
87499 bytes received in 0.012 secs (6912.55 Kbytes/sec)
local: memo.0628 remote:memo.0628
227 Entering Passive Mode (172,16,192,131,182,100).
150 Opening BINARY mode connection for memo.0628 (58235 bytes).
226 Transfer complete.
58235 bytes received in 0.0204 secs (2860.97 Kbytes/sec)
```

系统接受任何密码，按照惯例，你应当提供你的电子邮件地址。如果你正在登录公共网站，请勿使用重要的地址，因为该地址可能会根据此登录接收垃圾邮件。

许多系统允许匿名访问以便在 `pub` 目录下存储有趣的文件。大多数浏览器（如 Firefox）会在你点击文件名时在匿名 FTP 站点上登录并传输文件。

# 自动登录
