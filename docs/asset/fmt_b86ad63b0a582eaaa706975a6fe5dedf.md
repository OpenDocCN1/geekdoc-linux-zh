
然后它通过从 `MAKEFILE_LIST` 中移除 `this-makefile`（即 `help-system.mak`）获取所有其他包含的 makefile 列表：

```
other-makefiles := $(filter-out $(this-makefile),$(MAKEFILE_LIST))
```

`other-makefiles` 的最后一个元素将是 `help-system.mak` 的父级：

```
parent-makefile := $(call last-element,$(other-makefiles))
```

你使用 `last-element` 函数来获取空格分隔列表的最后一个元素：

```
define last-element
$(word $(words)1),$1
endef
```

`last-element` 通过使用 `$(words)` 获取单词计数并返回其引用的单词来返回列表中的最后一个单词。由于 GNU make 的列表从位置 1 开始计数，`$(words LIST)` 是最后一个元素的索引。

## 使用 print-help 文档化 Makefile

使用 `print-help` 文档化 Makefile 是很容易的。只需在你想要记录的每个目标的先决条件列表（prerequisite list）中添加相应的 `$(call print-help,target,description)` 即可。如果你将调用添加到用于该目标的命令旁边，帮助系统不仅会打印帮助信息，还会将用户引导到目标中的位置以查找更多信息。

保持文档更新也很容易，因为目标的描述实际上是目标定义的一部分，而不是在一个单独的帮助列表中。

## 完整的 help-system.mak

最后，这里是完整的 `help_system.mak`：

```
help := @echo $(if $(need-help)),Type \$(MAKE)(dash-f) help\' to get\'
need-help := $(filter helper,$(MAKEMDGOALS))
define print-help
$(if $(need-help),(warning $1 -- $2))
endef
define last-element
$(word $1,$1)
endef
this-makefile := $(call last-element,$(MAKEFILE_LIST))
other-makefiles := $(filter-out $(this-makefile),$(MAKEFILE_LIST))
parent-makefile := $(call last-element,$(other-makefiles))
dash-f := $(if $(filter-out Makefile GNUmakefile), \ $(parent-makefile))
```

只需包含 `help-system.mak` 即可在 makefile 中开始使用此系统进行文档。

在第 6 章中，我们将查看一个非常有用的资源——GMSL 项目。创建 GNU make 内置函数是很容易的，但它会导致维护问题：下一次 GNU make 更新时，我们需要将更改移植到新版本。如果我们可以在不修改源码的情况下使用 GNU make 内置函数完成我们需要的工作，那么 makefile 将将具有 GNU 可移植性。GMSL 在不修改 GNU GNU make 源码的情况下提供了大量额外功能。

# GNU MAKE 标准库

Make Standard Library (GMSL) 是一个托管在 SourceForge 上的开源项目，我启动它是为了捕获 makefile 作者反复编写的常用函数。为了防止 makefile 编写者造轮子，GMSL 实现了常用函数，例如反转列表、将字符串转换为大写或将函数映射到列表的每个元素上。

GMSL 包含列表和字符串处理函数、完整的算术库以及用于数据结构的函数。还包括 GNU make 实现的关联数组、集合和栈，以及内置的调试设施。

在本章中，你将学习如何在 makefile 中使用 GMSL 的函数。获取最新参考，请访问 http://gmsl.net/

## 导入 GMSL

GMSL 定义了布尔值 `true` 和 `false`，它们仅仅是变量，可以使用 `$(()` 或 `$()` 访问；例如 `$(true)` 或 `$(false)`；`false` 是空字符串，而 `true` 是字母 T；这些定义对应于 GNU make 对 true（非空字符串）和 false（空字符串）的概念。你可以在 GNU make 的 `$(if)` 函数或预处理器中使用 true 和 false：

```
$($true),It's true!,Totally false)
ife($(true),$(true))
--snip--
\endif
```

## 调用 GMSL 函数

GMSL 中的函数被实现为普通的函数定义。例如，`last` 函数（返回列表的最后一个元素）定义如下：

```
last = $(if $1,word $(1),$1)
```

使用 GNU make 的 `$(call)` 调用 `last` 函数。例如，要返回列表 1 2 3 的最后一个元素，执行：

```
$(call,1 2 3)
```

这将返回 3。`$(call)` 会展开第一个参数中指定的变量（在本例中为 `last`），并将特殊局部变量 ($1, $2, $3, ...) 设置为传递给 `$(call)` 的函数名之后的参数。在这种情况下，$1 是 1 2 3。

## 检查 GMSL 版本

GMSL 包含一个函数，你可以检查版本是否与你对 GMSL 的使用兼容。`gms_compatible` 函数检查包含的 GMSL 版本号大于或等于作为参数传递的版本号。

在本文写作时，当前的 GMSL 版本是 v1.1.7。要检查包含的 GMSL 至少为 v1.1.2，调用 `gmsl_compatible` 并传入一个包含三个元素的列表：1 1 2。

```
$(call gmsl_compatible,1 1 2)
```

此返回为 `$(true)`，因为当前的 GMSL 版本是 v1.1.7，它大于 v1.1.2。如果我们请求 v2.0.0，我们将得到返回 `$(false)`:

```
$(call gmsl_compatible,2 0)
```

要确保你正在使用正确版本的 GMSL，简单方法是将对 `gmsl_compatible` 的调用封装在断言（assertion）中：

```
$(call assert,$(call gmsl_compatible,1 0 0),Wrong GMSL version)
```

如果发现不兼容的 GMSL 版本，这将会带有一个错误并停止进程。

# 真实世界 GMSL 使用示例

现在你已经设置好了 GMSL，让我们来看一些示例。这些示例都解决了真实世界 Makefile 必须处理的问题，例如不区分大小的比较以及在路径中搜索文件。

## 不区分大小的比较

GMSL 包含两个函数，可以让你创建一个简单的函数，用于对两个字符串进行不区分大小的比较：

```
ifcase = $(call seq,$(call lc,$1),$(call lc,$2))
```

它的工作原理是将其参数转换为小写（使用 GMSL 的 `lc` 函数），然后调用 `seq`（GMSL 字符串相等函数）来检查它们是否相同。这里是使用 `ifcase` 的方法：

```
CPPFLAGS += $(if $(call equals,$(DEBUG),yes),-DEBUG)
```

在这里，它用于检查 `DEBUG` 变量是否设置为 yes；如果没有，则将 -DEBUG 添加到 `CPPFLAGS` 中。

## 在路径上查找程序

这里有一个函数定义，它会在 `PATH` 中搜索可执行文件：

```
findall = $(call first,$(call map,wildcard,$(call addsuffix,$1,$(call split,$(PATH))))
```
