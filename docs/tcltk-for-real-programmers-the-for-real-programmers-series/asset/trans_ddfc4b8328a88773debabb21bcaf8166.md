

## 6.3 获取过程信息

这四个信息子命令将返回有关已定义过程的信息：

- info commands `pattern`
返回名称与模式匹配的命令列表。

- info procs `pattern`
返回名称与模式匹配的程序列表。

- info body `procName`
返回程序的正体。

- info args `procName`
返回程序的参数。

`commands` 子命令将列出所有匹配通配符模式（glob pattern）的可用命令。当你调试运行在多个命名空间中的代码（在第7章中讨论）并且需要知道哪些命令定义在何处时，此命令非常。

**语法：** `info commands` `pattern`

- info commands
返回在局部和全局作用范围内匹配模式的命令列表。

- `pattern` 
一个用于尝试匹配的通配符模式。

`info body` 命令将返回程序的正体。这可以用于运行时生成和修改程序，以及在调试运行过程中生成新程序的脚本时。

**语法：** `info body` `procName`

- info body 返回程序的正体。

- `procName` 将返回正体的程序。

`info args` 命令返回程序的参数列表。同样，这在调试生成了自身程序的代码时非常有用。

**语法：** `info args` `procName`

- info args 返回程序的参数列表。

- `procName` 将返回参数的程序。

# 第6章 过程技术

下一个示例展示了如何检查一个程序是否存在，并在此基础上创建一个稍微不同的程序。

# 示例 6.3-1

# 示例脚本

```
# 定义一个简单的程序。
proc alpha {args} {
    puts "proc alpha is called with these arguments: $args"
}
# 确认程序是否存在
if {[[info commands alpha] != ""} {
    puts "There is a procedure named alpha"
}
# 从 alpha 程序获取参数列表和正体
set alphaArgs [info args alpha]
set alphaBody [info body alpha]
# 将程序体中的单词 "alpha" 修改为 "beta"
regsub "alpha" $alphaBody "beta" betaBody
# 创建一个新的程序 "beta"，它将显示其参数
proc beta $alphaArgs $betaBody
# 运行这两个程序以显示它们的行为
alpha How 'bout
beta them 'Cubs.
```

# 脚本输出

There is a procedure named alpha
proc alpha is called with these arguments: How 'bout
proc beta is called with these arguments: them 'Cubs.

## 6.4 字符串的替换与评估

## 6.4 Tcl 解释器的替换与评估

第4.2节讨论了 Tcl 解释器如何评估脚本：解释器检查一行，执行一轮命令和变量替换，然后评估生成的该行。Tcl 脚本可以访问这些解释器函数来对字符串进行替换，甚至将字符串作为命令进行评估。这是 Tcl 编程中不寻常的优势之一。大多数解释器都不允许被解释的程序访问其解析和评估部分。

提供解释器访问的两个命令是 `subst` 和 `eval`。

## 6.4.1 对字符串进行替换

`subst` 命令对字符串执行单次变量和命令替换，并返回修改后的字符串。这是命令被评估的第一个阶段，但命令的实际评估尚未发生。如果字符串包含方括号括的命令，则括号内的命令将作为替换的一部分被评估。

`subst` 命令可以在你需要将变量替换为其内容但不想将其作为命令评估时使用。下面的示例展示了如何使用 `subst` 将两个变量的内容合并到一个变量中。

语法：subst string

subst 对字符串执行一次替换操作。不评估结果。

string 要执行替换的字符串。

# 示例 6.4.1-1

# 示例脚本

```
% set x var
var
% set y name
name
% set varname "this is the test"
```

## 6.4.2 将字符串评估为 Tcl 命令

```
this is a test
% puts $(x)$(y)
$varname
% subst $(x)$(y)
this is a test
```

`eval` 命令将它的参数连接成一个字符串，然后像处理脚本中的文本一样对其进行评估。`eval` 命令允许脚本创建自己的命令行并对其进行评估。

你可以使用 `eval` 编写数据驱动的程序，这些程序可以根据可用数据有效地实现自我编写。你还可以使用 `eval` 命令编写代理风格的程序，其中一台机器上的任务将程序发送到另一台机器上的任务进行执行。这些技术（以及安全考虑因素）将在后续章节中出现时进行描述。

语法：eval arg args?

| command | 描述 |
| :--- | :--- |
| eval | 将参数评估为 Tcl 脚本。 |
| arg args? | 这些参数将连接成命令行并被评估。 |

下一个示例评估了几行文本以增加变量的值。

# 示例 6.4.2-1

示例脚本

```
set cmd(0) {set a 1}
set cmd(1) {puts "start value of A is: $a"}
set cmd(2) {incr a 3}
set cmd(3) {puts "end value of A is: $a"}
```

```
for {set i 0} {$i < 4} {incr i} {
    eval cmd($i)
}
```

## 6.5 全局和局部作用域的工作

脚本输出
start value of A is: 1
end value of A is: 4

## 6.5 全局和局部作用域的工作

Tcl 的作用域规则及其与 `upvar` 和 `uplevel` 命令的关系可能会令人困惑。本节将比之前更详细地讨论作用域以及 `upvar` 和 `uplevel`，并展示 `uplevel` 命令的行为。

这一讨论将在第7章讨论 `namespace` 命令时再次扩展。目前，命名空间（namespace）是一种用于封装和变量命名的技术。

## 6.5.1 全局和局部作用域

全局作用域是 Tcl 脚本中的主要作用域。所有未在命名空间定义的 Tcl 命令和程序都维护在这个作用范围内。所有的命名空间和程序都可以访问维护在全局作用域中的命令和变量。

任何声明全局或在程序外部的变量都维护在全局作用域中。维护在全局作用域中的变量一直持续到脚本退出或使用 `unset` 命令显式销毁。通过声明变量存在于全局作用域中，可以从任何其他作用作用域访问这些变量。在局部作用域中使用变量名之前，必须评估 `global` 命令。如果你尝试在局部作用域声明该变量，Tcl 解释器将产生错误。

```
set globalVar "I'm global"
```

```
proc goodProc {
  global globalVar

  # 下行将打印
#The globalVar contains: I'm global
puts "The globalVar contains: $globalVar"

proc badProc() {
  set globalVar "This 'globalVar' in the local scope"

  # 下行会导致错误
  globalVar


当程序被评估时，会创建一个局部作用域。变量在该作用域按需要创建，并在程序返回时销毁。程序内部使用的变量对调用的程序可见，但对栈外部的程序可见。

在程序内部定义新程序时，新程序定义在全局作用域中，并在定义它的程序返回时不会被删除。

每次程序调用另一个程序时，都会创建一个局部作用域。这些嵌套程序调用可以看作一个栈，全局作用域位于顶部，每个后续调用堆叠在之前的调用之下。

程序可以通过 `upvar` 和 `uplevel` 命令访问全局作用域或调用它的程序的作用域内的变量。`upvar` 命令将局部变量链接到之前的（较高的）栈作用域中的变量。

# 示例 6.5.1-1

# 示例脚本

```
proc top {topArg} {
  set localArg [expr $topArg+1]
  puts "Before calling bottom localArg is: $localArg"
  bottom localArg
  puts "After calling bottom, localArg is: $localArg"
}

proc bottom {bottomArg} {
```
