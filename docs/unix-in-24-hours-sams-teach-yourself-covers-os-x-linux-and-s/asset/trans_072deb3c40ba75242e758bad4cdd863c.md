

# 代码片段

```
% man mkdir
```

MKDIR(1)                          FreeBSD 通用命令手册                          MKDIR(1)

# 名称

mkdir - 创建目录

# 概要

mkdir [-p] [-m mode] directory_name ...

# 描述

Mkdir 按指定的顺序创建作为操作数的目录，使用模式 rwxrwxrwx (0777) 并根据当前 umask(2) 进行修改。

选项如下：

-   -m  将最终创建的目录的文件权限位设置为指定的模式。mode 参数可以使用 chmod(1) 命令指定的任何格式。如果指定了符号模式，则操作字符 '+' 和 '-' 相对于初始模式 'a=rwx' 进行解释。

-   -p  根据需要创建中间目录。如果未指定此选项，则每个操作数的完整路径前缀必须已存在。中间目录以 rwxrwxrwx (0777) 的权限位创建，并根据当前 umask 进行修改，同时为所有者增加写和搜索权限。

用户必须在父目录中具有写权限。

# 诊断

mkdir 实用程序在成功时退出 0，在发生错误时退出 >0。

# 另请参阅

rmdir(1)

# 标准

mkdir 实用程序预计与 IEEE Std1003.2 ('POSIX.2') 兼容。

# 历史

mkdir 命令出现在 AT&T UNIX 第 1 版中。

```
% man -k date | head -18
1. date(1) /usr/share/man/man1/date.1
date - write the date and time

2. gdate(1) /usr/share/man/man1/gdate.1
date - print or set the system date and time

3. strptime(3c) /usr/share/man/man3c/strptime.3c
strptime - date and time conversion

4. ftime(3c) /usr/share/man/man3c/ftime.3c
ftime - get date and time

5. clock(1t) /usr/share/man/man1t/clock.1t
clock - Obtain and manipulate dates and times

6. stime(2) /usr/share/man/man2/stime.2
stime - set system time and date
%
```

% whatis
whatis(1)      NAME    /usr/share/man/man1/whatis.1
whatis - display a one-line summary about a keyword
%

```
% whatis cd
No LSB modules are available.
Distributor ID:    Ubuntu
Description:    Ubuntu 15.04
Release:    15.04
Codename:    vivid
```

% apropos cd
1. cd(1t) /usr/share/man/man1t/cd.1t
cd - Change working directory

2. cd(1) /usr/share/man/man1/cd.1
cd, chdir, pushd, popd, dirs - change working directory

3. cdrw(1) /usr/share/man/man1/cdrw.1
cdrw - CD read and write

4. sound-juicer(1) /usr/share/man/man1/sound-juicer.1
sound-juicer, gnome-cd - GNOME CD ripper and player

5. cdio(7i) /usr/share/man/man7i/cdio.7i
cdio - CD-ROM control operations

6. eject(1) /usr/share/man/man1/eject.1
eject - eject media such as CD-ROM from drive

7. cdrecord(1) /usr/share/man/man1/cdrecord.1
cdrecord - record audio or data CD, DVD or BluRay

8. hsfs(7fs) /usr/share/man/man7fs/hsfs.7fs
hsfs - High Sierra & ISO 9660 CD-ROM file system

9. sd(7d) /usr/share/man/man7d/sd.7d
sd - SCSI disk and ATAPI/SCSI CD-ROM device driver

10. cdda2wav(1) /usr/share/man/man1/cdda2wav.1
cdda2wav - dumps CD audio data into sound files with extra data verification

11. brasero(1) /usr/share/man/man1/brasero.1
brasero - Simple and easy to use CD/DVD burning application for the Gnome Desktop

12. rmmount(1m) /usr/share/man/man1m/rmmount.1m
rmmount - removable media mounter for CD-ROM, Jaz drive, and others
others %

```
% alias apropos="man -k \!* | uniq | grep 1"
% apropos cd
1. cd(1t) /usr/share/man/man1t/cd.1t
2. cd(1) /usr/share/man/man1/cd.1
3. cdrw(1) /usr/share/man/man1/cdrw.1
4. sound-juicer(1) /usr/share/man/man1/sound-juicer.1
6. eject(1) /usr/share/man/man1/eject.1
7. cdrecord(1) /usr/share/man/man1/cdrecord.1
10. cdda2wav(1) /usr/share/man/man1/cdda2wav.1
11. brasero(1) /usr/share/man/man1/brasero.1
12. rmmount(1m) /usr/share/man/man1m/rmmount.1m
%
```

# 名称

sort - 对文本文件的行进行排序

# 概要

sort [-cmus] [-t separator] [-o output-file] [-T tempdir] [-bdifiMnr] [+POS1 [-POS2]] [-k POS1[,POS2]] [file...]
sort {--help,--version}

# 描述

本手册页记录了 GNU 版本的 sort。sort 对给定文件中的所有行进行排序、合并或比较，如果未给出文件，则使用标准输入。文件名 '-' 表示标准输入。默认情况下，sort 将结果写入标准输出。

sort 有三种操作模式：sort（默认）、merge 和检查已排序性。以下选项更改操作模式：

-c 检查给定文件是否已排序：如果未全部排序，则打印错误消息并以状态 1 退出。

-m 按组对给定文件进行合并排序。每个输入文件应已单独排序。始终可以改用排序；合并是提供的，因为在可行时速度更快。

一对行按如下方式比较：如果指定了任何键字段，sort 会按命令行指定的顺序比较每一对字段，根据相关的排序选项进行比较，直到找到差异或没有字段剩余。

