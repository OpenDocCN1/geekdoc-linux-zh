

![](img/e3f454b04d121b3b3750fddfda8dd21e_42_0.png)

**图 2：** 使用 apt-clone 信息归档文件的概述。

将尝试将它们包含在备份目录中。但请注意，尝试未必总是成功，因为可安装的 .deb 包并不自动具备 Debian 发行版所需的格式和标准。这类包在日常使用中完全正常，但可能不会被 apt-clone 识别（见图 1）。

无论如何，几分钟内，apt-clone 就会创建一个 TAR 压缩文件。如果你试图包含第三方软件包，由于每个第三方软件包都必须单独分析，所需时间可能会长得多。你可以使用以下命令读取新创建文件的一般信息：

```
apt-clone info FILE
```

在图 2 中，跨越七个不同的桌面，安装了 2,977 个软件包，但只有 2,619 个是官方 Debian 软件包，这意味着完美克隆的可能性不大，尽管基本功能应该能成功克隆。要查看归档文件的不同视图，可以使用诸如 Ark 这样的归档应用程序（图 3）。正如你所预期的，软件包源和 apt 设置是归档的主要类别，还有 apt-clone 的日志文件。偏好设置包括来自如 .config/ 或 .local 等目录的配置设置。理论上，你可以解开归档文件并尝试编辑，但这可能比值得付出的努力更多。不过，确切知道自己在做什么，而不是盲目遵循指示，永远不是浪费时间。

由于归档文件包含系统敏感信息，除非你计划在克隆后立即删除它，否则你应该对其进行加密。使用 GPG 并在非实际使用时保持文件加密是保证合理安全性的最快方法。

## 如何克隆

一旦你有了归档文件，请安装与源系统相同 Debian 版本的目标系统。使用其他 Debian 版本可能会起作用，但这会增加出现问题几率——这些问题花费的时间可能比 apt-clone 所能节省的还要多。将归档文件传输到目标系统的根目录，如有必要请解密，并以 root 身份运行：

```
apt-clone restore FILE
```

该过程类似于通常安装软件包的方式，在较新的硬件上可能需要 20 分钟或更长时间，具体取决于涉及的软件包数量。如果你选择使用 restore-new distro 而不是 restore，所需时间会更长，因为你将在同时尝试升级软件包。在恢复之前升级可能会减少出错的概率。

当过程结束时，克隆将完成，无需重启，就像安装新软件包时发生的情况一样。同样，因为源文件属于 root 并以 root 身份复制，你应该不会遇到权限问题。如果你确实遇到了任何问题，使用 apt-clone diff 与源机器的文件进行比较可能有助于解决问题。

## 局限性

apt-clone 的主要缺点是它专为配合官方存储库使用而设计。

![](img/e3f454b04d121b3b3750fddfda8dd21e_42_1.png)

**图 3：** 归档文件内容的概述。

如果你要克隆的系统包含来自第三方源安装的 .deb 软件包，apt-clone 会尝试处理它们，但有时可能不成功。这意味着，例如，如果你安装了来自 The Document Foundation 的最新版本 LibreOffice，你将不得不单独备份配置文件。同样，将配置文件传输到操作系统的较新版本可能也只会取得有限的成功。可能，使用 apt-clone 最实用的场景是当你安装由相同工作站组成的实验室，或想要一台与你旧电脑完全相同的新家用电脑时。当 apt-clone 满足你的需求时，它是一个优雅的小脚本，但它永远不会是针对所有可能情况的完整解决方案。 👍

## 信息

**[1]** apt-clone：

https://github.com/mvo5/apt-clone

## 作者

**布鲁斯·拜菲尔德（Bruce Byfield）** 是一名计算机记者，也是自由作家和编辑，专长于自由和开源软件。除了写作项目外，他还讲授在线学习课程。在他的业余时间，布鲁斯撰写关于西北海岸艺术的文章（https://brucebyfield.wordpress.com）。他也是 *Printice Pieces* 的联合创始人，这是一个关于写作和幻想的博客，位于 https://printicepieces.com/。

## 请求 Spotify 档案并使用 Go 和 R 进行评估

### 文件检查员

Spotify，这家互联网音乐服务，收集关于其用户及其音乐口味的数据。迈克·希尔利（Mike Schilli）请求了这些文件的副本，以便使用 Go 进行调查。*作者：迈克·希尔利*

像 Spotify 或 Apple Music 这样的流媒体服务主导着音乐行业。它们庞大的目录现在覆盖了所有可消费的音乐。依靠人工智能，这些服务通过其算法预测用户可能喜欢的歌曲，从而向用户推荐新歌。与传统实体音乐媒体相比，它们已无法与之抗衡，只能落在架子上积灰。当然，这种发展也意味着匿名音乐消费已成过去，因为流媒体服务会精确记录谁在什么时候播放了哪首曲目以及播放了多久。

应请求，Spotify 甚至会移交所获取的数据（图 1）。如果你在他们的网站上稍作探索，你会发现需要按下的按钮来请求这些文件的副本，位于“账户 | 隐私设置”中，但 Spotify 响应速度较慢。

从请求之时起，大约需要一周时间，他们的档案管理员才能从 Spotify 底层的文件中检索数据，进行压缩，并将其作为 ZIP 归档发布在网站上供你下载。收到 Spotify 的电子邮件通知后，你可以在接下来的两周内下载数据，并在本地尽情探索。

**作者**
迈克·希尔利（Mike Schilli）是加州旧金山湾区的一名软件工程师。在他的专栏中，自 1997 年以来每月更新，他研究各种编程语言的实际应用。如果你通过 mschilli@perimeter.com 给他发邮件，他会乐意回答任何问题。

![](img/e3f454b04d121b3b3750fddfda8dd21e_43_0.png)

![](img/e3f454b04d121b3b3750fddfda8dd21e_43_1.png)

### 编程快照 – Go 和 R

#### 深入探讨

![](img/e3f454b04d121b3b3750fddfda8dd21e_44_0.png)

#### 练习

包含下载数据的 ZIP 文件包括一个名为 `StreamWithHistory.json` 的 JSON 文件，其中按历史顺序列出了你播放的所有流媒体的元数据（图 2）。除了歌曲和艺术家外，条目还列出了开始日期和时间以及播放时长。播放时长特别有趣，因为如果用户在几秒钟后中断流媒体并快进到下一首歌，该曲目很可能是不小心被加入播放列表的，而不是用户真正喜欢的。在整理音乐建议时，这极有可能是一个误报。

为了使用 JSON 解析器从 Spotify 数据创建内部 Go 数据结构，必须已知该格式并与其实际的 JSON 格式匹配。Spotify 提供的 JSON 数据块，如图 2 所示，由一个数组组成，其每个元素对应一个流媒体曲目。艺术家和曲目名称以字符串形式存储在 `artistName` 和 `trackName` 字段中。`msPlayed` 给出以毫秒为单位的播放时间，而 `endTime` 包含播放结束时的日期和时间。清单 1 中 `stream` 结构的字段均以大写字母开头，这意味着其他包之后也可以访问它们。然而，这意味着名称与 JSON 格式中的变量名称不相同，后者均以小写字母开头。不过，这没什么大不了的，因为 Go 允许使用 `json:` 标签给结构体指定一个与字段名称不同的名称。

![](img/e3f454b04d121b3b3750fddfda8dd21e_44_1.png)

例如，第 10 行的 `ArtistName string \`json:"artistName"\`` 指定 Go 结构中 `artistName` 字段的艺术家类型为 `string`，并且

##### 清单 1: stats.go

```go
01 package main
02 import (
03     "encoding/json"
04     "fmt"
05     "log/ioutil"
06     "sort"
07 )
08 type stream struct {
09     EndTime     string `json:endTime`
10     ArtistName  string `json:artistName`
11     MsPlayed    int64  `json:msPlayed`
12     TrackName   string `json:trackName`
13 }
14 const jsonFile = "MyData/StreamingHistory0.json"
15 func main(){
16     bySong := map[string]int64{}
17     content, err := ioutil.ReadFile(jsonFile)
18     if err != nil {
19         panic(err)
20     }
21     data := []stream{}
22     err = json.Unmarshal(content, &data)
23     if err != nil {
24         panic(err)
25     }
26     for _, song := range data {
27         title := fmt.Sprintf("%s/%s", song.ArtistName, song.TrackName)
28         bySong[title] += 1
29     }
30     type kv struct {
31         Key   string
32         Value int64
33     }
34     kvs := []kv{}
35     for k, v := range bySong {
36         kvs = append(kvs, kv{k, v})
37     }
38     sort.Slice(kvs, func(i, j int) bool {
39         return kvs[i].Value > kvs[j].Value
40     })
41     for i := 0; i < 3; i++ {
42         fmt.Printf("%s (%dx)\n", kvs[i].Key, kvs[i].Value)
43     }
44 }
```

##### 清单 2: 前三首歌曲

- Sparks/When Do I Get to Sing "My Way" – 2019 – Remaster (19x)
- Falco/The Sound of Music (16x)
- Linkin Park/With You (14x)

