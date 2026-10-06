

```
me@linux share $ cd bin
me@linux bin $ pwd
/usr/local/bin
```

只要路径没有歧义，路径就可以缩写。如果我们输入：

```
me@linux ~ $ ls /usr/share<tab>
```

zsh 将其展开为：

```
me@linux ~ $ ls /usr/local/share/
```

这可以节省大量的输入工作！许多命令都提供了参数。要调用此功能，我们只需要输入命令以及选项开头的横杠，然后按下按键：

```
me@linux ~ $ rm <-tab>
--force 忽略不存在的文件，永不提示
--help 显示帮助信息并退出
-i 在删除前提示
-i 在删除多个文件时提示
-i-interactive 在特定条件下进行交互式提示（默认始终总是提示）
--preserve-root 不特殊对待 /
--one-file-system 仅留在所给参数指定的文件系统中
--preserve-root 不删除 /（默认）
--recursive -R r 递归地删除目录及其内容
--verbose 解释正在执行的操作
--v 输出版本信息并退出
```

这显示了命令的选项列表，就像 `cd` 命令一样，反复按下 tab 键 zsh 会循环切换这些选项。

## 路径扩展 (Pathname Expansion)

Shell 为路径扩展提供了几个强大的增强功能，可以在指定文件参数时节省步骤。我们可以使用 `**` 来触发递归扩展。例如，如果我们想在主目录及其子目录下列出所有以 .txt 结尾的文件，在 bash 中我们必须这样做：

```
me@linux $ find -name "*.txt" | sort
```

在 zsh 中，我们可以这样做：

```
me@linux ~ $ ls **/*.txt
```

并得到相同的结果。如果这还不够酷，我们还可以为通配符添加限定符（qualifiers），以执行 `find` 命令可以进行的许多测试。例如：

```
me@linux ~ $ **/*.txt
```

将只显示名称以 .txt 结尾的文件和符号链接。支持许多限定符，并且可以将它们结合起来以进行细粒度的选择。以下是一些示例：

| 限定限符 | 描述 | 示例 |
| :--- | :--- | :--- |
| - | 普通文件 | ls * (.) |
| / | 目录 | ls * (/) |
| @ | 符号链接 | ls * (@) |
| * | 可执行文件 | ls * (*) |
| F | 非空目录 | ls * (^F) |
| ^ | 空目录 | ls * (m) |
| m | n 前修改过 | ls * (m-5) |
| m-n | 在 n 天前修改过 | ls * (m+5) |
| m+n | 超过 n 天未修改 | ls * (L) |
| L | 空（长度为 0） | ls * (LM+5) |
| LK-n | 小于 n 千字节的文件 | ls * (LK0) |

## 全局别名 (Global Aliases)

Shell 提供了强大的别名功能。在 zsh 中，我们可以按照通常的方式定义别名，例如：

```
me@linuxbox ~ alias vi=/usr/bin/vim
```

它的行为会和 bash 中完全一样。但我们也可以定义全局别名，它可以在命令行的任何位置使用，而不仅仅是开头。例如，我们将一个常用的名称定义为别名：

```
me@linuxbox ~ alias -g ls='/var/log/syslog'
```

然后在命令行的任何地方使用它：

```
me@linuxbox ~ $ ls
```

使用别名名称并不是强制的，它只是为了方便查看的自定义习惯。我们还可以使用全局别名来定义常见的重定向：

```
me@linuxbox ~ $ alias -g L='| less'
```

或者

```
me@linuxbox ~ $ alias -g W='| wc -l'
```

然后我们就可以执行这样的操作：

```
me@linuxbox ~ $ cat /var/log/syslog
```

来显示行数。

## 后缀别名 (Suffix Aliases)

此外，我们可以通过定义后缀别名来定义类似于“用...打开”的功能。例如，我们可以定义一个别名，表示所有以“.txt”结尾的文件都用以下方式查看：

```
me@linuxbox ~ alias -s txt='less'
```

然后我们只需要输入文本文件的文件名，它就会由别名指定的应用程序打开：

```
me@linuxbox ~ dir-list.txt
```

这有多酷？

## 改进的历史搜索 (Improved History Search)

zsh 为历史搜索增加了一个巧妙的技巧。在 bash（以及 zsh 中）中，我们可以通过按下 Ctrl-r 执行反向增量历史搜索，随后的每次按键都会缩小搜索范围。zsh 更进一步，只需在命令行输入目标搜索字符串的几个字母并按下向上方向键。它会回溯历史查找第一个匹配项，每次按下向上方向键都会显示下一个匹配项。

## 环境变量编辑 (Environment Variable Editing)

zsh 提供了一个名为 `varied` 的内置命令来编辑 shell 变量。例如，如果我们想快速更改 PATH 变量，可以这样做：

```
me@linuxbox ~ $ varied PATH
```

PATH 变量的内容会出现在命令编辑器中，这样我们可以进行更改并按回车键，更改就会生效。

## 框架 (Frameworks)

我们只触及了 zsh可用功能的一部分。它非常丰富。但由于配置 zsh 以充分利用其潜力的复杂性很大，可能会令人望畏。在这里，手册页（man page）只是涵盖其他 10 多页各种主题的目录。幸运的是，许多社区已经涌现出来，提供了为 zsh 提供现成配置的框架。其中最流行的是 Oh-MyZsh，由 Robby Russell 领导。Oh-MyZsh 是大量的配置文件、别名和主题。它支持许多软件开发和系统管理任务。

## 切换 Shell (Changing to Another Shell)

现在我们已经了解 Linux 可用的不同 shell，如何尝试它们呢？首先我们可以直接从 bash 提示符输入 shell 的名称。这将作为 bash 的子进程启动第二个 shell：

```
me@linuxbox ~ $ tsh%
```

在这里我们启动了 tsch，并看到了默认的 tsch 提示符百分号。由于我们没有为新 shell 创建任何配置文件，得到的是基础环境。每个 shell 都有自己的交互式配置文件，就像 bash 有 .bashrc 文件来配置其会话一样。

以下是配置文件：

| Shell | 配置文件 |
| :--- | :--- |
| dash | ~/.profile |
| bash | ~/.bashrc |
| ksh | ~/.kshrc |
| tsch | ~/.tcrc |
| zsh | ~/.zshrc |

我们需要参考相应的 /usr/share/doc 目录。要退出 shell，只需输入 exit 命令：

```
me@linuxbox ~ $ exit
```

一旦我们完成了实验，就可以使用 chsh 将默认 shell 从 bash 更改为 zsh。例如，从 bash 切换到 zsh 使用：

```
me@linuxbox ~ $ chsh /bin/zsh
```

该名称必须出现在 /etc/shells 中。

## 总结

由于 Linux 在类 Unix 系统中日益流行，bash 已成为世界上最主要的 shell。它拥有早期 shell 的许多优秀特性以及一些自己的技巧。然而，如果需要轻量级和脚本执行（例如在嵌入式系统中），dash 是一个很好的选择。同样，如果需要与其他系统交互，ksh 将提供必要的兼容性。对于我们这些冒险者来说，zsh 的高级交互功能可以增强我们的日常 shell 体验。

