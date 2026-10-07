

# 第 6 章：高级变量用法 277

typeset -i x
typeset -F x
print=$x

- i 将变量从浮点数类型改为整数类型再改回来，对其值会有什么影响（假设没有溢出）？

答案：你的交互应该如下：

```bash
[6027]: typeset -i x
[6028]: typeset -F x
[6029]: print=$x
x=1.0000000000
[6030]:
```

小数部分丢失了。小数点后有十个零，是因为如果你在使用 `typeset -F` 时提供了数字，这是默认的位数。

![](img/694fa9f0320e707804a4c650b96a09b4_296_0.png)

`float` 命令实际上是 `typeset -E` 的别名。

`typeset` 命令有几个选项，可以让你控制值的打印方式。完整列表请见附录 B“内置命令参考”。

```bash
typeset +n alpha beta gamma delta
typeset -n gamma=delta
alpha=hi
beta=bye
gamma=hello
delta=good-bye
print alpha=$alpha beta=$beta gamma=$gamma \
delta=$delta
```

- j 第一条 `typeset` 命令实现了什么？

答案：它确保变量 alpha、beta、delta 和 gamma 之间没有名称引用。

# 实验 6.1：类型化变量与作用域

# 实验
6.1

你不太会有任何名称引用，但如果你开始输入这些命令并尝试更改某些内容，可能会得到一些难以理解的错误。`+n` 会“关闭”你可能已经设置的任何名称引用，这与使用 `set +o` 关闭 shell 选项非常相似。

- k) 打印了什么？

答案：你的交互应该如下：

```bash
[6030]: typeset +n alpha gamma delta
[6031]: typeset -n gamma=delta
[6032]: alpha=bye
[6033]: beta=bye
[6034]: gamma=hello
[6035]: delta=aloha
[6036]: print alpha=$alpha beta=$beta gamma=$gamma \
delta=$delta
alpha=bye beta=bye gamma=aloha delta=aloha
[6037]:
```

在代码中，你在给 `gamma` 赋值 `hello` 之后，给 `delta` 赋值 `aloha`，所以 gamma 和 delta 的值显示 aloha。通过使用名称引用，你可以为同一个变量设置两个名字。你并不是有两个具有相同值的变量，而是只有一个两个名字的变量。图 6.1 应该有助于理解这个概念。

在图 6.1 中，变量名在左侧的框中，它们的值在右侧的框中。名字 alpha 和 beta 代表独立的变量，每个都有自己的值，但 gamma 和 delta 是两个可以用来引用同一个共享值的名称。你无法在不改变 delta 的值的情况下改变 gamma 的值，反之亦然。

# 第 6 章：高级变量用法 279

# 实验 6.1

![](img/694fa9f0320e707804a4c650b96a09b4_298_0.png)

图 6.1

## 6.1.2 答案

```bash
integer i=3 j=5 k=7
let i=i+j
(( j = j + k ))
print i=$i j=$sj
```

- a) 在 `let` 命令中，等号右边的 i 和 j 代表字符，还是变量的引用？
答案：它们是变量的引用。

如果你愿意，可以在等号右侧加上美元符号，但你不需要这样做。

# 280 实验 6.1：类型化变量与作用域

然而，如果你在等号左侧的变量名前加上美元符号，你会收到来自 shell 的错误信息，提示“赋值需要左值”（assignment requires lvalue），因为 shell 会尝试使用 i 的值作为接收赋值的变量名。“左值”是指放置在等号左侧有意义的东西，所以它必须是变量名。

![](img/694fa9f0320e707804a4c650b96a09b4_299_0.png)

- b) 在双括号命令中，等号右边的 j 和 k 代表字符，还是变量的引用？

答案：它们是变量的引用。

shell 在 `let` 和双括号命令的变量引用中不需要美元符号，因为如果省略它们，就不会产生歧义。考虑以下交互：

```bash
meat=food
((potatoes=food))
print meat=$meat potatoes=$potatoes
meat= potatoes=0
```

即使 meat 和 potatoes 都没有声明为数值变量，第二次赋值也给 potatoes 赋了值零，因为它是在双括号内执行的。

- c) 在 `let` 和双括号中，执行了什么操作？
答案：在双括号中，shell 计算括号内部的值，然后使用该值来计算表达式的其余部分。在这段代码中，打印出 56，它是 3+5（即 8）再乘以 7 的结果。

# 第 6 章：高级变量用法 300

# 第 6 章：高级变量用法 301

- d) 在双括号中，你对空格的使用观察到了什么？
答案：在双括号中，shell 计算括号内部的值，然后使用该值来计算表达式的其余部分。

- e) 双加号（++）的作用是什么？它在名字之前或之后有什么区别？
答案：你的交互应该如下：

```bash
[6037]: i=3 j=5
[6038]: (( k = i++ )); print $i k=$k
i=4 k=3
[6039]: (( k = ++j )) ; print $j k=$k
j=6 k=6
[6040]:
```

双运算符递增变量的值（加 1）。将其放在变量名左侧是在使用该变量值计算表达式之前进行递增，而将其放在变量名右侧则是在使用变量值计算表达式之后进行递增。

- f) 星号在算术表达式中用于什么？
答案：用于乘法。

- g) 括号在算术表达式中用于什么？
答案：用于覆盖优先级规则，有时为了使表达式对人类来说更易读。

- h += 等于什么？
答案：你的交互应该如下：

