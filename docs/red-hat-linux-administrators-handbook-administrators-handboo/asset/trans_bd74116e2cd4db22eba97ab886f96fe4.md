
为了确保已安装的软件包未以任何方式被修改，请使用 -V 选项。例如，要验证所有已安装的软件包是否处于原始状态，请运行以下命令：

```
rpm -Va
```

如果发现一个或多个软件包可能已被您或其他人损坏，此选项将非常有用。

要卸载 sendmail 之类的软件包，请运行以下命令：

```
rpm -e sendmail
```

如果发现移除某个软件包或程序会导致其他程序损坏，因为它们依赖于该软件包或其文件，您必须决定是否要破坏这些程序。如果您仍决定移除该软件包或程序，请使用 -e 选项配合 --nodeps 选项，强制 rpm 卸载该软件包。

## tar

语法：

```
tar [c] [x] [v] [z] [f filename] file or directory names
```

tar 命令允许您将多个文件和目录归档到单个 TAR 文件中。它还允许您从此类归档文件中提取文件和目录。例如，

```
tar cf source.tar *.c
```

创建一个名为 source.tar 的 TAR 文件，其中将包含当前目录下所有 C 源码文件（以 .c 为扩展名）。

v 选项可让您查看正在归档的文件：

```
tar cvf source.tar *.c
```

在以下示例中，名为 important_dir 的目录下的所有文件和子目录都被归档到名为 backup.tar.gz 的文件中。请注意，由于 z 选项，该文件同时被压缩，因此结果文件应使用 .gz 扩展名。通常，.tar.gz 扩展名会被缩短为 .tgz。

```
tar cvzf backup.tar.gz important_dir
```

要提取归档文件 backup.tar，请运行以下命令：

```
tar xf backup.tar
```

要提取压缩的 tar 文件（如 backup.tgz 或 backup.tar.gz），请运行

```
tar xzf backup.tgz
```

## uncompress

语法：

```
uncompress [-v] file(s)
```

当使用 compress 命令压缩文件时，它不再处于原始形式。要将压缩文件恢复为原始形式，请使用 uncompress 命令。

uncompress 命令期望找到带有 .Z 扩展名的文件，因此命令行“uncompress inbox”等同于“uncompress inbox.Z。”

-v 选项会产生详细输出：

```
uncompress -v inbox.Z
inbox.Z: -- replaced with inbox
```

## unzip

语法：

```
unzip file(s)
```

unzip 命令解压缩具有 .zip 扩展名的文件。这些文件可以用 unzip 命令、Phil Katz's PKZIP 或任何其他 PKZIP 兼容程序进行压缩。

## uudecode

语法：

```
uudecode file
```

uudecode 命令将 uuencode 编码的文件转换回其原始形式。uudecode 使用 uuencode 命令指定的 "target_name" 创建文件，该名称也可以在 uuencode 编码文件的第一行中识别。

要将 uuencode 编码的文件从

```
uudecode a.out.txt
```

转换回其原始形式，可执行文件 a.out 将从文本文件 a.out.txt 创建。

## uuencode

语法：

```
uuencode in_file target_name
```

uuencode 命令通过将二进制文件转换为 ASCII 可打印字符，将二进制文件转换为可读形式。uuencode 的众多用途之一是通过电子邮件传输二进制文件。经过 uuencode 的文件会显示为一封大型电子邮件。收件人可以保存该消息并使用 uudecode 命令检索其二进制形式。

target_name 是使用 uuencode 工具时创建的二进制文件的名称。

以下示例将对可执行程序 a.out 进行 uuencode。uudecode 创建的目标名称将称为 b.out。a.out 的 uuencode 版本将保存在文件 a.out.txt 中。

```
uuencode a.out b.out > a.out.txt
```

## zip

语法：

```
zip [-ACde9] file(s)
```

此压缩实用程序以 PKZIP 兼容格式压缩文件，从而实现与 VMS、MS-DOS、OS/2、Windows NT、Minix、Atari、Macintosh、Amiga 和 Acorn RISC OS 等系统的兼容性。

zip 命令有一系列可通过其开关切换的选项。该命令可以创建自解压文件，为 zip 文件添加注释，从归档中删除文件，并对归档进行密码保护。

这些是 zip 支持的其中一些功能。有关更详细的描述，请参阅本地手册页。

## 文件系统特定命令

本节中的命令用于文件系统的管理。

### dd

语法：

```
dd if=input file [conv=conversion type] of=output file [obs=output block size]
```

此程序允许您转换文件格式。例如，

```
dd if=/tmp/uppercase.txt conv=lcase of=/tmp/lowercase.txt
```

读取 /tmp/uppercase.txt 文件并写入一个名为 /tmp/lowercase.txt 的新文件，将所有字符转换为小写（lcase）。要执行相反操作，您可以使用 conv=ucase 选项。然而，dd 最广泛的用途是将引导映像文件写入已由 mkfs 创建文件系统的软盘。例如，

```
dd if=/some/boot.img conv=lcase of=/dev/fd0 obs=16k
```

以 16K 块的形式将 /some/boot.image 文件写入第一张软盘（/dev/fd0）。

### df

语法：

```
df [-k] FileSystem | File
```

df 命令汇总系统上已挂载驱动器的可用磁盘空间。硬盘空间是计算机中的重要资源，应仔细监控。硬盘空间管理不当可能导致计算机运行缓慢，并导致一些用户不满意。

要查看当前文件系统的磁盘空间摘要，请运行

```
df .
```

-k 选项改为以 1024 块显示摘要。

### edquota

要为每个用户分配磁盘配额，请使用 edquota 命令。例如，要为名为 kabir 的用户分配磁盘配额，请运行以下命令：

```
edquota -u kabir
```

这将打开默认文本编辑器（如 vi 或 $EDITOR 环境变量中设置的内容），内容类似于以下内容：

```
Quotas for user kabir:
/dev/sda5: blocks in use: 0, limits (soft = 0, hard = 0)
    inodes in use: 0, limits (soft = 0, hard = 0)
```

在这里，用户 kabir 在磁盘分区 /dev/sda5（在 usrquota 控制下）上迄今已使用 0 块（以 K 为单位），并且限制（软限制或硬限制）尚未设置。同样，该用户尚未拥有任何文件（inode），并且尚未设置任何限制（软限制或硬限制）。

如您所见，您可以同时设置用户可消耗的空间量（以块为单位）的限制，并控制用户可以拥有的文件数量。软限制指定用户在文件系统上可以拥有的最大磁盘空间（块）或文件（inode）数量。硬限制是用户可以拥有的磁盘空间（块）或文件（inode）的绝对数量。

例如，假设您希望允许用户 kabir 的磁盘空间软限制为 1MB（1,024K），硬限制为 4MB（4,096K）。此外，假设您希望允许该用户的文件/目录（inode）软限制为 128，硬限制为 512。您可以使用 edquota -u kabir 按如下方式设置配额限制：

```
Quotas for user kabir:
/dev/sda5: blocks in use: 0, limits (soft = 1024, hard = 4096)
    inodes in use: 0, limits (soft = 128, hard = 512)
```

保存配置后，用户将无法超过硬限制。如果用户尝试超过这两个（磁盘空间和 inode 计数）限制中的任何一个，将显示错误消息。例如，在以下示例中，用户 kabir 尝试在 /home 中创建新目录，但该配额的配额限制已被超过，因此显示错误消息：

```
{kabir@picasso /home}$ mkdir eat_space
mkdir: cannot make directory 'eat_space': Disk quota exceeded
```

如果您有许多用户需要分配配额，以上方法可能非常耗时。为了帮助您处理这种情况，edquota 程序包含 -p 原型用户选项，允许您将原型用户的磁盘配额配置复制给其他用户。例如，假设您希望将刚刚为用户 kabir 创建的配额配置用于另外三个用户（sheila、jennifer 和 mrfrog）。您可以运行以下命令：

```
edquota -p kabir -u sheila jennifer mrfrog
```

现在，这三个用户都具有与 kabir 相同的配额配置。将组置于磁盘配额控制下非常相似。配置组配额要求的 edquota 语法如下：

```
edquota -g group name
```

要强制执行用户或组配额的软限制，您需要使用 edquota -t 命令配置宽限期。当您运行此命令时，编辑器将显示类似于以下内容的内容：
