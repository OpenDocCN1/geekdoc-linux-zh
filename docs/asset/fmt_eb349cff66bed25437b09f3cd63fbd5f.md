
我首先通过 `NANO_NAME` 变量给此磁盘指定一个唯一名称 ①。我对此设备有一个自定义内核配置 ②。我在哪里获取的这个内核配置？我启动三星磁盘以捕获 `GENERIC` 内核的 `/var/run/dmesg`，然后在互联网上搜索其他人使用的其他潜在有用内核。启动这种无设备唯一讨厌的地方是你必须在启动加载程序中禁用 ACPI。

由于磁盘启动，我知道 NanoBSD 使用闪存槽作为驱动器 `/dev/ad1` ③。如果我不在配置文件中设置此项，我的第一个 NanoBSD 将抱怨无法在 `/dev/ad0` 上找到分区。

然后我列出了想在该镜像上使用的 `custom_scripts`。这些脚本都是关于本章稍后部分的自定义的，我建议在你的第一个镜像中使用它们。

然后我们还有供 `make(1)` 在安装过程中使用的特殊选项。我们稍后会查看这些选项，但现在你只需要知道 `WITHOUT_TOOLCHAIN` 让 `make(1)` 不安装编译器、库或其他构建软件所需的其他工具。我们将在嵌入式系统上构建端口！

注意 `CONF_INSTALL` ⑤ 变量是如何设置的。我们在等号后有一个单引号（`''`），在它的某行中是我们的变量，然后之后又有一个单引号（`''`）。这保持了多个选项分离并使文件可读。我们对 `CONF_WORLD` 采取了类似的操作，期望每个变量都单独占一行，因为它将根据它们构建一个私有的 `make.conf`。

`CONF_WORLD` 中的每个选项都告诉不要构建 FreeBSD 的特定部分。例如，`WITHOUT_ACPI` 意味着不构建内核模块。我刻意构建我不想放入最终磁盘镜像的系统，例如 Sendmail、gmail 和数据包过滤器。

这些选项都埋在 FreeBSD 的结构中。其中一些已经存在多年；另一些是新的。其中一些将会消失——无法保证它们任何一个在未来的发布中仍然有效。你的 `src.conf` 手页有已安装的 FreeBSD 的构建变量当前列表，我包含整个列表是为了让你看到你删减得多么激进。FreeBSD 比许多 Linux 发行版小得多；但并不意味着它不能变得更小。

然而，NanoBSD 是。例如，`WITHOUT_SETUID_LOGIN` 对你的登录有不利影响。`WITHOUT_SYMVER` 会移除符号版本，这将导致无法在 NanoBSD 镜像中使用在其他 FreeBSD 上编译的二进制文件。在启用之前，请确保你理解构建选项的作用。

此外，请注意你可能需要为特定的 NanoBSD 镜像禁用某些构建选项。我正在构建一个 DNS 服务器，所以我需要 BIND。我在这次特定构建的配置文件注释了 `WITHOUT_BIND`。

在 `CONF_INSTALL_option` 中，我列出了在安装 FreeBSD 7.0 的构建不再使用的选项。`WITHOUT_TOOLCHAIN` 通知 `installworld` 不要在磁盘镜像上安装编译器、头文件或相关工具。我们需要构建一个新的编译器来构建新的 FreeBSD，但我们不需要在最终镜像中包含它。安装过程不会尝试安装我们从构建中剔除的任何内容，但运行 `buildworld` 需要一个最新的编译器。

这是一个完整的 NanoBSD 配置文件。现在，让我们使用它来构建自定义镜像。

# 构建 NanoBSD

将 `nanobsd.sh` 作为 shell 脚本运行，并使用 `-c` 指定配置文件：

```
# /bin/sh nanobsd.sh -c mynanoconfig.txt
```

NanoBSD 构建在进行过程中会打印通用日志：

```
## Clean and create object directory (/usr/obj/nanobsd.SoekrisDNS/)
## Construct build make.conf (/usr/obj/nanobsd.SoekrisDNS/make.conf)
## run buildworld
## log: /usr/obj/nanobsd.SoekrisDNS//_bw
## build kernel (SOEKRIS)
## build dimage
## log: /usr/obj/nanobsd.SoekrisDNS//_.di
## NanoBSD image completed
```

如果你看到 `NanoBSD image completed`，说明构建成功。如果没有，则构建在日志中看到的最后一个阶段失败了。对配置文件进行多轮排查以使其正常工作并不罕见，特别是当你激进地使用 `WITHOUT_options` 来减小 FreeBSD 体积时。

# NanoBSD 构建目录

NanoBSD 在 `/usr/obj` 下使用一个名为 `Nano_NAME` 的构建目录。我们的配置文件指定我们正在构建一个名为 `SoekrisDNS` 的 NanoBSD，因此我们的构建目录是 `/usr/obj/nanobsd.SoekrisDNS`。进入该目录并查看文件。你会发现多个命名文件、大型目录和磁盘镜像。

NanoBSD 使用以 `_` 开头的文件作为标记、日志和临时目录。尽管你在构建过程中看到的信息非常简短，但 NanoBSD 并没有真正丢弃它为构建磁盘镜像而运行的命令的输出；它将其重定向到其他文件。

# 表 20-1：NanoBSD 构建文件

| 文件 | 目的 |
| --- | --- |
| `_bk` | `make buildkernel` 日志 |
| `_bw` | `make buildworld` 日志 |
| `_cust.X` | 安装自定义 X |
| `_di` | `fdisk` 磁盘镜像 |
| `_dl` | `Disklabel` 磁盘镜像 |
| `_env` | 构建 NanoBSD 时使用的环境 |
| `_etc` | `make distribution` 日志 |
| `_fdisk` | `fdisk(8)` 配置 |
| `_ik` | `make installkernel` 日志 |
| `_iw` | `make installworld` 日志 |
| `_w` | 新构建的 world |
| `disk.image` | 单个分区的磁盘镜像 |
| `disk.full` | 完整设备的磁盘镜像 |

使用日志文件解决构建和配置问题。

# NanoBSD 构建故障

NanoBSD 在构建失败时提供的错误信息非常有帮助。例如，这里是一个失败的 NanoBSD 构建的完整输出：

```
# /bin/sh nanobsd.sh -c soekris-dns.conf
# Clean and create object directory (/usr/obj/nanobsd.SoekrisDNS/)
# Construct build make.conf (/usr/obj/nanobsd.SoekrisDNS/make.conf)
# Run buildworld
### log: /usr/obj/nanobsd.SoekrisDNS//_bw
```

你可以看到过程失败了，但不知道为什么。要获取实际错误，请查看消息中指定的日志文件。在这种情况下，日志文件为 `/usr/obj/nanobsd.SoekrisDNS/_bw`。该日志文件的末尾显示了失败进程的最后输出。你会看到升级过程中该部分常见的错误。

需要记住的一点是，NanoBSD 默认使用 `-j`。这可能会模糊日志中的错误信息，导致崩溃的错误可能在构建表面结束之前的几行处。

为什么从相同的源码进行常规升级是行通的，但 NanoBSD 却会失败呢？构建失败的主要原因是为源码树选择了不兼容的构建选项。NanoBSD 配置文件包含许多不同的 `WITHOUT_options`。你可能会注意到其中一些被注释掉了。在我构建此磁盘镜像时，那些选项导致了构建失败。虽然我的嵌入式 DNS 服务器不需要这些注释选项提供的软件，但未包含这些选项破坏了我的 NanoBSD 构建。（`WITHOUT_BIND` 当然被注释掉了，因为我希望在这个镜像上使用 BIND。）

当你构建 NanoBSD 镜像时可能遇到的另一个问题是构建完成后，磁盘镜像构建如下：

```
/usr/obj/nanobsd.SoekrisDNS/_mnt: write failed, filesystem is full
```

（注：原文后续存在大量重复内容，译文已按要求仅保留核心部分。）

NanoBSD 包含四个自定义脚本：

*   **cust_comconsole**：启用串口控制台和串口登录。
*   **cust_allow_ssh_root**：允许 root 用户通过 SSH 登录系统。
*   **cust_install_files**：将 Files 目录下的文件拷贝到完成的镜像中。
*   **cust_pkg**：将 Pkg 目录下的包安装到完成的镜像中。

正如你可能已经察觉到的，自定义脚本是驱动调整镜像的另外两种方法的核心。

## 添加包

在 NanoBSD 目录中创建一个 Pkg 目录。自定义脚本 `cust_pkg` 会将你放置在该目录中的任何包安装到你的镜像中。这确实非常高效。

但是，如果你的空间不足，你并不需要安装整个包。找到你想要运行的程序的二进制文件，使用 `ldd(1)` 识别所需的库文件，并只将这些文件拷贝到你的镜像中即可。

## 添加文件

`cust_install_files` 自定义脚本会将 Files 目录下的树结构中的文件拷贝到你完成的镜像中。默认情况下，Files 目录包含一个名为 `root` 的子目录。该目录的内容会被拷贝到镜像的 `/root/`。

如果你定期构建 NanoBSD 镜像，我建议修改 `cust_install_files` 脚本。NanoBSD 在 Files 目录中包含了几个文件，这些文件被视为系统文件。当你更新源码树时，`cp(1)` 会清除你对 Files 目录下文件所做的任何更改。将 `cust_install_files` 拷贝到你的配置文件中，给它命名，并将其指向 Files 以外的目录。

我正在构建一个 DNS 服务器，所以我需要创建一个自定义的 `named.conf` 和 `rndc.conf`。这些文件位于 `/var/named/etc/namedb`，因此我必须创建目录 `/usr/src/tools/tools/namedd/Files/var/named/etc/namedb`（真晦命！）并将我的自定义文件放在那里。

同样，我会在 `rc.conf` 中创建一个 `Files/rc.conf` 用于我的配置。我需要 SSH 密钥，我会像为磁盘工作站创建的那样创建它们。同样，还需要一个写入到我网络日志服务的 `syslog.conf`。

使用 NanoBSD 的最后一个烦恼是硬性控制台速度。在我们的配置文件中设置了 `CONSOLE_SPEED` 变量，让 FreeBSD 使用默认的 19200 控制台速度。如果你没有这样做，适应端口速度差异的最简单方法是将 FreeBSD 设置为使用更高的控制台速度。你可以通过在 `/boot/loader.conf` 中添加正确的条目来实现。只需在 `Files/boot/loader.conf` 中创建以下条目：

```
comconsole_speed="19200"
console=comconsole,vidconsole
```

这为你的 NanoBSD 安装提供了一个默认速度为 19,200bps 的串口控制台。然而，在引导加载程序启动之前，它不会生效。你最好通过 `CONF_WORLD` 变量以 19200 的控制台速度来构建你的 NanoBSD 世界。

## 完善自定义设置

构建 NanoBSD 镜像的头疼问题之一是为你的目的获取正确的自定义设置。你会添加你认为镜像中需要的每一个文件和设置，将完成的镜像拷贝到闪存盘，并在设备上启动它，结果发现你漏掉了某些内容，必须向镜像中添加文件。

虽然构建 NanoBSD 镜像需要一段时间，但过程中最长的部分是构建世界和内核。你可以向自定义镜像中添加文件，并通过向 `nanobsd.sh` 添加 `-b` 标志，在不构建整个世界和内核的情况下运行镜像构建过程。

```
# /bin/sh nanobsd.sh -b myconfig.txt
```

这将跳过 `buildworld` 和 `buildkernel` 阶段，并使用你更新后的文件组装磁盘镜像。

## 使用 NanoBSD

现在你有了一个可以启动并包含所有所需软件的 NanoBSD 镜像。你已将其拷贝到闪存盘并顺利运行。当你必须进行细微调整时会发生什么？不用担心，NanoBSD 为这些情况提供了特殊措施。

## 微量更新

NanoBSD 使用 `cfg` 分区来处理微调。`/cfg` 中的任何文件在启动时都会拷贝到运行中的 NanoBSD。这意味着你无需构建新镜像即可对 `/etc` 进行更改。这种方法的一个很好的例子是查看 `Files/root` 中的 `change_passwd` 脚本。该脚本运行 `passwd(1)` 来更改根密码，挂载 `/cfg` 为读写模式，将密码文件拷贝到 `/etc`，然后卸载 `/cfg`。当系统下次启动时，NanoBSD 会将这些关键密码文件拷贝到 `/etc`。

当你对运行中的 NanoBSD 系统进行更改时，我建议对你的 NanoBSD 构建系统进行相应的更改。这样当你需要制作新的磁盘镜像时，你的更改将完整保留并保持最新。

## 更新磁盘镜像

现在你已经构建了 NanoBSD 镜像并在 NanoBSD 上运行它。当你必须进行细微更改或升级时该怎么办？包含的升级脚本允许你升级磁盘镜像，如果新镜像无法工作，你可以启动原始镜像，在排查问题时恢复服务。

通过以下命令远程升级 NanoBSD 安装：

```
# /bin/sh nanobsd.sh -b myconfig.txt
```

对于你的第一个 FreeSBIE 构建，我建议尽可能少地更改。虽然许多选项可能很吸引你修改，但尽可能保持默认设置可以获得最佳的初始结果。过度野心的初始自定义会导致构建失败。与许多许多事情一样，我建议你一次学习 FreeSBIE 的隐藏陷阱。

```
BASEDIR="/usr/local/freesbie-fs"
```

这是 FreeSBIE 安装其新构建的世界系统、包和自定义文件的目录。

```
CLONEDIR="/usr/local/freesbie-clone"
```

FreeSBIE 在构建镜像时使用此目录作为临时暂存区域。

```
SRDIR="/usr/src"
```

这是 FreeSBIE 用于构建世界系统和内核的源码树。

```
ISOPATH="/usr/obj/FreeSBIE.iso"
```

FreeSBIE 将完成的 ISO 放置于此位置。

```
IMGPATH="/usr/obj/FreeSBIE.img"
```

这是用于闪存媒体的完成的 UFS FreeSBIE 镜像的完整路径。

```
MAKE_WORLD="-j3"
```

这决定了在构建世界系统时 `make(1)` 使用的 `-j` 参数。如果你构建失败并想确定是实际问题还是只是并行化问题，请设置此 `-j`。

```
KERNEL="-j1"
```

这设置了在构建内核时 `make(1)` 的并行化程度。

```
MAKEOPT="-DNO_CLEAN"
```

如果你想在构建世界系统和内核时使用 `make(1)` 选项，请在此处指定它们。

```
KERNELCONF="/usr/src/sys/i386/CUSTOMFRESBIE"
```

这是 FreeSBIE 内核配置文件的路径。我发现 FreeSBIE 提供的内核配置仅适用于 FreeSBIE 开发人员正在使用的 FreeBSD 版本。从 FreeBSD 7.0 开始，FreeSBIE 构建利用了以下非-GENERIC 选项：

| options | GEOM_UZIP |
| :--- | :--- |
| options | GEOM_LABEL |
| options | VESA |
| options | SC_PIXEL_MODE |

此外，我还删除了所有的 SCSI 和 RAID 控制器，因为我真的不需要访问那些磁盘。如果我不想碰硬盘，就使用此设备，这样我的磁盘镜像就找不到任何 IDE 磁盘。如果你需要防火墙功能，请添加 PF 内核选项。

```
MAKE_CONF="/etc/make.conf"
```

这定义了你想为 FreeSBIE 构建使用的自定义 `make.conf`。请注意，由于包是从已安装的系统复制的，任何特殊的 `make.conf` 设置都不会应用到包。你可能更应该使用 `src.conf`。

```
SRC_CONF="/etc/src.conf"
```

你可以使用 `src.conf` 自定义源码构建，就像对主 FreeBSD 构建所做的那样。在此处指定你 FreeSBIE 特有的 `src.conf` 的完整路径。

```
FILE_LIST="/home/mulucas/freesbie-files.txt"
```

你可以精确指定你想要安装在 FreeSBIE 磁盘上的哪些文件。如果你定义了一个列表文件，FreeSBIE 将仅将此列表中的文件安装到镜像中。（实际上，这意味着只有列表上的文件会从 FreeSBIE 基础目录复制到 FreeSBIE 目录。）这意味着你必须对实时 CD 上的所有文件列出一份百分之百完整的列表。在我看来，这对于类似 NanoBSD 的小型系统最有用。

```
PRUNE_LIST="home/mulucas/freesbie-prune.txt"
```

该文件包含构建包含的文件和目录列表，但在构建实时 CD 镜像之前必须删除它们。清理列表文件中列出的任何文件都会在从该目录构建镜像之前从克隆目录中删除。这对于减小实时 CD 的大小非常有用。

```
PKFILE="/home/mulucas/freesbie-packages"
```

此文件包含包列表，每行一个包并带有版本信息。如果你不设置此项，FreeSBIE 的 `makeselect` 将此列表上的所有包安装到你的实时镜像中。这会在 `/usr/local/share/freesbie/conf/packages` 文件中创建一个包列表。

```
EXTRA=customrootfs etcmfs sound tattoart
```
