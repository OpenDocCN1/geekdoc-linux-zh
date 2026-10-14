
| 选项 | 描述 |
|---|---|
| -a array | 将输入赋值给数组，从索引零开始。我们将在第 35 章讨论数组。 |
| -d | 字符串分隔符中的第一个字符用于表示输入的结束，而不是换行符。 |
| -e | 使用 Readline 处理输入。这样可以在输入时像命令行一样进行编辑。 |
| -i string | 如果用户只是按下 ENTER，则使用 string 作为默认回复。需要 -e 选项。 |
| -n num | 读取 num 个输入字符，而不是整行。 |
| -p prompt | 使用 string 作为提示符显示输入提示。 |
| -r | 原始模式。不将反斜杠字符解释为转义字符。 |
| -s | 静默模式。输入时不在显示器上回显字符。这适用于输入密码和其他机密信息。 |
| -t seconds | 超时。在 seconds 秒后终止输入。如果输入超时，read 返回非零退出状态。 |
| -u fd | 使用文件描述符 fd 的输入，而不是标准输入。 |

使用这些不同的选项，我们可以用 read 做一些有趣的事情。例如，使用 -p 选项，我们可以提供一个提示字符串。

```
#!/bin/bash

# read-single: read multiple values into default variable

read -p "Enter one or more values > "

echo "REPLY = '$REPLY'"
```

使用 -t 和 -s 选项，我们可以编写一个脚本，读取“秘密”输入，如果未在指定时间内完成输入，则超时。

```
#!/bin/bash

# read-secret: input a secret passphrase

if read -t 10 -sp "Enter secret passphrase > " secret_pass; then
    echo -e "\nSecret passphrase = '$secret_pass'"
else
    echo -e "\nInput timed out" >&2
    exit 1
fi
```

该脚本提示用户输入机密口令，并等待 10 秒。如果在指定时间内未完成输入，脚本将以错误退出。由于包含了 -s 选项，输入口令时不会在显示器上回显字符。

我们可以将 -e 和 -i 选项一起使用，为用户提供一个默认回复。

```
#!/bin/bash

# read-default: supply a default value if user presses Enter key.

read -e -p "What is your user name? " -i $USER
echo "You answered: '$REPLY'"
```

在这个脚本中，我们提示用户输入用户名，并使用环境变量 USER 提供默认值。运行脚本时，它会显示默认字符串，如果用户只是按下 ENTER，read 就会将默认字符串赋值给 REPLY 变量。

```
[me@linuxbox ~]$ read-default
What is your user name? me
You answered: 'me'
```

## IFS

通常，shell 会对提供给 read 的输入执行分词。正如我们所见，这意味着由一个或多个空格分隔的多个单词会成为输入行中的独立项，并由 read 分配给不同的变量。此行为由名为 IFS（Internal Field Separator，内部字段分隔符）的 shell
变量配置。IFS 的默认值包含一个空格、一个制表符和一个换行符，它们会将各项彼此分隔。

我们可以调整 IFS 的值来控制 read 输入的字段分隔。例如，/etc/passwd 文件包含使用冒号字符作为字段分隔符的数据行。通过将 IFS 的值改为单个冒号，我们可以使用 read 输入 /etc/passwd 的内容，并成功将字段分隔到不同的变量中。这里有一个脚本就实现了这一点：

```
#!/bin/bash

# read-ifs: read fields from a file

FILE=/etc/passwd

read -p "Enter a username > " user_name

file_info=$(grep "^$user_name:" $FILE)

if [ -n "$file_info" ]; then
IFS=":" read user pw uid gid name home shell <<< "$file_info"
echo "User =      '$user'"
echo "UID =       '$uid'"
echo "GID =       '$gid'"
echo "Full Name = '$name'"
echo "Home Dir. = '$home'"
echo "Shell =     '$shell'"
else
echo "No such user '$user_name'" >&2
exit 1
fi
```

该脚本提示用户输入系统上某个账户的用户名，然后显示在 /etc/passwd 文件中该用户记录中找到的不同字段。此脚本包含两行有趣的代码。第一行如下：

```
file_info=$(grep "^$user_name:" $FILE)
```

这行将 grep 命令的结果赋值给变量 file_info。grep 使用的正则表达式确保用户名
