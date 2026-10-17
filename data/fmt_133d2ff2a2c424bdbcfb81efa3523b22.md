
# 472 第 11 章 编写 Bourne Again Shell

```bash
function mycp (
{
  case $# in
    0)
      # 零参数
      # 文件描述符 3 复制标准输入
      # 文件描述符 4 复制标准输出
      exec 3<&4 -&1
    ;;
    1)
      # 一个参数
      # 打开由参数命名的文件用于输入
      # 并将其与文件描述符 3 关联
      # 文件描述符 4 复制标准输出
      exec 3<$1 4<&1
    ;;
    2)
      # 两个参数
      # 打开第一个参数命名的文件用于输入
      # 并将其与文件描述符 3 关联
      # 打开第二个参数命名的文件用于输入
      # 并将其与文件描述符 4 关联
      exec 3<$1 >$2
    ;;
    *)
      echo "Usage: mycp [source] [dest]"
      return 1
  esac

  # 调用 cat 从文件描述符 3 读取输入
  # 并输出到文件描述符 4
  cat <&3 >&4

  # 关闭文件描述符 3 和 4
  exec 3<&- 4<&-
}
```

该函数的实际工作是在以 `cat` 开头的行中完成的。脚本的其他部分安排了描述符 3 和 4（即 `cat` 命令的输入和输出）与适当的文件关联。

# 474 第 11 章 编写 Bourne Again Shell

下一个程序接受命令行上的两个文件名，对两者进行排序，并将输出发送到临时文件。程序将排序后的文件合并到标准输出，并在每行前面加上一个指示其来源的数字。

```bash
$ cat sortmerge
#!/bin/bash

usage ()
{
  if [ $# -ne 2 ]; then
    echo "Usage: $0 file1 file2" >&1
    exit 1
  fi
}

# 默认临时目录
: ${TMPDIR:=tmp}

# 检查参数计数
usage "$@"

# 为排序设置临时文件
file1=$TMPDIR/.$$.file1
file2=$TMPDIR/.$$.file2

# 排序
sort $1 > $file1
sort $2 > $file2

# 为读取打开 $file1 和 $file2。使用文件描述符 3 和 4。
exec 3<$file1
exec 4<$file2

# 从每个文件中读取第一行以确定如何开始。
read Line1 <&3
status1=$?
read Line2 <&4
status2=$?

# 策略：当两个文件中都有输入时：
# 输出应该先出现的行。
# 从该行所在的文件中读取新行。
while [ $status1 -eq 0 -a $status2 -eq 0 ];
do
    if [[ "$Line2" > "$Line1" ]]; then
        echo -e "1.\t$Line1"
        read Line1 <&3
        status1=$?
    else
        echo -e "2.\t$Line2"
        read Line2 <&4
        status2=$?
    fi
done

# 现在其中一个文件已到达末尾。
# 从每个文件读取到结束。
# 第一个 file1:
while [ $status1 -eq 0 ];
do
    echo -e "1.\t$Line1"
    read Line1 <&3
    status1=$?
done

# 下一个 file2:
while [ $status2 -eq 0 ];
do
    echo -e "2.\t$Line2"
    read Line2 <&4
    status2=$?
done

# 关闭并删除两个输入文件
exec 3<&-
rm -f $file1 $file2

exit 0
```

# 参数与变量

Shell 参数和变量已在第 277 页介绍。本节对之前的内容进行了补充，讨论了数组变量、全局与局部变量、特殊和位置参数，以及空变量和未设置变量的扩展。

## 数组变量

Bourne Again Shell 支持一维数组变量。下标是整数，且从 `0` 开始索引（即数组的第一个元素下标为 `0`）。以下格式用于声明并为数组赋值值：

```bash
name=(element1 element2 ...)
```

以下示例为 `NAMES` 数组分配了四个值：

```bash
$ NAMES=(max helen sam zach)
```

你通过如下方式引用数组的单个元素：

```bash
$ echo ${NAMES[2]}
sam
```

下标 `[*]` 和 `[]` 都可以提取整个数组，但在引号内使用时工作方式不同。`@` 是原始数组的副本；`*` 产生数组的单个元素（或普通变量），该元素包含 `IFS` 中的第一个字符（通常是空格）分隔的数组所有元素。在下面的示例中，数组 `A` 使用 `*` 用 `NAMES` 变量的元素填充，而 `B` 使用 `@` 填充。带有 `-` 选项的内置命令 `declare` 显示数组的值（并提醒你 `bash` 对数组使用从 `0` 开始的索引）：

```bash
$ A="${NAMES[*]}"
$ B="${NAMES[@]}"
```

```bash
declare -a
declare -a A='[0]="max helen sam zach"
declare -a B='[0]="max" [1]="helen" [2]="sam" [3]="zach"'
```

```bash
declare -a NAMES='[0]="max" [1]="helen" [2]="sam" [3]="zach"
```

![](img/c0494f8f1ebc7cc234d912ea2765b44e_513_0.png)

从 `declare` 的输出中，你可以看到 `NAMES` 和 `B` 有多个元素。相比之下，在双引号内使用 `*` 赋值的 `A` 只有一个元素：`A` 的所有元素都被包含在双引号之间。

在下一个示例中，`echo` 尝试显示数组 `A` 的元素 `1`。什么都没有显示，因为 `A` 只有一个元素：`A` 的所有元素都被包含在双引号之间。
