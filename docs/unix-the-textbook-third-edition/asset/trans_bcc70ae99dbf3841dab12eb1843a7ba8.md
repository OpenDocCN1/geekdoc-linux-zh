

```
% gunzip bash.man.gz
% gzip bash.man tcsh.man
% gzip -l bash.man.gz tcsh.man.gz
      compressed uncompressed ratio uncompressed_name
          105342      367470  71.3% bash.man
           77715      239996  67.6% tcsh.man
          183057      607466  69.8% (totals)
% gunzip *.man.gz
% ls -l *.man
-rw-r--r-- 1 sarwar faculty 367470 Aug 30 21:39 bash.man
-rw-r--r-- 1 sarwar faculty 239996 Aug 30 21:39 tcsh.man
%
```

## 7.2.5 gzexe 命令

gzexe 命令可用于压缩可执行文件。用 gzexe 命令压缩的可执行文件仍然可执行，可以通过其名称执行。如果用 gzip 命令压缩可执行文件则不然。因此，如果文件要从一台计算机传输到另一台计算机——例如通过互联网通过电子邮件传输——为了节省磁盘空间和网络带宽，可执行文件会用 gzexe 命令进行压缩。下面是对该命令的简要描述。

### SYNTAX
gzexe [options] [file-list]

目的：将 file-list 中给出的可执行文件压缩；备份文件创建在 file-name~ 中，应在压缩文件成功创建后删除
常用选项/功能：
- -d 解压缩已压缩文件

以下会话说明了 gzexe 命令的使用。注意，当你用 gzexe 命令压缩可执行文件 sh.temp 时，它会在 sh.temp~ 文件中创建原始文件的备份。sh.temp 文件被压缩后，可以像普通可执行文件一样执行。gzexe -d sh.temp 命令用于解压缩已压缩的 sh.temp 文件。压缩版本的备份保存在 sh.temp~ 文件中。

```
% cp /bin/sh sh.temp
% file sh.temp
sh.temp: ELF 64-bit LSB executable, x86-64, version 1 (FreeBSD), dynamically linked (uses shared libs), for FreeBSD 10.0 (1000510), stripped
% gzexe sh.temp
sh.temp:        49.2%
% ls -l sh*
-rw-------  1 sarwar faculty  71133 Aug 30 21:59 sh.temp
-rw-------  1 sarwar faculty 139264 Aug 30 21:59 sh.temp~
% gzexe -d sh.temp
49.2%
% ls -l sh*
-rw-------  1 sarwar faculty 139264 Aug 30 22:00 sh.temp
-rw-------  1 sarwar faculty 139264 Aug 30 21:59 sh.temp~
%
```

## 7.2.6 zcat 和 zmore 命令

将压缩文件转换回原始文件然后再显示它是一个耗时的过程，因为文件创建需要磁盘 I/O。如果您只想查看原始文件的内容，可以使用 UNIX 命令 zcat（压缩文件的 cat 命令），它显示用 compress 或 gzip 压缩的文件的内容。该命令在显示之前会解压缩文件。原始文件保持不变。zmore 命令可用于一次显示一屏压缩文件。当未给出文件或 - 作为参数时，这些命令从 stdin 读取输入。两个命令都允许您指定一个或多个文件作为参数。下面是对 zcat 命令的简要描述。

### SYNTAX
```
zcat [options] [file-list]
```

目的：将压缩文件以其原始形式连接并发送到标准输出；如果未指定文件，则从标准输入获取输入

常用选项/功能：
- -h 显示帮助信息
- -r 递归操作子目录
- -t 测试压缩文件的完整性

在以下会话中，gzip 命令用于压缩 bash.man 文件并将其存储在 bash.man.gz 文件中。当使用 more 命令显示压缩文件时，屏幕上会显示乱码。zmore 命令用于显示原始文件的内容。我们没有使用 zcat 命令，因为 bash.man 是一个大型、多页文件。

```
$ gzip bash.man
$ more bash.man.gz
<<BB>^HA<FE>T<97><C3>
<DD><A0><CC><D<AE>><B2><B0><G<FE>><BC><0C<DC><99><DD><8F><AC><"<E3>
<8E>_f<PA><E4><D9><0<8F><P9><0<E4><FP>/u<BE>><FP><F9><BA><FA><FA>I
<F5><E4>w<D5><BE>□<BE>x<DE>><AF><FB><AB>x<BF><FA><FA><BB><F8>i<B7>□
<F9><C3>'i97zu<BB><BE><BD>,
<F9><EF><BD><P7><EF><BD><F7><AC>z<F6><A7><EA>O
<F0><C5>oA0A<EB><BE><AD><BE><C5>??<F9><F0><E1>,
<FB>zu"Wu<F5><W<D5>Uf
<D1>m<B6><B6>Ý<F7>/ <E3><B8>y<B7>Z<D5><EB><C5>Y1<DB><F5>e<CF>
p<D1>.
<9B><97><EF><BD><P7>Y<F5><8F><A3><FE><BB><FA>=
...
% zmore bash.man.gz
```

```
BASH(1)                                                                 BASH(1)
NAME
    bash - GNU Bourne-Again SHell
SYNOPSIS
    bash [options] [command_string [f file]]
COPYRIGHT
    Bash is Copyright (C) 1989-2013 by the Free Software
    Foundation, Inc.
DESCRIPTION
    Bash is an sh-compatible command language interpreter
    that executes commands read from the standard input or from a
    file. Bash also incor-
...
%
```

在以下会话中，zcat 命令解压缩 t2.gz 文件并将其输出发送到标准输出（本例中为显示屏）。t2.gz 文件保持完整。

```
% gzip t2
% zcat t2.gz
This file will be used to test various UNIX and Linux commands and
tools.
UNIX and Linux rule the networking world!
%
```

如该命令描述中所述，zcat 命令可以显示多个文件。例如，可以使用 zcat t1.Z t2.Z t3.Z 来显示三个文件 t1.Z、t2.Z 和 t3.Z 的未压缩形式。zcat 命令也可以用于显示用 compress 命令压缩的文件——即扩展名为 .Z 的文件。

在以下章节练习中，您将使用 compress、uncompress、gzip、gunzip、zmore 和 zcat 命令来了解它们的语法和语义。

## EXERCISE 7.1

创建本节中使用的 t2 文件。使用 compress 命令压缩该文件。你使用了什么命令行？

