
`-a file` 文件是否存在？（与 `-e` 相同）
`-b file` 文件是否为特殊设备？
`-c file` 文件是否为字符特殊设备（例如，字符设备）？用于识别串口和终端设备。
`-d file` 文件是否为目录？
`-e file` 文件是否存在？（与 `-a` 相同）
`-f file` 文件是否存在，且是否为普通文件（例如，不是目录、socket、管道、链接或设备文件）？
`-g file` 文件是否设置了组组 ID（set-group-id）位？
`-h file` 文件是否为符号链接？（与 `-L` 相同）
`-k file` 文件是否设置了粘位（sticky bit）？
`-L file` 文件是否为符号链接？
`-n string` 字符串长度是否大于 0 字节？
`-O file` 你拥有该文件吗？
`-p file` 文件是否为命名管道？
`-r file` 你可读取该文件吗？
`-s file` 文件是否存在且是否大于 0 字节？
`-S file` 文件是否存在且是否为 socket？
`-t fd` 文件描述符是否连接到终端？
`-u file` 文件是否设置了用户 ID（set-user-id）位？
`-w file` 你可写入该文件吗？
`-x file` 你可执行该文件吗？
`-z string` 字符串长度是否为 0（零）字节？
`expr1 -a expr2` 第一个表达式和第二个表达式是否都真？
`expr1 -o expr2` 两个表达式中至少有一个为真？
`file -nt file2` 第一个文件是否比第二个文件新（使用修改时间戳）？
`file -ot file2` 第一个文件是否比第二个文件旧（使用修改时间戳）？
`file1 -ef file2` 两个文件是否通过链接（硬链接或符号链接）关联？
`var1 = var2` 第一个变量等于第二个变量吗？
`var1 -eq var2` 第一个变量等于第二个变量吗？
`var1 -ge var2` 第一个变量大于或等于第二个变量吗？
`var1 -gt var2` 第一个变量大于第二个变量吗？
`var1 -le var2` 第一个变量小于或等于第二个变量吗？
`var1 -lt var2` 第一个变量小于第二个变量吗？
`var1 != var2` 第一个变量不等于第二个变量吗？
`var1 -ne var2` 第一个变量不等于第二个变量吗？

还有一种执行测试的简写方法，对于简单的单命令操作非常有用。在接下来的示例中，两个管道（`||`）表示如果测试的目录不存在（`-d dirname`），则创建目录（`mkdir $dirname`）。

```bash
# [ test ] || {action}
# 如果测试为假，执行简单的单命令 (action)
# -d $dirname || mkdir $dirname
```

除了管道，你可以使用两个与（`&&`）来测试某个内容如果包含至少三个命令行参数。

```bash
# [ test ] && {action}
# 如果测试为真，执行简单的单命令 (action)
# $ -ge 3 && echo "There are at least 3 command line arguments."
```

## case 命令

另一个经常使用的结构是 `case` 命令。类似于编程语言中的 `switch` 语句，它可以替代多个嵌套的 `if` 语句。`case` 语句的一般形式如下：

```bash
case "VAR" in
  Result1)
    { body };
  Result2)
    { body };
  *)
    { body };
esac
```

`case` 命令的一个用途可能是帮助进行备份。接下来的 `case` 测试当天的前三个字母（使用 `case `date+%a` in`）。然后，根据日期，使用特定的备份目录（`BACKUP`）和磁带驱动器（`TAPE`）：

```bash
# 我们的 VAR 没有一个变量，
# 它是命令的输出
case `date+%a` in
  Mon)
    BACKUP="/backups/mon"
    TAPE="/dev/st0"
    ;;
  Tue)
    BACKUP="/backups/tue"
    TAPE="/dev/st0"
    ;;
  Wed)
    BACKUP="/backups/wed"
    TAPE="/dev/st0"
    ;;
  Thu)
    BACKUP="/backups/thu"
    TAPE="/dev/st0"
    ;;
  Fri)
    BACKUP="/backups/fri"
    TAPE="/dev/st0"
    ;;
  Sat)
    BACKUP="/backups/sat"
    TAPE="/dev/st0"
    ;;
  Sun)
    BACKUP="/backups/sun"
    TAPE="/dev/st0"
    ;;
  *)
    echo "Unknown day"
    ;;
esac
```

`case` 命令是一种根据模式匹配变量并执行代码的方法。在处理许多可能的值时，它比使用多个 `if-elif-else` 语句简洁。

## for 循环

循环用于重复执行代码块。在 bash 中使用 `for` 循环的常用方法是遍历列表。

```bash
for item in list; do
  commands
done
```

另一种使用 `for` 循环的方法遍历数字范围：

```bash
for i in {1..10}; do
  echo $i
done
```

你还可以使用 `for` 循环遍历目录下的文件：

```bash
for file in *.txt; do
  echo "Processing $file"
done
```

## while 循环

`while` 循环在条件保持为真时持续执行代码块。

```bash
while condition; do
  commands
done
```

这是一个从 0 数到 9 的 `while` 循环示例：

```bash
n=0
while [ $n -lt 10 ]; do
  echo $n
  ((n++))
done
```

## until 循环

`until` 循环执行代码直到条件变为真。它是 `while` 循环的反相反。

```bash
until condition; do
  commands
done
```

这是一个从 0 数到 9 的 `until` 循环示例：

```bash
n=0
until [ $n -eq 10 ]; do
  echo $n
  ((n++))
done
```

## 外部程序

Bash 非常强大并且内置命令，但它通常需要帮助来完成实用的工作。你看到的常用程序有 `grep`、`cut`、`tr` 和 `sed`。与所有的 UNIX 工具一样，这些程序大多设计为与标准输入和输出工作，因此你可以轻松地在管道和 脚本中使用它们。

### 通用正则表达式解析器 (grep)

正则表达式解析器这个名字听起来很吓人，但 `grep` 只是在文件或文本中查找模式的方法。把它想象成实用的搜索工具。精通正则表达式是一个巨大的挑战，但许多有用操作可以通过简单的形式完成。

例如，你可以使用 `grep` 搜索 `/etc/passwd` 文件中包含 `/home/` 文本的行，显示所有普通用户账户列表：

```bash
grep /home /etc/passwd
```

或者你可以使用以下命令找到所有以 `HO` 开头的环境变量：

```bash
env | grep ^HO
```

要查找 `grep` 命令可使用的选项列表，请输入 `man grep`。

### 删除文本行的某些部分 (cut)

`cut` 命令可以从行文本或文件中提取特定的字段。它对于将系统配置文件解析为易于理解的块状数据非常有用。你可以指定想要使用的字段分隔符，也可以根据字节来拆分行。

以下示例列出了你系统中所有的主目录。使用之前 `grep` 命令的示例，此行通过管道从 `/etc/passwd` 文件中列出普通用户列表，并以冒号（`-d ':'`）作为分隔符显示第6个字段（`-f6`）。

```
grep /home /etc/passwd | cut -f6 -d':'
```

### 翻译或删除字符 (tr)

`tr` 命令是一个基于字符的翻译器，用于将一个字符或一组字符替换为另一个，或者从行文本中删除某个字符。

以下示例将所有大写字母转换为小写字母，并显示结果“mixed upper and lower case”单词：
