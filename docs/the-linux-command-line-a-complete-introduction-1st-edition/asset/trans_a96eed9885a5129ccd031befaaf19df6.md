

使用 -r 选项将显示内核的网络路由表。
这显示了网络如何配置以将数据包从一个网络发送到另一个网络：

```
[me@linuxbox ~]$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
192.168.1.0     *               255.255.255.0   U         0     0          0 eth0
default         192.168.1.1     0.0.0.0         UG        0     0          0 eth0
```

在这个简单的示例中，我们看到防火墙/路由器后面局域网（LAN）上客户端机器的典型路由表。列表的第一行显示目标为 192.168.1.0。IP地址以零结尾指的是网络而不是单个主机，因此此目标表示 LAN 上的任何主机。下一个字段，Gateway，是用于从当前主机到目标网络的网关（路由器）的名称或 IP 地址。此字段中的星号表示不需要网关。

最后一行包含目标 default。这表示发往表中未另行列出的网络的任何流量。在我们的示例中，我们看到网关被定义为地址为 192.168.1.1 的路由器，它 presumably 知道如何处理目标流量。

netstat 程序有许多选项，我们只查看了其中几个。查看 netstat 手册页以获取完整列表。

## 在网络上传输文件

如果我们不知道如何跨网络移动文件，网络有什么用呢？有许多程序可以在网络上传输数据。我们现在将介绍其中两个，并在后面的章节中介绍更多。

## ftp—使用文件传输协议传输文件

ftp 是真正的“经典”程序之一，它的名字来源于其使用的协议，即文件传输协议。FTP 在互联网上被广泛用于文件下载。大多数，如果不是全部，网络浏览器都支持它，你经常会看到以协议 ftp:// 开头的 URI。

在出现网络浏览器之前，就有 ftp 程序。ftp 用于与 FTP 服务器通信，这些机器包含可以通过网络上传和下载的文件。

FTP（在其原始形式中）是不安全的，因为它以明文形式发送账户名和密码。这意味着它们未被加密，任何嗅探网络的人都可以看到它们。正因为如此，几乎所有通过互联网进行的 FTP 都是通过匿名 FTP 服务器进行的。匿名服务器允许任何人使用登录名 anonymous 和无意义的密码登录。

在下面的示例中，我们展示了使用 ftp 程序从匿名 FTP 服务器 fileserver 的 /pub/cd_images/Ubuntu-8.04 目录下载 Ubuntu ISO 映像的典型会话。

```
[me@linuxbox ~]$ ftp fileserver
Connected to fileserver.localdomain.
220 (vsFTPd 2.0.1)
Name (fileserver:me): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd pub/cd_images/Ubuntu-8.04
250 Directory successfully changed.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-rw-r-- 1 500 500 733079552 Apr 25 03:53 ubuntu-8.04-desktop-i386.iso
226 Directory send OK.
ftp> lcd Desktop
Local directory now /home/me/Desktop
ftp> get ubuntu-8.04-desktop-i386.iso
local: ubuntu-8.04-desktop-i386.iso remote: ubuntu-8.04-desktop-i386.iso
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for ubuntu-8.04-desktop-i386.iso (733079552 bytes).
226 File send OK.
733079552 bytes received in 68.56 secs (10441.5 kB/s)
ftp> bye
```

### 表 16-1：交互式 ftp 命令示例

| Command | Meaning |
|---|---|
| ftp fileserver | 调用 ftp 程序并使其连接到 FTP 服务器 fileserver。 |
| anonymous | 登录名。在登录提示后，会出现密码提示。一些服务器会接受空白密码。其他服务器需要以电子邮件地址形式输入密码。在这种情况下，尝试类似 user@example.com 的内容。 |
| cd pub/cd_images/Ubuntu-8.04 | 更改到远程系统上包含所需文件的目录。请注意，在大多数匿名 FTP 服务器上，供公众下载的文件都位于 pub 目录下的某个位置。 |
| ls | 列出远程系统上的目录。 |

