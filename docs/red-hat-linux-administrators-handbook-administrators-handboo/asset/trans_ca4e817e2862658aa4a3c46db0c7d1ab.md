
多个域。wu-ftpd FTP 服务器可以至少以两种方式配置以支持虚拟 FTP 服务，两者均在此描述。由于两种方法都需要你在系统上设置 IP 地址别名，请先查看 IP 别名问题。

## 创建 IP 别名

要拥有虚拟 FTP 服务器，首先需要为每个 FTP 主机准备适当的 DNS 记录。你需要多个 IP 地址（每个 FTP 服务器主机一个）路由到你的 FTP 服务器机器。使用 IP 别名技术，你必须为所有 IP 地址创建虚拟以太网接口。例如，假设我需要在名为 ftp.nitec.com 的 FTP 服务器上创建两个虚拟 FTP 服务器（ftp.client-01.com 和 ftp.client-02.com）。同时假设我已经为每个域设置了 DNS 记录，使得以下行成立：

```
; In client-01.com DNS database
ftp.client-01.com. IN A 206.171.50.51

; In client-02.com DNS database
ftp.client-02.com. IN A 206.171.50.52

; In nitec.com DNS database
ftp.nitec.com. IN A 206.171.50.50
```

在我设置 ftp.nitec.com 机器上的 IP 别名和路由后，如果我运行

```
cat /proc/net/aliases
```

我会看到以下 IP 别名：

| 设备 | 族 | 地址 |
|---|---|---|
| eth0:0 | 2 | 206.171.50.51 |
| eth0:1 | 2 | 206.171.50.52 |

## 创建有限的虚拟 FTP 服务

此方法比另一种方法更简单，但也相当受限。虽然你将拥有虚拟 FTP 服务，但你无法像使用另一种方法那样对其进行大量自定义。如果你想要完全可定制的服务（如主 FTP 服务器），请跳到下一节“创建完整的虚拟 FTP 服务”。

要创建这种有限的虚拟 FTP 服务版本，你需要制作 anon-ftp 包创建的文件/目录结构的多个副本。只需安装 anonftp 包并为每个虚拟主机制作其副本即可。对于前面的示例，我将创建两个虚拟 FTP 站点目录 — /home/client1/ftp 和 /home/client2/ftp — 并复制 /home/ftp 文件和目录的所有内容。制作 /home/ftp 的精确副本最简单的方法之一是运行以下命令：

```
cd /home/client1/ ; cp -a /home/ftp .
cd /home/client2/ ; cp -a /home/ftp .
```

这些命令将 /home/ftp 文件/目录结构复制到虚拟站点目录中。现在，编辑 /etc/ftpaccess 文件以添加 virtual 关键字，如下所示：

```
virtual 206.171.50.51 root      /home/client1/ftp
virtual 206.171.50.51 banner
/home/client1/ftp/banner.msg
virtual 206.171.50.51 logfile /home/client1/ftp/xferlog

virtual 206.171.50.52 root      /home/client2/ftp
virtual 206.171.50.52 banner
/home/client2/ftp/banner.msg
virtual 206.171.50.52 logfile /home/client2/ftp/xferlog
```

不要忘记用你之前选择的内容替换 IP 地址和目录路径。修改每个主机的 banner.msg 文件以反映你想要显示的任何站点特定信息。此外，你的虚拟 FTP 站点不需要 pub 子目录，因此将其从每个站点中删除。

在创建上述配置后，你的虚拟 FTP 服务器即可进行测试。FTP 到每个虚拟 IP 地址，注意每个主机的横幅文件是不同的。虽然这种虚拟设置非常容易创建，但它缺乏完全自定义服务器外观和感觉的能力。例如，你不能在 /etc/ftpaccess 中使用 email 关键字指向适用于虚拟站点的不同电子邮件地址。

标准 wu-ftpd 提供的 ftpshut 命令不支持虚拟站点的关闭，因为它仅在 /etc/ftpaccess 文件中 shutdown 关键字指定的单个位置写入关闭消息文件。此外，当需要重新启动服务器时，你需要手动删除关闭消息文件。为了克服这些麻烦，你可能想从以下网站获取替换的 ftpshut/ftprestart 实用程序：http://www.landfield.com/wu-ftpd/restart。你必须自行编译和构建这些实用程序。

## 创建完整的虚拟 FTP 服务

此方法要求你修补 wu-ftpd 源代码并自行编译：

- 1. 你可以从 ftp://ftp.academ.com/pub/wu-ftpd/private/ 下载 wu-ftpd 的源代码。你还需要从 ftp://ftp.meme.com/pub/software/wu-ftpd-2.4.2/ 获取补丁文件。
- 2. 阅读随补丁 tar-ball 提供的 README 文件，并将补丁应用到你之前下载的 wu-ftpd 源代码中。根据 wu-ftpd 源包提供的说明编译并安装修补后的 wu-ftpd。将新的 FTP 服务器安装到默认位置 /usr/sbin/in.ftpd。
- 3. 新修补的 wu-ftpd 程序（in.ftpd）现在接受 -a 选项的参数。通常，-a 告诉服务器你希望它读取 /etc/ftpaccess 文件。现在，修补版本允许它指定 ftpaccess 文件的不同路径。因此，这允许新服务器查看将用于创建虚拟 FTP 站点所需的不同 ftpaccess 配置文件。
- 4. 修改 /etc/inetd.conf 文件，使 FTP 服务具有如下行：
  - 这通过 TCP wrapper（tcpd）调用 FTP 服务器。
- 5. 修改 /etc/hosts.allow 文件，使其对每个 FTP 服务器（即主服务器和所有虚拟 FTP 服务器）具有如下类似的行：

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
```

```
# For the primary server
ftp@206.171.50.50 : ALL : twist exec \
```

```
/usr/sbin/in.ftpd -l -a /etc/ftp/ftpaccess
```

```
# For the virtual FTP server
ftp@206.171.50.51 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client1.ftpaccess
```

```
# For the second virtual FTP server
ftp@206.171.50.52 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client2.ftpaccess
```

- 6. 创建 /etc/ftp 目录并将 /etc/ftpaccess 文件移入该目录。制作 /etc/ftp/ftpaccess 文件的两份副本，以便你拥有 /etc/ftp/client1.ftpaccess 和 /etc/ftp/client2.ftpaccess 文件。从用于邮件 FTP 服务器的 /etc/ftp/ftpaccess 文件中删除任何 virtual 关键字。最后，修改 client1.ftpaccess 文件，使其具有如下行：

```
virtual 206.171.50.51 root /home/client1/ftp
```

类似地，修改 client2.ftpaccess 文件，使其具有如下行：

```
virtual 206.171.50.52 root /home/client2/ftp
```

不要忘记用你自己的 IP 地址和目录路径替换。

- 7. 复制 /home/client1/ftp 和 /home/client2/ftp 目录中的 anonftp 文件。
- 8. 在创建上述配置后，使用以下命令重新启动 inetd 服务器：

```
killall -HUP inetd
```

就这样。现在你有两个虚拟 FTP 站点，可以通过各自的主机名或 IP 地址访问。

## 监控传输日志

日志对于 FTP 服务非常重要，因为你希望能够知道谁在对你的文件做什么。wu-ftpd 服务器将传输记录在 xferlog 文件中，该文件通常位于 /var/log 目录中。你可以使用前面讨论的 log 命令和 log transfers 关键字来自定义日志记录。

如果你有兴趣定期监控 xferlog，请尝试 Dumpxfer，你可以从 ftp://ftp.microimages.com/tools/dumpxfer.1.2.tar.gz 下载。

## 使用商业 FTP 服务器

wu-ftpd 服务器是免费的，并且在提供标准 FTP 服务方面提供了相当好的可配置性。然而，wu-ftpd 在高负载下的性能不足，并且没有非常干净且可定制的虚拟 FTP 服务解决方案。如果你需要高性能的 FTP 服务器并且不介意付费，请考虑 NcFTPd 包，这是一款具有以下有趣功能的商业 FTP 服务器：

- 不通过 inetd 运行，因此启动性能比 wu-ftpd 好得多。基于 inetd 的进程从未打算用于高性能。
- 内置目录列表功能，而 wu-ftpd 必须为每个目录列表请求形成一个 ls 进程。因此，NcFTPd 在处理目录列表方面更好。它甚至可以在内存中缓存目录列表，以在高容量 FTP 站点中提供更快的文件传输。
- 高度可配置的虚拟主机功能。每个虚拟主机都可以拥有自己的欢迎消息、匿名 FTP 目录树、密码认证方案、用户限制和日志文件。

通过从 http://www.ncftp.com/download/ 下载来试用此商业 FTP 服务器。NcFTPd 对具有某些顶级域（如 .edu 和 .us）的教育机构免费。

## 使用 Trivial File Transfer Protocol 服务器

你可能已经安装了 TFTP 服务器。它被称为 tftpd 服务器。它实际上不是 FTP 服务器，因为它使用 Trivial File Transfer Protocol 而不是 File Transfer Protocol。TFTP 使用 UDP over IP，这是一种不可靠的、面向数据包的传输方法。FTP 使用 TCP over IP，这是一种可靠的，
