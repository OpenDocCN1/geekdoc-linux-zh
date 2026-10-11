
执行此文件后，`zsh` shell 会查找每个用户 `$HOME` 目录下的两个文件：

- `$HOME`/.zlogin
- `$HOME`/.zprofile

这些文件可以包含用户特定的环境变量设置，以及单个用户在登录到系统时希望运行的可执行命令，以便在命令行接口提示符出现之前执行。

你在 `$HOME`/.zprofile shell 中设置的环境变量将覆盖 `/etc/zprofile` 文件中设置的 system-wide 设置，同样适用于 `.zlogin` 文件。你可以通过在每个文件中添加一个简单的 `echo` 语句然后登录，来测试 `zsh` shell 执行这些文件的顺序：

```
$ zsh -l
This is the /etc/zshenv file.
This is the .zshenv file in HOME.
This is the /etc/zprofile file.
This is the .zprofile file in HOME.
This is the /etc/zlogin file.
This is the .zlogin file in HOME.
$ 
```

如示例所示，`zsh` shell 首先执行 `zshenv` 文件，然后执行 `zprofile` 文件，最后执行 `zlogin` 文件。

### 交互式 shell 文件

如果你启动一个交互式 `zsh` shell 会话，还有另一组文件可以容纳启动变量和命令：

- `/etc/zshrc`
- `$HOME`/.zshrc

`zsh` 外壳在启动交互式外壳时，会在启动文件之后立即执行这些文件：

```
% zsh
这是 /etc/zshenv 文件。
这是位于 HOME 目录中的 .zshenv 文件。
这是 /etc/zshrc 文件。
这是位于 HOME 目录中的 .zshrc 文件。
%
```

由于登录外壳也是一种交互式外壳，因此 `zsh` 外壳也会执行 `zshrc` 文件的内容：

```
% zsh -l
这是 /etc/zshenv 文件。
这是位于 HOME 目录中的 .zshenv 文件。
这是 /etc/zprofile 文件。
这是位于 HOME 目录中的 .zprofile 文件。
这是 /etc/zshrc 文件。
这是位于 HOME 目录中的 .zshrc 文件。
这是 /etc/zlogin 文件。
这是位于 HOME 目录中的 .zlogin 文件。
%
```

请注意 `zsh` 外壳执行这些文件的顺序。`zshrc` 文件对会在 `zprofile` 文件之后、`zlogin` 文件之前执行。

### 外壳注销文件

除了登录和启动文件外，`zsh` 外壳还能够在您从交互式或登录外壳会话注销时执行文件中的命令。这些文件可以位于以下位置：

- `/etc/zlogout`
- `$HOME`/.zlogout

如您可能已经意识到的，系统中的每个用户注销时都会执行 `/etc/zlogout` 文件中的命令，而每个特定用户都有唯一的 `$HOME`/.zlogout 文件。

`zsh` 外壳会在从当前外壳注销之前执行这些文件中的任意命令。这不仅包括退出交互式外壳。因此，如果您只是从现有外壳会话启动另一个 `zsh` 外壳，当退出该外壳时，`zsh` 外壳不会执行注销文件。但是，如果您启动一个登录外壳，注销文件应在退出时执行：

```
% zsh -l
这是 /etc/zshenv 文件。
这是位于 HOME 目录中的 .zshenv 文件。
这是 /etc/zprofile 文件。
这是位于 HOME 目录中的 .zprofile 文件。
这是 /etc/zshrc 文件。
这是位于 HOME 目录中的 .zshrc 文件。
这是 /etc/zlogin 文件。
这是位于 HOME 目录中的 .zlogin 文件。
$ exit
这是位于 HOME 目录中的 .zlogout 文件。
这是 /etc/zlogout 文件。
$
```

请注意，外壳先执行 `.zlogout` 文件，再执行全局 `zlogout` 文件，这与其它 `zsh` 文件类型的顺序相反。

### 第四部分：使用替代外壳

#### 环境变量

就像其他任何外壳一样，`zsh` 提供了标准的环境变量来跟踪系统和外壳信息。`zsh` 使用小写变量名和大写变量名的组合。

有几个环境变量，`zsh` 外壳为其提供了小写和大写两个版本。原因与 `zsh` 处理数组的方式以及与其他外壳的兼容性有关。

`zsh` 外壳使用空格分隔的单词列表来定义数组。许多由 Bourne 外壳派生的外壳使用冒号来分隔多值变量（如 Bash 外壳中的 `PATH` 变量）中的数组元素。

为了保持兼容性，`zsh` 外壳提供使用 `zsh` 风格数组的小写 `path` 变量，以及使用 Bourne 风格数组的大写 `PATH` 变量。表 23.2 列出了 `zsh` 外壳中存在的环境变量。

**表 23.2 zsh 环境变量**

| 变量 | 描述 |
| :--- | :--- |
| `!` | 最后一个后台命令的进程 ID。 |
| `#` | 命令行上指定的参数数量。 |
| `$` | 外壳的进程 ID。 |
| `*` | 包含命令行位置参数的数组。 |
| `-` | 命令行上设置的选项。 |
| `argv` | 包含命令行位置参数的数组。 |
| `ARGV0` | 外部命令的 argv[0] 值，通常是命令名称。 |
| `BAUD` | 当前连接的波特率。 |
| `cdpath` | 用于 `cd` 命令搜索路径的目录数组。 |
| `CDPATH` | 与 `cdpath` 相同，但使用冒号作为字段分隔符。 |
| `COLUMNS` | 终端会话中的列数。 |
| `CPUTYPE` | 系统的微处理器类别或型号。 |
| `DIRSTACKSIZE` | 目录堆栈的最大大小。 |
| `EGID` | 外壳进程的有效组 ID。 |
| `ENV` | 如果外壳作为 Bourne 或 Korn 外壳调用，此变量包含 `zprofile` 文件的位置。 |
| `ERRNO` | 最近一次失败系统调用的错误状态。 |
| `EUID` | 外壳进程的有效用户 ID。 |
| `FCEDIT` | 在命令历史编辑器中使用的默认编辑器。 |
| `fignore` | 在文件补全时忽略的文件后缀数组。 |
| `FIGNORE` | 与 `fignore` 相同，但使用冒号作为字段分隔符。 |
| `fpath` | 指定函数搜索路径的目录数组。 |
| `FPATH` | 与 `fpath` 相同，但使用冒号作为字段分隔符。 |
| `GID` | 外壳进程的实际组 ID。 |
| `histchars` | 历史命令使用的字符。 |
| `HISTCMD` | 当前历史行号。 |
| `HISTFILE` | 退出交互式外壳时保存历史的文件。 |
| `HISTSIZE` | 历史文件中允许的最大事件数。 |
| `HOME` | 用户的默认工作目录。 |
| `HOST` | 当前主机名。 |
| `IFS` | 内部字段分隔符，默认值为空格、制表符、换行符和 `NUL` 字符。 |
| `KEYTIMEOUT` | 在读取多字符序列时，外壳等待按下另一个键的时间（以百分之一秒为单位）。 |
| `LANG` | 任何未被 LC 变量覆盖的类别的语言环境类别。 |
| `LC_ALL` | 覆盖所有其他已定义语言环境类别的语言环境类别。 |
| `LC_COLLATE` | 用于确定字符冲突的语言环境类别。 |
| `LC_CTYPE` | 用于确定字符处理函数的语言环境类别。 |
| `LC_MESSAGES` | 用于显示消息的语言环境类别。 |
| `LC_NUMERIC` | 用于显示小数点和千位分隔符字符的语言环境类别。 |
| `LC_TIME` | 用于显示日期和时间的语言环境类别。 |
| `LINES` | 终端会话中的行数。 |
| `LINENO` | 脚本或外壳函数中当前命令的行号。 |
| `LISTMAX` | 在行编辑器中请求更多匹配项之前列出的匹配项数量。 |
| `LOGCHECK` | 使用 watch 参数检查不活动状态的间隔（以秒为单位）。 |
| `LOGNAME` | 与当前外壳会话对应的登录名称。 |
| `MAIL` | 如果设置，外壳会检查指定文件中的邮件。 |
| `MAILCHECK` | 邮件检查之间的间隔（以秒为单位）。 |
| `mailpath` | 用于检查邮件的文件名数组。 |
| `MAILPATH` | 与 `mailpath` 相同，但使用冒号作为字段分隔符。 |
| `manpath` | `zsh` 外壳未使用的目录数组（与 Bourne 外壳中使用的 `MANPATH` 相关）。 |
| `MANPATH` | 与 `manpath` 相同，但使用冒号作为字段分隔符。 |
| `module_path` | `zmodload` 用于加载新 `zsh` 模块的目录数组。 |
| `MODULE_PATH` | 与 `module_path` 相同，但使用冒号作为字段分隔符。 |
