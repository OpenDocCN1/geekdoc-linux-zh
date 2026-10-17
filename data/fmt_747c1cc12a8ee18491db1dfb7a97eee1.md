
```
ftp.redhat.com
Connected to ftp.redhat.com.
Red Hat Software Proudly Presents:
Red Hat 5.0 --
ftp://ftp.redhat.com/pub/redhat/redhat_5.0/
Red Hat Contrib --ftp.redhat.com/pub/contrib/
gonzales.redhat.com FTP server (Version 2.4.2 BETA)
Dec 12 20:41:30 EST 1997 ready.
Name (ftp.redhat.com:anonymous):
331 Guest login ok, send your email address as
Password:
230 Guest login ok, access restrictions apply.
Remote system type UNIX.
Using binary mode to transfer files.
cd /pub/redhat/updates/5.0/1386
Please read the file README.kernel last modified on Wed Dec 17 14:05:51 1997 - 109 days ago
CWD command successful.
ls
rw-r--r-- 1 root root 482029 Nov 26 11:31 kernel-2.0.32-2.1386.rpm
rw-r--r-- 1 root root 446095 Nov 26 11:31 kernel-headers
rw-r--r-- 1 root root 1229007 Nov 26 11:31 kernel-modules-2.0.32-2.1386.rpm
rw-r--r-- 1 root root 6195859 Nov 26 11:32 kernel-source-2.0.32-2.1386.rpm
Transfer complete.
binary
200 User type set to 1.
Interactive mode off.
mget kernel*
local: kernel-2.0.32-2.1386.rpm remote: kernel-2.0.32-2.1386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for kernel-2.0.32-2.1386.rpm (480229 bytes).
Transfer complete.
480229 bytes received in 240 secs (2 kbytes/sec)
local: kernel-headers-2.0.32-2.1386.rpm (446095 bytes).
Transfer complete.
446095 bytes received in 260 secs (1.7 kbytes/sec)
local: kernel-modules-2.0.32-2.1386.rpm (1229707 bytes).
Transfer complete.
1229707 bytes received in 565 secs (2.1 kbytes/sec)
local: kernel-source-2.0.32-2.1386.rpm (6195859 bytes).
Transfer complete.
6195859 bytes received in 2350 secs (2.6 kbytes/sec)
```

# 第一部分：配置你的系统

在此会话中，我下载了以下 RPM：

| RPM 文件名 |  |
|--- |--- |
| `kernel-2.0.32-2.1386.rpm` | 版本 2.0.32 的内核文件 |
| `kernel-modules-2.0.32-2.1386.rpm` | 内核 2.0.32 需要的所有模块 |
| `kernel-headers-2.0.32-2.1386.rpm` | Linux 版本 2.0.32 的头文件（如果你需要重建内核） |
| `kernel-source-2.0.32-2.1386.rpm` | Linux 版本 2.0.32 的源码（如果你需要重建内核） |

## 第 2 章：升级 Linux

此步骤将创建一个 `/lib/modules/2.0.32` 目录并将模块文件放置在该目录中。

只有在你想要构建新内核时，才需要安装内核源码和内核头文件（headers）RPM 包。使用以下命令安装这些包：

```
rpm kernel-source-2.0.32-1.i386.rpm
rpm kernel-headers-2.0.32-2.i386.rpm
```

### 创建新的初始 RAM 磁盘 (initrd)

如果你的系统中带有 SCSI 适配器且你正在使用 SCSI 设备驱动程序，你必须创建一个新的初始 RAM 磁盘镜像——这是一个可以复制到内存块并用作内存驻磁盘的文件。

要查看你是否有任何 SCSI 驱动模块，请尝试以下命令：

```
grep scsi /etc/conf.modules
```

如果此命令没有产生任何输出，说明你的系统没有使用 SCSI 模块，也不需要初始 RAM 磁盘。你可以跳过此步骤并继续配置 LILO。

在我带有 Adaptec AHA 1542 SCSI 适配器的其中一个系统上，当我使用 `grep` 命令搜索时得到了以下结果：

```
grep scsi /etc/conf.modules
alias scsi_hostadapter aha1542
```

在这种情况下，我必须使用名为 `mkinitrd` 命令的文件创建初始 RAM 磁盘。通常，初始 RAM 磁盘镜像存储在以 `initrd` 开头的文件中。正如你猜到的，`initrd` 是 initial RAM disk 的缩写，而 `mkinitrd` 命令之所以这样命名是因为它可以创建一个 initrd 文件。

要为版本 2.0.32 的内核创建 RAM 磁盘镜像，请输入以下命令：

```
/sbin/mkinitrd /boot/initrd 2.0.32.img 2.0.32
```

这会在 `/boot` 目录下创建 `initrd-2.0.32.img` 文件。你将在 LILO 配置文件 (`/etc/lilo.conf`) 中引用此 initrd。

### 重新配置 LILO

在安装 RPM 包并在必要时创建了初始 RAM 磁盘镜像后，你必须重新配置 LILO，使其能够引导新内核。重配置步骤类似于之前在“安装新内核”中描述的过程。唯一的区别在于，如果你的系统需要 SCSI 驱动模块，则需要包含一行 `initrd`。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_160_0.png)

使用 `vi` 或 `Emacs` 等文本编辑器编辑 `/etc/lilo.conf` 文件。在该文件的开头处，`timeout` 行之后添加以下行：

```
image=/boot/vmlinuz-2.0.32
label=linux-new
root=/dev/hda1
initrd=/initrd-2.0.32.img
read-only
```

在 `root=/dev/hda` 行上，将 `/dev/hda1` 更改为 Linux 系统根目录 (`/`) 所在磁盘分区的正确设备名称。

编辑并保存 `/etc/lilo.conf` 文件后，使用以下命令重新安装 LILO：

```
/sbin/lilo
```

现在你可以重启系统并尝试新版本的内核了。

### 尝试新内核

在你安装了内核和内核模块的 RPM 包、创建了初始 RAM 磁盘文件并重新配置了 LILO 后，你就准备好尝试新内核了。在 LILO 提示符输入以下内容：

```
reboot
```

当系统重启并看到 LILO 启动提示符时，输入 `linux-new` 来引导新内核。如果你在 LILO 配置文件中将新内核描述放在所有其他操作系统之前，即使你没有在提示符处输入任何内容，该内核也应该启动：

Linux 启动后，你应该在登录提示符之前看到以下消息：

Red Hat release 5.0 (Hurricane)

Kernel 2.0.32 on an i386

现在你的 Linux 系统正在运行内核 2.0.32 版本。

# 总结

Linux 的开发通过许多程序员（以及许多新程序员）的努力，他们不断增强 Linux 并发布错误修复和新版本。你可能偶尔需要获取某些更新或错误修复并重新构建 Linux 内核。本章提供了有关如何应用修复（称为补丁）以及如何构建新内核的详细信息。它还向你展示了如何以 Red Hat 包管理器 (RPM) 文件的形式从 Red Hat 下载并安装更新。下一章从安装和配置细节开始，并提供 Linux 的概述以及你可以用 Linux 做的事情。

## 第 2 章：升级 Linux

通过阅读本章，你将学习以下内容：
