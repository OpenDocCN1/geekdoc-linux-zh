
编辑 `smbwrapper.in` (`vi smbwrapper/smsh.in`) 并修改行：

```bash
SMBW_LIBDIR=$builddir
```

改为：

```bash
SMBW_LIBDIR=$SMBW_LIBDIR/bin
```

这将 Samba 的 "lib" 目录重定位到 "/usr/bin" 目录。

### 第二步

编辑 `Makefile.in` (`vi Makefile.in`) 并修改行：

```bash
SBINDIR = $bindir
```

改为：

```bash
SBINDIR = $bindir
```

```bash
VARDIR = $localdir
```

这将指定 Samba 二进制文件的 "bin" 目录位于 "/usr/sbin" 目录，且 Samba 的 "var" 目录位于 "/var/samba"。

#### 第三步

编辑 `convert_smpasswd` (`vi script/convert_smpasswd`) 并修改行：

```bash
awk 'FS=":"
```

改为：

```bash
awk 'FS=":"
```

这将指定 smpasswd 使用 GNU Linux 版本的 awk 而不是贝尔实验室版本的 awk。

#### 第四步

编辑 `smount.c` 文件 (`vi client/smount.c`) 并修改行：

```c
static void close_our_files(int client_fd)
```

```c
{
int i;
for (i = 0; i < 256; i++) {
if (i == client_fd) continue;
close(i);
}
```

改为：

```c
static void close_our_files(int client_fd)
```

```c
{
struct rlimit limits;
int i;
getrlimit(RLIMIT_NOFILE,&limits);
for (i = 0; i < limits.rlim_max; i++) {
if (i == client_fd) continue;
close(i);
}
```

此步骤使 `smount.c` 文件兼容 RedHat 的 `glibc 2.1`。

## 编译并优化

### 第一步

在终端上输入以下命令：

```bash
CC="gcc"
./configure
--prefix=/usr
--libdir=/etc
--withlockdir=/var/lock/samba
--withprivdir=/etc
--withswadir=/usr/share/swat
--with-mmap
--without-book
```

注意：`--with-mmap` 在某些机器上可以提升性能，而在另一些机器上没有任何影响，在某些情况下可能会降低性能。

这告诉 Samba 为此特定硬件进行设置：

- 包含 PAM 密码支持以提高安全性。
- 包含实验性的 MMAP 支持以提高 Samba 性能。
- 不安装随 Samba 分发的帮助文档。

### 第二步

现在我们在 Linux 服务器上安装 Samba。

```bash
[root@deep source]# make install
[root@deep source]# make install
[root@deep source]# rm -tm 755 script/mksmbasswd.swat /usr/bin/
[root@deep source]# rm -rf /usr/share/swat/ (如果你和我一样，不喜欢通过 HTML 配置 Samba)。
[root@deep source]# rm -rf /usr/sbin/swat
[root@deep source]# rm -rf /var/lock/samba
[root@deep source]# mkdir -p /var/spool/samba (如果您打算使用打印机共享)。
[root@deep source]# chmod 777 /var/spool/samba (如果您打算使用打印机共享)。
```

`install` 命令将在 `usr/bin` 目录下安装 `mksmbasswd.swat`。此脚本用于设置 Samba 用户通过 `smbsasswd` 文件连接到我们的服务器。请参阅文档后半部分关于如何设置和使用 Samba 密码的内容。

`rm` 命令将删除 `/usr/share/swat/` 目录及其下的所有文件，还将从 `/usr/sbin` 删除 `swat` 二进制程序。SWAT 程序是一个基于 Web 的配置工具，允许您通过 Web 界面配置 Samba 的 `smb.conf` 文件。当然，为了使用 SWAT 工具，您需要运行 Web 服务器（例如 Apache）。SWAT 工具可能会导致服务器安全漏洞，因此我建议不要使用它。

## 工作清理

`rm` 命令将删除我们用于编译和安装 Samba 的所有源码。它还会删除 `var/tmp` 目录下的 Samba 压缩包。

## 配置

不同服务的配置文件非常具体，取决于您的需求和网络架构。有人可能安装 Samba 服务器但只有一个客户端连接，而另一个人可能有 1000 个连接。

本书中描述的所有软件都有特定的目录和子目录，包含在一个名为 `floppy.tgz` 的压缩包中，其中包含特定程序的文件。如果您获取了压缩包文件，就不需要手动复制或复制粘贴下面的不同配置文件来创建您的配置文件。无论您决定手动复制，还是从压缩包获取为了您的方便而制作的文件，修改并根据您的需求进行调整，并将与 Samba 软件相关的文件放在服务器的相应位置将是您的责任，如下所示。下载服务器配置压缩包位于以下互联网地址：http://www.popen.com/books/floppy.tgz

+ 运行 Samba 服务器需要以下文件，并且必须将它们创建或复制到相应的目录中。

## 服务软件（文件共享网络服务） | 第 2 章

- 复制 `/etc/` 目录下的 `smb.conf` 和 `imhosts` 文件。
- 复制 `/etc/rc.d/init.d/` 目录下的 `smb` 脚本文件。
- 复制 `/etc/logrotate.d/` 目录下的 `samba` 文件。
- 复制 `/etc/pam.d/` 目录下的 `samba` 文件。

你可以从我们的 `floppy.tgz` 压缩包中获得列出的配置文件。请从解压后的 `floppy.tgz` 文件中适当的位置，或直接从此处复制粘贴到相关文件中。

## `/etc/smb.conf` 文件的配置

`/etc/smb.conf` 文件是 Samba 服务器的主配置文件，在其中你可以指定想要从 Windows 机器访问的目录、授权的 IP 地址等。该文件在 `[global]` 行下的前几行包含全局配置指令，这些指令适用于所有共享（除非在特定的共享上被覆盖），随后是不同的配置段（sections）。存在许多选项，阅读 Samba 随附的文档以获取有关不同设置和参数的更多信息非常重要。

以下示例是一个带有加密密码的 Samba 最小工作配置。此外，需要注意的是，我们在 Samba 配置中仅对与安全和优化相关的参数进行了注释，其余所有参数留给你自己研究。

在我们的示例中，我们只创建了一个目录 `[/tmp]`，并且只允许 C 类机器地址范围连接到 Samba 服务器。此外，此服务器上没有使用 Samba 和 Windows 之间的打印共享功能。

编辑 `smb.conf` 文件 (`vi /etc/smb.conf`) 并添加/更改以下参数：

```
[global]
workgroup = OPENNA
server string = R&D of Open Network Architecture Samba Server
encrypt passwords = user
security = user
smb password file = /etc/smbpasswd
log file = /var/log/samba log %m
socket options = IPTOS_LOWDELAY TCP_NODELAY
domain master = Yes
local master = Yes
preferred mask = Yes
os level = 65
dns proxy = No
name resolver order = hosts host
interfaces only = True eth0 192.168.1.1
hosts deny = 192.168.1.4 127.0.0.1
hosts allow = ALL
debug level = 1
create mask = 0644
directory mask = 0755
level2 oplocks = True
read raw = no
write cache size = 262144
```
