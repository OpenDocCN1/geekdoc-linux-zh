
# 我们经常需要为记录文件添加文件名

列表 1-18 所示的代码显示了一个合并过程，我们遍历记录文件名列表，并在追加每个记录文件构建批处理文件时，为每个记录添加文件名。查看列表 1-18，我们将在最后讨论细节。

```bash
MERGERECORDFILE=/data/mergerecord.$(date +%m%d%y)
RECORDFILELIST=/data/branch_records.lst

while read RECORDFILENAME
do
  sed s/$/$(basename $RECORDFILENAME)/g < $RECORDFILENAME >> $MERGERECORDFILE
done < $RECORDFILELIST
```

**列表 1-18** 固定长度记录文件的合并过程代码

# 第一部分 Shell 脚本基础

逐行读取文件时，我们将一个新记录文件分配给 `RECORDFILENAME` 变量。我们在 `sed` 语句中使用这个新值，该语句会将记录文件名附加到文件中每条记录的末尾。作为最后一步，将记录文件追加到 `$MERGERECORDFILE` 的末尾。列表 1-19 展示了该技术在变长记录文件上的应用。

```bash
MERGERECORDFILE=/data/mergerecord.$(date +%m%d%y)
RECORDFILELIST=/data/branch_records.lst
FD=

while read RECORDFILENAME
do
  sed s/$($FD) $(basename $RECORDFILENAME)/g \
  $RECORDFILENAME >> $MERGERECORDFILELIST # 注意：此处保留原文逻辑
done < $RECORDFILELIST
```

**列表 1-19** 用于变长记录文件的合并过程代码

列表 1-19 是一个用于变长记录文件的合并脚本。此脚本与列表 1-18 的唯一区别在于我们添加了字段分隔符变量 `FD`。我们定义了字段分隔符，然后在记录末尾和记录文件名之间添加该分隔符。

# 字符串操作

在处理固定长度记录文件时，一个非常有用的知识点是字符串长度。可以使用以下语法找到分配给变量的字符串长度：

```bash
echo ${#VAR}
```

例如，如果我将字符串 `1234567890` 分配给变量，字符串长度应为 10：

```bash
VAR=1234567890
echo ${#VAR}
10
```

有时我们需要固定长度记录的字符串长度来填充未填满数据字段的额外空间。例如，`TOTAL` 字段定义为第 46-70 个字符，长度为 25 个字符。不太可能有人会欠这么多现金，但这就是我们必须处理的数据字段。该字段是右对齐并带有前导零的，如下所示：

```
00000000000000000000009825
```

# 第 1 章 脚本快速上手与回顾

如果我们更改了一个记录字段且数据没有数据字段那么长，我们需要用某些内容填充剩余的数据字段部分——在这种情况下是零。用前导零填充数据的“硬方法”是先检查字符串长度，然后获取新数据的长度，并开始循环在数据数据前添加正确数量的前导零。使用 `typeset` 命令完成这要简单得多。`-Z` 选项实现带有前导零的右对齐。这正是我们需要的。`TOTAL` 变量长度为 25 个字符。后续的 `typeset` 命令为我们完成了此定义：

```bash
typeset -Z25 TOTAL
```

现在我们可以将 `TOTAL` 数据字段更改为不同的值，而无需担心添加多少个前导零。作为一个例子，让我们将总额改为 0 —— 我们付清了！

```bash
TOTAL=0
echo $TOTAL
00000000000000000000000
```

`typeset` 命令可以为我们完成很多工作。表 1-11 显示了更多你可能觉得好用的 `typeset` 选项。

## 表 1-11 typeset 命令选项

| 参数 | 产生的 typeset 效果 |
| :--- | :--- |
| -L | 左对齐并移除空格。 |
| -R | 右对齐并用前导空格填充。 |
| -Zn | 右对齐到 n 长度，如果第一个非空格字符是数字，则用前导零填充。 |
| -i | 变量为整数。 |
| -l | 将大写字母转换为小写字母。 |
| -u | 将小写字母转换为大写字母。 |
| -x | 自动导出此变量。 |

> **注意**：使用 `+` 取消 `typeset` 的定义。

# 创建伪随机数

有一个内置的 shell 变量名为 `RANDOM`，它可以创建一个伪随机数。以下代码段创建了一个 1 到用户定义的上限之间的伪随机数：

```bash
RANDOM=$$ # 将种子初始化为脚本的 PID
UPPER_LIMIT=$1

RANDOM_NUMBER=$((RANDOM % $UPPER_LIMIT + 1))
echo "$RANDOM_NUMBER"
```

如果用户将 `UPPER_LIMIT` 设置为 100，结果将是 1 到 100 之间的伪随机数。

# 使用 /dev/random 和 /dev/urandom

我们可以使用 `/dev/random` 和 `/dev/urandom` 字符设备文件来产生伪随机数。直接用 `dd` 读取 `/dev/random` 和 `/dev/urandom` 字符设备文件会返回不可打印的数据。为了获取一些随机数，我们可以通过 `dd` 获取随机数。

> **注意**：原文此处逻辑混乱，已尽量翻译修正。

# 自动化 FTP 文件传输

你可以使用此处文档中编写 FTP 文件传输脚本。其基本思路如下：

```bash
ftp -i -v n wilma <<END_FTP
user randy mypassword
lcd /scripts/download
cd /scripts
get auto_ftp_xfer.sh
bye
END_FTP
```

# 使用 rsync 复制数据

我们使用 `rsync` 的方式与使用 `rcp` 和 `scp` 非常相似。这三种方法都需要源文件和目标文件或目录，并且有递归命令行开关，允许我们保存文件权限、链接、所有权等，还可以递归地复制目录结构。几个示例是学习如何使用 `rsync` 的最佳方法。让我们从这个 `rsync` 语句开始：

```bash
rsync myscript.Bash yogi:/scripts/
```

这将把当前目录下的文件 `myscript.Bash` 传输到 yogi 服务器上的 `/scripts` 目录。现在，如果 `myscript.Bash` 文件已经存在于 yogi 服务器的 `/scripts` 目录中，则将使用 `rsync` 远程更新协议通过仅发送源和目标文件之间的差异来更新文件：

```bash
rsync -avz yogi:/scripts/data /scripts/tmp
```

该 `rsync` 语句将递归地将 yogi 机器 `/scripts/data` 目录下的文件和目录传输到本地机器的 `/scripts/tmp` 目录。`-a` 选项表示归档模式，它保留权限、所有权、符号链接、属性等，并在传输过程中指定递归复制。`-z` 选项指定在传输中使用压缩，以减少传输的数据量。请注意，此示例将在本地机器上创建一个新目录 `/scripts/tmp/data`。`-v` 选项指定为详尽输出模式。

```bash
rsync -avz yogi:/scripts/data/ /scripts/tmp
```

注意源路径结尾的斜杠：`yogi:/scripts/data/`

这个结尾斜杠会改变 `rsync` 的行为，消除在目标位置创建额外的目录（上一个示例产生了：`/scripts/tmp/data`）。源端的结尾斜杠让 `rsync` 复制目录的内容，而不是复制目录本身及其所有内容。

```bash
rsync -avz /scripts/data /scripts/tmp
rsync -avz /scripts/data/ /scripts/tmp
```

如你通过这两个示例所示，你可以复制本地文件也可以复制远程文件。注意，本地文件复制没有通过 `主机名:` 符号指定主机名。

# 简单的通用 rsync Shell 脚本

一个用于 `rsync` 的简单通用 shell 脚本仅包含定义指向我们想要复制的文件/目录的变量，以及单行的 `rsync` 语句。请查看列表 1-22，我们将在末尾介绍细节。
