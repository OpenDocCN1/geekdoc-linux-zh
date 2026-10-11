
入站 JSON 中使用的名称为 `artistName`。对于 `json.Unmarshal()` 来说，这就足够了，因为它可以深入解析第 22 行 JSON 文件中的所有条目，这是因为该函数接收到的指向这些流条目数组（此时仍为空数组）的指针是存储在 `data` 中的。利用 Go 的反射机制，该函数能够确定它需要处理哪些 JSON 结构。

清单 1 统计每首歌曲在流媒体历史中出现的次数，结果存储在定义于第 16 行的 `bySong` 映射中。为此，它使用标题字符串作为键，并在流媒体数据中每发现一次播放事件就将该 64 位整数映射值加一。最后，该函数需要按整数值的降序对映射进行排序，以输出前三个结果。

## 排序并非易事

在脚本语言中，排序映射数据轻而易举，但 Go 提供类型安全性，因此清单 1 将映射条目转换为 `kv`（代表键/值）结构数组切片，其类型定义从第 30 行开始。从第 31 行开始的 for 循环需要费力遍历映射中的每个条目，并将其发现的每个键值对作为一个 `kv` 结构附加到 `kv`s 数组切片中。然后可以使用 Go 标准库中的 sort `Slice()` 函数对该切片进行排序。第 39 行的回调函数告诉它，可以通过数值比较位于 i 和 j 位置的两个计数器，来确定切片中两个条目的期望顺序。

哇，这相当复杂！最后，从第 41 行开始的 for 循环遍历排序后的数组，输出前几个位置，并在第一个值之后终止。

## 用 R 更快

编写用于解析 JSON 数据并计算统计信息的 Go 程序真的让人头疼。Go 的类型安全性在此处需要不成比例的大量样板代码，而脚本语言只需优雅地跳过即可。这呼唤了像 R 这样的经典数据处理语言，它采用更轻松的方式，为程序员节省了大量工作。如果你的机器上还没有 R，只需在 Ubuntu 上安装它，例如使用以下命令：

```
sudo apt install r-base
```

清单 3 展示了一个简单应用，它扫描用户的 Spotify 流媒体历史，生成他们聆听歌曲实际播放时长的直方图，并将其美观地显示为条形图（图 3）。该图表表明，许多歌曲在不到 15 秒（15,000 毫秒）内就被简单取消了。在这种情况下，Spotify 的推荐算法很可能犯了错，惹恼了听众，导致他们切换到下一首歌。从大约一分钟的播放时长开始（即 60,000 毫秒之后），出现了一条类似高斯分布的钟形曲线，峰值在 220 秒。如今大多数歌曲大约长度为三分半钟，大部分在两到五分钟之间。

为了能够在命令行调用清单 3，第 1 行的 shebang 语句会在 shell 的搜索路径中寻找 Rscript 程序，并调用底层的 R 解释器来执行文件中的程序代码。此外，请确保通过 `chmod +x` 命令将文件 `hist.r`（清单 3）标记为可执行文件。

为了优雅地读取 JSON 数据，清单 3 使用了 `jsonlite` 包；你需要预先安装它。在打开 R 会话（只需在命令行输入 `R`）之后，`install.packages("jsonlite")` 命令会从 Comprehensive R Archive Network (CRAN) 加载该包的 C++ 源代码，在本地编译，并将库集成到本地的 R 环境中。之后，任何 R 脚本都可以使用 `library("jsonlite")` 来包含新库并调用其中的函数。

第 3 行使用从 `jsonlite` 导出的 `fromJSON` 函数从流媒体历史中读取 JSON 数据，并将其作为 `dataframe` 存储在 `jdata` 变量中。这种 R 数据类型是一种带有按行向量值的数据库表，每个值跨越多个列。除了数值和字符串，列还可以包含所谓的因子。在 R 中，这些因子是具有特定数量可能取值的变量，例如 `small`、`medium` 和 `large`。

## 播放时长统计

清单 3 需要将其分析的所有歌曲的最大记录播放时长限制为五分钟，因为我的流媒体历史中还包括 90 分钟的音频播放，这使统计数据变得无法辨认。过滤由第 4 行的 `recoding` 语句处理，该语句使用条件 `jdata$msPlayed < 300000` 在将结果再次分配给 `jdata` 变量之前，从 `jdata` 数据框中过滤掉所有播放时间超过 300 秒的曲目。

重构语句在行和列两个级别上进行。第 4 行方括号中包含的条件由逗号分隔。过滤器将第一个条件应用于每一行，第二个条件应用于每一列。结果是一个数据框，它可以同时减少行数和列数。然而在这种情况下，我们只需要删除行，而不需要删除列，因此方括号中逗号后面的条件第二部分保持为空。是的，你需要一双鹰眼才能正确阅读和理解 R 代码！

## 清单 3: hist.r

```r
#!/usr/bin/env Rscript
library("jsonlite")
jdata <- fromJSON("MyData/StreamingHistory0.json", simplifyDataFrame = TRUE)
jdata <- jdata[jdata$msPlayed < 300000, ]
attach(jdata)
png(filename="hist.png")
hist(msPlayed, main="Milliseconds Played")
detach(jdata)
```

![](img/e3f454b04d121b3b3750fddfda8dd21e_45_0.png)

图 3: 由清单 3 生成的播放时长直方图

|   | endTime         | artistName               | trackName          | msPlayed |
|---|-----------------|--------------------------|--------------------|----------|
| 1 | 2021-10-20 04:21 | Foster The People        | SHC                | 248030   |
| 2 | 2021-10-20 04:25 | Nothing But Thieves      | Futureproof        | 27397    |
| 3 | 2021-10-20 04:28 | Twenty One Pilots        | Shy Away           | 174963   |
| 4 | 2021-10-23 03:34 | Cypress Hill             | (Rock) Superstar   | 185931   |
| 5 | 2021-10-23 03:48 | Culcha Canela            | Monsta 2k21 - Radio Edit | 43929  |
| 6 | 2021-10-24 00:08 | Judas Priest             | Lightning Strike   | 209430   |

图 4: 来自 JSON 数据的原始数据框。

|   | endTime         | artistName               | trackName          | msPlayed | hour |
|---|-----------------|--------------------------|--------------------|----------|------|
| 1 | 2021-10-20 04:21 | Foster The People        | SHC                | 248030   | 21   |
| 3 | 2021-10-20 04:28 | Twenty One Pilots        | Shy Away           | 174963   | 21   |
| 4 | 2021-10-23 03:34 | Cypress Hill             | (Rock) Superstar   | 185931   | 20   |
| 6 | 2021-10-24 00:08 | Judas Priest             | Lightning Strike   | 209430   | 17   |

图 5: 带有小时列的过滤后的数据框。

## 清单 4: hourly.r

```
#!/usr/bin/env Rscript
library("jsonlite")

data <- fromJSON("/MyData/StreamingHistory.json", simplifyDataFrame = TRUE)
# only 50412 songs

jdata <- data[data$msPlayed > 60000, ]
d <- as.POSIXct(data$endTime, tz = "UTC")
jdata$hour <- as.numeric(format(d, tz="America/Los_Angeles", "%H"))
subset(jdata, , select=c(hour, artistName))
agg <- aggregate(songsPerhour, by=list(artistName=songsPerartistName, hour=songsPerhour), FUN=length)
winners <- agg[order(agg$hour, -agg$x),]
winners <- winners[!duplicated(winners[2]),]
winners
```

这个非常紧凑的清单随后为 jdata 数据框中的 msPlayed 条目创建直方图，并为条形图准备播放时长的计数值。这是由第 7 行的内置 R 函数 hist() 完成的，前提是第 5 行已将 jdata 数据框设为参考点，第 6 行已将未来生成的任何 PNG 输出文件设置为 hist.png。这确保了 R 在脚本结束时创建具有此名称和条形图的 PNG 文件。

## 热门组合

流媒体历史中的数据是否也能根据一天中的不同时间段得出对特定类型音乐偏好的结论？清单 4 对此进行了尝试，它读取 JSON 数据，从每个流媒体事件的 endTime 时间戳中提取播放结束时间的小时数（作为数值），然后确定在该时间窗口内（对所有流媒体日取平均值）最常播放的是哪位艺术家。

图 4 展示了数据框中的原始 JSON 数据，包含 JSON 文件中找到的所有字段。清单 4 中的第 5 行丢弃了所有播放时间未达到至少一分钟的歌曲，以避免向统计中引入假阳性。现在的任务是从 Spotify 时间戳中提取一天中的小时；这是在调整时区后完成的。Spotify 将时间标记为 UTC（即 GMT），但这并非美国西海岸太平洋时间（PT）区的音乐时间。这解释了为什么 as.POSIXct() 函数从 JSON 数据中读取值时将其视为 UTC，而第 7 行中的 format 格式器将其转换为 America/Los_Angeles 时区。执行此操作后，通过 %H 确定的本地时间小时值作为字符串可用。但是，为了稍后对条目进行排序，R 需要数值，因此 as.numeric() 将其转换为数字。

现在数据框位于 jdata 变量中，如图 5 所示。清单 4 中的第 8 行随后使用 subset() 将数据转换为仅包含两列（艺术家和播放小时）的数据框。然后，R 的内置 aggregate() 函数在第 9 行将所有具有相同小时值的艺术家的行聚合在一起。FUN=length 指定额外的聚合列包含长度（即艺术家-小时元组的数量）。

|     | artistName              | hour |
|-----|-------------------------|------|
| 293 | Zucchero                | 19   | 1 |
| 294 | ZZ Top                  | 19   | 1 |
| 343 | Linkin Park             | 20   | 11 |
| 365 | Sparks                  | 20   | 11 |
| 314 | Element Of Crime        | 20   | 7 |
| 317 | Eros Ramazzotti         | 20   | 6 |
| 356 | Pink Floyd              | 20   | 6 |
| 304 | Cypress Hill            | 20   | 5 |
| 321 | Foster The People       | 20   | 5 |
| 319 | Falco                   | 20   | 4 |

图 6: 每小时的聚合计数器。

