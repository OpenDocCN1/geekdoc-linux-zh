
### 挑战 4：以 `.bat` 结尾的文件

字符集会匹配括号内的任何字符。如果你只在括号内放一个点，它只能匹配字面的点。

#### 在行末尾锚定模式

上面的三个解决方案都移除了点的特殊含义。但如何保留以 `.bat` 结尾的文件呢？再次，解决方案在于正则表达式元字符。特别是美元符号 `$` 会匹配行尾。同样，由于美元符号在 shell 中也有特殊含义，我们必须保护它免受 shell 的解释。

最终导致这些可能的解决方案：

```bash
yesik:~/ItsFOSS$ grep '\.bat$' sample.data

login.bat

first-run.bat
```

或者

```bash
yesik:~/ItsFOSS$ grep \.bat\$ sample.data

login.bat

first-run.bat
```

或者让我找第三种，也许使用括号？

### 挑战 5：懒打字者挑战

#### 我想实现什么？

我的当前工作目录下有以下内容：

```bash
yesik:~/ItsFOSS$ ls -F

archives/

report-fall-2015.pdf

report-summer-2015.pdf

report-summer-2016.pdf

report-winter-2014.pdf
```

我只想把 2016 年夏季和 2015 年秋季的报告复制到存档文件夹中。这很简单：

```bash
yesik:~/ItsFOSS$ cp report-summer-2016.pdf

yesik:~/ItsFOSS$ cp report-fall-2015.pdf archives/
```

但是，因为我很懒，我无法接受这些命令，因为它们需要 70 次按键。对我这可怜的手来说太多了！你能帮我找到一种用最少按键次数复制这些文件的方法吗？

![Image](img/8f6bf8024f58c92982eb49d5f91a7bf7_24.png)

#### 我的解决方案

对于这个挑战我不声称拥有“唯一的”解决方案。也许你可以获得比我更好的分数？如果是那样，你真的值得祝贺！

总之……
第一个最显而易见的优化是将两个命令合并为一个：

```bash
cp report-summer-2016.pdf report-fall-2015.pdf archives/
```

然后我们可以使用通配符（`glob`）来缩短每个文件名。由于只有一个“秋季”报告，这一个很容易，但对于夏季报告我们必须格外小心，因为我只对 2016 版本感兴趣：

```bash
cp report-s*-2016.pdf report-fall*.pdf archives/
```

事实上，考虑到其他文件名的结构，我可以进一步这样操作：

```bash
cp *6* *fa archives/
```

顺便说一下，我们可以对目标目录执行同样的操作——它是这里唯一的子目录：

```bash
cp *6* *fa */
```

在某些情况下，使用大括号扩展可以进一步减少所需的按键次数。但在那种情况下，我们仍然停留在 15 个字符：

```bash
cp *{6,fa} */

cp *{6,fa*,}
```

除非*你*找到了“更好”的方法？

### 挑战 6：要删除的危险文件

#### 我想实现的是什么？

当我上学校时（在 `VT10` 时代），对于那些离开终端时没有关闭会话的倒霉蛋来说，当他们回来时发现自己的主目录下出现了一些命名奇特的文件，这并不常见见。

那是由其他路过的同学们开的“恶作剧”。对于这个挑战，让我们假设你刚刚在主目录下发现了一个名为 `-rf *` 的文件：

```bash
yesik:~/ItsFOSS$ ls -1

dont remove!

-rf *

yesik:~/ItsFOSS$ 
```

```bash
yesik:~/ItsFOSS$ ls -1

dont remove!

-rf *
```

那么，如何从命令行删除这个不需要的文件，而不删除任何其他文件呢？显然，`rm -rf *` 并不是解决方案……

> **注意**：
> 在尝试回答这个挑战之前，请先思考为什么这这是一场“恶作剧”。这个文件的名称包含哪些风险？如果你先无法回答这个问题，千万不要在主目录下尝试这种操作！

#### 解决方案

这可能是你的第一个反应，但不，使用引号或反斜杠`并不是`解决方案。这些语法都是无效的：

```bash
yesik:~/ItsFOSS$ rm -rf '*'

rm: invalid option --''

Try 'rm --help' for more information.

yesik:~/ItsFOSS$ rm \rf\ '*'

rm: invalid option --'

Try 'rm --help' for more information.
```

为什么这些不是有效的解决方案呢？因为它们会保护特殊字符免受 shell 的解释。但这里的问题不在于 shell，而在于 `rm` 命令本身。

#### 如何解决？

希望 `rm` 像其他几个标准命令一样支持 `--` 特殊选项，用于指示文件名列表的开始。在 `--` 之后，命令将不再尝试将以杠开头的字符串解释为选项。这正是我们需要的：

```bash
yesik:~/ItsFOSS$ rm -- '-rf *'
```

注意，引号（或反斜杠）仍然对于保护空格和星号免受 shell 解释是必要的。如果你想进行更多实验，我鼓励你使用 `ls` 和 `touch` 命令，它们都支持 `--` 选项。而且它们使用起来比 `rm` 命令安全得多！

![Image](img/8f6bf8024f58c92982eb49d5f91a7bf7_28_0.png)

### 挑战 7：不愿离开的文件

#### 我想实现的是什么？

我被要求删除下面列表中的最后一个文件：

```bash
yesik:~/ItsFOSS$ ls -l

total 0

-rw-r--r-- 1 yesik yesik 0 Nov 23 00:41 a

-rw-r--r-- 1 yesik yesik 0 Nov 23 00:41 b

-rw-r--r-- 1 yesik yesik 0 Nov 23 00:41 c

-rw-r--r-- 1 yesik yesik 0 Nov 23 00:41 d/e

yesik:~/ItsFOSS$ rm e

rm: cannot remove 'e': No such file or directory
```

```bash
yesik:~/ItsFOSS$ ls -l

total 0

-rw-r--r-- 1 yesik yesik 0 Nov 22 22:58 a

-rw-r--r-- 1 yesik yesik 0 Nov 22 22:58 b

-rw-r--r-- 1 yesik yesik 0 Nov 22 22:58 c

-rw-r--r-- 1 yesik yesik 0 Nov 22 22:58 e

yesik:~/ItsFOSS$ rm e

rm: cannot remove 'e': No such file or directory
```

但正如你所看到的，简单的 `rm` 命令不起作用。

为什么？如何删除那个文件？

#### 解决方案

**问题出在哪里？**

你知道斜杠 `/` 不能作为文件名的一部分。你可能以某种方式认为文件 `e` 在某个子目录 `d` 中。

但那是错误的。

首先，`ls -1` 命令没有理由以这种格式显示子目录的内容。而且，从 `ls` 输出的其余部分我们可以看到，这里并没有名为 `d` 的子目录。

这是一个典型的形似字混淆（`homoglyphic confusion`）。你认为你看到了一个斜杠。但实际上它是另一个字符，只是显示了一个不幸令人困惑的字形。在特定情况下，它是 `U+2215 DIVISION SLASH` `Unicode` 字符。

![Image](img/8f6bf8024f58c92982eb49d5f91a7bf7_30_0.png)

在我的 `UTF-8` 终端上，`U+2215 DIVISION SLASH` `Unicode` 字符使用三字节序列 `0xE2 0x88 0x95` 编码。你可以使用 `hexdump` 命令进行检查（配合一点 shell 脚本以获得更可读的输出）：

| `yesik:~/ItsFOSS$ for f in *; do echo -n $f | hexdump -C; done` |
| :--- |
| `00000000 61` | `a` |
| `00000001` | |
| `00000000 62` | `b` |
| `00000001` | |
| `00000000 63` | `c` |
| `00000001` | |
| `00000000 64 e2 88 95` | `d...e` |
| `00000005` | |

如果你在系统中安装了 `iconv`，你甚至可以通过将数据转换为 `utf-16` 来找到对应的 `Unicode` 节点：

| `yesik:~/ItsFOSS$ for f in *; do echo -n $f | iconv -t utf16 hexdump -C; done` |
| :--- |
| `00000000 00 61` | `a` |
| `00000002` | |
| `00000000 00 62` | `b` |
| `00000002` | |
| `00000000 00 63` | `c` |
| `00000002` | |
| `00000000 00 64 e2 88 95` | `d...e` |

### 挑战 9：我的 Bash 无法对列数据求和

#### 我尝试实现什么？

我有一些整数数据，以固定宽文本文件的格式存储。我只想找到这些数据每列的总和。然而，文件中缺失部分数据，而这些缺失数据应该被视为 0 来计算。

遗憾的是，这些数据似乎困扰了我的 `Bash` 脚本：

```bash
yedik:~/ItsFOSS$ cat sample.data

5 3 7 2

1 -12

  0 -7

  -14 4

    15

yedik:~/ItsFOSS$ declare -i SW SX SY SZ while read W X Y Z; do

  > SW=$W; SX+=$X; SY+=$Y; SZ+=$Z

done < sample.data

yedik:~/ItsFOSS$ printf "%4d %4d %4d %4d\n" "${W,X,Y,Z}"

7 -12 7 2
```

我期望的结果是 "6 -11 7 2"。但由于某种未知原因，我的 shell 计算的前两列总和差了 1。你能修复它吗？

- 你可以假设：
  - 数据文件严格遵循我 "printf" 命令中使用的格式。
  - 最后一列是密集的（即：没有缺失值）。

**额外挑战**：
你能仅使用 `Bash` 内置命令和/或 shell 扩展来找到解决方案吗？

#### 问题出在哪里？

`Bash` 内置命令 `read` 的默认行为是丢弃行首的空格，并将行中间的一组空格视为且仅视为分隔符。

所以基本上，我们看来是固定宽的数据文件，被 `read` 命令读取时会被空格分隔的数据文件。就像如果数据文件如下：

```text
while read ; do echo $REPLY; done < sample.data

5 3 7

1 -12

0 -7

-14 4

15
```

像这样显示时，就能看出为什么第一列之和是 7 而不是我们预期的 8 了。

#### 如何修复？

我可以看到获取正确结果两种策略。首先，我只需要在空单元格中添加缺失的 0 值，这样我们每行都会读取到 4 个整数。第二种策略是在代码中强制执行固定宽度格式。

![Image](img/8f6bf8024f58c92982eb49d5f91a7bf7_38_0.png)

#### 填充缺失的零

这是上述第一种策略的可能解决方案：

```bash
declare -i SW=0 SX=0 SY=0 SZ=0

while read W X Y Z; do

  SW+=$W; SX+=$X; SY+=$Y; SZ+=$Z

done < <(sed 's/ /0/' sample.data)

printf " %4d %4d %4d %4d\n" ${W,X,Y,Z}
```

在解决方案中，每当我遇到连续 5 个空格时，就在数据中放入一个零。现在，每行都有 4 个整数，`read` 命令正确解析了数据，因此我的总和是正确的。

#### 附加问题

你可以尝试简化 `sed` 表达式吗？

为什么使用管道连接 `sed` 命令和 `while` 循环不是一个好主意？

#### 按固定位置分割数据

另一种完全不同的策略是使用所谓的 `Bash` 字符串提取，使用 `${parameter:offset:length}` 语法。这样你就可以在固定位置切分数据。但为了让它工作，我们需要第二个“技巧”：能够一次读取一整行。

要实现这一点，你需要知道 `IFS` 变量。它存储了 `Bash` 用于将一行拆分为单词的分隔符。为了一次读取一整行（即忽略任何分隔符），我们只需要将 `IFS` 设置为空字符串。

结果如下：

```bash
declare -i SW=0 SX=0 SY=0 SZ=0

while IFS=' ' read LINE; do

  SW+=${LINE:0:5}; SX+=${LINE:5:5}

  SY+=${LINE:10:5}; SZ+=${LINE:15:5}

done < sample.data

printf " %4d %4d %4d %4d\n" ${W,X,Y,Z}
```

> *你可能在另一个挑战中找到这个问题的答案……*

### 挑战 10：在 rm 中幸存留的文件

#### 我尝试实现什么？

这个挑战的描述非常短：
我在目录中有三个文件。作为 `root` 用户，我在那个目录下执行了 `rm *`。
但有一个文件固执地拒绝删除：

```bash
root:011# ls -ls

total 12

4 -rw-r--r-- 1 root root 29 nov 21:25 a

4 -rw-r--r-- 1 root root 29 nov 21:25 b

4 -rw-r--r-- 1 root root 29 nov 21:23 c

root:012# rm *

rm: cannot remove 'c': Operation not permitted

root:013# rm -f c

rm: cannot remove 'c': Operation permitted

root:014# ls -ls

total 4

4 -rw-r--r-- 1 root root 29 nov 21:23 c
```

你的挑战是找到：
1. 是什么阻止了第三个文件被删除？
2. 如何真正删除它。

![Image](img/8f6bf8024f58c92982eb49d5f91a7bf7_40.png)

### 解决方案

#### 如何复现

这里是产生此挑战的原始代码。如果你在终端中运行它，将能够重现与图中所示完全相同的结果：

```bash
cd /tmp

mkdir -p ItsFOSS

touch ItsFOSS/a ItsFOSS/b ItsFOSS/c

chattr +i ItsFOSS/c

cd ItsFOSS

rm *

rm -f c
```

#### 问题出在哪里？

为了计算这些总和，问题在于我最初尝试直接将输入发送到 `grep`，导致丢弃了部分数据。

基本上有三种方法可以解决这个问题：

- 存储流后再处理；
- 复制流并对 `RED`、`BLUE` 和 `GREEN` 分别独立处理；
- 在到达时同时处理所有情况。

为了参考，在每个解决方案之后，我提供了我在系统上观察到的真实数据。这仅供参考，必须谨慎对待。所以请进行你自己的比较！

#### 存储处理方法

存储处理策略的简单实现显而易见：

```bash
stream > stream.cache

grep -F RED < stream.cache | wc -l > RED.CNT

grep -F BLUE < stream.cache | wc -l > BLUE.CNT

grep -F GREEN < stream.cache | wc -l > GREEN.CNT

rm stream.cache
```

（10,000,000 次数据耗 1.3 秒）

它有效，但有几个缺点：我们必须在处理之前存储所有数据。此外，我们是顺序处理这三种情况。更微妙的是，如果你多次读取 `stream.cache` 文件，如果并发进程在处理期间更新了文件，可能会出现竞争条件。

仍然在存储处理范围内，这里有一个完全不同的解决方案：

```bash
stream | sort | uniq -c
```

（10,000,000 次数据耗 5.9 秒）

我认为这是一种存储处理方法，因为 `sort` 命令必须在处理它们之前读取并存储（在内存或磁盘中）所有数据。更具体地说，在我的 `Debian` 系统中，`sort` 命令会在 `/tmp` 中创建几个具有读写权限的临时文件。基本上，这个解决方案和第一个方案有相同的缺点，但性能差得多。

#### 重复流

我们真的必须在处理数据之前存储它们吗？不需要。一个更聪明的想法是将流分成几部分，在每个子流中处理一种类型的标记（`token`）：

```bash
stream | tee >(grep -F RED | wc -1 > RED.CNT) \
>(grep -F BLUE | wc -1 > BLUE.CNT) \
>(grep -F GREEN | wc -1 > GREEN.CNT) \
>/dev/null

0.8s for 10,000,000
```
