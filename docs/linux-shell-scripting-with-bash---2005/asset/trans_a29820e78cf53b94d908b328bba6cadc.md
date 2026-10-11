

将每段引用的片段用空格分隔会导致之前看到的同样问题：Bash 会将它们视为三个独立的值。

或者，可以用花括号包围变量替换中的变量名，以明确变量的起始和结束位置。

```
$ TAX_MESSAGE="The tax is ${TAX}%"
```

除了空格解释外，引号的另一个效果是不进行模式匹配。通常，例如，星号 (*) 代表当前目录中的所有文件。引号可以防止星号被替换为文件列表。

```
$ printf "%s\n" *
orders.txt
archive
calc.sh
$ printf "%s\n" "*"
*
```

要打印字符串而不解释其中的特殊字符，请使用单引号。双引号不能阻止 Bash 解释特殊字符 $、‘ 和 \，但单引号会保持所有字符不变。

```
$ printf "%s" ‘${TAX_MESSAGE}’
${TAX_MESSAGE}
```

在这种情况下，单引号阻止 Bash 将该值解释为变量替换，因为美元符号不被特殊对待。

反斜杠 (\) 就像一个字符的单引号，保持该字符不变。例如，要打印双引号，请执行以下操作：

```
$ printf "%s" "\"" 
"
```

反斜杠表示第二个引号标记应被视为字符，而不是引号对的结束引号。

printf 格式化代码 %q（引号处理）会在每个对 shell 有特殊含义的字符前打印反斜杠。使用此功能可确保空格保持不变。

```
$ printf "%q" "${TAX_MESSAGE}"
The\ tax\ is\ 7.25%
```

例如，从文件读取会受 %q 影响。如果打印的变量包含空格，除非用反斜杠保护，否则 read 会将空格视为分隔符。

```
$ printf "%q %q\n" "Alpha Systems Inc" "Key West, Florida" > company.txt
$ read COMPANY LOCATION < company.txt
$ printf "%s\n" "$COMPANY"
Alpha Systems Inc
```

```
$ printf "%s %\n" "Alpha Systems Inc" "Key West, Florida" > company.txt
$ read COMPANY LOCATION < company.txt
$ printf "%\n" "$COMPANY"
Alpha
```

read 命令不知道该行的哪些文本最初属于哪个变量。它假设值由空格分隔，并将 Alpha 分配给 COMPANY。当使用 %q 时，read 知道受反斜杠保护的空格属于第一个值，它会读取直到第一个未受保护的空格为止，从而将 Alpha Systems Inc 分配给 COMPANY。

单词拆分由特殊变量 IFS 的值控制。通常，IFS 将空格、制表符和换行符视为单词分隔符——即，它使用空白字符。如果更改 IFS 的内容，新字符将被用作单词分隔符。然而，这是为了与 Bourne shell 兼容的较旧功能，脚本不应更改 IFS 变量，因为现在有 %q 格式化等较新的功能可用。

每当分配值或用美元符号进行替换时，始终用双引号包围值是一个好习惯，以防止包含空格的值出现问题。

# 变量属性

所有 Bash 变量都存储为简单字符串。每个变量都有称为属性的特定选项，可以使用 declare 命令以类似 shell 选项和 shopt 命令的方式开启或关闭这些选项。

如果变量使用 -i（整数）开关声明，Bash 将为该变量开启整数属性。shell 会记住该字符串应作为整数值处理。如果向整型变量分配非数值，Bash 不会报告错误，而是分配值为零。

```
$ declare -i NUMBER_ACCOUNTS=15
$ printf "%d\n" "$NUMBER_ACCOUNTS"
15
$ NUMBER_ACCOUNTS="Smith"  # 错误
$ printf "%d\n" "$NUMBER_ACCOUNTS"
0
$ NUMBER_ACCOUNTS=12
$ printf "%d\n" "$NUMBER_ACCOUNTS"
12
```

有时尝试分配字符串会产生错误，但你不能依赖这种行为。

```
$ NUMBER_ACCOUNTS="Smith Account"  # 错误
bash: Smith Account: syntax error in expression (error token is `Account')
```

变量属性可以使用 `-p (print)` 开关显示。

```
$ declare -p NUMBER_ACCOUNTS
declare -i NUMBER_ACCOUNTS=\"12\"
```

信息以可以保存并在另一个脚本中使用的方式显示。这允许你在命令行提示符处尝试声明，然后在满意结果后将声明写入脚本文件。

可以使用加号关闭整数属性。

```
$ declare +i NUMBER_ACCOUNTS # 关闭整数属性
$ printf "$d\n" "$NUMBER_ACCOUNTS"
bash: printf: Smith Account: invalid number
$ printf "%s\n" "$NUMBER_ACCOUNTS"
Smith Account
```

虽然 Bash 不认为分配非数值是错误，但 `printf` 命令会报告该值无法格式化为数字。

与 `printf` 命令一样，整型变量也可以分配八进制或十六进制数字。

```
$ declare -i NUMBER_ACCOUNTS=0x0F
$ printf "%i\n" "$NUMBER_ACCOUNTS"
15
```

常量是不变的变量，使用 `-r (只读)` 属性创建。如果尝试向常量分配值，Bash 会报告错误。假设常量 `COMPANY` 包含公司名称。

```
$ declare -r COMPANY="Smith and Jones"
$ printf "%s\n" "$COMPANY"
Smith and Jones
$ COMPANY="Wilson Distribution"
bash: COMPANY: readonly variable
```

可以使用加号关闭 `readonly` 属性。然而，这可能会使脚本难以阅读，因为读者会假设只读变量始终是只读的。要么移除 `readonly` 属性，要么改变脚本结构。

# 数组

数组是使用 `-a (array)` 属性创建的值列表。一个称为*索引*的数字表示数组中项目的位置。Bash 数组与其他计算机语言中的数组不同，因为它们是开放的。数组可以是任意长度，并且初始时为空字符串填充项。

```
$ declare -a PRODUCTS
```

新项使用方括号表示列表中的位置分配给数组。第一个位置是位置零（不是一）。如果指定了初始值，则分配给第一个位置。分配一个值并不是特别有用，但为了与其他 shell 兼容而包含。或者，可以通过在方括号中包含位置将初始值分配给特定位置。

```
$ declare -a DEPT[0]="accounting" DEPT[1]="shipping" \
DEPT[2]="customer service"
```

由于使用方括号，需使用花括号界定变量名并超越 shell 的路径名匹配过程。

```
$ echo "${DEPT[0]}"
accounting
$ echo "${DEPT[2]}"
customer service
```

数组中所有未分配的位置没有值。例如，PRODUCTS 数组中的位置 5 最初是一个空字符串。可以通过赋值语句分配值 hammers。

```
$ printf "%s" "${PRODUCTS[5]}"

$ PRODUCTS[5]="hammers"
$ printf "%s" "${PRODUCTS[5]}"
hammers
```

如果位置零有项，当未指定位置时，它也返回该值。

```
$ PRODUCTS[0]="screwdrivers"
$ printf "%s" "${PRODUCTS}"
screwdrivers
$ printf "%s" "${PRODUCTS[0]}"
screwdrivers
```

可以使用星号 (*) 或 at 符号 (@) 访问整个数组的位置。这两个符号仅在双引号使用时有所不同：星号返回一个字符串，每个项由 IFS 变量的第一个字符（通常是空格）分隔，而 at 符号将每个项作为单独的字符串返回，没有分隔字符。

```
$ printf "%s" "${PRODUCTS[*]}"
screwdrivers hammers
/home/kbrutch $[bash]
$ printf "%s" "${PRODUCTS[@]}"
screwdrivershammers
```

在此示例中，at 符号版本需要两个单独的 `\s` 格式化代码才能正确显示数组，每个数组项一个。

```
$ printf "\s \s\n" "${PRODUCTS[@]}"
screwdrivers hammers
```

可以使用括号中的列表分配多个值。

```
$ DIVISIONS=("North America" "Europe" "Far East")
$ printf "%s\n" "${DIVISIONS[*]}"
North America Europe Far East
```

列表项可以有可选的下标。

```
$ DIVISIONS=([3]="North America" [2]="Europe" [1]="Far East")
$ printf "%s\n" "${DIVISIONS[*]}"
Far East Europe North America
```

结合列表和 `declare` 命令，数组可以在创建时分配值。

当在变量名前使用 `#` 且位置为 `*` 或 `@` 时，返回数组中的项目数量。项目不必连续分配，数量也不反映项目存储的位置。

```
$ printf "%s\n" "${#PRODUCTS[*]}"
2
```

可以使用 `unset` 命令删除单独的数组值。通过将数组位置分配空字符串来擦除值并不会销毁它：在计算项目时，空字符串仍被视为数组项。

`read` 命令可以使用 `-a`（数组）开关将列表读入数组。使用此开关时，输入行中的每个项都会读入单独的数组位置。

`array` 属性是唯一在开启后不能关闭的变量属性。如果 Bash 允许关闭该属性，当数组变为普通变量时，数组中的数据将会丢失。

# 导出变量和 Linux 环境

shell 变量仅存在于声明它们的脚本或交互会话中。为了使 shell 变量在其起源之外可用，必须将其声明为*可导出*。使用 `declare` 的 `-x` (*export*) 开关，通过 `export` 属性将变量标记为*可导出*。`export` 属性提醒 shell，你希望将变量“导出”或提供给脚本运行的所有程序。

例如，程序 `cvs` 需要名为 `CVSROOT` 的变量存在于其所有程序中。

```
$ declare -x CVSROOT="/home/cvs/cvsroot"
```

