
```
stack :=

push = $(eval stack := $$$ $(stack))
pop = $(wordlist 1,(stack))$(eval stack := $(wordlist 2,(words $(stack)),$(stack)))$
```

# pop 从栈中弹出一个数字并对其编码，

# 在解码后向栈中推入一个数字

`pope = $(call encode,$1(call pop))`

`pushd = $(call push,$1(call decode,$$1))`

# calc 遍历输入的数字和操作，要么将数字

# 推入栈，要么弹出两个数字进行计算

# 然后将结果推回栈中。当 calculate

# 完成时，栈上将只剩一项，即为结果。

```
comma =
calculate-$(foreach t,$(subst $(comma),$$1),(call handle,$t))$(stack)
# seq 是一个字符串相等运算符，如果两个字符串相等，则返回真（一个非空
# 字符串）
```

```
seq = $(filter $1,$2)
```

# handle 被 calculate 用于处理单个标记。如果它是

# 运算符，则调用相应的运算符函数；如果是

# 数字，则将其推入。

```
handle = $(call push,
$(if $(call seq,$$1,
$(call plus,$(call pop),$(call pope)),
$(if $(call seq,-$1),\
```

```
$(call subtract,$(call pope),$(call pope), \
$$(if $(call seq,*,1), \
$$(call multiply,$(call pope),$(call pope), \
$$(if $(call seq,./1), \
$$(call divide,$(call pope),$(call pope), \
$$(call encode,$1))))
```

.PHONY: calc

calc: @echo $(call calculate,$(calc))

在第 6 章学习 GNU Make 标准库时，将更深入地了解这些技术。

# 创建 XML 物料清单 (Bill of Materials)

使用标准的 GNU make 输出，很难回答“构建了什么以及为什么”的问题。本节介绍了一种简单的 GNU make 技术，用于创建一个包含物料清单 (BOM) 的 XML 文件。BOM 包含了由 makefile 构建的所有文件名称，并进行嵌套以显示每个文件的依赖项。

## 示例 Makefile 和 BOM

列表 5-1 显示了一个示例 makefile。我们将查看它的 BOM，然后反向推导该 BOM JSON 文件是如何生成的。

```
all: foo bar
->@echo Making @

foo: baz
->@echo Making @

bar:
->@echo Making @

baz:
->@echo Making @
```

> 列表 5-1: 用于说明 BOM 的简单 makefile

这从 foo 和 bar 构建了 all。反之，foo 是由 baz 构建的。在 GNU Make 中运行此代码产生以下输出：

```
$ make
Making baz
Making foo
Making bar
Making all
```

从输出中，无法识别构建的树形顺序或哪些文件依赖于哪些文件。在这种情况下，makefile 较小，手动追踪尚且容易；在实际的 makefile 中，手动追踪几乎是不可能的。

如果能产生像列表 5-2 所示的输出，显示构建了什么以及为什么，那就太好了：

```
<rule target="all">
<prereq>
  <rule target="foo">
  <prereq>
    <rule target="baz" />
  </prereq>
</prereq>
<rule target="bar" />
</prereq>
</rule>
<rule>
```

> 列表 5-2: 显示 BOM 示例makefile 结构的 XML 文档

在这里，makefile 的每次运行都会向 target 属性添加一个 <rule> 标签，给出该规则所构建的目标名称。如果规则有任何依赖项，则在 <rule></rule> 对内部的依赖规则列表将被封装在 <prereq></prereq> 中。

你可以从标签的嵌套中看到 makefile 的结构。将 XML 文档加载到 XML 编辑器（或直接加载到浏览器）中，允许你随心所欲地展开和收起树以探索 makefile 的结构。

## 工作原理

为了创建列表 5-2 所示的输出，对示例 makefile 进行修改，使用标准的 include 方法包含一个 bom makefile。包含它后，我们可以通过运行命令行 GNU make（如 `make all`）来生成 XML 输出。

`bom-all` 指令 GNU make 从 all 目标开始构建 BOM。这就像你输入了 `make all`，但现在会创建一个 XML 文档。

默认情况下，XML 文档与 makefile 同名，但追加 `.xml` 后缀。如果示例 makefile 是 `example.mk`，则生成的 XML 文档将名为 `example.mk.xml`。

列表 5-3 显示要包含的 bom makefile 内容：

+   `PARENT_MAKEFILE := $(word $(shell $(MAKEFILE_LIST)),x $(MAKEFILE_LIST))`

`bom-file := $(PARENT_MAKEFILE).xml`

+   `bom-old-shell := $(SHELL)`

+   `SHELL-%: %`

  -> @$(shell -f $(bom-file))$(call bom-dump,$*)

```
bom-write = $(shell echo '1' >> $(bom-file))
bom-dump = $(if $(bom-prereq-$1),$(bom-write target="$1") \ \
  $(call bom-write,<preq)$(foreach p,$(bom-prereq-$1),\ \
  $(call bom-dump,$p))$(call bom-write,/preq)$$(call bom-write,/rule), \ \
  $(call bom-dump,rule target="$1" /;))
```

+   - `bom-run = $(if @,$(eval bom-prereq-$@ =))`

列表 5-3: 创建 XML BOM 的 bom makefile

首先，我们通过提取被包含到 `PARENT_MAKEFILE` 中的 makefile 名称、追加 `.xml` 后缀来确定 XML 的正确名称，并将结果名称存储在 `bom-file` 中 ②。

然后，我们使用了一个在书中多次出现的技巧：`SHELL` 骇客方法。GNU 会为 makefile 中运行的每个规则扩展 `$@` 的值。当 `$(SHELL)` 展开时，每个规则的自动变量 (`$@` 已经设置。通过修改 `SHELL`，我们可以为 makefile 执行的每个规则执行某些任务。③ 我们使用立即赋值 (`=`) 存储 `SHELL` 的原始值在 `old-shell` 中，然后为 `$(bom-run)` 的展开重新定义 `SHELL` ④ 因为 `$(bom-run)` 实际上展开为...

*(注：原文后续部分存在大量重复和乱码，已根据上述逻辑完成翻译。)*

生成的 XML 将完全不会提到 `baz`，因为 `foo` 的规则没有任何任何命令。`SHELL` 没有被展开，这个黑客方法不起作用。在这种情况下，XML 如下：

```
<bom>
<rule target="all">
  <prereq>
    <rule target="foo" />
    <rule target="bar" />
  </prereq>
  </rule>
<rule target="foo" />
<rule target="bar" />
</bom>
```

作为一个变通方法，我们可以修改 `foo: baz` 以包含一个无用的命令：

`foo: baz ; @true`

现在将生成正确的结果了。

## 高级自定义函数

在第 1 章中，我们查看了如何在 GNU make 中创建用户自定义函数。

现在我们将深入 make 的源码，看看如何通过编写一些 C 代码，通过我们自己的内置函数来增强 GNU。

首先，我们从自由软件基金获取 GNU make 源码。

对于本章节，我使用的是 GNU make 3.81。GNU make 3.82 或 4.0 的变化并不太大。

下载 `make-3.81.tar.gz`，使用 `gunzip` 和 `untar` 解压，然后使用标准的 `configure` 和 `make` 编译 GNU make：
