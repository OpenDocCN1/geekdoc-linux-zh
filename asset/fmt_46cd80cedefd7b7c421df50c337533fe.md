
```
[root@localhost]# cat /etc/sysconfig/network
NETWORK=yes
HOSTNAME=localhost.localdomain
[root@localhost]# -
```

在安装之前规划合适的主机名是一个良好的习惯，因为许多应用程序在安装期间会将此主机名记录在它们的配置文件中；如果你在安装后更改了主机名，可能需要修改这些文件。

虽然在指定网络上的计算机时使用主机名更易用，但 `TCP/IP` 协议无法使用它们来识别计算机。因此，你必须将主机名映射到关联 `IP` 地址，以便跨网络与其他计算机通信的应用程序能够找到主机名对应的 `IP` 地址。

将主机名映射到 `IP` 地址的最简单方法是在 `/etc/hosts` 文件中存入条目，如下所示：

```
[root@localhost]# cat /etc/hosts
# 不要删除以下行，否则各种
# 需要网络功能的程序将无法运行。
127.0.0.1 localhost localhost
3.0.0.2 ftp.sampleddomain.com fileserver
192.168.0.1 alpha
[root@localhost]# -
```

上述输出中的条目通过 `localhost.localdomain` 和 `localhost` 主名标识本地计算机 `127.0.0.1`。同样，你可以使用主机名 `ftp.sampleddomain.com` 或 `fileserver` 来引用 `IP` 地址为 `3.0.0.2` 的计算机。此外，`IP` 地址为 `192.168.0.1` 的计算机被映射到主机名 `alpha`。

你可以使用网络信息服务 (`NIS`) 在网络上的若干台 `Linux` 计算机之间共享 `/etc/hosts` 配置；`NIS` 将在本章稍后讨论。

## 第 15 章 Linux 网络

由于在 `/etc/hosts` 文件中列出互联网上所有主机的名称会非常繁琐，互联网服务提供可以在互联网上的 `DNS` 服务器中列出完全限定域名 (`FQDN`)。应用程序可以向 `DNS` 服务器请求特定 `FQDN` 关联的 `IP` 地址。要配置你的系统通过联系 `DNS` 服务器将名称解析为 `IP` 地址，只需在 `/etc/resolv.conf` 文件中指定 `DNS` 服务器的 `IP` 地址即可。该文件最多包含三个 `DNS` 服务器；如果第一个 `DNS` 服务器不可用，系统将尝试联系文件列出的第二个 `DNS` 服务器，然后是文件中列出的第三个 `DNS` 服务器。一个 `/etc/resolv.conf` 示例如下：

```
[root@localhost]# cat /etc/resolv.conf
nameserver 209.121.197.2
nameserver 192.139.188.144
nameserver 6.0.4.211
[root@localhost root]# _
```

要通过将名称解析为 `IP` 地址来测试 `DNS` 配置，你可以使用 `nslookup hostname`、`dig hostname` 或 `host hostname` 命令。

当使用特定应用程序指定主机名时，应用程序必须通过搜索本地 `/etc/hosts` 文件、`DNS` 服务器或 `NIS` 服务器将该主机名解析为相应的 `IP` 地址。应用程序用于解析主机名的顺序由 `/etc/nsswitch.conf` 文件中的 `hosts` 行决定，如下所示：

```
[root@localhost root]# grep hosts /etc/nsswitch.conf
hosts: files dns nis
[root@localhost root]# _
```

输出表明应用程序将首先使用 `/etc/hosts` 文件 (`files`) 解析主机名。如果失败，应用程序将联系 `/etc/resolv.conf` 中列出的 `DNS` 服务器 (`dns`)，或者如果配置了 `NIS` 服务器，则联系 `NIS` 服务器 (`nis`)。

在较旧的 `Linux` 计算机上，`/etc/host.conf` 文件仍然存在，用于支持旧的应用程序，并应包含与 `/etc/nsswitch.conf` 相同的名称解析顺序。一个 `/etc/host.conf` 示例允许应用程序搜索 `/etc/hosts` 文件，然后是 `DNS` 服务器 (`bind`) 和 `NIS` 服务器，输出如下所示：

```
[root@localhost]# cat /etc/host.conf
order hosts,bind,nis
[root@localhost root]# _
```

## 连接网络资源

一旦配置了网络接口，`Linux` 计算机就可以使用网络上的资源，如共享打印机、应用程序和文件。要使用网络资源，你首先需要能够连接到该资源的适当网络工具。某些网络工具易于使用，例如使用 `Web` 浏览器访问网络上 `Web` 服务器的 `Web` 页面，而其他网络工具如 `FTP` 则你在在使用之前学习特定的命令。

在本节中，我们将检查用于在系统中执行各种网络任务的最常用网络工具。

## 使用 FTP 下载文件

跨互联网传输文件最常用的方法是使用第 1 章中讨论的文件传输协议 (`FTP`)。大多数浏览器都内置了 `FTP` 客户端，允许你查看图 15-18 中的可用文件。使用 `Web` 浏览器访问网络上 `Web` 服务器的 `Web` 页面，而其他网络工具如 `FTP` 则要求你在在使用之前学习特定的命令。

远程计算机上的当前目录是 `root`。

或者，你可以按照如下格式指定计算机的主机名或 `IP` 地址。随后，你可以以 `root` 用户身份登录主目录。当前目录是 `root` 用户的主目录。要验证这一点并查看文件列表，你可以在 `ftp>` 提示符处使用以下命令：

表 15-1 常用 `FTP` 命令

| 命令 | 说明 |
| :--- | :--- |
| `help` | 显示常用命令 |
| `pwd` | 显示当前目录 |
| `dir` | 显示目录列表 |
| `cd` | 切换目录 |
| `lcd` | 切换本地目录 |
| `get` | 下载文件 |
| `ascii` | 用于文本（默认） |
| `binary` | 用于二进制文件 |
| `mget` | 下载多个文件 |
| `put` | 上传文件 |
| `close` | 关闭连接 |
| `open` | 打开连接 |
| `bye` | 退出 `FTP` 工具 |

远程计算机上的当前目录是 `root` 用户的主目录。要将 `file3` 下载到本地计算机的当前目录中，你可以使用以下命令：

```
ftp> get file3
local: file3: file3
227 Entering Passive Mode (192,168,0,1,137,37)
150 Opening BINARY mode connection for file3 (103996 bytes).
226 Transfer complete.
ftp>
```

> 如果你的连接缓慢，你可以改用 `get file3.gz` 命令：`FTP` 服务在传输前会自动使用 `gzip` 工具对 `file3` 进行压缩。

同样，将远程计算机的当前目录更改为 `/root/stuff`，并将本地当前目录中的 `file4` 副本上传到该处。

# 第 15 章 Linux 网络

在查看结果并退出 `FTP` 工具的同时，你可以在提示符 `ftp>` 处使用以下命令：

```
ftp> cd stuff
250 CWD command successful.
ftp> pwd
257 "/root/stuff" is current directory.
ftp> mput file4
mput file4? y
227 Entering Passive Mode (192,168,0,1,70,109)
150 Opening BINARY data connection for file4.
227 Transfer complete.
929 bytes sent in 0.00019 seconds (4.8e+03 Kbytes/s)
ftp> ls
227 Entering Passive Mode (192,168,0,1,235,354)
150 Opening ASCII data connection for directory listing.
total 8
-FW-r--r-- 1 root root 929 Aug 14 09:26 file4
227 Transfer complete.
ftp> bye
[root@localhost]#
```

## 使用 NFS 访问文件

不像 `FTP` 那么常用，但网络文件系统（`NFS`）是 `UNIX` 和 `Linux` 计算机之间传输文件的另一种常用方法。要使用 `NFS` 访问文件，只需将网络上已启动守护进程的远程计算机目录挂载到本地目录。只需在 `mount` 命令中指定文件系统类型、服务器名称或 `IP` 地址、远程目录和本地参数即可。例如，要使用 `NFS` 将名为 `sampledomain.com`（`IP` 地址 `192.168.0.1`）的远程计算机上的 `/var` 目录挂载到本地计算机的 `/mnt` 目录并查看结果，你可以使用以下命令：
