

## bash 配置文件

与大多数 shell 一样，*bash* 在启动时会查看多个配置文件，以设置初始值和环境变量。具体查看（source）哪些文件以及查看的顺序，取决于 shell 的启动方式，在一定程度上也取决于运行它的发行版。例如，OpenLinux 拥有比 *bash* 通常使用的更复杂的启动文件序列。

*登录* shell（从登录提示符启动，或使用 *-login* 选项启动的 *bash*）的正常序列如下：

- `/etc/profile`
  - bash 和 Bourne 类型的 shell 首先会读取此文件。它包含适用于所有 Bourne shell 的系统级默认值。
- `~/.bash_profile`
  - 然后 bash 尝试读取这个 bash 和用户特定的文件。
- `~/.bash_login`
  - 然后 bash 尝试读取这个 bash 和用户特定的文件。
- `~/.profile`
  - 最后 *bash* 尝试读取这个 Bourne 类型和用户特定的文件。
- `~/.bash_logout`
  - 退出时，它尝试读取此文件（99% 的情况下该文件仅包含用于清屏的 `clear` 命令）。

在 OpenLinux 中，这个过程稍显复杂。文件 `~/.bash_profile` 和 `~/.bash_login` 并不存在（在发行版安装中）。当你登录到 OpenLinux 时，流程如下：

`/etc/profile`

*bash* 最初读取这个文件。

`~/.profile`

*bash* 然后读取这个文件。它旨在保存适用于任何 Bourne 类型 shell 的用户特定设置。接着它会引入下一个文件：

`~/.bashrc`

此文件通常用于保存 bash 和用户特定的设置。然而，OpenLinux 发行版打算让此文件保存由安装程序设置的每个用户的变量。（在 OpenLinux 中，`.bashrc-private` 起到了其他系统中 `.bashrc` 通常起到的作用。）接着它会引入下一个文件：

`/etc/config.d/shells/bashrc`

这是交互式 shell 的系统级初始化文件（此文件是 OpenLinux 独有的，因此仅适用于 OpenLinux），它读取：

`~/.bashrc-private`

此文件也是 OpenLinux 独有的，旨在保存特定用户的设置，在其他系统中这些设置通常保存在 `~/.bashrc` 中。此文件处理完成后，控制权返回到：

`~/.profile`

它引入 ...

`/etc/config.d/shells/profile`

此文件保存适用于任何 Bourne 类型登录 shell 的系统级默认值（此文件也是 OpenLinux 独有的）：

`~/.profile-private`

最后读取此文件。它旨在保存适用于任何 Bourne 类型 shell 的用户特定设置。这同样是 OpenLinux 独有的特性。实际上，该文件在 OpenLinux 的默认安装中并不存在（但如果存在，它会被读取）。

`~/.bash_logout`

退出时，读取此文件（在 OpenLinux 中，该文件仅包含清屏命令）。

此外，如果可用，交互式 shell 可以读取 `~/.inputrc` 文件（OpenLinux 默认不包含此文件）以获取按键绑定。

对于交互式但非登录的 shell（即不带 -login 选项的 bash），仅读取 `~/.bashrc` 文件（由 bash 本身读取）。当然，在 OpenLinux 中，`~/.bashrc` 会引入 `/etc/config.d/shells/bashrc` 和 `~/.bashrc-private`。

非交互式 shell（通常是由程序启动或从程序中启动的 shell）将读取 BASH_ENV 变量指向的文件，然后读取 ENV 变量（如果其中任何一个存在）。

此外，如果 bash 作为 sh 被调用（即作为 /bin/sh 而非 /bin/bash 启动），它仅读取 /etc/profile 和 ~/.profile（但你已经看到在 OpenLinux 下这些文件会引入哪些内容）。

基本上，在 OpenLinux 中配置 bash 归结为查看所有上述文件以了解它们的作用。这一练习为了解 shell 变量和命令的工作原理提供了极佳的教材。

然而，你通常只需要修改 ~/.bashrc-private 即可将 shell 配置为你想要的方式。

## tcsh

tcsh 是 C shell (csh) 的修改版本。它完全向后兼容 csh，但包含了许多新功能，使用户交互更加容易。相对于 csh 最大的改进在于命令行编辑和历史导航领域。你会发现 tcsh 和 bash 有许多共同点，每个 shell 都有一些使其具有独特性的“特殊功能”。进行一些实验并熟悉自己的工作风格，将帮助你确定这些 shell 中哪一个对你来说更舒适、更有用。

### 比较 tcsh 和 bash

C shell 最初由 Bill Joy（因 Sun 公司而闻名）在开发 BSD UNIX 时创建。基本上，它是为了在 shell 中模拟 C 语言语法而编写的（因此得名），因为许多程序员觉得 Bourne 语法令人不快。事实证明，早期版本的 csh 存在一些缺陷，这些缺陷在编程中最为显眼和频繁地出现；因此，具有讽刺意味的是，csh 作为登录 shell 在日常用户中变得更加流行，而许多专业人士继续用 sh 编写程序。

bash 中的许多有用功能在 tcsh 中也存在，甚至工作方式相同（例如，命令补全、通配符和输入/输出重定向）。其他功能，如命令历史，是相似但不完全相同的；tcsh 还提供了 bash 中不可用的功能，例如拼写纠正。

### tcsh 命令摘要

以下是一些最实用的 tcsh 命令的简要列表：

- **alias** 用于设置和显示别名，即可由用户设置的命令昵称。
- **bg** 后台命令。用于强制挂起的进程在后台继续运行。
- **bindkey** 允许用户更改与按键序列相关联的编辑操作。
- **cd** 允许用户将当前工作目录更改为指定的目录。
- **exit** 允许用户终止 shell。
- **fg** 前台命令。用于强制挂起的进程在前台继续运行。
- **history** 允许用户显示和修改历史列表和历史文件的内容。
- **kill** 允许用户终止另一个进程。
- **logout** 允许用户终止登录 shell。
- **set** 用于设置 tcsh 变量的值。
- **source** 用于读取并执行文件的内容。
- **unalias** 用于移除使用 alias 命令定义的别名。

这些命令的更多细节和用法示例可在 tcsh 的手册页中找到。在提示符下，输入：

```
man tcsh
```

## 命令历史

tcsh shell 提供了一种访问命令历史的机制，这与 bash 中的机制类似。shell 会记住输入到 shell 的最后 $HISTSIZE 条命令（其中 $HISTSIZE 是一个可由用户定义的 tcsh 变量）。

tcsh 在历史列表中存储最后 $HISTSIZE 条命令的文本。当你登录到你的账户时，历史列表从历史文件初始化。此历史文件的默认文件名是 .history，但你可以使用 $HISTFILE tcsh 变量更改它。此文件位于你的主目录中。（请注意，该文件以句点开头。这意味着该文件是一个隐藏文件，只有使用 ls 命令的 -a 或 -A 选项时，它才会出现在目录列表中。）

### 注意

为了将历史列表保存在历史文件中，你必须确保 savelist 变量已设置为你想要保存的命令数量。

使用历史列表最简单的方法是使用向上和向下箭头键滚动浏览之前输入的命令。按向上箭头键将使最后输入的命令出现在命令行上。再次按向上箭头键会将之前的命令放置在命令行上，以此类推。如果你在命令缓冲区中向上移动超过了你想要的命令，你可以通过按向下箭头键一次移动历史列表中的一个命令向下。

命令行上的命令可以被编辑。你可以使用左移和右移箭头键在命令行上移动，并可以在任何位置插入文本。你

