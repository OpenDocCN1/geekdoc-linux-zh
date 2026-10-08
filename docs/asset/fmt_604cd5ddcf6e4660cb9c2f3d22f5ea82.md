
一旦我知道当前的时、分、秒，我需要计算绘制每个指针的角度。使用取模 12 转换 `localtime()` 返回的小时时间（12 到 12）并找到余数。在这里，涉及一个转换范围内的值（0 到 60 秒，0 到 60 分钟和 0 到 12 小时——时间碎片！）的问题：

```python
second_hand_angle = math.pi / 60 *
current_time_sec = sec
minute_hand_angle = math.pi / 60 *
current_time_min = min
```

然而，真实的模拟时钟将所有指针连接到同一个转子上，以不同速度移动的方式绘制每根指针。当分针转一圈时，时针只移动时钟周长的 1/12；但时针在每个小时标记处的移动是需要计算的：

```python
angle = math.pi / 12
multiplier = math.sin(angle)
ymultiplier = math.cos(angle)
```

```python
marks_to_center = clock_radius/12
numeral_size = clock_radius/s
```

## 深度解析

### 使用 Cairo 进行 Python 绘图

结论

在本文中，我向你展示了如何使用 Cairo 库绘制图形。我通过演示绘制一个显示当前时间的模拟钟的所有步骤，证明了这一点。这篇文章展示了 Cairo 能够实现的功能。例如，你可以绘制贝塞尔曲线，这些曲线在彩色渐变方面精确得多，且图案也比纯色更复杂。你还可以将其保存为 PDF 和 PNG 等其他文件格式。我有另一个绘制 SVG 文件的程序。如果你想将输出发送到打印机，Cairo 支持生成 PDF 或脚本输出。在随后的文章中，我将使用 GTK 用户库将时集成到交互式用户界面中。

列表 3：执行 (`config`)

```
101
context.move_to(mark_start*math.sin
102, mark_start*math.cos(angle))
103
context.line_to(mark_end*math.sin
104, mark_end*math.cos(angle))
105
context.stroke()
106
# 画每个刻度的数字
107
### (150 / 10 = 15 像素)
108
marks_to_numeral_gap = clock_radius/15
109
### (100 / 5 = 20 像素)
110
size = clock_radius/2
111
numeral_marks = marks - to_numeral_gap
112
context.select_font('serif', Cairo.Font.NORMAL, Cairo.Font.BOLD)
113
context.set_font_size(size)
114
for i in range(12):
115
angle = 2*math.pi/12 * i
116
x = multiplier*math.sin(angle)
117
y = multiplier*math.cos(angle)
118
text = context.text_extents(NUMERIC_STRING[i])
119
x -= text.width/2 + text.x
120
y -= text.height/2 + text.y
121
context.show_text(NUMERIC_STRING[i])
```

```
128
width = clock_radius/20
129
### (150 / 3 = 50 像素)
130
hour_length = clock_radius/3
131
### (150 / 2 = 75 像素)
132
minute_length = clock_radius/24
143
144
current_time = line.time()
145
146
angle = 2*math.pi / 60 *
147
current_time.tm_sec
148
angle = 2*math.pi / 60 *
149
current_time.tm_min +
150
second_hand / 60
151
angle = 2*math.pi / 12 *
152
current_time.tm_hour +
153
hour_hand / 12
154
155
draw_hand(hour_hand,
156
hour_length)
157
draw_hand(minute_hand,
158
minute_length)
159
draw_hand(second_hand,
160
second_length)
161
162
### 在中心绘制旋转凸盖
163
### 钟表底部，用于遮盖
164
### 线的尖锐边缘，
165
### 完成圆圈
166
context.arc(0, 0, clock_radius/2,
167
context.fill())
168
169
### 将表面写入 PNG 文件
170
surface.flush()
170
surface.write_to_png('clock.png')
```

## 信息

- [1] Cairo 图形：https://cairog.org/

- [2] GTK 用户界面工具包：https://www.gtk.org/

- [3] Cairo 文档列表：https://cairog.org/doc/

- [4] Cairo 程序员参考文档：https://cairog.org/manual/

- [5] X 窗口系统：https://www.x.org/

- [6] Pango 文本渲染库：https://pango.org/

- [7] Cairo 文本渲染能力文档：https://cairog.org/manual/cairo-text.html

## 作者

Michael Williams 是一位自由职业程序员，也是 Debian-Linux 发行版的狂热用户。他喜欢使用 GTK 图形工具包，是 Mate 项目（https://mate-desktop.org）的开发者。他在 GitHub（https://github.com/tesquash）和 Ubuntu MATE 社区（https://ubuntu.com/community/gordonsummer）上有多个公开项目。

2025 年 7 月

第 296 期

LINUX-MAGAZINE.COM

## DrupalCon

### 维也纳 2025

10 月 14 日 - 17 日

### 获取你的 DrupalCon 门票

维也纳 2025！

你是一个开发者、设计师、项目经理、代理机构负责人、托管提供商、技术创新者，还是渴望深入 Drupal 世界的学生？

来维也纳加入我们吧，度过为期四天的精彩学习、连接和贡献的时光！

### 期待内容：

- 充实的会议日程和 BoFs

- 主题演讲，包括 Driesnote、Drupal CMS 焦点以及 Web 2025

- 录制会议可用

- 社交活动：欢迎接待、狂欢之夜、女性开发者大会以及更多

- 与行业领袖、顶级创新者的交流

#### 单人

| 早鸟票 | 普通票 |

|---|---|

| 6 月 17 日前 | 805€ |

| 9 月 15 日 | 985€ |

| 晚期 | 1065€ |

| 10 月 16 日 | 85€ |

#### 团体票

| 早鸟票 | 普通票 |

|---|---|

| 6 月 17 日前 | 3900€ |

| 9 月 15 日 | 4775€ |

立即注册，不要错过欧洲盛事！

## 深度解析

### deorphan — 命令

管理 Debian 软件包

`deorphan` 工具帮助你跟踪基于 Debian 的系统的软件包和其他内容。Debian 以其软件包管理工具为特色。每个软件包管理器都有命令，但 `deorphan` 还有查找创建和安装软件包的功能。许多其他工具，如 `apt-cache`，已添加到 `apt`（`apt-get` 的精简版本）中，而 `deorphan` 则让你能够像它们那样进行查找。一个例子是 `deorphan` [1]，它能识别未使用的软件包。`deorphan` 对于释放空间非常有用，重要的是精确确定被留下的软件包，因为软件包管理命令不会删除它们。

通常将选项划分为四个部分。顶部部分列出了命令的选项，常用的 `--help` 和 `--version`。选项还包括 `-f`，供那些不想使用的人使用。第二部分输出修符，涵盖了更多实用的选项。通过此工具 `--show (-d) (-i)` 可以获得已安装软件包及其依赖关系的完整概述。通过其他选项，用户可以使用 `--priority (-j)` 修改软件包的优先级，如所示。使用 `--selection (-s)` 将显示在 Debian 仓库中可以找到软件包。第三部分搜索修符，涵盖了可以获取 `deorphan` 大部分的选项。

在某些情况下，你应该注意结果中的误报。顶部的列表是 `--all-packages`（图 3），它检查所有软件包，留下其他的。主页面建议使用 `--all` 可能会过度。使用单独的列表，`--list (-L)` 显示未包含在搜索结果中的软件包，可能是因为你想保留它们，或者它们可以安全地删除。无论位置如何，都可以通过编辑 apt 内部的选项找到文件。结果多种方式精炼，如表 1 所示的选项 `--keep-file(-K)`。使用 `apt --keep` 后跟空格分隔的软件包列表会将它们添加到列表中。同时，`--del (-k)` 会移除软件包。使用 `--mark` 移除文件的保留记录。你可以执行这样的操作并搜索该软件包名称和描述以确定它包含什么类型的文件。以下更改见表 2。然而，在关键库的情况下，应谨慎使用此选项。

如果 `deorphan` 值得使用，你也可以编写 `deorphan` [2]，它跟踪所有软件包，保留一个始终保留的软件包列表，特别是删除操作的功能。这两个命令极大地简化了软件包管理。

页面第四部分显示了 `/var/lib/keep` 的选项，该文件列出了要保留的软件包，或者通过选项 `--keep-file(-K)` 定义。当前列表是：

## 信息

- [1] https://man.debian.org/book/deorphan/en.html

- [2] https://man.debian.org/book/deorphan.en.html

### 表 1：搜索方法

| alsa-topography | main/utils | 充足 |

|---|---|---|

| | 为了给 deorphan |

| libasound-data | main/mail | akonadi-import-wizard | 更好的指导。 |

| alsa-ucm-conf | main/sound | alsa-oss | |

| libasound-data | main/sound | alsa-utils-gui | deorphan 以及 |

| bind9-lib | non-free/admin | amd64-microcode | debfoster |

| bind9-dnsutils | main/utils | aptamangelager | 起初，看起来 Debian 软件包 |

| | main/utils | apt-listchanges | 管理器没有移除 |

| | main/utils | apt-rebuilds | 随软件包的悬而未。然而，我们发现 |

| | gnome | blue | 可能一个依赖项 |

| | main/web | bluetooth | 可能会依赖另一个 |

| | main/utils | alsa-utils | 软件包和 |

| | non-free/admin | kernel | 检查何时 |

| | main/admin | blue-hicumd | 需要。 |

| | main/admin | blue-source | |

### 表 2：--guess-- 和 --no-guess-- 的选项

| common | 查找包含 --common 的软件包 |

|---|---|

| data | 查找包含 --data 的软件包 |

| deb | 查找包含 --deb 或 -y 的软件包 |

| dev | 查找包含 --no-dev 的软件包 |

| doc | 查找... |

| dummy | 查找描述中包含 dummy 或 transitional 的软件包 |

| kernel | 查找所有解释器，例如 Ruby, Pike, Python 和 Mono |

| Mono | 查找 Mono 模块 |

| perl | 查找 Perl 模块每 | 查找 Perl 模块 |

| pike | 查找 Pike 模块 |

| python | 查找 Python 模块 |

| ruby | 查找 Ruby 模块 |

| section | 查找被错误放在上面部分的库 |

| all | 尝试找到以上所有 |

| only | 完全忽略软件包的章节，并使用名称/描述（必须与上述 --guess-options 之一一起使用）。 |

## 安全保存

与 Basement 一起进行设计

# 光光临！

## 字符串与事物

使用这些工具处理事务的经历

# 特色

# 获取每一期 RASPBERRY PI GEEK

# 在一张完全可搜索的

# DVD 上！

### 特别赠送！

+ 2 本完整版特刊：

* 树莓派手册 (Raspberry Pi Handbook)

* 树莓派冒险 (Raspberry Pi Adventures)

# raspberry pi GEEK

## 树莓派手册

## 树莓派冒险

# raspberry pi GEEK

# raspberry pi GEEK

# raspberry pi GEEK

# raspberry pi GEEK

# raspberry pi GEEK

## 最非凡！终极树莓派存档 (THE ULTIMATE raspberry pi GEEK ARCHIVE)

## 创爱好者的圣地！

酷炫、多彩且充满创意的《Raspberry Pi Geek》杂志是全球创爱好者的最爱，因为你永远不知道会在里面发现什么。咖啡烘焙机？仓鼠的计步器？猫玩具的自动发射器？

RPG 深入探索了物联网宇宙的本质，研究了 MQTT、Mindstorms 和 3D 打印等技术。读者可以通过 Python、Minecraft、Scratch、PHP 和 Turtle Graphics 编程来学习，并在复古游戏、PyChess 和 littleBits 上磨练技能。

《Raspberry Pi Geek》已 2017 年停刊，但它的传奇在官方的树莓派存档（Raspberry Pi Archive）中延续——这是一份包含精美插图且易于访问的 PDF 格式完整合集！

超过 2,000 页的信息、项目和乐趣！另有额外版本！

# 立即购买 shop.linuxnewmedia.com

# 深度编程快照 – WebSockets

使用 WebSocket 连接实现浏览器即时刷新

## 快如闪电

WebSocket 协议帮助浏览器在服务器内容更改时立即重新加载页面。在本月的专栏中，Mike Schilli 用 Go 语言编写了一个 WebSocket 服务器来完成这项任务。

你可能想过，比如 WhatsApp 或 Slack 在你的浏览器中打开时，为什么能对对方“正在输入”的反馈响应如此迅速……这需要什么样的魔法？即使在消息发送之前，浏览器至少需要响应你正在查看的页面，但它是如何知道何时关闭连接的？相反，浏览器使用 WebSocket 与特定服务器建立一个持久连接。一旦建立，服务器和客户端就可以向对方发送消息，连接另一端的服务器可以获取这些消息。换句话说，双方都在连接上主动监听，并在任何新信息到达时做出反应。

## WebSocket 的起源

WebSocket 协议首次于 2011 年面，当时 RFC 6455 已经包含了如今所有 WebSockets 的内置支持。为了提供事实上的艺术感并在不引起烦刷新的情况下显示新到达的信息（就像 WhatsApp 一样），HTML 代码在页面加载时连接到 WebSocket 服务器。在最简单的情况下，浏览器可以定期询问服务器，但这会产生不必要的网络流量——毕竟，这还会导致大型静态页面的闪烁，看起来非常不专业。更好的方法是设置服务器，仅当服务器端的文件发生变化时才主动通知浏览器。与 HTTP 协议不同，浏览器将不再发送请求

## 作者

Mike Schilli 在加利福尼亚州旧金山湾担任工程师。在他每月的专栏中，他自 1997 年以来一直在介绍各种编程语言的实际应用。如果通过 `mschilli@gmail.com` 联系他，他将乐意回答你的任何问题。

```
fyne Create apps Toolkit in Go ...
gopher 9:27 AM
上面的代码来自 Jon Orchen 的沙盒：...
Jon Orchen 我修改了代码来创建这个：
{
  但窗口的内容不是空的。我在做什么？（错误）
}
Any Writer
你不能包含元素 容器的大小由父级设置。它由设置或使用 canvas getter 来控制你的代码控制大小 Any Writer 正在输入 ...
```

图 1：网页浏览器中的 Slack 使用 WebSockets 进行实时通信。

58 2025 年 7 月第 296 期 LINUX-MAXIMUM.COM

# 深度编程快照 - WebSockets

第一次。JavaScript 随后出现在事件循环中，等待通道上的新消息。在接收到浏览器文档对象模型 (DOM) 时通过从来自不同主机的服务器重新加载内容来更新显示的页面，但它不必这样做。

为了让这发生，List 导出了 `watch(cb)` 函数，它期望一个路径数组作为第一个参数；第二个参数是回调函数 `cb`，它会在内核的 `notify` 命令触发时调用

## 双向
