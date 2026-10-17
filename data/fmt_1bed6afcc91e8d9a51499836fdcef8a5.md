
| `term` | 您的终端的 termcap 代码 |

| `user` | 您的用户名 |

请注意，`csh` 的特殊变量使用小写字母编写，以与环境变量区分开来。

> 这些特殊 shell 变量仅由 `csh` 使用，而不是 `sh` 或 `ksh`。

### 22.3 设置特殊 csh 变量

`set` 命令用于给变量赋值。

- **输入 `set` 命令。** 例如，若要设置 `history` 变量的值，请输入以下内容：

```
% set history = 100 <Return>
```

- **使用 `echo` 检查设置。**

```
% echo $history <Return>
```

这应该会显示存储在 `history` 中的值：

100

特殊 `csh` 变量 `home`、`path`、`shell`、`term` 和 `user` 与其大写对应变量具有特殊关系。当您更改小写变量的值时，大写变量的值也会随之更改。例如，如果您更改 `term` 的值，`TERM` 的值会自动更改以匹配。

### 22.4 备份启动文件

创建或编辑 `.login` 或 `.cshrc` 的第一步是查看您是否已经拥有此类文件。如果有，您应该准备备份副本。

- **如有必要，进入您的主目录。** 请记住，不带参数的 `cd` 命令会将您带到主目录：

```
% cd <Return>
```

- **列出主目录中的所有文件。** 输入 `ls -a`（“list -all”）命令：

```
% ls -a <Return>
```

如果您看到名为 `.login` 和 `.cshrc` 的文件，这些文件很可能是在您的账户创建时放置到主目录中的。在编辑它们之前，您可能需要咨询您的讲师或系统管理员。

- **为现有的启动文件制作备份副本。**

```
% cp .login .login.BAK <Return>
% cp .cshrc .cshrc.BAK <Return>
```

### 22.5 登录消息

在本节中，您将创建一个 `.login` 文件（或编辑现有文件），以便在每次登录时在屏幕上显示消息。您将使用 `echo` 命令来实现这一点。

- **尝试登录消息。** 输入：

```
% echo "Your wish is my command, Oh Great One." <Return>
```

shell 应该会响应相应的消息：

Your wish is my command, Oh Great One.

- **使用文本编辑器打开 `.login` 文件。**

```
% vi .login <Return>
```

- **插入显示修改日期的注释。** 在 `.login` 的顶部放入以下行：

```
# This file was last modified on [today's date].
```

行首的 `#` 使其成为注释。这展示了注释的典型用途，即告知您文件最后编辑的时间。

- **将消息命令添加到文件中。**

```
echo "Your wish is my command, Oh Great One."
```

- **写入文件并退出编辑器。**

### 22.6 运行启动文件

此时，您*可以*注销并重新登录，以查看您的 `.login` 是否有效。然而，有一种更简单的方法：使用 *source* 命令。

- **对文件运行 `source` 命令**。因此，要运行 `.login` 中的命令，请输入：

```
% source .login <Return>
```

这将导致 shell 执行 `.login` 中的命令，就好像您刚刚登录一样。您应该看到登录消息：

Your wish is my command, Oh Great One.

除非您更改或删除 `.login` 中的此消息，否则 shell 将在每次您登录时显示此消息。

### 22.7 更改提示符符号

`csh` 的默认主提示符符号是百分号（`%`）。您可以通过更改变量 `prompt` 的值来更改提示符符号。在本节中，您将尝试各种提示符，然后编辑 `.login` 以显示其中一种新提示符。

- **更改 `prompt` 变量的值。** 输入以下行：

```
% set prompt = # <Return>
```

这将把您的 shell 提示符更改为磅号：

```
#
```

- **尝试另一种提示符。** 如果对提示字符串加引号，您可以在其中包含空格和特殊字符：

```
# set prompt = 'Your Majesty?' <Return>
```

提示符将更改为新的字符串：

```
Your Majesty?
```

- **在提示符中包含 shell 变量。** 一些用户喜欢将主目录的路径名作为提示符的一部分显示。请记住，主目录的路径名由 shell 存储在名为 `home` 的变量中。尝试以下命令（不要输入 Your Majesty?——它是提示符）：

```
Your Majesty? set prompt = "$home > " <Return>
```

`home` 前面的美元符号告诉 shell 将 `home` 的内容放入提示符中。现在，您的提示符应该会显示您主目录的绝对路径名，后面跟着一个箭头（`>`）。例如，如果您的主目录的绝对路径名是 `/home/you`，那么现在的提示符将是

```
/home/you >
```

让我们将此提示符放入您的 `.login` 中。

- **使用文本编辑器编辑启动文件。** 将以下内容添加到 `.login`：

```
set prompt = "$home > "
```

- **写入文件并退出编辑器。**

- **使用 `source` 命令运行 `.login` 中的命令。**

```
/home/you > source .login <Return>
```

您的提示符现在应由主目录的路径名组成，后面跟着一个箭头。因此，如果您的主目录是 `/home/you`，您会看到您的登录消息，然后是提示符

```
/home/you >
```

### 22.8 设置终端类型

每次登录时都需要设置终端很麻烦——尤其是如果您一直使用同一种终端。您可以在 `.login` 文件中设置终端。

- **编辑您的 `.login` 以设置终端类型。** 插入以下行，用您终端的 termcap 代码替换 `vt100`：

```
set term = vt100
echo "Terminal set to $term"
```

- **写入并退出编辑器。**

- **对 `.login` 应用 `source` 命令：**

```
/home/you > source .login <Return>
```

您的登录消息应该会出现，然后是消息：

```
Terminal set to vt100
```

### 22.9 创建日历文件

日历实用程序会提醒您即将到来的事件。这需要您在主目录中有一个日历文件，并且您修改 `.login` 以读取该日历文件。

- **使用文本编辑器编辑您的 `.login`。** 添加以下行：

```
calendar
```

- **将更改写入文件并退出编辑器。**

- **使用文本编辑器创建一个日历文件。** 请务必使用 `calendar` 的确切拼写，且使用小写字母。否则，shell 将无法识别该文件。

- **向日历文件中添加一条消息。** 在消息中包含今天的日期：

```
This is a test for [today’s date]
```

- **将更改写入日历文件并退出编辑器。**

- **使用 `source` 命令运行 `.login` 文件。**

```
/home/you > source .login <Return>
```

您应该看到您的登录消息、关于终端类型的消息以及日历消息：

```
Your wish is my command, Oh Great One.
Terminal set to vt100
This is a test for [today’s date]
```

### 22.10 创建 .cshrc 文件

如果您是使用 `csh` 的用户，您可以创建一个名为 `.cshrc` 的 shell 初始化文件。该文件通常用于设置命令别名和历史机制。在本节中，您将创建一个用于 `history` 命令的单字母别名。

- **使用文本编辑器编辑 `.cshrc` 文件。** 首先插入一行注释，给出今天的日期：

```
# This file was last modified on [today's date]
```
