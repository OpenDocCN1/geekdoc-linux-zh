

## gunzip

**语法：** `gunzip [-v] file(s)`

要将文件解压缩为其原始形式，请使用 gunzip 命令。gunzip 会尝试解压缩以 `.gz`、`-gz`、`.z`、`-z`、`Z`、`.Z` 或 `.tgz` 为扩展名的文件。

`-v` 选项在解压缩文件时显示详细输出：

```
gunzip -v README.txt.gz
README.txt.gz:   65.0% -- replaced with
README.txt
```

## gzip

**语法：** `gzip [-rv9] file(s)`

gzip 命令是另一个压缩程序。它以拥有最佳压缩比之一而闻名，但代价是速度相当慢。使用 gzip 压缩的文件将被替换为带有 `.gz` 扩展名的文件。

`-9` 选项可产生最佳压缩效果，但会牺牲速度。`-v` 选项是详细模式选项，它会列出每个文件的大小和压缩比。此外，`-r` 选项会递归遍历每个目录，压缩沿途的所有文件。

## rpm

**语法：** `rpm -i[vhqladeUF] [--force] [--nodeps] [--oldpackage] package list`

rpm 是 Red Hat Package Manager（红帽软件包管理器）程序。它允许您管理 RPM 软件包，使安装和卸载软件变得非常容易。

要安装一个名为 `precious-software-1.0.i386.rpm` 的新 RPM 软件包，请运行以下命令：

```
rpm -i precious-software-1.0.i386.rpm
```

您可以通过使用 `-ivh` 代替仅使用 `-i` 选项，使 rpm 的输出更加详细。如果您已经安装了该软件包，出于某种原因想在旧安装的基础上重新安装，请使用 `--force` 选项强制 rpm 执行。

如果您要升级软件包，请使用 `-U` 选项。例如，

```
rpm -Uvh precious-software-2.0.i386.rpm
```

将 **precious-software** 软件包的先前版本升级到 2.0 版。但是，如果您已经安装了更新的版本并想回退到之前的版本，rpm 会检测到这一点并显示一条错误消息，提示已安装的版本比您尝试安装的版本更新。在这种情况下，如果您决定继续操作，请将 `--oldpackage` 选项与 `-U` 选项一起使用，强制 rpm 降级您的软件。

要查找系统上安装的所有可用软件包的列表，请运行以下命令：

```
rpm -qa
```

要查明 sendmail 等程序属于哪个软件包，请运行

```
rpm -q sendmail
```

这将返回用于安装 sendmail 的 RPM 软件包名称。要查明特定文件（如 `/bin/test`）属于哪个软件包，请运行

```
rpm -qf /bin/test
```

这将显示指定文件的软件包名称。如果您有兴趣查找随文件附带的文档，请将 `-d` 选项与 `-qf` 选项一起使用。要列出与程序或软件包（如 sendmail）关联的所有文件，请使用 `-l` 选项，如下所示：

```
rpm -ql sendmail
```

为确保已安装的软件包未以任何方式被修改，请使用 `-V` 选项。例如，要验证所有已安装的软件包是否处于原始状态，请运行以下命令：

```
rpm -Va
```

如果您发现一个或多个软件包可能已被您或他人损坏，此选项将变得非常有用。

要卸载 sendmail 等软件包，请运行以下命令：

```
rpm -e sendmail
```

如果您发现移除某个软件包或程序会破坏其他程序，因为它们依赖于该软件包或其文件，您必须决定是否要破坏这些程序。如果您决定无论如何都要移除该软件包或程序，请将 `--nodeps` 选项与 `-e` 选项一起使用，强制 `rpm` 卸载该软件包。

## tar

**语法：** `tar [c] [x] [v] [z] [f filename] file or directory names`

tar 命令允许您将多个文件和目录归档到单个 TAR 文件中。它还允许您从这种归档文件中提取文件和目录。例如，

```
tar cf source.tar *.c
```

创建一个名为 **source.tar** 的 TAR 文件，该文件将包含当前目录中所有的 C 源文件（以 .c 为扩展名）。

`v` 选项让您可以看到正在归档哪些文件：

```
tar cvf source.tar *.c
```

在下面的示例中，名为 **important_dir** 的目录中的所有文件和子目录都被归档到一个名为 **backup.tar.gz** 的文件中。请注意，由于 `z` 选项，该文件也被压缩了，因此生成的文件应赋予 `.gz` 扩展名。通常，`.tar.gz` 扩展名会被缩写为 `.tgz`。

```
tar cvfz backup.tar.gz important_dir
```

要提取归档文件 **backup.tar**，请运行以下命令：

```
tar xf backup.tar
```

要提取压缩的 tar 文件（如 **backup.tgz** 或 **backup.tar.gz**），请运行

```
tar xzf backup.tgz
```

## uncompress

**语法：** `uncompress [-v] file(s)`

当文件使用 compress 命令压缩后，它就不再是原始形式。要将压缩文件转换回其原始形式，请使用 uncompress 命令。

uncompress 命令期望找到一个带有 `.Z` 扩展名的文件，因此命令行 `uncompress inbox` 等同于 `uncompress inbox.Z`。

`-v` 选项产生详细输出：

```
uncompress -v inbox.Z
inbox.Z: -- replaced with inbox
```

## unzip

**语法：** `unzip file(s)`

unzip 命令解压缩带有 `.zip` 扩展名的文件。这些文件可以用 zip 命令、Phil Katz 的 PKZIP 或任何其他兼容 PKZIP 的程序进行压缩。

## uudecode

**语法：** `uudecode file`

uudecode 命令将 uuencoded 文件转换回其原始形式。uudecode 通过使用 uuencode 命令指定的 *target_name*（目标名称）来创建文件，该名称也可以在 uuencoded 文件的第一行识别。

要将 uuencoded 文件从

```
uudecode a.out.txt
```

转换回其原始形式，可执行文件 *a.out* 将从文本文件 *a.out.txt* 创建。

## uuencode

**语法：** `uuencode in_file target_name`

uuencode 命令通过将二进制文件转换为 ASCII 可打印字符，将其翻译为可读形式。uuencode 的众多用途之一是通过电子邮件传输二进制文件。经过 uuencode 处理的文件显示为一条大的电子邮件消息。接收者可以保存该消息，然后使用 uudecode 命令恢复其二进制形式。

*target_name* 是使用 uudecode 实用程序时创建的二进制文件的名称。

下面的示例将对可执行程序 `a.out` 进行 uuencode 编码。uuencode 创建的目标名称将称为 `b.out`。`a.out` 的 uuencoded 版本将保存在文件 `a.out.txt` 中。

```
uuencode a.out b.out > a.out.txt
```

## zip

**语法：** `zip [-ACDe9] file(s)`

此压缩实用程序以兼容 PKZIP 的格式压缩文件，从而实现与 VMS、MS-DOS、OS/2、Windows NT、Minix、Atari、Macintosh、Amiga 和 Acorn RISC OS 等系统的兼容性。

zip 命令拥有大量由其开关切换的选项。此命令可以创建自解压文件、向 zip 文件添加注释、从归档中移除文件以及对归档进行密码保护。

这些只是 zip 支持的部分功能。如需更详细的说明，请参阅您本地的 man 手册页。

## 文件系统专用命令

本节中的命令用于文件系统的管理。

## dd

**语法：** `dd if=input_file [conv=conversion_type] of=output_file [obs=output_block_size]`

此程序允许您转换文件格式。例如，`dd if=/tmp/uppercase.txt conv=lcase of=/tmp/lowercase.txt` 读取 `/tmp/uppercase.txt` 文件并写入一个名为 `/tmp/lowercase.txt` 的新文件，将所有字符转换为小写 (lcase)。要执行反向操作，请使用 `conv=ucase` 选项。然而，dd 最广泛的用途是将启动镜像文件写入已由 mkfs 创建文件系统的软盘。例如，`dd if=some/boot.img conv=lcase of=/dev/fd0 obs=16k` 以 16K 块的大小将 `/some/boot.img` 文件写入第一个软盘 (`/dev/fd0`)。

## df

**语法：** `df [-k] FileSystem | File`

df 命令汇总系统上已挂载驱动器的可用磁盘空间。硬盘空间是计算机中的重要资源，应仔细监控。硬盘空间管理不善会导致计算机运行缓慢，并引起用户不满。

要查看当前文件系统的磁盘空间摘要，请运行 `df`。

`-k` 选项以 1024K 块为单位显示摘要。

## edquota

要为每个用户分配磁盘配额，请使用 edquota 命令。例如，要为名为 kabis 的用户分配磁盘配额，请运行以下命令：

```
edquota -u kabis
```

这将打开默认文本编辑器（如 vi 或 `$EDITOR` 环境变量中设置的任何编辑器），其内容类似于以下内容：

```
Quotas for user kabis:
/dev/sda5 : blocks in use: 0, limits (soft = 0, hard = 0)
inodes in use: 0, limits (soft = 0, hard = 0)
```
