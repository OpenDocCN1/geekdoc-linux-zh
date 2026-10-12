
```go
package main
import (
    "encoding/json"
    "fmt"
    "log/ioutil"
    "sort"
)
type stream struct {
    EndTime     string `json:endTime`
    ArtistName  string `json:artistName`
    MsPlayed    int64  `json:msPlayed`
    TrackName   string `json:trackName`
}
const jsonFile = "MyData/StreamingHistory0.json"
func main(){
    bySong := map[string]int64{}
    content, err := ioutil.ReadFile(jsonFile)
    if err != nil {
        panic(err)
    }
    data := []stream{}
    err = json.Unmarshal(content, &data)
    if err != nil {
        panic(err)
    }
    for _, song := range data {
        title := fmt.Sprintf("%s/%s", song.ArtistName, song.TrackName)
        bySong[title] += 1
    }
    type kv struct {
        Key   string
        Value int64
    }
    kvs := []kv{}
    for k, v := range bySong {
        kvs = append(kvs, kv{k, v})
    }
    sort.Slice(kvs, func(i, j int) bool {
        return kvs[i].Value > kvs[j].Value
    })
    for i := 0; i < 3; i++ {
        fmt.Printf("%s (%dx)\n", kvs[i].Key, kvs[i].Value)
    }
}
```

### 清单 2: 前三首歌曲

- Sparks/When Do I Get to Sing "My Way" – 2019 – Remaster (19x)
- Falco/The Sound of Music (16x)
- Linkin Park/With You (14x)

入站 `JSON` 中使用的名称为 `artistName`。对于 `json.Unmarshal()` 来说，这就足够了，因为它可以深入解析第 22 行 `JSON` 文件中的所有条目，这是因为该函数接收到的指向这些流条目数组（此时仍为空数组）的指针是存储在 `data` 中的。利用 `Go` 的反射机制，该函数能够确定它需要处理哪些 `JSON` 结构。

清单 1 统计每首歌曲在流媒体历史中出现的次数，结果存储在定义于第 16 行的 `bySong` 映射中。为此，它使用标题字符串作为键，并在流媒体数据中每发现一次播放事件就将该 64 位整数映射值加一。最后，该函数需要按整数值的降序对映射进行排序，以输出前三个结果。

### 排序并非易事

在脚本语言中，排序映射数据轻而易举，但 `Go` 提供类型安全性，因此清单 1 将映射条目转换为 `kv`（代表键/值）结构数组切片，其类型定义从第 30 行开始。从第 31 行开始的 `for` 循环需要费力遍历映射中的每个条目，并将其发现的每个键值对作为一个 `kv` 结构附加到 `kvs` 数组切片中。然后可以使用 `Go` 标准库中的 `sort.Slice()` 函数对该切片进行排序。第 39 行的回调函数告诉它，可以通过数值比较位于 `i` 和 `j` 位置的两个计数器，来确定切片中两个条目的期望顺序。

哇，这相当复杂！最后，从第 41 行开始的 `for` 循环遍历排序后的数组，输出前几个位置，并在第一个值之后终止。

### 用 R 更快

编写用于解析 `JSON` 数据并计算统计信息的 `Go` 程序真的让人头疼。`Go` 的类型安全性在此处需要不成比例的大量样板代码，而脚本语言只需优雅地跳过即可。这呼唤了像 `R` 这样的经典数据处理语言，它采用更轻松的方式，为程序员节省了大量工作。如果你的机器上还没有 `R`，只需在 `Ubuntu` 上安装它，例如使用以下命令：

```bash
sudo apt install r-base
```

清单 3 展示了一个简单应用，它扫描用户的 `Spotify` 流媒体历史，生成他们聆听歌曲实际播放时长的直方图，并将其美观地显示为条形图（图 3）。该图表表明，许多歌曲在不到 15 秒（15,000 毫秒）内就被简单取消了。在这种情况下，`Spotify` 的推荐算法很可能犯了错，惹恼了听众，导致他们切换到下一首歌。从大约一分钟的播放时长开始（即 60,000 毫秒之后），出现了一条类似高斯分布的钟形曲线，峰值在 220 秒。如今大多数歌曲大约长度为三分半钟，大部分在两到五分钟之间。

为了能够在命令行调用清单 3，第 1 行的 `shebang` 语句会在 `shell` 的搜索路径中寻找 `Rscript` 程序，并调用底层的 `R` 解释器来执行文件中的程序代码。此外，请确保通过 `chmod +x` 命令将文件 `hist.r`（清单 3）标记为可执行文件。

为了优雅地读取 `JSON` 数据，清单 3 使用了 `jsonlite` 包；你需要预先安装它。在打开 `R` 会话（只需在命令行输入 `R`）之后，`install.packages("jsonlite")` 命令会从 `Comprehensive R Archive Network` (CRAN) 加载该包的 `C++` 源代码，在本地编译，并将库集成到本地的 `R` 环境中。之后，任何 `R` 脚本都可以使用 `library("jsonlite")` 来包含新库并调用其中的函数。

第 3 行使用从 `jsonlite` 导出的 `fromJSON` 函数从流媒体历史中读取 `JSON` 数据，并将其作为 `dataframe` 存储在 `jdata` 变量中。这种 `R` 数据类型是一种带有按行向量值的数据库表，每个值跨越多个列。除了数值和字符串，列还可以包含所谓的因子。在 `R` 中，这些因子是具有特定数量可能取值的变量，例如 `small`、`medium` 和 `large`。

### 播放时长统计

清单 3 需要将其分析的所有歌曲的最大记录播放时长限制为五分钟，因为我的流媒体历史中还包括 90 分钟的音频播放，这使统计数据变得无法辨认。过滤由第 4 行的 `recoding` 语句处理，该语句使用条件 `jdata$msPlayed < 300000` 在将结果再次分配给 `jdata` 变量之前，从 `jdata` 数据框中过滤掉所有播放时间超过 300 秒的曲目。

重构语句在行和列两个级别上进行。第 4 行方括号中包含的条件由逗号分隔。过滤器将第一个条件应用于每一行，第二个条件应用于每一列。结果是一个数据框，它可以同时减少行数和列数。然而在这种情况下，我们只需要删除行，而不需要删除列，因此方括号中逗号后面的条件第二部分保持为空。是的，你需要一双鹰眼才能正确阅读和理解 `R` 代码！

### 清单 3: hist.r

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
