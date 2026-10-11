

```
$ torrentinfo-console Fedora-12-i386-DVD.torrent
torrentinfo-console 4.4.0 - decode BitTorrent metaInfo files

metaInfo file..... : Fedora-12-i386-DVD.torrent
info hash......... : 9aae97762980179119dbbdfefc1f8de0356f675f3
directory name.... : Fedora-12-i386-DVD
files........... :
				Fedora-12-i386-CHECKSUM (1511)
				Fedora-12-i386-DVD.iso (3204427776)
archive size....... : 3204429287 (12223 × 262144 + 243175)
tracker announce url: http://torrent.fedoraproject.org:6969/announce
comment......... :
```

## RPM：红帽软件包管理器

**rpm**（Red Hat Package Manager，红帽软件包管理器）实用程序仅适用于为 **rpm** 处理而构建的软件包；它用于安装、卸载、升级、查询和验证 **rpm** 软件包。由于红帽将 **rpm** 以 GPL 许可发布（第 4 页），许多不同的发行版都使用 **rpm**。此实用程序会跟踪软件包的安装位置、已安装软件包的版本以及软件包之间的依赖关系。

**rpm** 源软件包通常位于名为 **SRPMS**（source rpms，源 rpm 软件包）的目录中，而二进制 **rpm** 软件包通常位于 **Packages** 中。下载二进制软件包时，请确保它们适用于本地操作系统（包括发行版和版本——例如 Fedora 12）。$^1$ 它们还应针对相应的体系结构进行编译：

-   **i386** 涵盖所有基于 Intel 的大多数 AMD 系统。
-   **i586** 涵盖 Pentium 级或更高处理器。
-   **i686** 指 Pentium II 或更好的处理器，并包含 MMX 扩展。
-   **S390x** 用于 IBM System/390。
-   **ia64** 用于 Intel 64 位 Intel Itanium（与 x86_64 不兼容）。
-   **alpha** 用于 DEC/Compaq Alpha 芯片。
-   **ppc** 和 **ppc64** 分别指代 Power PC 32 位和 64 位处理器。
-   **x86_64** 用于 Intel 和 AMD 64 位处理器（非 Itanium）。
-   **sparc** 涵盖 Sun Sparc 处理器。

**rpm** 文件的名称包含了几乎所有必要的信息。

> yumdownloader 有关使用 **yumdownloader** 下载 **rpm** 软件包文件的说明，请参阅第 505 页。

1.  许多 **rpm** 软件包可以在除其编译目标以外的其他版本甚至其他发行版上运行。然而，安装为其他发行版准备的软件包可能会引发问题。

## 查询软件包和文件

rpm 实用程序可以从命令行运行。使用 `rpm -qa` 显示系统上已安装的所有软件包的一行摘要列表（任何用户都可以运行此实用程序）。输入命令 `rpm -q`，后跟软件包名称，以显示有关特定软件包的更多信息。例如，`rpm -q nis` 会告诉你 NIS 是否已安装，如果是，则是哪个版本。使用 `-ql` 选项列出软件包中的文件。

```bash
$ rpm -q nis
package nis is not installed

$ rpm -ql logrotate
/etc/cron.daily/logrotate
/etc/logrotate.conf
/etc/logrotate.d
/usr/sbin/logrotate
/usr/share/doc/logrotate-3.7.8
/usr/share/doc/logrotate-3.7.8/CHANGES
/usr/share/doc/logrotate-3.7.8/COPYING
/usr/share/man/man8/logrotate.8.gz
/var/lib/logrotate.status
```

使用 `-qi` 选项，rpm 将显示软件包的信息：

```bash
$ rpm -qi logrotate
Name          : logrotate                       Relocations: (not relocatable)
Version       : 3.7.8                           Vendor:       Fedora Project
Release       : 4.fc12                         Build Date:   Thu Sep 17 02:43:34 2009
Install Date  : Tue Sep 22 11:40:43 2009        Build Host:   x86-4.fedora.phx.redhat.com
Group         : System Environment/Base         Source RPM:   logrotate-3.7.8-4.fc12.src.rpm
Size          : 79680                           License:     GPL+
Signature     : (none)
Packager      : Fedora Project
Summary       : Rotates, compresses, removes and mails system log files
Description   :
The logrotate utility is designed to simplify the administration of
log files on a system which generates a lot of log files. Logrotate
allows for the automatic rotation compression, removal and mailing of
log files. Logrotate can be set to handle a log file daily, weekly,
monthly or when the log file gets to a certain size. Normally,
logrotate runs as a daily cron job.
```

如果你需要一个处理系统日志文件的实用程序，请安装 logrotate 软件包。

你可以使用 `-qf` 选项来确定文件属于哪个软件包。以下命令显示 `more` 属于 util-linux 软件包：

```bash
$ rpm -qf /bin/more
util-linux-ng-2.16-10.2.fc12.i686
```

将 `-p` 选项与其他选项一起使用，以查询未安装的 rpm 软件包文件。

## 安装、升级和移除软件包

虽然使用 `yum`（第 500 页）、`gpk-application`（第 123 页）或 `pirut`（第 505 页）通常更容易，但你也可以使用 `rpm` 来安装、升级或移除软件包。请以 root 身份登录（或 `su` 切换到 root）。（虽然你可以以非特权用户身份运行 `rpm`，但在安装或卸载期间，你没有权限写入必要的目录，操作将失败。在查询期间，你不需要此权限，因此可以且应当以非特权用户身份工作。）输入 `-U`（upgrade，升级）选项，后跟包含你要安装的软件包的 rpm 版本的文件名。`-U` 选项会升级现有软件包并安装新软件包（就好像你使用了 `-i` 选项一样）。对于内核，请使用 `-i`（而不是 `-U`），以便在安装新内核时保留旧内核。添加 `-v`（verbose，详细）选项以显示有关正在发生的事件的更多信息，并添加 `-h`（或 `--hash`）选项以在软件包解包和安装时显示哈希标记。例如，以 root 身份登录时，输入以下命令在本地系统上安装 samba 软件包：

```bash
# ls samba
samba-3.4.2-47.fc12.i686.rpm
# rpm -Uhv samba-3.4.2-47.fc12.i686.rpm
Preparing...                ########################################### [ 100%]
  1:samba                  ########################################### [ 100%]
```

安装软件包时，rpm 文件必须位于工作目录中，或者必须使用指向 rpm 文件的路径名。

要移除相同的软件包，请从任何目录输入以下命令：

```bash
# rpm -e samba
error: Failed dependencies:
samba is needed by (installed) system-config-samba-1.2.83-1.fc12.noarch
```

运行此命令时，rpm 会报告另一个软件包 system-config-samba 依赖于 samba 软件包。要移除 samba 软件包，你有两个选择：你可以包含 `rpm --nodeps` 选项来忽略依赖关系，或者你可以先移除依赖软件包，然后再移除 samba 软件包。

```bash
# rpm -e system-config-samba
# rpm -e samba
```

如果在移除依赖于它的软件包之前移除 samba 软件包，依赖软件包内的实用程序将无法工作。在前面的示例中，system-config-samba 实用程序将无法工作。

当你使用 rpm 移除软件包时，rpm 会查询其数据库以找到卸载软件包所需的信息，并移除链接、卸载设备驱动程序，必要时停止守护进程。有关更多 rpm 选项，请参阅 rpm 手册页。

## 安装 Linux 内核二进制文件

以下步骤用于安装新的 Linux 内核二进制文件。如果你想要配置并从头文件重新构建内核，而不是安装新的预构建内核二进制文件，请参阅第 15 章。

1.  运行 rpm 并使用 `-i` 选项安装新内核。不要使用 `-U` 选项：你正在安装一个新内核，其名称与旧内核不同；你并非在升级现有内核。
2.  在移除旧内核之前，确保新内核可以正常工作。要验证新内核是否正常工作，请使用新内核重启系统。在移除旧内核之前，你可能需要等待一段时间，以确保新内核没有出现问题。
3.  通过移除文件名中包含发行版本号（以及 EXTRANUMBER 或 [第 548 页]，如果适用）的文件来移除旧内核，这些文件位于 /boot 或 /（根）目录中。从 grub.conf（第 551 页）中移除有关旧内核的信息。代替手动移除旧内核，你可能能够使用用于安装它的工具（rpm、yum 或其他实用程序）来移除它。

## 安装非 RPM 软件

大多数非 rpm 格式的软件都附带了详细的说明，介绍如何配置、构建（如果需要）以及安装该软件。某些二进制发行版（包含在 Fedora/RHEL 上运行的预构建可执行文件）要求你从根目录解包软件。

## /opt 和 /usr/local 目录

一些较新的应用程序软件包包含脚本，可以自动将它们自己安装到 /opt 下的目录层次结构中，将文件放置在以软件包命名的 /opt 子目录中，可执行文件放置在 /opt/bin 或 /opt/package/bin 中。这些脚本对于 Fedora/RHEL 来说相对较新，但 Sun Solaris 已使用它们一段时间了。

其他软件包允许你选择解包位置。由于许多不同的人为 Linux 开发软件，因此没有一致的安装方法。获取软件时，请以尽可能一致和可预测的方式将其安装到本地系统上。标准 Linux 文件结构在 /usr/local 下有一个目录层次结构，用于二进制文件（/usr/local/bin）、手册页（/usr/local/man）等。为了避免日后混淆，并防止将来安装标准软件升级时覆盖或丢失软件，请避免在标准系统目录（如 /usr/bin）中安装非标准软件。在多用户系统中，确保用户知道在哪里找到本地软件，并在安装、更改或移除本地工具时发布公告。

## GNU 配置和构建系统

GNU 配置和构建系统，也称为 Automake，使得构建以源代码形式分发程序变得容易（www.gnu.org/software/automake/manual/automake.html#Autotools-Introduction）。这种两步过程不会

