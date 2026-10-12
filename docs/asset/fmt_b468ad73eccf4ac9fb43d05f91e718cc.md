
如果你是一个命令行狂热者，你会喜欢 Windows 自带的 FTP 命令。它并不漂亮，但能完成工作。在章节的末尾，你可以找到命令参考，详细列出了你可以与 FTP 命令一起使用的子命令。在本节中，我展示了一个典型的会话，你登录到名为 `ftp.com` 的 FTP 服务器，切换到名为 `pics` 的目录，下载一个文件，然后退出。

首先，打开一个命令窗口；为此，按 开始+运行，在文本框中输入 `cmd` 并点击确定。然后，导航到你想下载文件所在的目录。这一步很重要，因为你可以在 FTP 命令内部更改本地工作目录，从正确的目录启动 FTP 更容易。

要启动 FTP，输入带有 FTP 服务器名称作为参数的 `ftp`，如下：

```
>ftp ftp.com
```

假设你输入了正确性，FTP 连接到站点，显示横幅消息并提示你登录：

```
220 Connected to ftp.com.
220 Microsoft FTP Service
220 We have 999 users here, but there's always room for one!
User (ftp.com):
```

要匿名登录，输入 `Anonymous` 并回车。服务器响应允许匿名访问：

```
Anonymous
230 Anonymous logged in.
Password:
```

输入密码后，出现 `ftp` 提示：

```
230 Welcome to my FTP site!
230 Anonymous logged in, check out the pictures.
ftp>
```

通过输入 `dir` 命令查看目录列表：

```
>dir
250 PORT command successful.
150 ASCII mode connection for /bin/
06-03-03 08:05PM <DIR> pics
06-03-03 07:55PM 2365 readme.txt
06-03-03 07:56PM <DIR> videos
222 Transfer complete.
ft: 190 bytes received in 0.00 seconds 190.0K/sec.
ftp>
```

如所示，`dir` 命令的响应没有 MS-DOS 命令那样清晰。尽管如此，你可以识别出名为 `pics` 和 `videos` 的子目录，以及名为 `readme.txt` 的单个文件。该文件的大小为 2365 字节。

我想下载的文件位于 `pics` 子目录，因此下一个命令是 `cd pics`。结果如下：

```
>cd pics
250 CWD command successful.
ftp>
```

再次，命令的输出并不像你预期的那样。FTP 协议实际上并没有 CWD 命令。相反，它使用一个名为 CWD（代表更改工作目录）的命令来更改目录。Windows FTP 客户端使用 `CD` 命令而不是 `CWD`，是为了与 Windows/MS-DOS 用户界面保持一致，因为后者使用 `CD` 命令更改目录。当你在 `ftp>` 提示符输入 `CD` 命令时...

## 使用 FTP 命令行客户端

在提示符处，FTP 客户端向 FTP 服务器发送 `CWD` 命令。服务器随后回复“CWD command successful”（命令执行成功），表示目录已更改。

接下来，再次输入 `dir`。FTP 服务器显示 `pics` 目录的目录列表：

```
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
06-27-03 10:04AM 12316 door.jpg
06-27-03 10:06AM 112457 eclair.jpg
06-27-03 10:06AM 81610 fence.jpg
06-27-03 10:09AM 138102 fog.jpg
06-27-03 10:09AM 83712 gallows.jpg
06-27-03 10:10AM 166741 ghost.jpg
06-27-03 10:09AM 119859 skel01.jpg
06-27-03 10:05AM 87720 wall.jpg
```

```
226 Transfer complete.
ft: 400 bytes received in 0.00Seconds 400000.0Kbytes.
ftp>
```

在这里，我们可以使用包含八个文件的 `pics` 目录。要下载文件，您可以使用 `GET` 命令并指定想要下载的文件名。例如，要下载 `door.jpg` 文件，输入 `get door.jpg`。FTP 服务器将文件传输到您的计算机并显示以下响应：

```
200 PORT command successful.
150 Opening ASCII mode data connection for door.jpg(123126 bytes).
226 Transfer complete.
ft: 123126 bytes received in 0.13Seconds 985.01Kbytes.
ftp>
```

注意，响应表明服务器实际接收到的命令是 `PORT` 命令。文件以 ASCII 模式传输。整个传输过程耗时 0.13 秒，折合传输速度约为每秒 985KB。

现在您已经下载了文件，可以通过输入 `bye`结束会话。FTP 通过显示网站的欢迎消息作为响应；然后将您返回到 MS-DOS 提示符：

```
221 Hurry Back...
C:\>
```

当然，FTP 的操作比此会话所示的复杂得多。尽管如此，FTP 最常用的用途是下载文件，而大多数下载操作并不比此示例复杂。

## FTP 命令和子命令参考

本章的其余部分是 FTP 命令参考。在接下来的章节中，您可以找到 FTP 命令及其所有子命令的完整参考信息。本节的第一个命令是 FTP 命令本身。之后，所有 FTP 命令的子命令将按字母顺序列出。

### ftp 命令

功能：启动 FTP 客户端，以便您在 FTP 服务器之间传输文件。

语法：`ftp [-v] [-d] [-i] [-n] [-g] [-s:filename] [-a] [-windowsize] [-A] [host]`

- 参数：

- `-v` 关闭详细模式（Verbose mode）。
- `-d` 开启调试模式（Debug mode）。
- `-i` 关闭提示符模式（Prompt mode）。
- `-n` 强制手动登录。
- `-g` 关闭通配符模式（Glob mode）。
- `-s` 指定包含 FTP 命令的脚本文件。
- `-a` 指定可以使用任何网络接口来绑定数据连接。
- `-w` 指定传输缓冲区的大小。默认值为 4K。
- `-A` 自动以匿名用户（Anonymous）身份登录。

`Host`：您想要连接的 FTP 服务器。这可以是服务器的 DNS 名称或 IP 地址。

示例：

`ftp ftp.lowewriter.com`

`ftp ftp.lowewriter.com -A`

更多信息：与大多数 Windows 命令不同，此命令的开关是以连字符 `-` 开头，而不是斜杠 `/`。

如果您想编写子命令脚本，请使用 `-s`开关。FTP 不支持输入重定向。

当 FTP 运行时，会出现 `ftp>` 提示符。当显示此提示符时，您可以输入本章其余部分的任何 FTP 子命令。

### ! (转义)

功能：转义到命令 shell。

语法：`!`

更多信息：此命令会弹出一个临时命令提示符，以便您输入命令。要返回 `ftp>` 提示符，请输入 `exit`。

### ? (帮助)

功能：显示帮助信息。

语法：

`? [command]`

`help [command]`

示例：

`help mput`

更多信息：

`?` 和 `help` 可以互换。如果您单独输入 `?` 或 `help`，将出现 FTP 命令列表。如果您输入 `?` 或 `help` 后跟命令，将显示该命令的帮助。

### append

功能：将文件追加到现有文件的末尾。

语法：`append localfile [remotefile]`

示例：

`append extra.txt start.txt`

更多信息：

如果省略了 `remotefile` 参数，则假设远程文件与本地文件相同。

### ascii

功能：以 ASCII 模式传输。

语法：`ascii`

更多信息：文件以 ASCII 模式传输。

### bell

功能：在传输完成后发出蜂声。

语法：`bell`

更多信息：在传输完成后时发出蜂声。

### close

功能：关闭会话。

语法：`close`

### cd

功能：更改目录。

语法：`cd remotirectory`

### debug

功能：开启调试模式。

语法：`debug`

### delete

功能：删除文件。

语法：`delete`

### dir

功能：列出目录内容。

语法：`dir [remotirectory]`

### disconnect

功能：断开连接。

语法：`disconnect`

### glob
