
```
#!/bin/tcsh
if (-d dir1) then
echo "dir1 is a directory"
else
echo "dir1 is not a directory"
endif

if (-f file1) then
echo "file1 is a regular file"
else
echo "file1 is not a regular file"
endif

if (-r file1) then
echo "file1 has read permission"
else
echo "file1 does not have read permission"
endif

if (-w file1) then
echo "file1 has write permission"
else
echo "file1 does not have write permission"
endif
```

```
if (-x dir1) then
 echo "dir1 has execute permission"
else
 echo "dir1 does not have execute permission"
endif
```

```
if (-z file1) then
 echo "file1 has zero length"
else
 echo "file1 has greater than zero length"
endif
```

如果执行文件`compare3`，你会得到以下结果：

```text
dir1 is a directory
file1 is a regular file
file1 has read permission
file1 does not have write permission
dir1 has execute permission
file1 has greater than zero length
```

#### 逻辑操作符

逻辑操作符与条件语句一起使用。这些操作符用于否定逻辑表达式或执行逻辑与和逻辑或：

- `!` — 否定一个逻辑表达式
- `&&` — 逻辑与两个逻辑表达式
- `||` — 逻辑或两个逻辑表达式

此名为`logic`的示例使用了前面`compare3`示例中提到过的文件和目录。

```
#!/bin/tcsh
if ( -x file1 && -x dir1 ) then
 echo file1 and dir1 are executable
else
 echo at least one of file1 or dir1 are not executable
endif

if ( -w file1 || -w dir1 ) then
 echo file1 or dir1 are writable
else
 echo neither file1 or dir1 are executable
endif
```

```sh
if [ ! -w file1 ] then
    echo file1 is not writable
else
    echo file1 is writable
endif
```

如果执行`logic`，它会产生以下结果：

```text
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable
```

#### for 语句

`for` 语句用于在指定条件为真时每次执行一组命令。该语句有多种格式。`pdksh` 和 `bash` 使用的第一种格式如下：

```sh
for curvar in list
do
    statements
done
```

如果要对 `list` 中的每个值执行一次语句，应使用此形式。每次迭代时，列表的当前值会被赋给 `curvar`。`List` 可以是一个包含多个项目的变量，也可以是由空格分隔的值列表。第二种格式如下：

```sh
for curvar
do
    statements
done
```

在此形式中，语句会为传递给 shell 程序的每个位置参数执行一次。每次迭代时，位置参数的当前值会被赋给变量 `curvar`。

此形式也可以写成如下：

```sh
for curvar in $$*
do
    statements
done
```

请记住，`$*` 会给出传递给 shell 程序的位置参数列表，以与用户最初调用命令时一致的方式引用。

在 `tcsh` 下，`for` 语句称为 `foreach`。其格式如下：

```
foreach curvar (list)
    statements
end
```

在此形式中，语句会为 `list` 中的每个值执行一次，并且每次迭代时，`list` 的当前值会被赋给 `curvar`。

假设你想为目录中的每个文件创建一个备份版本到名为 `backup` 的子目录。你可以在 `pdksh` 和 `bash` 中这样做：

```
#!/bin/sh
for filename in *
do
    cp $filename backup/$filename
    if [ $? -ne 0 ]; then
        echo "copy for $filename failed"
    fi
done
```

在 `tcsh` 中相同的示例如下：

```
#!/bin/tcsh
foreach filename (`/bin/ls`)
cp $filename backup/$filename
if ($? != 0) then
    echo "copy for $filename failed"
endif
end
```

#### while 语句

`while` 语句可用于在指定条件为真时执行一系列命令。循环会在指定条件求值为 false 时立即终止。如果指定条件最初就求值为 false，则循环可能根本不会执行。你在使用 `while` 命令时应谨慎，因为如果指定条件永远不会求值为 false，循环将永远不会终止。

#### 无限循环在 Shell 程序中也有其用武之地

无限循环有时会很有用。例如，你可以很容易地构造一个简单的命令，通过几行脚本不断监控网络接口的 802.11b 链路质量：

```sh
#!/bin/sh
while :
  do
    /sbin/iwconfig eth0 | grep Link | tr '\n' '\r'
  done
```

该脚本输出搜索结果，然后 `tr` 命令格式化输出。结果是一个不断更新的单行信息的简单动画：

```
Link Quality=92/92  Signal level:-11 dBm  Noise level:-102 dBm
```

此技术也可用于创建 X 的图形监控客户端，用于输出网络接口的流量信息和活动情况：

```
#!/bin/sh
xterm -geometry 75x2 -e \
bash -c \
"while :; do \
/sbin/ifconfig eth0 | \
grep 'TX bytes' | \
tr '\n' '\r' ; \
done"
```

这个简单示例使用 `bash` 命令行脚本（由 `-c` 启用）来重复执行一条命令行。该命令行将 `ifconfig` 命令的输出通过管道传递给 `grep`，`grep` 搜索 `ifconfig` 的输出，然后将包含字符串 `"TX bytes"` 的行通过管道传递给 `tr` 命令。`tr` 命令随后删除行尾的回车符，以便在 `xterm` X11 终端窗口中显示信息，窗口大小由 `-geometry` 选项自动设定：

```
RX bytes:4117594780 (3926.8 Mb)  TX bytes:452230967 (431.2 Mb)
```

无限循环可能非常有用，以至于 Linux 包含了一个命令来重复执行给定的命令行。例如，你可以使用 `sensors` 命令快速获取系统硬件健康状况的报告。但与其使用 shell 脚本来无限循环输出，不如使用 `watch` 命令来重复信息并提供简单的动画：

```
$ watch 'sensors -f | cut -c 1-20'
```

在 `pdksh` 和 `bash` 中，`while` 流程控制构造的格式如下：

```
while expression
do
  statements
done
```

在 `tcsh` 中，使用以下格式：

```
while (expression)
  statements
end
```

如果你想将前五个偶数相加，可以在 `pdksh` 和 `bash` 中使用以下 shell 程序：
