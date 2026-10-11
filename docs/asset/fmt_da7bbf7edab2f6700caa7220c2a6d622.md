
在本节中，你将创建一个 `.profile` 文件（或编辑现有文件），以便每次登录时在屏幕上显示一条消息。你将使用 `echo` 命令来完成此操作。

1. 尝试登录消息。输入

```
$ echo "Your wish is my command, Oh Great One." (Return)
```

shell 应响应相应的消息：

```
Your wish is my command, Oh Great One.
```

2. 使用你的文本编辑器打开 `.profile` 文件。

```
$ vi .profile (Return)
```

3. 插入一条显示修改日期的注释。将以下行放在 `.profile` 的顶部：

```
# This file was last modified on [today's date].
```

行首的 `#` 使这成为一条注释。这展示了注释的典型用法，即告知你文件最后编辑的时间。

4. 将消息命令添加到文件中。

```
echo "Your wish is my command, Oh Great One."
```

5. **写入文件并退出编辑器。**

### 21.6 运行启动文件

此时，你*可以*注销并重新登录，以检查你的 `.profile` 是否有效。然而，有一种更简单的方法：使用“点”命令。

- **运行“点”命令。** 输入一个点号、一个空格和文件名：

```
$ . profile (Return)
```

这将导致 shell 执行 `.profile` 中的命令，仿佛你刚刚登录了一样。你应该能看到登录消息：

```
Your wish is my command, Oh Great One.
```

每次登录时，shell 都会显示此消息，除非你从 `.profile` 中更改或删除它。

### 21.7 更改提示符符号

`sh` 或 `ksh` 的默认主要提示符符号是美元符号 (`$`)。你可以通过更改变量 `PS1` 的值来更改提示符符号。在本节中，你将尝试各种提示符，然后编辑 `.profile` 以显示其中一个新提示符。

1. **更改 PS1 变量的值。** 输入以下行，确保等号周围没有空格：

```
$ PS1=# (Return)
```

这将把你的 shell 提示符更改为英镑符号（井号）：

```
#
```

2. **尝试另一个提示符。** 如果你给提示字符串加引号，可以在其中包含空格和特殊字符：

```
# PS1="Your Majesty? " (Return)
```

提示符将变为新的字符串：

```
Your Majesty?
```

3. **在提示符中包含 shell 变量。** 一些用户喜欢将主目录的路径名显示为提示符的一部分。请记住，你的主目录路径名由 shell 存储在名为 `HOME` 的变量中。尝试以下命令（不要输入 `Your Majesty?`——它是提示符）：

```
Your Majesty? PS1="$HOME > " (Return)
```

放在 `$HOME` 前面的美元符号告诉 shell 将 `$HOME` 的内容放入提示符中。现在你的提示符应显示主目录的绝对路径名，后面跟着一个箭头（`>`）。例如，如果你的主目录的绝对路径名是 `/home/you`，那么提示符现在将是

```
/home/you >
```

让我们把这个提示符放入你的 `.profile` 中。

4. 使用文本编辑器编辑启动文件。将以下内容添加到 `.profile`：

```
PS1="$HOME > "
export PS1
```

5. 写入文件并退出编辑器。

6. 使用“点”命令运行 `.profile` 中的命令。

```
/home/you > . .profile (Return)
```

你的提示符现在应由主目录的路径名组成，后面跟着一个箭头。因此，如果你的主目录是 `/home/you`，你将看到登录消息，然后是提示符

```
/home/you >
```

### 21.8 设置终端类型

每次登录时都要设置终端是个麻烦事——尤其是如果你一直使用同一种类型的终端。你可以在 `.profile` 文件中设置终端。

1. **编辑你的 `.profile` 以设置终端类型。** 插入以下行，用你终端的 *termcap* 代码替换 `vt100`：

```
TERM=vt100
export TERM
echo "Terminal set to $TERM"
```

2. 写入并退出编辑器。

3. 对 `.profile` 应用“点”命令：

```
/home/you > . .profile (Return)
```

你的登录消息应该会先出现，然后是关于终端类型的消息：

```
Terminal set to vt100
```

### 21.9 创建日历文件

`calendar` 实用程序会提醒你即将到来的事件。这要求你的主目录中有一个 `calendar` 文件，并且你需要修改 `.profile` 以读取 `calendar` 文件。

1. **使用文本编辑器编辑你的 `.profile`。** 添加以下行：

```
calendar
```

2. **将更改写入文件并退出编辑器。**

3. **使用文本编辑器创建一个 `calendar` 文件。** 请务必使用小写字母拼写的 `calendar`。否则，shell 无法识别该文件。

4. **向 `calendar` 文件添加一条消息。** 在消息中包含今天的日期：

```
This is a test for [today’s date]
```

5. **将更改写入 `calendar` 文件并退出编辑器。**

6. **使用“点”命令运行 `.profile` 文件。**

```
/home/you > . .profile (Return)
```

你应该看到登录消息、关于终端类型的消息，以及 `calendar` 消息：

```
Your wish is my command, Oh Great One.
Terminal set to vt100
This is a test for [today’s date]
```

*以 Apr 12、Apr 12 或 4/12 的格式书写日期。*

### 21.10 创建 .kshrc 文件（仅限 ksh）

如果你是 `ksh` 用户，你可以创建一个名为 `.kshrc` 的 shell 初始化文件。此文件通常用于设置命令别名和 `history` 机制。然而，在做此操作之前，你需要编辑 `.profile`：

1. **使用文本编辑器编辑 `.profile`。** 将以下行添加到文件中：

```
ENV=$HOME/.kshrc
export ENV
```

这告诉 `ksh` 它应在你的主目录中查找 `.kshrc`。如果未设置 `ENV` 变量，`ksh` 将不会执行 `.kshrc`。

2. **写入并退出编辑器。**

3. **使用文本编辑器编辑 `.kshrc` 文件。** 首先插入一条注释行，注明今天的日期：

### 21.11 创建别名（ksh）

`.kshrc` 的一个用途是创建别名。在本节中，您将为 **history** 命令创建一个单字母别名。

- 1. **使用文本编辑器编辑 `.kshrc` 文件。** 向该文件中添加以下行以创建 **history** 命令的别名：

    ```
    alias -x h=history
    ```

    `-x` 选项告知 `alias` 将该别名导出到所有子 shell。

- 2. **将更改写入文件并退出编辑器。**

- 3. **使用“点”命令运行 `.kshrc` 文件。**

    ```
    /home/you > .kshrc {Return}
    ```

此时，别名应该已经设置好。在下一节中，您将看到如何使用该别名来运行 **history** 命令。

### 21.12 使用 history 机制（ksh）

**history** 机制会保留您最近使用的命令列表，并允许您查看和重复列表中的命令。

- 1. **使用其别名运行 history 命令。** 输入 `h` 后跟 `{Return}` 来运行 **history** 命令：

    ```
    /home/you > h {Return}
    ```

如果您正确设置了 **history** 的别名，您应该看到一个最近执行命令的编号列表。请注意，**history** 命令本身将作为列表中的最后一项出现：
