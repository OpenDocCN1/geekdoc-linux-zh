
#### 在数据到达时处理数据

在这里，没有中间文件。`tee` 命令在数据到达时复制流数据。每个处理单元都获得数据的副本，并可以进行实时处理。这是一个聪明的主意，因为我们不仅在数据到达时处理它们，而且现在实现了并行处理。

在计算机科学中，我们可能会说上一个方案对问题采用了函数式方法。另一方面，接下来的方案将是纯命令式的解决方案。在这里，我们将依次读取每个标记，如果这是一个 `RED` 标记，我们就增加 `RED` 计数器；否则这是一个 `BLUE` 标记，我们就增加 `BLUE` 计数器；否则如果这是一个 `GREEN` 标记，我们就增加 `GREEN` 计数器。

这是该想法的简单 Bash 实现：

```bash
declare -i RED=0 BLUE=0

stream | while read TOKEN; do
  case "$TOKEN" in
    RED) RED+=1
    ;;
    BLUE) BLUE+=1
    ;;
    GREEN) GREEN+=1
    ;;
  esac
done

(103.2s for 10,000,000 tokens)
```

最后，作为 `Awk` 命令的忠实粉丝，我无法抵抗使用它来以一种简洁优雅的方式解决这个挑战的诱惑：

```bash
stream | awk '
/RED/ { RED++ }
/BLUE/ { BLUE++ }
/GREEN/ { GREEN++ }
END { printf "%d %d %d\n",RED,BLUE,GREEN }
'

(2.6s for 10,000,000 tokens)
```

我的 `Awk` 程序由四个规则组成：

1. 当遇到包含单词 `RED` 的行时，增加 `RED` 计数器
2. 当遇到包含单词 `BLUE` 的行时，增加 `BLUE` 计数器
3. 当遇到包含单词 `GREEN` 的行时，增加 `GREEN` 计数器
4. 在输入结束（`END`）时，显示所有计数器。

为了完全理解这一点，我们知道对于数学运算符，未初始化的变量被假设为零。

这效果非常好。但它需要重复相同的规则。在这里我们只有三个不同的标记，所以不是大问题。如果有许多标记，就会更令人麻烦。为了改进这个解决方案，我们可以依赖数组：

```bash
stream | awk '
{ C[0]++ }
END { printf "%d %d %d\n",C["RED"],C["BLUE"],C["GREEN"] }
'

(2.0s for 10,000,000 tokens)
```

然而，这里只需要两个规则，当标记数量很多时：

1. 无论读取到什么 (`$0`)，增加对应的数组单元格（这里是 `C["RED"]`、`C["BLUE"]` 或 `C["GREEN"]`）
2. 在输入结束时，显示不同标记的数组内容。

请注意，`"RED"`、`"BLUE"` 和 `"GREEN"` 现在在程序中被作为字符字符串处理（你看到它们周围的双引号了吗？）。这对于 `AWK` 来说不是问题，因为它支持关联数组。和普通变量一样，`AWK` 数组中未初始化的单元在数学运算符中也被假设为零。

正如我之前解释的那样，我选择了使用 `AWK`。但 Perl 粉丝可能对这个主题有不同意见。如果你是他们之一，会写你自己的解决方案吗？

### 挑战 12：在多个不同的文件顶部插入相同的表头

我想实现的是什么？

这次我处理多个数据文件和一个表头文件。我只想将表头内容插入到每个数据文件的顶部：

```bash
yesik:~/ItsFOSS$ head HEADER DATA01

==> HEADER <=<

# Month, Year, Est.Value

==> DATA01 <=<

Dec, 2015, 15000

Jan, 2016, 12540

Feb, 2016, 11970

yesik:~/ItsFOSS$ cat HEADER DATA01 | tee DATA01

# Month, Year, Est.Value

# Month, Year, Est.Value
```

```bash
yesik:~/ItsFOSS$ head HEADER DATA01

==> HEADER <=<

# Month, Year, Est.Value

==> DATA01 <=<

Dec, 2015, 15000

Jan, 2016, 12540

Feb, 2016, 11970
```

为了演示，我只显示了一个文件的内容。但你可以想象我有许多这样的文件——多到无法考虑手动编辑。

我以为我找到了一个使用 `cat` 命令的解决方案：

```bash
yesIk:-ItsFOSS$ cat HEADER DATA01 | tee DATA01

# Month, Year, Est.Value

# Month, Year, Est.Value
```

遗憾的是，由于某些原因，解决方案没有作用：不仅我丢失了数据，表头还出现了两次。

如你所见，我在这里需要帮助——既需要有人向我解释发生了什么，也需要帮助我解决这个问题。

### 解决方案

#### 问题所在哪里

在管道中，所有命令都是并行启动的。这意味着读取 `DATA01` 文件的 `cat` 命令和覆盖该文件的 `cat` 命令是同时启动的。

这确实是一个竞态条件。在 `cat` 命令有机会读取文件之前，`tee` 命令就已经覆盖了目标文件。为了说明这一点，我们让命令延迟：

```bash
cat HEADER DATA01 | sleep 1 | tee DATA01

# Month, Year, Est.Value

Dec, 2015, 15000

Jan, 2016, 12540

Feb, 2016, 11970
```

```bash
sleep 1 | cat HEADER DATA01 | tee DATA01

# Month, Year, Est.ValueDec, 2015, 15000

Jan, 2016, 12540

Feb, 2016, 11970
```

在这种情况下，`cat` 总是覆盖目标文件，直到 `cat` 命令有机会读取它。

#### 如何修复？

显然，没有人会使用 `sleep` 这种技巧来解决这个问题。在 POSIX 工具中，我们有很多命令可以向文件顶部插入表头。在此之前，让我们看看最基础的解决方案。

##### KISS 解决方案

```bash
cat HEADER DATA01 > DATA01.NEW

mv -f DATA01.NEW DATA01
```

我需要注释这个吗？嗯，虽然很原始，但这个解决方案有一个优点：由于我们使用了系统重命名，这种操作本身是原子的。

### 挑战 13：将文本转换为大写

#### 我尝试实现什么？

我有一个文本文件，里面包含了两次相同的句子，一次用英语写，另一次用法语写：

```
yesik.it:~/ItsFOSS$ cat text

This text should be written in all

ercase letters!

Ce text doit être affiché uniquement

en lettres majuscules!
```

我需要全大写地显示该文件的内容。你有什么想法可以完成这个任务吗？我的意思是在不需要重新输入所有文本的情况下……

### 解决方案

执行字符替换的标准工具是 `tr`，它是 transliteration（转写）。`tr` 命令接受两个参数：源字母表和目标字母表。它执行从前者到后者的一一映射。

```
yesik.it:~/ItsFOSS$ tr '[a-z]' '[A-Z]' < text

THIS TEXT SHOULD BE WRITTEN IN ALL

UPPERCASE LETTERS!

CE TEXT DOIT AFFICHÉ UNIQUEMENT

EN LETRES MAJUSCULES!
```

这有效。但只适用于 US-ASCII 字母。带重音的字母以及任何 US-ASCII 范围外的字母都没有被转换。

如果你有使用正则表达式的经验，你可能想使用字符类而不是显式范围：

> 注：`tr` 命令不使用正则表达式。但它接受一种类似于字符范围的语法来指定源和目标字母表。例如，语法 `[a-z]` 是 `abcdefghijklmnopqrstuvwxyz` 的简写。

```
yesik.it:~/ItsFOSS$ tr '[:lower:]' '[:upper:]' < text

THIS TEXT SHOULD BE WRITTEN IN ALL

UPPERCASE LETTERS!

CE TEXT DOIT être AFFICHÉ UNIQUEMENT

EN LETRES MAJUSCLES!
```

遗憾的是这效果并不更好。解决方案是显式地添加所需字符的映射：

```
yesik.it:~/ItsFOSS$ tr 'é[a-z]' 'ÉÉ[A-Z]' < text
THIS TEXT SHOULD BE WRITTEN IN ALL
UPPERCASE LETTERS!

CE TEXT DOIT ÊTRE AFFICHÉ UNIQUEMENT
EN LETRES MAJUSCLES!
```

这次成功了，但这很枯燥。特别是当你预先不知道文本文件中会出现哪些字母时。惊讶的是，`Bash` 比 `tr` 命令更适合更改字符大小：

```
yesik.it:~/ItsFOSS$ while read; do
    echo ${REPLY^^}
  done < text

THIS TEXT SHOULD BE WRITTEN IN ALL
UPPERCASE LETTERS!

CE TEXT DOIT ÊTRE AFFICHÉ UNIQUEMENT
EN LETRES MAJUSCLES!
```

在代码中，`while` 循环只是逐行读取输入文件。`Bash` `read` 命令默认将值存储在 `REPLY` 变量中。我只需要使用特殊的 `${var^^}` 符号来输出该变量，它会展开变量的内容并将字母转换为大写。

作为一个练习，你可以尝试一下 `${var,,}` 参数扩展，它的工作原理相同，但是转换为小写而不是大写。

### 挑战 14：两小时前的函数

#### 我尝试实现什么？

这次，我想让一个 shell 函数显示两个小时前的日期和时间。函数的输出必须遵循 `YYYY-MM-DD hh:mm` 格式。

我使用简单的 shell 算术得到了解决方案：

```bash
minus-two-hours() {
  date -d "$1" +%F %H:%M" | \
  IFS=":" read -a COMP
  echo "${COMP[0]} $((${10#${COMP[1]}-2)):${COMP[2]}"
}
```

正如你所看到的，该函数接受一个日期作为参数，解析它，并写回去两小时后的日期。遗憾的是，结果远不如意，因为并不总是遵循预期格式，我有时甚至得到负的小时：

```
yesik.it:~/ItsFOSS$ minus-two-hours now
2016-11-22 20:55
yesik.it:~/ItsFOSS$ minus-two-hours "2016/11/21 05:27:18"
2016-11-21 3:27
yesik.it:~/ItsFOSS$ minus-two-hours "2016/11/21 01:10:42"
2016-11-21 -1:10
```

能帮我找到一个获得预期结果的解决方案吗？

### 解决方案

算术问题比人们想象的要复杂得多。我强烈建议不要采取我最初尝试时使用的路径：永远不要自己进行日期时间计算。如果你真的需要一个理由来来说服你，可以考虑一下夏令时的问题。

尽管如此，我们还有哪些选择？任何优良的编程语言都应该具有处理特定时间问题的功能。在这里我们使用的是 `Bash`，我们必须依靠 `date` 工具来实现这一目的。

#### 如何修复？

##### 将日期转换为数量

当遇到类似的问题时，典型的解决方案是将（人类可读的）日期和时间转换为某些数值数量。

通常，我们将日期转换为自某个参考时间以来的秒数（或毫秒）。有了这个数值，我们现在可以使用经典的算术来加或减小时。最后，我们将其转换回日期格式。

在实践中，Unix 上的参考时间是 1970-01-01 00:00:00 UTC。因此我们将日期转换为秒，减去秒数，然后转换回日期格式。

```bash
minus-two-hours() {
  local seconds=$(date -d "$1" +%s)
  local new_seconds=$((seconds - 7200))
  date -d "@$new_seconds" +"%F %H:%M"
}
```

等等，上面的解决方案适用于 GNU `date`。在 macOS (BSD `date`) 上，你需要不同的语法：

```bash
minus-two-hours "2016/11/21 05:27:18"
2016-11-21 3:27
```

### 挑战 15：我的 Bash 不会计数

#### 我尝试实现什么？

我只想相加文件中存储的和最后一个整数。

```
yesik.it:001$ cat sample.data
1 2 3
yesik.it:002$ cut -d' ' -f1,3 sample.data | read X Z
yesik.it:003$ echo $X
1
yesik.it:004$ echo $((X+Z))
0
```

我的 shell 显示的结果是 0（零）。拜托，1+3 是 4，不是 0。坏了吗？

### 解决方案

感谢 Riccardo Bernard 对这个“问题”的精彩解释：第 2 行通过启动子进程执行。因此，`read` 不是在 shell 中运行，而是在子壳中运行并设置子壳变量。当执行第 3 行时，我们回到了父 shell——这里的变量从未被修改。注意这在 `zsh` 中是不同的。

要修复这个问题，可以使用进程替换或此处字符串（here string）：

```bash
read X Z < <(cut -d' ' -f1,3 sample.data)
echo $((X+Z))
4
```

或者

```bash
read X Z <<< "$(cut -d' ' -f1,3 sample.data)"
echo $((X+Z))
4
```

最后值得提到 `Bash` 并不是这类问题的最佳解决方案。一个简单的 `Awk` 程序可能会做得更好——特别是由于隐含循环允许你用完全相同的程序处理包含一行的文件和包含数千行的文件：

```bash
awk '{ print $1+$3 }' sample.data
```

### 挑战 16：在两台电脑之间发送文件

#### 我想实现什么？

我有两台连接在同一个局域网上的电脑。它们的 `IPv4` 地址分别为 `192.168.10.10` 和 `192.168.10.11`。

我想从 `192.168.10.10` 发送一个文件到 `192.168.10.11`。在已知它们没有任何文件共享服务的访问权限，且任何一个都没有启用如 `ssh` 或 `telnet` 等远程终端功能的情况下，我该如何做？

你可以假设它们之间可以互相 `ping`，并且你可以在每台主机上访问一个运行着 `Bash` 的终端。你不应该假设自己对任何一台主机拥有 `root` 权限。

显然，使用 `USB` `U` 盘等可移动存储介质是一种解决方案。但我把 `U` 盘留在家里了。而且现在是周日晚上，所有的商店都关门了。无论如何，我想寻求基于网络的解决方案！

### 解决方案

#### 问题是什么？

这里的挑战在于找到一种在主机之间开启某种网络通信通道的解决方案。然后通过该通道将文件从源主机拷贝到目标主机。

这就是像 `scp` 或客户端/服务器模式下的 `rsync` 等工具在底层使用的解决方案。但在挑战描述中，我假设这些功能不可用。

所以，我必须找到一种自己创建通信的方法。即时连接的传统工具是 `netcat`（在你的发行版中可能称为 `nc`）。`netcat` 有可能作为标准 Linux 安装的一部分被安装。所以让我们开始使用该程序吧——除非你的管理员删除了它。

#### 介绍 netcat

注意：如果你无法访问同一网络上的两台不同的电脑，你仍然可以通过在电脑上的两个不同终端进行实验，并使用 `localhost` 代替两个 `IP` 地址。

为了使用 `netcat` 在两个主机之间传输数据，你可能启动该工具的两个实例。每台主机一个。

第一个实例将打开一个端口并等待传入的请求。在目标主机上开启监听器更为直观。这就是我将做的：

```bash
#### 在目标主机上
192.168.10.11$ netcat -l 1234
```

通过这条命令，`netcat` 将打开端口 `1234`（任意数字）并等待传入的连接（选项 `-l` 表示 "listen"）。

在源主机上，我们也将使用 `netcat`，但这次是为了连接到我们刚刚打开的远程主机和端口：

```bash
#### 在源主机上
192.168.10.10$ echo hello | netcat 192.168.10.11 1234
```

按回车键，`"hello"` 消息将显示在目标主机上。

这里发生的情况可以总结为以下几步：

1. 目标 `netcat` 已打开了端口 `1234` 等待传入连接。
2. 源 `netcat` 建立了到目标主机 `192.168.10.11` 端口 `1234` 的连接。
3. 然后源 `netcat` 开始从其标准输入读取数据，并通过之前建立的连接发送数据。
4. 目标 `netcat` 在其标准输出上显示了从连接接收到的数据。
5. 在某一点，源 `netcat` 检测到没有更多数据可读并关闭了连接（遇到 `EOF` 的确切行为由 `-N` 选项控制）。
6. 目标 `netcat` 检测到连接已关闭并随之终止。

一旦你了解了这些，可以使用简单的重定向来实现文件传输：

```bash
#### 在目标主机上
192.168.10.11$ netcat -l 1234 > my.file
```

```bash
#### 在源主机上
192.168.10.10$ netcat 192.168.10.11 1234 < my.file
```

### 用 Bash 替换客户端 netcat
