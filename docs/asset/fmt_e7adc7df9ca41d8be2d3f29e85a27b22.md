
在关闭笔记本电脑之前，请记住将日志文件保存到 USB 拇指驱动器（或其他外部来源），如果你之前没有直接从那里运行 Kismet 的话。记住，当运行 live CD 时，日志文件被保存在临时 RAM 磁盘上，这在你关闭笔记本电脑电源时不会被保存。

## 管理你的结果

你从第一次 wardrive 回家，收集了数百（甚至可能数千）个网络。现在，你确切地打算用这些数据做什么？希望正如我们在上一节中解释的那样，你心中有一个目标。如果你将 wardriving 作为渗透测试的一部分，你可能希望仅解析出目标地点附近的那些网络。或者，你可能有兴趣编译你收集到的网络统计数据：信道使用情况、加密等。无论如何，考虑将你的数据上传到 WiGLE.net。

### WiGLE

WiGLE.net（无线地理日志引擎）是一个在线数据库，拥有超过 1500 万条记录的无线网络，大多数都带有地理坐标。WiGLE 为你提供服务集标识符（SSID）和制造商统计、八位位组及信道使用统计，以及一个可浏览的世界网络地图。通过创建账户，你可以上传和追踪你记录的日志网络，并被记为首先发现某些网络的人。

### 获取 BackTrack

- 你可以直接从 `http://www.remote-exploit.org/backtrack_download.html` 或通过 torrent 下载。
- 务必检查 MD5 哈希值，以确保你的下载未被篡改或无错误。
- 以较慢速度（4x–8x）刻录 BackTrack ISO 以获得更好的结果。

### 配置 Kismet

- 务必使用受支持的网卡（详见 `http://www.kismetwireless.net/documentation.shtml`）。
- 确保启用捕获源，可以通过编辑 `/usr/local/etc/kismet.conf` 文件或通过命令行来操作。
- 从你希望保存日志文件的位置启动 Kismet。
- 切勿让无线网络探测干扰安全驾驶。合上笔记本电脑盖子以抑制查看屏幕的冲动。
- 在进行无线网络探测时，请遵守 RenderMan 的“探测者伦理”。

# 使用 Kismet 进行无线网络探测

- 确保启用捕获源，可以通过编辑 `/usr/local/etc/kismet.conf` 文件或通过命令行来操作。
- 从你希望保存日志文件的位置启动 Kismet。
- 切勿让无线网络探测干扰安全驾驶。合上笔记本电脑盖子以抑制查看屏幕的冲动。
- 在进行无线网络探测时，请遵守 RenderMan 的“探测者伦理”。

# 索引

## A

Advance Packaging Tool (APT)，50

Aircrap 无线网卡适配器，175–177

`apt-get` 命令，50

`apt-get install` 命令，174

Asus eePC 安装

- Kismet 安装，172–173
- 工具安装，173–175

Asus WL-500g Prëmium 路由器，178

Atheros 芯片组，53

Atheros mini PCI 卡，178

Atmel 芯片组，53

autoft，默认排序模式，87

## B

BackTrack

- 启动，243
- 刻录到 CD，242
- 下载页面，240
- MD5 哈希计算，241

Backtrack，Live 发行版，41

Basic Service Sent Identifier (BSSID)，88, 105, 153, 167

Bluetooth，13

buildroot 工具，205

## C

Caceteck 工具，175–176

channel hopping（信道跳跃），196–198, 216

fine-tune（微调），124

`client_manual` 文件，97–98

color-coding（颜色编码），Kismet 界面，91, 113

color scheme（配色方案），168

command-line switches（命令行开关），168–169

cross-compiling process（交叉编译过程），189

Cygnwin 库，176

## D

Darwin’s speech functionality，166

DeepBurner 程序，242

Dr.GrEeN 脚本，233

driver program（驱动程序），50

drone（无人机/探针），188. 参见 Kismet drones

dumb kismet client interface，110–111

## E

Electronic Numerical Integrator and Computer (ENIAC)，6

Enhanced Specialized Mobile Radio (ESMR)，10

`/etc/config/network` 文件，180, 199

`/etc/init.d/S60kismet_drone` 文件，197

`/etc/init.d/S70WL_scan` 文件，196

`/etc/kismet/kismet.conf` 文件，181

`/etc/kismet/kismet_drone.conf` 文件，193, 200

Ethernet. See Local Area Network (LAN)

EXT3 文件系统，182

## F

firmware-based network discovery tools（基于固件的网络发现工具），131

flags（标志），154

## G

gkismet 界面，108

Global Positioning Systems (GPS)，92, 103, 107, 165

- applications
    - mapping and wireless（地图绘制与无线），12–13
    - public safety（公共安全），10–11
- and kernel（与内核），21
- receiver, in Kismet
    - disadvantages（缺点），74–77
    - plug and null modem（插头与空调制解调器），77–78
- signal measurement（信号测量），72
- software used（使用的软件），73–74

GPSD interfaces，127

`gpsd -p /dev/ttyS0` 命令，74

`gpsd -p /dev/ttyUSB1` 命令，74

`gpsdrive/` 目录，138

Gpsdrive，导航系统，137–138

- homepage（主页），229
- installation（安装），229–230
- Kismet + GpsDrive + MySQL，233
- mapping（地图绘制），234–235
- MySQL support（MySQL 支持），231–233

`gpsd` 软件，72–74

GPSMap

- features（特性），224
- patching（补丁），225

Graphical User Interface (GUI)，151

## H

Hermes II chipsets，53

hostap-compatible cards，120

## I

IGiGLE 界面，227

Irongeek’s WiGigLE WiFi Database to Google Earth Client for Wardrive Mapping (IGiGLE)，227–228

## K

Kamikaze OpenWRT

- allowedhosts 参数，200
- enable 参数，202
- LAN 配置，199
- `start` 命令，202
- `ul` 命令，204

KisMap, python-based tool. See GPSMap

Kismet

- complete setup（完整设置），78–80
- configuration
    - booting BackTrack（启动 BackTrack），243
    - GPS receiver，245
    - `kismet.conf` 文件，56
    - log file configuration（日志文件配置），245
    - madvifi-g_wifi0,ProximBG source，59
    - none.none.addme source，58
    - suiduser and user root，56–57
    - wireless card configuration（无线网卡配置），244–245
- C and C++ program，41–42
- customizing panels interface
    - client list window（客户端列表窗口），96, 106
    - customizing colors（自定义颜色），107
    - modified network list window（修改后的网络列表窗口），106
- definition（定义），84
- GPS receiver
    - disadvantages（缺点），74–77
    - plug and null modem（插头与空调制解调器），77–78
    - signal measurement（信号测量），72
    - software used（使用的软件），73–74
