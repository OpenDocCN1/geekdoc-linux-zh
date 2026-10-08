

# 32

# addbib

| 键值 | 说明 |
| --- | --- |
| %J | 包含文章的期刊。 |
| %K | 用于定位参考文献的关键词。 |
| %L | refer 命令 -k 选项使用的标签字段。 |
| %M | 贝尔实验室备录（未定义）。 |
| %N | 卷内页码。 |
| %O | 其他注释，打印在参考文献末尾。 |
| %P | 页码。 |
| %Q | 团体作者或外国作者（不反转）。 |
| %R | 报告、论文或论文（未出版）。 |
| %S | 系列标题。 |
| %T | 文章或书籍标题。 |
| %V | 卷号。 |
| %X | roffbib 使用的摘要，refer 不使用。 |
| %Y, Z | 被 refer 忽略。 |

# 示例

以下示例创建了一个名为 `bibliography` 的数据库，显示指令，添加一个条目，然后通过 `vi` 编辑器显示数据库内容。

```
castle@ addbib bibliography
Instructions? y
```

addbib 将提示你输入各种文献学字段。如果你不需要某个字段，只需按回车，该字段将不会出现在输出文件中。如果你想回到骨架中的之前的字段，输入单个减号 `-` 将每次退回一个字段。（这是输入多个作者的最佳方式。）如果你必须继续某个字段或添加不寻常字段，末尾的反斜杠 `\` 将允许临时转义。最后，系统会提示你根据所需的行数输入摘要，并以 `ctrl-d` 结束。要退出，在被询问是否继续时输入 'q' 或 'n'。要编辑数据库，请输入 'edit'、'vi' 或 'ex'。

| 作者: | Janice Winsor |
| 标题: | Opening the Dream Door |
| 期刊: | |
| 卷号: | |
| 页码: | 153 |
| 出版社: | Merrill-West Publishing |
| 城市: | 加利福尼亚州，卡梅尔 |
| 日期: | 1998 |
| 其他: | |

关键词：梦想，心理发展

摘要：(ctrl-d 结束)

不仅仅是另一本解梦书！Opening the Dream Door 是一本心理发展的实用指南。该书以亲切、个人化的风格编写，《Opening the Dream Door》并不尝试解释梦的符号。作者认为，每个人都有自己的个人神话和符号，这些无法通过集体方式进行解读。通过以自己的梦为例，Janice Windsor 为扩展潜意识生活和与其他领域联系提供了实用的建议。书中以易于懂的方式教授了记忆和访问梦境的过程。

是否继续? vi

#A Janice Windsor
#T Opening the Dream Door
#P 153

#X Merrill-West Publishing
#C Carmel, California
#D 1998

K dreams, psychic development
X 不仅仅是另一本解梦书！Opening the Dream Door 是一本心理发展的实用指南。该书以亲切、个人化的风格编写，《Opening the Dream Door》并不尝试解释梦的符号。作者认为，每个人都有自己的个人神话和符号，这些无法通过集体方式进行解读。通过以自己的梦为例，Janice Windsor 为扩展潜意识生活和与其他领域联系提供了实用的建议。书中以易于懂的方式教授了记忆和访问梦境的过程。

~

"bibliography" 27 行，946 个字符

# 属性

后续属性的描述请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNmcu |

# 参见

ed(1), ex(1), indxbib(1), lookbib(1), refer(1), roffbib(1), sortbib(1), vi(1), attributes(5)

# admin, sccs-admin — 创建和管理 SCCS 历史

文件

# 概要

```
/usr/ccs/bin/admin [-bhnz] [-a username |groupid]... [-d flag...]
[-e username |groupid]... [-f flag [value]]... [-i [filename]]
[-m mr-list] [-rrelease] [-t [description-file]] [-y[comment]]
s.filename...
```

# 描述

参见 sccs-admin(1)。

# aedplot — 各种绘图仪的图形过滤器

# 概要

```
/usr/ucb/plot [-Tterminal]
```

# 描述

参见 plot(1)。

# alias, unalias — 创建或删除别名

# 概要

```
/usr/bin/alias [alias-name=[string]...
/usr/bin/unalias alias-name...
/usr/bin/unalias -a
```

# csh

```
alias [name [def]]
unalias pattern
```

# ksh

```
*
alias [-tx] [alias-name=[value]...
unalias alias-name...
```

# 描述

alias 命令允许你定义简单的别名。别名是命令或系列命令的别名或简写术。别名在 C shell 和 Korn shell 环境中的功能有所不同。

# alias, unalias

你指定想要作为别名的名称，并定义一些文本，每当该词作为命令使用时，shell 会将其替换为该文本。例如，由于一名工程师将 `more` 命令误拼为 `moer`，他创建了一个别名，这样当他输入 `mo` 时就会执行 `more` 命令。你也可以创建别名来简化复杂的命令。使用 unalias 命令删除别名。

别名可以包含任意数量的词，只要将它们括在引号中。你还可以包含几个通过管道连接的命令。

`/usr/bin` 目录包含 alias 和 unalias 命令。C shell 和 Korn shell 也内置了 alias 和 unalias 命令。Bourne shell 不提供别名功能。根据环境的不同，定义别名的语法略有不同。

/usr/bin/alias

/usr/bin/unalias

显示已定义的别名列表，输入 alias 并按回车。别名定义影响当前 shell 的执行环境以及当前 shell 子 shell 的执行环境。当按照此处指定使用时，别名定义不会影响当前 shell 的父进程或由 shell 调用的任何命令。

unalias 命令删除指定的每个别名名称的定义。从当前 shell 环境中删除这些别名。

C Shell
要在标准输出上显示已定义的别名列表，输入不带参数的 alias 并按回车。

要为当前 shell 定义别名，输入 alias 名称并按回车。由于它们是保留字，你不能使用 alias 或 unalias 名称。

要在标准输出上显示已定义的别名列表，输入不带参数的 alias 并按回车。

要为当前 shell 定义别名，输入 alias 名称并按回车。由于它们是保留字，你不能使用 alias 或 unalias 名称。

要在标准输出上显示已定义的别名列表，输入不带参数的 alias 并按回车。

要为当前 shell 定义别名，输入 alias 名称并按回车。由于它们是保留字，你不能使用 alias 或 unalias 名称。

要在标准输出上显示已定义的别名列表，输入不带参数的 alias 并按回车。

要为当前 shell 定义别名，输入 alias 名称并按回车。由于它们是保留字，你不能使用 alias 或 unalias 名称。

要在标准输出上显示已定义的别名列表，输入不带参数的 alias 并按回车。

要为当前 shell 定义别名，输入 alias 名称并按回车。由于它们是保留字，你不能使用 alias 或 unalias 名称。

# 36

# alias, unalias

**注意** — 如果你在 `.profile` 文件中设置别名，只有登录 shell 可以访问它们，除非你使用 `-x` 选项将其导出。你之后调用的任何 shell（例如 xterms 或 Windows 环境）将没有导出的别名。

要创建一个 Korn ENV 文件，创建一个名为 filename 的文件并将别名放入其中。然后使用以下命令导出环境文件：

```
ENV=filename; export ENV
```

# 选项

# Korn Shell

Korn shell 为内置 alias 命令提供了选项。

- -t 创建跟踪别名。Korn shell 会记录命令的完整路径名，以便更快找到它并在任何目录下分发。如果你没有提供 alias-name 参数，则列出所有当前的跟踪别名。

- -x 导出别名以便在脚本和其他子 shell 中使用。如果你没有提供 alias-name 参数，则列出所有导出别名。

unalias 支持以下选项：

- -a 从当前 shell 环境中删除所有别名定义。

# 操作数

alias 支持以下操作数：

- alias-name 将别名定义写入标准输出。

unalias 支持以下操作数：

- alias-name 要删除的别名名称。

- alias-name=string 将 string 的值赋予别名 alias-name。

当你未指定操作数时，所有的别名定义都被写入标准输出。

# 输出

（未指定操作数或仅指定名称操作数时）显示别名的格式为：

```
"%s=%s\n" name, value
```

值字符串将带有适当的引号写入，使其适用于重新输入到 shell 中。

