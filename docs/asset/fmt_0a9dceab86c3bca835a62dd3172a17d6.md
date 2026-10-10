
### 6.3.2.2 输出记录分隔符

整个 `print` 语句的输出被称为输出记录。每个 `print` 命令产生一个输出记录，然后输出名为记录分隔符 `ORS` 的字符串。该变量的默认值为 `\n`（换行符）。因此，每个 `print` 语句生成一行。

要更改输出字段和记录的分隔，为 `OFS` 和 `ORS` 分配新值：

```
awk { OFS=";"; ORS="\n" }
{ print $1,$2 }
record1;data1
record2;data2
```

如果 `ORS` 的值不包含换行符，程序的输出将连在一起。

### 6.3.3 记录数

内置变量 `NR` 存储已处理的记录数。它在读取新行后递增。你可以在结尾使用它统计总记录数，也可以在每个输出记录中使用：

```
cat processed.awk
BEGIN { OFS=":"; ORS="\n" }
{ print "Record number " NR $1,$2 }
END { print "Number of records: " NR }
```

```
awk -f processed.test
Record number 1:
record1-data1
Record number 2:
record2-data2
Number of records: 2
```

第 6 章。GNU awk 编程语言

### 6.3.4 用户定义变量

除了内置变量外，你还可以定义自己的。当 `awk` 遇到一个不存在（未预定义）的变量引用时，该变量将被创建并初始化为空字符串。它可以是字符串或数字。

# 初学者 Bash 指南

- 如果配额守护进程正在运行，则使用该信息；如果没有，则使用 `find`。

3. 按照以下格式从制表符分隔的列表创建 XML 风格输出：

带有大量描述的极长行

```
meaning very long line

othermeaning      more longline

testmeaning      ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong line
```

输出应该是：

```
<row>
  <entry>Meaning</entry>
  <entry>
    very long line
  </entry>
</row>
<row>
  <entry>meaning</entry>
  <entry>
    long line
  </entry>
</row>
<row>
  <entry>otherthermeaning</entry>
  <entry>
    more longline
  </entry>
</row>
<row>
  <entry>testmeaning</entry>
  <entry>
    ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooool line, but i mean re
  </entry>
</row>
```

此外，如果你了解任何 XML 知识，请编写一个 `BEGIN` 和 `END` 脚本来完成表格。

或者用 HTML 完成。

# 第 7 章 条件语句

在本章中，我们将讨论 Bash 脚本中条件语句的使用。这包括以下主题：

- `if` 语句

- 使用命令的退出状态

- 输入和文件的比较与测试

- `if/then/else` 结构

- `if/then/elif/else` 结构

- 使用和测试位置参数

- 嵌套 `if` 语句

- 布尔表达式

- 使用 `case` 语句

## 7.1. if 简介

### 7.1.1. 通用

在 shell 脚本中，你需要根据命令的成功或失败指定不同的行动方案。`if` 结构允许你指定此类条件。

`if` 命令最紧凑的语法是：

```
if TEST-COMMAND; then CONSEQUENT-COMMANDS; fi
```

执行 `TEST-COMMAND` 列表，如果它的返回状态为 `0`，则执行 `CONSEQUENT-COMMANDS` 列表。返回状态是最后执行的命令的退出状态，如果没有测试任何条件，则为 `0`。

`TEST-COMMAND` 通常涉及数值或字符串比较测试，但也可以是任何在成功时返回状态、失败时返回其他状态的命令。单元表达式通常用于检查文件的状态。如果一个主操作的 `FILE` 参数是 `/dev/fd/N`，则检查描述符 "N"。`stdin`、`stdout` 和 `stderr` 及其文件描述符可用于测试。

### 7.1.1.1. 与 if 使用的表达式

下表包含了所谓的“主操作（primaries）”，它们构成了 `TEST-COMMAND` 命令或命令列表。这些主操作被放在方括号之间，表示对条件表达式的测试。

| 主操作 | 含义 |
| --- | --- |
| `-a FILE` | 如果 `FILE` 存在则为真。 |
| `-b FILE` | 如果 `FILE` 存在且是块设备文件则为真。 |
| `-c FILE` | 如果 `FILE` 存在且是字符设备文件则为真。 |
| `-d FILE` | 如果 `FILE` 存在且是目录则为真。 |
| `-e FILE` | 如果 `FILE` 存在则为真。 |
| `-f FILE` | 如果 `FILE` 存在且是普通文件则为真。 |
| `-g FILE` | 如果 `FILE` 存在且设置了 `SGID` 位则为真。 |
| `-h FILE` | 如果 `FILE` 存在且是符号链接则为真。 |
| `-k FILE` | 如果 `FILE` 存在且设置了粘滞位则为真。 |
| `-p FILE` | 如果 `FILE` 存在且是命名文件（`FIFO`）则为真。 |
| `-r FILE` | 如果 `FILE` 存在且可读则为真。 |
| `-s FILE` | 如果 `FILE` 存在且大小大于零则为真。 |
| `-t FD` | 如果文件描述符 `FD` 已打开并指向终端则为真。 |
| `-u FILE` | 如果 `FILE` 存在且设置了 `SUID`（用户 ID）位则为真。 |
| `-w FILE` | 如果 `FILE` 存在且可写则为真。 |
| `-x FILE` | 如果 `FILE` 存在且可执行则为真。 |
| `-O FILE` | 如果 `FILE` 由有效用户 ID 所有则为真。 |
| `-G FILE` | 如果 `FILE` 由有效组 ID 所有则为真。 |
| `-L FILE` | 如果 `FILE` 存在且是符号链接则为真。 |
| `-N FILE` | 如果 `FILE` 存在且自上次记录以来已修改过则为真。 |
| `-S FILE` | 如果 `FILE` 存在且是套接字则为真。 |
| `FILE1 -nt` | 如果 `FILE1` 的修改时间新于 `FILE2`，或者 `FILE1` 存在且 `FILE2` 不存在则为真。 |
| `FILE1 -ot` | 如果 `FILE1` 比 `FILE2` 旧，或者 `FILE2` 存在且 `FILE1` 不存在则为真。 |
| `FILE1 -ef` | 如果 `FILE1` 和 `FILE2` 指向同一个设备和节点号则为真。 |
| `-o OPTIONNAME` | 如果 shell "OPTIONNAME"启用则为真。 |
| `-z STRING` | 如果 "STRING" 的长度为 `0` 则为真。 |
| `-n STRING` | 如果 "STRING" 的长度不为 `0` 则为真。 |
| `STRING1 == STRING2` | 如果字符串相等则为真。为了符合 POSIX 标准可以使用 "=" 代替 "==" |
| `STRING1 != STRING2` | 如果字符串不等则为真 |
| `STRING1 < STRING2` | 在当前区域设置中，“STRING1" 的字典排序在 "STRING2" 之前则为真。 |
| `STRING1 > STRING2` | 在当前区域设置中，“STRING1" 的字典排序在 "STRING2" 之后则为真。 |
| `ARG1 OR ARG2` | "OP" 为 `-ne`, `-lt`, `-gt` 或 `-ge`。这些算术二元运算符在 "ARG1" 分别等于、小于、小于等于、大于或大于等于 "ARG2" 时返回真，前提是 `ARG1` 和 `ARG2` 是整数。 |

可以使用以下操作符组合表达式，按优先级从高到低列出：

### 表 7–2. 组合表达式

| 运算 | 效果 |
| --- | --- |
| `! EXPR` | 如果 `EXPR` 为假则为真。 |
| `( EXPR )` | 返回 `EXPR` 的值。这可以覆盖运算符的正常优先级。 |
| `EXPR1 -a EXPR2` | 如果 `EXPR1` 和 `EXPR2` 都为真则为真。 |
| `EXPR1 -o EXPR2` | 如果 `EXPR1` 或 `EXPR2` 任一为真则为真。 |

内置的 `(or (test))` 根据参数数量的一组规则评估条件表达式。关于此主题的更多信息可以参考 Bash 文档。

## 7.1.2. if 的简单应用

### 7.1.2.1. 测试退出状态

`$?` 变量保存上一个执行的命令（最近完成的前台进程）的状态。

以下示例显示了一个简单的测试：

```
anny -> if [ $? -eq 0 ]
More input> then echo 'That was a good job'
More input> fi
That was a good job!
```

下面的示例证明了 `TEST-COMMANDS` 可以是任何返回退出状态的 UNIX 命令，如果它返回的退出状态为 `0`：

```
anny -> if ! grep $USER /etc/passwd
More input> then echo "your user account is not managed locally"; fi
your user account is not managed locally
```

```
anny -> echo $?
0
```

可以通过以下方式相同的结果：

```
anny -> grep $USER /etc/passwd
anny -> if [ $? -ne 0 ] ; then echo "not a local account"; fi
not a local account
```

### 7.1.1.3. 检查文件

第一个示例检查文件是否存在：

```
anny -> cat msgcheck.sh
This scripts checks the existence of the file.
Checking...
if [ -f /var/log/messages ]
then
    echo "/var/log/messages exists."
fi
echo
...done.
```

### 7.1.1.4. 检查 shell 选项

添加到你的 Bash 配置文件中：

```
# 这些行在设置了 noclobber 选项时打印消息。
```

环境

上面的示例在命令行执行时将有效有效：

```
anny -> if [ -o noclobber ] ; then echo ; echo "your files are protected against overwriting." ; echo ; fi
```

your files are protected against overwriting.

然而，如果你使用依赖于环境的条件测试，在脚本中输入相同的命令时可能会得到不同的结果，因为脚本会打开一个新的 shell，其中预期的变量和选项可能不会自动设置。

# 初学者 Bash指南

### 7.1.2.2. 数值比较

下面的示例使用了数值比较：

```
anny > num=`wc -l work.txt`
anny > echo $num
201

anny > if [ "$num" -gt "150" ]
then echo "you've worked hard enough for today."
else echo;
fi
```

你今天已经足够努力了。 

anny >

此脚本由 `cron` 每周日执行一次。如果该周是偶数周，它会提醒你去倒垃圾：

```bash
#!/bin/bash

# 使用 date 命令计算周数：
WEEKOFFSET=$(($(date +"%W") % 2))

# 测试是否有余数。如果没有，说明是偶数周，发送消息。
# 否则，什么都不做。

if [ $WEEKOFFSET -eq "0" ]; then
    echo "Sunday evening, put out the garbage cans." | mail -s "Garbage cans out"@your_domain
fi
```

### 7.1.2.3. 字符串比较

一个用于测试用户 ID 的字符串比较示例：

```bash
if [ "$(whoami)" != 'root' ]; then
    echo "You have no permission to run $0 as non-root user."
fi
```

在 Bash 中，你可以缩短这段逻辑。上述测试的紧凑版本如下：

```bash
[ "$(whoami)" != 'root' ] && ( echo you are using a non-privileged account; exit 1 )
```

与 `&` 表达式（表示当测试为真时执行的操作）类似，`|` 指定了当测试为假时执行的操作。

比较中也可以使用正则表达式：

```
anny > gender="female"
anny > if [[ "$gender" == * ]];
 then echo "Pleasure to meet you, Madame."; fi
Pleasure to meet you, Madame.
anny >
```

## 第 7 章. 条件语句

大多数程序员更倾向于使用 `test` 内置命令，这等同于使用方括号进行比较，如下所示：

```bash
test [ "$(whoami)" != 'root' ] && (echo you are using a non-privileged account; exit 1)
```

查看 Bash 的 `info` 页面以获取更多关于使用 "(( EXPRESSION ))" 和 "[[ EXPRESSION]]" 结构进行模式匹配的信息。

## 7.2. 更高级的 if 使用

### 7.2.1. if/then/else 结构

#### 7.2.1.1. 哑哑示例

这是一个在命令测试为真时执行一种操作、测试为假时执行另一种操作的结构。示例：

```bash
freddy scripts> gender="male"
freddy scripts> if [[ "$gender" == "female" ]];
then echo "Pleasure to meet you, Madam."
else 
echo "How the lady hasn't got a drink yet?"
fi
how the lady hasn't got a drink yet?
```

紧跟 `then` 语句的 `CONSEQUENT-COMMANDS` 列表一样，`else` 语句后面的 `ALTERNATE-CONSEQUENT-COMMANDS` 列表包含任何返回退出状态的 UNIX 风格命令。

另一个示例，来自第 7.1.2.1 节：

```bash
anny -> su -
Password:
[root@elegance root]# if grep $USER /etc/passwd 2>/dev/null
then echo "user account is not managed locally"
else 
echo "your account is managed from the local /etc/passwd file"
fi
[root@elegance root]#
your account is managed from the local /etc/passwd file
```

我们切换到 `root` 账户是为了演示 `else` 语句的效果——你的 `root` 通常是本地账户，而你的用户账户可能由中央系统（如 `LDAP`）管理。

#### 7.2.1.2. 检查参数

与其设置变量然后执行脚本，不如在命令行上放置变量值通常更为优雅。

为此目的可以使用位置参数 `$1`, `$2`, ..., `$N`。`$$` 指的是命令行参数的数量。`$0` 指的是脚本的名称。

以下是一个简单的示例：

图 7–1. 使用 `if` 测试命令行参数

```
anny@octarine:~/testdir
File Edit View Terminal Help
anny is in ~/testdir cat penguin.sh
#!/bin/bash

# 此脚本允许向 Tux 展示不同的菜单。只有在给它鱼时，
# 它才会开心。

if [ "$1" = "fish" ]; then
    echo "Hnmmmm... Tux happy!"
else
    echo "Tux don't like that. Tux wants fish!"
fi
anny is in ~/testdir penguin.sh apple
Tux don't like that. Tux wants fish!
anny is in ~/testdir penguin.sh fish
Hnmmmm fish... Tux happy!
anny is in ~/testdir
```

这是另一个示例，使用了两个参数：

```bash
anny -> cat weight.sh
#!/bin/bash

# 如果你提供体重（公斤）和身高（厘米），
# 此脚本将打印一条关于你体重的信息的信息。

weight="$1"
height="$2"
idealweight=$((height-110))

if [ $weight -le $idealweight ]; then
    echo "You should eat a bit more fat."
else
    echo "You should eat a bit more fruit."
fi
```
