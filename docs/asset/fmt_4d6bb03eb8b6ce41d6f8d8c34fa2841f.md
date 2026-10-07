
注意：或者你也可以按 `Control + D`。

- 远程系统已注销。

```
[ferro:-] user login achilles tcsnet.net
- 
last login Thu Jan Z 11:22:27 from achilles
bash-2.03 $ logout
login connection closed
[ferro:-] user
```

# 传输文件

你经常可以其他系统获取所需的文件和应用程序。你可以使用 `ftp` 在你的系统与其他系统之间移动文件。`ftp` 命令与 `telnet` 同样悠，几十年来一直让 Unix 用户能够上传和下载文件。它的用法非常简单，尽管 `ftp` 服务器提供了大量的命令。

在最简单的形式下，`ftp` 允许你登录到一个系统，使用 `put` 命令上传文件，使用 `get` 命令下载文件，并在远程系统的目录结构中移动。你可以以二进制模式或 ASCII 模式传输数据。ASCII 模式为文本文件设计，`ftp` 会在 Unix 和 DOS 系统之间进行翻译。二进制模式为软件、图像文件以及使用非打印字符的其他类型文件设计，这些字符可能会干扰传输。

一种流行的 `ftp` 形式被称为匿名 `ftp`（anonymous ftp）。当使用匿名 `ftp` 时，你输入用户名和电子邮件地址或任意字符作为密码。匿名 `ftp` 允许在系统中没有账户的人上传或下载文件。例如，为你的客户设置一个投放箱（drop box），让他们上传错误日志，这样你就可以分析他们在使用软件时遇到的问题。许多人选择匿名 `ftp`。就像 Apple 一样，向客户提供文档和软件工具，因此使用匿名 `ftp`。

在启动 `ftp` 会话之前，你应该先 `cd` 进入你想存储下载文件的目录。与 `telnet` 一样，在最初安装操作系统时，Mac OS 并没有启用 `ftp` 作为一项服务。

| 终端 | 文件 | 编辑 | 回滚查看 | 字体 | 窗口 | 帮助 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

```
[--]user ftp world.world.com
Connected to world.world.com.
world.world.com ftp server (Version 2.6.1 (5) May 21 20:22:19 IST 2001)
ready.
name= world.world.com (user)
331 Password required for less
331 Password required for less
230 User logged in.
Remote system type is UNIX.
Remote using binary mode to transfer files.
ftp>
lftp -l
```

注意：执行此任务你必须连接到互联网。

- 输入你想下载文件的系统名称并按回车键。

- 输入 `ftp` 后跟一个空格。

- 在提示处输入你的用户名和密码并按回车键。

- 输入 `ascii` 并按回车键。

- 文件开始下载。

# 使用内部命令操作

### 额外

如果你知道要找什么，弄清楚文件中哪里出了问题就会变得更容易。下载错误的文件会有问题。如果你传输的二进制文件实际上是文本文件，它们可能会损坏且无法使用。如果你尝试显示或以其他方式使用这些文件，系统将显示错误信息。

如果你从另一个系统以二进制模式下载文本文件，它们通常是没问题的。然而，以二进制模式下载的文件在每行的末尾可能会多出一个额外的字符。这个字符代表 Unix 系统不使用的回车符。当你用编辑器打开这些文件时，它会显示为 `^M`。

示例 更好地使用 ping：`ping` 是系统管理员排除网络相关问题最喜欢的工具之一，用于使用 Unix `tr` 命令移除这些不需要的字符。

示例：

```
[--] cat textfile | tr -d "" > textfile
```

```
[--] mv textfile
```

| 终端 | 文件 | 编辑 | 回滚查看 | 字体 | 窗口 | 帮助 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 238 User logged in. | | | | | | |

| Remote system is UNIX | | | | | | | |

| 500 ERROR: command not understood. | | | | | | |

| 150 Opening ASCII data connection for yo.txt | | | | | | |

| 226 transfer complete | | | | | | |

| 8 bytes received in 00 (0.01 KB/s) | | | | | | |

| 216 Binary | | | | | | |

| 227 Entering Mode | | | | | | |

| 150 Opening data connection for 2 | | | | | | |

| 2 bytes | | | | | | | |

| 100 ftp get size | | | | | | |

| typ1 | | | | | | |

| [--] user9@ftp.apple.com | | | | | | |

| 220 Welcome to ftp.apple.com. | | | | | | |

| 220 Pro Anonymous FTP Server | | | | | | |

| 230 Anonymous access denied. | | | | | | |

| 500 FTPS not understood. | | | | | | |

| 227 Transfer complete. | | | | | | |

| 150 Opening ASCII mode connection for file list | | | | | | |

| drwxr-xr-x root 19:48 | | | | | | |

| drwxr-xr-x ftp 1024 May 18 | | | | | | |

| drwxr-xr-x root 1024 200 | | | | | | | |

2

 May 18 20:59 | | | | | | |

| 226 Transfer complete. | | | | | | |

| 220 Goodbye. | | | | | | |

# 使用匿名 FTP

- 1 输入你想下载文件的系统名称并按回车键。

- 2 输入 `ftp` 后跟一个空格。

- 3 在提示处输入你的用户名和密码并按回车键。

- 4 输入 `ascii` 并按回车键。

- 5 文件开始下载。

# 更安全地操作计算机

# 更安全地登录

使用 `ssh` 比使用 `telnet` 或 `login` 登录远程系统更安全。`telnet`、`login` 和 `ftp` 命令以明文传输用户名和密码。位于你与系统之间网络路径上的任何人都可以“嗅探”包括登录信息在内的网络流量。由于这个原因，人们创建了安全工具，可以在不暴露密码和账户的情况下提供远程登录和文件传输。对于某些 `ssh` 连接，可以使用用户名/密码对登录。其他人可能提供数字证书。

对于用户来说，在 `telnet` 或 `login` 中使用 `ssh` 区别不大。如果使用用户名和密码登录，过程和结果几乎相同。加密和解密是透明的。当连接客户端和服务器安装了数字证书时，登录过程可能会简化。然而，这种登录仅适用于安装了证书的系统。

同样，你可以使用 `sftp` 替代 `ftp` 来传输文件。当你使用 `sftp` 时，文件下载过程中是安全的。

## 使用网络命令操作

如果你需要一个远程系统上的文件，并且受限于只能使用安全连接，你仍然可以下载文件，但必须使用 sftp。当你使用 sftp 时，你下载的文件在远程服务器和你的系统之间是加密的，这使得下载敏感文件更加安全。你可以按照上述描述的方法使用 sftp 下载文件，也可以在终端中输入单行命令。输入下方所示的行，并将命令中括号内的部分替换为你的数据。

示例：

```
[ferro:-] sftp user@remote.system.net:/home/user/file.txt
```

```
Connecting to remote.system.net...
user@remote.system.net's password:
Fetching /home/user/file.txt to file.txt
```

# 安全地传输文件

- 1 输入 `sftp` 后紧跟一个空格。

- 2 输入你的用户名后跟一个 `@` 符号。

- 3 输入远程系统的名称并按回车键（Return）。

- 4 在提示符处输入你的密码。

你已通过 sftp 登录。

- 5 输入并按回车键以显示远程账户中的文件列表。

- 6 输入 `get` 后紧跟一个空格。

- 7 输入文本文件的名称并按回车键下载该文件。

- 8 输入 `bye` 退出。

## UNIX 网络文件

你可以使用 `curl` 命令非常费力地下载文件。下载网页最显而易见的方法是在浏览器的地址栏中输入 URL 或使用“另存为”功能，但这并不一定是最简单或最高效的方法。UNIX 包含一个名为 `curl` 的命令行工具 - 用于下载网页。Curl 支持多种协议，包括 HTTP、HTTPS、FTP、GOP、DICT、TELNET、LDAP 等。

`curl` 不仅允许你在命令行中下载网页，还允许你在脚本中使用 `curl` 命令下载文件。事实上，你可以在完全完全无人值守的情况下下载并安装文件。`curl` 命令的语法足够灵活，允许你通过单个命令访问多个页面或网站。

要使用 `curl`，你输入 `curl` 后跟你想要指定的任何选项以及 URL 字符串。类似 `curl -O http://www.sandrich.com/index.html` 的命令将使用相同文件名从指定网站打开文件到你的当前目录。使用 `-o`，`curl` 命令会将文件下载到屏幕并向你展示 HTML。

`Curl` 允许你复制不仅是网页。你也可以用它下载二进制文件，包括图像文件和软件。事实上，该命令非常强大，设计用于从互联网定位和下载应用程序的 Unix 工具经常使用 `curl` 来下载数据。你可以使用通配符扩展字符串以匹配搜索内容。例如，使用 `*.[a,b,c].com` 来匹配三个系统 - www.a.com、www.b.com 和 www.c.com。

## 复制网页

- 输入 `-O` 后紧跟一个空格。

- 输入包含范围的 URL 并按回车键。

注意：执行这些任务时必须连接互联网。

- 1 输入 `curl` 后紧跟一个空格。

- 2 指定的页面将下载。

- 3 在终端中，输入 `curl` 后紧跟一个空格。

- 4 输入网页的 URL 并按回车键。

- 5 下载的页面保持相同的文件名。

- 6 输入 `-O` 后紧跟一个空格。

## 使用网络命令操作

## 应用它

`Curl` 可以可以向网站发送 POST 请求，也可以下载各种类型的文件。POST 命令包括要执行的脚本名称，以及你在在线表单中输入的参数。你需要了解一些表单的知识才能成功向其提交数据。下面的示例假设参数 `birthyear` 和 `vote` 被在线表单收集。它还假设当按下按钮且 `press` 的值等于 `OK` 时数据会进行处理。

`curl` 中的一个 post 命令可能如下所示：

```
curl -d 'birthyear=1985&vote=1&press=OK' www.site.com/vote.cgi
```

这种类型的命令可以用于脚本以实现自动化提交。要了解更多关于 `curl` 以及你如何在脚本中使用它，你可以阅读手册页（man page）或在线下载教程。

## 输入此内容：

## 结果：

```
[ferro-] curl -O http://url.planetmirror.com/docs/httpscript.html
```

`httpscript.html` 教程已下载。

## 下载二进制文件

- 1 输入 `curl` 后紧跟一个空格。

- 2 输入 `-O` 后紧跟一个空格。

- 3 输入包含压缩 tar 文件的网页 URL 并按回车键。

注意：在拨号连接上，这可能需要一些时间来下载指定的二进制文件。

## 使用 CURL 创建下载网页的脚本

- 1 启动编辑器创建一个名为 `url` 的文件。

- 2 输入 `/bin/touch` 并按回车键。

- 3 输入 `-n "URL"` 并按回车键，然后设置 URL 并按回车键。

### 4 输入 `; curl -O $URL`

- 5 保存文件并退出。

## 开启计算机的远程访问

你可以允许他人登录你的计算机，或者让你能够从任何系统登录。虽然 Mac OS 系统让你轻松登录以浏览网页和下载文件，但它们不允许他人登录你的系统或在命令行中访问文件。如果你想使用这种访问类型，必须通过修改系统配置来启用它。或者，你可以配置服务启动。

*(注：由于原文中存在大量重复段落，此处遵循“不要重复输出原文”原则，仅翻译核心逻辑部分)*

## 使用网络命令操作

如果你需要一个远程系统上的文件，并且受限于只能使用安全连接，你仍然可以下载文件，但必须使用 sftp。当你使用 sftp 时，你下载的文件在远程服务器和你的系统之间是加密的，这使得下载敏感文件更加安全。你可以按照上述描述的方法使用 sftp 下载文件，也可以在终端中输入单行命令。输入下方所示的行，并将命令中括号内的部分替换为你的数据。

示例：

```
[ferro:-] sftp user@remote.system.net:/home/user/file.txt
```

```
Connecting to remote.system.net...
user@remote.system.net's password:
Fetching /home/user/file.txt to file.txt
```

# 安全地传输文件

- 1 输入 sftp 后紧跟一个空格。

- 2 输入你的用户名后跟一个 `@` 符号。

- 3 输入远程系统的名称并按回车键。

- 4 在提示符处输入你的密码。

你已通过 sftp 登录。

- 5 输入并按回车键以显示远程账户中的文件列表。

- 6 输入 get 后紧跟一个空格。

- 7 输入文本文件的名称并按回车键下载该文件。

- 8 输入 bye 退出。

## UNIX 网络文件

你可以使用 curl 命令非常费力地下载文件。下载网页最显而易见的方法是在浏览器的地址栏中输入 URL 或使用“另存为”功能，但这并不一定是最简单或最高效的方法。UNIX 包含一个名为 curl 的命令行工具 - 用于下载网页。Curl 支持多种协议，包括 HTTP、HTTPS、FTP、GOP、DICT、TELNET、LDAP 等。

curl 不仅允许你在命令行中下载网页，还允许你在脚本中使用 curl 命令下载文件。事实上，你可以在完全完全无人值守的情况下下载并安装文件。curl 命令的语法足够灵活，允许你通过单个命令访问多个页面或网站。

要使用 curl，你输入 curl 后跟你想要指定的任何选项以及 URL 字符串。类似 curl -O http://www.sandrich.com/index.html 的命令将使用相同文件名从指定网站打开文件到你的当前目录。使用 -o，curl 命令会将文件下载到屏幕并向你展示 HTML。
