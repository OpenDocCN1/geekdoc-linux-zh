
| 功能 | | | |
| :--- | :--- | :--- | :--- |
| 使用电子邮件地址注册 | 是 | 是 | 是 |
| NSFW 选项 | 是 | 否 | 受限 |
| 支持 2FA | 是 | 是 | 是 |
| 支持自有服务器 | 是 | 是 | 是 |
| 支持封闭群组 | 是 | 是 | 是 |
| 个人档案转移 | 是 | 是 | 是 |

#### 信息

- [1] ActivityPub: https://www.w3.org/TR/activitypub/
- [2] Diaspora: https://diasporafoundation.org
- [3] Friendica: https://friendi.ca
- [4] Friendica 安装: https://friendi.ca/resources/installation/
- [5] Mastodon: https://joinmastodon.org
- [6] Mastodon 文档: https://docs.joinmastodon.org/user/run-your-own/

## Linux Magazine

`Linux Magazine` 是你通往 Linux 世界的指南。打开期刊，你会发现你无法在别处找到的高级技术信息！

### 通过以下内容扩展你的 Linux 技能

- 关于热门话题的深度文章，包括比特币、勒索软件、云计算等！
- 关于节省时间和保护数据的有用工具的指南和教程
- 故障排除和优化技巧
- 关于开源领域关键发展的深入新闻
- 针对树莓派、Arduino 和其他创客板系统的酷炫项目

如果你想走得更远，用 Linux 做更多，请立即订阅，不要错过任何一期！

### 立即订阅！

`shop.linuxnewmedia.com/subs`

**立即获取！我们的 PDF 版提供快速配送**

![订阅](img/b40e8bf6cf651f8eebf36f5265123095_34_0.png)

## 使用 Bash 进行简单的网络抓取

### 滑雪报告

通过一行 `Bash` 代码，`Pete` 抓取网络并构建了一个桌面通知应用，以获取每日降雪报告。**作者：`Pete Motaiffe`**

最近在进行一个小项目时，我惊讶地发现仅用一行 `Bash` 就能进行如此多的网络抓取。我使用了基于文本的 `Lynx` 浏览器 [1]，然后将输出通过管道传递给 `grep` 搜索。图 1 展示了抓取 `Sunshine Village` 降雪预测网页上当前积雪深度的一行 `Bash` 示例。

在本文中，我将介绍一些轻松抓取网页的技术，然后我将创建一个提供每日降雪预报的桌面通知脚本。

### `Lynx` 文本浏览器

对于我的 `Bash` 网络抓取，我一开始查看使用 `curl` [2] 和 `html2text` [3] 实用工具等命令行工具。这种技术确实有效，但我发现使用 `Lynx` 浏览器可以提供一步到位的解决方案，并产生稍微更干净的文本输出。

要在 `Raspbian/Debian/Ubuntu` 上安装 `Lynx`，请使用：

```bash
sudo apt install lynx
```

`Lynx` 的 `-dump` 选项会将网页输出为文本，并去除 `HTML` 标签、`HTML` 编码和 `JavaScript`。图 2 显示，`Lynx` 转储可以大大清理原始网页，使搜索变得更加容易。有时一个简单的 `Bash` `grep` 搜索就足够了。然而，有很多情况需要一些文本操作。好消息是，`Bash` 拥有一系列不错的行和字符串操作工具。

图 3 中显示的示例使用行操作来查找佛罗里达州 `Key West` 的当前天气。对字符串 `"As of"` 进行 `grep` 搜索，并使用选项 `-B 3` 返回所需的数据行以及额外的三行行。如果需要，你可以使用 `tail` 命令删除 `"As of"` 行。重要的是要注意，你在网页上看到的内容可能与 `Lynx` 输出的文本不匹配，可能需要一些试错测试。

图 4 使用字符串操作来查找 `Sunshine` 滑雪场的新雪。该滑雪场的网页使用 `JavaScript` 以厘米或英寸显示新雪量，但 `Lynx` 文本输出同时显示这两个值及其单位。

要删除字符串变量的部分，你可以使用 `%` 来提取字符串的第一部分，使用 `#` 来提取字符串的最后一部分（如清单 1 所示）。

### 一个 `Bash` 网络抓取项目

为了在家庭滑雪之旅前兴奋起来，我想创建一个早晨通知脚本，显示新雪量和基础积雪。

为了创建通知脚本（清单 2），我使用了 `Lynx` 实用工具的两次传递。第一次抓取新雪量（如图 4 所示），然后第二次获取新的基础积雪（如图 1 所示）。然后，降雪结果作为字符串 (`$msg`) 传递给 `notify-send` 实用工具 [4]，该工具将消息发布到工作站桌面（图 5）。你可以使用 `cron` 或 `at` 实用工具安排此 `Bash` 脚本每天早上运行。

### 摘要

抓取网页可能很棘手，而且页面随时可能改变。因此，在查看网络抓取之前，最好始终检查是否可用 `API`。

使用 `Beautiful Soup` 库的 `Python` 一直是我的网络抓取首选方法，但知道也有一个简单的 `Bash` 替代方案是很棒的。

#### 信息

1. `Lynx`: [https://lynx.invisible-island.net/](https://lynx.invisible-island.net/)
2. `curl`: [https://curl.se/](https://curl.se/)
3. `html2text`: [https://github.com/Alir3z4/html2text/](https://github.com/Alir3z4/html2text/)
4. `notify-send`: [https://delightlylinux.wordpress.com/2020/10/25/bash-show-notifications-from-scripts-using-notify-send/](https://delightlylinux.wordpress.com/2020/10/25/bash-show-notifications-from-scripts-using-notify-send/)

### 作者

你可以在 [https://funprojects.blog.](https://funprojects.blog.) 探索 `Pete Metcalfe` 和他的女儿们的更多有趣项目。

#### 清单 1：提取字符串的部分

```bash
01  newsnow='5.8cm2.0'
02  # 获取 'cm' 之前的部分
03  echo "${newsnow%*cm}"
04  5.8
05  # 获取 'cm' 之后的部分
06  echo "${newsnow#*cm}"
07  2.0
```

#### 技术亮点一览

太忙而没有时间阅读新闻稿和琐碎的技术新闻网站？让我们将最相关的新闻、技术文章和工具技巧直接发送到你的收件箱。

- `Linux Update`
- `ADMIN Update`
- `ADMIN HPC`

掌握 IT 行业的脉搏。

`ADMIN` 和 `HPC`: `bit.ly/HPC-ADMIN-Update`

`Linux Update`: `bit.ly/Linux-Update`

#### 清单 2：`Bash` 网络抓取通知脚本

```bash
01 #!/bin/bash
02 #
03 # skitrip.sh – 在通知中显示 Sunshine 的滑雪状况
04 #
05 theurl="https://www.snow-forecast.com/resorts/Sunshine/6day/mid"
06
07 # 获取新雪深度
08 thestr="New snow in Sunshine Village:" 
09 result=$(lynx -dump "$theurl" | grep "${thestr}")
10 newsnow="${result%cm} cm"
11
12 # 获取基础积雪
13 thestr="Top Lift:" 
14 base=$(lynx -dump "$theurl" | grep "${thestr}") 
15
16 # 在桌面通知中显示结果，等待时间为 120 分钟
17 msg="$newsnow\n$base" 
18 icon="$HOME/Downloads/mountain.png"
19 notify-send -t 120000 -i "$icon" "Sunshine Ski Resort" "$msg"
```

## 像专家一样思考

**《Linux Shell 手册 2022 年版》**

这一新版内容充实，涵盖了用于配置和故障排除系统的最重要实用程序。

![](img/b40e8bf6cf651f8eebf36f5265123095_38_0.png)

以下是书中部分内容的预览：

- 定制 `Bash`
- 正则表达式
- `Systemd`
- `Bash` 脚本编程
- 网络工具
- 还有更多！
