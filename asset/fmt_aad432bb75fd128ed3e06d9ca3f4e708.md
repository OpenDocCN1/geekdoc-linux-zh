
- 客户端可以要求 FTP 服务器为数据传输建立 `PASV`（被动——默认）或 `PORT`（主动）连接。一些服务器仅限于一种类型的连接。被动和主动 FTP 连接之间的区别在于数据连接是由客户端还是服务器发起的。在被动模式下，客户端发起与服务器的连接（默认在 20 端口）；在主动模式下，服务器发起连接（没有默认端口；有关确定服务器使用哪些端口的参数，请参阅第 734 页的“连接参数”）。一种方法在本质上并不比另一种更安全。被动连接更常见，因为使用 NAT（第 910 页）的客户端可以连接到被动服务器，且编程可扩展的被动服务器更简单。

### FTP 客户端

- `ftp` Fedora/RHEL 提供了几个 FTP 客户端，包括 `ftp`（较旧版本的 BSD ftp 实用程序）。本节讨论 `ftp`，因为它被广泛使用，且大多数其他 FTP 客户端（包括 `sftp` 和 `lftp`）提供了 `ftp` 命令的超集。

- `sftp` 作为 OpenSSH 套件的一部分，`sftp`（`openssh-clients` 包）是 `ftp` 的安全且功能等效的替代方案。`sftp` 实用程序不是一个真正的 FTP 客户端——它不理解 FTP 协议。它将 `ftp` 命令映射到 OpenSSH 命令。有关更多信息，请参阅第 697 页。

- `lftp` `lftp` 实用程序（`lftp` 包）提供与 `sftp` 相同的安全性，但提供更多功能。有关更多信息，请参阅 `lftp` 手册页。

- `gftp` `gftp` 实用程序（`gftp` 包）是一个图形客户端，适用于 FTP、SSH 和 HTTP 服务器。此客户端具有许多有用功能，包括恢复中断的文件传输。有关更多信息，请参阅 `www.gftp.org` 和 `freshmeat.net/projects/gftp`。

- `ncftp` `ncftp` 实用程序（`ncftp` 包）是一个文本客户端，提供比 `ftp` 更多的功能，包括文件名补全和命令行编辑。有关详细信息，请参阅 `www.ncftp.com` 和 `freshmeat.net/projects/ncftp`。

## 更多信息

- 本地 在 `ftp>` 提示符下输入 `help` 或 `?` 以显示命令列表。在 `?` 后跟随一个空格和一个 `ftp` 命令以显示有关该命令的信息。

- 文件：`/usr/share/doc/vsftpd-*`

- 手册页：`ftp`, `sftp`, `lftp`, `ncftp`, `vsftpd.conf`

- Web `vsftpd` 主页：`security.appspot.com/vsftpd.html`

- HOWTO FTP `mini-HOWTO`

### 备注

运行 `ftp` 的 Linux 系统可以与支持 FTP 的众多操作系统中的任何一个交换文件。许多站点在 FTP 服务器上提供免费信息的存档，尽管对许多站点来说，这只是一个比更容易访问的网站替代方案（例如，请参阅 `ftp://ftp.ibiblio.org/pub/Linux` 和 `http://www.ibiblio.org/software/linux`）。大多数浏览器可以连接到 FTP 服务器并从中下载文件。

`ftp` 实用程序对文件系统命名或结构不做任何假设，因为你可以使用 `ftp` 与非 UNIX/Linux 系统交换文件（它们可能使用不同的文件命名约定）。

### 运行 ftp 和 sftp FTP 客户端

本节描述了如何使用 `ftp` 和 `sftp` FTP 客户端。这里涵盖的命令适用于这两种实用程序。

### 先决条件

安装以下软件包：

- `openssh-clients`（默认安装；包含 `sftp`）

- `ftp`

对于 `ftp` 或 `sftp` 客户端没有需要启动的服务。

### 快速入门 I：使用 ftp 下载文件

此快速入门部分分为两部分：基本命令的描述以及展示用户操作 `ftp` 的教程会话。

### 基本命令

输入命令

```
$ ftp hostname
```

其中 `hostname` 是你想要连接的 FTP 服务器的名称。如果你在服务器上有一个账户，请使用你的用户名和密码登录。如果是公共系统，请作为用户 `anonymous`（或 `ftp`）登录，并将你的电子邮件地址作为密码。在服务器上，使用 `ls` 和 `cd` `ftp` 命令，就像你在 shell 中使用相应的实用程序一样。`get file` 命令从服务器复制文件到本地系统，`put file` 命令从本地系统复制文件到服务器，`status` 显示有关 FTP 连接的信息，`help` 显示命令列表。

除 `status` 外，上述命令也可在 `sftp`、`lftp` 和 `ncftp` 中使用。

## 教程会话

以下是 Sam 在与名为 `plum` 的 `vsftpd` 服务器之间传输文件的两个 FTP 会话。当 Sam 执行命令 `ftp plum` 时，本地 `ftp` 客户端连接到服务器，服务器会要求输入用户名和密码。由于他在本地系统中以 `sam` 身份登录，`ftp` 建议 Sam 以 `sam` 身份在 `plum` 上登录。若要登录为 `sam`，他只需按 RETURN（回车键）即可。然而，由于他在 `plum` 上的用户名是 `sls`，因此在看到 `Name (plum:sam):` 提示时，他输入了 `sls`。当 Sam 用他常用的系统密码响应 `Password:` 提示后，`vsftpd` 服务器会向他致意，并告知他“正在使用二进制模式传输文件”。在二进制模式下，Sam 可以传输 ASCII 和二进制数据（第 720 页）。

### 连接和登录

```
$ ftp plum
Connected to plum (192.168.206.181).
220 (vsFTPd 3.0.2)
Name (plum:sam): sls
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
```

登录后，Sam 使用 `ftp ls` 命令查看其远程工作目录（即他在 `plum` 上的主目录）中有哪些内容。然后，他切换到 `memos` 目录并显示其中的文件。

### ls 和 cd

```
ftp> ls
227 Entering Passive Mode (192,168,206,181,246,88).
150 Here comes the directory listing.
drwxr-xr-x 2 1001 1001 4096 Jun 13 17:17 expenses
drwxr-xr-x 2 1001 1001 4096 Jun 13 17:19 memos
drwxr-xr-x 2 1001 1001 4096 Jun 13 17:17 tech
226 Directory send OK.

ftp> cd memos
250 Directory successfully changed.

ftp> ls
227 Entering Passive Mode (192,168,206,181,254,97).
150 Here comes the directory listing.
-rw-r----- 1 1001 1001 79915 Jun 13 17:19 memo.0514
-rw-r----- 1 1001 1001 74069 Jun 13 17:19 memo.0628
-rw-r----- 1 1001 1001 37489 Jun 13 17:19 memo.0905
-rw-r----- 1 1001 1001 85699 Jun 13 17:18 memo.0921
-rw-r----- 1 1001 1001 55181 Jun 13 17:18 memo.1102
226 Directory send OK.
```

接着，Sam 使用 `ftp get` 命令将 `memo.1102` 从服务器复制到本地系统。使用二进制模式可以确保无论该文件是二进制文件还是 ASCII 文件，他都能获得一份完整的副本。服务器确认文件已成功复制，并报告了文件大小以及复制所需的耗时。随后，Sam 将本地文件 `memo.1114` 复制到远程系统。该文件被复制到他的远程工作目录 `memos` 中。

### get 和 put

```
ftp> get memo.1102
local: memo.1102 remote: memo.1102
227 Entering Passive Mode (192,168,206,181,122,35).
150 Opening BINARY mode data connection for memo.1102 (55181 bytes).
226 Transfer complete.
55181 bytes received in 0.000392 secs (140767.86 Kbytes/sec)

ftp> put memo.1114
local: memo.1114 remote: memo.1114
227 Entering Passive Mode (192,168,206,181,71,174).
150 Ok to send data.
226 Transfer complete.
25897 bytes sent in 0.00174 secs (14857.72 Kbytes/sec)
```

现在，Sam 决定将 `plum` 上 `memo` 目录中的所有文件复制到其本地系统的一个新目录中。他执行 `ls` 命令以确保复制正确的文件，但 `ftp` 已超时。他没有退出 `ftp` 并在 shell 中再次执行 `ftp` 命令，而是给 `ftp` 发送了 `open plum` 命令以重新连接到服务器。登录后，他使用 `ftp cd` 命令将目录切换到服务器上的 `memos`。

### 超时和 open

```
ftp> ls
No control connection for command: Success
Passive mode refused.
ftp> open plum
Connected to plum (192.168.206.181).
220 (vsFTPd 3.0.2)
Name (plum:sam): sls
...
ftp> cd memos
250 Directory successfully changed.
```

### 本地 cd (lcd)

在此时，Sam 意识到他还没有创建用于存放要下载文件的新目录。执行 `ftp mkdir` 命令会在服务器上创建新目录，但 Sam 想在本地系统上创建新目录。他使用感叹号 (!) 后跟 `mkdir memos.hold` 命令来调用 shell 并在本地系统上运行 `mkdir`，从而在本地系统的工作目录中创建一个名为 `memos.hold` 的目录。（您可以使用 `lpwd` 显示本地系统上工作目录的名称。）接下来，由于 Sam 想将文件从服务器复制到本地系统的 `memos.hold` 目录，他必须更改本地系统上的工作目录。执行命令 `lcd memos.hold` 无法实现 Sam 的目标，因为感叹号会在本地系统生成一个新的 shell，而 `cd` 命令仅在新的 shell 中有效，而不是在运行 `ftp` 的 shell 中有效。针对这种情况，`ftp` 提供了 `lcd`（本地 `cd`）命令，该命令用于更改 `ftp` 的工作目录，并报告新的本地工作目录：

```
ftp> !mkdir memos.hold

ftp> lcd memos.hold
Local directory now /home/sam/memos.hold
```

Sam 使用 `ftp mget`（多文件获取）命令，后跟星号 (*) 通配符，将远程 `memos` 目录中的所有文件复制到本地系统的 `memos.hold` 目录。当 `ftp` 提示他第一个文件时，Sam 意识到他忘记关闭提示功能，因此他回答 n 并按下 CONTROL-C 以停止响应第二个提示时的文件复制。服务器询问他是否希望继续执行 `mget` 命令。

随后，Sam 执行 `ftp prompt` 命令，该命令切换提示动作（如果提示已开启则关闭，如果已关闭则开启）。现在，当他执行 `mget *` 命令时，`ftp` 会在不提示的情况下复制文件。获取所需的文件后，Sam 执行 `quit` 命令以关闭与服务器的连接，退出 `ftp` 并返回到本地 shell 提示符。

### mget 和 prompt

```
ftp> mget *
  mget memo.0514? n
  mget memo.0628? CONTROL-C
Continue with mget? n

ftp> prompt
Interactive mode off.

ftp> mget *
local: memo.0514  remote: memo.0514
227 Entering Passive Mode (192,168,206,181,216,120).
150 Opening BINARY mode data connection for memo.0514 (79915 bytes).
226 Transfer complete.
79915 bytes received in 0.00188 secs (42485.38 Kbytes/sec)
local: memo.0628  remote: memo.0628
227 Entering Passive Mode (192,168,206,181,24,77).
150 Opening BINARY mode data connection for memo.0628 (74069 bytes).
226 Transfer complete.
74069 bytes received in 0.0114 secs (6518.44 Kbytes/sec)
...
150 Opening BINARY mode data connection for memo.1114 (25897 bytes).
226 Transfer complete.
25897 bytes received in 0.00107 secs (24293.62 Kbytes/sec)
ftp> quit
221 Goodbye.
```

## 匿名 FTP

许多系统——最著名的是那些允许您下载免费软件的系统——允许您以匿名身份登录。支持匿名登录的大多数系统接受名称 `ftp` 作为 `anonymous` 的同义词，因为 `ftp` 拼写更简单且输入速度更快。匿名用户通常被限制在文件系统的特定部分中，该部分专门用于存放要与远程用户共享的文件。当您以匿名用户身份登录时，服务器会提示您输入密码。虽然系统接受任何密码，但按照惯例，您被要求提供您的电子邮件地址。如果您正在登录公共站点，请勿使用重要的电子邮件地址，因为该地址可能会基于此次登录收到垃圾邮件。允许匿名访问的许多系统将有趣的文件存储在 `pub` 目录中。大多数浏览器（如 Firefox）在您点击文件名时，会以匿名 FTP 站点登录并传输文件。

## 自动登录

`.netrc` 您可以存储特定于服务器的 FTP 用户名和密码信息，这样每次访问 FTP 站点时就不必手动输入。`~/.netrc` 的每一行都标识一个服务器。当您连接到 FTP 服务器时，`ftp` 会读取 `~/.netrc` 文件以确定您是否为该服务器设置了自动登录。`~/.netrc` 中行的格式为：

```
machine server login username password password
```

其中 `server` 是服务器名称，`username` 是您的用户名，`password` 是您在 `server` 上的密码。在文件的最后一行，将 `machine` 替换为 `default`，以指定未列在 `~/.netrc` 中的系统的用户名和密码。`default` 行对于登录匿名服务器非常有用。下面是一个 `~/.netrc` 文件的示例：

```
$ cat ~/.netrc
machine plum login sls password mypassword
default login anonymous password sam@example.com
```

为了保护 `.netrc` 中的账户信息，请使其仅对该主目录所在的用户可读。更多信息请参阅 `netrc` man 手册页。

## 二进制与 ASCII 传输模式

`vsftpd` FTP 服务器可以但不总是提供两种文件传输模式。二进制模式传输始终逐字节精确复制文件的映像，且从不更改换行符。请使用二进制模式传输所有二进制文件。除非需要转换换行符，否则也请使用二进制模式传输 ASCII 文件。这些描述不适用于由 Word 或 LibreOffice 等文字处理程序创建的文件，因为这些程序生成的是二进制文件。`vsftpd` 服务器可以映射 Linux 换行符为 Windows 换行符（当您上传文件时）以及 Windows 换行符为 Linux 换行符（当您下载文件时）。

要在允许此功能的 FTP 服务器上使用 ASCII 模式，请在登录后执行 `ascii` 命令（第 722 页），并将 `cr` 设置为 ON（默认值；第 723 页）。如果服务器不允许您在传输文件时更改换行符，您可以在以二进制模式传输文件之前或之后使用 `unix2dos`（第 260 页）实用程序。

安全性 为了增强安全性，默认情况下，`vsftpd` 在传输每个文件时都使用二进制模式，即使它看起来像是在使用 ASCII 模式。在服务器端，您可以通过设置 `ascii_upload_enable` 和 `ascii_download_enable` 参数来启用真正的 ASCII 模式传输。

(page 732) 设为 YES。当服务器设置为允许 ASCII 传输时，客户端通过使用 `ascii`、`binary` 或 `cr` 命令（第 722 页）来控制是否映射换行符。

## FTP 特定事项

本节介绍了使用 `ftp` 的详细信息。

## 格式

`ftp` 命令行的格式如下：
