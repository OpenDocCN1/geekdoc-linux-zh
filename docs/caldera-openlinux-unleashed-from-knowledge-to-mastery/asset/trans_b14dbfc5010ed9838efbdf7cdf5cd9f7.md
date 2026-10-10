
是相似的。我没有展示 C shell 脚本，因为同时学习两套语法只会让人困惑。此外，Bourne shell 在每个 UNIX 系统上都可用，而某些系统则缺少 C shell。

如果你对学习 C shell 编程感兴趣，请查阅 `tosh(1)` 手册页。

# awk 脚本

*awk* 是一种用于处理文本文件的语言。它是一种扫描和模式匹配语言。*awk* 逐行处理文本文件，并将每一行与模式进行匹配。如果发生匹配，就会执行相应的操作。*awk* 的强大之处在于，你可以创建特定的模式和操作来执行你所需的精确处理。

*awk* 语言由 *awk* 程序进行解释（在 Linux 系统中，则由 *gawk* 程序解释）。我会通过书写 *awk* 表示语言，而用 `awk` 表示 UNIX 命令，来区分二者。

*awk* 程序由一系列“模式-操作”语句组成：

`pattern { action }`

*awk* 的工作方式如下：

- 它从作为参数传入的所有文件名（如果没有提供文件名参数，则从标准输入）中读取行。
- 每次读取一行时，它都会扫描所有模式。任何匹配的模式都会导致其关联的操作被执行。如果多个模式匹配，操作将按照它们在 *awk* 程序中出现的顺序执行。

## awk 模式

*awk* 模式可以采取以下形式之一：

- `BEGIN`——与 `BEGIN` 关联的操作会在读取任何行之前执行。
- `END`——与 `END` 关联的操作会在读取完所有行之后执行。
- `/regexp/`——如果该行匹配正则表达式 *regexp*，则执行操作。（正则表达式在附录 A 的“正则表达式”部分中有描述。）
- `pattern1 && pattern2`——如果 *pattern1* 和 *pattern2* 都匹配，则匹配成功。
- `pattern1 || pattern2`——如果 *pattern1* 或 *pattern2* 任一匹配，则匹配成功。
- `pattern1, pattern2`——这是一个范围模式。它匹配从第一个匹配 pattern1 的行开始，到第一个匹配 pattern2 的结束（包含该行）之间的所有行。
- `expression`——匹配所有使 expression 计算结果非零的行。

还有其他形式的模式（参见 `awk(1)` 手册页），但上面列出的这些是最常见的。

## 记录和字段

当读取每一行（称为一个记录）时，*awk* 会将其分割为字段。通常，*awk* 基于空白字符来分割行。例如，行 `This is a line` 会被分割为四个字段，每个字段对应一个单词。但是，你可以使用 `awk` 的 `-F` 命令行选项来更改 *awk* 用于分割记录的策略。（当我描述如何调用 `awk` 时，会详细介绍这一点。）

每次 *awk* 分割一个记录时，它会设置某些内部变量。变量 `NF` 被设置为该记录中字段的数量。特殊记法 `$n`（其中 `n` 是整数）指代第 n 个字段，从 1 开始计数。记法 `$0` 指代整个记录。

## 调用 `awk`

以下示例是一个非常简单的 `awk` 程序：

```bash
$ awk '{print NF ": " $0}' < /etc/issue
0:
2: Caldera OpenLiux(TM)
2: Version 2.3
5: Copyright 1996-1999 Caldera Systems, Inc.
0:
0:
```

整个程序都在命令行上给出（用单引号包裹，以防止 shell 尝试进行变量插值）。

该程序没有模式部分，只有操作。在这种情况下，操作会对读取的每一行执行。

该操作由单个 `print` 语句组成，它（对于每个输入行）打印字段数量，后跟一个冒号，再后跟该行本身。该程序从标准输入读取，我将其重定向自文件 `/etc/issue`。正如你所见，`awk` 按空白字符分割行。空白行被视为零个字段。

`awk` 程序可能会变得很长且复杂。你肯定不想每次都把它们敲在命令行上。你可以将你的 `awk` 程序放入一个文本文件中，并使用 `-f` 选项调用 `awk`。它会从该文件读取脚本。

让我们来看一个较大的 `awk` 脚本。创建一个名为 `vowel.awk` 的文件，内容如下：

```awk
#!/usr/bin/awk -f

# Initialize counters
BEGIN {
    na = 0;
    ne = 0;
    ni = 0;
    no = 0;
    nu = 0;
    total = 0;
}

# Count vowels
/[Aa]/ { na = na + 1; }
/[Ee]/ { ne = ne + 1; }
/[Ii]/ { ni = ni + 1; }
/[Oo]/ { no = no + 1; }
/[Uu]/ { nu = nu + 1; }

# Add to total
{ total = total + 1; }

# Summarize results
END {
    print "Out of", total, "lines:"
    print na, "contained the letter 'A'"
    print ne, "contained the letter 'E'"
    print ni, "contained the letter 'I'"
    print no, "contained the letter 'O'"
    print nu, "contained the letter 'U'"
}
```

请注意，`awk` 将以 `#` 开头的行视为注释并忽略它们。（大多数 UNIX 脚本解释器都这样做；这使得处理 “hash-bang” 记法更容易。）

运行以下示例（可能需要几秒钟）：

```bash
$ awk -f vowel.awk < /usr/dict/words
Out of 45402 lines:
23405 contained the letter 'A'
30253 contained the letter 'E'
23873 contained the letter 'I'
17776 contained the letter 'O'
10892 contained the letter 'U'
```

注意那行 hash-bang 行 `#!/usr/bin/awk -f`。这允许你将脚本作为可执行文件运行：

```bash
$ chmod a+x ./vowel.awk
$ ./vowel.awk < /usr/dict/words
Out of 45402 lines:
...
```

## 更改字段分隔符

你可以使用 `-F` 选项更改字段分隔符。假设你想打印 `/etc/passwd` 中的全名字段。这是文件中的第五个字段，但字段是以冒号分隔的。以下 `awk` 命令可以做到这一点：

```bash
$ awk -F: '{ print $5 }' /etc/passwd
```

## 赋值变量值

你可以使用 `-v` 选项在命令行上为变量赋值。此 `awk` 命令打印 `/etc/passwd` 中的第一个字段：

```bash
$ awk -F: -v COL=1 '{ print $COL }' /etc/passwd
```

而这个示例打印第六个字段：

```bash
$ awk -F: -v COL=6 '{ print $COL }' /etc/passwd
```

注意脚本本身没有变化。唯一改变的是对 `COL` 的赋值。显然，对于如此小的示例，使用变量赋值的好处微乎其微，但对于较大的 `awk` 程序，在命令行上为变量赋值以调整其行为可能非常方便。

## 内置的 `awk` 变量

`awk` 包含一系列控制其行为或向脚本提供信息的内置变量。表 30.2 展示了一些变量。有关所有内置变量的详细信息，请参阅 `awk(1)`。

| **变量** | **含义** |
| :--- | :--- |
| ARGC | 作为命令行参数给出的文件名数量。 |
| ARGV | 从 0 到 ARGC - 1 索引的命令行文件名参数数组。 |
| ARGIND | 当前正在处理的文件在 ARGV 中的索引。 |
| FILENAME | 当前正在处理的文件的名称。对于标准输入设置为 -，在 BEGIN 块内未定义。 |
| FNR | 当前输入文件中的记录编号。记录通常对应于行，编号从 1 开始。当读取新文件时，FNR 重置为 1。 |
| FS | 输入字段分隔符（默认为空格）。如果设置为单个字符，该字符即为字段分隔符。如果设置为多字符字符串，该字符串被解释为正则表达式，任何匹配该正则表达式的字符都视为字段分隔符。 |
| NF | 当前记录中的字段数量。 |
| NR | 迄今为止读取的总记录数。读取新文件时，NR 不会重置。 |
| OFS | 输出字段分隔符，默认为空格。此字符串在 print 命令的逗号分隔参数之间打印。 |
| ORS | 输出记录分隔符，默认为换行符。这在每个 print 命令之后打印。 |
| RS | 输入记录分隔符（默认为换行符）。如果设置为单个字符，该字符即为记录分隔符。如果设置为多字符字符串，该字符串被解释为正则表达式，任何匹配该正则表达式的字符都视为记录分隔符。如果 RS 是空字符串，则空行分隔记录。 |

## 数组

除了前面示例中的简单变量外，`awk` 还支持数组变量。数组是一组完整的值集合。特定的值通过其索引访问。在许多编程语言中，数组索引必须是整数。然而，`awk` 支持允许其索引为任意字符串的关联数组。

让我们看一个例子。以下脚本使用了许多我尚未讲解的 `awk` 结构，但它是一个如何使用数组的好例子。我会详细解释每一部分。创建一个名为 `countwords.awk` 的文件，包含以下内容：

