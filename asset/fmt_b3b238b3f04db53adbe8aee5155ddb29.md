
当 `make` 展开此函数时，它将每个 `param` 分配给临时变量 `$(1)`、`$(2)` 等。变量 `$(0)` 将包含 `variable`。参数没有上限。也没有最小值，但没有参数没有意义。

然后 `variable` 值中对 `$(1)` 的引用将解析为 `call` 调用时的第一个参数。

注意 `variable` 是变量名，而不是该变量的引用。因此，编写它时通常不需要使用 `$` 或括号。 （但是，如果你希望名称是一个常量，可以在名称中使用变量引用）。

如果 `variable` 是内置函数的名称，则内置函数总是会被调用（即使存在同名的 make 变量）。

`call` 函数在将参数分配给临时变量之前会展开参数。这意味着包含特殊规则（如 `foreach` 或 `if`）内置函数引用的变量值可能无法按照预期方式工作。

一些示例可以使这一点清晰：

```
reverse := $(2) $(1)
```

```
foo := $(call reverse,a,b)
```

这里 `foo` 将包含 'ba'。

这个稍微有趣：它定义了一个宏在以下内容中搜索路径的第一个实例：

```
pathsearch := $(firstword $(wildcard $(addsuffix $(1),$(subst ,$(PATH))))
```

```
LS := $(call pathsearch,ls)
```

现在变量 `LS` 包含 `/bin/ls` 或类似内容。

`call` 函数是可以嵌套的。每次递归调用都会获取其自己的局部值，用于 `$(1)` 等；这些值会掩盖更高层调用的值。例如，这里是一个 `map` 函数的实现：

```
map = $(foreach a,$(),call $(1),$(a)))
```

现在你可以将一个通常接受一个参数的函数（例如 `origin`）映射到，中一次性乘以多个值：

```
o = $(call map.origin,o make MAKE)
```

并最终 `o` 包含类似于 'file default' 的内容。

注意：在向 `call` 的参数添加空格时要小心。与其他函数一样，第二个及后续参数中包含的任何空格都会保留；这可能会导致奇怪的副作用。通常为 `call` 提供参数时，移除所有多余的空格是最安全的。

## 8.7 value 函数

`value` 函数提供了一种在不展开变量的情况下使用该变量值的方法。请注意，这并不会撤销已经发生的展开；如果你定义了一个简单展开的变量，它在定义期间就会被展开；在这种情况下，`value` 函数返回的结果与直接使用变量相同。

`value` 函数的语法为：

```
$(value variable)
```

注意 `variable` 是变量名，而不是对它的引用。因此，在编写它时你不需要使用 '$' 或括号。不过，如果你希望名称不是常量，可以在名称中使用变量引用。

该函数的返回结果是一个包含变量值的字符串，且不会发生任何展开。例如，在如下 makefile 中：

```
FOO = $PATH
```

```
all:
@echo $(FOO)
@echo $(value FOO)
```

第一行输出将是 `$PATH`，因为 '$' 会被展开为一个 make 变量；而第二行输出将是你的 `$PATH` 环境变量的当前值，因为 `value` 函数规避了展开。

`value` 函数通常与 `eval` 函数结合使用（见第 8.8 节 [Eval Function]，第 88 页）。

## 8.8 eval 函数

`eval` 函数非常特殊：它允许你定义新的、非常量的 makefile 结构；作为评估其他变量和函数的结果。`eval` 函数的参数会被展开，然后将该展开的结果被解析为 make 语法。展开后的结果可以定义新的 make 变量、目标、隐式或显式规则等。

`eval` 函数的结果始终为空字符串；因此，它几乎可以放在 makefile 的任何位置而不会引起语法错误。

## 第 8 章：用于转换文本的函数

重要的是，`eval` 的参数会被展开两次：首先由 `eval` 函数展开，展开的结果在被解析为 make 语法时再次被展开。这意味着在使用 `eval` 时，你可能需要对 "$" 符号提供额外的转义层。在这些情况下，`value` 函数（见第 8.7 节 [Value Function]，第 88 页）可能很有用，以规避非预期的展开。

这里是 `eval` 的用法示例；此示例结合了多个概念和其他函数。虽然在这个示例中使用 `eval` 看起来可能比直接写规则要复杂得多（过度复杂），但请考虑以下两点：首先，模板定义（在 `PROGRAM_template` 中）可能比这里展示的要复杂得多；其次，你可能将此示例中复杂的“泛型”部分放在另一个 makefile 中，然后将其包含在所有的独立模块中。现在，你的独立模块就变得非常简单了。

```
PROGRAMS = server client
```

```
server_OBJS = server.o server_priv.o server_access.o
server_LIBS = priv protocol
```

```
client_OBJS = client.o client_api.o client_mem.o
client_LIBS = protocol
```

### 这都是泛型的

```
.PHONY: all
all: $(PROGRAMS)
```

```
define PROGRAM_template =
$(1): $$$($(1)_OBJS) $$($(1)_LIBS:--1%)
ALL_OBJS += $$($(1)_OBJS)
endef
```

```
$(foreach prog,$(PROGRAMS),$(eval $(call PROGRAM_template,$(prog))))
```

```
$(PROGRAMS):
$($(.o) ^ $(LDLIBS) $$
```

```
clean:
rm -f $(ALL_OBJS) $(PROGRAMS)
```

## 8.9 origin 函数

`origin` 函数与其他函数不同之处在于，它不作用于变量的值：它告诉你一些关于变量的信息。具体来说，它告诉你变量源自哪里。

`origin` 函数的语法为：

```
$(origin variable)
```

注意 `variable` 是要查询的变量名，而不是对该变量的引用。因此，在编写它时通常不需要使用 '$' 或括号。 （不过，如果你希望名称不是常量，可以在名称中使用变量引用。）

该函数的返回结果是一个字符串，告诉你变量 *variable* 是如何定义的：

`undefined`

如果 *variable* 从未被定义过。

`default`

如果 *variable* 有默认定义，如 `CC` 等通常如此。见第 10.3 节 [Variables by Implicit Rules]，第 107 页。注意，如果你重新定义了一个默认变量，*origin* 函数将返回后定义的来源。

`environment`

如果 *variable* 继承自提供给 make 的环境变量，并且是-

`environment override`

如果 *variable* 继承自提供给 make 的环境变量，并且由于 '-e' 参数覆盖了 makefile 的设置。

`file`

如果 *variable* 在 makefile 中定义。

`command line`

如果 *variable* 在命令行上定义。

`override`

如果 *variable* 通过 `override` 指令定义。

`automatic`

如果 *variable* 是自动变量。

## 8.10 flavor 函数

`flavor` 函数与其他函数（与 `origin` 函数类似）不同之处在于它不作用于变量的值；它告诉你一些关于变量的信息。具体来说，它告诉你变量的类型（见第 6.2 节 [The Two Flavors of Variables]，第 58 页）。

该函数的语法为：

```
$(flavor variable)
```

见第 8.2 节 [Function Function]，第 50 页。

该函数的返回结果是一个标识变量类型的字符串：

- `undefined` 如果 *variable* 从未被定义。
- `recursive` 如果 *variable* 是一个递归展开变量。
- `simple` 如果 *variable* 是一个简单展开变量。

## 8.11 shell 函数

`shell` 函数与其他任何函数（包括 `wildcard` 函数，见第 4.3 节 [Function wildcard]，第 24 页）的不同在于它可以与 make 外部的世界进行通信。
