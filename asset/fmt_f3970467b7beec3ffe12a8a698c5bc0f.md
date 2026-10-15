
| 运算符 | 正在测试什么？ |
| --- | --- |
| `-b file` | 文件是否为特殊块（例如，块设备）？用于识别磁盘和磁带设备。 |
| `-c file` | 文件是否为特殊字符（例如，字符设备）？用于识别串口线和终端设备。 |
| `-d file` | 文件是否为目录？ |
| `-e file` | 文件是否存在？ |
| `-f file` | 文件是否存在且为普通文件（例如，不是目录、套接字、管道、链接或设备文件）？ |
| `-g file` | 文件是否设置了组 ID（set-group-id）位？ |
| `-G file` | 文件是否存在且其组所有权是否与当前用户的主组相同？ |
| `-k file` | 文件是否设置了粘滞位（sticky bit）？ |
| `-L file` | 是否为符号链接？ |
| `-n string` | 字符串长度是否大于 0 字节？ |
| `-0 file` | 文件是否存在且当前用户是否拥有它？ |
| `-p file` | 是否为命名管道？ |
| `-r file` | 文件是否存在且可读？ |
| `-s file` | 文件是否存在且是否大于 0 字节？ |
| `-S file` | 文件是否存在且为套接字？ |
| `-t fd` | 文件描述符是否已打开？ |
| `-u file` | 文件是否设置了用户 ID（set-user-id）位？ |
| `-w file` | 文件是否存在且可写？ |
| `-x file` | 文件是否存在且可执行？ |
| `-z` | 字符串长度是否为 0 字节？ |
| `expr1 -a expr2` | 第一个和第二个表达式是否都为真？ |
| `expr1 -o expr2` | 两个表达式中是否有一个为真？ |
| `file1 -nt file2` | 第一个文件是否比第二个文件新（使用修改时间）？ |
| `file1 -ot file2` | 第一个文件是否比第二个文件旧（使用修改时间）？ |

# 第 12 章自动化系统任务 401

| 运算符 | 正在测试什么？ |
| --- | --- |
| `file1 -ef file2` | 两个文件是否通过链接关联（硬链接或符号链接）？ |
| `var1 -eq var2` | 第一个变量是否等于第二个变量？ |
| `var1 -ge var2` | 第一个变量是否大于或等于第二个变量？ |
| `var1 -gt var2` | 第一个变量是否大于第二个变量？ |
| `var1 -le var2` | 第一个变量是否小于或等于第二个变量？ |
| `var1 -lt var2` | 第一个变量是否小于第二个变量？ |
| `var1 -ne var2` | 第一个变量是否不等于第二个变量？ |

以下是一些演示 `if` 语句和测试表达式用的示例：

```
if [ -x /sbin/config ]
if [ $4 -eq "nl" ]
if [ $# -gt 2 ]
if [ -z $HOSTNAME ]
```

在上一个示例中，第一个语句检查 `/sbin/config` 程序是否可执行。第二个示例检查字符串 `nl` 是否等于存储在 `$4` 中的值（第四个命令行参数）。下一行检查命令行参数的数量（由变量 `$#` 表示）是否大于 2。最后一个示例确定变量 `$HOSTNAME` 是否为空。

## 用于嵌套语句的 case 命令

另一个经常使用的结构是 `case` 命令。类似于编程语言中的 `switch` 语句，它可以替代多个嵌套语句。`case` 语句的通用形式如下：

```
case "VAR" in
  Result1) { body }
  Result2) { body }
  *) { body }
esac
```

这是一个 `case` 命令的示例。这段代码根据 `/etc/passwd` 文件中第七列（冒号分隔）的默认 shell 设置 `TYPE` 和 `RCFILE` 变量：

```
Shell=$(grep "$USER:" /etc/passwd | awk -F: '{ print $7 }')
case "$Shell" in
```

## 402 部分 管理 Red Hat Linux

```
/bin/sh) TYPE=Bourne
RCFILE=".profile"
/bin/csh) TYPE=C
RCFILE=".cshrc"
/bin/bash) TYPE=Bourne
RCFILE=".bashrc"
/bin/tcsh) TYPE=C
RCFILE=".tcshrc"
*) TYPE=other
RCFILE=".unknown"
esac
```

星号 (`*`) 用作通配符。如果循环中没有匹配到其他项，则匹配星号并将值设置为 `unknown`。

## while ... until ... 循环

两种可能的循环结构是 `while ...` 循环和 `until ...` 循环。它们的结构如下：

```
while condition
do
  body
done
```

在 `while` 循环中，`condition` 通常是一个测试语句，但也可以用于直到遇到文件结束 (`<EOF>`)。如果使用了测试条件，当 `condition` 为假时会执行 `body` 中的代码。这里有一个示例：

```
read COL1 COL2
echo -n $COL2 > /home/user/file
done
```

此循环将从键盘读取值（每 4 个为一组），重新排列列，并以特定格式输出到文件。`until` 循环在 `condition` 为真（返回值为 0）时执行 `body` 中的代码。

```
COUNT=1
until [ $COUNT -eq 4 ]
do
  DIR=/home/user/proj/$COUNT
  if [ ! -d $DIR ]
  then
    mkdir $DIR
  fi
  cp /home/user/proj/template $DIR
  COUNT+=1
done
```

前述循环在目录不存在时创建目录，并将 `template` 文件复制到其中。这将一直重复直到 `COUNT` 变量的值等于 4（四次迭代）。

## 尝试一些简单的脚本

有时最简单的脚本可能是最有用的。如果你反复输入相同的命令，将这些命令存储在文件中是有意义的。这里有一些简单实用的 shell 脚本示例。

### 一个简单的备份脚本

如果你多年来一直在收集项目数据，你可能希望备份你的工作以防原始文件发生意外。与其每次都输入完整的命令，不如将备份存储在 shell 脚本中：

```bash
#!/bin/bash
mt /dev/0 rew
cd /home/user/data
tar cvf /dev/0
mt /dev/0 rew
```

此脚本带有 `rew` 运行 `mt` 命令，重置磁带驱动器（`/dev/0`）中的磁带。接下来，`cd` 命令将目录更改到 `/home/user/data`。`tar` 命令从当前目录的文件创建归档 (`c`)，详细模式 (`v`) 描述其正在操作，并将归档输出到磁带设备 (`f /dev/0`)。`mt` 命令重置并弹出磁带设备 (`rew` `/dev/0`)）。要进行进一步的自动化，请参见本章后面关于 `cron` 功能的部分。

备份操作系统同样重要。有关备份和恢复文件的详情请参见第 13 章。

![](img/176fafece2d30daee750bc078e98ee4_434_0.png)

### 磁盘检查脚本

另一个常见的管理问题是磁盘空间，资源似乎总是短缺。如果你经常检查用户目录的大小，以下脚本可能很有用：

```
#!/bin/bash
cd /home ; du -s * | sort -rn
```

使用 `-h` 选项可以让 `du` 的输出更易读。此脚本列出 `/home` 下的所有目录并报告其以 KB 为单位的大小。输出按数字排序，最大的目录位于列表顶部。如果你有位于 `/home` 目录以外的用户目录，以下（稍微复杂的）脚本会更有用：

```bash
#!/bin/bash
TMPfile=/tmp/$$
for i in $(awk -F: 'if ($3 > 500) print $6 ' /etc/passwd)
du -s $i > $TMPfile
done
sort -rn $TMPfile
rm $TMPfile
exit 0
```

在此脚本中，`awk` 从 `/etc/passwd` 文件中选择特定的信息。使用冒号作为分隔符（`-F:` 选项），`awk` 检查每行的第三字段（用户 ID 或 UID）是否大于或等于 500（默认情况下，普通用户账户的起点）。如果是，则返回用户的家目录（第六字段）。`for` 循环检查 `awk` 返回的列表，对每个目录执行磁盘检查。结果存储在一个唯一的临时文件中（`$$` 变量代表运行程序的进程 ID）。该临时文件按数字排序并删除。上述任一程序的程序的结果看起来如下：

936890 /home/jsmith

489349 /home/oracle

20439 /home/wilhelm

748 /home/acard
