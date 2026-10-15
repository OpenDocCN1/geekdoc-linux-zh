
# 工作原理

此脚本根据命令行参数是电影名称还是 IMDb 电影 ID 构建不同的 URL，然后将 `lynx` 从网页的输出保存到 `$tempout` 文件。

如果命令行参数是电影名称，脚本将检查 `$tempout` 中的字符串 `"IMDb title search"`，以查看文件是否包含电影名称列表（当有多个电影匹配搜索标准时）或单部电影的描述。使用一系列依赖于源结构的复杂 `sed` 替换操作。

# 运行脚本

命令行参数是电影名称，脚本将检查 `$tempout` 中的字符串 `"IMDb title search"`，以查看文件是否包含电影名称列表（当有多个电影匹配搜索标准时）或单部电影的描述。使用一系列依赖于源结构的复杂 `sed` 替换操作。

# 结果

命令行参数是电影名称，脚本将检查 `$tempout` 中的字符串 `"IMDb title search"`，以查看文件是否包含电影名称列表（当有多个电影匹配搜索标准时）或单部电影的描述。使用一系列依赖于源结构的复杂 `sed` 替换操作。

## 计算值

命令行参数是电影名称，脚本将检查 `$tempout` 中的字符串 `"IMDb title search"`，以查看文件是否包含电影名称列表（当有多个电影匹配搜索标准时）或单部电影的描述。使用一系列依赖于源结构的复杂 `sed` 替换操作。

# 多版本的 bc，其中 1 != 0.9999999999999

```bash
useuro="$(scriptbc 1 / euro) + 0.000000001"
cuscand="$(scriptbc 1 / canada) + 0.000000001"
ususyen="$(scriptbc 1 / japan) + 0.000000001"
uspound="$(scriptbc 1 / uk) + 0.000000001"
```

```bash
if [ $ -ne 2 ]; then
  echo "Usage: $(basename $0) amount currency"
  echo "where currency is USD, Euro, Canadian, Yen, or Pound."
  exit 0
fi
```

```bash
amount=$1
currency="$(echo $2 | tr '[:upper:]' '[:lower:]' | cut -c1-2)"
case $currency in
us ) if [ -z "$(echo $1 | grep '\.'" ]; then
    masterrate="$1.00"
  else
    masterrate="$1"
  fi
  eu ) masterrate="$(scriptbc 1 \* \$euro)"
  ;;
  ca(d) masterrate="$(scriptbc 1 \* \$canada)"
  ;;
  yye ) masterrate="$(scriptbc 1 \* \$japan)"
  ;;
  pos(t) masterrate="$(scriptbc 1 \* \$uk)"
  ;;
  *) echo "$0: unknown currency specified."
  echo "I only know USD, EURO, CAN/CDN, YEN and GBP/POUND."
  exit 1
esac
```

```bash
echo "Currency Exchange Rate Equivalents for ${2}:"
showrate \$masterrate
echo "US Dollars: \$rate"
showrate \$(scriptbc \$masterrate \* \$euro)
echo "EC Euros: \$rate"
showrate \$(scriptbc \$masterrate \* \$uscand)
echo "Canadian Dollars: \$rate"
showrate \$(scriptbc \$masterrate \* \$usyen)
echo "Japanese Yen: \$rate"
showrate \$(scriptbc \$masterrate \* \$uspound)
echo "British Pounds: \$rate"
```

```bash
exit 0
```

# 工作原理

运行时，如果交换汇率数据库 `.exchangerate` 期时间超过 12 小时，第一个脚本 `getexchange` 将从 CNN 网站获取最新的交换汇率信息，提取脚本中指定的各种货币的汇率，然后将其以 `货币=数值` 的格式保存。以下是脚本运行后 `.exchangerate` 文件的内容：

```
$ cat /tmp/.exchangerate
cada=0.747100
euro=1.173303
japan=0.009163
uk=1.664400
```

第二个脚本 `exexchange` 相当长，并且所有的数学计算都依赖于第 9 号脚本 `scriptbc`。该脚本的基本算法是：通过通过相应的汇率满足命令行参数中指定的货币值，将其归一化为美元，然后利用美元与每种外币之间的关系来计算每种货币的等值金额。

从技术角度来看，请特别注意 `exexchange` 如何从 `.exchangerate` 数据文件中引入汇率值：

- `$exchranefile`

这被称为“源文件”（sourcing a file），它会导致指定的文件（脚本）被读取，就像其内容是此脚本的一部分一样。与下面行的结果进行对比，会更容易理解：

```
sh $exchranefile
```

这样做完全是反反的：它启动了一个子壳（subshell），在子壳中设置了汇率变量，然后退出子壳，导致调用脚本无法访问这些变量的值。

# 运行脚本

这对脚本是典型的 Unix 高级交互：`getexchange` 是“管理员”脚本，负责执行必要的后台工作以确保汇率正确且最新；而 `exchange` 是“用户”脚本，它具备所有完备的功能特性，但完全不接触互联网。

尽管 `getexchange` 脚本可以根据需要频繁运行，但实际上只有在 `$exchranefile` 超过 24 小时时才会获取并更新货币汇率（等一下，让我重读一遍：实际上只有在 `$exchranefile` 超过 12 小时时才会获取并更新）。这适合作为每日的 cron 任务（定时任务），可能只需要在工作日运行（货币市场周末不开放，因此汇率从周五晚上到周一早上不会发生波动）。

`exchangerate` 脚本需要两个参数：货币金额和货币名称。它在这方面非常灵活，因此 100 CDN 和 100 Canadian 是相同的，而 25 EU 和 25 Euros 也可以用。如果没有指定货币名称，默认是 USD（美元）。

# 结果

- `$ getexchrate`
成功。汇率已于 2003 年 10 月 9 日周四 23:07:27 MDT 更新。

`$ exchange 250 yen`
250 日元的等值金额为：
美元: 2.29
欧洲欧元: 1.95
加加元: 3.06
日元: 250.00
英镑: 1.33

`$ exchange 250 yen`
250 日元的等值金额：
美元: 2.29
欧洲欧元: 1.95
加加元: 3.06
日元: 250.00
英镑: 1.33

`getstock` 脚本是本章中最简单的脚本之一。它模拟对 CNN Finance 的查询，通过查找网页中指示“Last Price:”的行并提取后续价格来获取指定股票的值。

`portfolio` 脚本计算组合中所有股票的价值，使用存储在组合数据文件中的信息，该文件采用简单的文本格式，包含股票名称、代码和股数。为了方便解析，数据文件使用 `|` 字符分隔（该字符不会出现在公司名称中）。脚本提取字段的值，通过调用 `getstock` 计算每只股票的价值，并乘以股数以确定该股票的总价值。将它们相加即可得到组合总价值。

一旦通过 `eval` 进行评估，`name`、`ticker` 和 `hold` 这三个变量将实际上根据指定的值进行实例化。脚本的其余部分就可以通过名称引用这些值，而无需任何额外的调整。

# 运行脚本

`getstock` 脚本的设计意图不是直接运行，给定一个股票代码，它将返回当前的交易价格。`portfolio` 脚本需要一个单独的数据文件，其中包含名称、股票代码和持有的股数。以下是该文件可能格式的示例：

```
$ cat /.portfolio
# 格式为公司名，股票代码，持股量
```
