
常见的请求是：是否有方法可以找到当前`makefile`的名称和路径？人们所说的当前通常是指 GNU `make`正在解析的那个。没有内置方法可以快速获取答案，但可以使用 GNU `make`变量`MAKEFILE_LIST`实现。`MAKEFILE_LIST`是当前加载或包含的`makefiles`列表。每当一个`makefile`被加载或包含时，`MAKEFILE_LIST`就会追加其路径和名称。变量中的路径和名称相对于当前工作目录（GNU `make`启动的地方或通过`-C`或`--directory`选项切换到的地方），但你可以访问当前目录。

因此，你可以定义一个 GNU `make`函数（我们称之为`where-am-i`），它将返回当前的`makefile`（它使用`$word`获取列表中的最后一个`makefile`名称）：

```
where-am-i = $(CURDIR)/($words $(MAKEFILE_LIST)),$(MAKEFILE_LIST)
```

然后，每当你想找到当前`makefile`的完整路径时，在`makefile`的顶部写入以下内容：

```
THIS_MAKEFILE := $(call where-am-i)
```

这一行位于顶部至关重要，因为任何`include`语句都会改变`MAKEFILE_LIST`的值，所以你想在这些发生之前获取当前`makefile`的位置。

列表 4-13 显示了一个`makefile`示例，其中`where-am-i`包含了`foo/`子目录下的另一个`makefile`，而该文件又包含了`foo/bar/`目录下的一个`makefile`。

```
where-am-i = $(CURDIR)/($word $(MAKEFILE_LIST)),$(MAKEFILE_LIST)

include foo/makefile
```

列表 4-13: 一个可以确定自身在文件系统中位置的`makefile`

`foo/makefile`的内容如列表 4-14所示。

```
THIS_MAKEFILE := $(call where-am-i)
$(warning $(THIS_MAKEFILE))
```

列表 4-14: 被列表 4-13 包含的`makefile` `foo/bar/makefile`

`foo/bar/makefile`的内容如列表 4-15所示。

```
THIS_MAKEFILE := $(call where-am-i)
$(warning $(THIS_MAKEFILE))
```

```
foo/makefile:2: /tmp/foo/foo/makefile
foo/bar/makefile:2: /tmp/foo/bar/makefile
```

在本章中，我们查看了`makefile`创建者和维护者在处理真实`makefile`时遇到的常见问题。在任何使用`make`的大型项目中，你可能会遇到其中一个或多个（甚至是全部！）问题。

## 5 突破极限

![](img/544ed9176)

在本章中，你会发现某些内容不是必须的，但有时很有用。

### 进行算术运算

GNU `make`没有内置的算术运算。但可以创建用于加、减、乘、除的函数。`$(filter PATTERN,LIST)`函数会遍历列表并移除匹配模式的元素。

类似的模式也适用于减法：

```
subtract = $(if $(call gte,$1,$2), \
$(filter-out xx,$(join $1,$2)), \
$(warning subtraction underflow)
```

暂时忽略定义中的`$(warning)`和`$(if)`部分，重点关注`$(filter-out)`。`$(filter-out)`是`$(filter)`的相反操作；它会从列表中移除匹配模式的元素。例如，我们可以看到这里的`$(filter-out)`实现了减法功能：

```
$filter-out, xx,$join(six),$(five))
-> $(filter-out, xx,$join(x x x x x,x x x x x))
-> $(filter-out,xx,xx xx xx x)
-> x
```

不幸的是，如果五被反过来，这种方法仍然有效，因此我们首先需要检查第一个参数是否大于等于第二个参数。在减法的定义中，特殊函数`gte`（大于或等于）如果其第一个参数大于第二个参数，则返回一个非空字符串。我们使用`gte`来决定是执行减法还是使用`$(warning)`输出警告。

`te`函数是通过另外两个用于“大于”和“且等于”的函数实现的：

```
gt = $(filter-out words $2),$(words $(call max,$1,$2))
eqq = $(filter(words $1)),$(words $2))
te = $(call gt,$1,$2)$(call eq,$1,$2)
```

如果`gt`或`eq`返回非空字符串，则`gte`返回非空字符串。`eq`函数有点有点绕脑筋。它根据两个参数工作，将一个参数视为模式，另一个视为列表，并使用`$(filter)`来判断它们是否相同。这里有一个它们相等的例子：

```
$(call eq,(five),$(five))
-> $(call eq,x x x,x x x)
-> $(filter(words x x x),words x x x))
-> $(filter(words x x x),words x x))
```

`eq`函数将两个`$(five)`都转换为一个`x`列表。然后使用`$(words)`将它们都转换为数字 5。这两个 5 被传递给`$(filter)`。因为`$(filter)`的两个参数相同，所以结果是 5，而且因为 5 不是空字符串，所以它被解释为真。这里是它们不相等时会发生的情况：

```
$(call eq,(five),$(six))
-> $(call eq,x x x,x x x)
-> $(filter(words x x x),words x x x))
-> $(filter,5,6)
```

此过程与`$(call eq,(five),$(five))`相同，但其中一个`$(five)`被替换为`$(six)`。由于`$(filter,5,6)`是空字符串，所以结果为假。因此`$(filter)`函数充当了某种等价运算符；在这种情况下，两个字符串是长度。`gt`函数的实现方式类似：如果第一个字符串的长度不等于两个字符串中的最大值，则返回一个非空字符串。这里有一个例子：

```
$(call gt,(six),$(five))
-> $(call gt,x x x x,x x x)
-> $(filter-out(words x x x x),words x x x))
-> $(call max,x x x x,x x x))
-> $(filter-out(words x x x x),words x x x))
-> $(filter-out(5,6))
```

`gt`函数的工作方式与`eq`（之前描述）类似，但使用`$(filter-out)`将第一个与两个中的最大值进行比较。当第一个数字大于第二个数字时，`$(filter-out)`返回非空字符串。这里有一个第一个数字小于第二个数字的例子：

```
$(call gt,(five),$(six))
-> $(call gt,x x x,x x x x)
-> $(filter-out(words x x x),words x x x x))
-> $(call max,x x x,x x x x))
-> $(filter-out(5,6))
```

在这里，因为两个数字中的最大值与第二个相同，`$(filter-out)`返回空字符串。同样地，我们可以定义不等于`ne`、小于`lt`和小于等于`le`运算符：

```
lt = $(filter-out(words $1),words $(call max,$1,$2)))
```

```
lte = $(call,1,$2)$(eq,1,$2)
```

`increment`将其参数加 1，`decrement`将减 1。请注意，`decrement`不进行范围检查，也不会溢出，但它会错误地显示 0 - 1 = 0

```
increment = $1 x
decrement = $(wordlist,2,$words $1),$$1)
```

`double`将其参数翻倍，`halve`将减半

```
double = $1 $1

halve = $(sub xx,x,$(filter-out xy y,$(join $1,$a,$1,y x)))
```

此代码通过将存储在`calc`变量中的、以逗号分隔的运算符`+ - *` `/`和数字转换为对该`makefile`中定义的算术函数的相应调用，从而实现了一个逆波兰表达式（Reverse Polish Notation）计算器。

这是输入到计算器的当前数字栈。`push`函数将一个项推入栈顶（列表的开头），`pop`移除栈顶项。
