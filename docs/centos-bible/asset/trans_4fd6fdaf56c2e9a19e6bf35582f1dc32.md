

## 测试表达式运算符

### 代码示例

你也可以使用感叹号（!）来反转测试。在下面的示例中，如果 STRING 不等于 Monday，则会回显 "At least it's not Monday"。

```bash
STRING="Friday"
if [ "$STRING" != "Monday" ] ; then
  echo "At least it's not Monday"
fi
```

在下面的示例中，使用 elif（即“否则如果”）来测试额外的条件（filename 是文件还是目录）。

```bash
filename="$HOME"
if [ -f "$filename" ] ; then
  echo "$filename is a regular file"
elif [ -d "$filename" ] ; then
  echo "$filename is a directory"
else
  echo "I have no idea what $filename is"
fi
```

从上述示例中可以看出，你要测试的条件被放置在方括号 [ ] 之间。当测试表达式被评估时，它返回值为 0（表示真）或 1（表示假）。请注意，echo 行进行了缩进。这是可选的，只是为了使脚本更易读。

表 11-2 列出了可测试的条件，是一个非常实用的参考。（如果你很赶时间，可以在命令行输入 `help test` 来获取相同的信息。）

还有一种执行测试的特殊简写方法，对于简单的单命令操作可能非常有用。在下面的示例中，两个管道符（||）表示如果正在测试的目录不存在（`-d $dirname`），则创建该目录（`mkdir $dirname`）。

```bash
# [ test ] || (action)
# 如果测试为假，则执行简单的单命令操作 (action)
dirname="~/tmp/testdir"
[ -d "$dirname" ] || mkdir "$dirname"
```

你可以使用两个和号（&&）代替管道符来测试某事物是否为真。在下面的示例中，测试一条命令以查看它是否包含至少三个命令行参数。

```bash
# [ test ] && (action)
# 如果测试为真，则执行简单的单命令操作 (action)
[ $# -ge 3 ] && echo "There are at least 3 command line arguments."
```

## 表 11-2：测试表达式运算符

| 运算符 | 测试内容？ |
| :--- | :--- |
| `-a file` | 文件是否存在？（等同于 `-e`） |
| `-b file` | 文件是否为特殊块设备？ |
| `-c file` | 文件是否为字符特殊设备（例如，字符设备）？用于识别串行线和终端设备。 |
| `-d file` | 文件是否为目录？ |
| `-e file` | 文件是否存在？（等同于 `-a`） |
| `-f file` | 文件是否存在，且是否为常规文件（例如，不是目录、套接字、管道、链接或设备文件）？ |
| `-g file` | 文件是否设置了 set-group-id 位？ |
| `-h file` | 文件是否为符号链接？（等同于 `-L`） |
| `-k file` | 文件是否设置了 sticky 位？ |
| `-L file` | 文件是否为符号链接？ |
| `-n string` | 字符串长度是否大于 0 字节？ |
| `-O file` | 你是否拥有该文件？ |
| `-p file` | 文件是否为命名管道？ |
| `-r file` | 你是否可以读取该文件？ |
| `-s file` | 文件是否存在，且大小是否大于 0 字节？ |
| `-S file` | 文件是否存在，且是否为套接字？ |
| `-t fd` | 文件描述符是否连接到终端？ |
| `-u file` | 文件是否设置了 set-user-id 位？ |
| `-w file` | 你是否可以写入该文件？ |
| `-x file` | 你是否可以执行该文件？ |
| `-z string` | 字符串长度是否为 0（零）字节？ |
| `expr1 -a expr2` | 第一个表达式和第二个表达式是否都为真？ |
| `expr1 -o expr2` | 两个表达式中是否有一个为真？ |
| `file1 -nt file2` | 第一个文件是否比第二个文件新（使用修改时间戳）？ |
| `file1 -ot file2` | 第一个文件是否比第二个文件旧（使用修改时间戳）？ |
| `file1 -ef file2` | 两个文件是否通过链接（硬链接或符号链接）相关联？ |
| `var1 = var2` | 第一个变量是否等于第二个变量？ |
| `var1 -eq var2` | 第一个变量是否等于第二个变量？ |
| `var1 -ge var2` | 第一个变量是否大于或等于第二个变量？ |
| `var1 -gt var2` | 第一个变量是否大于第二个变量？ |
| `var1 -le var2` | 第一个变量是否小于或等于第二个变量？ |
| `var1 -lt var2` | 第一个变量是否小于第二个变量？ |
| `var1 != var2` | 第一个变量是否不等于第二个变量？ |
| `var1 -ne var2` | 第一个变量是否不等于第二个变量？ |

## case 命令

另一个常用的构造是 *case* 命令。类似于编程语言中的 *switch* 语句，它可以取代多个嵌套的 *if* 语句。*case* 语句的一般形式如下：

```bash
case "$VAR" in
    Result1)
        { body };;
    Result2)
        { body };;
    *)
        { body };;
esac
```

*case* 命令的一个用途可能是帮助备份。下面的 *case* 语句测试当前日期的前三个字母（*case* "`date +%a`" in）。然后，根据星期几，设置特定的备份目录（BACKUP）和磁带驱动器（TAPE）。

```bash
# 我们的 VAR 不一定非要是一个变量，
# 它也可以是命令的输出
# 根据星期几执行操作
case "$(date +%a)" in
    "Mon")
        BACKUP=/home/myproject/data0
        TAPE=/dev/rft0
        ;;
    # 注意使用 "|" 表示 "或"
    "Tue" | "Thu")
        BACKUP=/home/myproject/data1
        TAPE=/dev/rft1
        ;;
    "Wed" | "Fri")
        BACKUP=/home/myproject/data2
        TAPE=/dev/rft2
        ;;
    # 周末不进行备份。
    *)
        BACKUP="none"
        TAPE=/dev/null
        ;;
esac
```

星号 (*) 用作通配符，类似于 C 编程语言中的 *default* 关键字。在这个例子中，如果在循环中匹配不到其他任何条目，则匹配星号，*BACKUP* 的值变为 *none*。注意使用 *esac*（即 case 的倒写）来结束 case 语句。

## for . . . do 循环

循环用于反复执行操作，直到满足条件或处理完所有数据。最常用循环之一是 *for* . . . *do* 循环。它遍历值列表，对列表中的每个元素执行循环体。语法和几个示例如下：

```bash
for VAR in LIST
do
    { body }
done
```

*for* 循环将 *LIST* 中的值逐个赋值给 *VAR*。然后，对于每个值，在 *do* 和 *done* 之间的大括号内的循环体会被执行。*VAR* 可以是任何变量名，*LIST* 可以由几乎任何值列表或生成列表的内容组成。

```bash
for NUMBER in 0 1 2 3 4 5 6 7 8 9
do
    echo The number is $NUMBER
done
```

```bash
for FILE in `/bin/ls`
do
    echo $FILE
done
```

你也可以这样写，这样稍微清晰一些：

```bash
for NAME in John Paul Ringo George ; do
    echo "$NAME is my favorite Beatle"
done
```

LIST 中的每个元素之间用空白符分隔。如果不注意，这可能会带来麻烦，因为某些命令（如 `ls -l`）每行输出多个字段，每个字段之间用空白符分隔。字符串 done 结束 for 语句。

如果你是一名资深的 C 程序员，Bash 允许你使用 C 语法来控制循环：

```bash
LIMIT=10
# 双括号，即使是变量 LIMIT 也没有 $ 符号！
for ((a=1; a <= LIMIT ; a++)) ; do
    echo "$a"
done
```

## while . . . do 和 until . . . do 循环

另外两种可能的循环构造是 *while* . . . *do* 循环和 *until* . . . *do* 循环。它们的结构如下所示：

```bash
while condition         until condition
do                        do
( body )                 ( body )
done                      done
```

*while* 语句在条件为真时执行。*until* 语句在条件为真时执行完毕，换句话说，在条件为假时执行。

这里是一个 *while* 循环的示例，它将输出数字 0123456789：

```bash
N=0
while [ $N -lt 10 ] ; do
    echo -n $N
    let N=$N+1
done
```

输出数字 0123456789 的另一种方法是使用 *until* 循环如下：

```bash
N=0
until [ $N -eq 10 ] ; do
    echo -n $N
    let N=$N+1
done
```

