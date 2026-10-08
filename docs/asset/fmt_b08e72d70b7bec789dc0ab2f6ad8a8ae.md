
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
close("filename")
```

其中 `filename` 是在 `getline` 中指定的（它也可以是 `stdin`、包含文件名的变量，或与 `getline` 使用的精确命令）。

## 输出

输出有几个高级功能可用：美化格式、将输出发送到文件以及将输出通过到其他命令。`printf` 命令用于美化格式——与其查看 awk 默认选择的输出（通常很难看），不如你可以指定它的工作方式。

## printf

`print` 语句为你生成简单的输出。如果你希望能够格式化数据（例如产生固定列），则需要使用 `printf`。awk `printf` 的优越之处在于它使用的语法与 C 语言中的 `printf()` 函数非常相似。

awk `printf` 的通用格式如下（括号仅在包含关系表达式时才需要）：

```
printf format-specifier,variable1,variable2,variable3,...variables
printf(format-specifier,variable1,variable2,variable3,...variables)
```

## awk 编程

第 26 章

我个人习惯使用第二种形式，因为我习惯了用 C 语言编码。

变量是可选的，但格式符（`format-specifier`）是强制性的。你经常会只包含格式符的 `printf` 语句（用于打印不包含变量的消息）：

```
printf ("Program Starting\n")
printf ("\%") # 输出中的新页
```

格式符可以由文本、转义字符或实际的打印说明符组成。打印说明符以百分号（`%`）开头，后跟一个可选的数值用于指定字段大小，然后是格式类型（描述变量类型或输出格式）。如果你想在输出中打印百分号，请使用 `%%`。

字段大小可以由两个用小数点（`.`）分隔的数字组成。对于浮点数，第一个数字是整个字段的大小（包括小数点），第二个数字是小数点右侧位数。对于其他类型的字段，第一个数字是最小字段大小，第二个数字是最大字段大小（实际打印的字符数）；如果你省略了第一个数字，它将取最大字段大小的值。

打印说明符决定了如何打印变量；还有改变说明符行为的修饰符。表 26.9 显示了打印格式符。

### 表 26.9 awk 的格式符

| 格式 | 含义 |
| :--- | :--- |
| `%c` | ASCII 字符 |
| `%d` | 整数（十进制） |
| `%i` | 整数，与 `%d` |
| `%e` | 使用科学计数法的浮点数 (1.00000E+01) |
| `%f` | 浮点数 (10.43) |
| `%g` | awk 在 `%e` 和 `%f` 显示格式之间选择（较短的那个），并抑制不重要的零 |
| `%o` | 无符号八进制（基 8）数（整数） |
| `%s` | 字符字符串 |
| `%x` | 无符号十六进制（基 16）数（整数） |
| `%X` | 与 `%x` 相同，但使用 ABCDEF 代替 abcdef |

## 自动化、编程与系统修改

第四部分

> 注意

如果你尝试使用 `%c` 打印数值或变量，它将作为字符打印（将打印该值的 ASCII 字符）。

格式修饰符改变了格式符的默认行为。列表 26.4 显示了各种说明符和修饰符的使用。

### 列表 26.4 printf 格式符和修饰符

```
printf("%3.d %03.d %3.d %-3d\n", 64, 64, 64, 64, 64, 64, 64)
printf("%c %c %-2c %2.2c %2c %-2c\n", "abc", "abc", "abc", "abc", "abc")
printf("%2s %-2s %2s %-2s %2s %-2s\n", "abc", "abc", "abc", "abc", "abc")
printf("%6.1f %06.1f %1f %6f\n", 123.456, 123.456, 1f, 6f)
```

## awk 编程

第 26 章

除非你使用减号 (`-`) 修饰符，否则所有数值字段都是右对齐的，该修饰符会导致左对齐。

确定打印结果的最佳方法是亲自操作。尝试各种修饰符，看看你的输出呈现什么样子。

## 输出到文件

你可以将输出（来自 `print` 或 `printf`）发送到文件。以下操作创建一个新的（或清空）包含打印消息的文件：

```
printf ("hello world\n") > "datafile"
```

如果你多次执行此语句或其他将输出重定向到 `datafile` 的语句，输出将保留在文件中。文件的创建/清空只在第一次使用时发生。

要追加到现有文件，请使用以下操作：

```
printf ("hello world\n") >> "datafile"
```

## 输出到命令

除了重定向输出到文件外，你还可以将程序的输出作为另一个命令的输入。你可以编写如下代码：

```
printf ("hello world\n") | sort -t ,
```

任何其他管道数据到相同命令的输出语句都会管道符（`|`）之后指定完全相同的命令，因为这是 awk 跟踪哪个命令正在接收程序输出的方式。

## 关闭输出文件或管道

每当你将输出发送到文件或管道时，在完成数据处理后应该关闭它。awk 允许的最大文件数取决于操作系统版本或个人账户配置（管道被视作一个文件）。

关闭文件的语法简单为

```
close("filename")
```

其中 `filename` 是在输出语句中指定的（它也可以是 `stdout`、包含文件名的变量，或与管道一起使用的精确命令）。

## Functions

除了内置函数（例如 `gsub` 或 `rand`），gawk 还允许你编写自己的函数。用户定义函数是创建代码块的方法，该代码块可以在代码的多个地方被访问。这些函数还可以用于构建常用例程的库，这样你就不需要重复编写相同的算法了。

用户定义函数并不是原始 awk 的一部分——它们被添加到 nawk 中并受到 gawk 的支持。

使用函数包含两个部分：定义和调用。函数定义包含要执行的代码（函数本身），而调用则临时从主代码转移到函数。命令的执行通过两种方式传回主代码：隐式返回和显式返回。当 gawk 到达函数的末尾（右括号 `}`）时，它会自动（隐式地）将控制权返回给调用程序。如果你想在底部之前离开函数，可以显式使用 `return` 语句提前退出。

## 函数定义

gawk 函数定义的通用形式如下：

```
function functionname(parameter list) {
  the function body
}
```

你编写函数就像编写任何其他动作语句一样，你可以将其放置在任何可以放置模式/动作集的地方。如果你仔细想一下，定义中的 `function functionname(parameter list)` 部分可以被视为模式，而函数体可以视为动作。

> 注意

gawk 支持另一种函数定义形式，其中 `function` 关键字缩写为 `func`。其余语法相同：

```
func functionname(parameter list) {
  the function body
}
```

### 列表 26.5 定义和调用函数

```
BEGIN { print_header() }

function print_header( ) {
    print("This is the header\n");
    printf("this is a second line of the header\n");
}
```

This is the header

this is a second line of the header

函数内部的代码只执行一次——当在 `BEGIN` 动作内部调用该函数时。此函数使用了隐式返回方法。

> 注意

在使用用户定义函数时，调用该函数时，必须在函数名后立即放置包含参数列表的括号。当你使用内置函数时，并不是要求的。

像 C 语言一样，gawk 通过值传递参数传递给函数。也就是说，会创建原始值的副本，并将该副本传递给被调函数。即使函数更改了值，原始值也保持不变。

任何参数都列在函数定义中，并用逗号分隔。如果你没有参数，可以将参数列表（括号内）留空。

### 列表 26.6 传递参数

```
BEGIN { pageno = 0;
    print_header(pageno);
    printf("the page number is now %d\n", pageno);
}
```

### 列表 26.6 继续

```
function print_header(page) {
    page++;
    printf("This is the header for page %d\n", page);
    printf("This is a second line of the header\n");
}
```

This is the header for page 1

this is a second line of the header

the page number is now 0

页码在第一次调用 `print_header` 函数之前初始化，并在函数中递增。但在函数调用后打印时，它保持保持原始值。

> 注意

gawk 不执行参数验证。当你调用函数时，列出的参数可以比函数预期的多或少。任何多余的参数会被忽略，任何缺失的参数默认为零或空字符串（取决于如何使用它们）。

> 提示

你可以利用缺乏函数参数验证的特点。它可以用于在调用函数内部创建局部变量——只需在函数定义中列出的变量比你在函数调用中使用的变量更多。我强烈建议你注释掉额外参数实际上被用作局部变量的事实。

被调函数可以通过几种方式更改调用程序中的变量——通过显式返回或直接在调用程序中使用这些变量。（这些变量通常是全局的。）

## return 语句（显式返回）

如果你想返回一个值或提前离开函数，你需要编写一个 `return` 语句。如果你没有编写，函数将在右括号（`}`）处结束。我个人倾向于将它们写在底部。

如果调用代码期望从你的函数获得返回值，你必须在如下位置编写 `return` 语句：

`return variable`

扩展列表 26.6 以让函数更改页码，列表 26.7 显示了 `return` 语句的使用。

### 列表 26.7 返回值

```
BEGIN { pageno = 0;
  pageno = print_header(pageno);
  printf("the page number is now %d\n", pageno);
}

function print_header(page) {
  page++;
  printf("This is the header for page %d\n", page);
  printf("this is a second line of the header\n");
  return page;
}
```

This is the header for page 1

this is a second line of the header

the page number is now 0

![This is the header for page 1](img/7675a0)

this is a second line of the header

the page number is now 1

> 注意

`return` 语句允许向调用程序返回一个值。

## 编写报告

在 awk 中生成报告涉及一系列步骤，每一步都为下一步产生输入。编写报告通常是一个三步过程：选择数据、排序数据并美化输出。

## 复杂报告

使用 awk，你可以快速创建复杂的报告。执行字符串比较、动态构建数组以及利用关联数组比在任何其他语言（如 C）中编码要简单得多。与其遍历数组匹配文本键，不如将此键作为数组的下标。

我使用 awk 生成了具有三层控制分组的报告、同一个控制分组中的多个报告部分以及多个汇总页。汇总页对应每个控制分组，并有一个最终总页；如果某个控制分组没有特定类型的数据，相应的汇总页也没有。如果某个分组中只有一个成员

这份报告最终超过了 1000 行 awk 代码（具体来说是 nawk）。它比同类的 C 程序运行时间慢一点，但创建时间要短得多。因为它容易创建和修改，它是通过原型进行开发的。用户简要描述了他们想要的内容，我就生成了一份报告。他们决定需要更多的控制分组，我就添加了它们；然后他们发现他们在汇总页上浪费了大量纸张，因此修改了报告。

在不知道最终结果的情况下进行增量开发对我来说更容易也更有趣。因为我对用户的变化做出了响应，用户非常开心！

## 提取数据

正如本章早期提到的，许多系统产生的数据并不符合格式。在处理存储在关系型数据库中的数据时，有两种主要方法提取数据：使用带有 SQL 的查询工具或编写程序从数据库获取数据并按所需的格式输出。SQL 查询工具的格式化能力有限，但可以快速方便地访问数据。我发现的一种非常有用的技术是将数据从数据库提取到一个文件中，然后由 awk 脚本处理该文件以生成所需的确切格式。在需要时，awk 脚本甚至可以创建用于查询数据库的 SQL 语句（指定要选择行的键值）。

以下示例用于查询工具在数字字段前放置一个空格，而对于在另一个系统（大型机 COBOL）中使用数据的程序，必须移除该空格：

```awk
{ printf("%s%s-25.2s\n", $1, $2, $3); }
```

awk 在将输入记录拆分为单独字段时，会自动删除字段分隔符（空格字符），并且 `printf` 中的 `%s` 字符串格式说明符之间是连续的（它们之间没有空格）。

## 即时执行命令

将一个命令的输出通过管道传递给另一个的能力非常强大，因为第二个命令可以对该输出进行处理。单行 awk 程序的的一个频繁用例是基于列表创建命令。

`find` 命令可以用于生成符合条件的文件列表，也可以执行一个接受单个命令行参数的单个命令。你可以通过以下命令查看目录（及其子目录）中符合特定条件的文件：

```bash
$ find -name "*.prn" -print
```

这输出：

- .exam2.prn

- .exam1.prn

- .exam3.prn

或者，你可以使用以下命令打印这些文件的内容：

`find` 命令会将定位到的各个文件名填充到 `{}` 的位置并执行 `lp` 命令。如果你想执行一个需要两个参数的命令（将文件复制为新名称）或一次执行多个命令，仅靠 `find` 是无法做到的。你可以创建一个 shell 脚本来接受单个参数并在多处使用它，或者创建一个 awk 单行程序：

```bash
$ find -name "*.prn" -print | awk '{print echo bak $1; print "cp " $1 " " $1".bak;"}'
```

这输出：

```text
echo bak.exam2.prn
cp .exam2.prn .exam2.prn.bak
echo bak.exam1.prn
cp .exam1.prn .exam1.prn.bak
echo bak.exam3.prn
cp .exam3.prn .exam3.prn.bak
```

## 自动化、编程与系统修改

第四部分

为了让命令实际执行，你需要将命令传递到其中一个 shell 中。以下示例使用了 Korn shell；你可以使用任何你喜欢的 shell：

```bash
$ find -name ".*" -print |
awk '{print echo bak " $1; print "cp " $1 " "$1.bak";}' | 
ksh
```

这输出：

bak/.exam2.prn

bak/.exam1.prn

bak/.exam3.prn

在每次复制发生之前，都会显示信息。如果你想在多个子目录的文件中搜索字符串（使用 `grep` 命令），这也非常方便。许多版本的 `grep` 命令不会显示被搜索的文件，除非你使用通配符（或在命令行上指定多个文件名）。以下使用 `$find` 搜索 C 源文件，使用 `awk` 创建查找错误信息的 `grep` 命令，并使用 shell 命令显示正在搜索的文件：

```bash
$ find -name "*.c" -print |
awk '{print echo " $1; print "grep error-message " $1";}' |
ksh
```

相同的技术可以用于对系列子目录中的源代码进行 lint 检查（检查）。我定期在 shell 脚本中执行以下操作来检查所有 C 代码：

```bash
$ find -name "*.c" -print |
awk '{print "lint " $1" > "$1.lint";}' |
ksh
```

某个系统上的 lint 版本会将代码错误作为标题行打印，并将问题的代码部分作为列表显示在下方。`grep` 显示标题但未显示详细行。`awk` 脚本打印从标题到第一行（lint 区域结束）的所有行。

> 注意

> 虽然你不会在 Red Hat Linux 语法发行版中找到包含 lint 程序，但你可以从马萨诸理工学院（MIT）找到一个类似的（在许多方面更强大的）C 语法检查器，名为 lclint。请查看 http://sunsite.unc.edu/pub/Linux/devel/lang/c。你会发现 lclint 以及许多其他可以安装在你的 Red Hat Linux 系统上的编程工具。

在有疑问时，可以将输出传递给 `more` 或其他命令以查看创建的命令，然后再将它们传递到 shell 中执行。

## 最后一个内置函数：system

另外一个不属于字符或数字类别的内置函数是 `system`。`system` 函数执行作为参数传递给它的字符串，允许你在 awk 代码需要时即时执行命令或脚本。

你可以编写一个报告，在完成后自动打印到纸上。代码看起来类似于列表 26.8。

### 列表 26.8 使用 system 函数
