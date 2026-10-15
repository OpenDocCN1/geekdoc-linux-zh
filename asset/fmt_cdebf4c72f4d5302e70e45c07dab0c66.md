
```bash
#!/bin/bash

# convertatemp--Temperature conversion script that lets the user enter
# a temperature in Fahrenheit, Celsius, or Kelvin and receive the
# equivalent temperature in the other two units as the output

if [ $# -eq 0 ]; then
    cat << EOF >&2
Usage: $0 temperature[F|C|K]
where the suffix:
    F  indicates input is in Fahrenheit (default)
    C  indicates input is in Celsius
    K  indicates input is in Kelvin
EOF
    exit 1
fi

unit="$(echo $1 | sed -e 's/-*[[:digit:]]//g' | tr '[:lower:]' '[:upper:]')"
temp="$(echo $1 | sed -e 's/[^[:digit:]]//g')"

case ${unit:-F} in
F) # Fahrenheit to Celsius formula: Tc = (F - 32) / 1.8
    fahr="$temp"
    cels="$(echo "scale=2;($fahr - 32) / 1.8" | bc)"
    kelv="$(echo "scale=2;$cels + 273.15" | bc)"
    ;;
C) # Celsius to Fahrenheit formula: Tf = (9/5)*Tc+32
    cels=$temp
    kelv="$(echo "scale=2;$cels + 273.15" | bc)"
    fahr="$(echo "scale=2;(1.8 * $cels) + 32" | bc)"
    ;;
K) # Celsius = Kelvin - 273.15, then use Celsius -> Fahrenheit formula
    kelv=$temp
    cels="$(echo "scale=2; $kelv - 273.15" | bc)"
    fahr="$(echo "scale=2; (1.8 * $cels) + 32" | bc)"
    ;;
*)
    echo "Given temperature unit is not supported"
    exit 1
    ;;
esac

echo "Fahrenheit = $fahr"
echo "Celsius     = $cels"
echo "Kelvin      = $kelv"

exit 0
```

*Listing 3-8: The convertatemp shell script*

### 如何工作

在本书的这个阶段，脚本的大部分内容可能已经很清楚了，但让我们更仔细地看看完成所有工作的数学和正则表达式。“先讲数学”，大多数学龄儿童肯定不会喜欢听到！以下是将华氏度转换为摄氏度的公式：

C = (F - 32) / 1.8

将其转换为可以输入 `bc` 并求解的序列，看起来像代码中的 ①。反向转换，摄氏度到华氏度，在 ① 处。脚本还将温度从摄氏度转换为开尔文 ②。该脚本展示了使用助记符变量名的一个重要原因：它使代码更容易阅读和调试。

这里其他有趣的代码部分是正则表达式，其中最复杂的是 ①。我们做的事情相当直接，如果你能解开 `sed` 替换的话。替换总是看起来像 `s/old/new/`；这里的旧模式是零个或多个 `-`，后跟数字集合中的任意一个（回想一下 `[:digit:]` 是 ANSI 字符集表示法，表示任何数字，`*` 匹配前一个模式的零个或多个出现）。新的模式是我们想要用它替换旧模式的内容，在本例中它只是 `/`，表示空模式；当你只想删除旧模式时，这个模式很有用。这种替换有效地删除了所有数字，因此像 `-31F` 这样的输入就变成了只是 `F`，给出了单位类型。最后，`tr` 命令将所有内容规范化为大写，因此例如 `-31f` 变成了 `F`。

另一个 `sed` 表达式则相反：它通过使用“`^`”运算符来否定 `[:digit:]` 类中的任何字符，从而删除所有非数字字符。（大多数语言使用 `!` 作为否定。）这为我们提供了最终使用适当方程转换的值。

### 运行脚本

此脚本具有简洁直观的输入格式，即使对于 Unix 命令来说相当不寻常。输入以数值形式输入，可选后缀表示输入温度的单位；当未给出后缀时，代码假定单位为华氏度。

要查看 0° 华氏度的摄氏度和开尔文等效值，请输入 `0F`。要查看 100° 开尔文在华氏度和摄氏度中的数值，请使用 `100K`。要将 100° 摄氏度转换为开尔文和华氏度，请输入 `100C`。

你将在第 190 页的脚本 #60 中再次看到这种单字母后缀方法，该脚本转换货币值。

### 结果

第 3-9 节显示了跨多个不同温度的转换。

```text
$ convertatemp 212
Fahrenheit = 212
Celsius     = 100.00
Kelvin      = 373.15
$ convertatemp 100C
Fahrenheit = 212.00
Celsius     = 100
Kelvin      = 373.15
$ convertatemp 100K
Fahrenheit = -279.67
Celsius     = -173.15
Kelvin      = 100
```

*Listing 3-9: Testing the convertatemp shell script with a few conversions*

### Hacking the Script

你可以添加一些输入标志来生成简洁的输出，每次只进行一种转换。例如，`convertatemp -c 100F` 就可以只输出 100° 华氏度的摄氏度等效值。这种方法也有助于你在其他脚本中使用转换后的值。

## 25 计算贷款付款

用户可能处理的另一个常见计算是贷款付款的估算。第 3-10 节中的脚本也有助于回答“用那笔奖金能做什么？”这个问题，以及相关问题“终于能买得起那辆新特斯拉了吗？”

虽然根据贷款本金、利率和期限计算还款额的公式有点棘手，但合理地使用 shell 变量就能驯服这个数学难题，让它变得出人意料地易于理解。

## The Code

```
#!/bin/bash

# loancalc--Given a principal loan amount, interest rate, and
#   duration of loan (years), calculates the per-payment amount

# Formula is M = P * ( J / (1 - (1 + J) ^ -N)),
# where P = principal, J = monthly interest rate, N = duration (months).

# Users typically enter P, I (annual interest rate), and L (length, years).

. library.sh      # Start by sourcing the script library.

if [ $# -ne 3 ] ; then
  echo "Usage: $0 principal interest loan-duration-years" >&2
  exit 1
fi

P=$1 I=$2 L=$3
J="$(scriptbc -p 8 $I / \( 12 * 100 \ ))"
N="$(($L * 12 ))"
M="$(($L * 12 ))"
M="$(scriptbc -p 8 $P * \( $J / \(1 - \(1 + $J\) ^ -$N\) \ ))"

# Now a little prettifying up of the value:

dollars="$(echo $M | cut -d. -f1)"
cents="$(echo $M | cut -d. -f2 | cut -c1-2)"

cat << EOF
A $L-year loan at $I% interest with a principal amount of $(nicenumber $P 1 )
results in a payment of $$dollars.$cents each month for the duration of
the loan ($N payments).
EOF

exit 0
```

Listing 3-10: The loancalc shell script

## How It Works

深入探讨公式本身超出了本书的范围，但值得注意的是，一个复杂的数学公式如何可以直接在 shell 脚本中实现。
