
如果你在登录期间向 `PATH` 添加目录，该目录将仅在你的登录会话期间有效。当你重新登录时，初始化文件 `.bash_profile` 将再次用其原始目录集初始化你的 `PATH`。`.bash_profile` 文件将在本章稍后部分详细介绍。要永久地向你的 `PATH` 添加新目录，你必须编辑 `.bash_profile` 文件并找到 `PATH` 变量的赋值。然后，你只需在其前面加上冒号并插入到赋值给 `PATH` 的路径集中即可。

### 指定 Bash 环境：BASH ENV

`BASH ENV` 变量存储了每当生成 BASH shell 时要执行的 bash shell 初始化文件的名称。例如，当执行 BASH shell 脚本时，在执行脚本之前之前会检查 `BASH ENV` 变量及其所持有的脚本名称。`BASH ENV` 通常持有 `HOME/.bashrc`。`.bashrc` 文件将在本章稍后讨论。如果你愿意，可以使用其他文件代替 `.bashrc` 供 BASH shell 脚本。

### 配置 Shell 提示符

`PS1` 和 `PS2` 变量分别包含主、次提示符符号。BASH shell 的主提示符符号是美元符号 `$`。你可以通过给 `PS1` 变量分配一组新字符来更改提示符符号。在下一个示例中，shell 提示符被改为 `->` 符号：

```
$ PS1='->'

->> export PS1
```

你可以将提示符更改为任何字符，包括字符串，如下：

```
$ PS1="Please enter a command: "

Please enter a command: export PS1

Please enter a command: ls

mydata /reports

Please enter a command:
```

`PS2` 变量持有次提示符符号，用于需要几行才能完成的命令。默认的次提示符是 `>`。添加的命令行行以次提示符而非主提示符开头。你可以像更改主提示符一样轻松更改次提示符，所示：

```
$ PS2="@"
```

## 第 9 章：Shell 配置 173

与 TCSH shell 一样，BASH shell 提供了一组预定义的代码，你可以使用它们来配置提示符。通过这些代码，你可以将时间、用户名或目录路径成为提示符的一部分。你甚至可以让提示符显示你即将输入的当前命令的历史事件编号。每个代码都以反斜杠开头。`\w` 表示工作目录，`\t` 表示时间，`\u` 表示你的用户名。`!` 将显示下一个历史事件编号。在下一个示例中，用户将当前工作目录添加到提示符中：

```
$ PS1=\w \$ $

/home/dylan $
```

这些代码必须包含在引号字符串中。如果没有引号，代码字符将不会被求值，而是本身将作为提示符使用。`PS1=\w` 将提示符设置为字符 `\w`，而不是工作目录。接下来的示例将时间和历史事件编号结合到一个新的提示符中：

```
$ PS1=\t -> $
```

下表列出了配置提示符的代码：

| 提示符代码 | 描述 |
| :--- | :--- |
| ! | 当前历史编号 |
| \$ | 除 root 用户外，所有用户使用 $ 作为提示符，root 用户使用 # 作为提示符 |
| \d | 当前日期 |
| \s | 当前活跃的 shell |
| \t | 当天时间 |
| \u | 用户名 |
| \w | 当前工作目录 |

### 配置你的新闻服务器

一些 shell 系统变量用于设置网络应用程序（如 Web 浏览器）的值。`NNTPSERVER` 用于设置网络上可访问的远程服务器。如果你正在使用 ISP，ISP 通常会提供一个你可以通过新闻阅读器应用程序访问的新闻服务器。然而，这是 `NNTPSERVER` 的作用。互联网上的新闻服务器使用 NNTP 协议。`NNTPSERVER` 应该持有此类服务器的地址。对于许多 ISP，新闻服务器地址是以 `nntp` 开头的域名。接下来的示例将新闻服务器地址 `nntp.myservice.com` 分配给 `NNTPSERVER` 系统变量。新闻阅读器会自动从 `NNTPSERVER` 获取新闻服务器地址。由于此赋值放置在 shell 初始化文件 `.bash_profile` 中，因此每个用户登录时都会自动设置。

```
NNTPSERVER=nntp.myservice.com

export NNTPSERVER
```

### 配置你的登录 Shell：.bash_profile

`.bash_profile` 文件是 bash 的登录初始化文件，也可以命名为 `.profile`（如 Solaris Linux 中）。它是一个脚本文件，每当用户登录时都会自动执行。它包含了用于管理你的 shell 的环境变量的 shell 命令。它们可以是系统定义变量的重新定义，也可以是自定义变量的定义。例如，当你登录时，你的用户 shell 需要知道哪些目录包含 home 命令令。它将引用 `PATH` 变量来查找这些目录的路径。然而，首先必须为 `PATH` 变量分配这些路径。在 `.bash_profile` 文件中，赋值操作正是如此。由于它在 `.bash_profile` 文件中，此赋值被放置在 shell 初始化文件中，每次用户登录时都会自动设置。

### 导出变量

`BASH ENV` 变量持有了每当生成 BASH shell 时要执行的 bash shell 初始化文件的名称。例如，当执行 BASH shell 脚本时，在执行脚本之前会检查 `BASH ENV` 变量及其所持有的脚本名称。`BASH ENV` 通常持有 `HOME/.bashrc`。`.bashrc` 文件将在本章稍后讨论。如果你愿意，可以使用其他文件代替 `.bashrc` 供 BASH shell 脚本。

`.bash_profile` 文件是 bash 的登录初始化文件，也可以命名为 `.profile`（如 Solaris Linux）。它是一个脚本文件，每当用户登录时都会自动执行。它包含了用于管理你的 shell 的环境变量的 shell 命令。它们可以是系统定义变量的重新定义，也可以是自定义变量的定义。例如，当你登录时，你的用户 shell 需要知道哪些目录包含 home 命令。它将引用 `PATH` 变量来查找这些目录的路径。然而，首先必须为 `PATH` 变量分配这些路径。在 `.bash_profile` 文件中，赋值操作正是如此。由于它在 `.bash_profile` 文件中，此赋值被放置在 shell 初始化文件中，每次用户登录时都会自动设置。

*(注：原文后续存在大量重复段落，此处已按要求处理核心逻辑并完成翻译)*

## 176 第二部分：环境

或者，你可以使用 `source` 命令来执行 `.bash_profile` 初始化文件，或者 TCSH shell 中使用的任何初始化文件如 `.login`，或 `.bashrc`。

```bash
$ source .bash_profile
```

### 系统 Shell Profile 脚本

你的 Linux 系统也有自己的 profile 文件，每当用户登录时系统都会执行它。这种系统初始化简称为 profile，位于 `/etc` 目录下，即 `/etc/profile`。该文件包含了系统为每个用户提供所需的系统变量定义。下面是系统 .profile 的副本。Red Hat 有一个路径函数，用于为 `PATH` 变量生成目录列表。为 root 用户生成的路径看起来像这样，包含了系统目录和用户应用程序目录。普通用户的路径会锁定系统目录（即路径中的 `/sbin`）以及 Kerberos 工具的名称和 `/usr/kerberos/bin`（它们不在路径中）。

```bash
$ echo PATH
/local/sbin:/sbin:/usr/bin:/bin:/usr/bin/bin/X11:

/usr/X11R6/bin:/usr/local/bin:/usr/bin:/root/bin
```

`HISTFILE` 也被重新定义，以包含更多的历史事件。通常情况下，新闻服务器地址是一个需要为所有用户设置的值。此类赋值应该由系统管理员在系统的 `/etc/profile` 文件中进行，而不是在单个用户的 `.bash_profile` 文件中。`/etc/profile` 文件还会执行 `/etc/profile.d` 目录下的任何脚本。这种设计允许了更具模块化的结构。你不需要通过编辑 `/etc/profile` 文件来添加条目，只需向 `profile.d` 目录添加脚本即可。BASH shell 的脚本扩展名为为 `.sh`。例如，`profile.d` 目录中的 `kde.sh` 脚本会检查 `KEDIR` 变量的定义，如果没有正在生效的定义，则会设置一个。

```bash
/etc/profile

### /etc/profile

### 全局环境和启动程序，用于登录设置

### 函数和别名放入 /etc/bashrc

pathmunge ()
```
