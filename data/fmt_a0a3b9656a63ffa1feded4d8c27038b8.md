
每当我们探索 ImageMagick 时，都会发现有另一个参数和另一种利用其功能的方法。在这种情况下，你可以使用 ① 处的 `-format` 参数从与图像相关的 EXIF 信息中仅提取特定的匹配参数。

注意，我们使用 PSL 作为 `grep` 搜索的模式，而不是 GPS。这样我们就不需要挑选报告的额外 GPS 相关信息。尝试移除 `l` 看看会打印出多少其他 EXIF 数据！

之后，就是提取特定的信息字段并使用 `bc` 求解数学方程将数据转换为有意义的格式，如 ② 处的 `latdeg` 行所示。

到此为止，你对多次使用 `cut` 的管道应该应该很熟悉了。这些是超级实用的脚本工具！

一旦所有数据和所有方程都完成后，我们需要按照纬度的标准表示法重新组合信息，正如我们在 ③ 处所的那样。完成了！

## 运行脚本

给脚本一个图像，如果文件包含纬度和经度信息，脚本将将其转换为可以由 Google Maps、Bing Maps 或任何其他主要映射程序分析的格式，列表 14-10 所示。

## 结果

```bash
$ geoloc pairing-lot-with-geotags.jpg
Coords: 40 30' 19.73" N, 103 12' 3.72" W
$
```

列表 14-10：运行 `geoloc` 脚本

## 改进脚本

如果你输入一张没有 EXIF 信息的照片会发生什么？你认为脚本应该优雅地处理这种情况，而不是只输出来自失败调用的丑陋错误信息或打印空坐标吗？增加一些防御性代码，以确保从 ImageMagick 提取的 GPS 位置值是合理的将是一个很有用的补充。

# 15

## 天与日期

![](img/954a28cc04c09826495e330f44c0085b_360_0.png)

计算日期是非常复杂的，无论你是试图确定某一年是否为闰年、距离圣诞节还有多少天，还是你活了多少天。这就是基于 Unix 的系统（如 OS X）与具有 GNU 基础的 Linux 系统之间的差异之处。David Mackenzie 为 GNU 版本 Linux 重写的 `date` 工具在功能上远胜。

如果你正在使用 OS X 或运行 `date --version` 生成错误信息的系统，可以下载一组核心工具，它们将提供 GNU `date` 作为新的命令行选项（可能通过安装 `gdate` 来实现）。对于 OS X，你可以使用 brew 包管理器（默认未安装，但为了以后使用很容易安装）：

```bash
$ brew install coreutils
```

一旦你安装了 GNU，计算例如某一年是否为闰年就可以由程序本身处理，而你不需要去处理关于能被 4 整除但不能被 100 整除等等等规则。

```bash
if [ $( 12/31/$year*$j ) -eq 366 ]
```

也就是说，如果一年的最后一天是年的第 366 天，它必须是闰年。GNU `date` 优秀的另一个特性是它可以追溯过去。标准的 Unix `date` 命令是以 UTC 时间 1970年1月1日00:00:00 作为“时间零”或纪元日期构建的。想知道 1965 年发生的事情？没门。通常，通过本章中的三个巧妙的脚本，你可以利用 GNU `date` 的优势。

## 99 查找过去特定日期的星期

快问：你出生在星期几？尼尔·阿姆朗和巴兹·奥尔德林第一次登上月球是星期几？列表 15-1 中的脚本可以帮助你快速回答这些经典问题，并完美地展示了 GNU `date` 有多强大。

### 代码部分

```bash
#!/bin/bash
# daypass--给定一个日期，报告该日期是星期几
```

```bash
if [ $# -ne 3 ]; then
  echo "Usage: $(basename $0) mon day year" >&2
  echo "   仅使用数值（ex: 7 7 1776)" >&2
  exit 1
fi
```

```bash
date --version > /dev/null 2>&1
if [ $? -ne 0 ]; then
  date="gdate"
else
  date="date"
fi

dayofweek=$date -d "$2/$1/$3" +%A

case $dayofweek in
  Sunday ) echo "That was Sunday" ;;
  Monday ) echo "That was Monday" ;;
  Tuesday ) echo "That was Tuesday" ;;
  Wednesday ) echo "That was Wednesday" ;;
  Thursday ) echo "That was Thursday" ;;
  Friday ) echo "That was Friday" ;;
  Saturday ) echo "That was Saturday" ;;
esac
```

```bash
if [ $# -ne 3 ]; then
echo " $(basename $0) mon day year"
echo " with just numerical values (ex: 7 7 1776)"
exit 1
fi

$date --version /dev/null 2>&1 # 如果有错误则丢弃。

```

```bash
if [ $# -ne 0 ]; then
echo "Sorry, but $(basename $0) can't run GNU date." >&2
exit 1
fi
```

```bash
eval $(date +"thismon=%m;thisday=%d;thisyear=%Y;dayofyear=%j")
startmon=$1 startday=$2 start=$3
```

`daysMonth $start` # 设置全局变量 `dim`。

```bash
if [ $startday -lt 0 -o $startday -gt $dim ]; then
echo "Invalid: Month #$startmon only has $dim days." >&2
exit 1
fi
```

```bash
if [ $startmonth -eq 2 -a $startday -eq 29 ]; then
isleap $startyear
if [ -z "$leapyear" ]; then
echo "Invalid: \$startyear wasn't a leap year; February had 28 days." >&2
exit 1
fi
```

###########################

#### 计算天数

###########################

#### 起始年份剩余天数

```bash
# 为指定的起始日期计算日期字符串格式。
startdate="$startmon/$startday/$startyear"
```

```bash
calculate=$(((10#($date -d "12/31/$startyear +%j))) \
-((10#($date -d $startdatefmt +%j))))
```

`daysleftyear=$(( $ calculate ))`

#### 间接年份的天数

```bash
daysbetweenyears=0
tempyear=$(( $startyear + 1 ))
```

```bash
while [ $tempyear -lt $thisyear ]; do
daysbetweenyears=$((daysbetweenyears + \
(10#($date -d "12/31/$tempyear +%j))))
tempyear=$(( $tempyear + 1 ))
done
```

#### 当前年份的天数

```bash
dayofyear=$($date +%j) # 这很简单！
```

#### 汇总总和

```bash
totaldays=$((((10#$daysleftyear)) + \
((10#$daysbetweenyears)) + \
((10#$dayofyear)) ))
```

```bash
/bin/echo -n "$totaldays days have elapsed between \
/bin/echo -n "$startday/$startyear " \
echo "today, and $dayofyear of $thisyear." \
exit 0
```

Listing 15-3: `daysago` 脚本

## 工作原理

这是一个长脚本，但其逻辑并不复杂。闰年函数非常直观——我们只需要检查该年份是否为 366 天。
