
| 2 | 2021-10-20 04:25 | Nothing But Thieves | Futureproof | 27397 |

| 3 | 2021-10-20 04:28 | Twenty One Pilots | Shy Away | 174963 |

| 4 | 2021-10-23 03:34 | Cypress Hill | (Rock) Superstar | 185931 |

| 5 | 2021-10-23 03:48 | Culcha Canela | Monsta 2k21 - Radio Edit | 43929 |

| 6 | 2021-10-24 00:08 | Judas Priest | Lightning Strike | 209430 |

图 4: 来自 JSON 数据的原始数据框。

| | `endTime` | `artistName` | `trackName` | `msPlayed` | `hour` |
|---|-----------------|--------------------------|--------------------|----------|------|
| 1 | 2021-10-20 04:21 | Foster The People | SHC | 248030 | 21 |
| 3 | 2021-10-20 04:28 | Twenty One Pilots | Shy Away | 174963 | 21 |
| 4 | 2021-10-23 03:34 | Cypress Hill | (Rock) Superstar | 185931 | 20 |
| 6 | 2021-10-24 00:08 | Judas Priest | Lightning Strike | 209430 | 17 |

图 5: 带有小时列的过滤后的数据框。

### 清单 4: `hourly.r`

```r
#!/usr/bin/env Rscript
library("jsonlite")

data <- fromJSON("/MyData/StreamingHistory.json", simplifyDataFrame = TRUE)
## only 50412 songs

jdata <- data[data$msPlayed > 60000, ]
d <- as.POSIXct(data$endTime, tz = "UTC")
jdata$hour <- as.numeric(format(d, tz="America/Los_Angeles", "%H"))
subset(jdata, , select=c(hour, artistName))
agg <- aggregate(songsPerhour, by=list(artistName=songsPerartistName, hour=songsPerhour), FUN=length)
winners <- agg[order(agg$hour, -agg$x),]
winners <- winners[!duplicated(winners[2]),]
winners
```

这个非常紧凑的清单随后为`jdata`数据框中的`msPlayed`条目创建直方图，并为条形图准备播放时长的计数值。这是由第 7 行的内置 R 函数`hist()`完成的，前提是第 5 行已将`jdata`数据框设为参考点，第 6 行已将未来生成的任何 PNG 输出文件设置为`hist.png`。这确保了 R 在脚本结束时创建具有此名称和条形图的 PNG 文件。

### 热门组合

流媒体历史中的数据是否也能根据一天中的不同时间段得出对特定类型音乐偏好的结论？清单 4 对此进行了尝试，它读取 JSON 数据，从每个流媒体事件的`endTime`时间戳中提取播放结束时间的小时数（作为数值），然后确定在该时间窗口内（对所有流媒体日取平均值）最常播放的是哪位艺术家。

图 4 展示了数据框中的原始 JSON 数据，包含 JSON 文件中找到的所有字段。清单 4 中的第 5 行丢弃了所有播放时间未达到至少一分钟的歌曲，以避免向统计中引入假阳性。现在的任务是从 Spotify 时间戳中提取一天中的小时；这是在调整时区后完成的。Spotify 将时间标记为 UTC（即 GMT），但这并非美国西海岸太平洋时间（PT）区的音乐时间。这解释了为什么`as.POSIXct()`函数从 JSON 数据中读取值时将其视为 UTC，而第 7 行中的`format`格式器将其转换为`America/Los_Angeles`时区。执行此操作后，通过`%H`确定的本地时间小时值作为字符串可用。但是，为了稍后对条目进行排序，R 需要数值，因此`as.numeric()`将其转换为数字。

现在数据框位于`jdata`变量中，如图 5 所示。清单 4 中的第 8 行随后使用`subset()`将数据转换为仅包含两列（艺术家和播放小时）的数据框。然后，R 的内置`aggregate()`函数在第 9 行将所有具有相同小时值的艺术家的行聚合在一起。`FUN=length`指定额外的聚合列包含长度（即艺术家-小时元组的数量）。

| | `artistName` | `hour` | |
|-----|-------------------------|------|---|
| 293 | Zucchero | 19 | 1 |
| 294 | ZZ Top | 19 | 1 |
| 343 | Linkin Park | 20 | 11 |
| 365 | Sparks | 20 | 11 |
| 314 | Element Of Crime | 20 | 7 |
| 317 | Eros Ramazzotti | 20 | 6 |
| 356 | Pink Floyd | 20 | 6 |
| 304 | Cypress Hill | 20 | 5 |
| 321 | Foster The People | 20 | 5 |
| 319 | Falco | 20 | 4 |

图 6: 每小时的聚合计数器。

### 深入解析

#### 编程快照 – Go 和 R

图 6 展示了该中间结果的一个摘录。基于此，`ZZ Top`在 19:00 正好播放了一次，而在 20:00 出现了不少于 11 条`Linkin Park`的条目。有几种不同的方法可以从该视图中过滤出仅有的顶级表现者（例如，20:00 时的`Linkin Park`）。一种完全依赖 R 标准函数方法如下：对数据框按小时（升序）和事件数量（降序）进行排序。使用去重功能，算法仅保留每个小时值的第一个条目，并丢弃其余部分。每个小时值的顶级表现者得以保留。
