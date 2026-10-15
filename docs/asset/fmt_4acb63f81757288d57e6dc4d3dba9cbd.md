
```text
| Apple Computer | AAPL | 500 |
| Cable & Wireless | CWP | 100 |
| Intel | INTC | 300 |
| Jupiter Media | JUPM | 50 |
| eBay | EBAY | 200 |
| Microsoft | MSFT | 200 |
| Qualcomm | QCOM | 100 |
```

# 结果

```text
$ portfolio
Apple Computer 交易价格为 22.61（你的 500 股 = 11305.00）
Cable & Wireless 交易价格为 5.63（你的 100 股 = 563.00）
Intel 交易价格为 28.59（你的 300 股 = 8577.00）
Jupiter Media 交易价格为 3.95（你的 50 股 = 197.50）
eBay 交易价格为 55.41（你的 200 股 = 11082.00）
Microsoft 交易价格为 26.52（你的 200 股 = 5304.00）
Qualcomm 交易价格为 41.33（你的 100 股 = 4133.00）
投资组合总价值：41161.50
```

# 改进脚本

显而易见的改进区域将支持海外交易所持仓、允许通过指定通用股票名称动态查找股票代码，以及——如果你是一个能够忍受偶尔损失的真实玩家——在组合文件中将每只股票的原始购买价格作为第四个字段，然后不仅计算当前的投资组合总值，还计算组合中每只股票与其原始购买价格之间的价值差异。

# #68 追踪网页上的变化

有时，伟大的灵感来自于看到一个现有的业务并对自己说：“这似乎并不难。”追踪网站变化的任务是收集此类灵感材料的一种非常简单的方法，正如 `changetrack` 脚本所示。该脚本包含一个有趣的细节：当它检测到网站发生变化时，它会将新网页发送电子邮件，而不是仅仅在命令行中报告。

## 代码

```sh
#!/bin/sh

# changetrack - 跟踪给定的 URL，如果自上次访问以来
# 有变化，则将新页面发送到指定的地址。

sitearchive="/usr/tmp/changrack"      # 根据需要更改
sendmail="/usr/bin/sendmail"          # 可能需要调整！
fromaddr="webscraper@intuitive.com"   # 根据需要更改

if [ $# -ne 2 ]; then
    echo "Usage: $(basename $0) url email" >&2
    exit 1
fi

if [ ! -d $sitearchive ]; then
    if ! mkdir $sitearchive; then
        echo "$(basename $0) failed: couldn't create $sitearchive." >&2
        exit 1
    fi
    chmod 777 $sitearchive              # 你可能为了隐私更改此项
fi

if [ "$(echo $1 | cut -c1-5)\ != "http:" ]; then
    echo "Please use fully qualified URLs (e.g., http://)" >&2
    exit 1
fi

fname="$(echo $1 | sed 's|^/\\///|g' | tr '/?&' '...')"
baseurl="$(echo $1 | cut -d '-' -f3)"

# 将网页副本获取到存档文件中。注意，
# 我们通过查看内容来跟踪变化（例如使用 '-dump' 而不是
# '-source'），因此我们可以跳过任何 HTML 解析
lynx -dump $1 | uniq > $sitearchive/$(fname).new

if [ -f $sitearchive/$fname ]; then
    # 我们以前见过这个网站，所以用 'diff' 比较两者
    diff $sitearchive/$fname $sitearchive/$(fname).new > /dev/null ; then
echo "Site $1 has changed since our last check."
else
rm -f $sitearchive/$(fname).new # 没有新内容...
  # 没有变化，我们就离开
fi
echo "Note: we've never seen this site before."
```

为了脚本执行到这里，网站必须发生了变化，我们需要将 `.new` 文件的内容发送给用户，并用 `.new` 替换原始文件以供脚本调用。

```sh
( echo Content-type: text/html
echo "From: fromaddr (Web Site Tracker)"
echo "Subject: Web Site $1 Has Changed"
echo "To: $z"
echo "
"
lynx -source $1 | \
sed -e"[sS][h][rR][cC]=\|SRC=\\$baseurl|g" \
sed -e"[sS][h][rR][cC][eE]=[ff]=\|HREF=\\$baseurl|g" \
sed -e"$baseurl|http:|g"
```

一旦通过 `eval` 进行评估，`name`、`ticker` 和 `hold` 这三个变量将实际上根据指定的值进行实例化。脚本的其余部分就可以通过名称引用这些值，而无需任何额外的调整。

# 运行脚本

`getstock` 脚本的设计意图不是直接运行，给定一个股票代码，它将返回当前的交易价格。`portfolio` 脚本需要一个单独的数据文件，其中包含名称、股票代码和持有的股数。以下是该文件可能格式的示例：

```text
$ cat /.portfolio

# 格式为公司名，股票代码，持股量
```
