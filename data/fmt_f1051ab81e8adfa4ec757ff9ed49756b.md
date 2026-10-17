
`lrwxr-xr-x 1 root root 11 Sep 25 10:46 linux -> linux-2.2.9`

`drwrf-xr-x 3 root root 1024 Sep 25 10:46 linux-2.2.9`

在前面的示例中，我在 `/boot` 目录下复制了一份内核二进制文件 `vmlinux` 并将其命名为 `vmlinux.safe`。我复制并粘贴了内核的原始 LILO 启动项，并修改了 `image` 和 `label` 行以反映原始内核——即安全的 Linux 内核。如果你想在 `label` 名称中留有空格，需要将其放在引号中。当你安装新内核时，它会覆盖 `/boot/vmlinux` 并成为默认启动镜像，即 `default=linux`。如果你发现启动新内核时出现问题，可以在 LILO 提示符处输入你原始内核的 `label`。这会启动你的原始内核，并让你能够修复新内核的任何问题。最后，你必须记得运行 `/sbin/lilo` 以让 LILO 读取你的更改。

```
[root@sloth [etc]# /sbin/lilo

Added linux *

Added safe-linux

Added dos
```

## 安装内核源码

在备份了内核源码和二进制文件后，你就可以放心地安装新内核了，并相信你可以从任何不幸的意外或其他意外之外的问题中恢复。正如我之前解释的，你可以从多个位置获取源码。我涵盖了你可以获取内核源码的三种流行格式以及如何安装它们。

### RPM

内核源码通常以两个 RPM 文件的形式提供。第一个 RPM 文件包含源码所需的所有头文件。第二个 RPM 文件包含实际的源代码。你可以像第四章“升级到最新最强大的版本”中描述的那样使用 `TurboPkg`。你也可以从多个地方下载相应的 RPM 文件。对于本示例，我从 TurboLinux FTP 站点下载了 APM 版本内核的源码和头文件 RPM。作为参考，以下是我获取这些 RPM 的步骤简要总结。

```
ncftp ftp.turbolinux.com

>cd /pub/turbolinux/tlw-6.0-updates/kernels/APM/

>ls

kernel-headers-2.2.12.apm-8.1386.rpm

kernel-source-2.2.12.apm-8.1386.rpm

>get kernel-headers-2.2.12.apm-8.1386.rpm

>get kernel-source-2.2.12.apm-8.1386.rpm
```

获取 RPM 文件后，你必须安装它们。按照指示顺序输入以下命令：

```
rpm -Uvh kernel-headers-2.2.12.apm-8.i386.rpm

rpm -Uvh kernel-source-2.2.12.apm-8.i386.rpm
```

这会将头文件和源码安装在 `/usr/src/linux`。

> 注意：如果你使用 `TurboPkg` 升级系统并选择了内核头文件和源码，它会为你下载并安装这些 RPM 文件。

### Tar 包 (Tar Ball)

“tar 包”一词通常用于指代 tar 档并压缩的文件或 tar 文件。`tar` 是一个工具，它可以提取许多文件和目录并将它们全部放入一个名为 tar 文件的单个文件中。tar 文件以 `.tar` 扩展名结尾。例如：

```
> tar -cvf myTarFile.tar tmp/

tmp/kernel-headers-2.2.12.apm-8.i386.rpm

tmp/kernel-source-2.2.12.apm-8.i386.rpm
```

上述命令将 `tmp/` 目录的内容放入一个名为 `myTarFile.tar` 的单个文件中。要从 tar 文件提取文件和目录，你必须对其进行解压（untar）。

```
> tar -xvf myTarFile.tar

tmp/

tmp/kernel-headers-2.2.12.apm-8.i386.rpm

tmp/kernel-source-2.2.12.apm-8.i386.rpm
```

在这个示例中，tar 文件 `myTarFile.tar` 的内容被提取到当前工作目录。如果文件不存在，则会创建。如果文件已存在，则会被覆盖，因此请注意你解压 tar 包的位置。

> 提示：在解包之前检查 tar 文件是一个良好的习惯。大多数 tar 包的内容都包含在一个唯一的目录中，因此当你提取内容时，它们不会覆盖或不必要的弄乱当前工作目录。如果文件不在它们自己的目录中，你可能希望创建一个并在新目录中提取 tar 包，以保持 tar 包的内容。你可以使用 `-t` 选项检查 tar 包的内容。

```
> tar -tvf myTarFile.tar
```

此外，tar 文件经常被压缩以节省磁盘空间。许多工具都能压缩文件。最常用的是 `compress`、`gzip` 或 `bzip` 工具来压缩文件。文件以指示所用压缩方法的扩展名结尾——`.gz` 用于 `zip`，`.bz` 用于 `bzip`。当 tar 文件被压缩时，`gzip` 的扩展名与 `.tar` 扩展名结合形成 `.tgz`。GNU `tar` 命令能够使用 `-Z` 和 `-z` 选项分别解压 `Z` 和 `.gz` tar 包。你需要使用 `bunzip` 工具解压 bzip 文件。`.bz` 扩展名会给你留下一个 `.tar` 扩展名。然后你可以像往常一样解压文件。

内核源码 tar 包是一个包含源码的大型文件。你可以从多个位置获取内核 tar 包。通过浏览 `http://www.kernel.org` 网站，我获取了最新的内核源码：

`ftp://ftp.kernel.org/pub/linux/kernel/v2.2/linux-2.2.13.tar.gz`

获取 tar 包后，将其移动到 `/usr/src`。检查其内容以查看文件将如何提取。

```
[root@sloth src]$$ tar -ztvf linux-2.2.13.tar.gz | more

drwx-xr-x torvalds/eng 0 1999-10-19 20:16 linux/

r-rw--r--r torvalds/eng 13427 1999-10-19 20:16 Makefile

drwx-xr-x torvalds/eng 0 1999-10-19 20:14 linux/fs/

r-rw--r--r torvalds/eng 6155 1999-11-19 20:16 linux/fs
```
