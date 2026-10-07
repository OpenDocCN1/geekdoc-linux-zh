
# 计算机阅读指南

本文件记录了 GNU `make` 实用，它能够自动确定大型程序中哪些部分需要重新编译，并发布重新编译这些部分的命令。

- 5.9 空配方 ................................................................................ 57
- 6.7 `override` 指令 ...................................................................... 68
- 10.5 定义和重新定义模式规则 ................................................ 118
- 10.5.2 模式规则示例 ................................................................ 119
- 10.5.6 取消隐式规则 ........................................................ 125
- 10.7 旧式后缀规则 ............................................................ 125
- 11.3 使用归档时的危险.................................................. 130
- 12.2.1 Load 指令........................................................ 136

`make` 工具自动确定大型程序中哪些部分需要重新编译，并发布命令来重新编译这些部分。本手册描述了 GNU `make`，它由 Richard Stallman 和 Roland McGrath 实现。自版本 3.76 以来的开发由 Paul D. Smith 负责。

GNU `make` 符合 IEEE 标准 1003.2-1992 (POSIX.2) 的 6.2 部分。

我们的示例展示了 C 程序，因为它们最常见，但你可以在任何编译器可以运行 shell 命令的编程语言中使用 `make`。事实上，`make` 不局限于程序。你可以用它描述任何任务，即当文件发生变化时，某些文件可以从其他文件自动更新。

要使用 `make`，你必须编写一个名为 `makefile` 的文件，描述你程序中文件之间的关系，并提供更新每个文件的命令。在程序中，通常可执行文件是从对象文件更新的，而对象文件又是通过编译源文件生成的。

一旦存在合适的 `makefile`，每当你更改某些源文件时，只需执行简单的 shell 命令：

```
make
```

就足以执行所有必要的重新编译。`make` 程序使用 `makefile` 基础和文件的最后修改时间来决定哪些文件需要更新。对于这些文件，它会执行数据库中的配方（recipes）。

你可以向 `make` 提供行命令行参数来控制哪些文件应该重新编译，或者参阅第 9 章 [如何运行 make]，第 99 页。

如果你是 `make` 的新手，或者正在寻找通用的介绍，请阅读每一章的前几节，跳过后面的章节。在每一章中，前几节包含介绍性或通用信息，后面的章节包含专门的或技术信息。例外是第 2 章 [Makefile 简介]，第 3 页，其内容都是介绍性的。

如果你熟悉其他程序，请参阅第 13 章 [GNU make 的特性]，第 143 页，该章列出了 GNU `make` 拥有的增强，以及第 14 章 [不兼容性与缺失特性]，第 147 页，该章解释了 GNU `make` 缺失的其他程序具备的缺陷。

快速摘要请参见第 9.7 [选项总结]，第 104 页，附录 A [快速参考]，第 165 页以及第 4.8 [特殊目标]，第 32 页。

如果你在使用 GNU `make` 时遇到问题或认为你发现了一个 bug，请向开发人员报告；我们无法承诺要做什么，但我们可能想修复它。

在报告 bug 之前，确保你确实发现了一个真实的 bug。仔细重读文档，看看它是否真的说你可以做你正在尝试的事情。如果不确定是否应该做某事，请报告它：那是文档的 bug！

你需要一个名为 `makefile` 的文件来告诉 `make` 要做什么。在本章中，我们将讨论一个描述编译和链接的简单 `makefile`。当 `make` 重新编译编辑器时，每个更改的源文件必须重新编译。如果头文件发生了，每个包含该头文件的源文件必须重新编译。每次编译产生一个对象文件。

## 规则的外

`makefile` 由如下形状的规则组成：

```
target : prerequisites
	recipe
```

`target` 是程序生成的文件名；目标的示例包括执行文件或对象文件。目标也可以动作名称，例如‘`clean`’（参见节 4.5 [伪目标]，第 29 页）。

`prerequisite` 是创建目标时作为输入的文件。目标通常依赖于多个文件。

`recipe` 是执行的动作。`recipe` 可以包含多个命令，可以在同一行，也可以每个命令单独占一行。注意：你需要在每条 `recipe` 行的开头放一个制表符（tab character）！

这是一个直观的 Makefile，它描述了名为 `edit` 的可执行文件依赖于对象文件，而这些对象文件又依赖于 `edit` 的 C 源代码和三个头文件。

在这个示例中，所有的 C 文件都包含了 'defs.h'，但只有定义了编辑命令的文件包含了 'command.h'，只有包含编辑器缓冲器的低级文件包含了 'buffer.h'。

```
edit : main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

```
main.o : main.c defs.h
    cc -c main.c
kbd.o : main.c defs.h command.h
    cc -c kbd.o
command.o : command.c defs.h command.h
    cc -c command.o
display.o : display.c defs.h buffer.h
    cc -c display.o
insert.o : insert.c defs.h buffer.h
    cc -c insert.o
search.o : search.c defs.h buffer.h
    cc -c search.o
files.o : files.c defs.h buffer.h
    cc -c files.o
utils.o : utils.c defs.h
    cc -c utils.o
```

```
clean :
    rm main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

我们使用反斜杠/换行符将每一行分成两行；这就像使用了一行一样，但更容易阅读。参见第 3.1 节 [拆分长行]，第 12 页。

要使用此 Makefile 创建可执行文件 'edit'，请输入：

```
make
make clean
```

要使用此 Makefile 删除目录中的可执行文件和所有对象文件，请输入：

在示例 Makefile 中，目标（targets）包括可执行文件 'edit' 以及对象文件 'main.o' 和 'kbd.o'。先决（prerequisites）是文件如 'main.c' 和 'defs.h'。事实上，每个 '.o' 既是目标也是先决。配方（Recipes）包括 'cc - main.c' 和 'cc - kbd.o'。

当目标文件时，如果它的任何先决发生变化，则需要重新编译或重新链接。此外，任何本身自动生成的先决都必须更新。在这个示例中，'edit' 依赖于八个对象文件每一个；对象文件 'main.o' 依赖于源代码 'main.c' 和头文件 'defs.h'。

配方可以跟在每一行包含目标和先决的行之后。这些配方会更新目标文件。一个制表符（或由 `.RECIPEPREFIX` 变量指定的任何字符；参见第 6.14 节 [特殊变量]，第 73 页）必须位于配方每行的开头，以便将配方与 Makefile 中的其他行区分开来。（请记住，`make` 并不知道配方是如何工作的。提供更新目标文件的配方是你的责任。`make` 所做的只是在目标文件需要更新时执行你指定的配方。）

'clean' 不是一个文件，而是一个动作的名称。由于你通常不想执行文件中的动作，因此 'clean' 不是任何其他目标的先决。因此，除非你明确告诉它，否则 `make` 永远不会执行任何操作。该规则不是先决，也没有先决，因此该规则的唯一目的是运行指定的配方。不引用文件的目标请参见第 4.5 节 [伪目标]，第 29 页获取有关此类目标的信息。参见第 5.5 节 [配方中的错误]，第 49 页查看如何让 `make` 忽略 `rm` 或任何其他命令的错误。

### 2.3 make 如何处理 Makefile

默认情况下，`make` 从第一个目标开始（不是名称以 '.' 开头的目标）。这是默认目标。（目标是 `make` 努力最终更新的规则。你可以使用命令行来覆盖此行为（参见第 9.2 节 [指定目标的参数]，第 99 页）或使用 `.DEFAULT_GOAL` 特殊变量（参见第 6.14 节 [其他特殊变量]，第 73 页）。

在前一节的简单示例中，默认目标是更新可执行文件 'edit'；这是我们放置规则的文件。

```
make
```

其他规则之所以被处理是因为它们作为目标的先决出现。如果某个其他规则没有被目标依赖（或它依赖于目标，等等），则该规则不会被处理，除非你告诉 `make` 这样做（使用如 `make clean` 这样的命令）。

在重新编译对象文件之前，`make` 会考虑更新它的先决，即源代码文件和头文件。`make` 没有为它们指定任何要执行的操作——'.c' 和 '.h' 文件没有被指定操作。如果源代码或任何命名为先决的头文件比对象文件新，或者该文件不存在，则必须重新编译。

### 2.4 变量让 Makefile 更简单

```
edit : main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

这种重复很容易出错；如果向系统添加一个新的对象文件，我们可能会在地方添加而忘记另一个。我们可以使用变量消除这种风险并简化 Makefile。每个 Makefile 通常都有名为 `objects`、`OBJECTS` 或 `OBJ` 的变量，它是对象文件名列表。我们可以在 Makefile 中通过如下行定义这样的变量：

```
objects = main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o
```

然后，在我们任何想要放置对象列表的地方，我们通过编写 `$(objects)` 来替换变量的值（参见第 6 章 [如何使用变量]）。

当你对象使用变量时，完整的 Makefile 看起来如下：

```
objects = main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o

edit : $(objects)
cc -o edit $(objects)
main.o : main.c defs.h
    cc -c main.c
kbd.o : main.c defs.h command.h
    cc -c kbd.o
command.o : command.c defs.h command.h
    cc -c command.o
display.o : display.c defs.h buffer.h
    cc -c display.o
insert.o : insert.c defs.h buffer.h
    cc -c insert.o
search.o : search.c defs.h buffer.h
    cc -c search.o
files.o : files.c defs.h buffer.h
    cc -c files.o
utils.o : utils.c defs
    cc -c utils.o

clean:
rm edit $(objects)
```

没有写出编译单个 C 源代码的配方，因为 `make` 可以推断出一个有一个隐式规则，可以使用 'cc -c' 从同名的 '.c' 文件更新 '.o' 文件。例如，它将使用 'cc -c main.c -o main.o' 配方将 'main.c' 编译为 'main.o'。参见第 10 章 [使用隐式规则]，第 111 页。

当 '.c' 文件以这种方式自动使用时，它也会自动添加到先决列表中。因此，只要我们省略了配方，就可以从先决列表中省略 '.c' 文件。

这里是应用了这些更改并使用建议的变量 `objects` 后的整个示例：

```
objects = main.o kbd.o command.o display.o \
  insert.o search.o files.o utils.o
```

```
edit : $(objects)
cc -o edit $(objects)
```

```
main.o : defs.h
kbd.o : defs.h command.h
display.o : defs.h buffer.h
insert.o : defs.h buffer.h
search.o : defs.h buffer.h
files.o : defs.h buffer.h command.h
utils.o : defs.h
```

```
clean:
  rm edit $(objects)
```

这就是在实际操作中 `clean` 目标是如何生成 Makefile 的。（与 `clean` 相关的复杂性在别处描述：第 4.5节 [伪目标]，第 29 页和第 5.5节 [配方中的错误]，第 49 页）。

由于隐式规则非常方便，它们非常重要。你会经常看到它们被。

当 Makefile 中的对象文件仅通过隐式规则创建时，可以使用另一种 Makefile 样式。在这种风格的 Makefile 中，你根据其依赖项而不是目标对条目进行分组。它的样子如下：

```
objects = main.o kbd.o command.o display.o \
  insert.o search.o files.o utils.o
```

```
edit : $(objects)
cc -o edit $(objects)
```

```
$(objects) : defs.h
kbd.o command.o files.o : command.h
display.o insert.o search.o files.o : buffer.h
```

在这里，`defs.h` 被给出所有对象文件的依赖项；`command.h` 和 `buffer.h` 是为其列出的特定对象文件的依赖项。

这种方式是否更好取决于个人口味：它更紧凑，但有些人并不喜欢它，因为他们认为将每个目标的所有信息放在一个地方更清晰。

编译程序并不是你可能想要编写规则的唯一事情。Makefile 通常还会告诉除编译程序之外的如何执行其他几件事：例如，如何删除所有对象文件和可执行文件，以便目录是“干净”的。

以下是我们如何为我们的示例编辑器编写一个清理规则的：

```
rm edit $(objects)
```

在实践中，我们可能希望以稍微复杂一点的方式规则以处理意外情况。我们会这样做：

```
.PHONY : clean
-rm edit $(objects)
```
