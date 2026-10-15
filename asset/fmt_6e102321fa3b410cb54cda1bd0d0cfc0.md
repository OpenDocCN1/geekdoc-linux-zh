
### 7.3 使用循环重复命令：`for` 语句

`for` 命令也允许多次执行命令。它的工作原理如下：

```bash
for i in cow sheep chickens pigs
do
  echo "$i is a farm animal"
done

echo -e "but\nGNUs are not farm animals"
```

`for` 命令获取 `in` 之后的每一个字符串，并执行 `do` 和 `done` 之间的行，其中用 `i` 替换该字符串。字符串可以是任何内容（甚至是数字），但通常是文件名。

`if` 命令在满足条件时执行一组命令（`-gt` 表示大于，`-lt` 表示小于）。`if` 命令执行 `if` 和 `fi`（"if" 的倒写）之间的所有行。

```bash
X=10
Y=5
if test "$X" -gt "$Y"; then
    echo "$X is greater than $Y"
fi
```

`if` 命令的完整形式可以包含如下内容：

```bash
X=10
Y=5
if test "$X" -gt "$Y"; then
    echo "$X is greater than $Y"
elif test "$X" -lt "$Y"; then
    echo "$X is less than $Y"
else
    echo "$X is equal to $Y"
fi
```

现在让我们创建一个解释其参数的脚本。创建一个名为 `backup-lots.sh` 的新脚本，内容如下：

```bash
#!/bin/sh
for i in 0 1 2 3 4 5 6 7 8 9; do
    cp $1 $1.BAK-$i
done
```

现在创建一个名为 `important_data` 的文件，其中包含任意内容，然后运行 `./backup-lots.sh important_data`，这将复制文件 10 次，并带有 10 个不同的扩展名。如你所见，`$1` 有特殊含义——它是命令行上的第一个参数。现在让我们让它变得复杂一点（使用 `-e` 测试文件是否存在）：

```bash
#!/bin/sh
if test "$1" = ""; then
    echo "Usage: backup-lots.sh <filename>"
    exit
fi
for i in 0 1 2 3 4 5 6 7 8 9; do
    NEW_FILE=$1.BAK-$i
    if test -e $NEW_FILE; then
        echo "backup-lots.sh: 文件已存在"
    else
        echo "backup-lots.sh: 备份了 $NEW_FILE"
    fi
done
```

### 7.4 退出循环与继续循环：`break` 和 `continue`

`break` 命令用于从内部退出循环。`continue` 命令则跳过当前迭代的剩余部分并进入下一次迭代。它们在 `for`、`while` 和 `until` 循环中都很有用：

```bash
#!/bin/sh
for i in 0 1 2 3 4 5 6 7 8 9; do
    if [ $i -eq 5 ]; then
        echo "在 5 处退出循环"
        break
    fi
    if [ $i -eq 2 ]; then
        echo "跳过 2 并继续后续"
        continue
    fi
    echo "数字: $i"
done
```

### 7.5 针对通配符进行循环

我们知道 shell 可以展开通配符。例如，shell 可以展开文件名：

```bash
#!/bin/sh
for i in *.txt; do
    echo "找到文件: $i"
done
```

`for` 命令可以展开匹配模式的任何字符串。这在任何情况下都有效：

### 7.6 `case` 语句

`case` 语句允许变量的值指定不同的块。例如：

```bash
#!/bin/sh
case $1 in
  --test)
    echo "你使用了 test 选项"
    exit 0
    ;;
  --help)
    echo "用法:"
    echo "myprog.sh [--test|--help]"
    exit 0
    ;;
  --version)
    echo "myprog.sh 版本"
    exit 0
    ;;
  *)
    echo "错误：无此类选项 $1"
    exit 1
esac
```

### 7.7 使用函数

到目前为止，我们的程序主要从上往下执行。通常，代码需要重复，但重复语句是良好的做法。函数定义提供了将语句分组的方法。例如：

```bash
#!/bin/sh
function usage ()
{
  echo "用法:"
  echo "myprog.sh [--test|--version]"
}
```

在出现 `usage` 关键字的地方，它会被替换为 `{` 和 `}` 内部的内容。这种方法有而易见的优点：如果你想更改程序的用法说明，只需要更改代码中的一处。良好的程序频繁使用函数，以至于连续代码不会超过 50 行。

### 7.8 正确处理命令行参数：`shift` 关键字

我们看到的大多数程序都可以接受许多命令行参数，有时顺序任意。这里是我们如何通过这种方式创建自己的 shell 脚本。命令行参数可以通过 `$1`、`$2` 等访问。脚本：

```bash
#!/bin/sh
echo "第一个参数是: $1, 第二个参数是: $2, 第三个参数是: $3"
```

可以通过 `myfile.sh dogs cats birds` 运行并打印 `第一个参数是: dogs, 第二个参数是: cats, 第三个参数是: birds`。

我们需要遍历每个参数并决定对它做什么。像这样的脚本：

```bash
for i in $1 $2 $3 $4; do
    <语句>
done
```

并没有给我们提供多少灵活性。`shift` 关键字旨在让事情变得更容易。它将所有参数向上移动一位，使得 `$1` 获取 `$2` 的值，`$2` 获取 `$3` 的值，以此类推。（测试 `"$1" != ""`——即，检查它是否为空，因此已经过了最后一个参数。）尝试

## 7.9 更多关于命令行参数：`$@`

其中 `$1`、`$2`、`$3` 等扩展为传递给程序的各个参数，而 `$@` 则会扩展为所有参数。这种行为对于将所有剩余参数传递给第二个命令非常有用。例如，

```bash
if test "$1" = "--special"; then
    shift
    myprog2.sh "$@"
fi
```
