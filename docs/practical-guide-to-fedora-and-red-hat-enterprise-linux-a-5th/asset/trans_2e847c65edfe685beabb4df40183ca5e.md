
因为位于 NAT 后面的客户端（第 820 页）可以连接到被动服务器，并且编程实现可扩展的被动服务器更为简单。
控制 vsftpd 服务器允许的连接类型的参数在“连接参数”（第 664 页）中进行了讨论。

## 更多信息

- 在 **ftp>** 提示符下输入本地类型 **help** 或 **?** 以显示命令列表。在 **?** 后加上一个 **SPACE** 和一个 **ftp** 命令以显示该命令的信息。
- 文件：/usr/share/doc/vsftpd*
- 手册页：ftp, netrc, vsftpd.conf
- Web **vsftpd** 主页：vsftpd.beasts.org
- HOWTO *FTP 迷你 HOWTO*

## FTP 客户端

- **ftp** Fedora/RHEL 提供多个 FTP 客户端，包括 **ftp**（较早版本的 BSD **ftp** 工具）。本节讨论 **ftp**，因为大多数其他 FTP 客户端提供了 **ftp** 命令的超集。
- **sftp** **sftp** 是 OpenSSH 套件的一部分，是 **ftp** 的安全替代方案。有关更多信息，请参见第 631 页。
- **gftp** **gftp** 工具（**gftp** 软件包）是一个图形客户端，可与 FTP、SSH 和 HTTP 服务器配合使用。该客户端具有许多有用功能，包括恢复中断的文件传输能力。有关更多信息，请参见 **gftp** 手册页。
- **ncftp** **ncftp** 工具（**ncftp** 软件包）是一个文本客户端，提供比 **ftp** 更多的功能，包括文件名补全和命令行编辑。有关详情，请参见 **ncftp** 手册页。

### 先决条件

**ftp** 和 **sftp** 工具已安装在大多数 Fedora/RHEL 系统上。您可以通过将这两个工具的名称作为命令输入来检查它们是否存在：

```
$ ftp
ftp> quit

$ sftp
usage: sftp [-iXv] [-B buffer_size] [-b batchfile] [-F ssh_config]
      [-o ssh_option] [-P ftp_server_path] [-R num_requests]
      [-S program] [-s subsystem | sftp_server] host
      sftp [[user@]host[:file [file]]]
      sftp [[user@]host[:dir[/]]]
      sftp -b batchfile [user@]host
```

如果需要，请安装 **ftp** 或 **openssh-clients**（包含 **sftp**）软件包。

## 快速入门：使用 ftp 下载文件

本节快速入门分为两部分：基本命令的描述以及展示用户如何使用 ftp 的教程会话。

### 基本命令

输入命令

```
$ ftp hostname
```

其中 *hostname* 是您想要连接的 FTP 服务器的名称。如果您在服务器上有账户，请使用您的用户名和密码登录。如果是公共系统，请作为用户 *anonymous*（或 *ftp*）登录，并将您的电子邮件地址作为密码。在服务器上，像使用 shell 中的对应实用程序一样使用 *ls* 和 *cd* ftp 命令。命令 *get* *file* 从服务器复制 *file* 到本地系统，*put* *file* 从本地系统复制 *file* 到服务器，*status* 显示关于 FTP 连接的信息，而 *help* 显示命令列表。

上述说明（除 *status* 外）也适用于 *sftp* 和 *ncftp*。

### 教程会话

以下是两个 ftp 会话，其中 Alex 在与名为 *bravo* 的 vsftpd 服务器之间传输文件。当 Alex 输入命令 *ftp* *bravo* 时，本地 ftp 客户端连接到服务器，服务器会要求输入用户名和密码。由于他在本地系统上以 *alex* 的身份登录，ftp 建议 Alex 在 *bravo* 上以 *alex* 的身份登录。要以 *alex* 的身份登录，他只需按 RETURN 键即可。然而，由于他在 *bravo* 上的用户名是 *watson*，因此他在 `Name (bravo:alex):` 提示符后输入 *watson*。Alex 在 `Password:` 提示符后输入他的正常系统密码，vsftpd 服务器向他致意并告知他正在使用二进制模式传输文件。在 ftp 的二进制模式下，Alex 可以传输 ASCII 文件和二进制文件（第 650 页）。

![](img/f28adb66a7398a382f0505e0ba74a872_686_0.png)

```
$ ftp bravo
Connected to bravo.
220 (vsFTPD 2.2.0)
530 Please login with USER and PASS.
530 Please login with USER and PASS.
KERBEROS_V4 rejected as an authentication type
Name (bravo:alex): watson
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

登录后，Alex 使用 ftp 的 *ls* 命令查看其远程工作目录（即他在 *bravo* 上的主目录）中的内容。然后他 *cd* 到 *memos* 目录并显示其中的文件。

![](img/f28adb66a7398a382f0505e0ba74a872_686_1.png)

```
ftp> ls
227 Entering Passive Mode (192,168,0,6,79,105)
150 Here comes the directory listing.
drwxr-xr-x    2 alex  alex    500 Oct 10 23:52 expenses
drwxr-xr-x    2 500     500   4096 Oct 10 23:59 memos
drwxrwxr-x   22 500     500   4096 Oct 10 23:32 tech
226 Directory send OK.

ftp> cd memos
250 Directory successfully changed.

ftp> ls
227 Entering Passive Mode (192,168,0,6,114,210)
150 Here comes the directory listing.
-rw-r--r--    1 500     500   4770 Oct 10 23:58 memo.0514
-rw-r--r--    1 500     500   7134 Oct 10 23:58 memo.0628
-rw-r--r--    1 500     500   9453 Oct 10 23:58 memo.0995
-rw-r--r--    1 500     500   3466 Oct 10 23:59 memo.0921
-rw-r--r--    1 500     500   1945 Oct 10 23:59 memo.1102
226 Directory send OK.
```

接下来，Alex 使用 ftp 的 *get* 命令从服务器将 *memo.1102* 复制到本地系统。二进制模式确保无论该文件是二进制还是 ASCII，他都能获得该文件的良好副本。服务器确认该文件已成功复制，并报告文件大小及复制所需时间。然后，Alex 将本地文件 *memo.1114* 复制到远程系统。该文件被复制到他的远程工作目录 *memos* 中。

```
get and put

ftp> get memo.1102
local: memo.1102 remote: memo.1102
227 Entering Passive Mode (192,168,0,6,194,214)
150 Opening BINARY mode data connection for memo.1102 (1945 bytes).
226 File send OK.
1945 bytes received in 7.1e-05 secs (2.7e+04 Kbytes/sec)

ftp> put memo.1114
local: memo.1114 remote: memo.1114
227 Entering Passive Mode (192,168,0,6,174,97)
150 Ok to send data.
226 File receive OK.
1945 bytes sent in 2.8e-05 secs (6.8e+04 Kbytes/sec)
```

现在，Alex 决定他想将 *bravo* 上 *memo* 目录中的所有文件复制到本地系统上的一个新目录中。他输入 *ls* 命令以确保复制正确的文件，但 ftp 已超时。他没有退出 ftp 并从 shell 输入另一个 ftp 命令，而是给 ftp 输入一个 *open* *bravo* 命令以重新连接到服务器。登录后，他使用 ftp 的 *cd* 命令将服务器上的目录更改为 *memos*。

```
Timeout and open

ftp> ls
No control connection for command: Bad file descriptor
Passive mode refused.  Turning off passive mode.
No control connection for command: Bad file descriptor
ftp> open bravo
Connected to bravo (192.168.0.6).
220 (vsFTpd 2.2.0)
...
ftp> cd memos
250 Directory successfully changed.
```

**本地 cd (lcd)** 此时，Alex 意识到他还没有创建一个新的目录来存放他想要下载的文件。输入 ftp 的 *mkdir* 命令会在服务器上创建新目录，但 Alex 需要的是在本地系统上的新目录。他使用感叹号 (!) 后跟一个 **mkdir memos.hold** 命令来调用 shell 并在本地系统上运行 **mkdir**，从而在本地系统的工作目录中创建一个名为 **memos.hold** 的目录。（您可以使用 `pwd` 显示本地系统上工作目录的名称。）接下来，由于 Alex 想要将文件从服务器复制到本地系统上的 **memos.hold** 目录，他必须更改本地系统上的工作目录。输入命令 `!cd memos.hold` 无法实现 Alex 的目标，因为感叹号会在本地系统上生成一个新的 shell，而 cd 命令仅在新的 shell 中有效，该 shell 并不是 ftp 运行所在的那个 shell。针对这种情况，ftp 提供了 *lcd*（local cd）命令，它会更改 ftp 的工作目录并报告新的本地工作目录：

```
ftpp> !mkdir memos.hold
ftpp> lcd memos.hold
Local directory now /home/alex/memos.hold
```

Alex 使用 ftp 的 *mget*（multiple get）命令，后跟星号 (\*) 通配符，将远程 **memos** 目录中的所有文件复制到本地系统上的 **memos.hold** 目录。当 ftp 提示第一个文件时，Alex 意识到他忘记关闭提示，因此他输入 *n* 并按下 CONTROL-C 以停止在第二个提示处复制文件。服务器检查他是否想要继续执行 *mget* 命令。

接下来，Alex 输入 **ftp prompt** 命令，该命令切换提示操作（如果已开启则关闭，如果已关闭则开启）。现在当他输入 **mget \*** 命令时，ftp 会复制所有文件而不进行提示。获取所需文件后，Alex 输入 **quit** 命令以关闭与服务器的连接，退出 ftp 并返回本地 shell 提示符。

```
mget and prompt
ftpp> mget
    mget memo.0514? n
    mget memo.0628? C
    Continue with mget? n

ftpp> prompt
Interactive mode off.
ftpp> mget
    Local: memo.0514  Remote: memo.0514
    227 Entering Passive Mode (192,168,0,6,53,55)
    150 Opening BINARY mode data connection for memo.0514 (4770 bytes).
    226 File send OK.
    4770 bytes received in 8.8e-05 secs (5.3e+04 Kbytes/sec)
    Local: memo.0628  Remote: memo.0628
    227 Entering Passive Mode (192,168,0,6,65,102)
    150 Opening BINARY mode data connection for memo.0628 (7134 bytes).
    226 File send OK.
```

