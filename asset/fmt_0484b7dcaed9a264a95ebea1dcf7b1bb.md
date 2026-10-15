
只有当内置的 `and` 和 `or` 函数存在时，这些变量才为 `T`。在 3.81 之前的 GNU make 版本（或在像 `clearmake` 这样的模拟程序中），`have_native_and` 和 `have_native_or` 将为空，因为 GNU make 找不到名为 `and` 或 `or` 的函数，也不会找不到名为 `and T`、`T T` 或 `or T`、`T T` 的变量！

你可以使用 `ifneq` 检查这些情况的结果，并且在需要时定义你的函数，如下所示：

```make
ifneq ($(have_native_and),T)
and = $(if $1,($2,T))
endif
ifneq ($(have_native_or),T)
or = $(if $1$2,T)
```

*(注：原文后续部分似乎存在大量重复或损坏的乱码文本，已根据指令要求翻译可见逻辑部分)*

此代码段导致 `FOO` 的值为雨之前的值，因为在通过 `:=` 设置 `FOO` 时，`BAR` 还是之前的值。相比之下，

```
BAR = before
FOO = $(BAR) the rain
BAR = after
```

这导致 `FOO` 的值为 `$(BAR)`，而 `rain` 在雨之后求值。这是因为 `=` 定义了一个递归变量（可以使用 `()` 或 `$()` 语法引用其他变量的变量），其值在每次使用该变量时都会确定。相比之下，使用 `:=` 定义的简单变量在定义时通过展开所有变量引用确定了一个单一的固定值。

- 简单变量有一个明显的优势，因为它们是固定的字符串，不需要每次使用都进行展开。它们用起来可能很棘手，因为 Makefile 编写者通常假设变量可以按任何顺序设置，而递归变量（使用 `=` 的变量）只有在被使用时才会获得最终值。尽管如此，简单变量的访问通常比递归变量快，如果可以的话，我倾向于使用 `:=`。

但如果你能兼顾两者的优点呢？变量只在第一次使用时获取，但会被设置为一个不再改变固定值。如果一个变量需要大量计算，但最多只需要计算一次，如果该变量从未被使用则可能不需要计算，那么使用 `$(eval)` 函数就可以实现这一点。

考虑以下定义：

```
SHALIST = $(shell find -name '*.c' | xargs shasum)
```

`SHALIST` 变量将包含当前目录及所有子目录下 `.c` 文件的名称和 SHA1 加密哈希值。这可能需要很长时间来评估。使用 `=` 定义 `SHALIST` 意味着每次使用 `SHALIST` 时都会发生这个昂贵的调用。如果你使用它多次，可能会显著减慢 Makefile 的执行速度。

另一方面，如果你定义为 `SHALIST :=`，`$(shell)` 只执行一次——但它会在每次加载 Makefile 时都发生。如果 `SHALIST` 的值并不总是需要的（例如运行 `clean` 时），这可能是低效的。

我们希望有一种定义 `SHALIST` 的方法，使得在 `SHALIST` 未被使用时不执行 `$(shell)`，而在在使用时只调用一次。以下是实现方法：

```
SHALIST = $(eval SHALIST := $(shell find -name '*.c' | xargs shasum))$(SHALIST)
```

如果 `$(SHALIST)` 何被求值，`$(eval SHALIST := $(shell find -name '*.c' | xargs shasum)` 部分就会被评估。因为这里使用了 `:=`，它实际上执行了 `$(shell)` 并将 `SHALIST` 重新定义为该的结果。GNU make 然后获取 `$(SHALIST)` 的值，该值刚刚由 `$(eval)` 设置。

你可以通过创建一个小型 Makefile 来观察过程，使用 `value` 函数（它可以显示变量的定义而不进行展开）来在不求值的情况下检查 `SHALIST` 的值：

```
SHALIST = $(eval SHALIST := $(shell find -name '*.*.c' | xargs shasum)$(SHALIST)
```

```
$(info Before SHALIST is: $(value SHALIST))
$(info SHALIST is: $(SHALIST))
$(info After SHALIST is: $(value SHALIST))
```

在目录中带单个 .c 文件运行将得到以下输出：

```
$ make
Before SHALIST is: $(eval SHALIST := $(shell find -name '*.c' | xargs shasum)$(SHALIST)
SHALIST is: 3450ad043393b9b489756cb348469ac57ce821 ./foo.c
After SHALIST is: 3450ad043393b9b489756cb348469ac57ce821 ./foo.c
```

显然，`SHALIST` 自第一次被使用以来值已经发生了。

# 简单列表操作

在 GNU make 中，列表元素由空格分隔。例如，`peter paul and mary` 是一个包含四个元素的列表，`C:\Documents And Settings\Local` 也是如此。GNU make 有几个内置函数用于操作列表：

- `$(firstword)` 获取列表中的第一个单词。
- `$(words)` 统计列表元素的数量。
- `$(word)` 从特定索引（从 1 开始计数）提取单词。
- `$(wordlist)` 从列表中提取一段单词。
- `$(foreach)` 允许你遍历列表。

获取列表的第一个元素是非常简易的：

```
MY_LIST = a program for directed compilation
$(info The first word is $(firstword $(MY_LIST))
```

输出将是：`The first word is a`

你可以通过计算列表中单词的总数 $N$，然后取第 $N$ 个单词来获取最后一个元素。这里有一个返回列表中单词的最后一个函数：

```
lastword = $(if $1,(word $1),$($1))
MY_LIST = a program for directed compilation
$(info The last word is $(call lastword,$(MY_LIST)))
```

`$(if)` 是必要的，因为如果列表是空的，`$(words $1)` 将是 0，且 `$(word 0,$1)` 会产生致命错误。之前的输出显示 `The last word is compilation`。

注意：GNU make 3.81 及更高版本具有内置的 `lastword` 函数，它比之前的实现更快。

```
notfirst = $(wordlist 2,$(words $1),$1)
MY_LIST = a program for directed compilation
$(info The first word is not $(call notfirst,$(MY_LIST)))
```

输出 `The first word is not compilation`。

去掉最后一个元素需要一些技巧，因为无法在 `wordlist` 中直接进行算术运算：我们可以定义一个函数，它将一个哑元元素添加到列表开头，然后使用原始长度减1来切掉：

```
notlist = $(wordlist 2,$(words $1),$1)
MY_LIST = a program for directed compilation
$(info $(call notlist,$(MY_LIST)))
```

输出 `program for directed compilation`。

# 用户自定义函数

本节关于在 Makefile 中定义函数。在第 5 章中，你将学习如何修改源码以定义复杂的函数。我们在之前的章节中使用了许多用户自定义函数，但现在我们将仔细观察。

## 基础知识

这是一个非常简单的函数，它接收三个参数并通过插入斜杠来生成日期：

```
make_date = $1/$3
```

使用 `make_date` 时，这样调用 `$(call)`：

```
today := $(call make_date,5,5,2014)
```

这导致 `today` 包含 `5/5/2014`。如果调用函数时缺少参数，这些变量的内容是未定义的并被视为空字符串。

特殊参数 `$0` 包含函数的名称。前面的参数是 `make_date`。

由于函数本质上是引用 GNU make 自动创建并填充的变量（如果你对任何参数变量 $1 等使用 `$(origin)` 函数），它们被归类为自动变量，就像 ($ 一样），你可以使用内置 GNU 函数来构建复杂的函数。

这是一个使用 `$(subst)` 函数将路径中的每个 `/` 转换为 `\` 的函数：
