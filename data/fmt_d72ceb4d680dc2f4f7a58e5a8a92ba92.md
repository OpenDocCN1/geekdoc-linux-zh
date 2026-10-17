
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

`$ mail tim ...`向本地用户 `tim` 发送一些邮件。

`Subject: 邮件测试 ...`输入邮件的主题

Hi Tim,

Amanda 怎么样了？

- with best regards from Graham

`^D ...`输入结束；标准输入作为邮件发送。

`$ _`

```
我想创建一个名为“music”的邮件组，以便我能向我乐队中的所有人发送邮件。为了实现这一点，我在主目录下创建了以下名为“.mailrc” 的文件：
```

```
group music jeff richard kelly bev
```

这使我能够按照以下方式发送邮件：

```
$ mail music ...向组中的每位成员发送邮件。

Subject: Music

Hi guys

什么时候找时间一起即兴演奏？

- with best regards from Graham.

^D ...输入结束。

$ _
```

对于长度超过几行的邮件消息，最好的做法是通过文本编辑器编写消息，将其保存到命名的文件中，然后从该文件重定向 `mail` 的输入：

```
$ mail music < jam.txt ...将 jam.txt 作为邮件发送。

$ _
```

若要向 Internet 上的用户发送邮件，请使用第 9 章描述的标准 Internet 命名方案。

```
$ glass@utdallas.edu < mesg.txt ...发送它。

$ _
```

## 读取邮件

当邮件发送给你时，它存储在一个名为 `/var/mail/<username>` 的文件中，其中 `<username>` 是你的登录名。存放邮件的文件被称为“邮件文件夹”。例如，我的收件邮件存储在 `/var/mail/glass` 邮件文件夹中。要读取邮件文件夹，输入 `mail`，后跟一个可选的文件夹指定符。如果当前没有邮件，你将收到通知：

```
$ mail ...尝试从默认文件夹读取我的邮件。

No mail for glass

$ _
```

如果存在邮件，`mail` 会显示入件邮件头的列表，并用 `&` 符号提示你。按回车键按顺序读取每条消息，按 `q`(uit) 退出邮件。你读取的邮件会被追加到主目录下的 `mbox` 邮件文件夹中，稍后可以通过在主目录输入以下命令来读取它：

```
$ mail -f mbox ...读取保存的 mbox 文件夹的内容。
```

在后续示例中，我删除了 `mail` 的一些冗余信息，以便输出空间合理。在接接的示例中，我从朋友 Tim 那里读取了两封邮件，然后退出了邮件：

```
$ ls -l /var/mail/glass ...查看邮件是否存在。

-rw----1 glass 758 May 2 14:32 /var/mail/glass

$ mail ...从默认文件夹读取邮件。

Mail version SMI 4.0 Oct 11 12:59:09 PDT 1990

Type ? 以获取帮助.

"/var/mail/glass": 2 messages 2 unheard

>U 1 tim@utdallas.edu Sat May 2 14:32 11/382 Mail test

U 2 tim@utdallas.edu Sat May 2 14:32 11/376 Another

&<Enter> ...按回车读取消息 #1。

From tim@utdallas.edu Sat Mar 14 14:32:33 1998

To: glass@utdallas.edu

Subject: Mail test

hi there

&<Enter> ...按回车读取消息 #2。

From tim@utdallas.edu Sat Mar 14 14:32:33 1998

To: glass@utdallas.edu

Subject: Mail test

hi there
```

# 第 3 章 高级用户的 UNIX 工具

## 动机

除了常见的以文件为导的 UNIX 工具外，还有许多其他处理文本、调度命令、归档文件和排序文件的工具。本章包含了对提高你工作效率最有用的工具的描述和示例。

## 先决条件

为了理解本章，你应该已经阅读了本书的前两章。如果你能够访问 UNIX 系统，将会有帮助，这样你可以尝试我讨论的各种工具。

## 目标

在本章中，我将向你展示如何使用大约 30 个实用工具。

## 介绍

本文信息将以几个示例 UNIX 会话的形式呈现。

## 工具

本章介绍了以下工具，按字母顺序排列：

```
at      crypt  gzip    tar

awk     diff    ln      time

biff    dump    mount  tr

cmp    egrep  od      ul
```

```
compress fgrep perl umount
cpio find sed uncompress
cron grep sort uniq
crontab gunzip su whoami
```

除了描述这些标准的 UNIX 工具外，本章还对 Perl 进行简要介绍。虽然它没有包含在许多 UNIX 版本中，但它已成为许多 UNIX 环境中不可或缺的一部分。

## 引言

我们将讨论的工具逻辑上分组，如图 3.1 所示。我将逐一检查每个组，描述其成员并说明它们的运行示例。请注意，虽然这些工具大部分存在于所有版本的 UNIX 中，但并非每个版本都如此。

| 章节 | 工具 |
| :--- | :--- |
| 过滤文件 | egrep, fgrep, grep, uniq |
| 排序文件 | sort |
| 比较文件 | cmp, diff |
| 归档文件 | tar, cpio, dump |
| 搜索文件 | find |
| 调度命令 | at, cron, crontab |
| 可编程文本处理 | awk, perl |
| 硬软链接 | ln |
| 切换用户 | su |
| 检查邮件 | biff |
| 转换文件 | compress, crypt, gunzip, gzip, sed, tr, ul, uncompress |
| 查看原始文件内容 | od |
| 挂载文件系统 | mount, umount |
| 识别 shell | whoami |
| 文档准备 | nroff, spell, style, troff |
| 命令执行计时 | time |

图 3.1

高级 UNIX 工具。

## 过滤文件

在很多时候，能够过滤文件的内容是非常方便的，只选择符合某些标准的行。执行此操作的工具包括：

- `egrep`, `fgrep` 和 `grep`，它们会过滤掉所有不包含指定模式的行
- `uniq`，它会过滤掉相邻的重复行

### 模式过滤：egrep/fgrep/grep

`egrep`, `fgrep` 和 `grep` 允许你扫描一个文件并过滤掉所有不包含指定模式的行。这些工具在本质上是类似的，主要的区别在于它们各能过滤的文本模式类型。我将首先描述这三者的共同特征，然后说明它们之间的区别。图 3.2 提供了这三个工具的简要概述。

```
工具: grep -hilnw pattern {fileName}*

grep -hilnw string {fileName}*

grep -hilnw pattern {fileName}*
```

`grep`（全局或获取正则表达式并打印）是一个允许你在文件列表中搜索模式的工具。如果没有指定文件，它将搜索标准输入，其中模式可以是一个正则表达式。所有匹配模式的行都作为标准输出显示。如果指定了多个文件，每个匹配行将通过其所在的文件名显示，除非 `-h` 选项导致每个匹配项前面带有其行号。`-i` 选项会忽略模式的大小写。`-l` 选项显示包含模式的文件列表。`-v` 选项导致 `grep` 显示所有不匹配模式的行。`-w` 选项将匹配限制为单词。`fgrep`（固定 grep）是带有正则表达式的 grep 快速版本。`egrep`（扩展 grep）支持使用正则表达式进行匹配。`fgrep` 还支持 `-x` 选项，它只输出与字符串完全相等的行。

关于正则表达式的更多信息，请参阅附录。

图 3.2
`grep` 命令的描述。

要获取文件中所有包含某个字符串的行列表，请在 `grep` 后面加上字符串和要扫描的文件名。这里有一个示例：

```
$ cat grepfile ...列出要过滤的文件。

你知道该睡觉了，

所以把灯关掉，

做完所有的祈祷，然后，

噢，你们这些睡睡虫做些奇妙的事吧，

美丽的人鱼将在海中畅游，

你们也会在那里游泳。

$ grepfile ...搜索单词 "the"

所以把灯关掉，

做完所有的祈祷，然后，

美丽的人鱼将在海中畅游，

你们也会在那里游泳。

-$
```

注意，包含 "string" 的单词也满足匹配内容。这里是使用 `-w` 和 `-n` 选项的示例：

```
$ -wn the grepfile ...这次更具体一点！

2:所以把灯关掉，

5:美丽的人鱼将在海中畅游，

-$
```

要只显示文件中不匹配的行，请使用 `-v` 选项，如下例所示：
