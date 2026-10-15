
`irc` 命令显示一个滚动的屏幕，屏幕底部有一个命令行。

## FIGURE 20.2

- 2. 如果你是第一次使用 `irc`，请使用 `/HELP` 命令，后跟关键词 `superuser`，如下所示：
`> /HELP newuser`

显示器将打印出一一两个屏幕的有用信息。你也可以通过使用 `/HELP` 命令后接以下关键词或主题来浏览 `irc` 命令的帮助功能并阅读介绍信息：`basics`（基础）、`commands`（命令）、`etiquette`（礼仪）、`expressions`（表达式）、`intro`（介绍）、`irc`、`menus`（菜单）、`superuser`（新用户）和 `rules`（规则）。

- 3. 要查看服务器上活跃聊天组的列表，在 `irc` 命令行上使用 `/LIST` 命令，如下：
`> /LIST`

稍等片，屏幕会滚动显示当前讨论组列表，如图 20.3 所示。

| Assignment | Apple Buys 5% of Apple Stock Today, Manager/Buyout Is |
| :--- | :--- |
| Class | It's not April-fool's joking... April looks is* |
| E-mail | |
| E-chat | |
| IRC | |
| Tutorial | help groups and discussion - the portal - |
| Exercises | |
| Projects | |
| Presentation | Real & Study vs. Czech and Chong |
| Reading | Peter's Last was the once, cons, col. |
| Writing | |
| Speech | I won't be on tonight, just sleep... see you tomorrow |
| Video | --.Sticker is in the Penthouse |
| Web | Relatlessness makes lives - A weakness needs a war loss for needs a bicycle Not that is 'flaming' |
| Meeting | |
| Discussion | |
| Homework | |
| Exercises | |
| Other | |
| Other | |
| Other | |
| Assignment | Apple Buys 5% of Apple Stock Today, Manager/Buyout Is |
| Class | It's not April-fool's joking... April looks is* |

## FIGURE 20.3
`IRC` `LIST` 命令显示当前讨论组的列表。

- 4. 要查看特定群组成员的详情，使用 `/WHO` 命令，后接组名，如下：
`> /WHO #giggles`

`IRC` 命令会列出任何成员的名字。

- 5. 要成为某个组的成员，使用 `/JOIN` 命令，后接组名，如下：
`> /JOIN #giggles`

你的屏幕会滚动显示消息，如图 20.2 所示。

- 6. 要退出 `irc` 程序，使用 `QUIT` 命令并按回车键。

另另

- 关于启动的更多信息，请第 25 页。

# 编写 Shell 程序

Shell 程序类似于 DOS 世界中的批处理文件（`batch files`）。然而，与 DOS 批处理文件不同，Shell 程序具有更先进的功能；它们类似于传统的编程语言。关于大多数可用的 Shell 已经有整本书著作；本章仅涵盖 `bash`，因为它是最受欢迎的，而且它是 Red Hat、Caldera 以及大多数流行的 Linux 发行版中默认使用的 Shell。

# 良好的编程实践

良好的 Shell 程序应该是易于阅读和理解的。如果其他人必须修改你的工作，或者如果你在几个月后回来修复或扩展某些内容，这一点至关重要。编写得糟糕的代码非常难以处理和理解。如果代码没有经过正确的格式化和注释，不要怀疑自己是否记得自己写过的内容（更不用说别人写的内容了）。我不喜欢说教，但在查看示例时，请提醒自己：缩进等设计是为了帮助你理解代码的。请给那些需要处理你代码的人以礼貌。

一个简单的脚本由常规 Shell 命令组成，即那些在命令行中交互式输入的命令。Shell 还可以定义仅在脚本使用的命令。因为在需要修改或修复 Shell 脚本时，记录你正在做什么是非常方便的，所以可以通过在行首加上 `#` 字符在脚本中包含注释行。`bash` 然后会将行的其余部分视为注释。

当情况变得复杂时，缩进是帮助代码可读性的重要工具。空行也可以使用。然而，过多的空行、缩进和注释会让代码看起来和把所有内容挤在一行一样杂乱。

# 示例程序

世界不需要另一个“Hello, World!”程序了。相反，我想向你展示一些实用的东西。例如，假设你想对当前目录下的内容进行格式化良好的打印输出。列表 21.1 显示的代码提供实现这一点的方法（每行开头的数字是供你使用的；它们实际上不会出现在代码中）。

# 第五部分 系统管理

# 第 21 章 基础 Shell 编程

## Listing 21.1 printdir 将经过适当分页的文件和目录列表发送到打印机

```bash
#!/bin/bash
# Sample Program for Practical Linux
# Jan Walter jwater@rogers.wave.ca
# Practical, Chapter 21
# Copyright 2000 Macmillan Computer Publishing and Jan Walter
# All rights reserved.
# This code comes without warranty of any kind. If it breaks you
# to keep both pieces.
ls -l >/tmp/lstmp
pr /tmp/lstmp | lpr
rm /tmp/lstmp
# End of script
```

该脚本在你普通用户而非系统管理员身份登录时效果最好；它假设你已经安装并正确配置了打印机。简单来说，它按顺序执行文件中的命令。此列表最有趣的方面如下：

- 第 1 行告诉系统应该启动哪个 shell 来执行脚本。这至关重要，因为不同的 Shell 程序支持不同的内置命令。

- 第 9 行执行 `ls -l` 程序并将输出重定向到系统临时目录中的一个文件。

- 第 10 行将内容传递给 `pr`（它将文件分成若干页，并根据参数对页面进行编号、添加更美的页眉等），并将 `pr` 的输出传递给 `lpr`（系统打印后台处理程序）。这里的重点是命令输出的重定向，而不是命令本身。

- 第 11 行删除第 3 行创建的临时文件。（提醒：确保你的程序对系统上的其他用户是礼貌的，并在完成后清理现场。）

现在尝试你的脚本：

1. 启动一个编辑器，如 `joe`，如下：

`joe printdir`

2. 编辑器启动后，输入列表 21.1 中的脚本文本。

3. 如果你使用的是 `joe`，按 `Ctrl+K`，然后按 `X` 保存文件并退出。

4. 你仍然需要告诉 Linux 该文件确实是它可以执行的。要做到这一点，使用 `chmod` 命令：

`chmod +x printdir`

5. 通过执行以下命令尝试你的作品：

`./printdir`

你的 shell 应该输出一份你目录内容的长列表。承认所有这些都可以通过以下命令在命令行轻松完成：

`ls -l | pr | lpr`

这确实创建了一个长目录列表，包含文件权限、大小等，并使用管道重定向了程序的输出。在这种情况下，输出被发送到 `pr`，它将文本格式化为美观的 60 行一页，带有页码、时间和日期，然后 `pr` 的输出被传递给 `lpr`。

> 注意
> 你可以使用 `man` 命令在系统手册中查找这些命令。

厌倦了输入 `/bin` 来启动脚本吗？

你可以将使用的脚本放在家目录下的 `bin` 目录中。该目录的内容始终在你应用程序路径中（系统在查找不带目录名前缀的程序时搜索的目录），这允许你在不使用常规系统程序的情况下使用脚本。请注意，这样做会带来安全风险。例如，如果一个名为 `ls` 的恶意磁盘破坏程序进入了你的 `/bin` 目录，那么每当你想列出目录时，都可能运行它。

尽管如此，重点在于你现在可以使用更简单的命令 `./printdir` 完成所有操作。这个想法也适用于那些实际执行操作的大型脚本。在列表 21.2 中，shell 显示了实际发生的情况。（注：由于 OCR 文本存在大量重复，已根据逻辑流清理了输出）。

# 第五部分 系统管理

# 第 21 章 基础 Shell 编程

## 修改登录 shell 中的变量
