
`mget` 检索多个上传文件或完整文件名。（如果使用本地登录账户登录，而非匿名登录）

`put` 从你的机器上传一个文件到目标主机

`mput` 向你的目标远程主机上传多个文件

`pwd` 打印远程主机上的工作目录

`quit` 结束 FTP 会话

本地命令（在你的主机上处理）

`ls` 列出你主机上的文件（当前目录）

`lcd` 更改用于上传/下载的本地主机目录

`pwd` 打印本地主机的工作目录

=======================================================================

## 408 第 8 章：网络客户端服务

### 系统安装期间的

如果你使用了“服务器安装”模式，你应该已经拥有 FTP 服务了。如果你使用了“工作站”选项，你可能没有 FTP 服务。如果你使用了“自定义”选项，你必须手动选择 FTP 包，该包默认是不选中的。

你可以通过 `rpm all` 命令的输出使用“ftp”或“anon”字符串来检查已安装的软件包，如图 10 所示。

如果尚未安装，你可以安装 `anonftp` 和 `wu-ftp` 软件包。你需要挂载光驱器并访问 `/RedHat/RPMS` 目录，如图 11 所示。

#### 图 10

检查是否安装了 FTP（参见 446_0.png）

#### 图 11

安装 FTP 和 WU_FTP 软件包

```
[root@linux6 /root]# mount /dev/cdrom

[root@linux6 /root]# cd /cdrom/RPMS/

[root@linux6 RPMS]# rpm -iv anontftp-2.8-1386.rpm

anontftp-2.8...

[root@linux6 RPMS]# rpm -iv wu-ftpd-2.4.2vr17-3.1386.rpm

wu-ftpd-2.4.2vr17-3...

[root@linux6 RPMS]# umount /dev/cdrom
```

### 配置匿名 FTP 服务器

FTP 软件包的基础安装创建了一个允许匿名访问的 FTP 服务。你可以从网络上的任何主机测试你的安装情况。

匿名 FTP 服务使用 `/home/ftp/` 目录作为唯一的可访问树。在配置此匿名服务的最后，你应该对树的内容进行自定义。例如，你可以将一些 RPM 包放在 `pub` 目录中，供所有用户下载到他们的 Linux 主机，如图 8-12 所示。默认安装不会向 `pub` 目录添加文件。

### 测试你的 FTP 服务

最后一步是测试 FTP 服务的匿名登录。在任何命令行中，你都可以使用应用程序连接到任何主机，包括你自己的主机。只要目标主机运行着 FTP 服务，连接到哪个主机并不重要。Windows 9.x 和 NT 工作站默认没有 FTP 服务，只有 FTP 客户端应用程序。NT 服务器拥有 FTP 服务，但默认不安装。

# 410 第 8 章：网络客户端服务

## 图 8-12
`/home/ftp` 包含 RPM 包的列表示例

```
[root@linux ftp#] ls -R

binetclubpub -

bin:

compresspiogziplsshtartzac

etc:

groupld.so.cachepasswd

lib:

ld-2.1.1.solic-2.1.1.libnsl-2.1.1.libnss_files-2.1.1.so

l-linux.so.2libbc.so.61libns.so.libnss_files.so.2

pub:

206.195.1.hosts vga_cardgames-1.3.1-7.1386.rpm

bd-games-1.3-8.1386.rpmvga_gamespack-1.3-7.1386.rpm

x3-3.lib6.rpm

[root@linux ftp]#
```

与任何网络连接一样，FTP 客户端都需要一个有效的地址来将名称解析为 IP 地址。如果你使用“名称”，系统必须能够简单地查找 `/etc/hosts` 文件。每台机器在该文件中都至少有一个名为 `localhost` 的项，指向本地机器。在不知道主机名或其 IP 地址的情况下，你可以使用名称 "`localhost`" 测试连接。

请注意，在图 8-13 中，登录名为 `anonymous`（匿名），当密码为 `root@localhost` 时，系统会报错，尽管这是建议的基于电子邮件的密码。事实上，`root@anydomain.anygroup` 被接受，而不是建议的电子邮件地址。

### 超守护进程配置 `/etc/inetd`

FTP 服务守护进程实际上是由 `inetd` 超守护进程启动的。`inet` 守护进程通常列出除 HTTP 以外的所有配置协议。每个要监听的服务协议都指定在 `/etc/inetd.conf` 中。每当接收到用于该服务的的数据包时，`inet` (`INET`) 进程就会启动特定的服务。

图 8-14 显示了 `/etc/inetd.conf` 文件的截断视图，包含前几行，以及 FTP 和 telnet 控制行。你通常不需要更改此文件中的任何内容。

#### 图 8-13
测试 匿名登录 FTP

```
****************************************************************

root@linux6 RMEI#ftplocalhost

Connected to localhost.

220 linux.example.com FTP server (Version 2.4.2-09:17(1) Mon Apr 09 09:21:53 EDT 1999) ready.

330 Name: anonymous

331 Guest login ok, send your email address as password.

Password:(do not use 'root@localhost')

230-The response 'root@localhost' is not valid

230-User please send your email address as your password

230-example: root@localhost

230 Guest login ok, access restrictions apply.

Remote system is UNIX.

Using binary mode to transfer files.

tftp> l m

total 6

drwxr-xr-x 6 root root 1024 Sep 24 07:08

drwxr-xr-x 6 root root 1024 Sep 24 07:08

-xr-xr--x 2 root root 1024 Sep 24 07:08 bin

-xr-xr--x 2 root root 1024 Sep 24 07:08 etcc

drwxr-xr-x 2 root root 1024 Sep 24 07:08 lib

drwxr-xr-x 6 root ftp 1024 Mar 21 1999 pub

226 Transfer complete.

tftp> l pub

200 HORT command successful.

150 Opening ASCII mode data connection for /bin/lftp

drwxr-xr-x 6 root root 1024 Sep 24 17:06

drwxr-xr-x 6 root root 1024 Sep 24 17:04 206.195.1.hosts

r-xr-r-- 1 root root 49818 Sep 24 16:50 sed-games-1.1.8.1386.rmp

r-xr-r-- 1 root ftp 27856 Sep 24 16:56 vga_games-1.3.7.1386.rmp

r-xr-r-- 1 root ftp 21064 Sep 24 16:56 vga_games-1.3.7.1386.rmp

r-xr-r-- 1 root root 108147 Sep 24 16:50 xx-3.9.1386.rmp

224 Transfer complete.

tftp> quit

221-You have transferred 0 bytes in 0 files.

221-Total transfer for this session was 2886 bytes in 6 transfers

221-Thank you for using the FTP service on linux.example.com.

221 Goodbye.

root@linux6 RMEI#************************************
```
