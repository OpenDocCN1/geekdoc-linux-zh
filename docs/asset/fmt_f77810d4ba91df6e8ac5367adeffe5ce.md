
- 1. 这是一个关于算术扩展的练习。

```bash
printf "Enter cm: ""      # 提示
read CM                        # 读取厘米数
FEETS=$(( $CM / 30 ))          # FEET 易于计算
CM=$(( $CM % 30 ))             # 将 CM 替换为剩余的厘米
                               # 上述英尺之后
INCHES=$(( $CM * 12 / 30 ))   # 将剩余厘米
                               # 转换为英寸
```

```
printf "%d cm is %d foot %d inches\n" $CM $FEET $INCHES
```

这个练习要求在开始使用 `test` 命令对作为脚本参数传递的文件名进行检查，随后使用多种 UNIX 工具。

```bash
# 检查参数数量
if [ $# -ne 1 ];
then
    echo "Requires one argument"
    exit 1

# 如果只有一个参数，检查其是否可读
elif [ ! -r $1 ];
then
    echo "File is unreachable"
    exit 1
```

```bash
LINES=0             # 计数行数
COLS=0                          # 计数字符数
while read LINE                # read 在输入结束时返回 false
done
```

## 选问题的答案

```
# 行的字符数（包括换行符）
COLONLINE=$( echo "$LINE" | wc -c )
# 加到 COL 并减去 1 个换行符

COL=$(( $COL + $COLONLINE - 1 ))
# 增加行数
LINES=$(( $LINES + 1 ))
done <<<1 # 从文件输入
```

```
# 因为需要 2 位小数，必须使用 bc 来
# 计算平均值，而不是算术扩展
AVERAGE=$( echo "scale=2"; $COL / $LINES" | bc )
```

```
# 最后，显示平均值
printf "Average is %s\n" $AVERAGE
```

- 5 用于显示小时，然后对输出进行模式匹配：

```bash
# 格式 %H 给出的小时为 2 位数，00-23
case $( date "+\%H" ) in

# 任何 00 到 09 小，也包括 10 或 11
0?|1[0-1]) echo Good Morning;

# 任何 12 到 17 小
1[2-7]) echo Good afternoon;

# 其他任何时间都是晚上
*) echo Good evening;
esac
```

- 7 这个解决方案涉及一个中等复杂的 `while` 循环。

```bash
# 检查参数数量
if [ $# -ne 1 ]
then echo "Requires 1 argument"
exit 1
```

```bash
# 检查参数是否在 1 到 15 之间
case $1 in
[1-9]|1[0-5]) ;;
**) echo "Require number 1-15"
exit 1
esac
```

```bash
LINE=1 # 用于遍历行
while [ $LINE -le $1 ]
```

## 介绍 UNIX 和 Linux

```bash
do
# 处理正方形的第一行和最后一行
if [ $LINE -eq 1 ] || [ $LINE -eq $1 ]
    then printf "+"      # 第一列
    COL=2                      # 下一个打印的列
    while [ $COL -lt $1 ]
        do printf "-"
        COL=$(( $COL + 1))
        done
    printf "\n"      # 最后一列
# 中间行
    else printf "|"      # 第一列
    COL=2                      # 下一个打印的列
    while [ $COL -lt $1 ]
        do printf " "
        COL=$(( $COL + 1))
        done
    printf "\n"      # 最后一列
fi
LINE=$(( $LINE + 1 ))
done
```

这可以使用对参数进行模式匹配来解决，但由于带选项运行 `eurhello` 有许多可能，解决此问题的清晰方法是使用 `getopts`。

## 设置字符串 GREETING 为常用的问候

`GREETING="Hello"`

```bash
# 使用 getopts 遍历所有可能的选项
# 这些可以是 f 或 g，或者 G 后面跟一个参数
# 遇到选项时，将其存储在 OPTIONNAME 中
while getopts fgG: OPTIONNAME

    # 检查三种可能性
    case "$OPTIONNAME" in
        # 法语
        f) GREETING="Bonjour";
        # 德语
        g) GREETING="Guten Tag";
        # -G 的参数存储在 OPTARG 中
        G) GREETING="$OPTARG";
    esac
done
```

## 如果带有无效选项调用脚本

```bash
# getops 将丢弃它们并显示错误
message
# 现在移除已处理的选项
shift $((OPTIND - 1))

# 检查名称字符串是否为脚本的参数
if [ $# -eq 0 ]; then
    echo "usage: $0 [-f] [-g] name"
    exit 1
fi

# 最后，产生输出
echo "$GREETING"
```

## 第 9 章

- 1. 这是一个简单的函数，只需要在大括号之间编写两个命令。

```bash
thisyear() {
    printf "This year is "
    date "+%Y"
}
```

或者，这可以使用 `echo` 实现：

```bash
thisyear() {
    echo "This year is $(date +%Y)"
}
```

注意，`date` 的参数不需要在引号内，因为在这种情况下它不包含特殊字符。在第一个解决方案中，为了清晰起见包含了它们，在第二个中省略了它们以避免与引号冲突。

- 3. 这个函数的体与将其写成脚本一样。它必须写成函数，以便可以更改当前 shell 中 `PATH` 的值——无法从子进程导出到父进程。

## 介绍 UNIX 和 Linux

```
cost = 100 + 5*$3
revenue = $3*$4*rate[$5]
profit = revenue - cost
printf("%d/%d %s-%s: ", $6, $7, $1, $2)
if (profit > 0)
    printf("profit %.2f\n")
else
    printf("loss %.2f\n", -profit)
```

## 第 12 章

对于 Aw 的解决方案，针对 Perl 问题还有许多其他可能的解决方案

- 2 `$available_chars=72;`

`$output_line="";`

`while (<STDIN>) {`

```perl
# 删除换行符
chomp()

# 移除前面的空格
$_ = s/^[ ]*//;

# 移除末的空格
$_ = s/[ ]*$//;

# 为输入行中的单词创建一个数组
@words=split;

# 逐个循环单词...
for ($i=0; $i<=#words; $i++) {
    $word = $words[$i];

    # 如果它无法放入输出行中...
    if (length($word) >= $available_chars) {

        # 打印当前输出行
        print $output_line " \n";
        # ... 重置变量
        $available_chars=72 - length($word);
        $output_line=$word;
    }
```

```perl
# 将单词添加到输出行（不要忘记
# 空格）并重置存储
# 可空间的变量
$available_chars = $available_chars - length($word) - 1;
$output_line = $output_line . " " . $word;
}
print $output_line . "\n";
```

- 3
