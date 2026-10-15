
```
[ejr@hobbes compression]$ ls -l z*
-rw-r--r-- 1 ejr users 501760 Jul 27 10:22 zipadeedoodah
[ejr@hobbes compression]$ zip -r zipped zipadeedoodah
adding: zipadeedoodah (deflated 52%)
[ejr@hobbes compression]$ ls -l z*
-rw-r--r-- 1 ejr users 501760 Jul 27 10:22 zipadeedoodah
-rw-r--r-- 1 ejr users 239943 Jul 27 10:41 zipped.zip
[ejr@hobbes compression]$
```

### 代码清单 13.12 使用 `zip` 压缩文件，特别是那些你将与 Windows 用户共享的文件。

## 使用 `unzip` 解压压缩文件

你可以使用 `unzip` 解压压缩文件，这很合理，因为你肯定不会用 `unVelcro` 或 `unsnap` 来解压压缩文件（代码清单 13.13）。

### 使用 `unzip` 解压 `zip` 文件的方法：

- 1. `ls -l *.zip`

  在 shell 提示符下，使用 `ls *.zip` 验证 `zip` 文件的名称。

- 2. `unzip zipped.zip`

  输入 `unzip` 和要解压的文件名（带或不带 `.zip` 扩展名）。`unzip` 将解压缩文件并返回到 shell 提示符。

`gunzip` 也理解如何解压缩一些 `.zip` 文件，所以如果你愿意，可以使用 `gunzip` 代替 `unzip`。在 Unix 端，使用你觉得最容易的方法，或者如果你真的不在乎，就用 `gunzip`。如果你向 Windows 用户提供文件，`zip` 更可靠一些，因为它创建的格式更标准。

### 提示

如果你尝试解压一个文件，而要解压的文件或文件已存在，`unzip` 将提示你对每个文件进行判断，是否要覆盖（销毁）现有文件、取消解压过程，或将你要解压的文件重命名为安全名称。

```
[ejr@hobbes compression]$ ls -l *.zip
-rw-rw-r-- 1 ejr users 268156 Jul 23 06:53 folderzip.zip
-rw-rw-r-- 1 ejr users 55124 Jul 23 06:38 fortunes1.zip
-rw-rw-r-- 1 ejr users 53792 Jul 23 06:52 newzip.zip
-rw-r--r-- 1 ejr users 239943 Jul 27 10:41 zipped.zip
[ejr@hobbes compression]$ unzip zipped.zip
Archive: zipped.zip
replace zipadeedoodah.tar? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
 inflating: zipadeedoodah.tar
[ejr@hobbes compression]$
```

代码清单 13.13 `unzip` 让你可以在不意外销毁文件的情况下解压缩文件。

## 处理编码和压缩文件

```
[ejr@hobbes compression]$ ls -l *.Z
-rw-r--r-- 1 ejr users 297207 Jul 27 10:06
    tar.gz
[ejr@hobbes compression]$ zcat tar.gz
    > tar xf -
[ejr@hobbes compression]$ ls -l
-rw-r--r-- 1 ejr users 501760 Jul 27 10:06
    tar.gz
[ejr@hobbes compression]$ ls -ld f*
drwxr-xr-x 2 ejr users 1024 Jul 27
    10:16 feather
[ejr@hobbes compression]$
```

**代码清单 13.15** 在找到压缩文件后，你可以同时解压缩和解包它们，然后使用 `ls -ld`（长格式和目录标志）来检查你的工作。

### 同时解压缩和解包：

- `zcat filename.tar.Z | tar xf -`

  在 shell 提示符下，输入 `zcat` 然后是文件名（与往常一样）并将该输出通过管道传递给 `tar`。在 `tar` 命令和标志后跟一个 `-`，这样 `tar` 就能够将文件保存到预期的名称（**代码清单 13.15**）。

### 同时打包和 `gzip`：

- `tar -cf - Feather | gzip > feather.tar.gz`

  在 shell 提示符下，按通常方式使用 `tar` 命令，但在文件名前添加 `-`（和一个空格），以便输出可以被管道传输。然后，将输出通过管道传递给 `gzip`，并将该输出重定向到一个带有 `.tar` 和 `.gz` 扩展名的文件名，以显示文件已被打包和 `gzip` 压缩（**代码清单 13.16**）。

```
[ejr@hobbes compression]$ ls -ld f*
drwxrwxr-x 2 ejr users 1024 Jul 23 10:56 feather
[ejr@hobbes compression]$ tar -cf - feather | gzip > feather.tar.gz
[ejr@hobbes compression]$ ls -l f*
-rw-r--r-- 1 ejr users 106752 Jul 27 10:54 feather
-rw-r--r-- 1 ejr users 128886 Jul 23 11:45 file1.htm
-rw-r--r-- 1 ejr users 128886 Jul 23 11:45 file2.html
-rw-r--r-- 1 ejr users 686080 Jul 23 10:41 folder.tar
-rw-r--r-- 1 ejr users 268150 Jul 23 06:51 folderzip.zip
-rw-r--r-- 1 ejr users 128886 Jul 23 06:37 fortunes1.txt
-rw-r--r-- 1 ejr users 55124 Jul 23 06:38 fortunes1.zip
[ejr@hobbes compression]$
```

**代码清单 13.16** 你也可以高效地同时打包和 `gzip`。

## 安装自己的软件

如果你使用 Unix 时间够长了，你最终会想要或需要安装新软件。安装软件可能只是安装你从朋友那里得到的 shell 脚本，也可能意味着编译并安装一个从互联网下载的完整程序。

在本章中，我们将探讨在 Unix 系统上安装软件的过程。按提供的顺序完成每个部分，并记住以下几点：

- 在 Windows 或 Macintosh 系统上执行相同操作相比，安装 Unix 软件的过程稍微复杂一些。
- 我们在此使用的示例可能与你为系统选择的程序或脚本所需的确切流程略有不同。
- 你应该向系统管理员咨询有关在系统上可以和不可以安装的内容的具体信息。许多 ISP 会让你安装你想要的软件，但其他人可能有特定限制，甚至可能使你在账户中编译软件变得不可能。
- 如果你没有系统管理员 `root` 访问权限，则安装软件会困难得多。

### 章节内容

- 理解 Unix 软件安装
- 查找 Unix 软件
- 下载、放置和解压缩软件
- 配置软件
- 编译和安装软件

## 理解 Unix 软件安装

在你的 Unix 系统上安装软件时，请记住两点。首先，大多数软件，包括脚本，都依赖于其他程序或脚本在系统内的特定位置可用。例如，一个脚本可能要求 `bash` shell 可用并且位于 `/bin/bash`。或者，一个程序可能期望它位于 `/usr/local/bin`，并且所有用户主目录都在 `/home` 下。因此，在安装过程中，你应特别注意确保所有其他必需的脚本或程序都可用。

其次，程序（但不是脚本）是编译的，这意味着它们从一种可能大多可读的语言（通常称为源代码）中取出，并翻译成计算机可读的文件（通常称为二进制文件）。在软件编译过程中，会内置硬件和操作系统特定的特征（或依赖项）。因此，编译为在特定平台和操作系统上运行的程序无法在其他平台上运行——也就是说，在 Pentium 上 Linux 编译的程序无法在 Alpha 上的 Linux、Pentium 上的 Solaris 或 SPARC 上的 Digital Unix 上运行。

事实上，大多数 Unix 程序是以源代码形式分发，而不是二进制文件，这样你可以在安装时为特定系统编译它们。

### ✓ 提示

- 在开始下一节之前，你可以先回顾第 1 章和第 2 章，了解有关探索你的 Unix 系统的信息，并回顾第 7 章，了解如何查找你使用的操作系统和硬件。

## 查找 Unix 软件

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_311_0.png)
