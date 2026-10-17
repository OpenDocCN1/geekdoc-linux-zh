
```
[root@server1 ~]# ls -l

total 28

drwx---- 3 root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root 27298 Jul 21 08:15 samplefile

-rw-rw-r-- 1 root 540 Jul 21 08:18 samplefile2

[root@server1 ~]# _
```

在解压过程中，如果任何现有文件将被覆盖，`uncompress`命令会提示你确认。为了防止此确认，你可以在`uncompress`命令中使用`-f`选项。

在使用`uncompress`命令时可以省略`.z`扩展名。命令`uncompress -v samplefile samplefile2`将达到与前面输出中显示的命令相同的结果。

此外，`compress`实用是一个过滤命令，可以从标准输入（Standard Input）获取信息并发送到标准输出（Standard Output）。例如，要将`who`命令的输出发送给`compress`工具并将压缩信息保存到名为`file.Z`的文件中，你可以执行以下命令：

```
[server1 ~]# who | compress -v >file.Z

Compression: 17.0%

[server1 ~]#
```

随后你可以使用`zcat`命令显示`file.Z`的内容，并使用`uncompress`命令对其解压，如下输出所示：

```
[server1 ~]# zcat file.Z

root pts/1 Jul 20 19:22 (3.0.0.2)

root tty5 Jul 15 19:03

root pts/1 Jul 17 19:58

[server1]# uncompress -v file.Z

file.Z: -- replaced with file

[server1 ~]#
```

表 11-1 提供了`compress`工具中常用选项的摘要。

| 表 11-1 `compress`工具中常用选项 |
| 选项 | 描述 |
| :--- | :--- |
| -c | 与`uncompress`命令配合使用时，它会将压缩文件的内容显示到标准输出（与`zcat`命令的功能相同）。 |
| -f | 与`compress`命令配合使用时，它可以压缩链接文件。与`uncompress`命令配合使用时，它会在不提示用户的情况下覆盖现有文件。 |
| -r | 指定递归地压缩或解压指定目录内的所有文件。 |
| -v | 在压缩和解压期间显示详细输出（压缩率和文件名）。 |

### 使用 GNU zip

GNU zip是一种 Lempel-Ziv 压缩算法 (`LZ77`)，它与`compress`命令使用的算法略有不同。通常，这种算法产生的压缩效果比`compress`使用的算法更好。GNU zip的平均压缩率为 60–70%。要使用 GNU zip 压缩文件，你可以使用`gzip`命令。

与`compress`类似，除非给出`-f`选项，否则`gzip`命令不会压缩链接文件，可以使用`-r`选项来压缩特定目录中的所有文件。此外，压缩文件的所有者、修改时间和访问时间默认会被保留，且`gzip`命令的`-v`选项可以显示压缩率和文件名。然而，`gzip`默认使用`.gz`扩展名。

要压缩之前的`samplefile`和`samplefile2`并查看压缩率，你可以使用以下命令：

```
[root@server ~]# gzip -v samplefile samplefile2

samplefile: 82.2% -- replaced with samplefile.gz

samplefile2: 65.0% -- replaced with samplefile2.gz
```

由于 GNU 使用与`compress`相同的底层压缩算法，你可以使用`zcat`、`zmore`、`zgrep`命令将 gzip 压缩文件的内容输出到标准输出。同样，`gzip`命令可以通过标准输入接受信息。因此，要将 date 命令的输出压缩到文件 file.gz 并在查看其内容，你可以使用以下命令：

```
[root@server ~]# date | gzip -v file.gz

-6.9%

[root@server ~]# zcat file.gz

Sun Jul 25 19:24:56 EDT 2019

[root@server ~]#
```

要解压上述输出中的 file.gz，你可以使用`gzip`命令的`-d`选项或`gunzip`，如下所示：

```
[root@server ~]# gzip -d file.gz

file.gz: -6.9% -- replaced with file
```

如果指定了`-f`选项，`gunzip`命令允许覆盖现有文件。此外，在解压文件时可以省略`.gz`扩展名，如下所示：

```
[root@server ~]# gunzip -v file.gz
file.gz: -6.9% -- replaced with file
[root@server ~]#
```

## 第11 章 压缩、系统备份与软件安装

### 使用 xz

与`compress`和`gzip`类似，`xz`命令可以使用 Lempel-Ziv 压缩算法 (`LZMA`) 对文件和标准输入进行压缩；然而，由于其实现方式不同，对于大多数文件，压缩率通常比`compress`和`gzip`高（平均高出 60-80%）。此外，`xz`默认使用`.xz`扩展名作为压缩文件的后缀，并实现了与 tail 11-z 所示相同的 gzip 选项，但`-n`和`-r`除外。要解压缩 xz 压缩的文件，可以使用`xz`命令的`-d`选项，或者使用`unxz`命令。

以下示例展示了如何使用`xz`对之前显示的`samplefile`和`sample2`进行最高压缩率的压缩，以及如何使用`unxz`解压相同的文件。

```
[root@server]# ls -1
total 20
dw------ 3 root root 4096 Jul 21 08:15 Desktop
-rw-r---- 1 root root 27298 Jul 21 08:15 samplefile
-rw-rw-- 1 root root 540 Jul 21 08:15 samplefile2
[root@server]# ls -v -9 samplefile samplefile2
sample(1/2)
100 % 4,632 B / 26.7 KiB = 0.170
samplefile2 (2/2)
100 % 264 B / 540 B = 0.489
[root@server]# ls -1
total 28
dw------ 3 root root 4096 Jul 21 08:15 Desktop
-rw-r---- 1 root root 4632 Jul 21 08:15 samplefile.xz
-rw-rw-- 1 root root 264 Jul 21 08:18 samplefile2.xz
[root@server]# unxz -v samplefile.xz samplefile2.xz
samplefile.xz (1/2)
100 % 4,632 B / 26.7 KiB = 0.170
samplefile2.xz (2/2)
100 % 264 B / 540 B = 0.489
[root@server]# ls -1
total 20
dw------ 3 root root 4096 Jul 21 08:15 Desktop
-rw-r---- 1 root root 27298 Jul 21 08:15 samplefile
-rw-rw-- 1 root root 540 Jul 21 08:18 samplefile2
[root@server]# 
```

> 注意

与`uncompress`和`gunzip`不同，使用`xz`命令解压缩文件时，必须包含文件扩展名。

你可以使用`xzcat`、`xzmore`、`xless`或`xgrep`命令将 xz 压缩文件的内容发送到标准输出。

### 使用 zip

`zip`命令是跨平台工具 PKZIP 的 Linux 实现，它最初设计用于将多个文件压缩成单个压缩文件。由于它使用与 zip 相同的 Lempel-Ziv 算法实现来压缩文件和标准输入，因此平均压缩率相似。`zip`命令在压缩时会压缩链接文件，并保留所有者、修改时间和访问时间。虽然 zip 压缩归包没有使用默认文件扩展名，但习惯上通常使用`.zip`。

> 注意

Ubuntu Server 默认未安装 `zip`。要从互联网上的软件仓库安装它，可以以 root 身份运行 `apt-get install zip` 命令。
