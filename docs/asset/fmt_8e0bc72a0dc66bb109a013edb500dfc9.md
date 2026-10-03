
到本地目录的窗口。CTRL-点击执行的是复制操作，而不是移动。当文件下载时，会出现一个对话窗口显示进度。

## gFTP

该 FTP 程序是一个简单的 GNOME FTP 客户端，旨在让您进行标准的 FTP 文件传输（见图 8-6）。gFTP 窗口由几个面板组成。左上面板列出您本地目录中的文件，右上面板列出您的远程目录。子目录具有文件夹图标，通过双点条目 (`..`) 引用，每个列表顶部有一个向上箭头。双击目录条目即可访问它。所有目录的路径显示在每个面板上方的框中。如果您想，可以为不同的目录输入新名称进行更改。

![](img/660de85fae8d68d8e30eb0e48a1ee77d_259_0.png)

图 8-6：gFTP FTP 客户端

面板之间的两个按钮用于传输文件。左箭头 `<` 下载远程目录中的选定文件，右箭头 `>` 从本地目录上传文件。要下载文件，请在右侧面板点击它并点击左箭头 `<`。文件下载完成后，其名称将出现在左侧面板的您的本地目录中。窗口顶部的菜单允许您管理传输。连接管理器允许您输入特定站点的登录信息。您可以指定是执行匿名登录还是提供用户名和密码。点击“连接”连接到该站点。站点下拉菜单允许您选择请求的站点。中断的下载可以轻松重启。

## wget

`wget` 工具让您能够轻松访问特定目录和文件的 Web 和 FTP 站点。目录可以递归下载，让您可以复制整个网站。`wget` 将您想要的文件或目录的 URL 作为选项。有用的选项包括 `-q` 静默模式、`-r` 递归（目录）、`-b` 在后台下载以及 `-c` 继续下载已中断的文件。其缺点之一是，您的 URL 引用可能非常复杂。您必须已经知道 URL。您无法像使用 FTP 客户端那样交互式地定位项目。以下命令将在后台下载 Fedora 安装 DVD。

```
wget -b ftp://download.fedora.redhat.com/pub/fedora/linux/releases/8/Fed/i386/iso/FC-8-i386-DVD.iso
```

提示：使用 Gnome Wget 工具，您可以使用 GUI 界面运行 `wget`。选择“应用程序 \| Internet \| 下载管理器”来显示 Gnome。

## curl

`curl` 客户端的操作方式与 `wget` 类似，但灵活性更高。通过 `curl`，您可以在命令行上指定多个 URL。您还可以使用大括号来指定多个匹配的 URL，例如具有相同域名的不同 Web 站点。您可以在大括号内列出不同的 Web 站点主机名，随后是域名（或反之）。您还可以使用括号指定多个项目的范围。这对于下载具有相同根名但不同期数的同一份杂志存档文件非常有用。`curl` 可以使用任何协议进行下载，并在未提供协议时将尝试智能地猜测协议。更多信息请查看 `curl` man 手页。

## ftp

`ftp` 名称指代在 Unix 和 Linux 系统上原始 FTP 客户端。`ftp` 客户端使用命令行界面，拥有一系列丰富的命令和选项供您管理 FTP 传输。您可以在 shell 提示符处输入 `ftp` 命令来启动 `ftp` 客户端。如果您有一个想要连接的特定站点，可以在命令行 `ftp` 关键字之后包含该站点的名称。否则，您需要在打开 `ftp` 命令后连接到远程系统。系统会提示“to”以输入远程系统名称。当您输入远程系统名称时，`ftp` 连接到该系统并提示输入登录名。登录名提示由“Name”一词以及括号中的系统名称和您的本地登录名组成。有时远程系统上的登录名与您本地系统的登录名相同。如果名称相同，在提示处按回车。如果不同，输入远程系统的登录名。输入登录名后，系统会提示输入密码。在下一个示例中，用户连接到远程系统 `garnet` 并登录到 `robert` 账户：

```
$ ftp
ftp> garnet
(to) garnet
Connected to garnet.berkeley.edu.
220 garnet.berkeley.edu FTP server ready.
Name (garnet.berkeley.edu:root): garnet
password required
Password:
user robert logged in
```

一旦登录，您可以在远程系统或您的本地系统上执行 Linux 命令。在 `ftp` 中，通过在命令前加感叹号在本地系统执行命令。任何不带感叹号的 Linux 命令都将在远程系统上执行。该规则有一个例外：虽然您可以使用 `cd` 命令更改远程系统上的目录，但要更改本地系统上的目录，需要使用名为 `lcd` (local cd) 的特殊 `ftp` 命令。在下一个示例中，第一个命令列出远程系统中的文件，而第二个命令列出本地系统中的文件：

```
ftp> ls
ftp> !ls
```

`ftp` 程序提供了一组管理远程系统文件和目录的基本命令，前提是您拥有权限。

| 命令 | 说明 |
| :--- | :--- |
| `ls` | 列出远程系统上的文件 |
| `!ls` | 列出本地系统上的文件 |
| `get` | 从远程系统下载文件 |
| `put` | 向远程系统上传文件 |
| `mkdir` | 在远程系统上创建目录 |
| `rmdir` | 删除远程系统上的目录 |
| `delete` | 删除远程系统上的文件 |
| `rename` | 重命名远程系统上的文件 |
| `quit` | 结束 `ftp` 会话 |
| `bye` | 退出 `ftp` 会话 |
| `mget` | 从远程系统下载多个文件 |
| `mput` | 向远程系统上传多个文件 |
| `ascii` | 将传输模式设置为 ASCII |
| `binary` | 将传输模式设置为二进制 |
| `lcd` | 更改本地目录 |
| `cd` | 更改远程目录 |

`ftp` 程序提供了一组管理远程系统文件和目录的基本命令，前提是您拥有权限。

## ftp 客户端命令参考

| 命令 | 效果 |
| --- | --- |
| `ftp` | 调用 `ftp` 程序。 |
| `open site-address` | 开启与另一个系统的连接。 |
| `close` | 关闭与系统的连接。 |
| `quit` or `bye` | 结束 `ftp` 会话。 |
| `ls` | 列出目录内容。 |
| `dir` | 以长格式列出目录内容。 |
| `get filename` | 将文件从远程系统发送本地系统。 |
| `put filename` | 将文件从本地系统发送到远程系统。 |
| `mget regular-expression` | 允许从远程系统同时下载多个文件。你可以使用特殊字符指定文件。 |
| `mput regular-expression` | 允许一次性向远程系统发送多个文件。你可以使用特殊字符指定文件。 |
| `unique` | 切换是否使用唯一文件名存储文件，如果本地系统已存在该文件，则将生成新文件名。 |
| `re filename` | 从中断的地方继续传输中断的文件。 |
| `binary` | 以二进制模式传输文件。 |
| `ascii` | 以 ASCII 模式传输文件。 |
| `cd directory` | 更改远程系统的目录。 |
| `lcd directory` | 更改本地系统的目录。 |
| `help` or `?` | 列出 `ftp` 命令。 |
| `mkdir directory` | 在远程系统上创建目录。 |
| `rmdir` | 删除远程目录。 |
| `delete filename` | 删除远程系统上的文件。 |
| `mdelete file-list` | 同时删除多个远程文件。 |
| `rename` | 重命名远程系统上的文件。 |
| `hash` | 下载期间显示进度哈希符号。 |
| `status` | 显示 `ftp` 的当前状态。 |

表 8-6：ftp 客户端命令

```
ftp mget
(remote-files) *.c
mget calc.c? y
PORT command successful
ASCII data connection
ASCII transfer complete
mget main.c? y
PORT command successful
ASCII data connection
ASCII transfer complete
ftp>
```

如果你计划下载大量文件（例如系统更新文件），那么为每个文件回答提示可能是一项繁琐的任务。在这种情况下，你可以关闭提示命令，该命令可以切换交互模式的开启和关闭。`mget` 操作将一个接一个下载它匹配的所有文件。

```
ftp prompt
Interactive mode off.
ftp mget
(remote-files) *.c
PORT command successful
ASCII data connection
ASCII transfer complete
PORT command successful
ASCII data connection
ASCII transfer complete
ftp>
```

`ftp` 客户端具有自动登录能力并支持宏。这两者都输入在用户的名为 `.netrc` 的 `ftp` 配置文件中。每当你连接到一个站点时，系统都会检查 `.netrc` 文件中的连接信息，例如用户名和密码。这样，你就不需要每次连接到站点时都输入用户名和密码。此功能对于匿名登录特别有用。你不需要输入用户名“anonymous”并将你的电子邮件地址作为密码，它们可以从 `.netrc` 文件中自动读取。你甚至可以将匿名登录信息设置为默认值，这样除非另有指定，否则对于尝试连接的任何 FTP 站点都会尝试匿名登录。如果你有需要登录的站点，可以在 `.netrc` 文件中指定它们，并在连接时，自动使用该站点的用户名和密码登录，或者被提示输入它们。

`.netrc` 文件中的条目具有以下语法。站点的条目以“machine”术语开始，后面是网络或 Internet 地址，然后是登录和密码信息。

```
machine system-address login remote-login-name password password
```

以下示例显示了在 `turtle.trek.com` 系统上登录 `dylan` 账户的条目：

```
machine golf.mygames.com login dylan password legogolf
```

对于你需要匿名登录的站点，你可以在登录名输入“anonymous”，并将你的电子邮件地址作为密码。

```
machine download.fedora.redhat.com login anonymous password dylan@turtle.trek.com
```

在大多数情况下，你使用的是 `ftp` 访问匿名 FTP 站点。与其尝试为每个站点都创建一个条目，不如为匿名 FTP 登录创建一个默认条目。当你连接到站点时，`ftp` 会在 `.netrc` 文件中查找宏条目。如果不存在，`ftp` 会查找默认条目并使用它。默认条目以“default”单词开头，没有网络地址。将匿名登录设置为你的登录方式，并将你的电子邮件地址设置为你的登录和密码。

```
default login anonymous password dylan@turtle.trek.com
```

这里显示了一个带有宏定义和默认条目的示例 `.netrc` 文件内容：

```
machine golf.mygames.com login dylan password legogolf
default login anonymous password dylan@turtle.trek.com
```

你也可以在 `.netrc` 文件中定义宏。通过宏，你只需使用宏名即可一次执行多个 `ftp` 操作。宏在连接期间有效。你可以在 `ftp` 命令行中、在连接期间定义宏。当你关闭连接时，宏会失效。尽管在 `.netrc` 条目中定义它们更有意义。这样一来，你就不需要重新定义它们。它们会自动从 `.netrc` 文件中读取并为你定义好。在 `.netrc` 文件中，在 `machine` 条目中定义的宏仅在你连接到该站点时才会定义。

宏定义的语法如下。它以 `macdef` 关键字开头，后跟着你想给它定义的名称，并以空行结束。宏可以接受参数，在宏中使用 `$1` 来引用第一个参数，`$2` 引用第二个，依此类推。如果你需要在宏中使用 `$` 字符，必须使用反斜杠进行引用。

```
macdef macro-name
ftp commands
empty line
```

接下来定义的 `fedup` 宏切换到一个目录，然后下载当前版本的更新。它还切换到一个用于放置更新文件的本地目录。`prompt` 命令关闭了每个文件的下载提示。`mget` 命令随后下载文件。该宏假设你已经连接到 Fedora 站点。

```
macdef fedup
cd /fedora/linux/updates/8/i386
lcd /root/fedup
prompt
mget *
```

这是一个示例 `.netrc` 文件的内容，其中为特定和默认条目定义了宏。每个宏定义后都有一个空行。你可以为 `machine` 或默认条目定义多个宏。在 `machine` 条目后的宏定义将为该连接自动定义。

```
machine download.fedora.redhat.com login anonymous password dylan@turtle.trek.com

# 从 Fedora 站点下载更新的宏
macdef fedup
cd /fedora/linux/updates/8/i386
lcd /root/fedup
prompt
mget *

default login anonymous password dylan@turtle.trek.com
macdef ls
!ls
```

## lftp

`lftp` 程序是一个增强型 FTP 客户端，具有高级功能，例如下载镜像站点和同时在后台运行多个 FTP 操作的能力。它使用的命令集与 `ftp` 客户端类似。使用 `get` 和 `mget` 命令下载文件，并使用 `-o` 选项选择本地位置。使用 `lcd` 和 `cd` 更改本地和远程目录。

为了管理后台命令，你可以使用许多与 shell 相同的命令。在命令末尾加上 `&` 会将其放入后台。使用 `CTRL-Z` 将正在运行的任务置于后台。命令可以使用括号分组并一起放入后台。使用 `jobs` 命令列出你的后台作业，并使用 `wait` 和 `fg` 命令将作业从后台移动到前台。当你退出 `lftp` 时，程序将继续运行任何后台作业。实际上，`lftp` 本身也变成了一个后台作业。

当你连接到某个站点时，可以使用 `queue` 命令对命令进行队列，设置一个要执行的 FTP 操作列表。通过此功能，你可以为某个站点队列多个下载操作。如果需要，可以对队列进行重新排序或删除。你还可以连接到多个站点并为每个站点设置一个队列。`mirror` 命令允许你维护镜像站的本地版本。你可以下载整个站点，或者仅更新新文件，并删除镜像站上不再存在的文件。

你可以通过设置 `/etc/lftp.conf` 文件中的选项来定制 `lftp`。系统级设置放置在该文件中。在这里，你可以设置提示用户输入匿名密码的功能。`lftp` 目录包含了对命令历史、日志、书签和启动命令的支持功能。`lftp` 程序还支持 `.netrc` 文件，并检查其以获取登录信息。

## Talk 与即时消息客户端：VoIP、ICQ、IRC 和 IM

你可能有时与网络上的其他用户直接通信。你可以通过 VoIP、ICQ、IM（即时消息）和 IRC 工具实现这一目的，前提是另一个用户同时登录在已连接的系统中（见表 8-7）。通过越网络语音（Voice over the Internet Protocol）应用程序，你可以通过互联网连接进行通话，就像在电话上一样。

| 客户端 | 说明 |
| --- | --- |
| Ekiga | VoIP |
| Pidgin | 支持所有即时消息协议的界面，包括 MSN、AIM、Yahoo、MySpaceIM、ICQ、XMPP 和 IRC。Pidgin 曾名为 GAIM。 |
| X-Chat | 互联网聊天 (IRC) 客户端，也拥有 GNOME 版本 `gnome-xchat`。 |
| Konversation | KDE IRC 客户端 |
| Gabber | Jabber 客户端 (XMPP) |
| psi | 使用 QT (KDE) 的 Jabber 客户端，XMPP |
| Finch | 基于命令行光标的 IRC、ICQ 和 AIM 客户端 |
| naim | 基于命令行光标的 IRC、ICQ 和 AIM 客户端 |

表 8-7：Talk 与即时消息客户端

ICQ (I Seek You) 是一种互联网工具，它会在其他用户在线时通知你，并允许你与他们通信。ICQ 的工作方式类似于即时消息软件。通过互联网聊天 (IRC) 工具，你可以连接到一个其他用户也连接在远程服务器，并与他们聊天。

注意：Talk 工具是一个较旧的 Unix 命令行工具，其原理类似于双向文本消息工具，允许你与另一个用户进行直接的文本对话。Talk 是为同一系统或通过局域网连接的用户设计的。

## IM

即时消息 (IM) 客户端的工作方式与 ICQ 类似，允许同一 IM 系统上的用户跨越互联网进行通信。目前，一些主要的 IM 系统包括 AIM (AOL)、微软网络 (MSN)、Yahoo、ICQ 和 Jabber。与其他系统不同，Jabber 是一个开源即时消息软件 (www.jabber.org)。它使用由 XMPP 开发的 XML 协议，即可扩展的消息传递和存在性协议 (www.xmpp.org)。
