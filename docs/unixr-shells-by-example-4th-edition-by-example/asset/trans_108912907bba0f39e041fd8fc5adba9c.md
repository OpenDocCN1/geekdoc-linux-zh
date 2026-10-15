

/etc/cron.allow 文件：(3) 你是普通用户，但你的系统包含一个文件 /etc/cron.deny，且该文件为空。

## crypt—对文件进行编码或解码

```
crypt [ password ]
```

crypt 对文件的内容进行加密和解密。密码是选择一种转换类型的密钥。

## cut—从文件的每一行中删除选定的字段或字符

```
cut -clist [ filename ... ]
```

```
cut -flist [ -dc ] [ -s ] [ filename ... ]
```

cut 命令从文件的一行中剪切出列或字符；如果未给出文件，则使用标准输入。-d 选项指定字段分隔符。默认分隔符是制表符。

## EXAMPLE A.17

|  |  |
|---|---|
| 1 | cut -d: -f1,3 /etc/passwd |
| 2 | cut -d: -f1-5 /etc/passwd |
| 3 | cut -c1-3,8-12 /etc/passwd |
| 4 | date | cut -c1-3 |

## EXPLANATION

- 1. 使用冒号作为字段分隔符，显示 /etc/passwd 文件的字段 1 和 3。
- 2. 使用冒号作为字段分隔符，显示 /etc/passwd 文件的字段 1 到 5。
- 3. 剪切并显示 /etc/passwd 文件中每一行的第 1 到 3 个字符和第 8 到 12 个字符。
- 4. 将 date 命令的输出作为输入发送给 cut。打印前三个字符。

## date—显示日期和时间或设置日期

```
[ -u ] [ -a [ - ] sss.fff ] [ yymmddhhmm [ .ss ] ] [+format ]
```

不带参数时，date 命令显示日期和时间。如果命令行参数以加号开头，则参数的其余部分用于格式化输出。如果使用百分号，则下一个字符是格式化字符，用于提取日期的特定部分，例如仅年份或星期几。要设置日期，命令行参数以表示年份、月份、日期、小时和分钟的数字表示。

## EXAMPLE A.18

```
1  date +%T
2  date +20%y
3  date "It is now %m/%d/%y"
```

## EXPLANATION

- 1  以 20:25:51 的格式显示时间。
- 2  显示 2096。
- 3  显示 It is now 07/25/96。

## dd—在复制文件时转换文件

```
dd [--help] [--version] [if=file] [of=file][ibs=bytes] [obs=bytes] [bs=bytes] [cbs=bytes] [skip=blocks] [seek=blocks] [count=blocks] [conv={ascii,ebcdic,ibm,block,unblock,lcase,ucase,swab,noerror,notrunc,sync}]
```

从一个位置复制文件到另一个位置，最常见的是到磁带驱动器或从磁带驱动器，或在不同的操作系统之间。

## EXAMPLE A.19

```
1  $ dd --help
2  $ dd if=inputfile of=outputfile conv=ucase
```

## EXPLANATION

- 1  打印所有选项和标志，并附带简短说明。
- 2  将 inputfile 中的所有字符转换为大写并发送输出到 outputfile。

## diff—比较两个文件的差异

```
[ -bitw ] [ -c ] [ -Cn ]
```

比较两个文件并逐行显示差异。还显示你将使用 ed 编辑器使用的命令来做出更改。

## EXAMPLE A.20

## EXPLANATION

显示 file1 和 file2 的每一行如何不同。第一个文件由 < 符号表示，第二个文件由 > 符号表示。每行前面都有一个 ed 命令，表示将用于使文件相同 的编辑命令。

## dos, xdos, dosexec, dosdebug—一个 Linux DOS 模拟器，可在 Linux 下运行 MS-DOS 和 MS-DOS 程序

（请参阅 Linux 手册页以获取完整说明。内容很长……）

## df—汇总可用磁盘空间

```
df [-aikPv] [-t fstype] [-x fstype] [--all][--inodes][--type=fstype]
[--exclude-type=fstype][--kilobytes] [--portability] [--print-type]
[--help] [--version] [filename...]
```

df 命令显示每个文件所在的 文件系统 的信息，或默认情况下显示所有文件系统。

## EXAMPLE A.21

```
df
Filesystem      1024-blocks Used Available Capacity Mounted on
/dev/hda5       1787160 1115587 579141 66% /
```

## du—汇总磁盘使用情况

```
du [-arskod] [name ...]
```

du 命令报告每个目录和文件中包含的 512 字节块数，以及（递归地）其中的所有文件和目录。

## EXAMPLE A.22

```
1  du -s /desktop
2  du -a
```

## EXPLANATION

- 1. 显示 /desktop 及其子目录中所有文件的块使用情况汇总。
- 2. 显示此目录及其子目录中每个文件的块使用情况。

