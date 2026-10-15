
# float_divide.ksh Shell 脚本

## 主程序开始

列表 22.10 `float_divide.ksh` shell 脚本列表。（继续）

```bash
###### 设置陷阱 ######

trap exit_trap; exit 2

################################

# 检查是否至少有两个命令行参数
# 且不少于四个

if (($# < 2));
then
    echo "\ERROR: 命令行参数太少"
    usage
    exit 1
elif (($# > 4));
then
    echo "\ERROR: 命令行参数过多"
    usage
    exit 1
fi

# 解析命令行参数以查找精度值（如果存在）。

while getopts ":s:S:" ARGUMENT
do
    case $ARGUMENT in
        s|S) SCALE=$OPTARG
            ;;
        \?) # 因为有负数，我们需要
            # 测试以连字符 (-)开头的
            # ARGUMENT 是数字而不是无效的开关！！！
            for TST_ARG in "$@";
            do
                if [[ $(echo $TST_ARG | cut -c1) = '-' ]] ||
                && [ $TST_ARG != '-*' -a $TST_ARG != '-S*' ];
then
                    case $TST_ARG in
                        +([-0-9])*) : # 无操作，什么都不做
                            ;;
                        +([-0-9].*) : # 无操作，什么都不做
                            ;;
                        +([-0-9])) : # 无操作，什么都不做
                            ;;
                        *) echo "\ERROR: $TST_ARG 是无效参数\n"
                            usage
                    esac
                fi
            done
            ;;
    esac
done
```

**22.10** `float_divide.ksh` shell 脚本列表。（继续）

```bash
# 解析命令行并收集数字列表。

TOTAL_NUMBERS=0
while ((COUNT < MAX_COUNT))
do
  TOKEN=$1
  case $TOKEN in
    +([-0-9])*) # 无操作，什么都不做
      ;;
    +([-0-9].*) 
      TOTAL_NUMBERS=$((TOTAL_NUMBERS + 1))
      if ((TOTAL_NUMBERS == 1))
      then
        DIVIDEND=$TOKEN
      elif ((TOTAL_NUMBERS == 2))
      then
        DIVISOR=$TOKEN
      else
        echo "\ERROR: 数字过多"
        usage
        exit 1
      fi
      ;;
  NUM_LIST="$NUM_LIST $TOKEN"
  ((COUNT < MAX_COUNT)) && shift
esac
done
```

**22.10** `float_divide.ksh` shell 脚本列表。（继续）

```bash
# 通过我们在在本章之前涵盖的正则表达式
# 验证“数字”是否实际上是整数或
# 浮点数。

# 在列表 22.10 的 shell 脚本中我们省略了
# 构建数学语句的步骤。在这段代码脚本中没有必要
# 因为我们已经在列表 22.9 的代码段中获取了
# 被除数和除数。查看列表 22.10 中的
# shell 脚本并密切注意**粗体文本**。

```bash

# 浮点数运算与 bc 实用程序 579

esac

done

################################################

```bash
QUOTIENT=$(bc <<EOF
scale=$SCALE
$DIVIDEND / $DIVISOR
EOF
```

################################################

# 将除法结果显示给用户。

echo "\nt 结果：$DIVIDEND / $DIVISOR"

echo "\na 精度 $SCALE：$QUOTIENT"

```

**22.11** `float_divide.ksh` shell 脚本实例。

注意精度在除法脚本中有效！我们已经完成了加、减、乘、除所有运法的 shell 脚本。我想在下一部分展示另一种变体。

## 创建 float_average.ksh Shell 脚本

使用列表 22.1 中的加法 shell 脚本，我们可以进行一些微调并计算一系列数字的平均值。我不会显示整个 shell 脚本，只显示我对 `float_add.ksh` shell 脚本进行的修改，以计算该系列数字的平均值。

列表 22.1 的第一个新增是添加了变量 `TOTAL_NUMBERS`。为了计算一个数字列表的平均值，我们需要知道列表中有多少个数字，这样我们就可以将 `$NUM_LIST` 除以数字的总数。计数器在 `$NUM_LIST` 的合理性检查中添加，我们确保这些数字是整数或浮点数。此修改显示在列表 22.12。

**列表 22.12** 用于保持数字总和的代码段。

```bash
TOTAL_NUMBERS=0

for NUM in $NUM_LIST
do
  ((TOTAL_NUMBERS = TOTAL_NUMBERS + 1))
  case $NUM in
    +([0-9])) # 检查是否为整数
      # 无操作，什么都不做。
      ;;
    ++(-([0-9])) # 检查是否为负整数
      # 无操作，什么都不做。
      ;;
    +([-([0-9][.[0-9])) # 检查是否为正浮点数
      # 无操作，什么都不做。
      ;;
    +(-([0-9][.[0-9])) # 检查是否为带 + 前缀的正浮点数
      # 无操作，什么都不做。
      ;;
    +([-([0-9][.[0-9])) # 检查是否为负浮点数
      # 无操作，什么都不做。
      ;;
    +([-.([0-9])) # 检查是否为负浮点数（此处重复）
      # 无操作，什么都不做。
      ;;
    +([.+0-9])) # 检查是否为正浮点数
      # 无操作，什么都不做。
      ;;
    *) echo "\ERROR: $NUM_LIST 不是一个有效数字"
      exit 1
      ;;
  esac
done
```

**列表 22.12** 用于保持数字总和的代码段。（续）

```bash
;;
;;
esac
done
```

修改行在列表 22.12 中用粗体显示。唯一的修改是这里文档（here document），我们在其中添加了 `$ADD` 除以 `$TOTAL_NUMBERS` 的操作，以及向用户展示结果的代码。代码修改显示在列表 22.13 代码段中。

**列表 22.13** 计算平均值的代码段。

```bash
# 使用 bc 命令的这里文档进行数学运算

AVERAGE=$(bc <<EOF
scale=$SCALE
($ADD) / $TOTAL_NUMBERS
EOF
)

# 将结果显示给用户
echo "\n 的平均值为: $(echo $ADD | sed s+//+/g)"
echo "\nt 精度为 $SCALE 是 $AVERAGE\n"
```
