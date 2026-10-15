
`command`（命令）是 `make` 执行的操作。一个规则可以有多个命令，每个命令单独占一行。请注意：你需要在每行命令的开头输入一个制表符（`tab character`）！这是一个会让疏忽者出错的模糊之处。

通常，命令位于一个带有前提条件的规则中，并在当任何前提条件发生变化时用于创建目标文件。然而，指定目标命令的规则可能没有前提条件。例如，与目标‘`clean`’相关的包含删除命令的规则就没有前提条件。

因此，规则解释了如何以及何时删除作为该特定规则目标的某些文件。`make` 执行前提条件上的命令以创建或更新目标。规则也可以解释如何以及何时执行某操作。参见第 4 章 [Writing Rules]，第 19 页。

`makefile` 可能包含规则之外的文本，但简单的 `makefile` 只包含规则。规则看起来可能比此模板中显示的稍微复杂一些，但它们大体都符合该模式。

## 2.2 简单的 Makefile

这是一个直观的 `makefile`，它描述了一个名为 `edit` 的可执行文件依赖于 8 个对象文件，而这些对象文件又依赖于 8 个 C 源文件和 3 个头文件。

在这个示例中，C 文件包含了 'defs.h'，但只有定义编辑命令的文件包含了 'command.h'，只有更改编辑器缓冲的底层文件包含了 'buffer.h'。

```
edit : main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o

main.o : main.c defs.h
    cc -c main.c
kbd.o : kbd.c defs.h command.h
    cc -c kbd.o
command.o : command.c defs.h command.h
    cc -c command.o
display.o : display.c defs.h buffer.h
    cc -c display.o
insert.o : insert.c defs.h buffer.h
    cc -c insert.c
search.o : search.c defs.h buffer.h
    cc -c search.o
files.o : files.c defs.h buffer.h command.h
    cc -c files.o
utils.o : utils.c defs.h
    cc -c utils.o

clean:
    rm edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

我们使用反斜杠加换行将每行拆分为两行；这类似于使用了一行长代码，但更容易阅读。

使用此 `makefile` 来创建一个名为 `edit` 的可执行文件，输入：

`make`

使用此 `makefile` 删除可执行文件和所有对象文件，输入：

`make clean`

## 2.3 make 如何处理 Makefile

默认，`make` 从第一个目标开始（以 `.` 开头的目标除外）。

```
edit : main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

如果对象文件不存在，或者任何前提条件文件比对象文件新，`make` 会重新编译源文件来更新它。

```
main.o : main.c defs.h
    cc -c main.c

kbd.o : kbd.c defs.h command.h
    cc -c kbd.o

command.o : command.c defs.h command.h
    cc -c command.o

display.o : display.c defs.h buffer.h
    cc -c display.o

insert.o : insert.c defs.h buffer.h
    cc -c insert.c

search.o : search.c defs.h buffer.h
    cc -c search.o

files.o : files.c defs.h buffer.h command.h
    cc -c files.o

utils.o : utils.c defs.h
    cc -c utils.o

clean:
    rm edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

我们使用反斜杠加换行将每行拆分为两行；这类似于使用了一行长代码，但更容易阅读。

使用此 `makefile` 来创建一个名为 `edit` 的可执行文件，输入：

`make`

使用此 `makefile` 删除可执行文件和所有对象文件，输入：

`make clean`

如果源文件被重新编译，所有的对象文件（新生成的或从之前的编译保存的）都必须链接在一起，以生成新的可执行编辑器。

这些规则中被执行的操作。

目标 '`clean`' 不是一个文件，仅仅是操作的名称。不引用文件而仅引用操作的 `target` 称为“伪目标（`phony targets`）”。关于这类目标信息，请参见第 4.4 节 [Phony Targets]，第 27 页。要了解如何让 `make` 忽略任何命令错误，请参见第 5.4 节 [Errors in Commands]，第 44 页。

## 2.4 变量让 Makefile 更简单

在我们的示例中，我们必须在 '`edit`' 规则中列出两次所有的对象文件（如下）：

```
edit := main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

这种重复很容易出错；如果系统添加了新的对象，我们可能会将其添加到其中一个列表而忘记另一个。我们可以通过使用变量来消除风险并简化 `Makefile`。变量允许定义一次文本字符串，并在以后多次替换（参见第 6 章 [How to Use Variables]，第 55 页）。

每个 `Makefile` 的标准做法是名为 `objects`、`OBJECTS`、`objs`、`OBJ` 或 `OBJ` 的变量，它是所有对象文件的名称列表。我们会在 `Makefile` 中通过如下行定义这样的 `objects` 变量：

```
objects := main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

然后，在每个想要放置对象文件名称列表的地方，我们都可以通过编写 `$(objects)` 来替换变量的值。

# 第2章：Makefile 简介

当你使用变量来定义对象文件时，完整的简单的 `Makefile` 如下：
