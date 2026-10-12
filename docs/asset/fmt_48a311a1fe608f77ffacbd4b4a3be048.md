
```
$ declare -r COMPANY="Smith and Jones"
$ printf "%s\n" "$COMPANY"
Smith and Jones
$ COMPANY="Wilson Distribution"
bash: COMPANY: readonly variable
```

可以使用加号关闭`readonly`属性。然而，这可能会使脚本难以阅读，因为读者会假设只读变量始终是只读的。要么移除`readonly`属性，要么改变脚本结构。

## 数组

数组是使用`-a`(`array`)属性创建的值列表。一个称为*索引*的数字表示数组中项目的位置。Bash 数组与其他计算机语言中的数组不同，因为它们是开放的。数组可以是任意长度，并且初始时为空字符串填充项。

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

数组中所有未分配的位置没有值。例如，`PRODUCTS`数组中的位置 5 最初是一个空字符串。可以通过赋值语句分配值`hammers`。

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

可以使用星号(`*`)或 at 符号(`@`)访问整个数组的位置。这两个符号仅在双引号使用时有所不同：星号返回一个字符串，每个项由`IFS`变量的第一个字符（通常是空格）分隔，而 at 符号将每个项作为单独的字符串返回，没有分隔字符。

```
$ printf "%s" "${PRODUCTS[*]}"
screwdrivers hammers
/home/kbrutch $[bash]
$ printf "%s" "${PRODUCTS[@]}"
screwdrivershammers
```

在此示例中，at 符号版本需要两个单独的`\s`格式化代码才能正确显示数组，每个数组项一个。

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

结合列表和`declare`命令，数组可以在创建时分配值。

当在变量名前使用`#`且位置为`*`或`@`时，返回数组中的项目数量。项目不必连续分配，数量也不反映项目存储的位置。

```
$ printf "%s\n" "${#PRODUCTS[*]}"
2
```

可以使用`unset`命令删除单独的数组值。通过将数组位置分配空字符串来擦除值并不会销毁它：在计算项目时，空字符串仍被视为数组项。

`read`命令可以使用`-a`（数组）开关将列表读入数组。使用此开关时，输入行中的每个项都会读入单独的数组位置。

`array`属性是唯一在开启后不能关闭的变量属性。如果 Bash 允许关闭该属性，当数组变为普通变量时，数组中的数据将会丢失。

## 导出变量和 Linux 环境

shell 变量仅存在于声明它们的脚本或交互会话中。为了使 shell 变量在其起源之外可用，必须将其声明为*可导出*。使用`declare`的`-x`(*export*)开关，通过`export`属性将变量标记为*可导出*。`export`属性提醒 shell，你希望将变量“导出”或提供给脚本运行的所有程序。

例如，程序`cvs`需要名为`CVSROOT`的变量存在于其所有程序中。

```
$ declare -x CVSROOT="/home/cvs/cvsroot"
```

同样地，在你的配置文件脚本中声明的任何变量都必须被导出，否则它们在命令提示符下将不存在。在配置文件脚本运行完毕后，它们就会消失。

当变量被导出时，由脚本执行的程序所做出的任何更改都会在程序完成时被丢弃。如果第二个脚本将`CVSROOT`更改为值`/home/local/cvsroot`，当第二个脚本结束时，`CVSROOT`将再次变回`/home/cvs/cvsroot`。这些更改会被“回滚”。

通过使用导出（export）和只读（read-only）开关来创建全局常量。

```bash
$ declare -rx COMPANY_BRANCH="West Coast Branch"
```

`COMPANY_BRANCH`仅在当前脚本中是只读变量。当它被导出到第二个脚本时，它作为普通变量被导出——只读效果会丢失。这种奇怪行为的原因源于 Linux 在程序之间共享环境变量的方式，这与 Bash shell 本身无关。

*环境变量*是 Linux 在程序及其执行者之间共享的变量。就像洋葱的层一样，每个程序必须显式地将变量导出到环境中，下一个程序才能看到它。

虽然 Linux 提供了导出环境变量的机制，但没有方式为它们分配任何属性。Linux 没有属性的概念。Bash 属性是在环境变量最初发明之后才想到的。当 Bash 变量交给 Linux 与一个新程序共享时，属性会丢失。当第二个 shell 脚本开始时，它无法知道原始属性是什么。

与新程序共享的变量是原始变量的副本。如果一个脚本声明了一个导出的变量并运行第二个脚本，第二个脚本对该变量所做的任何更改对第一个脚本都是不可见的。第二个脚本没有方式将新值分配给第一个脚本能看到的变量。与其他编程语言不同，导出 shell 变量是一条单行道。

假设有两个脚本，分别称为*outer.sh*和*inner.sh*。`outer.sh`声明一个变量，然后运行`inner.sh`脚本，如清单 5.1 和 5.2 所示。

### 清单 5.1 outer.sh

```bash
# outer.sh
#
# 此脚本首先运行。

declare -rx COMPANY_BRANCH="West Coast Branch"
bash inner.sh
printf "%s\n" "$COMPANY_BRANCH"

exit 0
```

### 清单 5.2 inner.sh

```bash
# inner.sh
#
# 此脚本由 outer.sh 运行。

printf "This is the inner script.\n"

declare -p COMPANY_BRANCH
COMPANY_BRANCH="East Coast Branch"
printf "%s\n" "$COMPANY_BRANCH"

printf "Inner script finished\n"

exit 0
```

当运行`outer.sh`时，`COMPANY_BRANCH`变量是只读的。然而，在`inner.sh`内部，只读属性已丢失。`inner.sh`将变量更改为新值，但当`inner.sh`结束时，`outer.sh`显示该变量的值未变。

```bash
$ bash outer.sh
This is the inner script.
declare -x COMPANY_BRANCH="West Coast Branch"
East Coast Branch
Inner script finished
West Coast Branch
```

将值返回给调用程序的唯一方法是将值写入文件（或标准输出），然后由调用程序读取（或赋值）该值回变量。

## eval 命令
