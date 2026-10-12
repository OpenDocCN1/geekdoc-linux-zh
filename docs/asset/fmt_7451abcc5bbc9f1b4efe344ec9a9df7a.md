
Mihalis Toukalos
赫尔辛基大学的管理员，曾任程序员和数学家。自 1993 年以来一直如此

# 资源

| 文本编辑器 | Gawk |
| :--- | :--- |
| | `gnu.org/software/gawk` |
| `Mawk` | `invisible-land.net/mawk` |

| 右 使用 `ERRNO` 变量使用 `extfile` 函数可以帮助你在处理多个文件时避免出现致命错误 |

# 02 AWK awks

`AWK` 按行读取输入，并将每行拆分为行字段。`AWK` 具有自动初始内置变量，还具有用于字符串、数值和时间处理的内置函数。

`NF` 包含输入记录中的字段数；每个记录可以有不同数量的字段。`FS` 是内置字段分隔符，默认定义为单个空格。此外，任何数量的前导或尾随空格都被视为空白。如果它的值不为空，那么该行中的字符将成为字段分隔符。

> 第一个 `gawk` 版本于 1986 年引入。它仍然是 `AWK` 最强大且流行的版本

只有 `END` 在不带任何额外代码的情况下读取，在 `END` 规则引用 `FNR` 或 `NR` 之前，所有指定的输入都会被读取。

`FNR` 变量用于保留仅从输入文件中读取的记录总数，跟踪到目前已读取的记录数。

# AWK 的版本

`AWK` 的原始版本在 1977 年的 `AWK` 中引入。

`Michael Bryan` 在 1986 年引入了名为 `gawk` 的 `AWK` 变体，它现在仍然是一个流行的 `AWK` 版本。

# 03 使用 BEGIN 和 END

`AWK` 拥有名为 `BEGIN` 和 `END` 的模式，每个模式都有特定的含义。注意的是，两者都只执行一次：一次在获取任何输入和处理输入之前。它们被用于设置和完成一个 `AWK` 程序。

虽然不需要在你的 `AWK` 程序之前有 `BEGIN` 规则并在末尾有 `END` 规则，但将它们放在那里被认为是一种良好实践。`AWK` 程序可以有多个 `BEGIN` 和 `END` 规则。

如果一个 `AWK` 程序只有 `BEGIN` 规则而没有其他规则且不读取任何输入，那么该 `AWK` 程序包含

# 04 使用 BEGINFILE 和 ENDFILE

两个模式具有特殊功能：`BEGINFILE` 和 `ENDFILE` —— 请注意这些仅在 `GAWK` 上有效。`BEGINFILE` 在读取第一个记录之前执行，`ENDFILE` 在处理完文件的最后一个记录后执行。

`ENDFILE` 可用于从输入文件中删除行，`AWK` 可以将控制传递给 `ENDFILE`（几乎正常停止）以及描述发生错误的 `ERNO` 变量。同样，在 `BEGINFILE` 中使用 `nextfile` 允许 `gawk` 移动到下一个数据文件，而不是带有致命错误退出且不执行 `END`。

演示通过打印文件总数以及每个项的文件名展示了它们的用法。每个代码还会报告读取文件时是否存在问题。文件名的打印是借助 `FILENAME` 变量完成的。

```
New BEGINFILE.awk
New file CANNOTREAD
Cannot read CANNOTREAD next file!
New functions.awk
New special.awk
Total number of files processed: 6
```

```
cat BEGIN.awk

# /usr/bin/gawk -f
BEGIN {
BEGINFILE {
  print "New file", FILENAME
}
# 检查在尝试读取文件时是否有错误
if (ERRNO)
}
n
```

*(注：由于原文中存在大量重复段落，此处已按要求翻译核心内容，并确保不重复原文)*

```bash
cat awkprof.out

# gawk profile, created Mon Jun 29 18:07:04 2015
# Rule(s)
5
9 {
    for (i = 1; i <= NF; i++) {
        print $1, "\t", sumTon($i)
    }
}
# Functions, listed alphabetically
9
function isnnum(x)
9 {
    return (x == x + 0)
}
9
function sumToTon(n)
9
1 {
    sum = 0
    if (n < 0) { # 1
        n = -n
    }
    if (isnum(n)) { # 6
```

# 10 对 AWK 程序进行性能分析

在这里你可以看到每行开头某个规则或语句被使用了多少次。

正在运行的主程序包含以下代码行：

> 字母变位词（anagram）使用原单词中完全相同的字母来组成新单词

- `chars += length($0) + 1`
- `lines += NF`
- `words += $NF`

这种实现是最简洁且最易理解的。尝试用 `C` 或 `Python` 编写相同的程序，以理解其真实的复杂度。

# 10 对 AWK 程序进行性能分析

你可以借助 `-profile` `gawk` 选项对 `AWK` 进行性能分析。分析的默认名为 `awk.out`。你可以使用 `-profile-anothername` 选项来更改它。将以 `functions.awk` 程序作为示例进行性能分析。要为 `functions.awk` 创建性能分析信息，你必须删除第一行并保存为 `profile.awk`，然后执行以下命令：

```bash
$ gawk -profile -f profile.awk function_input
$ -l awkprof.out
-r--r-1 mtsouk Sun Jun 29 18:07:25
awkprof.out
```

```bash
cat awkprof.out

# creating anagrams, a, i, result
function asort(x, a, result) {
    split(x, a, "")
    for (i=1; i<=length(a); i++) {
        result[i] = a[i]
    }
}
```
