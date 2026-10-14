
通过在脚本逻辑区域的每行开头放置注释符号，我们可以防止该部分代码被执行。然后可以再次测试，以查看删除代码对错误行为是否有任何影响。

# 追踪 (Tracing)

错误通常是脚本内部意外的逻辑流导致的。也就是说，脚本的某些从未从未执行，或者以错误的顺序或时间执行。为了查看程序的实际执行流，我们使用一种名为*追踪* 的技术。
追踪涉及在脚本中放置信息性消息，以显示执行的位置。我们可以向代码片段中添加消息。

```bash
echo "preparing to delete files" >&2

if [[ -d $dir_name ]]; then

  if cd $dir_name; then

    echo "deleting files" >&2

  else

    echo "cannot cd to '$dir_name'" >&2

    exit 1

  fi

else

  echo "no such directory: '$dir_name'" >&2

  exit 1

fi

echo "file deletion complete" >&2
```

我们将消息发送到标准错误，以便将其与输出分开。我们也没有对包含消息的行进行缩进，这样在需要删除它们时更容易找到。
现在当执行脚本时，可以看到文件删除已经执行。

```bash
$me@linuxbox ~$ deletion-script

preparing to delete files

deleting files

file deletion complete

me@linuxbox ~$
```

`bash` 还提供了另一种追踪方法，通过 `-x` 选项以及带有 `-x` 选项的 `set` 命令来实现。使用我们之前的故障脚本，可以通过在第一行添加 `-x` 选项来激活整个脚本的追踪。

```bash
#!/bin/bash -x
```

# trouble: 演示常见错误的脚本

`number=1`

```bash
if [ $number = 1 ]; then
  echo "Number is equal to 1"
else
    echo "Number is not equal to 1"
fi
```

执行时，结果如下所示：

```bash
me@linuxbox ~$ trouble
+ number=1
+'1 = 1 '
+ echo 'Number is equal to 1.'
Number is equal to 1.
```

通过追踪，我们看到了应用了扩展后执行的命令。开头的加号表示追踪显示，以便将其与普通输出行区分开。加号是追踪输出的默认字符。它包含在 `PS4`（提示符字符串 4） shell 变量中。可以调整此变量的内容来使提示符更有用。
我们修改了变量的内容，包含了执行追踪时脚本中的当前行号。注意，需要单引号来防止在提示符实际使用之前进行扩展。

```bash
me@linuxbox ~$ export PS4=$LINENO +
me@linuxbox ~$ trouble
5 + number=1
7 +'1 = 1 '
8 + echo 'Number is equal to 1.'
Number is equal to 1.
```

为了对脚本的选部分而不是整个脚本进行追踪，我们可以使用带有 `-x` 选项的 `set` 命令。

```bash
#!/bin/bash

# trouble: 演示常见错误的脚本

number=1

Troubleshooting 393
```

```bash
set -x # 开启追踪
if [ $number = 1 ]; then
  echo "Number is equal to 1"
else
  echo "Number is not equal to 1"
fi
set +x # 关闭追踪
```

我们使用带有 `-x` 选项的命令来激活追踪，使用 `+x` 选项来取消追踪。这种技术可以用于检查故障脚本的多个部分。

# 在执行期间检查值

在追踪的同时，显示变量的内容通常很有用，可以查看脚本在执行期间的内部机制。添加额外的 `echo` 语句通常可以解决问题。

```bash
#!/bin/bash

# trouble: 演示常见错误的脚本

number=1

echo "number=$number" # DEBUG
set -x # 开启追踪
if [ $number = 1 ]; then
  echo "Number is equal to 1"
else
  echo "Number is not equal to 1"
fi
set +x # 关闭追踪
```

在这个示例中，我们简单地显示了变量 `number` 的值，并用注释标记添加的行，以便日后识别和删除。这种技术在观察脚本中循环和算术的行为时特别有用。

## 总结

在本章中，我们查看了开发过程中可能出现的少数问题。当然，还有很多。这里描述的技术将使我们能够发现大多数常见错误。调试是一门艺术，通过经验既了解如何避免错误（在整个开发过程中不断测试）以及如何发现错误（有效使用追踪）来培养的。

# 31

# 流程控制： 使用 CASE 进行分支

![](img/0cf46e6370424e4fc9bc72ba090b1e02_426_0.png)

在本章中，我们将继续研究流程控制。在第 28 章中，我们构建了一些简单的菜单，并构建了用于处理用户选择的逻辑。为了实现这一点，我们使用了一系列 `if` 命令来识别选取了可能的选项中的哪一个。这种逻辑结构在程序中频繁出现——以至于许多编程语言（包括 shell）为多项选择决策提供了特殊的流程控制机制。

# case 命令

在 `bash` 中，多项选择复合命令称为 `case`。它具有以下语法：

```bash
case word in
  [pattern | pattern]...) commands ;;
esac
```

如果如果我们看第 28 章的 `read-menu` 程序，我们可以看到用于处理用户选择的逻辑。

```bash
#!/bin/bash

# read-menu: 一个菜单驱动的系统信息程序

clear

echo ""

echo "Please Select: "
```

- 1. 显示系统信息
- 2. 显示磁盘空间
- 3. 显示主目录空间利用
- 0. 退出

```bash
read -p "Enter selection [0-3] > " 
if [[ $REPLY = 1 ]]; then
  echo "Display System Information"
elif [[ $REPLY = 2 ]]; then
  echo "Display Disk Space"
elif [[ $REPLY = 3 ]]; then
  echo "Display Space Utilization"
elif [[ $REPLY = 0 ]]; then
  echo "Quit"
else
  echo "Invalid selection"
fi
```

使用 `case`，可以用更简单的方式替换这种逻辑。

```bash
#!/bin/bash

# case-menu: 一个菜单驱动的系统信息程序

clear

echo ""

echo "Please Select: "

1. Display System Information

2. Display Disk Space

3. Display Space Utilization

0. Quit

read -p "Enter selection [0-3] > "

case "$REPLY" in

  0)
    echo "Program terminated."
    exit
  1)
    echo "Display System Information"
    ;;
  2)
    echo "Display Disk Space"
    ;;
  3)
    echo "Display Space Utilization"
    ;;
  *)
    echo "Invalid entry" >&2
    exit 1
    ;;

esac
```
