

## 命令 Shell 简介

你之前已经学习过 vi 可以在 .exrc 文件中存储默认信息，程序也可以从环境变量 `EXINIT` 中读取配置信息。我将所有的模式搜索都设为不区分大小（也就是说，搜索 `precision` 会匹配 `Precision`），我在 `EXINIT` 中设置了相应的 vi 变量。我的设置是 `:set ignorecase`。如果你希望始终显示行号，可以轻松地将 `EXINIT` 设置为 `:set number`。

我经常使用的另一个程序是 `rn`，或者说读取 Netnews。电子邮件相当于通过邮政服务收到的信件和杂志，而 Networks 相当于电子版的超级公告板。区别在于它有成千上万个不同的板，每当在任何板上钉一条笔记时，该笔记的副本都会发送到世界各地的 UNIX 系统。现在你可以看到我为 `rn` 程序定义了三个环境变量：`RNINIT`，我的个人 `rn` 配置选项；`SUBLINE`，表示新消息主题行的显示格式；以及 `ORGANIZATION`，指示我所属该系统的具体组织。它们如之前所示。

你可以为自己定义许多环境变量。UNIX 程序有自己的环境变量，允许你根据自己的需求和偏好定制程序的行为。UNIX 本身有几个环境变量，在你成为专家之前，我建议你习惯于查看这些变量并确保它们具有合理的值，而不是修改它们。请特别关注表 14.1 中定义的变量集。如果它们错了，可能会带来麻烦；而如果其他环境变量错了，通常不会太有麻烦。

## 任务 14.5：探索 csh 配置文件

C shell 使用两个文件进行配置，尽管这两个文件都不一定存在，但你都可以在家目录下找到它们：`.login` 和 `.cshrc`。它们之间的区别微妙但非常重要。`.login` 文件在每次启动 C shell 时都会读取。因此，当你登录并进入 `:vi` 时，vi 会通过启动一个新的 shell 然后将命令传递给 csh 来执行该命令。因此，从 vi 等程序内部启动的新 csh shell 将无法看到在 `:login` 中启动的关键 shell 变量。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_326_0.png)

## 操作

- 1. 首先，使用 `cat` 列出我的 .login 文件的内容。记住，任何以 `#` 开头的行都是注释并会被忽略。

```bash
% cat .login
#
# @($)Revision: 62.2 $
setenv TERM vt100
stty "^H" "^U" intr "^C" eof "^D"
stty crtybs crterase      # special DMIX stuff for bs processing
# shell vars
set noclobber history=100 savehist=50 filec
# set up some global environment variables...
setenv ignorecase
# Some RN related variables...
setenv RNINIT      -hmessage -reference -hdate-r -hsender -summary
hthely -dhistr -htlines -hline -hfoillow -hnews -hkey -hresent -htreturn
hto -ht-original -hx-sun -hx-nodeoriginator -hnntp
setenv SUBLINE       "-st--%s"
setenv ORGANIZATION  "Educational Computing group, School of Education
setenv NAME "Dave Taylor"

newmail

mesg y
```

一旦删除了所有注释，这就非常直接。三种不同类型的环境配置命令是：`setenv`、`stty` 和 `set`。

`setenv` 命令定义环境变量；事实上，你可以看到上一个单元显示的所有变量都定义在我的 .login 文件中。我使用 `stty` 设置与我的终端相关的特定配置选项（`stty "set tty driver options"`）。我用它来确保 `^h` 擦除（退格），`^u` 是一个方便的快捷键，允许我删除整整行，而 `^c` 向正在运行的程序发送中断。我用 `^d` 表示文件结束符（EOF）。上一个输出示例的第二行表示 CRT 能够在显示器上进行退格和删除字符。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_327_0.png)

## 命令 Shell 简介

这里有更晦奥的 UNIX 术语：CRT（如在 `stty crtabs` 中使用，或指阴射线管）用于标准终端屏幕的技术。然而，“终端”（Terminal）已不再准确，因为 `stty crtabs` 命令也适用于我的 LCD（液晶显示二极管，如果你非要知道的话）笔记本。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_328_0.png)

最后，`set` 命令是 C shell 的配置。我告诉 C shell 在使用文件重定向覆盖现有文件之前警告我（`noclobber`），记住最后 100 条命令（`history=100`），并且如果我注销并重新登录，记住其中的 50 条（`savehist=50`）。我还希望 C shell 尽可能为我补全文件名，即 `the file`。注意这里有两种类型的设置：开启/关闭选项（如 `noclobber`）以及我必须分配特定数值的选项。

C shell 还有条件语句和各种其他命令来指示运行哪些命令。在这里，我使用 `if (expression) then` 来定义一组仅在 shell 是交互式运行时使用的命令（也就是说，我能够输入命令）。这种非交互式 shell 的示例是在编辑器内输入此内容时创建列表的 vi。`$prompt true` 如果为 shell 有提示符（也就是说，如果它是交互式的）。如果不是，该变量为假，shell 将跳转到 `endif` 然后继续执行命令。

然而，如果是交互式 shell，我创建了几个别名并定义了一些 C shell 配置选项，以确保它们在子 shell 中始终被设置。设置了 `umask` 值，然后我调用 `prompt`，这是一个命令别名，用于运行命令 `setprompt="$system (cwd) \ :"`。

