

### 问题 14

以下哪项可用于跨文件系统链接文件？

- a. 硬链接
- b. 符号链接
- c. 字符特殊文件
- d. 门（Door）

答案 b 正确。符号链接可用于跨文件系统链接文件。硬链接基于文件在当前磁盘上的位置来引用文件，因此无法引用另一磁盘上的文件，所以答案 a 不正确。字符特殊文件和门（Door）都是文件类型，而不是链接，所以答案 c 和 d 不正确。

### 需要了解更多？

![](img/b957f979417d9f16274c2eb52c8f2c9f_246_0.png)
- Mulligan, John P. 著，*Solaris 与必备参考*（New Riders，印第安纳波利斯，印第安纳州：2001），ISBN 0-7357-1007-4。

![](img/b957f979417d9f16274c2eb52c8f2c9f_246_1.png)
- Sun Microsystems 著，*系统管理指南，第 1 卷*。有印刷版（部件号 805-7228-10），可在 **http://docs.sun.com** 网站上获取，也可以通过 Solaris 8 操作系统附带的联机文档 AnswerBook2 获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_246_2.png)
- Sun Microsystems 著，*系统参考手册，第 1 部分——用户命令*。有印刷版（部件号 806-0624-10），可在 **http://docs.sun.com** 网站上获取，也可以通过 Solaris 8 操作系统附带的联机文档 AnswerBook2 获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_246_3.png)
- Sun Microsystems 著，*系统参考手册，第 1M 部分——管理命令*。有印刷版（部件号 806-0625-10），可在 **http://docs.sun.com** 网站上获取，也可以通过 Solaris 8 操作系统附带的联机文档 AnswerBook2 获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_247_0.png)

## 系统基础

**你需要理解的术语：**

- 目录树
- 元字符
- 绝对路径名和相对路径名

**你需要掌握的技术：**

- 使用绝对路径名和相对路径名浏览目录树
- 使用元字符选择目录和文件
- 创建和删除目录
- 创建、复制、重命名和删除文件
- 使用 vi 文本编辑器
- 在系统之间传输数据
- 在远程系统上执行程序

本章介绍一些系统基础知识，包括浏览 Unix 目录树、使用 **vi** 编辑器以及访问远程系统。本章涵盖*基本命令语法*、*编辑器*和*远程连接*的测试目标。

### Unix 目录树

Unix 数据存储设施是一个包含文件和其它目录的目录集合。这些文件和目录以层级结构组织，并以根（/）目录为起点。因此，Unix 数据存储采用倒置树的形式，目录是树枝，文件是树叶。

#### 元字符

*元字符* 是可以表示目录名或文件名全部或部分的字符或字符组合。借助元字符，你可以用简短的短语表示较长的目录/文件名，甚至可以表示一系列目录/文件名。三种标准 shell（Bourne、C 和 Korn）都支持表 10.1 中列出的元字符。

**表 10.1 目录/文件名元字符**

| 元字符 | 描述 |
|---|---|
| `?` | 匹配任意单个字符。 |
| `*` | 匹配任意字符的零次或多次出现。 |
| `[...]` | 表示一个字符集，其中任意一个字符都可以匹配。常用字符集可以用范围表示。例如，小写字母（`[a-z]`）、大写字母（`[A-Z]`）和数字（`[0-9]`）经常使用。 |

下面的示例最能说明元字符的用法。给定一组文件——filea、fileb 一直到 filez——你可以将以下元字符表达式作为 ls 命令的参数，以表示全部 26 个文件：

```shell
ls file[abcdefghijklmnopqrstuvwxyz]
ls file[a-e f-j k-o p-t u-z]
ls file[a-mn-z]
ls file[a-z]
ls file*
ls file?
```

因此，元字符可用于引用具有公共前缀或后缀的文件。例如，给定一组以 .c 扩展名结尾的 C 语言源代码文件，你可以使用 `*.c` 元字符表达式引用所有这些文件。

#### 目录树导航

用户登录系统后，会被定位在 Unix 目录树中的某个位置——通常是用户帐户的主目录。当前目录也称为*当前工作目录*，可以使用 pwd(1) 命令显示。

用户可以使用 cd(1) 命令在目录树中移动。不带任何命令行参数使用时，cd 会将用户重新定位到 HOME 环境变量指定的目录（通常是用户帐户的主目录）。可以将新目录指定为命令行参数。如果该目录存在且用户对该目录拥有执行权限，则用户将被重新定位到该目录。新目录可以通过完整目录名、部分目录名加元字符，或（在少数情况下）仅用元字符来指定。

新目录也可以指定为从根（/）目录开始的*完整或绝对路径名*，或从当前工作目录开始的*部分或相对路径名*。你可以使用单个点（.）引用当前目录，使用两个点（..）引用当前目录上方的目录（*父目录*），如下例所示：

```sh
$ pwd
/export/home/dla
$ cd ..
$ pwd
/export/home
$ cd .
$ pwd
/export/home
$ cd /export/home
$ pwd
/export/home
$ cd dla
$ pwd
/export/home/dla
$
```

你还可以在同一路径中使用（..）引用多个父目录，如下例所示：

```sh
$ pwd
/export/home/dla
$ cd ../../..
$ pwd
/export
$
```

元字符 `?` 和 `*` 也可以用来指定目录名。请记住，`?` 可表示任意单个字符，`*` 可表示任意数量的任意字符。假设主目录 dla 是 /export/home 下唯一与所有这些元字符表达式匹配的目录，那么以下所有命令都会将当前工作目录更改为 /export/home/dla：

```bash
cd /export/home/dla
cd /export/home/dl?
cd /export/home/d?a
cd /export/home/???
cd /export/home/?la
cd /export/home/?l?
cd /export/home/??a
cd /export/home/???
cd /export/home/*
cd /export/home/d*
cd /export/home/*a
cd /export/home/*l*
cd /export/home/?l*
```

![](img/b957f979417d9f16274c2eb52c8f2c9f_250_0.png)

请务必理解用于构造目录路径和文件名的 `?`、`*` 和 `[]` 元字符的含义和用法。无论是单独使用还是组合使用，它们都可以简化对冗长、复杂的路径名或大量文件的指定。

#### 目录

有几个命令可以让你创建、移动和删除目录：

- `mkdir(1)`——创建目录。
- `mv(1)`——移动文件或目录。
- `rmdir(1)` 或 `rm(1)`——删除目录。

##### 使用 mkdir 命令创建目录

mkdir(1) 命令创建以命令行参数形式指定的目录。该命令行参数可以是绝对（从 / 开始）路径名，也可以是相对于当前目录的路径名。该目录的所有者将是用于创建目录的用户帐户以及该用户所属的组。创建时会根据当前 umask 或 `-m mode` 命令行参数指定的访问权限来设置访问权限；mode 是一组使用绝对模式格式定义的权限。要创建多个目录，请将它们作为命令行参数（以空格分隔）指定。通常情况下，要在其中创建新目录的父目录必须已经存在。但是，如果指定 **-p** 命令行参数，则会首先创建任何必要的父目录。以下示例展示了 **mkdir** 命令的几种用法。第一个示例使用 **umask** 权限创建目录。第二个示例以指定的权限创建目录。第三个示例失败，因为必需的父目录不存在。第四个 **mkdir** 命令使用 **-p** 命令行参数创建父目录：

```text
# mkdir exam

# ls -l exam
total 0

# ls -ld exam
drwxr-xr-x  2 root     other       512 Apr 13 17:32 exam

# mkdir -m 777 test2

# ls -ld test*
drwxr-xr-x  2 root     other       512 Apr 13 17:32 exam
drwxrwxrwx  2 root     other       512 Apr 13 17:33 test2

# mkdir /exam/Solaris/8
mkdir: Failed to make directory "/exam/Solaris/8":
No such file or directory

# mkdir -p /exam/Solaris/8

# ls -lR /exam
/exam:
total 2
drwxr-xr-x  3 root     other       512 Apr 13 17:33 Solaris

/exam/Solaris:
total 2
drwxr-xr-x  2 root     other       512 Apr 13 17:33 8

/exam/Solaris/8:
total 0
#
```

##### 使用 mv 命令移动目录

mv(1) 命令可以像移动普通文件一样移动目录及其内容：

```text
# mv /exam /test

# ls -lR /test
/test:
total 2
drwxr-xr-x  3 root     other       512 Apr 13 17:33 Solaris

/test/Solaris:
total 2
drwxr-xr-x  2 root     other       512 Apr 13 17:33 8
```

