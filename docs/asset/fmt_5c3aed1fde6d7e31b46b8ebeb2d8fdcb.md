
`then`                            # `then`

    `cp acme /tmp/archive`          # 命令(s)

    `rm /tmp/acme`                   #

`fi`

```
if 语句的完整通用语法如左侧，右侧为示例：

```bash

if [ "$CNT" -eq 25 ]      # if 条件 1

then                            # then

    cp acme /tmp/archive          # 命令(s)

    rm /tmp/acme                   #

elif [ "$CNT" -gt 25 ]         # elif 条件 2

then                            # then

    cp acme2                        # 命令(s)

elif [ "$CNT" -gt 0 ]          # elif 条件 3

then                            # then

    cp acme0 /tmp/archive          # 命令(s)

    cp acme0 /tmp/acme              #

    rm /tmp/acme1                   #

else                           # else

    rm -f /tmp/acme                # 命令(s)

    rm -f /tmp/acme1               #

fi                              # fi

```
以下是工作原理：在所有情况下，条件都是你执行的任何命令。如果命令的退出状态为 `0` (`0`)（意味着执行成功），则将执行紧随条件之后的命令，直到遇到下一个 `else`、`elif` 或 `fi`。如果命令的退出状态为非零（意味着命令以某种方式失败），则将跳过条件后的命令，直到遇到下一个 `else`、`elif` 或 `fi`。

`else` 语句（如果存在）代表 "else if"，允许你在进入 `else` 语句或退出 `if` 语句之前测试另一个条件。语句的这部分不是必须的，提供以便在你需要使用。

`else` 语句（如果存在）仅在之前的 `if` 条件不成立时执行。语句的这部分也不是必须的：

```bash

if cp acme /usr/fred

then

    rm acme

fi

```

# 第六部分 编程
## 第 28 章 编写 Bourne Shell 脚本

在上一个示例中，条件是执行 `cp` 命令。如果复制成功，将执行该词之后的代码，并删除 `acme` 文件。如果 `cp` 失败，则不会发生这种情况：

```bash

if cp acme /usr/fred

then

    rm acme

else

    echo "Error: could not copy acme to /usr/fred" >&2

fi

```

上一个示例说明了 `then` 与 `else` 的二选性。如果 `cp` 成功，你将删除文件 `acme`。如果不成功，你将输出错误信息。

如果你不想浪费一行代码，可以选择将其放在与单独的一行在同一行，可以使用 `if` 或 `elif` 关键字，只要你使用分号将其与条件隔开：

```bash

if condition; then

elif condition; then

```

你会发现条件可以是任何命令，但它通常是测试命令（`test`）。`test` 命令是一个真实的 UNIX 命令，带有许多选项，你可以在输入以下内容时了解它们：

```bash

man test

```

以下是你如何使用 `test` 命令来检查变量 `SCNT` 是否包含值 `25`：

```bash

if test "SCNT" -eq 25    # test 的旧形式（很少使用）

t...

fi

```

在今天的许多 shell 脚本中，`test` 词被左括号 `[` 和右括号 `]` 替换：

```bash

if [ "SCNT" -eq 25 ]    # test 命令通常出现的形式

t...

fi

```

`test` 命令的格式需要空格。不正确的间距会导致条件求值错误，但它不会产生错误：

# 根据测试结果执行代码 第 28 章

```bash

if [ "$CNT" -eq 25 ] # 正确的间距

if[ "$CNT" -eq 25 ] # 错误的间距

if [ "$CNT" -eq 25 ] # 错误的间距

if [ "$CNT" -eq 25 ] # 错误的间距

if [ "$CNT" -eq 25 ] # 错误的间距

```

## 注意间距
`if` 条件中错误的间距是一个很容易的错误，因为它不会产生明显的错误，除了程序给出的结果错误。记住这个简单的规则：括号字符 `[]` 永远不要直接接触任何其他非空格字符。

接下来的章节提供了在 `if` 语句中使用 `test` 命令的更多示例。

## 检查文件类型、大小或权限

`test` 命令的功能之一是可以检查任何文件系统对象（文件或目录）的若干属性，并根据它们在脚本中做出决策。表 28.1 不是 `test` 用于文件系统对象的选项完整列表，但它涵盖了最常用的选项。

表 28.1 用于文件系统对象的测试选项

| 选项 | 说明 |
| :--- | :--- |
| - d file | 文件是目录吗？ |
| - f file | 文件是普通（正常）文件吗？ |
| - r file | 运行此脚本的用户可以读取该文件吗？ |
| - w file | 运行此脚本的用户可以写入该文件吗？ |
| - x file | 运行此脚本的用户可以执行该文件吗？ |
| - s file | 文件长度大于零吗？ |

### 使用 test 命令
`test` 命令允许的功能之一是检查任何文件系统对象（文件或目录）的若干属性，并根据它们在脚本中做出决策。表 28.1 不是 `test` 用于文件系统对象的选项完整列表，但它涵盖了最常用的选项。

### 使用 test 命令
1. 在这里创建一个文件并对它进行若干测试。首先，让一个文件并设置权限：
`touch /tmp/testfile`
`chmod 775 /tmp/testfile`

2. 现在使用 `if` 语句编写脚本：

```bash

MYFILE="/tmp/testfile"

if [ -d $MYFILE ]

then

    echo "My file is a directory!"

    fi

if [ -f $MYFILE ]

then

    echo "My file is a regular (normal) file!"

    if [ -w $MYFILE ]

    then

        echo "This file is writable!"

    else

        echo "This file is not writable"

    fi

    if [ -r $MYFILE ]

    then

        echo "This file is readable!"

    else

        echo "This file is not readable"

    fi

```

注意你可以将一个 `if` 语句放在另一个 `if` 语句中。对于当前的文件权限，此脚本应该输出以下内容：

```
% ./test2

My file is a regular (normal) file!

This file is writable!

This file is readable!

```

3. 现在稍微修改文件的权限，关闭对它的写入能力以便测试脚本：
`chmod -w /tmp/testfile`

4. 现在再次运行脚本：

```
% ./test2

My file is a regular (normal) file!

This file is not writable

This file is readable!
```
