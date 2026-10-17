
`-rw-r--r-- 1 emma 156K 2 08:08 bigfile-xz1.xz`

`-rw-r--r-- 1 emma 143K 2 08:08 bigfile-xz9`

并不是每次使用文件时都对其解压缩。压缩工具通常带有用于读取文本文件的工具特殊版本。例如，`gzip`拥有`cat`、`grep`、`diff`、`less`、`more`以及其他几个版本。对于`gzip`，这些工具以`z`为前缀，而`bzip2`使用前缀`b`，`xz`使用`x`。以下是使用`zcat`读取并显示用`gzip`压缩文件的示例：

```bash
$ cp /etc/hosts ./
$ gzip hosts
$ zcat hosts.gz
127.0.0.1 localhost
```

```bash
# 以下行对于支持 IPv6 的主机是理想的
::1 localhost ip6-local ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-routers
```

版本: 2023-04-14 | 基于 CC BY-NC-ND 4.0 许可 | learning.lpi.org | 173

### 归档工具

`tar`程序可能是 Linux 上使用最广泛的归档工具。如果你好奇它为什么叫这个名字，它是 "tape archive"磁带归档）的缩写。用`tar`创建的文件通常被称为 tar ball（压缩包）。以源码形式分发的应用程序非常常见使用`tar`格式。

Linux 发行版带的 GNU 版本的`tar`有很多选项。本课程将涵盖最常用的选项。

让我们首先创建一个用于压缩文件的归档：

```bash
$ cd ~/linux_essentials-3.1
$ tar cf archiving/3.1.tar compression
```

`c`选项指示`tar`创建一个新的归档文件，`f`选项是要创建的文件名。紧跟选项后的参数将是要操作的文件名。其余参数是你想从文件中添加、列表或提取的任何文件或目录。在示例中，我们正在将`compression`目录及其所有内容添加到归档。

要查看`tar`包的内容，使用`tar`的`t`选项：

```bash
$ tar -tf 3.1.tar
compression/
compression/bigfile-xz.1
compression/bigfile-gz9.gz
compression/hosts.gz
compression/big2
compression/bigfile
compression/bigfile-gz1.gz
compression/bigfile-xz9.xz
compression/big3
compression/big4
```

注意选项前面带有`-`。与大多数程序不同，在`tar`中指定选项时不需要`-`，尽管使用它也不会产生任何副作用。

现在我们来提取文件：

```bash
$ cd ~/linux_essentials-3.1/archiving
$ ls
3.1.tar
$ tar xf 3.1.tar
$ ls
3.1.tar compression
```

假设你只需要归包中的一个文件。如果是这样，你可以在归包文件名之后指定它。如果有需要，你可以指定多个文件：

```bash
$ cd ~/linux_essentials-3.1/archiving
$ rm -rf compression
$ ls
3.1.tar
$ tar xvf 3.1.tar compression/hosts.gz
compression/
compression/bigfile-xz1.xz
compression/bigfile-gz9.gz
compression/hosts.gz
compression/bigfile2
compression/bigfile
compression/bigfile-gz1.gz
compression/bigfile-xz9.xz
compression/bigfile3
compression/bigfile4
$ ls
3.1.tar compression
$ ls compression
hosts.gz
```

除了绝对路径（以`/`开头的路径）外，`tar`文件在创建时会保留文件的整个路径。由于文件`3.1.tar`是用单个目录创建的，解压时，该目录将相对于你的当前工作目录创建。另一个例子可以说明这一点：

```bash
$ cd ~/linux_essentials-3.1/archiving
$ rm -rf compression
$ cd ../compression
$ tar cf ..../tar/3.1-nodir.tar *
```

```bash
$ cd ..//archiving
$ mkdir untar
$ cd untar
$ tar -xf ../3.1-nodir.tar
$ ls
```

> 提示：如果你在`tar`文件中使用绝对路径，必须使用`P`选项。请注意，这可能会覆盖重要文件并可能在你的系统上引起错误。

`tar`程序还可以动态对归档进行压缩和解压。`tar`通过调用在本节稍早讨论的压缩工具之一来实现这一点。这只需要添加与压缩算法相对应的选项即可。最常用的分别是`j`、`z`，以及用于`bzip2`、`xz`和`gzip`的`x`选项。以下是使用上述算法的示例：

```bash
$ cd ~/linux_essentials-3.1/compression
$ ls
bigfile bigfile3 bigfile-gz.1 bigfile-xz.1 hosts.gz
bigfile2 bigfile4 bigfile-gz.9 bigfile-xz.99
$ tar -czf gip.tar.gz bigfile2 bigfile3
$ tar -cjf bzip2.tar.bz bigfile2 bigfile3 bigfile3
$ tar -cf xz.tar.xz bigfile2 bigfile3
$ ls -l | grep tar
-rw-r--r-- 1 emma 450202 Jun 27 05:56 bzip2.tar.bz
-rw-r--r-- 1 emma 548656 Jun 27 05:56 gzip.tar.gz
-rw-r--r-- 1 emma 147068 Jun 27 05:56 xz.tar.xz
```

注意`.tar`文件的尺寸不同。这说明它们已成功压缩。如果你创建了压缩压缩的`.tar`归档，应该始终添加一个表示你所用算法的文件扩展名。对于`xz`、`bzip2`和`gzip`，它们分别是`.xz`、`.bz`和`.gz`。有时也会使用缩短的扩展名如`.tar`。

可以对已经压缩的归档进行解压缩。使用`u`选项进行解压缩。如果你尝试添加一个`u`归档，将得到错误。

```bash
$ cd ~/linux_essentials-3.1/compression
$ ls
bigfile bigfile3 bigfile-gz.1 bigfile-xz.1 bzip2.tar.bz hosts.gz
bigfile2 bigfile4 bigfile-gz.9 bigfile-xz.99 gzip.tar.gz xz.tar.xz
$ tar cf plain.tar bigfile
$ tar tf plain.tar
bigfile
bigfile2
bigfile3
$ tar uf plain.tar bigfile4
$ tar tf plain.tar
bigfile
bigfile2
bigfile3
bigfile4
$ tar uzf gzip.tar bigfile4
tar: Cannot update compressed archives
使用 'tar --help' 或 'tar --usage' 获取更多信息。
```

## ZIP 文件

Windows 通常没有处理`tar`包的 Linux 系统中的许多压缩工具。如果你需要与 Windows 系统交互，请使用 ZIP 文件。ZIP 文件类似于压缩的`tar`归档文件。

`zip`和`unzip`程序用于在 Linux 系统上操作 ZIP 文件。下面的示例将说明这一点。首先创建一个文件组：

```bash
$ cd ~/linux_essentials-3.1
$ mkdir zip
$ cd zip
$ mkdir dir
$ touch dir/file1 dir/file2
```

现在使用`zip`将这些文件打包成 ZIP 文件：

```bash
$ zip -r zipfile.zip dir
adding: dir/ (stored%)
adding: dir/file1 (stored%)
adding: dir/file2 (stored%)
$ rm -rf dir
```

最后，再次解压 ZIP 文件：
