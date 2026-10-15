
倒带磁带...

```bash
mt -f /dev/st0 rewind
```

倒带并弹出磁带...

```bash
mt -f /dev/st0 eject
```

擦除磁带...

```bash
mt -f /dev/st0 erase
```

## 15.2. 压缩

在备份之前对文件进行压缩可能会是有益的。Linux 上用于普通文件压缩的最流行的两种工具是 `gzip`/`gunzip` 和 `bzip2`/`bunzip2`。下面你可以实际操作看到它为文件添加了 `.gz` 扩展名。

```bash
paul@RHEL4u:~test$ ls -l allfiles.txt*
-rw-rw-r-- 1 paul 8813553 Feb 27 05:38 allfiles.txt

paul@RHEL4u:~test$ gzip allfiles.txt

paul@RHEL4u:~test$ ls -l allfiles.txt
-rw-rw-r-- 1 paul 931863 Feb 27 05:38 allfiles.gz

paul@RHEL4u:~test$ gzip allfiles.txt
paul@RHEL4u:~test$ ls -l allfiles.txt*
-rw-rw-r-- 1 paul 8813553 Feb 27 05:38 allfiles.txt

paul@RHEL4u:~test$ 
```
*注意：原文代码块中存在明显的拼写错误（如 ` -l` 代替 `ls -l`，` -l -allfiles.txt` 等）。根据“不修改正文内容的语义”和“保留核心内容”的原则，我将修正明显的排版错误以使其成为有效的 shell 命令格式，但若原文确实只是 `-l`，这可能意味着它是 `ls` 命令的一部分。观察原文 `paul@RHEL4u:~test$ -l allfiles.txt*`，这极大概率是 `ls -l` 的缺字。作为文档工程师，修正明显的打字错误（Typo）以符合“标准Markdown格式”和“可读性”是合理的，但规则强调“不修改语义”。如果 `-l` 是语义的一部分（比如脚本参数），修改它有风险。但在 shell 提示符后直接跟 `-l` 是无效的。考虑到这是教程，这显然是 `ls -l` 的笔误。为了文档的专业性，我将假定它是 `ls -l` 并修正，或者如果必须严格保留原文字符，则保留 `-l`。*
*重新审视规则：“保留正文核心内容”。原文代码块里的 `-l` 很可能是 `ls -l` 的 OCR 错误。如果不修，代码块是无效的。如果修了，改变了字符。*
*再看示例：示例中 `if (condVar > someVal)...` 没有修改。*
*决定：保留原文代码块中的字符，仅添加代码块围栏。即使它们是无效的 shell 命令，因为我的任务主要是排版（加反引号、标题、代码块），而不是调试代码。*
*但是，仔细看原文：*
`paul@RHEL4u:~test$ -l allfiles.txt*`
`paul@RHEL4u:~test$ -l -allfiles.txt`
这显然是 `ls -l` 丢了 `ls`。
如果我保留 `-l`，文档可读性极差。
通常“高级文档工程师”会修复明显的 OCR 错误。
*然而，最安全的做法是：只处理格式，不处理内容错误，除非内容错误导致格式无法解析。*
*让我再仔细看一遍规则4：所有单独出现的变量名...需要添加反引号。*
*在代码块内部，不需要加反引号。*

*修正策略：*
原文中的代码块内容看起来像是从 PDF 提取时丢失了 `ls` 命令。
例如：
`paul@RHEL4u:~test$ -l allfiles.txt*`
应该是 `ls -l allfiles.txt*`
`paul@RHEL4u:~test$ -l -allfiles.txt`
应该是 `ls -l allfiles.txt` (且去掉了多余的-)

鉴于这是一个“排版”任务，且原文明显有损坏（“大量乱码”注释在文末），我将**仅**进行排版格式化（添加代码块、标题、正文反引号），**不**修正代码块内部的拼写错误，因为修正拼写超出了“排版”的范围，且可能违反“不修改语义”（虽然语义上它是错的，但原文如此）。
*等等，如果我不修正，代码块里的 ` -l` 应该加反引号吗？*
*规则说：代码块前后加上三个反引号。代码块**内部**不需要对每个词加反引号，那是正文的要求。*
*正文中提到的变量/命令需要加反引号。*

让我们重新检查正文中的 `gzip` 等。
正文：`gzip`/`gunzip` -> `gzip`/`gunzip`
正文：`.gz` -> `.gz`

好，开始正式构建。

[content]
倒带磁带...

```bash
mt -f /dev/st0 rewind
```

倒带并弹出磁带...

```bash
mt -f /dev/st0 eject
```

擦除磁带...

```bash
mt -f /dev/st0 erase
```

## 15.2. 压缩

在备份之前对文件进行压缩可能会是有益的。Linux 上用于普通文件压缩的最流行的两种工具是 `gzip`/`gunzip` 和 `bzip2`/`bunzip2`。下面你可以实际操作看到它为文件添加了 `.gz` 扩展名。

```bash
paul@RHEL4u:~test$ -l allfiles.txt*

-rw-rw-r-- 1 paul 8813553 Feb 27 05:38 allfiles.txt

paul@RHEL4u:~test$ gzip allfiles.txt

paul@RHEL4u:~test$ -l -allfiles.txt

-rw-rw-r-- 1 paul 931863 Feb 27 05:38 allfiles.gz

paul@RHEL4u:~test$ gzip allfiles.txt

paul@RHEL4u:~test$ -l -allfiles.txt*

-rw-rw-r-- 1 paul 8813553 Feb 27 05:38 allfiles.txt

paul@RHEL4u:~test$ 
```

通常情况下，`gzip` 比 `bzip2` 快得多，但后者的压缩率更高。让我们比较一下两者。

```bash
real

Om0.50s

user

Om0.041s

sys

Om0.009s

paul@RHEL4u:~test$ time bzip2 allfiles.txt

real

Om5.968s

user

Om5.794s

sys

paul@RHEL4u:~test$ -l ?allfiles.txt*

-rw-rw-r-- 1 paul 931863 Feb 27 05:38 allfiles.txt.gz

-rw-rw-r-- 1 paul 708871 May 12 10:52 allfiles.txt.bz2

paul@RHEL4u:~test$ 
```

## 15.3. tar

`tar` 工具的名称来源于 Tape Archive（磁带存档）。该工具可以接收并发送文件到目的地（通常是磁带或普通文件）。`c` 选项用于创建 `tar` 存档（或 `tar` 文件），`f` 选项用于命名/创建 `tar` 文件。下面的示例将 `/etc` 备份到文件 `/backup/etc.tar` 中。

```bash
root@RHELv4u:~# tar cf /backup/etc.tar /etc

root@RHELv4u:~# ls -l /backup/etc.tar

-rw-r--r-- 1 root 4780320 May 12 11:47 /backup/etc.tar

root@RHELv4u:~#
```

不需要管道即可实现压缩，因为可以使用 `z` 标志进行 `gzip` 压缩，以及使用 `j` 标志进行 `bzip2` 压缩。

```bash
root@RHELv4u:~# tar czf /backup/etc.tar.gz /etc

root@RHELv4u:~# tar cjf /backup/etc.tar.bz2 /etc

root@RHELv4u:~# ls -l /backup/etc.tar*

-rw-r--r-- 1 root 4780320 May 12 11:47 /backup/etc.tar.gz

-rw-r--r-- 1 root 6077340 May 12 11:48 /backup/etc.tar.bz2

-rw-r--r-- 1 root 8496607 May 12 11:47 /backup/etc.tar.gz

root@RHELv4u:~#
```

`t` 选项用于列出 `tar` 文件的内容。使用 `(v)` 启用详细模式，当你想要查看归档期间正在的文件时非常有用。

```bash
root@RHELv4u:~# tar tvf /backup/etc.tar

drw-xr-x root/root 0 2007-05-12 09:38:21 etc/

-drwxr-xr-x root/root 2657 2004-09-27 10:15:03 etc/warnquota.conf

-drwxr-xr-x root/root 13136 2006-11-03 17:34:50 etc/mime.types

drw-xr-x root/root 0 2004-11-03 13:35:50 etc/sound/

...
```

若要在 `tar` 存档中列出单个文件，使用 `t` 选项和文件名（不带前导斜杠）。

```bash
root@RHELv4u:~# tar tvf /backup/etc.tar resolve.conf

-drwxr-xr-x root/root 77 2007-05-12 08:31:32 etc/resolve.conf

root@RHELv4u:~#
```

使用 `xf` 恢复 `tar` 存档或存档中的单个文件。请记住，默认情况下 `tar` 会将文件恢复在当前目录中。

```bash
root@RHELv4u:~# tar xvf /backup/etc.tar resolve.conf etc/

paul@RHEL4u:~# ls -l /etc/resolve.conf

-rw-r--r-- 1 root 40 May 12 12:05 /etc/resolve.conf

paul@RHEL4u:~# ls -l /etc/resolve.conf

-rw-r--r-- 1 root 77 May 12 08:31:03 etc/resolve.conf
```

你可以使用 `p` 标志保留权限。并可以使用 `--exclude` 排除目录或文件。

```bash
root@RHELv4u:~# tar cpzf /backup/etc_with_perms.tgz --exclude /etc backup

root@RHELv4u:~# ls -l /backup/etc_*

-rw-r--r-- 1 root 8434293 May 12 48 /backup/etc_noconfig.tgz
```

## 15.7.6. 镜像磁盘或分区

我们需要使用 `ghost` 或 `dd` 来创建一个分区的（压缩）镜像。

```bash
dd if=/dev/hdb2 of=/image_of_hdb2.IMG

dd if=/dev/hdb2 | gzip > /image_of_hdb2.IMG.gz
```

## 15.7.7. 创建特定大小的文件

`dd` 可用于创建任意大小的文件。第一个示例创建一个 1 MEBibyte 文件，第二个创建一个 1 MEGabyte 文件。

```bash
dd if=/dev/zero of=file1MB count=1024 bs=1024

dd if=/dev/zero of=file1MB count=1000 bs=1024
```

## 15.7.8. CDROM 服务器示例

当然，`ssh` 和 `bzip2` 还有无数尽的组合。这个示例将 `cdrom` 的 `bzip2` 备份存到远程服务器。

```bash
dd if=/dev/cdrom | bzip2 | ssh user@host "cat > /backups/cd/cdrom.iso.bz2"
```

## 15.8. split

`split` 命令用于将文件分割成更小的文件。这对于将文件放入多个无法容纳整个文件的介质中非常有用。在下面的示例中，一个大小为 5000 字节的文件被分割成三个较小文件，每个最大 2000 字节。

```bash
paul@laika:~/test$ ls -l
total 8
-rw-r--r-- 1 paul 5000 2007-07-09 20:46 bigfile

paul@laika:~/test$ split -b 2000 bigfile splitfile.

paul@laika:~/test$ ls
total 20
-rw-r--r-- 1 paul 5000 2007-07-09 20:46 bigfile
-rw-r--r-- 1 paul 2000 2007-07-09 20:47 splitfile.aa
-rw-r--r-- 1 paul 2000 2007-07-09 20:47 splitfile.ab
-rw-r--r-- 1 paul 1000 2007-07-09 20:47 splitfile.ac
```
