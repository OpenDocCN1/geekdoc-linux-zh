
除了用户定义的变量外，`bash` 还带有许多内置或预定义变量。其中许多是环境变量，例如 `$BASH_VERSION` 或 `$DIRSTACK`。预定义变量的另一个子集是位置参数，它们包含了传递给脚本的命令行参数（`shell` 函数将在稍后介绍，它们也接受参数）。参数 `"$0"` 包含脚本名称；实际参数为 `"$1"`（如果超过九个，你必须使用 `{}` 语法——例如使用 `"${10}"` 来获取其值）。传递给脚本或函数的位置参数对这些函数是只读的。然而，函数中的其他变量默认是全局的，除非你用 `local` 关键字声明它们。

`bash` 还有三个特殊的位置参数：`"$# "`、`"$0"` 和 `"$*"`。`"$# "` 的求值为传递给脚本或函数的参数数量（不包括 `"$0"`）；`"$* "` 是所有位置参数的列表（除 `"$0"` 外），格式化为单个字符串，每个参数由 `IFS` 的第一个字符分隔（`IFS` 是内部分隔符，另一个 `bash` 环境变量）。另一方面，`"$# "` 是以 `N` 个双引号字符串呈现的所有位置参数。

`"$#"` 和 `"$0"` 之间有什么区别？区别又在哪里？这种区别允许你以两种方式处理命令行参数。第一种格式 `"*"`，因为它是一个单一字符串，可以更灵活地显示，而不需要大量的 `shell` 代码。另一方面，`"$0"` 允许你单独处理每个参数，因为它的值是 `N` 个独立的参数。列表 34.2 阐了 `"$#"` 和 `"$0"` 之间的区别。

### 列表 34.2 位置参数

```bash
1 # #!/bin/bash
2 # Listing 34.2
3 # posparam.sh - 使用位置参数
4
5 ########################################
6 function cntparam
{
7
8 echo -e "inside cntparam $sh parms: $*\""
9 }
10
11 cntparam "$*"
12 cntparam "$0"
13
14 echo -e "outside cntparam $*\n"
15 echo -e "outside cntparam #\n"
```

该脚本的输出如下：

```
1 $ ./posparam.sh Kurt Roland Wall
2 inside cntparam 1 parms: Kurt Roland Wall
3 inside cntparam 3 parms: Kurt Roland Wall
5 outside cntparam Kurt Roland Wall
8 outside cntparam Kurt Roland Wall
```

第 11 行和第 12 行特别说明了位置参数 `$*` 和 `$0` 之间的实际区别。暂时将函数定义和调用视为黑盒即可。第 11 行使用 `"*"` 将位置参数作为单一字符串传递，因此 `cntparm` 报告了一个单一参数，如输出列表的第 2 行所示。然而，对 `cntparm` 的第二次调用将脚本命令行参数作为 3 个独立的字符串传递，因此 `cntparm` 报告了三个参数（第 4 行）。不过，在打印时参数的外观上并没有功能上的差异，输出的第 6 行和第 8 行清晰所示。

`echo` 命令的 `-e` 选项强制其将 `\n` 序列打印为新行（第 8、14 和 15 行）。如果你不用 `-e` 选项，请不要用 `\n` 强制换行，因为 `echo` 会自动在其输出中添加换行。

## bash 运算符

我在讨论其他主题时已经介绍了 `bash` 的许多运算符。然而，本节将让你熟悉 `bash` 的字符串和模式匹配运算符。后续章节将频繁使用这些运算符，因此现在涵盖它们将使其他章节进展得顺利。

### 字符串运算符

字符串运算符在 `bash` 文档中也称为替换运算符，用于测试变量是否未设置或为空。表 34.2 列出了这些运算符，并对每个运算符的功能进行了简单描述。

### 表 34.2 bash 字符串运算符

| 运算符 | 功能 |
| --- | --- |
| `${var:-word}` | 如果 `var` 存在且不为空，返回其值，否则返回 `word`。 |
| `${var:=word}` | 如果 `var` 存在且不为空，返回其值，否则将 `var` 设置为 `word`，然后返回其值。 |
| `${var:+word}` | 如果 `var` 存在且不为空，返回其值，否则返回 `null`。 |
| `${var?:message}` | 如果 `var` 存在且不为空，返回其值，否则显示 ``bash:$message`` 并终止当前命令或脚本。 |
| `${var:offset[:length]}` | 返回 `var` 从 `offset` 开始的长度为 `length` 的子字符串。如果省略了 `length`，将返回从 `offset` 开始的整个字符串。 |

为了说明，考虑一个初始化为 `defined` 的 `shell` 变量 `status`。将表 34.2 中的前四个字符串运算符应用于 `status` 得到的结果如下：

```
$ echo ${status:-word}
defined
$ echo ${status:=word}
defined
$ echo ${status:+word}
defined
$ echo ${status?:message}
bash: message
```

现在，考虑未设置的变量 `status`。将表 34.2 中的前四个字符串运算符应用于 `status` 得到的结果如下：

```
$ echo ${status:-word}
word
$ echo ${status:=word}
word
$ echo ${status:+word}
$ echo ${status?:message}
bash: message
```

### 模式匹配运算符

模式匹配运算符处理文件名时最有用。例如，假设你有一个名为 `myfile` 的 `shell` 变量，值为 `/usr/src/linux/Documentation/ide.txt`。使用 `/ **` 和 `/*` 作为模式，你可以模拟 `dirname` 和 `basename` 命令的行为，如 34.3 所示。

### 表 34.3 bash 模式匹配运算符

| 运算符 | 功能 |
| --- | --- |
| `${var#pattern}` | 从 `var` 的开头删除最短的 `pattern` 匹配。 |
| `${var##pattern}` | 从 `var` 的开头删除最长的 `pattern` 匹配。 |
| `${var%pattern}` | 从 `var` 的末尾删除最短的 `pattern` 匹配。 |
| `${var%%pattern}` | 从 `var` 的末尾删除最长的 `pattern` 匹配。 |
| `${var/pattern/string}` | 将 `var` 中第一个 `pattern` 匹配替换为 `string`。 |
| `${var//pattern/string}` | 将 `var` 中所有的 `pattern` 匹配替换为 `string`。 |

### 列表 34.3 模式匹配运算符

```bash
1 # #!/bin/bash
2 # Listing 34.3
3 #pattern.sh - 演示模式匹配运算符
4 ################################################
5
6 myfile=/usr/src/linux/Documentation/ide.txt
7
8 echo '${myfile##*/}' '${myfile##*/
9 echo 'basename $myfile = '$(basename $myfile)'
10
11 echo '${myfile%*}' '${myfile%*}'
12 echo 'dirname $myfile = '$(dirname $myfile)'
```

第 8 行从变量开头开始删除文件名中匹配 `*/` 的长字符串，这删除了直到最后一个斜杠之前的所有内容，只返回文件名。第 11 行从变量末尾开始匹配 `/*` 之后的任何内容，这剥离了文件名并返回文件路径。其输出如下：

```
$ ./pattern.sh
${myfile##*/} = ide.txt
basename $myfile = ide.txt
${myfile%*} = /usr/src/linux/Documentation
dirname $myfile = /usr/src/linux/Documentation
```

# 使用 GNU bash 进行 Shell 编程

第34 章

`/home/kwall/bin`

`/home/kwall/wp/wpbin`

当然，你的语句看起来会有所不同。`echo` 的 `-e` 参数告诉它将 `\n` 解释为新行，而不是字面字符串。然而，矛盾的是，你必须转义转义符 (`\n`)，才能将换行符放入变量中，以便 `echo` 对进行解释。

## 流程控制

到目前为止介绍的几个脚本都是全通过式脚本，缺乏循环和条件等控制结构。任何配得上名字的编程语言都必须具备重复执行某些代码块以及根据条件条件执行或不执行其他代码块的功能。在本节中，你将遇到 `bash` 的所有流程控制结构，包括：

- `if`—如果条件为真或为假，则执行一个或多个语句。
- `for`—以固定次数执行一个或多个语句。
- `while`—只要条件为真（或假），就一直执行一个或多个语句。
