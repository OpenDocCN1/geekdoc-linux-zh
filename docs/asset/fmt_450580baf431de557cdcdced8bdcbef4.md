
```
cd /cdrom/RedHat/RPMS
ls -rpm | more
AnotherLevel-0.5.2.noarch.rpm
BRU2000 15:0p 1.1386.rpm
BRU2000 11:05p-1.1386.rpm
Electricference-2.0.5-1.1386.rpm
ImageMagick-3.9.1-1.1386.rpm
ImageMagick-devel-3.9.1-1.1386.rpm
MAKEDEV-2.3.1-noarch.rpm
SysVinit 2.71 3.1386.rpm
X11R6-contrib 3.3.1 1.1386.rpm
XFree86 100dpi fonts 3.3.1 14.1386.rpm
XFree86-3.3.1-14.1386.rpm
XFree86-75dpi-fonts-3.3.1-14.1386.rpm
(其余列表已删除)
```

如列表所示，所有的 RPM 文件都以 `.rpm` 扩展名结尾。为了理解文件名的各个部分，请考虑以下 RPM：

`XFree86-3.3.1-14.1386.rpm`

该文件名由以下由连字符 (`-`) 分隔的部分组成：

- 包名：`XFree86`
- 版本号：`3.3.1`
- 发布版本：`14`（这是 Red Hat 分配的发布版本）
- 架构：`i386`（这意味着该包适用于 Intel 8036 兼容处理器）

通常，包名具有足够的描述性，让你能猜出 RPM 可能包含的内容。版本号与软件包的当前版本号相同（即使它是以其他形式，如 tar 文件，分发的）。Red Hat 通过分配发布版本来跟踪更改。对于你想在带有 Intel x86 兼容处理器的 PC 上安装的 RPM，架构应该是 `i386` 或 `noarch`。

### 了解 RPM

`rpm` 命令在安装软件包时会构建一个已安装 RPM 的数据库。你可以使用 `rpm -q` 命令对该数据库进行查询，以确定安装在你的系统上的软件包的详细信息。

例如，要查找系统上安装的 Linux 内核版本号，请输入以下 `rpm -q` 命令：

```
rpm -q kernel
kernel-2.0.31-7
```

响应结果是内核的 RPM 名称（这是内核的可执行版本，而不是源代码）。该名称与 RPM 文件名相同，除了最后部分——没有显示 `.i386.rpm`。在这种情况下，RPM 的版本部分告诉你是内核版本为 2.0.31。

如果你打算编译内核，可能想知道系统中安装的 GNU C 编译器 (`gcc`) 的版本。要查看 `gcc` 版本号，请输入：

```
rpm -q gcc
gcc-2.7.2.3-8
```

响应结果告诉你你拥有 `gcc` 版本 2.7.2.3。

你可以通过以下命令查看所有已安装 RPM 的列表：

```
rpm -qa
```

你会看到一个长长的 RPM 列表在屏幕上滚动。为了一次显示一屏列表，可以使用：

```
rpm -qa | grep kernel
```

如果你想搜索特定的软件包，可以将 `rpm -qa` 的输出传递给 `grep` 命令。例如，要查看名称中包含 `kernel` 的所有软件包，请输入：

```
rpm -qa | grep kernel
kernel-2.0.31-7
kernel-headers-2.0.31-7
kernel-modules-2.0.31-7
kernelcfg-0.4-7
kernel-source-2.0.31-7
```

你可以使用 `rpm -q` 命令查询不仅是软件包的版本号。通过添加单项选项，你可以获取关于软件包的其他有用信息。例如，尝试以下命令来查看内核包中的文件：

```
rpm -ql kernel
/boot/System.map-2.0.31
/boot/module-info-2.0.31
/boot/vmlinuz-2.0.31
/sbin/installkernel
```

## 第 2 章：升级 Linux

以下是几种用于查询软件包信息的常用 `rpm` 命令形式（要使用任何这些 `rpm` 命令，请在输入命令后加上包名）：

| 命令 | 说明 |
| :--- | :--- |
| `rpm qc` | 列出包中的所有配置文件 |
| `rpm qd` | 列出包中的所有文档文件。这些通常是在线帮助页（也称为 man pages）。 |
| `rpm qi` | 显示软件包的详细信息，包括版本号、大小、安装日期和概要描述。 |
| `rpm ql` | 列出包中的所有文件。对于某些软件包，列表可能很长。 |
| `rpm qs` | 列出包中所有文件的状态。 |

### 安装 RPM

要安装 RPM，必须使用 `rpm` 命令。你必须提供 RPM 文件的名称作为参数。一个典型的示例是从 CD-ROM 安装 RPM。通常，你必须先挂载 CD-ROM，然后进入 RPM 所在的目录。然后使用 `rpm -i` 安装 RPM。

例如，从 CD-ROM 安装内核-source RPM（包含操作系统的源文件），你需要输入以下命令：

```
mount /dev/hdc /cdrom
mount: block device /dev/hdc is write protected, mounting read only
cd /cdrom/RedHat/RPMS
rpm -i kernel-source-*
```

注意，不需要输入完整的 RPM 名称——可以使用名称开头的几个字符加上星号。确保输入的名称能唯一标识该 RPM 文件。

如果你尝试安装已经安装的 RPM，`rpm` 命令会显示错误。例如，当在系统中尝试安装 `emacs` 时发生这种情况：

```
rpm -i emacs-20*
package emacs-20.2.4 is already installed
error: emacs-20.2.4.rpm cannot be installed
```

如果为了强制 `rpm` 命令安装软件包，请在 `rpm -i` 命令后加上 `-f`：

```
rpm -if emacs-20*
```

### 移除 RPM

如果你发现不需要某个软件包，可能想移除它。可以使用 `rpm -e` 命令轻松地移除。在移除之前，你需要软件包的名称。找到名称的一种好方法是结合使用 `rpm -qa` 和 `grep` 进行搜索。例如，你可以尝试：

```
rpm -qa | grep XFree
XFree86-3.3.1-14
XFree86-75dpi-fonts-3.3.1-14
XFree86-devel-3.3.1-14
XFree86-libs-3.3.1-14
```

在这种情况下，`XFree86-devel` 正是你需要的包名。要移除它，输入：

```
rpm -e XFree86-devel
```

注意，你不需要完整的 RPM 名称；你需要的是名称到版本号之前的部分。`rpm -e` 命令不会移除其他软件包。例如，当我尝试移除 `kernel-headers` 软件包时，收到以下消息：

```
rpm -e kernel-headers
removing these packages would break dependencies:
kernel-headers is needed by glibc-devel-2.0.5-10
kernel-source-2.0.31-7
```

### 升级 RPM

使用 `rpm -U` 命令升级 RPM。你必须提供包含新软件的 RPM 文件名。例如，如果我的系统中安装了 1.2.4 版本的 Apache 服务器，我想升级到 1.2.5 版本，我从 Red Hat 的 FTP 服务器（`http://ftp.redhat.com/pub/redhat/updates/5.0/`）下载 RPM 文件 `apache-1.2.5-1386.rpm`，然后使用以下命令：

```
rpm -U apache-1.2.5-1386.rpm
```

`rpm` 命令通过首先移除旧版本的软件包然后安装新的 RPM 来执行升级。只要可能，你应该升级而不是重新安装。升级会自动保存旧配置文件，从而避免重新安装后配置软件的麻烦。

当你升级内核和包含可用 Linux 内核的内核模块包时，应该使用 `rpm -i` 命令进行安装（而不是使用 `rpm -U` 命令）。这样你就不会覆盖当前的内核。查看“使用 Red Kernel RPM 升级”部分以学习如何从内核 RPM 中提取新内核。

### 验证 RPM

你可能不会经常这样做，但如果你怀疑某个软件包没有安装正确，请使用 `rpm -V` 命令验证软件包。例如，要验证内核包，请输入以下内容：

```
rpm -V kernel
```

这会导致 `rpm` 将软件包中每个文件的大小和其他属性与原始文件进行比较。如果所有内容验证正确，`rpm -V` 命令不会打印任何内容。如果存在任何差异，你将看到差异报告。例如，我修改了 Apache Web 服务器的配置文件。当我验证 `apache` 包时，我看到的是：
