
在这里，我们使用 `-o /dev/stdout` 将 `udecode` 的输出发送到标准输出，然后将 `udecode` 命令的输出通过管道给 `gunzip`，最后将 `gunzip` 的输出重定向到 `home` 文件。呼！详情请参见代码列表 13.14。

```
[ejr@hobbes compression]$ ls -l h*
-rw-rw-- 1 ejr users 73978 Jul 23 11:15 home.gz.uue
-rw-r--r- 1 ejr users 177607 Jul 27 09:34 house.home
[ejr@hobbes compression]$ udecode -o /dev/stdout home.gz.uue | gunzip > home
[ejr@hobbes compression]$ ls -l h*
-rw-r--r- 1 ejr users 128886 Jul 27 10:48 home
-rw-rw-- 1 ejr users 73978 Jul 23 11:15 home.gz.uue
-rw-r--r- 1 ejr users 177607 Jul 27 09:34 house.home
[ejr@hobbes compression]$
```

### 要同时进行解压缩和 untar：

- `zcat filename.tar | tar -xf -`

在 shell 提示符下

```
[ejr@hobbes compression]$ ls -l *.*
-rw-r--r- 1 ejr users 297027 Jul 27 10:06 labrea.tar.Z
[ejr@hobbes compression]$ zcat labrea.tar.Z | tar -xf -
[ejr@hobbes compression]$ ls -l *
-rw-r--r- 1 ejr users 501760 Jul 27 10:06 labrea.tar
[ejr@hobbes compression]$ ls -ld *
drwx-xr-x 2 ejr users 1024 Jul 27 10:16 labrea.tar
[ejr@hobbes compression]$
```

### 要同时进行 `tar` 和 `gzip`：

- `tar -cf - | gzip > feather.tar.gz`

在 shell 提示符下，像往一样输入命令，但在文件名之前添加 `- `（空格），这样输出就可以通过管道。将输出交给 `gzip`，并将 `.tar` 和 `.gz` 扩展名的输出重定向到文件名，以显示文件已经过 `tar` 和 `gzip` 处理（**代码列表 13.16**）。

代码列表 13.15：找到压缩文件后，你可以一次性对它们进行解压缩和 untar，并使用 `ls -ld`（详细和目录标志）来检查你的工作结果。

```
[ejr@hobbes compression]$ ls -ld F*
drwxrxr-x 2 ejr users 1024 Jul 23 10:56 Feather
[ejr@hobbes compression]$ tar -cf - | gzip > feather.tar.gz
[ejr@hobbes compression]$ ls -l *
-rw-r--r- 1 ejr users 128886 Jul 27 10:48 home
-rw-rw-- 1 ejr users 73978 Jul 23 11:15 home.gz.uue
-rw-r--r- 1 ejr users 177607 Jul 27 09:34 house.home
[ejr@hobbes compression]$
```

# 第 14 章

## 下载、放置和解压软件

一旦你找到了想要安装的软件，下一步就是下载它，将它放在合适的位置，然后对其进行解压（**代码列表 14.1**）。这个过程包含了你已经在从本书的其他部分学过的任务，因此我们在这里不再详细介绍这些内容。对于本节，我们假设你已经知道自己想要下载什么，以及可以在何处找到它们。在示例中，我们正在使用来自 `www.yencode.org` 网站的链接下载 `yencode` 的最新版本。

```
jdoe /home/jdoe $ mv yencode-0.46.tar.gz ~/src/
jdoe /home/jdoe $ cd ~/src
jdoe /home/jdoe/src $ tar -xzf yencode-0.46.tar.gz
jdoe /home/jdoe/src $ cd yencode-0.46
jdoe /home/jdoe/src/yencode-0.46 $
```

**代码列表 14.1** 下载软件并为安装做准备的过程非常直接。

**要下载、放置和解压软件：**

1. `links www.yencode.org`

   使用 `links` 连接到软件归档、网站或你从中下载任何内容。

2. 浏览到正确的位置。

   继续吧。我们会等的。

3. 当文件链接被高亮时，按 `Enter` 键选择要下载的文件。

   确认你要下载该文件。

4. [image]

   传输完成后退出 `links` 程序。

```
mv yencode-0.46.tar.gz ~/src/
```

将归档文件移动到家目录下的 `src` 子目录（如果有必要，请先创建该目录）。你可以使用任何目录，但使用 `src` 目录是标准做法。

```
cd ~/src
```

进入 `src` 目录。

```
tar -xzf rpm-2.5.1.tar.gz
```

使用 `tar` 解压并解包（untar）源码归档。

```
cd yencode-0.46
```

进入你的新目录，准备好编译和安装。呼！关于该过程的大部分内容，请参见代码列表 14.1。

- *提示*：你也可以使用 `wget` 或 `ftp` 下载你的软件，如果你确切知道想要下载的软件的 URL，这可能会更简单。

## 配置软件

在你下载并解压新软件后，你必须对其进行配置和微调以适应你的系统。通常情况下，你将进行的更改包括：

- 调整路径名称（例如，安装到 `/home/yourid/bin` 而不是 `/usr/local/bin`，因为你可能无法在后者安装软件）。

- 指定你正在运行的是哪种 Unix 系统。

- 插入你的电子邮件地址和类似的数据。

- 在两个或三个特定的系统设置中选择一个。每个系统应该选择哪一个，在你将使用的文件中会有明确的标记。

如果你正在安装一个将被编译的程序，你的步骤将与这些非常相似。如果你正在安装一个脚本，步骤可能会有所不同，但请继续阅读这些步骤，因为脚本和程序在修改内容的原则上是相同的。

你具体需要做哪些更改（在程序或脚本中）几乎总是记录在 `INSTALL` 文件中（或者如果软件没有附带 `INSTALL` 文件，则在 `README` 中——在 `Makefile` 中（针对程序）或你将运行的实际 `.pl` 或 `.sh` 文件中（针对脚本）。

**代码列表 14.2**。所以请务必阅读这些文件！本节的步骤假设你从下载的解压和解包文件的主目录开始。

```
jdoe /home/jdoe/src/yencode-0.46 $ README

这是 yencode，一个用于 Usenet "yEnc" 格式的编码器/解码包，根据 GNU 通用许可证许可。

### 特性

- 适用于所有 Unix 操作系统的可移植程序。
- 编码器可以输出任何大小的单部分或多部分编码归档。
- 智能解码器可以处理多个文件，包括乱序指定或文件名异常的文件。
- 易于使用的 Usenet 发布软件支持对单个文件或文件组进行单行发布，根据需要还可以创建 SFV/FRC 校验和文件。
- 可选扫描模式：在指定目录或递归地自动定位并解码单部分或多部分编码归档。
- 完全符合 yEnc 规范的所有版本（当前为 v1, v2, v3）。
- 正确实现了 CRC 值，包括多部分归档每个部分的 pcrc32，以及多部分归档最后一个部分的 crc32。
- 由 GNU gettext 提供全面的国际化（多语言）支持。
```

有关 yenc 的信息，请访问 `http://www.yenc.org/`。

无法访问很多系统类型。如果你在编译或安装此程序时遇到问题，请给我发邮件（或发送补丁！），我会尝试添加对你系统的支持。此版本已在 FreeBSD 和 Linux 上测试过。

国际化支持目前支持英语，因为我是一个无知的美国人。欢迎翻译。

此程序应被视为“alpha 质量”。它尚未在实际应用中经过广泛测试。请通过电子邮件向我的错误报告、评论和建议。将建议和错误报告发送到 `<bboy@net>`。
