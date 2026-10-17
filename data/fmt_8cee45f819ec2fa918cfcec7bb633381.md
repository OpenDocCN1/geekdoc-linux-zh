
```bash
fi

if [ $(($int % 2)) -eq 0 ]; then

    echo "$int is even."

else

    echo "$int is odd."

fi

fi

else

    echo "Input value is not an integer." >&2

    exit 1

fi
```

我们使用 `-n` 选项 `echo` 以显示提示而不输出尾随换行，然后使用 `read` 为变量 `int` 输入值。运行此脚本的结果如下：

```
[me@linuxbox ~]$ read-integer

Please enter an integer -> 5

5 is positive.

5 is odd.
```

`read` 可以将输入分配给多个变量，如本脚本所示：

```bash
#!/bin/bash

# read-multiple: read multiple values from keyboard

echo -n "Enter one or more values > "

read var1 var2 var3 var4 var5

echo "var1 = '$var1'"

echo "var2 = '$var2'"

echo "var3 = '$var3'"

echo "var4 = '$var4'"

echo "var5 = '$var5'"
```

在此脚本中，我们分配并显示最多五个值。请注意 `read` 在给定不同数量的值时的行为：

```
[me@linuxbox ~]$ read-multiple

Enter one or more values > a b c d e

var1 = 'a'

var2 = 'b'

var3 = 'c'

var4 = 'd'

var5 = 'e'

[me@linuxbox ~]$ read-multiple

Enter one or more values > a

var1 = 'a'

var2 = ''

var3 = ''

var4 = ''

var5 = ''

[me@linuxbox ~]$ read-multiple

Enter one or more values > a b c d e f g

var1 = 'a'

var2 = 'b'

var3 = 'c'

var4 = 'd'

var5 = 'e f g'
```

如果 `read` 接收到的值少于预期数量，额外的变量为空，而过多的输入会导致最后一个变量包含所有额外输入。

如果 `read` 命令后没有列出变量，shell 变量 `REPLY` 将被分配所有输入：

```bash
#!/bin/bash

# read-single: read multiple values into default variable

echo -n "Enter one or more values > "

read

echo "REPLY = "$REPLY""
```

运行此脚本会得到以下结果：

```
[me@linuxbox ~]$ read-single
Enter one or more values > a b c d
REPLY = 'a b c d'
```

## Options

`read` 支持前面在表 28-1 中显示的选项。使用这些不同的选项，我们可以对 `read` 做一些有趣的事情。例如，使用 `-p` 选项，我们可以提供一个提示字符串：

```bash
#!/bin/bash

# read-single: read multiple values into default variable

read -p "Enter one or more values > "

echo "REPLY = '$REPLY'"
```

使用 `-t` 和 `-s` 选项，我们可以编写一个脚本来读取“秘密”输入，并在输入未在指定时间内完成时超时：

```bash
#!/bin/bash

# read-secret: input a secret passphrase

if read -t 10 -sp "Enter secret passphrase > " secret_pass; then
        echo -e "\nSecret passphrase = '$secret_pass'"
else
        echo -e "\nInput timed out" >&2
        exit 1
fi
```

该脚本提示用户输入一个秘密密码短语并等待 10 秒输入。如果在指定时间内未完成输入，脚本将以错误退出。由于包含 `-s` 选项，密码短语的字符在输入时不会回显到显示器上。

## 使用 IFS 分隔输入字段

通常，shell 会对提供给 `read` 的输入执行词分割。如我们所见，这意味着由一个或多个空格分隔的多个单词会成为输入行上的单独项目，并由 `read` 分配给不同的变量。这种行为由一个名为 `IFS` 的 shell 变量配置，即内部字段分隔符。`IFS` 的默认值包含一个空格、一个制表符和一个换行符，每个字符都会将项目彼此分隔开。

我们可以调整 `IFS` 的值来控制输入到 `read` 的字段的分隔方式。例如，`/etc/passwd` 文件包含使用冒号字符作为字段分隔符的数据行。通过将 `IFS` 的值更改为单个冒号，

我们可以使用 `read` 输入 `/etc/passwd` 的内容并成功地将字段分离到不同的变量中。下面有一个脚本正好实现了这一点：

```bash
#!/bin/bash

# read-ifs: read fields from a file

FILE=/etc/passwd

read -p "Enter a username > " user_name

file_info=$(grep "^${user_name}:" $FILE) ①

if [ -n "$file_info" ]; then

  IFS=":" read user pw uid gid name home shell <<< "$file_info" ②

  echo "User = $user"

  echo "UID = $uid"

  echo "GID = $gid"

  echo "Full Name = $name"

  echo "Home Dir. = $home"

  echo "Shell = $shell"

else

  echo "No such user $user_name" >&2

  exit 1

fi
```

该脚本提示用户输入系统上账户的用户名，然后显示在 `/etc/passwd` 文件中用户记录中找到的不同字段。脚本包含两行有趣的代码。第一行在 ①，将 `grep` 命令的结果赋给变量 `file_info`。`grep` 使用的正则表达式确保用户名只匹配 `/etc/passwd` 文件中的单行。

第二行有趣的代码在 ②，由三部分组成：变量赋值、带有变量名列表作为参数的 `read` 命令，以及一个奇怪的新重定向运算符。我们先来看变量赋值。

shell 允许在命令之前立即进行一个或多个变量赋值。这些赋值会更改后续命令的环境。赋值的效果是临时的，仅在命令执行期间更改环境。在我们的例子中，`IFS` 的值被更改为冒号字符。或者，我们也可以这样编写：

```bash
OLD_IFS="$IFS"

IFS=":"

read user pw uid gid name home shell <<< "$file_info"

IFS="$OLD_IFS"
```

其中我们存储 `IFS` 的值，分配新值，执行 `read` 命令，然后将 `IFS` 恢复到其原始值。显然，将变量赋值放在命令前面是一种更简洁的做同样事情的方法。

`<<<` 运算符表示 here string。here string 类似于 here document，只是更短，由单个字符串组成。在我们的示例中，来自 `/etc/passwd` 文件的数据行被馈送到 `read` 命令的标准输入。我们可能会想知道为什么选择这种相当迂回的方法，而不是

```bash
echo "$file_info" | IFS=":" read user pw uid gid name home shell
```

嗯，有原因的……

## YOU CAN'T PIPE READ

虽然 `read` 命令通常从标准输入获取输入，但你不能这样做：

```bash
echo "foo" | read
```
