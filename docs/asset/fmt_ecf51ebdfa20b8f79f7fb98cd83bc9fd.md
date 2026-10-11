
`\u` 是用户名的替换符（参见 `bash (1)` 手册页的 `PROMPTING` 章节）。其他常用的替换符包括：

- `\h` 主机名（短格式，不包含域名）
- `\!` 历史编号
- `\w` 当前目录。由于这可能很长，你可以使用 `\W` 只显示最后一个组件。
- 如果作为用户账户运行显示 `$`，如果是 root 运行则显示 `#`

### 13.3.4 别名 (Aliases)

现代用户环境的痛点之一是别名，这是 shell 的一项功能，在执行命令之前用一个字符串替换另一个字符串。这些可以是高效的快捷方式，节省一些打字时间。然而，别名也有这些缺点：

- 操作参数可能很棘。
- 它们会令人困惑；shell 的内置命令可以告诉你某个东西是否是别名，但它不会告诉你它在哪里定义的。
- 它们在子 shell 和非交互式 shell 中是不受欢迎的；它们在其他 shell 中不起作用。

鉴于这些缺点，你可能应该避免使用别名，编写一个 shell 函数或完全全新的 shell 脚本会更容易。现代计算机启动和执行 shell 的速度非常快，别名与完全新命令之间的差异对你来说应该微不足道。

尽管如此，当你想要更改 shell 环境的一部分时，别名确实很有用。你无法通过 shell 脚本更改环境变量，因为脚本是在子 shell 中运行的。（你也可以定义 shell 函数来执行此任务。）

## 13.3.5 权限掩码 (The Permissions Mask)

正如第 2 章所述，shell 内置的 `umask`（权限掩码）机制设置了你的权限。你应该在其中一个启动文件中运行 `umask`，以确保你创建的任何文件都具有你期望的权限。两个合理的选择是：

> `077` 此掩码是最严格的权限掩码，因为它没有给其他用户访问新文件和目录的权限。在多用户系统上通常是合适的，在那种系统中你不希望用户查看你的任何文件。然而，当设置为默认值时，当用户想要共享文件但不知道如何正确设置权限时，有时会导致问题。（没有经验的用户倾向于将文件设置为可写可读模式。）

> `022` 此掩码允许他人访问新文件和目录。这在单用户系统上可能很重要，因为许多以伪用户身份运行的守护进程无法看到用最严格的 `077` umask 创建的文件和目录。

某些应用程序（尤其是邮件程序）会覆盖 `umask`，将其更改 `077`，因为它们认为文件是文件所有者之外的人的事务。

## 13.4 启动文件顺序和示例

现在你已经知道要在启动文件中放入什么了，是时候看一些具体的例子了。惊讶的是，创建启动文件最困难和困惑的部分之一是决定使用多个启动文件中的哪。接下来的章节介绍了两种最流行的 Unix shell：`bash` 和 `tsh`。

## 13.4.1 bash Shell

在 `bash` 中，你可以从 `.bash_profile`、`.profile`、`.bash_login` 和 `.bashrc` 启动文件名中选择。哪一个适用于你的命令路径、手册页路径、提示符、别名和权限掩码？答案是，你应该有一个 `.bashrc` 文件，并配以一个指向 `.bashrc` 的 `.profile` 符号链接，因为有几种 shell 实例类型。

两种 shell 实例类型是交互式是非交互式的，但只有交互式 shell 是值得关注的，因为非交互式 shell（例如运行 shell 脚本的）通常不运行任何启动文件。交互式 shell 是你从终端运行命令的 shell，例如你在书中看到的那些，它们可以被分类为登录（login）或非登录（non-login）。

登录 shell 是你使用如 `/bin/login` 的程序通过终端首次登录系统时获得的 shell。使用 SSH 远程登录也会给你一个登录 shell。基本思想是登录 shell 是初始 shell。你可以通过运行 `echo $` 来判断 shell 是否为登录 shell；如果第一个字符是 `-`，那么该 shell 就是登录 shell。

当 `bash` 作为登录 shell 运行时，它会运行 `/etc/profile`。然后它查找用户的 `.bash_profile`。

### 非登录 shell (Non-Login Shells)

非登录 shell 是在你已经登录并打开新终端窗口时获得的。它仍然是一个交互式 shell，但不是登录 shell。主要区别在于它不会加载 `/etc/profile` 或用户的 `.bash_profile`。相反，它加载 `.profile` 和 `.bashrc`。

这两个不同文件之所以存在是因为在过去，用户将环境（路径、手册路径等）设置在 `.bashrc` 中，而在登录 shell 中永远看不到它。然而，如果你以后要在控制台或远程登录，仍然需要 `.bash_profile`。

### 两个 shell 的后果 (The Consequences of Two Shells)

如今，大多数用户通过图形界面管理器登录（你将在下一章学习更多）。大多数这些以 `.bashrc` 开始。

## 示例 .bashrc (Example .bashrc)

为了满足非登录登录 shell，如何创建一个也可以作为你的 `.bash_profile` 的 `.bashrc`？这里有一个基础（但足够）的示例：

```bash
# 命令路径。
PATH=/usr/local/bin:/bin:/usr/games
PATH=$HOME/bin:$PATH
```

```bash
# PS1 是常规提示符。
# 替换符包括：
# u 用户名 \w 当前目录
# ! 历史编号 \$
PS1='\u\$ '
```

```bash
# EDITOR 和 VISUAL 决定了像 man 这样的程序
# 在被请求编辑文件时调用的编辑器。
EDITOR=vi
VISUAL=vi
```

```bash
# PAGER 是像 man 这样的程序的默认文本查看器
PAGER=less
```

```bash
# 这些是 less 的一些方便选项。
# 不同的样式是 LESS=FRX
# (F)=结束退出，R=显示原始字符，X=不使用全屏)
LESS=
```

```bash
# 你必须导出环境变量。
export PATH EDITOR VISUAL PAGER LESS
```

```bash
# 默认赋予其他用户对大多数新文件的只读权限。
umask 022
```

正如之前描述，你可以通过符号链接将此 `.bashrc` 与 `.bash_profile` 共享，你也可以通过将 `.bash_profile` 创建为单行命令使这种关系更加清晰：

- `$HOME/.bashrc`

## 检查登录和交互式 shell (Checking for Login and Interactive Shells)

有了与 `.bash_profile` 匹配的 `.bashrc`，你通常不需要为登录 shell 运行额外的命令。然而，如果你想定义不同的操作

对于登录和非登录 shell，你可以将以下测试添加到你的 `.bashrc` 中，该测试会检查 shell 的 `$-` 变量是否包含字符 `i`：

```bash
case $ -
  *1*) # 交互式命令放在这里
    command
    --snip---
    ;
  *) # 非交互式命令放在这里
    command
    --snip---
    ;
esac
```

## 13.4.2 tcsh Shell

几乎在所有 Linux 系统上的标准 `csh` 都是 `tcsh`，它是 `Csh` 的增强版，它让命令行编辑以及多模式文件名和命令补全等功能变得流行起来。即使你没有将 `tcsh` 作为默认用户 shell（我们建议使用 `bash`），如果你的用户恰好遇到了 `tcsh`，你也应该提供 `tcsh` 的启动文件。

你不需要担心 `tcsh` 中登录 shell 和非登录 shell 之间的区别。启动时，`tcsh` 会查找 `.tcsh` 文件。如果找不到，它会去查找 shell 的 `.csh` 文件而不是 `.cshrc`；这种顺序的原因是，你可以使用 `.tcsh` 文件来实现 `csh` 中无法使用的 `csh` 扩展。你应该坚持使用传统的 `.cshrc` 而不是 `.tcshrc`；极不太可能有人会在 `csh` 中使用你的启动文件。如果用户确实在某些其他系统上遇到了 `csh`，你的 `.cshrc` 也可以工作。

### 示例 .cshrc

这是一个示例 `.cshrc` 文件：

```bash
# 命令路径。
setenv PATH /usr/local/bin:/usr/bin:/bin:$HOME/bin
```

```bash
# EDITOR 和 VISUAL 决定了程序（如 less
# 和邮件客户端）在编辑文件时调用的编辑器。
setenv EDITOR vi
setenv VISUAL vi
```

```bash
# PAGER 是 man 等程序的默认文本文件查看器。
setenv PAGER less
```

```bash
# 这些是 less 的一些方便选项。
setenv LESS meIX
```
