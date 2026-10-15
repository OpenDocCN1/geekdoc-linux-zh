
**列表 10.24** 批文件的输出。

29. 我有一个睡眠舱。
30.
31. >> `brainhat` 有活动。
32. 我有活动。
33.
34. >> `brainhat` 有餐厅。
35. 我有餐厅。
36.
37. >> `brainhat` 有信息。
38. 我有信息。
39.
40. >> 如果你有房间那么房间是可用的。
41. 如果我有房间它们是可用的。
42.
43. >> 你叫什么名字？
44. 我的名字是 `alisha`。
45.
46. >> 你住在哪里？
47. 我确实住在火星上。
48.
49. >> 你有房间吗？
50. 有的。我有一个睡眠舱，房间是可用的。
51.
52. >> 房间可用吗？
53. 有的。房间是可用的。
54.
55. >> 你有一个房间吗？
56. 有的。我有一个睡眠舱，有一个睡眠舱是可用的。
57.
58. >> 房间可用吗？
59. 有的。有一个睡眠舱是可用的。

**列表 10.24** 批文件的输出（续）

创建一个批文件，包含当前的火星 7 号殖民地，随后跟一个用于测试场景的问题列表。将文件保存为 `batch-test` 并位于 `Brainhat` 目录的根级别。在命令行中使用 `brainhat -r batch-test` 运行该文件以激活。

# 直觉对话

FAQ 引擎可以通过提问用户、发表陈述或等待更多响应来继续。通常情况下，如果系统是由经验丰富的使用的，他们将不需要很多提示。

# 准备就绪回答

FAQ 引擎可以通过提问用户、发表陈述或等待更多响应来继续。通常情况下，如果系统是由经验丰富的使用的，他们将不需要很多提示。

# 最终场景

列表 10.31 显示了一个完整的火星 7 号殖民地场景。它包含了程序关于自己的信息、一组程序可以回答特定问题的事实，以及一组从这些事实得出推理的逻辑。列表 10.32 是 `extended-vocabulary.txt` 文件，定义了场景中的新术语，列表 10.33 显示了 `whereas7.txt` 和 `whatisc7.txt` 文件的内容，它们对应列表 10.31 的第 18 和第 19 行。

# FAQ 引擎 345

16. `Brainhat` 拥有信息。
17.
18. 如果说话者询问 7 号殖民地在哪里，则提供 `7.txt`。
19. 如果说话者询问 7 号殖民地是什么，则提供 `whatisc7.txt`。
20.
21. 火星是干燥的。
22. `Brainhat` 喜欢火星，因为那里天气很冷。
23.
24. 如果你有房间，那么房间是可用的。
26.
27. 如果说话者询问房间多少钱，告诉说话者一个房间需要一个火星库（`mars-kugen`），并询问说话者是否想要预订。
30.
31. 如果我需要房间，那么我想要房间。
33. 如果我想要房间，我想要预订。
35. 如果说话者想要预订，询问说话者是否有信用卡。
37.
38. 如果说话者有信用卡，则提供 `reservation-info.txt`。
40.
41. 如果说话者没有信用卡，告诉说话者你没有房间，并询问说话者是否有悬气艇。
44.
45. 如果说话者有悬气艇，告诉说话者你很高兴。

**列表 10.31** 完整场景。（继续）

1. define greeting-informal
2. label hi
3. label whats up
4. label sup
5. label yo
6. label whats up homeboy
7. child-of-greeting
8.
9. define goodbye-2
10. label q
11. label outta here
12. label later

**列表 10.32** 最终扩展词表.txt。（持续）

| | | |
| :--- | :--- | :--- |
| 13. | child-of-goodbye-1 | |
| 14. | | |
| 15. | define | accommodations-1 |
| 16. | label | accommodations |
| 17. | label | room |
| 18. | label | place to stay |
| 19. | label | place to sleep |
| 20. | label | sleeping accommodations |
| 21. | label | sleeping pod |
| 22. | | child-of-rooms-1 |
| 23. | | | |
| 24. | define | credit-card-1 |
| 25. | label | credit card |
| 26. | label | creditcard |
| 27. | | child-of-things |
| 28. | | | |
| 29. | define | krugen-1 |
| 30. | label | mars-krugen |
| 31. | related | valuable-1 |
| 32. | child-of | krugens-1 |
| 33. | | | |
| 34. | define | krugens-1 |
| 35. | label | mars-krugens |
| 36. | related | valuable-1 |
| 37. | child-of | things |
| 38. | | | |
| 39. | define | vehicle-1 |
| 40. | label | hovercraft |
| 41. | | child-of-things |
| 42. | | | |
| 43. | define | earthling-1 |
| 44. | label | earthling |
| 45. | | child-of-human-1 |

`whereisc7.txt`:
7 号殖民地位于本地太阳系的第四颗行星<break size="small"/>第三象限<break size="small"/>其他区域<break size="small"/>sec 7891<break size="small"/>主路口是第 12 街和 Vine 街。

**列表 10.33** 准备文本文件的内容。

```
whatisc7.txt:

火星 7 号殖民地是为其他 6 个殖民地的休闲圆，这些殖民地正在行星表面进行探索和基础设施扩张！这现在解释了殖民地的编号系统，解释了火星 7 号殖民地存在的理由，并确保了殖民地拥有来自火星本身不断变化的人口，而不仅仅是来自地球的匆忙游客。
```

**列表 10.33** 准备文本文件的内容。（继续）

完成火星 7 号殖民地场景。更新 `extended-vocabulary.mpm` 文件以定义场景中的新术语。为复杂项目的详细说明添加准备文本文件。

## 设置 VoiceXML 入口

一旦设置并测试了场景，设置到 `Brainhat` 服务器的 VoiceXML 网关就相对简单。我们将首先设置一个测试脚本以确认对 `Brainhat` 服务器的访问，然后创建一个在用户调用服务器时播读的简短介绍。最后，必须为 VoiceXML 网关创建一个词表，该词表将被语音转文本翻译器识别并传递给 `Brainhat` 环境。

## 在 VoiceXML 模式下设置服务器

VoiceXML 守护进程模式的执行从单个目录进行。在 Linux 机器上，这将是 `/usr/local/etc/brainhat/vxml`。在 Windows 平台上，运行目录将是你启动守护进程的地方。出于安全考虑，守护进程无法访问运行目录以上目录的文件。有一些适用于运行 `Brainhat` 模式的开关。它们允许选择运行什么场景、运行什么语法文件。

表 10 `Brainhat` 服务器命令行选项

| 开关 | 效果 |
| :--- | :--- |
| `-d` | 设置守护进程模式 |
| `-h` | 设置 html 守护模式 |
| `-x` | 设置 vxml 守护模式 |
| `-N` | 开启 vxml 模式 |
| `-g` | 选择语法文件（默认为 `brainhat.gram`） |
| `-i` | 选择初始化文件（默认为 `brainhat.init`） |
| `-l` | 选择介绍（默认为 `brainhat.intro`） |
| `-R` | 选择重置文件 |
| `-p` | 如果在防火墙后运行时可能需要使用此项 |
| `-t` | 输出跟踪 |
| `-e` | 开启输出 |
| `-r` | 运行文件 |
| `-j` | 开启动态输出 |
| `-S` | 以 html 守护进程运行 |

通过 `-x` 选项让 `Brainhat` 运行 VoiceXML 模式。`-N` 选项指示 `Brainhat` 询问语音门户的选择。`-i` 选项是初始问候：“这是 7 号殖民地。有什么可以帮您的吗？”。`-o` 选项选择场景。`-p` 选项如果你在防火墙后运行时可能需要使用此项。`-help` 选项可以查看选项列表。

VoiceXML 模式下的 `Brainhat` 命令行。

命令行的最后一项 `data` 是我们之前讨论的预编译单词和模式的路径。之前的命令行假设已经编译。这意味着如果你对词表进行了更改，在启动 VoiceXML 模式之前必须运行该命令。

**列表 10.34** 在 VoiceXML 模式下启动 `Brainhat`

```
1. brainhat -x -N 3
2. -I brainhat.intro
3. -i brainhat.init
4. -g brainhat.gram
5. ./data/data
```

> VoiceXML 模式下的 `Brainhat` 不预编译数据文件，因为它使用交互模式。你必须在启动 VoiceXML 服务器之前从命令行运行程序。

## 创建简单访问脚本

我们处理过的其他项目指向 Web 服务器来获取动态数据。在这个项目中，`Brainhat` 将充当 Web 服务器，处理调用请求并实时输出 VoiceXML 文档。然而，它对某些特定的 URL 有不同的响应。这是作为 FAQ 程序的关键。

一旦守护进程运行，你可以通过 `http://server:8080/index.xml` 这种 从 BeVocal 访问 `Brainhat`。测试你的服务器应没有错误。如果你想进行原始测试，可以 `telnet-server 80 get/index.html HTTP/1.0`

> 下一组脚本中指向的 `Brainhat` 测试环境可供开发人员进行概念证明。要下载 7 号殖民地服务器上的最新场景和词表文件，请访问 `colony7.brainhat.com/faq-files`。

`Brainhat` 的第一个引用 `/index.xml` 返回动态生成的 VoiceXML 页面，带有初始条目。它还包含对 `VoiceXML.grammar` 的引用，语音门户需要它来解释调用者的响应。后续访问将访问 `/dialogXXX.xml` 页面，这些页面由服务器动态生成，其中 XXX 代表任何随机数字，以防止语音门户缓存。

# 350 项目 10

# 文档与语法的缓存

语音门户将缓存动态生成的页面。如果你对语法做了更改，你可能希望更改语法名称，并稍微修改提供给语音门户的初始页面名称。这将强制语音门户拉取页面或语法的最新副本。你可以使用修改后的名称引用第一个页面；`Brainhat` 并不在意你请求的是 `index.xmlmz` 还是任何后缀字符的组合。

> 语音门户将尝试缓存动态页面并冻结语法。如果在更新应用程序时对语法进行了更改，请重命名语法文件，调整你的应用程序指向新文件，并重命名入口文件的扩展名。

# FAQ 引擎 351

```
1. <?xml version="1.0"?>
2.
3. <xml version="2.0">
4. <form>
5. <block>
6. <submit next=http://maddie.brainhat.com:8080/index.xml
7. method="get"/>
8. </block>
9. </form>
10. </xml>
```
