
FIRST=$(convert_base_10_to_16 $a)

SECOND=$(convert_base_10_to_16 $b)

THIRD=$(convert_base_10_to_16 $c)

FOURTH=$(convert_base_10_to_16 $d)

这四个函数调用的结果是将十六进制值赋值给四个新变量：`FIRST`、`SECOND`、`THIRD` 和 `FOURTH`。现在我们已经有了十进制值，我们需要做的就是将十六进制字符串组合成单个字符串。组合方式所示：

```bash
echo "$(FIRST) $(SECOND) $(THIRD) $(FOURTH)"
```

我为了临时使用的从空获取的 IP 地址（`163.155.204.42`）生成的输出如下：

```bash
[root:yogi]@scripts# ./mk_swkey.ksh
a39bcc2a
```

这个十六进制字符串就是绑定到 IP 地址的软件许可证。

## 在任意数字进制之间转换的脚本

到目前为止，我们一直在一个受限的环境中工作，切换数字进制的能力有限。此脚本将在系统限制范围内将任何数字转换为任意数字进制。进制转换的可用性至少为 36，某些系统可能会更高。我不确定你会用 36 进制的数字做什么，但如果你想的话，可以创建一个。

在这里，我们依赖于两个命令行开关，每个开关都需要一个参数。此脚本将转换任何数字。进制转换的可用性至少为 36，某些系统可能会更高。我不确定你会用 36 进制的数字做什么，但如果你想的话，可以创建一个。

# 第23章

```bash
are not NULL.

if [ -z "$START_BASE" ] || [ "$START_BASE" = '' ] || \
  [ -z "$END_BASE" = '' ]
then
  echo "\nERROR: Base number conversion fields are empty\n"
  usage
  exit 1
fi
```

确保 `START_BASE` 和 `END_BASE` 变量具有整数值，用于数字进制转换。

```bash
case $START_BASE in
+([0-9])) : # 什么都不做 - 冒号是空操作。
  ;
n*) echo "\nERROR: $START_BASE is not an integer value"
    usage
    exit 1
  ;
esac
```

```bash
case $END_BASE in
+([0-9])) : # 什么都不做 - 冒号是空操作。
  ;
n*) echo "\nERROR: $END_BASE is not an integer value"
    usage
    exit 1
  ;
esac
```

## 主程序开始

从要转换的 `BASE_NUM` 的 1 开始。从 1 计数到命令行参数的最大个数。

```bash
while ((COUNT < MAX_COUNT))
do
  ((COUNT=COUNT + 1))
  case $TOKEN in
    -f) shift; shift
      ((COUNT = COUNT + 1))
      ;
    -f$(START_BASE)) shift
      ;
    -t) shift; shift
      ((COUNT = COUNT + 1))
      ;
    -t$(END_BASE)) shift
      ;
    *) BASE_NUM=$TOKEN
      break
      ;
  esac
done

# 定义 RESULT 变量为目标数字进制
typeset -i$END_BASE RESULT

# 将 BASE_NUM 变量赋值给 RESULT 变量
# 并加上起始数字 (START_BASE)，带有正号 (#) 
# 作为前缀，以便进行转换。
# 注意：如果输入了无效数字，系统将显示
# 错误。例如输入 1114400 作为
# 二进制数，这对于二进制数来说是非法的。

RESULT=$(START_BASE)#$(BASE_NUM)

# 将结果显示给用户或调用程序。
echo "$RESULT"

脚本结束...
```

**列表 23.4** `equate_any_base.ksh` 脚本列表。

请继续关注我！列表 23.4 并没有看起来那么困难。因为我们要求用户提供命令行参数，所以我们需要进行大量的测试，以确保我们有良好的数据可以处理。如果检测到用法错误，我们还需要给用户提供良好且信息丰富的反馈。记住，始终让用户知道正在发生什么。保持用户知情就是良好的脚本！

让我们从 `equate_any_base.ksh` 脚本的顶部开始，逐步分析细节。我们做的第一件事是定义三个变量：`$SCRIPT_NAME` 变量指向此脚本的名称。我们需要查询系统获取，原因有两个：首先，脚本的名称在未来可能会改变；其次，`SCRIPT_NAME` 变量被用于 `usage` 函数。如果我们在 `usage` 函数内部执行 `basename $0` 命令，我们将得到函数的名称而不是 shell 脚本的名称。这是一个需要说明的重要点。我们需要知道在引用位置参数时作用域在哪里。

当我们在 shell 脚本的主体内引用位置参数时，位置参数是命令行参数，包括 shell 脚本的名称。当我们在函数内部引用位置参数时，位置参数的作用域是提供给函数的参数，而不是 shell 脚本。在任何情况下，都可以通过 `basename` 引用 shell 脚本或函数的名称。

下一个变量定义 `COUNT=0` 和 `MAX_COUNT=$#` 用于解析每一个 shell 命令行参数，其中 `$#` 代表 shell 脚本的命令行参数总数。我们稍后将对这些变量进行更详细的说明。

在下一节中，我们将定义此脚本所需的任何函数。对于此脚本，我们需要一个 `usage` 函数。如果你查看该 `usage` 函数，你会看到关于如何使用该 shell 脚本的大量信息，紧随其后的是 USAGE 语句。在 23.4 中，我们提供了一个使用该 shell 脚本的示例。这对于不熟悉运行脚本的用户来说非常有帮助。

如之前所述的，我们需要进行大量的检查，因为我们依赖用户提供命令行参数来获取执行行为。我们将进行七项独立测试，以确保我们接收到的数据是可以处理的良好数据。

前两个测试是确保我们有正确的命令行参数数量。对于 `equate_base.ksh` 脚本，用户提供的参数最少三个，最多五个。这种变化可能有点奇怪，但使用 `getopts` 命令，它将变得直观易见。为了测试参数数量，我们使用 if-then-elif-fi 结构，通过测试 `$#` 参数来确保值不大于五且小于三，所示：

```bash
if (($# > 5))
then
    echo "\nERROR: 命令行参数过多"
    usage
elif (($# < 3))
then
    echo "\nERROR: 命令行参数过少"
    usage
    exit 1
fi
```

## 使用 getopts 解析命令行参数

当我们在 shell 脚本的主体内引用位置参数时，位置参数是命令行参数，包括 shell 脚本的名称。当我们在函数内部引用位置参数时，位置参数的作用域是提供给函数的参数，而不是 shell 脚本。在任何情况下，都可以通过 `basename` 引用 shell 脚本或函数的名称。

下一个变量定义 `COUNT=0` 和 `MAX_COUNT=$#` 用于解析每一个 shell 命令行参数，其中 `$#` 代表 shell 脚本的命令行参数总数。我们稍后将对这些变量进行更详细的说明。

在下一节中，我们将定义此脚本所需的任何函数。对于此脚本，我们需要一个 `usage` 函数。如果你查看该 `usage` 函数，你会看到关于如何使用该 shell 脚本的大量信息，紧随其后的是 USAGE 语句。在 23.4 中，我们提供了一个使用该 shell 脚本的示例。这对于不熟悉运行脚本的用户来说非常有帮助。

## 正确用法 equate_any_base.ksh

## 错误用法 equate_any_base.ksh

```bash
root@user:~ ./equate_any_base.ksh
```
