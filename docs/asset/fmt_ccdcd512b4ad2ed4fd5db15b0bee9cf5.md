
在安装前规划合适的主机名是一种良好的实践，因为许多应用程序在安装过程中会在其配置文件中记录该主机名。如果在安装后更改主机名，你可能需要修改这些文件。

虽然主机名在指定网络上的计算机时比 IP 地址更容易使用，但 `TCP/IP` 无法使用它们来标识计算机。因此，你必须将主机名映射到其关联的 IP 地址，以便通过网络联系其他计算机的应用程序能够找到特定主机名对应的合适 IP 地址。

将主机名映射到 IP 地址最简单的方法是向`/etc/hosts`文件中添加条目，如下例所示：

```
[root@server1 root]$ cat /etc/hosts
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1	server1 localhost.localdomain localhost
3.0.0.2	ftp.sampledomain.com fileserver
192.168.0.1	alpha
[root@server1 root]$ _
```

上述输出中的条目通过主机名`server1`、`localhost.localdomain`和`localhost`标识本地计算机`127.0.0.1`。同样，你可以使用主机名`ftp.sampledomain.com`或`fileserver`来引用 IP 地址为`3.0.0.2`的计算机。此外，IP 地址为`192.168.0.1`的计算机被映射到主机名`alpha`。

![](img/09bf13b782f71165e17bb3839040c96a_563_0.png)

> 你可以使用网络信息服务 (NIS) 在网络中的多台 Linux 计算机之间共享`/etc/hosts`配置文件。NIS 在第 15 章“配置网络服务和安全”中进行了讨论。

由于在互联网上的所有主机名称都列入`/etc/hosts`文件会非常繁琐，ISP 可以在互联网上的 DNS 服务器中列出 FQDN。应用程序随后可以向 DNS 服务器查询与特定 FQDN 关联的 IP 地址。要配置系统通过联系 DNS 服务器来将名称解析为 IP 地址，只需在`/etc/resolv.conf`文件中指定 DNS 服务器的 IP 地址即可。该文件最多可以包含三个 DNS 服务器；如果第一个 DNS 服务器不可用，系统将尝试联系文件列出的第二个 DNS 服务器，然后是第三个 DNS 服务器。以下输出展示了一个`/etc/resolv.conf`文件示例：

```
[root@server1 root]$ cat /etc/resolv.conf
nameserver 209.121.197.2
nameserver 192.139.188.144
nameserver 6.0.4.211
[root@server1 root]$ _
```

![](img/09bf13b782f71165e17bb3839040c96a_564_0.png)

## 注意

要通过将名称解析为 IP 地址来测试 DNS 配置，你可以在命令提示符下输入`nslookup name`、`dig name`或`host name`，其中`name`是远程主机的主机名或 FQDN。

当使用某个应用程序并指定主机名时，该应用程序必须通过搜索本地`/etc/hosts`文件、DNS 服务器或 NIS 服务器来将该主机名解析为合适的 IP 地址。应用程序解析主机名的方法由`/etc/nsswitch.conf`文件中的`hosts`行决定；该文件的一个示例如下所示：

```
[root@server1 root]# grep hosts /etc/nsswitch.conf
hosts:      files dns nis
[root@server1 root]# _
```

上述输出表明，应用程序首先使用`/etc/hosts`文件（`files`）来解析主机名。如果失败，应用程序将联系`/etc/resolv.conf`（`dns`）中列出的 DNS 服务器，随后如果配置了 NIS 服务器，则联系 NIS 服务器（`nis`）。

在较旧的 Linux 编译器上，使用`/etc/host.conf`文件代替`/etc/nsswitch.conf`；`/etc/host.conf`文件至今仍存在，以支持较旧的应用程序，并且应包含与`/etc/nsswitch.conf`相同的名称解析顺序。以下输出展示了一个`/etc/host.conf`文件示例，它指示应用程序先搜索`/etc/hosts`文件，然后搜索 DNS 服务器（`bind`）和 NIS 服务器：

```
[root@server1 root]# cat /etc/host.conf
order hosts,bind,nis
[root@server1 root]# _
```

### 连接网络资源

在配置了网络接口后，Linux 计算机可以使用网络上的资源，例如共享打印机、应用程序和文件。要使用网络资源，你首先必须拥有能够连接到该资源的合适网络工具。一些网络工具易于使用，例如使用 Web 浏览器访问网络上的 Web 服务器上的 Web 页面，而其他网络工具如 FTP 要求你在使用前学习特定命令。

本节介绍了用于在系统上执行各种网络任务的最常见的网络工具。

#### 使用 FTP 下载文件

跨互联网传输文件最常用的方法是使用文件传输协议 (FTP)，如第 1 章“Linux 简介”中所述。大多数 Web 浏览器内置了 FTP 工具，允许你输入形如`ftp://ftp.sampledomain.com`的 FQDN，并使用 Web 浏览器屏幕查看远程计算机上公开可用的文件和目录，如 14-12 图所示。

![](img/09bf13b782f71165e17bb3839040c96a_565_0.png)

> 你也可以使用`ftp://IP_address`连接公共 FTP 服务器，而无需进行名称解析。

![](img/09bf13b782f71165e17bb3839040c96a_565_1.png)

**图 14-12** *使用 Web 浏览器 FTP 客户端*

使用鼠标点击 14-12 图中显示的文件，会出现一个对话框，允许你将文件保存到本地文件系统的适当位置。

或者，你可以将运行 FTP 服务的计算机的主机名或 IP 地址作为参数指定给`ftp utility`，以打开一个允许向该计算机传输文件或从该计算机传输文件的连接。随后，你可以以该计算机上的有效用户身份登录，并被放置在该计算机的主目录中，或者以用户`anonymous`登录，并

放置在公共可访问的 FTP 目录中（通常是`/var/ftp`）。登录后，您会收到接受 FTP 命令的`ftp>`提示符；表 14-2 展示了常见的 FTP 命令列表。

## 注意

大多数 FTP 服务器要求用户在以匿名用户身份登录时输入密码；此密码通常是您的电子邮件地址。

### 表 14-2 常见的 FTP 命令

| **命令** | **描述** |
| :--- | :--- |
| `help` | 显示命令列表 |
| `pwd` | 显示远程计算机上的当前目录 |
| `dir, ls` | 显示远程计算机上的目录列表 |
| `cd directory` | 将远程计算机上的当前目录更改为`directory` |
| `lcd directory` | 将本地计算机上的当前目录更改为`directory` |
| `get filename` | 将`filename`下载到本地计算机的当前目录 |
| `ascii` | 指定文本文件下载（默认） |
| `binary` | 指定二进制文件下载 |
| `mget filename` | 将`filename`下载到本地计算机的当前目录；它还允许使用通配符元字符来指定`filename` |
| `put filename` | 将`filename`从本地计算机的当前目录上传到远程计算机的当前目录 |
| `mput filename` | 将`filename`从本地计算机的当前目录上传到远程计算机的当前目录；它还允许使用通配符元字符来指定`filename` |
| `!` | 在本地计算机上运行`shell` |
| `close` | 关闭与远程计算机的 FTP 连接 |
| `open hostname or IP` | 打开到指定`hostname or IP`地址的 FTP 连接 |
| `bye, quit` | 退出 FTP 实用程序 |

在 FTP 会话期间显示的确切输出因 FTP 服务器上使用的 FTP 软件版本不同而略有差异。以下输出示例是使用`ftp`实用程序以`root`用户身份连接到名为`ftp.sampledomain.com`的 FTP 服务器：
