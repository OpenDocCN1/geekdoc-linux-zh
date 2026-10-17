
### `HOSTYPE` 环境变量

设置一个描述机器类型的字符串。默认值取决于系统。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `IFS` 环境变量

用于单词拆分的字段分隔符。默认值为`<空格><制表符><换行>`。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `IGNOREEOF` 环境变量

控制接收 EOF 字符时的操作。如果设置，该值为 shell 在退出前接受的连续 EOF 字符数。不存在则禁用此功能。这仅在交互式 shell 中生效。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `INPATH` 环境变量

启动脚本的文件名，覆盖默认的 `~/.input`（参见 `READLINE`）。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `LINENO` 环境变量

在脚本或函数中，每次引用此参数时，shell 都会替换为当前顺序行的数字（从 1 开始）。在非脚本或函数中，替换的值不保证有意义。在函数中，该值为命令所在的源行号（执行函数时该信息已丢失），它是执行简单命令数量的近似值。如果 `LINENO` 未设置，它将失去其特殊属性，即使随后重置也是如此。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `MAIL` 环境变量

如果此参数设置为文件名且未设置 `MAILPATH` 变量，bash 会通知用户指定文件中有新邮件。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `MAILCHECK` 环境变量

指定检查邮件的间隔秒。默认值为 60 秒。当需要检查邮件时，shell 会在提示之前执行。如果此变量未设置，shell 将禁用邮件检查。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `MAILPATH` 环境变量

要检查邮件的路径列表，用冒号分隔。打印的消息可以通过 `?` 分隔路径名和消息来实现。`$` 代表示例名称：`MAILPATH=/usr/spool/mailbox/"You have mail~/shell-mail!"`。Bash 为此变量提供了默认值，使用的用户邮件位置取决于系统（例如 `/usr/spool/mail/SUUSER`）。源自《用户指南》

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### `$MAIL_WARNING`

标点

如果已设置，且检查邮件的文件自上次检查以来已被访问过，则会打印消息 `The mail in mailfile has been read`。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$OLDPWD`

上一个工作目录由 `cd` 命令设置。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$OOSTYPE`

自动被设置为一个描述执行 bash 运行操作系统的字符串。默认值取决于系统。来自 [Route–Users–Guide](http://www.tld.org/LDP/linux-Dictionary/html/index.html)

### `$PATH`

命令的搜索路径。它是一组由冒号分隔的目录列表，shell 在这些目录中查找命令（见下文“命令执行”）。该路径取决于系统，并由安装 bash 的管理员设置。一个常见值为来自 [Route–Users–Guide]

```
/usr/bin:/usr/local/bin:/usr/sbin:/usr/bin:
```

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

### `$PATH`

shell 在 `PATH` 变量中的文件路径列表中查找命令和程序。环境变量将信息存储在其他程序和命令可以访问的地方。环境变量存储此类信息，如你正在使用的 shell、你的登录名和工作目录。在提示符处 `set` 可以更改工作目录。当你在提示符处输入命令时，shell 将查找所有定义的环境变量；在 `PATH` 变量中的每个目录中设置该命令的程序文件，或者运行第一个找到该命令的程序。如果在 `PATH` 环境变量的目录中没有找到命令，shell 将返回 `commands not found`。默认情况下，shell 不会在你的工作目录或主目录中查找命令。这是一种安全机制，防止你意外执行程序。如果一个恶意用户在你的主目录中放置了有害命令怎么办？如果你输入了命令，而 shell 在读取 `/bin` 目录之前先在你的主目录中查找伪造程序，你认为会发生什么？如果你是这样想的，你的思路是正确的。由于你的 `PATH` 没有将当前目录作为搜索位置之一，目录中的程序必须使用绝对路径或相对路径调用，例如 `/prompt-name`。要查看哪些目录属于你的 `PATH`，使用此命令：

```
# echo PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/bin2
```

来自 [Complete-Idot's Guide to Linux]

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

### `$PROMPT_COMMAND`

如果已设置，在每次发出提示符时，该值将作为命令执行。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$PS1`

此变量的值会被展开（见下文“提示符”）并用作主提示符字符串。默认值为 `\$#` 来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$PS2`

此变量的值会被展开并用作次提示符。默认值为 `>>`。

来自 [Route–Users–Guide] `http://www.tld.org/LDP/Linux–Dictionary/html/index.html`

### `$PS3`

此变量的值用作 `select` 命令的提示符（见上文“shell 语法”）。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$PS4`

此变量的值会在执行期间期间每个命令显示之前被展开并打印。`PS4` 的第一个字符会根据需要重复多次，以指示多级间接。默认值为 `^+`。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$PWD`

由 `cd` 命令设置的当前工作目录。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$RANDOM`

每当引用此参数时，都会生成一个随机整数。随机数序列可以通过给 `RANDOM` 赋值来初始化。如果 `RANDOM` 未被设置，它将失去其特殊属性，即使随后被重置也是如此。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$SECONDS`

每当引用此参数时，都会返回自 shell 启动以来的秒数。后续引用的返回值为自赋值以来的秒数加上赋值的值。如果 `SECONDS` 未被设置，它将失去其特殊属性，即使随后被重置也是如此。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `$SHLVL`

每当启动一个 bash 实例时加 1。来自 [Route–Users–Guide](http://www.tld.org/LDP/Linux-Dictionary/html/index.html)

### `#01`

另一种用于已扫描演示的电影胶卷中挑选文件的方法来自 [Whatis–Extensions]

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

### `$$$`

OS/2 用于跟踪归档文件来自 [Whatis–Extensions]
