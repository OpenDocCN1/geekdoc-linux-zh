
能够充分利用属性的故障排除者发现，排除 Samba 故障比简单的系统容易得多。为了让 Samba 故障排除变得简单且统一，本章提出了以下排除流程：

1. 备份 `smb.conf` 和任何其他数据。
2. 描述并重现症状。
3. 执行快速检查。
4. 浓缩症状描述。
5. 缩小问题范围。
6. 修复并测试。

重要的是，运行 `DIAGNOSIS.txt` 测试发生在第 2 步，因为哪个 `DIAGNOSIS.txt` 测试失败的信息是任何 Samba 症状描述中不可或缺的一部分。

Samba 附的 `DIAGNOSIS.txt` 文件包含一个 10 项线性的、预定义的诊断程序，该程序在之前的测试中已通过验证。这种预定义的诊断可以在不到五分钟的测试内极大地缩小问题范围。本章提供了一个脚本，可以以多种形式在一分钟内运行这些测试。测试结果记录在日志中供分析。自动化测试增加了一个测试 1.5，使用 `ps` 命令检查正在运行的 `smb` 和 `nmbd` 守护进程。

Samba 许多许多测试点和测试工具。本章使用了以下非常简单的 Samba 系统模型：

![](img/3a3dd42091ecc215c9b779bbd31cd990_703_0.png)

引入了许多诊断工具，每种工具都能测量或注入到 Samba 系统的不同点。以下是最重要的诊断工具，本章均对其进行了详细介绍：

# 排除 Samba 故障

第 22 章

- `nmblook`
- `nbtstat`
- `net view`
- `net use`
- `smbstatus`
- `smbclient`
- `preexec=`
- `testparm`
- `SWAT`
- `strace`
- `tcpdump`
- `netstat`
- `ping`
- `smbpasswd`
- `Test jigs`

在线帮助对 Samba 技术人员来说是一个巨大的优势。取决于他们如何组织信息请求，这种优势对某些人很大，对另一些人则不然。请求应该被构思为成员与其他成员之间的交流，而不是外来者。症状描述必须先说明最重要的事实，因为大多数受众只有不到一分钟的时间来决定如何处理每封邮件。显然缺乏准备会限制获得信息回复的可能性。而且，当然，必须使用标准的网络礼仪（netiquette）。

快速查看任何 Samba 邮件列表或新闻组，都会发现排除 Samba 故障被认为是非常困难的。仔细观察帖子会发现，遇到困难的人并没有利用本章描述的 Samba 原生故障排除工具。一旦了解并利用这些工具，大多数 Samba 故障排除将变得异常简单。

![](img/3a3dd42091ecc215c9b779bbd31cd990_704_0.png)

# Samba 学习工具

作者：Steve Litt

## 本章内容

- 创建你自己的信息工具 660
- 阅读源码，路加 Luke 665
- 实验 678
- 加入 Samba 项目 679
- SWAT 作为学习工具 679
- 发行版文档 680
- 手页 (Man Pages) 683
- 网站、新闻组和邮件列表 683

# 创建即插用的 Samba 系统

第二部分

Samba 拥有一个卓越的核心开发团队，但仅此不足以解释其现象级的成功。即使是卓越的产品也不够的。

Samba 的成功很大程度上归功于数千名 Samba 管理员和程序员组成的队伍，他们发现并修复漏洞，同时也让其他人了解了 Samba 知识。结果是巨大的增长。最令人惊讶的是，几乎没有正式的 Samba 课程。相反，Samba 管理员和程序员利用了 Samba 免费提供的各种学习工具。本章描述了其中一些工具。

## 创建你自己的信息工具

本节描述了信息工具的创建。所有这些工具都包含在单个目录下，当该目录为当前目录时，它们都能正常工作。这样做的好处是它们形成了一个不依赖于其他内容的独立工具箱。

引入了许多诊断工具，每种工具都能测量或注入到 Samba 系统的不同点。以下是最重要的诊断工具，本章均对其进行了详细介绍：

## testparam-Based Global/Share

排除 Samba 故障可以被认为是非常困难的。仔细观察帖子会发现，遇到困难的人并没有利用本章描述的 Samba 原生故障排除工具。一旦了解并利用这些工具，大多数 Samba 故障排除将变得异常简单。

## 工具

本节描述了信息工具的创建。所有这些工具都包含在单个目录下，当该目录为当前目录时，它们都能正常工作。这样做的好处是它们形成了一个不依赖于其他内容的独立工具箱。

# 创建即插用的 Samba 系统

`global` 被放置于共享定义中。本节描述了一个名为 `global.gran` 的脚本，它将参数（从空文件通过 `testparam` 得出的合法值）放入共享中，对新配置运行 `testparam`，检测任何错误消息并输出 `SHARE`、`GLOBAL` 或 `BADPARAMETER`。注意，如果它不是主同义词，将产生错误结果，因此有时必须直接调用粒度函数。以下是 `global` 脚本：

```bash
#!/bin/sh

./syntax1.inc
```

```bash
# 创建临时配置文件
echo [noshare] > ./temp.conf
echo $value >> ./temp.conf
```

```bash
# 确定全局还是共享
phrase="global parameter \$1 found in service section"
temp1=$(testparam -s ./temp.conf | grep "\$phrase")
 [ "$temp1 = * ] && type="GLOBAL"
```

```
# 打印结果
echo $type
```

再次，调用此方法是将 `mainname` 作为参数。注意以下三个命令的结果：

```
$ ./global.gran "read only"
SHARE
```

```
$ ./global.gran "write ok"
BADPARAMETER
```

```
$ ./global.gran "$(./mainname "write ok")"
SHARE
$
```

`./mainname "write ok"` 周围的引号是必要的，因为 `./mainname "write ok"` 返回字符串 `read only`，如果不加引号，它会被视为 `./mainname` 的两个独立的参数。

一个更简单的命令名为 `global`，它在内部包含了对 `mainname` 的调用：

```
#!/bin/sh
./syntax1.inc
./global.gran $(./mainname "$1")
```

以下是上述命令的结果：

```
$ ./global "read only"
SHARE
$ ./global "write ok"
SHARE
$ ./global "printing"
BADPARAMETER
$
```

上述三个调用中的最后一次演示了 `granular` 函数必须是可用的。`mainname` 脚本无法准确处理 `printing=` 参数。`printing=` 的正确调用方式如下：

```
$ ./global.gran "printing"
SHARE
$
```

## 基于 testparm 的默认值显示器

可以编写一个脚本来显示参数的默认值。该脚本除非传递主同义词否则无法工作，因此它是一个需要包含 `mainname` 的颗粒脚本。以下是 `default.gran` 脚本：

```bash
#!/bin/bash
./syntax1.inc
echo -> empty.conf
testpharm -s ./empty.conf | grep -i "1"
```

它的调用方式如下：

```
$ ./default.gran "$(./mainname "write ok")"
```

或

```bash
$ ./default.gran "printing"
```

在前面的示例中，记住 `mainname` 脚本对 `printing=` 参数给错误的结果，因为 `printing` 既不是 0 也不是 1。对于 `mainname` 可的大多数参数，可以创建一个脚本来提供更简单的命令。以下名为 `default` 的脚本就是一个示例：

```bash
#!/bin/bash
./syntax1.inc
./default.gran "$(./mainname "$1")"
```

## 创建开箱用的 Samba 系统

第二部分

之前的调用使用 `arg1` 作为主同义词运行 `default.gran`。以下是使用 `mainname` 运行该参数的结果：

```
$ ./default "write ok"
  read only = Yes
$ ./default "allow hosts"
  hosts allow =
```

## 基于 man 页的同义词查找器

得于 `testparam` 的翻译，从另一个同义词查找主同义词非常容易。更困难的是找到主同义词的所有同义词。一种方法是在 man 页中查找短语 "synonym for $1" 的实例，如下所示所示：

```sh
#!/bin/sh
../syntax.1.inc
man smb.conf | sed s/\H//g | grep -iC "synonym for \*$1"
```

以下是这种用法的示例：

```
$ ./syns "$(mainname hosts allow)"
  allow hosts ($)
```

`hosts allow` 的同义词。

这种方法的可靠性取决于 `smb.conf` man 页，而后者的目的并不是一致的逻辑。

更优的方法是创建一个 C 程序，循环遍历 Samba 的 `parm_table`，并以所需的参数作为 `ptr` 输出每个元素的标签。从克隆 `testparam` 开始设置一个程序是非常容易的。请注意，由于 `parm_table[]` 是静态的，它在 `loadparam.c` 之外无法直接访问，因此你可能需要在 `loadparam.c` 中创建一个很小的访问函数。

也可能编写一个 Perl 程序来解析 `param/loadparam.c` 中的表初始化，但那是一种权宜之计。

## Samba 专用 Linux 机器

学习 Samba 的最佳工具是一个运行 Samba 的测试箱（test jig box）。没有什么比无意义系统上的 root 密码更能激发你内心的冒险精神了。最快的学习方法是通过观察微小变化的结果。

## Samba 学习工具

第 23 章

专用 Linux 机器的另一个好处是可以共享（希望是只读的）映射到 Linux 根目录的目录。这样就可以从 Windows 进行浏览和搜索了。记得设置 `symlinks=no` 以防止递归。

## 在浏览器中查看 man 页

查看 man 页的最佳方法是在 Web 浏览器中查看。查看大量文本并使用滚动条快速滚动是无价的。对于像 `smb.conf` 这样的 man 页，这是至关重要的。

查看“HTML 化” Samba man 页的最佳方法是使用 SWAT。SWAT 的首页包含指向所有主要 Samba 页面的链接。此外，`share`、`global` 和 `printer` 上的每个参数都有指向其 man 页中文本的链接。

但有时没有安装 SWAT，可能是出于安全考虑或其他原因。在这种情况下，可以写一个 CGI 脚本来在浏览器中显示 man 页：

```perl
#!/usr/bin/perl -w
use strict;
my($manpage) = $ENV{QUERY_STRING};
print `man -C man.conf.man2html $manpage | man2html` 
```

在前面的案例中，行中命令周围的引号是反引号。`man2html` 是 Red Hat Linux（以及其他 Linux 发行版和 UNIX 版本）自带的可执行文件。在 Red Hat Linux 6 上，它位于 `/usr/bin`。文件 `man.conf.man2html` 是 `/etc/man.conf` 的特殊配置副本。TROFF、NFF 和 TBL 的处理器更改为 `/bin/cat`。EGN 和 NEQN 的处理器被注释掉了，REFER、PIC 和 PAGER 的处理器也是如此。它还必须添加。

# cvs.log

`grepcf` 和 `grepsrc` 脚本会返回字符串使用的位置，但不会说明原因。`cvs.log` 文件通常包含更改的理由。`cvs.log` 命令可以快速获取包含字符串的实例：

```bash
#!/bin/bash
[ "1" = "*" ] || \
  echo NOARG: Syntax: $0 \string\" [context lines]; exit
  [ "3" = "*" ] && \
  echo XS ARGS: Syntax: $0 \string\" [context lines]; exit

context-S2
[ "2" = "*" ] context=0
  ./setsource.inc

# grep -iC$1" $sourcedir/cvs.log | less -N
cat -n $sourcedir/cvs.log | grep -iEC$context "$1" | less
```

注意上述命令搜索的是 `cvs.log`。

# grepfall
