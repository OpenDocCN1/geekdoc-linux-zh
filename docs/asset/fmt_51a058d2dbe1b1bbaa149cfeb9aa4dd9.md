
如果你执行该 shell 程序，将得到以下结果：

[点击此处查看代码图片]

- `dir1` is a directory
- `file1` is a regular file
- `file1` has read permission
- `file1` does not have write permission
- `dir1` has execute permission

# 逻辑运算符

你使用逻辑运算符通过布尔逻辑来比较表达式，布尔逻辑使用表示 NOT、AND 和 OR 的字符来比较值：

- `!` 对逻辑表达式进行取反
- `&&` 对两个逻辑表达式进行逻辑与
- `||` 对两个逻辑表达式进行逻辑或

这个具命名逻辑示例使用了之前 `compare3` 示例中提到的文件和目录：

点击此处查看代码图片

```sh
#!/bin/sh

if [ -x file1 -a -x dir1 ]; then
    echo file1 and dir1 are executable
else
    echo at least one of file1 or dir1 are not executable
fi

if [ -w file1 -o -w dir1 ]; then
    echo file1 or dir1 are writable
else
    echo neither file1 or dir1 are executable
fi

if [ ! -w file1 ]; then
    echo file1 is not writable
else
    echo file1 is writable
fi
```

如果你执行逻辑操作，它将产生以下结果：

```
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable
```

# 使用 `tcsh` 比较表达式

如前所述，在 `tcsh` 中比较表达式的方法在 `pdksh` 和 `bash` 下使用的方法不同。本节演示的表达式比较使用了 `tcsh` shell 环境所必需的语法。

## 字符串比较

你可以使用以下运算符来比较两个字符串表达式：

- `==` 比较两个字符串是否相等
- `!=` 比较两个字符串是否不等

以下示例在 shell 程序 `compare1` 中比较了两个字符串 `string1` 和 `string2`：

点击此处查看代码图片

```tcsh
#!/bin/tcsh

set string1 = "abc"
set string2 = "abd"

if (string1 == string2) then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
endif

if (string2 != string1) then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string1"
endif
```

如果你执行 `compare`，你将得到以下结果：

```
string1 not equal to string2
string2 not equal to string1
```

## 数字比较

你可以使用以下运算符来比较两个数字：

- `>=` 比较一个数字是否大于或等于另一个数字
- `<=` 比较一个数字是否小于等于另一个数字
- `>` 比较一个数字是否大于另一个数字
- `<` 比较一个数字是否小于另一个数字

下一个示例在 shell 程序 `compare2` 中比较了三个数字 `number1`、`number2` 和 `number3`：

点击此处查看代码图片

```tcsh
#!/bin/tcsh

set number1=5
set number2=10
set number3=5

if (number1 > number2) then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
endif

if (number1 >= number2) then
    echo "number1 is greater than or equal to number2"
else
    echo "number1 is not greater than or equal to number2"
endif

if (number1 < number2) then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
endif

if (number1 <= number2) then
    echo "number1 is less than or equal to number2"
else
    echo "number1 is not less than or equal to number2"
endif
```

shell 程序，其引用方式与用户最初调用命令的方式一致。

在 `tcsh` 中，`for` 语句被称为 `foreach`。其格式如下：

```
foreach curvar (list)
  statements
end
```

在这种形式下，`statements` 会为 `list` 中的每个值执行一次，并且在每次迭代中，`list` 的当前值会被赋值给 `curvar`。

假设你想为目录中的每个文件创建一个备份版本，并将其存放在名为 `backup` 的子目录中。你可以在 `pdksh` 和 `bash` 中执行以下操作：

[点击此处查看代码图片]

```sh
#!/bin/sh

for filename in *
  cp $filename backup/$filename
  if [ $? -ne 0 ]; then
    echo "copy for $filename failed"
  fi
done
```

在前面的示例中，为每个文件创建了备份副本。如果复制失败，将生成一条消息。

在 `tcsh` 中相同的示例如下：

[点击此处查看代码图片]

```tcsh
#!/bin/tcsh

foreach filename (`/bin/ls`)
  cp $filename backup/$filename
  if [ $? != 0 ]; then
    echo "copy for $filename failed"
  endif
end
```

## `while` 语句

你可以使用 `while` 语句在指定条件为真时执行一系列命令。一旦指定的条件求值为假，循环就会立即终止。如果指定的条件初始求值为假，则循环可能不会执行所有内容。你应该小心使用 `while` 命令，因为如果指定的条件从不求值为假，那么该循环将永远不会终止。

### 无限循环在 Shell 程序中的用处

无限循环有时是有有用的。例如，你可以通过几行脚本轻松地构建一个简单的命令，持续监控网络接口的 802.11 链路质量：

[点击此处查看代码图片]

```sh
#!/bin/sh

while :
do
  /sbin/iwconfig eth0 | grep Link | tr '\n' '\r'
Done
```

该脚本输出搜索结果，然后通过 `tr` 命令对输出进行格式化。结果是一个不断更新的单行信息的简单动画：

[点击此处查看代码图片]

```
Link Quality:92/92 Signal level:-11 dBm Noise level:-102 dBm
```

你还可以使用这种技术为 X 创建一个图形化监控客户端，输出关于网络接口的流量信息和活动：

[点击此处查看代码图片]

```sh
#!/bin/sh

xterm -geometry 75x2 -e \
bash -c \
  "while ; ; do \
    /sbin/ifconfig eth0 | \
    grep 'TX bytes' | \
    tr '\n'\r'; \
Done
```

这个简单的示例使用 `bash` 命令行脚本（通过 `-c` 启用）来重复执行命令行。该命令将 `ifconfig` 命令的输出通过 `grep`，`grep` 搜索 `ifconfig` 的输出，然后将包含 "TX bytes" 字符串的行通过 `tr` 命令。
`tr` 命令删除行尾的回车符，以便在由 `-geometry` 参数自动调整大小的 `xterm` X11 终端窗口中显示信息：

[点击此处查看代码图片]

```
RX bytes:4117594780 (3926.8 Mb) TX bytes:452230967 (431.2 Mb)
```
