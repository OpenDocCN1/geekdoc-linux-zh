
```bash
$ md5sum ubuntu.iso
cace6ea9dde8dc158174e345aa0e3fae ubuntu.iso
```

使用 `md5sum` 命令显示大文件的 md5 哈希值

`md5sum` 命令计算指定文件的 MD5 和（有时也称为 *哈希值*）。它与之前讨论的 `cksum` 命令类似，但计算更密集。MD5 哈希值相当于数字指纹，不太可能像 `cksum` 哈希值（在某些罕见情况下）那样被重复或填充。

上述示例显示了从互联网下载的 Ubuntu Linux CD 镜像的 MD5 哈希值。可以将生成的 MD5 哈希值与下载站点的哈希值进行比较，以确保下载无误。

**注意** *在 BSD 系统上，使用 `md5` 命令代替 `md5sum`。*

**常用示例**：

- `md5sum [FILE]`：计算指定文件的 MD5 和
- `md5sum -c [FILE]`：比较指定文件中的 MD5 和

### ln

**用途**：创建文件或目录的链接（快捷方式）。

**用法语法**：`ln [OPTIONS] [TARGET] [LINK]`

```bash
$ ln -s TheSourceFile ThisIsTheLink
$ ls -l
-rw-r--r--  1 nick nick  14 2009-05-23 10:16 TheSourceFile
lrwxrwxwx  1 nick nick  13 2009-05-23 10:18 ThisIsTheLink -> TheSourceFile
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_52_0.png)

`ln` 命令创建文件或目录的链接。链接是命令行中的快捷方式。在上面的示例中，创建了指向名为 `TheSourceFile` 的文件的链接。请注意，上面示例中的链接在权限部分有一个 `l` 前缀。这表明该文件是一个链接。

在大多数系统上，`ln` 命令的默认操作创建的是所谓的硬链接。硬链接有两个主要限制：

- 硬链接不能指向目录
- 硬链接不能跨越多个文件系统/磁盘

如今，符号链接被更广泛地用于克服硬链接的不足之处。当使用 `-s` 选项运行 `ln` 命令时，会创建符号链接。这是创建链接的推荐方式，因为它不会受到硬链接相同限制的影响。

> 注意：编辑符号链接文件等同于编辑源文件，但删除符号链接不会删除源文件。

常用示例：

| 命令 | 描述 |
| :--- | :--- |
| `ln [SOURCE] [TARGET]` | 创建指向指定目标的硬链接 |
| `ln -s [SOURCE] [TARGET]` | 创建指向指定目标的符号链接 |

### alias

**用途**：创建命令行别名。

**用法语法**：`alias [OPTIONS] [COMMAND]`

```bash
$ alias rm='rm -i'
$ rm TestFile
rm: remove regular empty file 'TestFile'? y
创建命令别名
```

`alias` 命令创建命令行别名。这允许您将冗长的命令字符串简化为简单的形式。在上面的示例中，`rm` 命令被别名为 `rm -i`，因此每次执行 `rm` 命令时，`-i` 选项都会自动包含在内（无需手动输入）。

不带参数执行 `alias` 将显示当前定义的所有别名，如下一个示例所示。

```bash
$ alias
alias cp='cp -i'
alias l='ls -l'
alias rm='rm -i'
显示所有定义的别名
```

> **提示**
> 注销时会丢失别名。`unalias` 命令可用于删除别名，而无需注销。要使别名永久保存，必须将其添加到用户主目录中的 `/etc/profile` 或 `~/.profile` 文件里。

**常用示例**：

| 命令 | 描述 |
| :--- | :--- |
| `alias` | 显示已定义的别名 |
| `alias [NAME]='[COMMAND]'` | 为指定命令创建别名 |

### gzip / gunzip

**用途**：压缩/解压缩文件。

**用法语法**：`gzip [OPTIONS] [FILE]`

```bash
# ls -lh BigFile
-rw-r--r-- 1 root root 3.0M 2010-05-20 14:02 BigFile
# gzip BigFile
# ls -lh BigFile.gz
-rw-r--r-- 1 root root 433K 2010-05-20 14:02 BigFile.gz
使用 gzip 压缩文件
```

`gzip` 是大多数 Linux 和 BSD 系统上的一种简单压缩工具。在上面的示例中，`gzip` 用于通过将其压缩为 `.gz` 归档来减小 `BigFile` 文件的大小。

`gunzip`（或 `gzip` `-d`）命令用于解压缩 `gzip` 归档，如下一个示例所示。

**用法语法**：`gunzip [OPTIONS] [FILE]`

```bash
$ gunzip BigFile.gz
# ls -lh BigFile
-rw-r--r-- 1 root root 3.0M 2010-05-20 14:02 BigFile
使用 gunzip 解压缩文件
```

> 在较旧的 Unix 系统上，使用 `compress` 和 `uncompress` 命令代替 `gzip` 和 `gunzip`。这些系统上的压缩文件通常具有 `.Z` 文件扩展名，而不是 `.gz`。

常用示例：

| 命令 | 描述 |
| :--- | :--- |
| `gzip [FILE]` | 压缩指定文件 |
| `gzip --fast [FILE]` | 使用最快方法压缩指定文件 |
| `gzip --best [FILE]` | 使用最高压缩级别压缩文件 |
| `gzip -tv [ARCHIVE]` | 测试指定归档是否有错误 |
| `gzip -l [ARCHIVE]` | 显示关于指定归档文件的信息 |
| `gunzip [ARCHIVE]` | 解压缩指定归档 |
| `gzip -d [ARCHIVE]` | 解压缩指定归档 |

### split

**用途**：将大文件拆分为多个片段。

**用法语法**：`split [OPTIONS] [FILE] [OUTPUT]`

```bash
$ ls -l ubuntu.iso
-rw-r--r-- 1 nick nick 671686656 2009-10-27 12:07 ubuntu-9.10.iso
$ split -b 100M ubuntu.iso ubuntu.iso.
$ ls -lh ubuntu*
-rw-r--r-- 1 nick nick 641M 2009-10-27 12:07 ubuntu-9.10.iso
-rw-r--r-- 1 nick nick 100M 2010-04-11 11:44 ubuntu.iso.00
-rw-r--r-- 1 nick nick 100M 2010-04-11 11:44 ubuntu.iso.01
-rw-r--r-- 1 nick nick 100M 2010-04-11 11:44 ubuntu.iso.02
-rw-r--r-- 1 nick nick 100M 2010-04-11 11:44 ubuntu.iso.03
-rw-r--r-- 1 nick nick 100M 2010-04-11 11:44 ubuntu.iso.04
-rw-r--r-- 1 nick nick 100M 2010-04-11 11:44 ubuntu.iso.05
-rw-r--r-- 1 nick nick 41M 2010-04-11 11:44 ubuntu.iso.06

使用 split 命令将大文件拆分为多个片段
```

`split` 命令将大文件拆分为多个片段。上面的示例演示了如何将大文件 `ubuntu.iso` 拆分为几个 100MB 的片段（如 `-b 100M` 参数所示）。在这个示例中，`split` 命令将创建所需数量的 100MB 文件，并带有递增的扩展名。

> **注意** *创建拆分文件时，原始文件保留在原处。*

`cat` 命令（第 68 页有讨论）可用于重新组合拆分后的文件，如下一个示例所示。

```bash
$ cat ubuntu.iso.* > ubuntu-joined.iso
$ ls -lh *.iso
-rw-r--r-- 1 nick nick 641M 2009-10-27 12:07 ubuntu-9.10.iso
-rw-r--r-- 1 nick nick 641M 2010-04-11 11:47 ubuntu-joined.iso

使用 cat 命令组合拆分文件
```

> **提示** *您可以使用 `cksum` 或 `md5sum` 命令验证组合后的文件是否与原始文件相同。*

常用示例：
