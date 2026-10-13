

这个构造的真正价值在于，它允许在 `if`、`while` 和 `until` 命令中使用算术表达式。如果比较结果为假，比较运算符会将退出状态设置为非零值；如果比较结果为真，则设置为零值。因此，编写

```
(( i == 100 ))
```

可以测试 `i` 是否等于 100，并相应地设置退出状态。这使得整数算术非常适合包含在 `if` 条件中：

```
if (( i == 100 ))
then
        ...
fi
```

如果 `i` 等于 100，`(( i == 100 ))` 返回退出状态零（真），否则返回一（假），其效果与编写以下代码相同：

```
if [ "$i" -eq 100 ]
then
        ...
fi
```

使用 `((...))` 而不是 `test` 的另一个优点是能够在测试中执行算术运算：

```
if (( i / 10 != 0 ))
then
        ...
fi
```

在这里，如果 `i` 除以 10 的结果不等于零，则比较返回 TRUE。

`while` 循环也可以从整数算术中获益。例如，

```
x=0
while (( x++ < 100))
do
        commands
done
```

执行 `commands` 100 次。

## 整数类型

Korn 和 Bash shell 都支持整数数据类型。你可以使用带有 `-i` 选项的 typeset 命令将变量声明为整数：

```
typeset -i variables
```

其中 `variables` 是任何有效的 shell 变量名。也可以在声明变量时为其赋初始值：

```
typeset -i signal=1
```

主要好处：使用 `((...))` 构造对整数变量执行的算术运算比非整数值更快。

然而，整数变量只能被赋值为整数值或整数表达式。如果尝试为其赋非整数值，shell 会打印消息 `bad number`：

```sh
$ typeset -i i
$ i=hello
ksh: i: bad number
```

Bash 会简单地忽略任何不包含数值的字符串，并针对同时包含数字和其他字符的内容生成错误：

```sh
$ typeset -i i
$ i=hello
$ echo $i
0
$
$ i=1hello
bash: i: hello: value too great for base (error token is "1hello")
$ i=10+15
$ echo $i
25
$
```

前面的示例还表明，无需使用 `((...))` 构造即可将整数值表达式赋给整数变量。这两种 shell 都如此。

## 不同基数的数字

Korn 和 Bash 也都允许你以不同的数值基数执行算术运算。要在这些 shell 中以不同基数书写数字，可以使用以下表示法：

`base#number`

例如，要以 8（八进制）表示数值 100，你可以编写

`8#100`

你可以在允许整数值的任何地方以不同基数编写常量。要将八进制 100 赋给整数变量 i，你可以编写

```sh
typeset -i i=8#100
```

请注意，在 Korn shell 中，赋给整数变量的第一个值的基数会设置该变量所有后续使用的默认基数。换句话说，如果你赋给整数变量 i 的第一个值是八进制数，那么每次在命令行引用 i 的值时，Korn shell 都会使用 `8#value` 表示法将其显示为八进制数。

```sh
$ typeset -i i=8#100
$ echo $i
8#100
$ i=50
$ echo $i
8#62
$ (( i = 16#a5 + 16#120 ))
$ echo $i
8#705
$
```

因为赋给 i 的第一个值是八进制数 (8#100)，所以对 i 的所有后续引用也将是八进制。当接下来将基数为 10 的 50 赋给 i，然后再显示 i 时，我们得到值 8#62，即 50 在基数 10 下的八进制等价形式。

上面的示例中还有一个微妙之处：虽然 i 的显示值被设置为八进制，但赋给该变量的值的默认数值基数仍然是十进制，除非另有指定。换句话说，即使 shell 知道 i 将以基数 8 被引用，i=50 也不同于 i=8#50。

在前面的示例中，使用 `((...))` 构造将两个十六进制值 a5 和 120 相加。然后结果显示，同样是八进制。我们承认，这相当晦涩，不太可能在日常 shell 编程或交互式使用中遇到！

Bash 既使用 *基数#数字* 语法来表示任意基数，也使用 C 语言语法来表示八进制和十六进制数——八进制数以 0（零）开头，十六进制数以 0x 开头：

```sh
$ typeset -i i=0100
$ echo $i
64
$ i=0x80
$ echo $i
128
$ i=2#1101001
$ echo $i
105
$ (( i = 16#a5 + 16#120 ))
$ echo $i
453
$
```

与 Korn shell 不同，Bash 不会跟踪变量的数值基数；整数变量以十进制值显示。你随时可以使用 printf 以八进制或十六进制格式打印整数。

如你所见，使用 Bash 和 Korn shell 可以轻松地处理不同的基数，这使编写执行基数转换和非十进制算术的函数成为可能。

## alias 命令

别名（alias）是 shell 提供的一种简写表示法，用于实现命令自定义。shell 维护一个别名列表，在输入命令时，会在任何其他替换发生之前搜索该列表。如果命令行的第一个词是别名，它就会被别名的文本所替换。

使用 alias 命令定义别名。格式如下：

```
alias name=string
```

其中 name 是别名的名称，string 是任意字符串。例如，

```
alias ll='ls -l'
```

将 ls -l 赋值给别名 ll。现在，当用户输入命令 ll 时，shell 会静默地将其替换为 ls -l。更好的是，你可以在命令行中别名名称后面输入参数，例如

```
ll *.c
```

在执行别名替换后，它会变成这样：

```
ls -l *.c
```

shell 在设置别名和使用别名时都会执行正常的命令行处理，因此引号的使用可能会很棘手。例如，回想一下，shell 会在名为 PWD 的变量中记录你的当前工作目录：

```
$ cd /users/steve/letters
$ echo $PWD
/users/steve/letters
$
```

你可以使用 PWD 变量和参数替换构造之一，创建一个名为 dir 的别名，用于给出当前工作目录的基名：

```
alias dir="echo ${PWD##*/}"
```

这看起来合理，但让我们看看这个别名在实践中如何工作：

```
$ alias dir="echo ${PWD##*/}"    *Define alias*
$ pwd                              *Where are we?*
/users/steve
$ dir                              *Execute alias*
steve
$ cd letters                      *Change directory*
$ dir                              *Execute the alias again*
steve
$ cd /usr/spool                   *One more try*
$ dir
steve
$
```

无论当前目录是什么，`dir` 别名都会输出 steve。这是因为我们在定义 dir 别名时对引号不够小心。回想一下，shell 会在双引号内进行参数替换，问题在于 shell 在定义别名时就已经对 `${PWD##*/}` 进行了求值。这意味着 `dir` 别名本质上被定义为如同我们键入了以下内容：

```sh
$ alias dir="echo steve"
```

难怪它不生效！

解决方案是在定义 `dir` 别名时使用单引号而非双引号，将参数替换延迟到别名执行时：

```sh
$ alias dir='echo ${PWD##*/}'        Define alias
$ pwd                                  Where are we?
/users/steve
$ dir                                  Execute alias
steve
$ cd letters                           Change directory
$ dir                                  Execute alias again
letters
$ cd /usr/spool                        One more try
$ dir
spool
$
```

如果别名以空格结尾，则别名后面的单词也会被检查是否需要进行别名替换。例如：

```sh
alias nohup="/bin/nohup "
nohup ll
```

这会使 shell 在将 `nohup` 替换为 `/bin/nohup` 后，对字符串 `ll` 执行别名检查。

对命令加引号或在命令前面加上反斜杠可以防止别名替换。例如：

```sh
$ \ll
ksh: ll: command not found
$
```

### 格式

```
alias name
```

会使别名的值被列出，而不带参数的 alias 命令会使所有别名被列出。

