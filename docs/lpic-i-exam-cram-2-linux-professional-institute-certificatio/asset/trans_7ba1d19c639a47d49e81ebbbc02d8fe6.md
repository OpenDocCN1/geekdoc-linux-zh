
## 计数

在许多情况下，能够确定特定文件或输出中的行数或词数非常有用。`wc` 命令可以显示以下三种计数中的任意一种：

- -l—输出行数
- -w—输出词数
- -c—输出字符数（或字节数）

例如，要查看在给定时刻系统上有多少用户，一个好方法就是使用 `wc` 来统计 `who` 或 `w` 命令的输出行数：

```bash
who | wc -l
34
w | wc -l
36
```

![](img/49f4f38f3aec011238fa50f89e643db3_247_0.png)

> 这两个命令都在同一系统上执行，一个紧接着另一个执行，且用户数量相同。`w` 命令有两行标题，会被 `wc` 程序计入，而 `who` 仅为每个用户输出一行。在使用 `wc` 统计项目之前，务必先查看原始输出；否则，你可能会错误报告或呈现不准确的信息。

## 制表符

处理列式数据的位置有时很棘手。当输出为屏幕格式化时，由于每个字段中数据的长度不同，制表符分隔的文件可能会显示列位置错乱。`expand` 命令有助于将制表符转换为固定数量的空格。

假设一个文件包含以下行（行号仅供参考）：

```
1: steve johnson
2: guillermo villalobos
3: ed denzler
4: lawrence aribacus
5: marge innovera
```

如果使用制表符来分隔数据字段，第 1、3 和 5 行在字段 1 和 2 之间会有两个制表符，从而使得列对齐。第 2 和 4 行由于第一个字段的长度，只有一个制表符。`expand` 将制表符转换为固定数量的空格，使数据在大多数情况下能正确显示。

## 截取列

虽然 LPI 一级考试的目标不包括 awk 命令（列式数据之王），但它确实会测试 `cut` 命令，该命令非常擅长在两个列之间截取数据：

```
cut -c 20-40 /etc/passwd | tail -n 5
ar/spool/postfix:/bin
hare/pwn3:/bin/bash
ross brunson:/home/rb
home snuffy:/bin/bash
:/home/quota boy:/bin/
```

这仅显示 *file1* 中从第 20 列到第 40 列的内容，排除每行上的其他所有数据。

它还可以从文件中提取特定字段，例如 `/etc/passwd` 文件。要获取每个用户的用户名、描述和主目录字段，请使用以下命令：

```
cut -d: -f 1,5,6 /etc/passwd | tail -n 5
postfix::/var/spool/postfix
pvm::/usr/share/pvm3
rbrunson:ross brunson::/home/rbrunson
snuffy:::/home/snuffy
quota boy:::/home/quota boy
```

`-d` 选项设置分隔符，在本例中为 `:` 字符。默认情况下，`cut` 使用制表符作为分隔符。

## 粘贴与连接

两个功能相似的命令是 `paste` 和 `join`。`paste` 不会从输出中删除任何数据，但 `join` 会从数据中移除冗余的关键字段。

例如，假设你有以下文件：

```
file1:
Line one of file1
Line two of file1

file2:
Line one of file2
Line two of file2
```

在这两个文件上使用 "paste" 产生的输出如下：

```
Line one of file1	Line one of file2
Line two of file1	Line two of file2
```

注意，文件中没有任何内容丢失。所有数据都在那里，但如果你想从两个或更多文件生成一个联合文件，这可能是极度冗余的。

`join` 命令更像是数据库连接风格，而不是拼接风格。它接受一个文件作为第一个参数，默认将该文件的第一字段视为关键字段。第二个及后续文件也以相同方式处理。输出是按顺序显示文件中匹配的各行，但除了第一个文件外，其他文件中的冗余关键字段会被移除。

例如，假设你有以下文件，`users` 和 `location`：

`users`:
`rbrunson:500:`
`snuffy:501:`
`quotaboy:502:`

`location`:
`rbrunson			123 anystreet anytown ID 83858`
`snuffy				123 circle loop chicago IL 88888`
`quotaboy			123 some lane anyburg MT 59023`

如你所见，这些输出的结果仅包含每个文件中的独特信息，去除了 `location` 的关键字段：

```
join users location
rbrunson:500:		123 anystreet anytown ID 83858
snuffy:501:			123 circle loop chicago IL 88888
quotaboy:502:		123 some lane anyburg MT 59023
```

## 唯一数据

当你合并服务器时，需要完成的任务之一是合并 `/etc/passwd` 文件。只要每个文件中的所有用户都有相同的 UID/GID 设置，合并这些文件仍然会生成一个包含各种用户多个条目的输出文件。

例如，如果你已将三个服务器的所有 `/etc/passwd` 文件复制到单个文件中，运行以下命令将仅输出整个文件中的唯一行：

```
uniq -u /etc/bigpasswd
rbrunson:x:500:500::/home/rbrunson:/bin/bash
snuffy:x:501:501::/home/snuffy:/bin/bash
quotaboy:x:502:502::/home/quotaboy:/bin/bash
```

`-u` 选项导致仅输出文件中的唯一行，因此此处显示的命令可以通过添加重定向符号和新文件名，将输出重定向到新的 `/etc/passwd` 文件：

```
uniq -u /etc/bigpasswd > /etc/newpasswd
```

要打印文件中每个重复行的单个示例，请使用以下命令：

```
uniq -d bigpasswd
```

要打印每个重复行的所有实例，请使用此命令：

```
uniq -D bigpasswd
```

## 头部还是尾部？

`head` 命令主要用于（默认情况下）查看给定文本文件的前 10 行。可以配置 `head` 从文件顶部开始显示特定数量的行。使用 `-n` 参数后跟要显示的行数（从文件开头算起），可以显示超过默认数量的行。此参数按以下方式使用：

```
head -n 5 /etc/fstab
LABEL=/                  /
none                     /dev/pts
none                     /proc
none                     /dev/shm
/dev/hda6                swap

ext3 defaults 1 1
devpts gid=5, mode=620 0 0
proc defaults 0 0
tmpfs defaults 0 0
swap defaults 0 0
```

`head` 命令不能显示行范围，只能从文件开头显示。

`tail` 命令是 `head` 命令的完全相反：它默认显示给定文件的最后 10 行，可以配置显示较少或较多的行，但只能从文件末尾开始。它不能显示范围。这是一个示例：

```
tail -n 5 /etc/passwd
netdump:x:34:34:Network Crash Dump user:/var/crash:/bin/bash
quagga:x:92:92:Quagga routing suite:/var/run/quagga:/sbin/login
radvd:x:75:75:radvd user:://sbin/login
rbrunson:x:500:500::/home/rbrunson:/bin/bash
snuffy:x:501:501::/home/snuffy:/bin/bash
```

`tail` 命令对于跟踪日志文件也很有用，例如 `/var/log/messages` 文件，以查看最新的系统登录尝试：

```
tail -f /var/log/messages
```

这将返回类似以下显示的输出：

```
Feb 23 21:00:01 localhost sshd(pam_unix)[29358]:
session closed for user root
Feb 23 21:00:04 localhost sshd(pam_unix)[29501]:
Session opened for user root by (uid=0)
Feb 23 21:00:13 localhost sshd(pam_unix)[29501]:
Session closed for user root
Feb 23 21:00:16 localhost sshd(pam_unix)[29549]:
Session opened for user root by (uid=0)
```

当你结合这两个命令时，真正有趣的事情成为可能。例如，假设你想查看一个 50 行文件中第 31-40 行。请记住，这两个命令都不能显示范围，但通过将它们结合在一起，你可以使用以下命令显示文件 50linefile 中的一段行范围：

```
head -n 40 50linefile | tail -n 10
```

```
31 Both software and hardware watchdog drivers are available in the
32 standard
33 kernel. If you are using the software watchdog, you probably also want
34 to use "panic=60" as a boot argument as well.
35
36 The wdt card cannot be safely probed for. Instead you need to pass
37 wdt=ioaddr,irq as a boot parameter - eg "wdt=0x240,11".
38
39 The SA1100 watchdog module can be configured with the "sa1100_margin"
40 commandline argument which specifies timeout value in seconds.
```

![](img/49f4f38f3aec011238fa50f89e643db3_251_0.png)

> 在考试中注意 `head` 和 `tail` 命令，特别是用于跟踪日志文件最新条目的 `-f` 选项。

## 拆分文件

`split` 命令对于获取大量记录并将其拆分为包含特定数据量的多个独立文件非常有用。

`split` 命令的选项包括（`#` 字符代表前缀字符的数量）：

- -a #—使用指定长度的后缀（默认是 xaa）。
- -b #—输出文件将包含指定字节数的数据。
- -c #—输出文件将包含指定字节数的数据。
- -l #—输出文件将包含指定行数的数据。

