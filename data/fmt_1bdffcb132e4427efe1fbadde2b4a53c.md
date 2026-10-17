
# 5 在规则中编写配方 (Writing Recipes)

配方规则由一个或多个 shell 命令组成，这些命令将按照它们出现的顺序逐一执行。通常，执行这些命令的结果是规则的目标更新到最新。

用户使用许多不同的 shell 程序，但除非 Makefile 中另有说明，否则 Makefile 中的配方始终由 `/bin/sh` 解释。参阅第 44 页第 5.3 节 [`Recipe Execution`](Recipe Execution)。

## 5.1 配方语法 (Recipe Syntax)

Makefile 有一个特殊的属性，即一个文件中实际上存在两种不同的语法。Makefile 使用 `make` 语法（参阅第 11 页第 3 章 [`Writing Makefiles`](Writing Makefiles)）。然而，配方旨在由 shell 解释，因此使用 shell 语法编写。`make` 程序并不尝试理解 shell 语法：它在将配方交给 shell 之前，仅对配方内容进行特定的翻译。

配方中的每一行必须以制表符开头（或以 `RECIPEPREFIX` 变量值的第一个字符开头；见第 70 页第 6.14 节 [`Special Variables`](Special Variables)），但第一行配方可以使用分号连接到目标和先置行。Makefile 中任何以制表符开头并出现在“规则上下文”中的行（即从规则开始到另一个规则或变量定义之前的行）都将被视为该配方的一部分。空行和注释行可能会出现在配方行之间；它们会被忽略。

这些规则的一些后果包括：

- 带有制表符的空行不是空的：它是一个空配方（见第 55 页第 5.9 节 [`Empty Recipes`](Empty Recipes)）。
- 配方中的注释不是 make 注释；它将原样传递给 shell。shell 是否将其视为注释取决于你的 shell。
- 在“规则上下文”中，以制表符作为行首字符缩进的变量定义将被视为配方的一部分而非 make 变量，并传递给 shell。
- 在“规则上下文”中，以制表符作为行首字符缩进的条件表达式（`ifdef, ifeq`。见第 74 页第 7.2 节 [`Syntax of Conditionals`](Syntax of Conditionals)）将被视为配方的一部分并传递给 shell。

### 5.1.1 拆分配方行 (Splitting Recipe Lines)

`make` 解释的一种方式是检查换行符之前的反斜杠 `\`。在标准的 make 语法中，可以通过在每个换行符之前放置反斜杠，将单行配方拆分为 Makefile 中的多行物理行。这样的行序列被视为单条配方行，并将调用 shell 来运行。

然而，与 Makefile 中其他地方的处理方式相反，反斜杠-换行符不会从配方中移除。反斜杠和换行符都被保留并传递给 shell。反斜杠-换行的解释方式取决于你的 shell。如果反斜杠后的下一行的第一个字符是配方前缀（默认为制表符；见第 70 页第 6.14 节 [`Special Variables`](Special Variables)），那么该字符（仅限该字符）会被移除。空格永远不会添加到配方中。例如，此 Makefile 中 `all` 目标的配方：

```
all:
    @echo no\
    space
    @echo no\
    space
    @echo one \
    space
    @echo one\
    space
```

由四个独立的 shell 命令组成，输出为：

nospace

nospace

one space

one space

更复杂的示例，此 Makefile：

```
all : ; @echo 'hello \
    world'; echo "hello" \
    world"
```

将调用一个 shell，命令为：

echo 'hello \

    world'; echo "hello" \

    world"

根据 shell 引用规则，将产生以下输出：

hello \

    world

hello \

    world

注意反斜杠/换行对在单引号 ('...') 内没有被移除，而是从字符串中。这是默认 shell ('bin/sh') 处理反斜杠/换行对的方式。如果你在 Makefile 中指定了不同的 shell，可能会以不同方式处理它们。

有时你希望使用单引号拆分长行，但不希望反斜杠-换行出现在引用内容中。这在将脚本传递给 Perl 等语言时经常发生，脚本内部额外的反斜可能会可能会其含义或导致语法错误。处理此问题的简单方法是将引用字符串（甚至整个命令）放入 make 变量，然后在配方中使用该变量。在这种情况下，将使用 Makefile 的换行引用规则，反斜杠-换行的配方前缀会被移除。

## 5.2 输出 (Echoing)

通常，`make` 在执行之前会打印配方的每一行。这对于查看 make 正在做什么很有用，但有时你想抑制输出。可以通过行开头加上 `@` 来实现。

```
all:
    @echo hello world
```

输出将是：

```
hello world
```

如果你不使用 `@`，输出将是：

```
@echo hello world
hello world
```

你还可以使用 `@` 来抑制 `echo` 命令本身的输出：

```
all:
    @echo "hello world"
```

输出将是：

```
hello world
```

## 5.3 配方执行 (Recipe Execution)

配方规则由一个或多个 shell 命令组成，按照它们顺序逐一执行。通常，执行这些命令的结果是规则的目标更新到最新。

用户使用许多不同的 shell 程序，但除非 Makefile 中另有说明，否则 Makefile 中的配方始终由 `/bin/sh` 解释。参见第 44 页第 5.3 节 [`Recipe Execution`](Recipe Execution)。

## 5.1 配方语法 (Recipe Syntax)

Makefile 有一个特殊的属性，即一个文件中实际上存在两种不同的语法。Makefile 使用 `make` 语法（参阅第 11 页第 3 章 [`Writing Makefiles`](Writing Makefiles)）。然而，配方旨在由 shell 解释，因此使用 shell 语法编写。`make` 程序并不尝试理解 shell 语法：它在将配方交给 shell 之前，仅对配方内容进行特定的翻译。

配方中的每一行必须以制表符开头（或以 `RECIPEPREFIX` 变量值的第一个字符开头；见第 70 页第 6.14 节 [`Special Variables`](Special Variables)），但第一行配方可以使用分号连接到目标和先置行。Makefile 中任何以制表符开头并出现在“规则上下文”中的行（即从规则开始到另一个规则或变量定义之前的行）都将被视为该配方的一部分。空行和注释行可能会出现在配方行之间；它们会被忽略。

这些规则的一些后果包括：

- 带有制表符的空行不是空的：它是一个空配方（见第 55 页第 5.9 节 [`Empty Recipes`](Empty Recipes)）。
- 配方中的注释不是 make 注释；它将原样传递给 shell。shell 是否将其视为注释取决于你的 shell。
- 在“规则上下文”中，以制表符作为行首字符缩进的变量定义将被视为配方的一部分而非 make 变量，并传递给 shell。
- 在“规则上下文”中，以制表符作为行首字符缩进的条件表达式（`ifdef, ifeq`。见第 74 页第 7.2 节 [`Syntax of Conditionals`](Syntax of Conditionals)）将被视为配方的一部分并传递给 shell。

### 5.1.1 拆分配方行 (Splitting Recipe Lines)

`make` 解释的一种方式是检查换行符之前的反斜杠 `\`。在标准的 make 语法中，可以通过在每个换行符之前放置反斜杠，将单行配方拆分为 Makefile 中的多行物理行。这样的行序列被视为单条配方行，并将调用 shell 来运行。

然而，与 Makefile 中其他地方的处理方式相反，反斜杠-换行符不会从配方中移除。反斜杠和换行符都被保留并传递给 shell。反斜杠-换行的解释方式取决于你的 shell。如果反斜杠后的下一行的第一个字符是配方前缀（默认为制表符；见特殊变量），那么该字符（仅限该字符）会被移除。空格永远不会添加到配方中。例如，此 Makefile 中 `all` 目标的配方：

```
all:
    @echo no\
    space
    @echo no\
    space
    @echo one \
    space
    @echo one\
    space
```

由四个独立的 shell 命令组成，输出为：

nospace

nospace

one space

one space

更复杂的示例，此 Makefile：

```
all : ; @echo 'hello \
    world'; echo "hello" \
    world"
```

将调用一个 shell，命令为：

echo 'hello \

    world'; echo "hello" \

    world"
