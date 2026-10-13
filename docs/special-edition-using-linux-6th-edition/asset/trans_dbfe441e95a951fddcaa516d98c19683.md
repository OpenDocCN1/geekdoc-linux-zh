
我有一个新的打印服务器设备，在设置过程中需要获取IP地址。如何在Linux下设置这个打印服务器？

打印服务器在启动时会通过ARP查找其地址。请执行以下操作：

1. 请确保您有DNS条目，或者在`/etc/hosts`文件中为打印服务器添加一个条目。在此示例中，打印服务器将被命名为`rps1.fish.net`。
2. 在打印服务器本身上查找硬件地址（也称为MAC地址）。这将是六个十六进制数字，可以用空格或冒号分隔。示例可能如下所示：

   `00:00:C0:7B:C0:00`

3. 使用以下命令将打印服务器的IP/主机名映射发送给它：

   `arp -s rps1.fish.net 00:00:c0:7b:c0:d0 temp`

此命令告诉您的系统与打印服务器的以太网卡通信，并向其（在其MAC地址为`00:00:c0:7b:c0:d0`——您的地址会不同）发送与`rps1.fish.net`对应的IP地址。现在您应该能够telnet到打印服务器，根据打印服务器附带的说明对其进行编程。如果打印服务器已关机，您可能需要重复执行arp命令。

## 第32章：文件传输协议（FTP）

### 本章内容

- FTP概述 604
- FTP客户端 605
- 使用FTP会话下载文件 609
- 使用FTP提供文件服务 612
- 故障排除 615

### FTP概述

文件传输协议（FTP）使用起来非常简单，但在促进两个系统之间传输文件或数据方面却相当强大。尽管在FTP之后设计和开发了许多网络协议和文件共享系统，它仍然是远程传输文件最流行的方法。存在多种FTP服务器。一些发行版使用了可能是最广泛使用的FTP版本wu-ftp，它由圣路易斯华盛顿大学开发（详情参见 www.wu-ftpd.org）。Caldera和Red Hat默认使用它。Debian也提供此版本。其他FTP服务器包括netkit FTP服务器和ProFTPD。

FTP提供了在两个系统之间传输任何类型文件的能力。它的设计（参见RFC 959）使得两个系统不必相同。换句话说，任何支持TCP/IP并提供FTP服务的操作系统都可以交换文件。其中一个系统充当服务器，另一个充当客户端。数据的格式，无论是文本文件、数据库文件还是二进制程序，都无关紧要。

FTP服务基于传输控制协议/网际协议（TCP/IP）标准。FTP使用两个完全独立的TCP会话来完成文件传输。一个会话通常称为控制连接或协议解释器（PI）会话，另一个称为数据连接或数据传输过程（DTP）。图32.1描绘了FTP会话的基本组件。

**图32.1**  
协议解释器会话预定义在端口21上进行，数据传输过程发生在端口20。这些端口在`/etc/services`文件中定义。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_623_0.png)

只要底层TCP/IP网络就位并且FTP服务已配置，就可以在两个主机之间建立FTP会话。FTP客户端通过连接到FTP服务器来发起FTP会话。每当客户端发出FTP请求时，服务器组件必须已配置并处于活动状态。默认情况下，大多数Linux发行版（包括随本书附带的发行版）在安装FTP服务器软件包时会启用FTP服务器。

> **警告：** 如果您的FTP服务器处于活动状态，并且您的机器对互联网上的任何人开放，请注意默认情况下所有用户都可以访问FTP服务器，除非进行明确的更改以禁用访问。

### FTP客户端

Linux发行版附带标准的命令行FTP客户端。它不是最华丽的工具，但能完成任务。Linux还带有许多其他FTP客户端，包括内置在Netscape Web浏览器中的FTP客户端功能，以及几个图形化的拖放客户端。这些FTP客户端可能更易于使用，并提供更好的用户界面；然而，理解命令行客户端不仅能让您更好地理解FTP服务的工作原理，还能提供一些附加功能，例如无人值守或批处理模式传输。

使用`ftp`作为客户端执行文件传输是一项简单的任务。它基本上包括以下两个步骤：

1. 建立到FTP服务器的连接。
2. 指定要放置在服务器上或从服务器下载的文件。

下面仔细看看每个步骤。首先，为了建立到FTP服务器的连接，您必须提供服务器名称。许多FTP站点配置了机器名称，使名称的第一部分设置为`ftp`。例如，Caldera Systems的FTP服务器被恰当地命名为`ftp.calderasystems.com`。可以按如下方式建立到此FTP服务器的FTP会话：

```text
# ftp ftp.calderasystems.com
Connected to ftp.calderasystems.com.
220 locust4.calderasystems.com FTP server (Version wu-2.5.0(1) Tue Feb 22 08:21:59 MST 2000) ready.
ftp> quit
221 Goodbye.
```

建立连接后，您必须向FTP服务器进行身份验证。可以通过两种方式之一进行：作为普通用户帐户或作为匿名用户。除非您在所访问的FTP服务器上拥有个人登录帐户，否则您必须作为匿名用户进行身份验证。

向FTP服务器进行身份验证的方式是提供用户名和密码，或者使用用户名anonymous（名称ftp也可以）并将您的电子邮件地址作为密码。您可能已经猜到，以匿名用户身份连接到FTP服务器时，可以输入任何您想要的密码。但是，以这种方式连接时，提供您的电子邮件地址是常见的礼貌做法，因为这使FTP服务器的系统管理员可以在需要时与您联系。完成与FTP服务器的连接如下：

```text
$ ftp ftp.calderasystems.com
Connected to ftp.calderasystems.com.
220 locust4.calderasystems.com FTP server (Version wu-2.5.0(1) Tue Feb 22 08:21:59 MST 2000) ready.
331 Guest login ok, send your complete e-mail address as password.
230-
230-        Welcome to the Caldera Systems FTP site!
230-                ftp.calderasystems.com
230-
230-        "Extend Your Systems to the World!"
230-
230-This site is provided as a public service by Caldera Systems, Inc. This
230-server is located in Orem, Utah, USA; use in violation of any applicable
230-laws strictly prohibited.
230-
230-For comments on this site, please contact <ftp-master@calderasystems.com>.
230-==========================================================================
230-** All file transfers are logged.  If you object to this, logout now. **
230-==========================================================================
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

当收到 ftp> 提示符时，连接即完成。此时可以发起文件传输。这种交互式方法还提供了在FTP会话期间执行其他几项任务的能力。可以通过在 ftp> 提示符下输入 help（问号显示相同的列表）来显示FTP客户端会话中可用的命令，如下所示：

```text
ftp> help

!              debug           mdir            sendport        site
$              dir             mget            put             size
account        disconnect      mkdir           pwd             status
append         exit            mls             quit            struct
ascii          form            mode            quote           system
bell           get             modtime         recv            sunique
binary         glob            mput            reget           tenex
bye            hash            newer           rstatus         tick
case           help            nmap            rhelp           trace
cd             idle            nlist           rename          type
cdup           image           ntrans           reset           user
chmod          lcd             open            restart         umask
close          ls              prompt          rmdir           verbose
cr             macdef          passive         runique          ?
delete         mdelete         proxy           send
```

表32.1中列出了每个命令的简要说明。
