
- 发布号：`5`（这是一个 Red Hat 分配的数字）

- 架构：`i386`（此软件包适用于 Intel 86 处理器）

通常，软件包名足以让你猜测 RPM 可能的内容。版本号与软件包当前的版本号相同（即使它是以其他形式如 tar 包分发的）。Red Hat 指定发布号来跟踪更改。对于要在 Intel x86 兼容处理器上安装的 RPM，架构应该是 `i386` 或 `noarch`。

## 查询 RPM

在安装时，`rpm` 命令建立已安装 RPM 的数据库。你可以使用 `rpm -q` 命令查询系统中已安装的软件包。例如，查询系统中安装的 Linux 内核版本号，输入以下 `rpm -q` 命令：

```
rpm -q kernel
```

你应该看到类似下面的响应：

```
kernel-2.4.20-20.2013.npt1
```

响应是内核 RPM 的名称（这是内核的可执行版本，而不是源文件）。名称与 RPM 文件名相同，只是没有显示最后部分——`i386.rpm`。在这种情况下，RPM 的版本部分告诉你内核是 `2.4.20`。

## 466 使用 Red Hat 软件包管理器

你可以使用以下命令查看所有已安装的 RPM 列表：

```
rpm -qa
```

你会看到一长长的 RPM 列表在屏幕上滚动。如果想一次显示一屏列表，可以使用：

```
rpm -qa | more
```

如果你想搜索特定的软件包，可以将 `rpm -qa` 的输出通过传递给 `grep` 命令。例如，要查看所有名称中包含 `kernel` 的包，请输入：

```
rpm -qa | grep kernel
```

结果取决于系统上安装了哪些部分的内核 RPM。例如，在我的系统上，该命令显示如下：

```
kernel-pcmia-cs-3.1.31-13
kernel-source-2.4.20-20.1.2013.nptl
kernel-2.4.20-20.1.2013.nptl
```

使用 `rpm -q` 命令可以查询的内容远比软件包版本号得多。通过添加单字母选项，你可以找到其他有用信息：例如，尝试以下命令来查看内核包中的文件：

```
rpm -ql kernel
```

以下是该命令输出的几行：

```
/boot/System.map-2.4.20-20.1.2013.nptl
/boot/config-2.4.20-20.1.2013.nptl
/boot/vmlinux-2.4.20-20.1.2013.nptl
/dev
/lib/modules
/lib/modules/2.4.20-20.1.2013.nptl/build
/lib/modules/2.4.20-20.1.2013.nptl/kernel
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/cpuid.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/edd.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/microcode.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/msr.o
(其余列表已删除)
```

## 使用 Red Hat 软件包管理器（47 节）

这里是其他一些有用的 `rpm -q` 命令形式，用于查询软件包信息（要使用任何这些 `rpm -q` 命令，请在输入命令后加上包名）：

- `rpm -qc` — 列出软件包中的所有配置文件。
- `rpm -qd` — 列出软件包中的所有文档文件。这些通常是在线手册页（也作为 man 页面）。
- `rpm -qf` — 显示特定字段所属的包名（如果有）。
- `rpm -qi` — 显示软件包的详细信息，包括版本号、大小、安装日期和简要描述。
- `rpm -ql` — 列出软件包中的所有文件。对于某些软件包，这可能是一个非常长的列表。
- `rpm -qs` — 列出软件包中所有文件的状态。

这些命令仅提供已安装软件包的信息。如果你想查找未安装的 RPM 文件信息，请在每个命令的命令行选项添加字母 `p`。例如，要查看命名为 `rdist-6.1.5-27.1.i386.rpm` 的 RPM 文件中的列表，请使用以下命令：

```
rpm -qpl rdist-*.rpm
```

当然，这仅在当前目录包含 RPM 文件时才有效。

## 安装 RPM

要安装 RPM，请使用 `rpm -i` 命令。你将 RPM 文件名作为参数提供。一个典型的例子是从本书的包含 Red Hat Linux RPM 的随附 DVD 中安装 RPM。按照惯例，你必须挂载 DVD 并切换到 RPM 所在的目录。然后使用 `rpm -i` 命令安装 RPM。如果你想查看 RPM 安装的进度，请使用 `rpm -ivh`。在解包软件包时，会显示一系列哈希标记（`#`）。

例如，从随附 DVD 安装 `kernel-source` RPM（包含 Linux 系统的源码文件），我插入 DVD 并在挂载后，输入以下命令：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh kernel-source-*
```

## 468 使用 Red Hat 软件包管理器（48 节）

你不需要输入完整的 RPM 文件名——可以使用名称开头的几个字符后跟一个星号（`*`）。确保你输入的名称足够，能够唯一标识该 RPM。

如果你尝试安装一个已经安装的 RPM，`rpm -i` 命令会显示错误信息。例如，当我在系统上输入以下命令安装 man 软件包时，发生了这种情况：

```
rpm -i man-1*
```

我收到了 `rpm -i` 命令的以下错误信息：

```
package man-1.5k-8 is already installed
```

要强制 `rpm` 命令在存在错误的情况下安装软件包，只需在 `rpm -i` 命令中添加 `--force`，如下所示：

```
rpm -i --force man-1*
```

## 移除 RPM

当你意识到不需要某个软件包时，可能想要移除它。要移除软件包，请使用 `rpm -e` 命令。你提供要删除的包名。如果该包被其他包需要，命令将显示错误信息。要强制移除软件包，请使用 `--force` 选项：

```
rpm -e --force package_name
```

要移除软件包及其所有依赖项，请使用 `--nodeps` 选项：

```
rpm -e --nodeps package_name
```

## 从源文件构建软件包

通过 Web 浏览器使用匿名 FTP 下载压缩的 tar 文件。通常，这不需要你付出额外努力，只需点击链接并将文件保存到系统中合适的目录中。

若要尝试下载和构建软件包，你可以在 X 多媒体系统 (`XMMS`) 上进行练习——这是一个用于播放 MP3 和其他多媒体文件的图形化 X 应用。`XMMS` 随 Red Hat Linux 自带，你的系统中应该已经安装了。然而，重新下载并重新构建 `XMMS` 程序包也没有处。

从 `www.xmms.org/download.php` 下载 `XMMS` 的源文件。文件以压缩 tar 归档的形式打包。点击源码的 ftp 链接并将其保存到你 Red Hat Linux 系统中的 `/usr/local/src` 目录中。（务必以 root 身份登录；否则你无法保存到 `/usr/local/src` 目录。）

下载压缩的 tar 文件后，使用以下命令检查内容：

```
tar ztf xmms*.gz | more
```

你应该会看到类似下面的列表：

+ xmms-1.2.7/

xmms-1.2.7/Makefile.in

xmms-1.2.7/README

xmms-1.2.7/stamp-h1.in

xmms-1.2.7/ABOUT-NLS

xmms-1.2.7/AUTHORS

xmms-1.2.7/COPYING

xmms-1.2.7/ChangeLog

xmms-1.2.7/INSTALL

xmms-1.2.7/Makefile.am

xmms-1.2.7/NEWS

xmms-1.2.7/TDOOD

xmms-1.2.7/acconfig.h

xmms-1.2.7/acinclude.m4

xmms-1.2.7/acclocal.m4

xmms-1.2.7/config.guess

xmms-1.2.7/config.h.in

xmms-1.2.7/config.sub

xmms-1.2.7/configure

（其余输出略）
