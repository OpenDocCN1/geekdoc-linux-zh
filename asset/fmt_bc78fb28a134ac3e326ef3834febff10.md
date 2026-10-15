
```
       ^ 
      ! !__
  WELCOME TO THE...  !  _--
      --  ! !__
     -!_-_  !  ! 
    !    !  !  ! 
    !    !  !  !  -
    !    !  !  ! 
    !    !  !  ! 
    !    !  !  !  !
    !    !  !__  !
      !  !_!  !
      !  !__  !
      CLEVAND FREE-NET
      COMMUNITY COMPUTER SYSTEM
      -------------------------
```

由 Case Western Reserve University
Office of Information Services
提供

您是：

+   1. 注册用户
2. 访客

# Linux 食南：日常使用的技巧与技术

请输入 1 或 2： 1

在 `Login:` 提示符处输入你的用户 ID（小写）。然后按照提示输入你的密码。请注意，输入密码时，密码不会显示在屏幕上。

Login:

在这个示例中，用户连接到了系统 `kanga.ins.cwru.edu`；底部的 `Login` 提示符是远程系统的提示符（如果你不确定自己正处于哪个系统，请使用 `hostname` 作为 shell 提示符；参见第 2.4 章 [运行命令]，第 22 页）。

要断开系统连接

- 要断开远程 Linux 系统连接，请输入：

```bash
$ Ctrl-d

Connection closed.

$
```

在上述示例中，第一个 shell 提示符在远程系统上，而第二个提示符在本地系统上。

### 32.1.1 挂起与其他系统的连接

你也可以通过输入转义字符临时返回本地 shell，该字符是一个在 `telnet` 到达远程系统之前解释的序列。随后你会被带回 `telnet` 命令提示符，你可以在那里挂起 `z` 命令；要返回远程系统，请将任务调回前台（参见第 3.3.3 章 [将任务放入前台]，第 42 页）。

- 要返回远程系统，请输入：

```bash
faraway-system$ Ctrl-[

telnet> z

[2]+ Stopped

telnet

$
```

- 要返回远程系统，

```bash
$ fg

faraway-system$
```

事实上，在上述两个示例中，转义字符 `Ctrl-[` 是在远程系统上输入的，该示例中的 shell 提示符为 `faraway-system$`（尽管你不必非要在 shell 提示符处输入转义字符；无论你正在运行什么程序或处于远程系统的哪个位置，都可以输入）。然后，将 `z` 命令交给 `telnet` 以挂起 `telnet` 连接。在第二个示例中，挂起的远程系统 `telnet` 连接被带回前台。

**注意：** 你应该意识到，可能（尽管并不理想）通过从上一个系统连接到下一个、再下一个……而在不断开与前一个系统连接的情况下，“嵌套”多层 `telnet` 会话。为了避免这种情况，当你准备 `telnet` 到另一个系统时，请确保知道你正在离开哪个主机；`hostname` 工具对此很有用（参见第 2.2.1 章 [登录系统]，第 18 页）。

### 32.1.2 使用加密连接另一个系统

Debian: `kerberos4th-user`
WWW: http://web.mit.edu/kerberos///
WWW: http://www.openssh.com/

在某些系统上，系统管理员可能允许你安装和使用 `kerberos`、`openssh` 或其他网络安全工具，以便以比 `telnet` 更安全的方式连接远程系统。这些工具会在连接会期间加密本地和远程系统之间传输的数据；它们现在在对安全敏感的管理员中非常流行。你应该会被要求使用其中一种，请按照管理员的说明为你的系统进行安装和配置。

**注意：** 为了使用本章讨论的任何服务和工具，你的系统必须在线或通过其他连接到网络；参见第 29 章 [通信]，第 307 页。

### 32.2 使用另一个系统传输文件

FTP（“文件传输协议”）是跨系统交换文件的一种方式。使用 `ftp` 工具通过此协议连接到另一个系统，并将要连接的系统名称或数字 IP 地址作为参数提供。连接后，系统将提示你使用用户名和密码登录（如果你在该系统上有相应的账号的话）。

许多系统设置了“匿名 FTP”连接，普通公众可以下载其中的文件公存储库；要使用此功能，请使用用户名 `anonymous` 登录，并提供你的电子邮件地址作为密码。

- 要到 ftp.leo.org 建立匿名 FTP 连接，请输入：

```bash
$ ftp.leo.org

Connected to ftp.leo.org.

220-Welcome to LED.ORG.

220-See README for more information about this archive.

220-

220-Your connection class is named: The world outside Germany

220-

220-If you don't connect from inside Munich and login anonymously,

220-your data transfers are limited to a certain bandwidth.

220-If you notice unusual behaviour, drop a note to ftp-admin@leo.org.

220 FTP server leo.org-0.9alpha ready.

Name (ftp.leo.org-m): anonymous RET

331 Guest login ok, send your email address as password.

Password: attl8$@po.cwr.edu RET
```

```
| | | | | \ |

|---|---|---|---|LEO - Link Everything Online |

|---|---|---|Munich University of Technology (TUM) |

| ////////|Department of Computer Science |
```

- 这个匿名 FTP 站点位于德国慕尼黑，欧洲。
- 它是周二 Sep ...

使用 `i` 来指定以二进制格式传输文件；通常，传输设置为文本文件。当你想要传输程序、归包、压缩文件或任何非文本文件时，请将传输类型设置为 `i`。

近年来，大多数公共系统增加了安全功能，禁止匿名用户上传到 `~/tmp` 目录以外的任何地方，或者禁止到 `~/incoming` 或 `~/pub/incoming` 目录以外的任何地方。

`mput` 命令的作用与 `put` ，但相反——可以使用通配符。默认情况下，`mput` 会对每个文件询问你是否上传该文件；要关闭此文件提示，请给出 `mput` 命令之前输入 `prompt`。该命令是一个开关——再次输入 `prompt` 即可在你的会话中重新开启文件提示。

# Linux 食南：日常使用的技巧与技术

```bash
ftp > lcd /tmp RET

Local directory now /home/james/tmp

ftp get INDEX.gz RET

local: INDEX.gz remote: INDEX.gz

Transferred 10942767 bytes

ftp>
```
