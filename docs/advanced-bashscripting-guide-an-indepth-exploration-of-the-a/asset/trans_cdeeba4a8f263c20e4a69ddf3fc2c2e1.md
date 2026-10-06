

## 高级 Bash 脚本指南

```bash
for i in [list] missing...
  do ==> 所以是对命令行参数进行操作
  case "$i" in
    0*) ibase=2; # 二进制
    0x*[a-f]*[A-F]*) ibase=16; # 十六进制
    ibase=8; # 八进制
    [1-9]*) ibase=10; # 十进制
    *)
      echo "illegal number $i - ignored"
      continue;
  esac

  # 前缀，将十六进制数字转换为大写 (bc 需要此)
  number=$(echo "$i" | sed -e 's:0x:[0-9a-fA-F]//' | tr '[a-f]' '[A-F]')
  # 使用 \ 作为分隔符，而不是 ""
  # 将数字转换为十进制
  dec=$(echo "ibase=$ibase;$number" | bc) # 计算器工具
  case "$dec" in
    [0-9]*) # 数字正常
      continue;
    *) ) # 错误：忽略
  esac

  # 在同一行打印所有转换结果。
  # == 'here document' 命令列表输入到 'bc'
  bc <<EOF
    obase=16; "hex": $dec
    obase=10; "dec": $dec
    obase=8; "oct": $dec
    obase=2; "bin": $dec
EOF | sed -e 's/"//g'
done

while [ $# -gt 0 ];
  do
    case "$1" in
      -\) shift; break;
      -h) Usage; ==> 帮助信息。
         Usage;
         break;
      *) ) # 第一个数字
    esac
    ==> 对非法输入进行错误检查将会很有用。
  shift
done

if [ $# -gt 0 ];
  then
    PrintBases "$@" # 从标准 读取
  else
    while read line
      do
        PrintBases $line
      done
  fi
```

一种使用嵌入在 [command substitution] 块中的 [here document] 来调用 bc 的替代方法。当脚本需要向 bc 传递一组选项和命令时，这种方法特别适用。

## 12.7. 终端控制命令

```bash
variable=`bc << LIMIT_STRING
options
statements
operations
LIMIT_STRING

...或者...

variable=$(bc << LIMIT_STRING
options
statements
operations
LIMIT_STRING
)
```

## 示例 12–32. 调用 bc 的另一种方法

```bash
#!/bin/bash
# 使用命令替换
# 结合 'here document' 来调用 'bc'

var1=$(bc << EOF
18.33 * 19.78
EOF)
echo $var1      # 362.56

# $(...) 记法同样有效。
v1=23.53
v2=17.881
v3=83.501
v4=171.63

var2=$(bc << EOF
scale = 4
a = ($v1 + $v2)
b = ($v3 + $v4)
a * b + 15.35
EOF)
echo $var2      # 593847.8452

var3=$(bc -1 << EOF
scale = 9
s ( 1.7 )
EOF)
# 返回 1.7 弧度的正弦值。
# "-1" 选项调用 'bc' 数学库。
echo $var3      # .991664810
```

## 现在，在函数中尝试一下...
```bash
hyp # 声明全局变量。
hypotenuse () # 计算直角角的斜边。
{
hyp=$(bc -1 << EOF
scale = 9
sqrt ( $1 * $1 + $2 * $2 )
EOF
# 遗憾的是，Bash 函数无法返回浮点数值。
)
hypotenuse 3.68 7.31
echo "hypotenuse = $hyp"      # 8.18403934

exit 0
```

在脚本中进行浮点数运算的另一种方法是在 shell 包装器中使用 awk 的内置数学函数。

## 示例 12–33. 计算三角形的斜边

```bash
#!/bin/bash
# hypotenuse.sh: 返回直角三角形的“斜边”。
# “直角边”平方的根

ARGS=2      # 脚本需要传递三角形的边。
E_BADARGS=65  # 参数数量错误。

if [ $# -ne "$ARGS" ]; then  # 测试脚本的参数数量。
then
    echo "Usage: $0 side_1 side_2"
    exit $E_BADARGS
fi

AWKSCRIPT='printf("%3.3f\n", sqrt($1 + $2*$2))' 
  # 传递给 awk 的参数
  command(s)

echo -n "Hypotenuse of $1 and $2 = "
echo $1 $2 | awk "$AWKSCRIPT"

exit 0
```

## 12.9. 杂命令

### 命令列表

这些工具输出整数序列

每个整数之间正常的分隔符是...

