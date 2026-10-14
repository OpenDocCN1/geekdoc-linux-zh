

- 使用历史编号。
- 使用命令的开头部分。
- 搜索历史列表。

术语“history number”指的是历史列表中每个条目左侧的编号。例如，在前面的历史列表中，第一项的历史编号为 33。

你可以通过在命令编号前加上感叹号来执行历史列表中的任意一条命令。感叹号在 UNIX 和 Linux 中有时被称为 bang。因此，要执行我们示例中最新的 mount 命令，你输入 !41（读作“bang forty-one”）。

Shell 会显示与该编号匹配的命令并立即执行它。如果你已经知道要执行的命令的编号，就不需要先查看历史列表再使用此技巧。但请注意，随着你输入新的命令，编号会发生变化。

要使用命令名重复一条命令，请使用感叹号后跟上你想要重复的命令的第一部分。在所示的示例历史输出中，你可以使用以下命令执行最新的 mount 命令：

```
# !mou
```

执行此命令时，shell 会搜索最近以字母 “mou” 开头的命令并执行它。

![](img/43f64015de86d989e30eff5bb284fb96_144_0.png)

使用上述三种方法中的任何一种从历史列表执行命令时，请记住，命令都是从你当前的工作目录执行，这可能与它们最初被执行时的目录不同。如果一条命令不包含完整路径名，你可能会看到意外的结果。在使用部分命令名方法重新执行命令而不检查命令的完整文本时，尤其要小心。

你也可以在不重新执行命令的情况下搜索历史列表，以查看命令参数是什么或你是如何完成某项任务的。此方法需要使用管道符号（ | ）和 grep 命令，这些内容将在本章后面以及第 5 章“Understanding Text Processing”中讨论。要使用此方法，输入 history 命令，然后是管道符号，然后是 grep 命令和你想要查找的命令名。例如，在前面所示的示例历史输出中，假设你想搜索 mount 命令以查看它包含哪些参数。以下命令会显示历史列表中包含 mount 命令的所有条目。然后你可以查看显示的输出以了解之前执行的命令。

```
# history | grep mount
```

bash shell 支持执行命令的额外技巧。但这里所示的关于使用 Tab 补全和 history 命令的示例应该能帮助你在 Linux 中更高效地输入命令。要了解有关这些功能的更多信息，请通过输入 man bash 查看 bash shell 的在线手册页。

## The Shell Start-up Process

登录 Linux 或启动新的 shell 时会执行多个脚本。这些脚本会初始化（或配置）你环境中的各个部分。

当用户首次登录 Linux 系统时，会执行脚本 /etc/profile。/etc/profile 脚本包含适用于系统上每个用户的配置信息。每个用户的 home 目录可以包含另一个名为 .profile（以句点开头）的启动脚本。用户登录时也会执行用户 home 目录中的 .profile 脚本，但 .profile 脚本特定于单个用户。每个用户的 home 目录可以包含不同的 profile 脚本。只有 root 用户可以更改 /etc/profile 脚本；任何用户都可以更改其 home 目录中的 .profile 脚本。

![](img/43f64015de86d989e30eff5bb284fb96_145_0.png)

> Linux 中以句点开头的任何文件名都是隐藏文件。这与其说是安全功能，不如说是一种方便的方式，让很少更改的文件保持在视线之外。要查看包含所有隐藏文件的列表，请使用 ls 命令的 -a 选项。在你的 home 目录中，命令 ls -a 会生成一份包含大量隐藏配置文件 的长列表。

在某些系统上，用户登录时还会执行额外的脚本。例如，在 Red Hat Linux 中，/etc/profile.d 目录中的一组脚本由 /etc/profile 脚本启动。/etc/profile.d 目录中的脚本为许多不同的 Linux 程序添加特定的配置信息。Red Hat Linux 还使用名为 .bash_profile 的文件，而不是每个用户 home 目录中的标准 .profile 脚本。

profile 脚本在用户登录时执行；启动 shell 时会执行额外的脚本。因为用户在文本模式屏幕登录时 shell 会立即启动，所以这些额外的脚本通常在 profile 脚本之后立即执行。在图形环境中工作的用户可以在不再次登录 Linux 的情况下启动多个 bash shell。当已登录的用户启动新 shell 时，下文所述的额外脚本（如 /etc/bashrc）会被执行；但是 profile 脚本不会再次执行。

一些 Linux 发行版，包括 Red Hat Linux，提供了一个 /etc/bashrc 脚本，该脚本在每次为系统上的所有用户启动 bash shell 时都会执行。其他 Linux 发行版则依赖 /etc/profile 脚本来进行应适用于所有用户的配置设置，但该脚本仅在用户登录时执行。

每个用户的 home 目录包含一个名为 .bashrc 的脚本。每次用户启动 bash shell 时都会执行 .bashrc 脚本。用户希望添加到其环境中的任何配置信息都可以放在 .bashrc 文件中。某些 Linux 发行版有时会使用名称相似的额外脚本。示例包括以下内容：

- .bash_default，每次启动 bash shell 时都会执行
- .bash_login，每次启动 bash shell 时都会执行
- .bash_logout，每次用户关闭 bash shell 时都会执行

你可能会在 Linux 发行版上找到其他名称相似的脚本。一般来说，这些文件的名称描述了它们的使用时机。如果你不确定文件的使用方式，请咨询你的 Linux 厂商或尝试在每个文件中放置测试命令（请参阅第 14 章了解说明）。图 3-2 显示了用户登录 Linux 时典型的启动脚本执行序列。

```
/etc/profile → ~/.profile → /etc/bashrc → ~/.bashrc
                or
                ~/.bash_profile
```

### Figure 3-2 The process of executing start-up shell scripts

![](img/43f64015de86d989e30eff5bb284fb96_146_0.png)

X Window System 启动时还会执行额外的脚本。例如，用户 home 目录可能包含一个名为 .xclients 或 .xinitrc 的脚本文件，X Window System 在图形系统启动时会检查并执行它。需要注意的一个关键区别是，当用户登录或启动 shell 时，系统范围的脚本文件（如 /etc/profile）会先执行，然后执行用户 home 目录中对应的文件。但在启动 X Window System 时，系统默认文件（如 /etc/X11/xinit/xinitrc）只有在用户 home 目录中未找到对应文件时才会被执行。第 15 章“Advanced Topics and Troubleshooting”更深入地描述了这些问题。

这里描述的脚本适用于启动 bash shell 时。选择使用 C shell、Korn shell 或其他 shell 时也会执行类似的文件。例如，用户 home 目录可能包含一个名为 .cshrc 或 .kshrc 的文件。这些脚本分别在每次启动 C shell 或 Korn shell 时执行。因为每种 shell 的脚本格式不同，所以需要不同的脚本文件来初始化每种 shell。这些配置脚本可以共存于用户的 home 目录中（以及 /etc 目录中用于系统范围配置的文件），每个脚本仅在对应的 shell 启动时执行。

## Using Aliases

别名是一个在 shell 提示符下被替换为另一串字符的字符串。alias 命令让你定义 shell 如何将你在 shell 提示符下输入的一个文本串替换为另一个文本串。alias 命令的一般格式如下：

```
alias <string entered by user>=<string substituted by the shell>
```

