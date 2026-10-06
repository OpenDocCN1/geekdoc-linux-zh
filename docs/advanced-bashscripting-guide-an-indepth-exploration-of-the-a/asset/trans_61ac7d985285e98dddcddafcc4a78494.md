

# 高级 Bash 脚本指南

关于将数组传递给函数的更详细示例，请参见示例 A–8。

- 使用双括号 `()` 结构，可以使用 C 语言语法来设置和增加变量，以及在 `for` 和 `while` 循环中使用。请参见示例 10–12 和示例 10–17。
- 一种实用的脚本技术是反复将过滤器的输出（通过管道）传递给同一个过滤器，并使用不同的参数集和/或选项。如果这是 `tr` 命令，这种方法尤为适用。

```bash
# 来自 "wstrings.sh" 示例。
wlist="strings "$* | tr A-Z a-z | tr '[:space:]' Z | |
tr -cs '[[:alpha:]]' Z tr -s '\1\37\37' Z tr Z ' '
```

- `run-parts` 命令非常适合顺序执行一组命令脚本，特别是与 `cron` 或 `at` 结合使用时。
- 如果能从 shell 脚本中调用 X–Windows 组件就太好了。目前已经几个实现此功能的包，即 Xscript、Xmenu 和 widtools。其中前两个似乎较难维护。幸运的是，在这里仍然可以扩展 widtools。

![](img/1ce1edffaa36e4f698a8543e71cd3b_327_0.png)

widtools 软件包需要安装 `XForms`。此外，在典型的 Linux 系统上需要对 `Makefile` 进行一些编辑。最后，提供的六个包中有三个无法工作（实际上它们已经失效了）。

为了更有效地编写脚本，请尝试 `wish`（Tcl 的衍生品）、PerlTk（Perl 的 Tk ）、ksh（ksh 扩展）、XForms4l（Perl 的 XForms ）或 PyQt（Python 的 Qt ）。

## 34.6. 递归

脚本可以递归地调用自己。

示例 34–9. 一个递归调用自己的脚本。

```bash
#!/bin/bash
# recurse.sh

# 脚本可以递归地调用自己吗？
# 是的，但这只是“概念验证”。

RANGE=10
MAXVAL=9
i=$RANDOM  # 在 0 到 $MAXVAL 之间生成一个随机数。
```

```bash
if [ "$i" -lt "$MAXVAL" ]
then
  echo "$i = $i"
# 脚本递归地生成自身的另一个实例。
# 每个子进程执行相同的操作，直到 $i 等于 $MAXVAL
# 使用 "while" 循环代替 "if/then" 测试会导致问题。
# 解释原因。

exit 0
```

![](img/1ce1edffaa36e4f698a8543e71cd3b_328_0.png)

递归深度会耗尽脚本的栈空间，导致段错误（segfault）。

## 34.7. 可移植性问题

本书专门涉及 GNU/Linux 系统上的脚本编写。同样，sh 和 ksh 的用户将从这里获得很多价值。

事实上，许多 shell 和脚本语言似乎都在向 POSIX 1003.2 标准收敛。使用 `--posix` 选项调用 Bash 或在脚本头部插入 `-o posix` 会使 Bash 严格遵循该标准。缺乏这一措施，大多数 Bash 脚本在 ksh 下无法运行，反之亦然。由于 Chet Ratney 已将 ksh 特性推向最新的 Bash 版本，这种趋势只会加速。

## 34.8. 在 Windows 下编写脚本

运行其他操作系统的用户也可以编写类 Unix 脚本，并从本书的许多课程中受益。Cygwin 软件包和 Mortice Associates 的 MKS 工具为 Windows 增加了脚本能力。

## 35. Bash 版本 2

你机器上运行的 Bash 版本实际上是 2.XX。

```bash
bash$ echo $BASH_VERSION
2.04(1)-release
```

经典 Bash 脚本语言的这次更新增加了数组变量、以及更好的间接变量引用方法。

### 35–1. 字符串扩展

```bash
#!/bin/bash

# 字符串扩展。
# 在 Bash 版本 2 中引入。

# 形式为 $'xxx' 的字符串会解释转义字符。

echo '$Ringing bell 3 times \a \a'
echo '$Three feeds \f \f'
echo '$10 newlines \n\n\n\n\n\n\n'

exit 0
```

### 35–2. 间接引用——新方法

```bash
#!/bin/bash

# 间接变量引用。
# 这具有 C++ 引用的一些属性。

a=letter_of_alphabet
letter_of_alphabet=z

echo "a = $a"      # 直接引用。
echo "Now a = ${!a}" # 间接引用。
echo "$(variable) 表示法远优于旧方法"
t=table_cell_3
table_cell_3=387
echo "t = ${!t}"    # t = 387
echo "Value of t to ${!t}"

# 这对于引用数组成员或模拟多维数组很有用。
# 如果有索引选项就更好了 ()。
exit 0
```

### 35–3. 使用间接引用的简单数据库

```bash
#!/bin/bash
# resistor-inventory.sh
# 使用间接引用的简单数据库应用程序。

############################################
# 数据
B123_value=470                          # 欧姆
B123_powerdissip=.25                   # 瓦特
B123_colorcode="yellow-violet-brown"  # 色带
B123_loc=17                           # 位置
B123_inventory=78                      # 数量

B124_value=1000
B124_powerdissip=.25
B124_colorcode="brown-black-red"
B124_loc=24
B124_inventory=43

B125_value=10000
B125_powerdissip=.25

############################################
echo "Inventory:"
# 这里的逻辑只是为了演示间接引用
# 实际应用中会遍历变量
for i in B123 B124 B125; do
  echo "Item $i: ${!i_value} ohms, ${!i_powerdissip}W"
done
```

