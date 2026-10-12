
`SCRIPT_NAME=$(basename $0)`

`SCALE="0"` # 初始化精度值为零

`NUM_LIST=` # 初始化 `NUM_LIST` 为空

`COUNT=0` # 初始化计数器为零

`MAX_COUNT=$#` # 设置 `MAX_COUNT` 为命令行参数的总数

#################################################################
############ 函数 ############################
#################################################################

### 列表 13-10 `float_divide.ksh` shell 脚本

```ksh
function usage
{
echo "\n用途: 除两个数字\n"
echo "\用法: $SCRIPT_NAME [-s scale_value] N1 N2"
echo "\n如需无任何有效小数的整数结果..."
echo "\n示例: $SCRIPT_NAME 2048.221 65536 \n"
echo "或者若需 4 位有效小数"
echo "\n示例: $SCRIPT_NAME -s 2048.221 65536"
echo "\n\t...正在退出...\n"
}
```

```ksh
function exit_trap
{
echo "\n.正在在捕获到信号时退出...\n"
}
```

############################################################
###################### 主程序开始 #######################
############################################################
###### 设置陷阱 #######

`trap 'exit_trap; exit 2' 1 2 3 15`

# 检查至少有两个命令行参数 且不少于四个

```bash
if (($# < 2));
then
echo "\nERROR: 命令行参数太少"
    usage
    exit 1
elif (($# > 4));
then
echo "\n错误: 命令行参数过多"
    usage
    exit 1
fi
```

# 解析命令行参数以查找精度值（如果存在）。

```bash
while getopts ":s:S:" ARGUMENT
do
```

列表 13-10（续）

## 464 第二部分 面向程序员、测试人员和分析师的脚本

```bash
case $ARGUMENT in
  s) SCALE=$OPTARG ;;
  S) SCALE=$OPTARG ;;
esac
done
```

# 解析命令行参数并收集需要除数的数字列表。

`TOTAL_NUMBERS=0`

```bash
while ((COUNT < MAX_COUNT))
do
    ((COUNT = COUNT + 1))
    TOKEN=$1
    case -|S|) shift 2
      ((COUNT = COUNT + 1))
      ;;
      -s$(SCALE)) shift
      ;;
      -S$(SCALE)) shift
      ;;
      *) ((TOTAL_NUMBERS = TOTAL_NUMBERS + 1))
        if ((TOTAL_NUMBERS == 1))
        then
          DIVIDEND=$TOKEN
          elif ((TOTAL_NUMBERS == 2))
          then
            DIVISOR=$TOKEN
          else
            echo "ERROR: 除数数字过多"
            usage
            exit 1
        fi
        NUM_LIST=$NUM_LIST $TOKEN
        ((COUNT < MAX_COUNT)) && shift
    esac
done
```

# 确保精度为整数

```bash
case $SCALE in
    [0-9]*) ;;
    *) echo "\ERROR: 无效精度 - $SCALE - 必须是整数"
        usage
        exit 1
        ;;
esac
```

# 检查提供的每个数字以确保都是整数或浮点数。

```bash
for NUM in $NUM_LIST
do
    case $NUM in
        [0-9]*) # 检查正整数
            ;;
        -[0-9]*) # 检查负整数
            ;;
        [0-9]+\.[0-9]*) # 检查正浮点数
            ;;
        -[0-9]+\.[0-9]*) # 检查负浮点数
            ;;
        \.[0-9]*) # 检查领先的小数点
            ;;
        *) echo "\ERROR: $NUM 不是有效数字"
          usage
          exit 1
          ;;
    esac
done
```

# 使用此处文档（here document）向 `bc` 命令提供输入以执行数学运算。除法结果被赋值给 `QUOTIENT` 变量。

```bash
QUOTIENT=$(bc <<EOF
scale=$SCALE
$DIVIDEND / $DIVISOR
EOF)
```

# 将除法结果展示给用户。

```bash
echo "\nt $DIVIDEND / $DIVISOR"
echo "\n精度 $SCALE 的结果为 ($QUOTIENT)\n"
```

# 第13章 浮点数数学与 bc 工具 467

替换使用带有标签的双重重定向（`<<EOF`），它定义了在此文档（here document）的开始，用于设置浮点数的精度（`scale`）并对数字进行除法。如果命令行上没有给出 `scale`，则 `scale` 为 0，表示整数值。在此文档以最后的标签（`EOF`）结束，从而结束文档并退出 `bc` 工具，`bc` 是一个交互式程序。最后一步是将结果呈现给用户。在列表 13-11 中，你可以看到 `float_divide.ksh` 脚本的运行。

```
[root:yogi|]/scripts# float_divide.ksh -s 6 .3321 -332.889

.3321 / -332.889 的商为：

精度为 6 的结果是 .000997
```

**列表 13-11** `float_divide.ksh` 脚本运行示例

注意，`scale` 在脚本中生效了，因为我们在除法从未未使用过超过 6 位有效数字的浮点数，因此我们从未覆盖过 `scale` 值。我们已经完成了加、减、乘、除 shell 脚本。我想在下一节中介绍一种变体。

## 创建 `float average.ksh` Shell 脚本

使用列表 13-1 中的加法脚本，我们可以进行一些微小的修改并计算一系列数字的平均值。

列表 13-1 的第一个修改是添加了变量 `TOTAL_NUMBERS`。为了计算一组数字的平均值，我们需要知道列表中有多少个数字，以便我们可以将 `SUM` 除以数字的总数。计数器在 `$NUM_LIST` 数字的合理性检查中添加，在那里我们确保数字要么是整数或者是浮点数。这种修改在列表 13-12 中。

```
TOTAL_NUMBERS=0

for NUM in $NUM_LIST
do
  ((TOTAL_NUMBERS = TOTAL_NUMBERS + 1))
  case $NUM in
    ([0-9])) # 检查是否为整数
      : # 无操作，什么都不做。
      ;
    +-([0-9])) # 检查是否为负整数
      : # 无操作，什么都不做
      ;
    +([0-9][.[0-9]))
      : # 检查是否为正浮点数
```

**列表 13-12** 保持数字运行总的代码段
