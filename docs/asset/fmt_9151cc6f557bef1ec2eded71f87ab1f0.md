
`-a` (archive) 选项将文件推送到服务器，这会开启详细模式，`-p` 是 `--progress` 的缩写。如果传输被中断，yoyo 会在目标服务器上保留部分文件，`--progress` 显示过程每。当调用时图 4：具有两秒超时和最多两次尝试的 yoyo 运行。yoyo 也会终止。在图 5 中，`git pull` 变长后，yoyo 的监控

| 进度 | 大小 | 速度 |
|---|---|---|
| 写入对象 | 80% (16/20) | 44.17 MB | 49.00 Ki/s |
| 写入对象 | 80% (16/20) | 44.38 MB | 50.00 Ki/s |
| 写入对象 | 80% (16/20) | 44.42 MB | 50.00 Ki/s |
| 写入对象 | 80% (16/20) | 44.55 MB | 51.00 Ki/s |
| 写入对象 | 80% (16/20) | 44.68 MB | 51.00 Ki/s |
| 写入对象 | 80% (16/20) | 44.80 MB | 54.00 Ki/s |
| 写入对象 | 85% (17/20) | 44.88 MB | 54.00 Ki/s |
| 增量对象 | 85% (17/20) | 44.93 MB | 32.00 Ki/s |

超时。正在关闭。
重启中...
正在计算对象: 25, 完成。
正在计数对象: 4% (1/25)
正在计数对象: 8% (2/25)
正在计数对象: 12% (3/25)
正在计数对象: 16% (4/25)
正在计数对象: 20% (5/25)
正在计数对象: 24% (6/25)
正在计数对象: 28% (7/25)
正在计数对象: 32% (8/25)
正在计数对象: 36% (9/25)

yoyo 监控重试过程以查看它是否持续产生输出。如果由于服务器缓慢而没有任何发生，yoyo 将中止并重启，无需进一步延迟，除非有自定义函数。注意，yoyo 期望的是完整路径，与 shell 不同。这正是医生所匹配的，并允许人类专注于活跃工作，得益于图 5：在 `git pull` 停滞后，yoyo 活了它。

信息
- Expect: https://github.com/mitwating/expect

## 在树莓派上玩老游戏
*作者：Erik Baerwald*

许多用户仍然喜爱旧 DOS 游戏，也许正是因为它们像素化的图形、哔哔声和断断续续的音乐。当然，先进的 PC 为旧的 16 位操作系统安装游戏用处不大。安装通常失败，硬件太快了，而且系统不再支持 SoundBlaster 16 声卡或软盘驱动器等组件。DOS 运行环境和模拟器需要在 Linux 上运行像 DOBox 或 DOSBox 这样的设置来运行旧游戏。

由于对于 20 世纪 80 年代和 90 年代 16 位操作系统有用的旧电脑越来越稀少，树莓派是玩旧游戏的很好的替代方案。配合意大利程序员 Carmelo Mailinto 开发的 Dosbian [1]，它提供了一个成熟且易于部署的解决方案。要在 Dosbian 上运行，建议使用带有额外内存的树莓派 4，因为这些游戏的软件需要大量的内存容量。Dosbian 没有列出其他要求。操作系统会自动检测所需的硬件（如 USB 网络硬件和显卡），并分配资源以进行匹配。此外，Dosbian 的当前版本允许你生成设计容量高达 32GB 的软磁盘和硬盘存储。

### 前提条件

树莓派上的 Dosbian 在资源方面要求不高。操作系统可以在树莓派 2 上运行，尽管需要对配置进行一些修改才能流畅运行。所有较新的小型计算机 (SBC) 都能支持 Dosbian，然而，对于 Windows

### 设置

Dosbian 基于 Raspberry Pi OS 和 DosBox。由于该发行版专门为 Dos 软件定制，不建议使用传统的桌面系统。你可以从项目网站选择在具有 3GB 内存的 Pi 上的 32 位架构。你可以将镜像传输到 SD 卡（例如，使用树莓派镜像或 Linux `dd` 命令）。与 Raspberry Pi OS 不同，Dosbian 将你进入 DOS 提示符而不是图形界面。Dosbian 模拟一个以 66MHz 运行的 8486 CPU。操作系统在后台启动预配置的 DosBox [2]。

## 树莓派上的旧 DOS 游戏

DOSBox 版本 1.5 - MENU

使用方向键移动

- 1 START MY SUPER 606X: 你选择作为默认
- CONFIGURATION HELPER: 帮助你完成首次配置
- DOSBOX CUSTOMIZATION: 更改启动屏幕，在启动时禁用哔哔声
- UPDATE DOSBOX: 保留你的默认 DosBox 发行版（需要网络连接）

```
>> OPTIONAL PACKAGES <<

ROLAND-32: 安装模拟器
```

# 在 Pi 上运行 MAKESPACE 经典游戏

已安装的应用程序可以通过开始菜单调用，以便在提示符时切换目录。此外，你可以在 Dosbian 中配置 LaunchBox，使其在启动时自动运行，甚至跳过提示符。

要将 LaunchBox 设置为系统启动后的启动屏幕，请使用命令退出 DOS 并在 Dosbian 配置对话框中选择该选项。

现在将 LaunchBox 设置为启动屏幕，并在提示符后打开一个窗口。重启后，最初你将只会在菜单中看到两个已安装游戏的列表。要添加更多游戏或应用程序——请使用鼠标点击应用程序内存的顶部。

在“Title（标题）”框中，输入你希望在菜单中作为星标显示的标题。在“Run Commands（运行命令）”框中，输入你通常用于启动新游戏或应用程序的命令。如果你不知道确切的命令，点击右侧带有小型文件管理器图标的“Browse（浏览）”按钮，在其中你可以点击目录结构来选择并选择可执行文件。“Configure（配置）”框还列出了额外的可选参数（例如，如果你需要在项目文件夹中添加额外文件）。然后你可以通过点击字段右侧的“Browse”按钮来选择它们。

点击右下角的“Details（详情）”按钮可以编辑应用程序的元数据（查看“Search（搜索）”框了解为什么这是一个好主意）。

生成、发布和发行年份。如果你勾选“Favorites（收藏）”框，会将该条目选为收藏，它现在将出现在选择菜单的最上方。完成这些步骤后，新游戏或应用程序将出现在 LaunchBox 主菜单中（图 4）。

# 搜索

如果你在主菜单中添加了大量游戏，可以通过底部选项使用关键词过滤列表——假设你为搜索输入了一些元数据。Tab 键允许你按类型顺序向前向后跳转到各个类别。例如，类型栏中的游戏将过滤你添加的游戏列表。选择其中一个类型并按回车键，该软件将跳转到一个新列表，仅显示符合标准的条目。按回车启动所选的游戏。

在许多情况下，具备 Linux 和 DOS 的知识可以跳过提示符，且不需要任何关于命令参数的知识。如果你想使用原本为 DOS 设计的软件，树莓派 上的 Dosbian 是旧硬件的替代方案，后者效率低下且容易损坏。

# Info

- 1) Dosbian: https://cmaiolord.wordpress/dosbian/
- 2) DOSBox: https://www.dosbox.com

# 结论

Dosbian 在日常使用中留下了持续良好的印象。该系统是开箱即用的，在我们运行几个游戏时没有出现任何稳定性或速度问题。Dosbian 也是资源限制的人士的极佳选择。

图 3：使用编辑对话框配置 LaunchBox 菜单项。

图 4：LaunchBox 让你能够创建一种启动系统中已安装游戏的简单方法。

## 快速上手 Linux

想让你的朋友和同事切换到 Linux 吗？

本单期向初学者介绍了如何：

- 安装 Linux
- 下载并安装适用于 Linux 系统的免费软件
- 玩游戏
- 创建文档和电子表格
- 处理照片
- 播放音乐和视频以及更多！

在线订购：shop.linuxnewmedia.com/specials

## 制作空间
使用简单的 Gemini 协议进行轻量级网络通信

创建 Gemini 页面以显示传感器数据或控制树莓派漫游车。作者：Pete Metcalfe

Gemini 协议 [1] 是一种用于访问远程文档的较新网络协议。与包含层样式表、JavaScript 和 HTML 标签的 HTML 页面不同，Gemini 文档是一个简单的易读文档。Gemini 的格式非常容易学习，仅有五种代码。新编码人员无需任何编程技能即可轻松组装出一个小型通信服务器或客户端。

在篇文章中，我将通过三个项目介绍 Gemini 协议。第一个项目仅需一行代码即可创建一个 Gemini 服务器。在第二个项目中，一个 Bash 脚本创建一个通用网关接口（CGI）页面，连接到服务器存储温度数据。第三个项目使用 Gemini 链接

## 列表 1：Gemini 文档

```
## 一级标题 (H1)

## 二级标题 (H2)

### 三级标题 (H3)
```

-> 另一个页面的链接

> 这一行将作为区块显示

- 列表
- 这是第一个列表
- 这是另一个列表

# 入门

任何文本编辑器都可以创建 Gemini 文档。Gemini 格式有点像 Markdown 的精简版。Gemini 文档的扩展名为 `.gmi`。列表 1 中的示例文件 `.gmi` 显示了所有的 Gemini 代码，包括标题（三级）、链接、列表和预格式文本。我将展示预格式文本用于 ASCII 艺术和 Bash 命令。

## 代码或 ASCII 块

```
/ / / / / / / / / / / / /
```
代码或 ASCII 块

图 1：Gemini 客户端中的示例文档。

## 服务器与客户端

对于基本测试，可以使用一行 Bash 脚本作为 Gemini 服务器或客户端。Gemini 协议通常使用套接 (SSL) 和传输层安全 (TLS)加密。需要 Bash `ncat` 工具（注意：该命令不支持 SSL）。提供单个页面的 Bash 代码为：

```
while true; do
echo -n "Content-Type: text/gemini\r\n"
cat page1.gmi | ncat -p 1984 --done
```

当收到请求时，此 bash 会输出 Gemini 内容类型（text/gemini）并 (`cat`) 示例文件。`ncat` 工具使用 (`-l`) 在端口 1965（Gemini 默认端口）接收请求。连接到 Gemini 服务器的脚本为：

```
echo "gemini://192.168.0.105" | ncat --ssl 192.168.0.105 1965
```

Gemini 客户端开始使用“gemini://<请求的地址>”。此脚本启用了 SSL (`--ssl`) 并定义了 Gemini 服务器的 IP 和端口。此 Bash 客户端语句

## 动态 Bash日期

与其使用 `cat` 语句列出静态文件，不如调用脚本来

图 3：连接到树莓派的 BME280 传感器。

## Gemini 协议

图 2 显示了 Bash 服务器的输出，该服务器位于 Jetforge 主主目录下。

图 4 显示了一个读取传递给 Cowboy 的温度和湿度变量的示例。

列表 3，(sh) 显示了在 Cowboy ASCII 艺术下方创建一个带有预格式化模式的 Gemini 页面（图 5）的 Bash 代码。

## 传感器项目

Gemini 格式不支持图形，但你可以使用 ASCII 艺术。对于我的项目，目标是使用一些 ASCII 艺术显示传感器数据，以及一个笑话或每日运势。

最后一步是安装 `fortune` 工具：

一个好的传感器应该是易用的。我使用了一个 BME280 传感器（约 $15），它可以返回温度、压力和湿度测量值。BME280 使用 I2C 总线连接到树莓派上的 SDA、CL、GND 和 S3。

## 漫游项目

Context 不像网页那样支持按钮和表单；可以使用简单的文档链接来传递参数信息。对于漫游项目，我在文档链接中以字符串的形式传递操作（action）和主机（master）。

```bash
sudo apt install cowboy
```

使用单行 Bash 服务器的局限性之一是创建多个 Gemini 页面很麻烦。幸运的是，有很多轻级的 BME280 传感器。不过，我使用基于 Python 的服务器运行在树莓派 [3] 上解决了硬编码问题。

图 6 显示了源文件以及文档链接中带有查询字符串的 Gemini 页面 (`cg.sh`)。例如，链接传递参数将第一个定义为 0，第二个定义为 1，将操作语句设置为 reader。

BME280 Python 库还带有一个读取传感器数据的命令行工具。安装该库和 `read_bme280` 工具：

```bash
## pip install bme280
## read_bme280 --i2c-address 07
101.26 hPa
22.62 %
21.24 C
## 检查传感器地址：
```

```bash
pip install fortune
fortune --dir /home/pi/temp --host "0.0.0.0" --hostname $(hostname) - &
```

`cowboy` 是一个以 ASCII 艺术形式存在的命令行工具。使用以下命令安装它：

## 列表 2：Gemini 文档示例

## 列表 3：Gemini 文档示例

```bash
#!/bin/bash
## show.data "20 text gemini"
## weather.sh - 将 BME280 传感器发送到 Gemini 页面
echo "VSTAT"
echo "$(date)"
echo ""
## 为 ASCII 设置 Gemini 格式
echo "<pre>"
echo "cowboy is today is $fortune with $humidity"
echo "</pre>"
echo "</html>"
```

```bash
## 使用 read_bme280 工具获取天气
temp=$(read_bme280 --i2c-address 07 --temperature)
humidity=$(read_bme280 --i2c-address 07 --humidity)
```

```bash
# 输出 Gemini 页面
echo "20 text gemini"
# 注意：某些 Gemini 服务器可能会执行此操作
echo "<pre>"
# 设置预格式模式
echo cowboy is today with $fortune
echo "</pre>"
# 每日笑话/运势
```

# 在 bash 中在 cowboy 中显示数据
temp=$(read_bme280 --i2c-address 07 --temperature)
humidity=$(read_bme280 --i2c-address 07 --humidity)
cowboy Today is: $temp with $humidity
```

Today is: 21.22 C | 24.92 % humidity | |

| Zein | |

| :--- | :--- |

| Today is: 21.38 C | 24.17 % humidity |

![](img/31162a00ee46c5d590c544cb2d944405_63_0.png)

你有犯错的能力。你今天会学到很多。

# 图 4：Cowboy 中的传感器数据。

# Gemini 协议 MAKERSPACE

不建议直接连接到树莓派——因为大型设备需要的功率超过了树莓派能提供的，而且电源浪涌可能会损坏树莓派硬件。可以使用多个树莓派电机或继电器来停止我的设置：引脚 24 上的左电机和引脚 29 上的右电机。要将 GPIO 设置为输出，我手动使用树莓派 GPIO 引脚。通过以下命令安装 `gpi` 工具：

```bash
git clone https://github.com/WiringPi/WiringPi.git
/build
```

对于这个项目，我使用了 Pimoroni Explorer HAT PRO（约 $23）、一个 Arduino 底盘（约 $15）和一个充电器。左侧电机引脚的连接将适用于你的设置。

24 是引脚号。为了让 Gemini 看起来更好看，我使用了 ASCII 链和 fidget 工具 (4) 来生成

| 文件 | 编辑格式 | 运行选项 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | //bash | | | |
| # | .sh -- 在查询中查看命令 | | | |
| # | Gemini context 和页面的其余部分 | | | |
| # | echo "test" | | | |
| # | echo "Query" | | | |
| # | echo "$QUERY_00716" | | | |
| # | echo "$QUERY_00716" | | | |
| # | echo "Pass document" | | | |
| # | echo "QUERY_STRING" | | | |
| # | echo "${QUERY_STRING:1}" | | | |
| # | echo "${QUERY_STRING:1}" | | | |
| # | echo "Action statement ${QUERY_STRING:3}" | | | |
| Ln 13 Col 12 | | | |

![](img/31162a00ee46c5d590c544cb2d944405_64_0.png) gpi 24

![](img/31162a00ee46c5d590c544cb2d944405_64_1.png) 图 6：解析文档。# shop.linuxmedia.com 发现并投资 New Media 的解决方案。你想订阅报刊亭的内容吗？shop.linuxmedia.com

![](img/31162a00ee46c5d590c544cb2d944405_64_2.png)
