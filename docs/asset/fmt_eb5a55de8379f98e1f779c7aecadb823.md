
数据文件，包括文本文件，通常会被压缩，以便占用更少的存储空间或在更短的时间内传输。压缩（或压实）程序通常会在文件中查找冗余，然后使用一个代表性符号代替所有相同的数据片段。这样，不会丢失任何数据。

## 使用 gzip 压缩文件

Linux 使用一个名为 `gzip` 的命令，利用一种称为 Lempel-Ziv（`LZ77`）编码的算法来压缩指定文件中的数据。其语法如下：

```
$ gzip [-options] filename(s)<Enter>
```

其他类 UNIX 操作系统可能使用 `gzip` 或另一个名为 `compress` 的程序，该程序使用不同版本的 Lempel-Ziv 编码，通常与 `tar` 命令一起用于归档数据。`gzip` 命令最多可以将（ASCII）文件压缩 80%。

默认情况下，`gzip` 使用原始文件名命名压缩后的文件，但在文件名末尾附加 `.gz` 以指示它是一个压缩文件，如示例 9.16 所示。然后它会删除原始文件。同样默认地，`gzip` 将原始的所有者、权限模式以及访问和修改时间转移到新的 `.gz` 文件上。

您可以使用众多选项来增强 `gzip` 的使用或覆盖默认设置。如需完整的选项列表和说明，请查阅相关资源。表 9.3 描述了三个最实用的选项。

### 示例 9.16 使用详细（-v）选项的 gzip

唐·吉诃德在拉曼查的侄女兼管家知道唐·吉诃德和桑丘将在八月出行。她们永远无法联系到正在旅行的唐·吉诃德（她们不愿意说“当他在路上时”，因为他以前经常在碎石路和柏油路上摔倒）。因此，她们给 Juana 打电话要求一份电话簿的副本。Juana 很乐意配合。她将所有的三个 `RFL_Tel*` 文件合并为一个名为 `RFL_Phone$` 的文件，然后压缩该文件以便通过电子邮件传输。以下是她使用 `cat` 创建单个文件并使用带有 `-v`（详细）选项的 `gzip` 的方法，以便她可以看到任务已完成：

```
$ cd /home/gutie/jua/phone#<Enter>
$ cat RFL_Tel* > RFL_Phone$<Enter>
$ gzip -v RFL_Phone$<Enter>
RFL_Phone$::  58.0% --  replaced with RFL_Phone$.gz
```

| 选项 | 描述 |
| :----- | :---------- |
| -v | 详细。打印原始名称和新的压缩文件名，以及文件所经历的压缩百分比。 |
| -r | 递归。当与目录名一起使用时，对目录中的所有文件以及从该目录向下直到文件系统深处的文件执行 `gzip`。 |
| n | 压缩速度；*n* 是 1 到 9 之间的数字。1 以最快的速度执行压缩，压缩率最低。9 以最慢的速度执行压缩，产生最高的压缩率。默认值为 6。 |

## 使用 zcat 查看和操作压缩文件

下一个命令 `zcat` 用于两个目的：
- 查看压缩文件的内容，而无需经过解压缩的过程
- 将压缩文件作为一个或多个管道命令的输入

我们在示例 9.17 中为了第一个目的使用 `zcat`。`zcat` 的输出与未压缩文件的输出相同，类似于使用 `cat` 得到的结果。可以看出，`zcat` 对压缩文件的作用与其对应命令 `cat` 对未压缩文件的作用相同。与 `cat` 一样，`zcat` 不能来回翻阅文件输出。为了这个目的，您可能希望使用 `zless` 命令，其行为与 `less` 程序（参见第 5 章，“在 Linux 中使用文件”，以回顾 `less` 命令）完全相同，只是它要求压缩文件作为输入参数。`zcat` 的语法是

```
$ zcat [-options] filename(s)<Enter>
```

### 示例 9.17 使用 zcat 查看压缩文件内容

在 Juana 将电话簿文件合并为一个文件并压缩该文件之后（参见示例 9.16），在将其传输到拉曼查之前，她想检查压缩文件在内容和格式方面是否完好。她使用管道连接的 `zcat` 和 `less` 来执行此操作：

```
$ zcat RFI_Phone$.gz | less<Enter>
```

`zcat` 返回的输出类似于如果使用 `cat` 在原始未压缩文件上得到的输出。

## 使用 gunzip 解压缩文件

`gunzip` 命令解压缩已使用 `gzip` 或 `compress` 压缩的文件。基本上，`gunzip` 反转了 `gzip` 的过程，将压缩文件恢复为其原始的未压缩组件。其语法如下：

```
$ gunzip [-options] filename(s)<Enter>
```

该命令使用的大部分选项与 `gzip` 相同（请参阅你的信息源）。例如，我们将在示例 9.18 中使用 `gunzip` 的 `-v` 选项。

### 示例 9.18 gunzip

当堂吉诃德的侄女收到来自 RFI 胡安娜的电话列表（文件名：`RFI_Phones`；参见示例 9.16）后，她对其进行解压，以便阅读和打印。以下是她如何使用 `gunzip` 进行此操作的说明：

```bash
$ gunzip -v RFI_Phones.gz <Enter>
RFI_Phones.gz : 50.0% - replaced with RFI_Phones
```

> **注意** 你的 Linux 发行版中可能还提供了 `zip` 和 `unzip` 命令。你或许更喜欢使用这些命令来压缩和解压文件。

### 显示不可打印字符：cat 命令选项

在这里，我们将讨论三个选项，这些选项可以与现在大家熟悉的 `cat` 命令结合使用（有关 `cat` 的原始讨论请参见第 5 章），以确定以下内容：
- 文本文件或文件名（即目录）中是否存在不可见或无法打印的字符
- 文本文件中空格的自然特性

第二次判定可能很重要，因为 `diff` 命令的输出可能出乎意料，或者 `sort` 命令的输出可能存在问题。当某人正在撰写文档或指定文件或目录名称时，可能会意外输入某些按键序列，从而导致文档或文件/目录名称出现意外结果。例如，请查看表 9.4，其中列出了在使用 `vi` 文本编辑器时有时会输入的一些奇怪的按键序列。该表还展示了在 `vi` 中创建文件期间、在命令行下使用 `cat` 命令时以及在使用 `cat` 的 `-etv` 选项时，这些按键序列的外观。

由于使用 `cat` 时不会显示任何字符，因此我们称这些字符为不可打印字符。因此，可能无法基于目录或文件内容的典型查看方式来解决这些问题。使用这里讨论的带有相应选项的 `cat` 可能有助于确定文件内容或名称是如何创建的，从而可能有助于你确定日后如何读取或操作它们。当然，其语法与其他情况下 `cat` 的语法相同：

```bash
$ cat [-options] [file(s)] <Enter>
```

示例 9.19 中使用的选项定义见表 9.5。

| 选项 | 描述 |
|---|---|
| -e | 显示 `$` 以指示行尾按键；即 Enter 或 Return。 |
| -t | 显示 `^I` 以指示用作空格的 Tab。 |
| -v | 显示 `^G` 以指示其他不可见的 Ctrl-G 按键序列。 |

#### 示例 9.19 使用 cat 显示不可打印字符

胡安娜每天早上都会检查她的“请求”文件（`Req-K1`、`Req-K2` 和 `Req-K3`）。7 月下旬，她阅读了一条来自堂吉诃德的乱码信息：

```bash
$ cat Req-K1 <Enter>
Date: July @, 2001
   Subject: Request for Advance Funds for August Trip
Status: Urgent
Deadline: ASA
From: Quixote de

       a Mancha

need 100 Euros as an advance. For the August trip.
Sancho will requisition his own funds, etc.
zizante needs new equipment [shoes, blanket] and provisions.
Will likely leave  August     at }:3] HRS
lus, can someone make an appointment for me at Toledo spa?
now the manager?
hope this meets with your approval and
Very much appreciate your cooperation. t to . ady Dulcinea’s, too.
Signed, Q de
         a M
```

她打电话给堂先生讨论这一情况。一旦一切都满意了，她就打电话给弗雷斯顿，弗雷斯顿建议她对同一条信息执行以下操作：
