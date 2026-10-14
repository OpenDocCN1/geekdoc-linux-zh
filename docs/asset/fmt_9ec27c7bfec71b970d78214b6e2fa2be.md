
其中 `expression` 是一个被评估为真或假的表达式。当表达式为真时，`test` 命令返回退出状态 0，当表达式为假时返回状态 1。

## 文件表达式

表 27-1 中的表达式被用于评估文件的状态。

### 表 27-1: test 文件表达式

| 表达式 | 如果 . . . 则为真 |
| - | - |
| `file1 -ef file2` | `file1` 和 `file2` 具有相同的 inode 节点（两个文件名通过硬链接引用同一个文件）。 |
| `file1 -nt file2` | `file1` 比 `file2` 新。 |
| `file1 -ot file2` | `file1` 比 `file2` 旧。 |
| `-b file` | 文件存在且是一个块特殊（设备）文件。 |
| `-c file` | 文件存在且是一个字符特殊（设备）文件。 |
| `-d file` | 文件存在且是一个目录。 |
| `-e file` | 文件存在。 |
| `-f file` | 文件存在且是一个普通文件。 |
| `-g file` | 文件存在且归有效组所有。 |
| `-G file` | 文件存在且归有效用户所有。 |
| `-k file` | 文件存在且设置了“粘性位”。 |
| `-L file` | 文件存在且是一个符号链接。 |
| `-p file` | 文件存在且是一个命名管道。 |
| `-r file` | 文件存在且可读（有效用户具有读取权限）。 |
| `-s file` | 文件存在且长度大于零。 |

### 表 27-1（续续）

| 表达式 | 如果 . . . 则为真 |
| - | - |
| `-S file` | 文件存在且是一个网络套接字（socket）。 |
| `-t fd` | `fd` 是指向终端的文件描述符。 |
| `-u file` | 文件存在且设置了 setuid。 |
| `-w file` | 文件存在且可写（有效用户具有写入权限）。 |
| `-x file` | 文件存在且可执行（有效用户具有执行权限）。 |

这里我们有一个演示了一些文件表达式的脚本：

```bash
#!/bin/bash

# test-file: 评估文件的状态

FILE=".bashrc"

if [ -e "$FILE" ]; then

  if [ -f "$FILE" ]; then

    echo "$FILE is a regular file."

  if [ -d "$FILE" ]; then

    echo "$FILE is a directory."

  if [ -r "$FILE" ]; then

    echo "$FILE is readable."

  if [ -w "$FILE" ]; then

    echo "$FILE is writable."

  if [ -x "$FILE" ]; then

    echo "$FILE is executable."

else

  echo "$FILE does not exist"

  exit 1

fi
```

该脚本评估常量 `FILE` 并显示其结果。关于这个脚本有两个有趣的地方：首先，注意表达式中的 `$FILE` 是带引号的。这不是强制要求的，但为了防止参数为空。如果 `$FILE` 的扩展结果为空值，会导致错误（运算符会被解释为空字符串而不是运算符）。对参数加引号确保了即使字符串为空，运算符后面也有内容。其次，注意脚本末尾的 `exit` 命令。`exit` 命令接受一个可选参数，这成为脚本的状态。如果 `FILE` 扩展为不存在的文件名，使用 `exit` 允许脚本指示失败。如果没有传递参数，当脚本运行结束（到达文件末尾），默认以退出状态 0 终止。

同样，shell 函数可以通过向 `return` 命令传递整数返回退出状态。如果我们把上面的脚本转换为 shell 函数并包含更大的程序中，可以用 `return` 语句替换 `exit` 命令并获得所需的行为：

```bash
test_file() {

  # test-file: 评估文件的状态

  FILE=".bashrc"

  if [ -e "$FILE" ]; then

    if [ -f "$FILE" ]; then

      echo "$FILE is a regular file."

    if [ -d "$FILE" ]; then

      echo "$FILE is a directory."

    if [ -r "$FILE" ]; then

      echo "$FILE is readable."

    if [ -w "$FILE" ]; then

      echo "$FILE is writable."

    if [ -x "$FILE" ]; then

      echo "$FILE is executable."

  else

    echo "$FILE does not exist"

    return 1

  fi

}
```

## 字符串表达式

表 27-2 中的表达式用于评估字符串。

### 表 27-2: test 字符串表达式

| 表达式 | 如果 . . . 则为真 |
| --- | --- |
| `string` | 字符串为空。 |
| `-n string` | 字符串长度大于零。 |

### 表 27-2（续）

| 表达式 | 如果 . . . 则为真 |
| - | - |
| `-z string` | 字符串长度为零。 |
| `string1 = string2` | `string1` 和 `string2` 相等。可以使用单双等号，但强烈建议使用双等号。 |
| `string1 != string2` | `string1` 和 `string2` 不相等。 |
| `string1 > string2` | `string1` 在 `string2` 之后排序。 |
| `string1 < string2` | `string1` 在 `string2` 之前排序。 |

**警告：** 使用 `>>` 时必须加引号（或用反斜杠转义）。如果不加，它们会被 shell 解析为重定向运算符，可能导致破坏性结果。此外注意，虽然 bash 文档说明排序顺序符合当前 locale 的排序规则，但事实并非如此。在包括 4.0 在内的 bash 版本中，使用的是 ASCII (POSIX) 排序。

这里有一个结合字符串表达式的脚本：

```bash
#!/bin/bash

# test-string: 评估字符串的值

ANSWER=maybe

if [ -z "$ANSWER" ]; then

    echo "There is no answer." >&2

    exit 1

fi

if [ "$ANSWER" = "yes" ]; then

    echo "The answer is YES."

elif [ "$ANSWER" = "no" ]; then

    echo "The answer is NO."

elif [ "$ANSWER" = "maybe" ]; then

    echo "The answer is MAYBE."

else

    echo "The answer is UNKNOWN."

fi
```

## 整数表达式

表 27-3 中的表达式用于整数。

### 表 27-3：测试整数表达式

| 表达式 | 如果满足以下条件则真 |
|---|---|
| `integer1 -eq integer2` | `integer1` 等于 `integer2`。 |
| `integer1 -ne integer2` | `integer1` 不等于 `integer2`。 |
| `integer1 -le integer2` | `integer1` 小于等于 `integer2`。 |
| `integer1 -lt integer2` | `integer1` 小于 `integer2`。 |
| `integer1 -ge integer2` | `integer1` 大于等于 `integer2`。 |
| `integer1 -gt integer2` | `integer1` 大于 `integer2`。 |

这里是一个演示这些内容的脚本：

```bash
#!/bin/bash

# test-integer: 评估整数的值。

INT=-5

if [ -z "$INT" ]; then

    echo "$INT is empty." >&2

    exit 1

fi

if [ $INT -eq 0 ]; then

    echo "$INT is zero."

else

    if [ $INT -lt 0 ]; then

        echo "$INT is negative."

    else

        echo "$INT is positive."

    fi

    if [ $((INT % 2)) -eq 0 ]; then

        echo "$INT is even."

    else
```
