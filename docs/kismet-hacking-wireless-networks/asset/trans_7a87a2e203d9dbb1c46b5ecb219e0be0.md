
# 使用 Kismet 进行无线网络探测

- 确保启用捕获源，可以通过编辑 `/usr/local/etc/kismet.conf` 文件或通过命令行来操作。
- 从你希望保存日志文件的位置启动 Kismet。

- 切勿让无线网络探测干扰安全驾驶。合上笔记本电脑盖子以抑制查看屏幕的冲动。
- 在进行无线网络探测时，请遵守 RenderMan 的“探测者伦理”。

# 索引

## A

Advance Packaging Tool (APT)，50

Aircrap 无线网卡适配器，175–177

apt-get 命令，50

apt-get install 命令，174

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

client_manual 文件，97–98

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

/etc/config/network 文件，180, 199

/etc/init.d/S60kismet_drone 文件，197

/etc/init.d/S70WL_scan 文件，196

/etc/kismet/kismet.conf 文件，181

/etc/kismet/kismet_drone.conf 文件，193, 200

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

gpsd -p /dev/ttyS0 命令，74

gpsd -p /dev/ttyUSB1 命令，74

gpsdrive/ 目录，138

Gpsdrive，导航系统，137–138

- homepage（主页），229
- installation（安装），229–230
- Kismet + GpsDrive + MySQL，233
- mapping（地图绘制），234–235
- MySQL support（MySQL 支持），231–233

gpsd 软件，72–74

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
- start 命令，202
- ul 命令，204

KisMap, python-based tool. See GPSMap

Kismet

- complete setup（完整设置），78–80
- configuration
    - booting BackTrack（启动 BackTrack），243
    - GPS receiver，245
    - kismet.conf 文件，56
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
- graphical front end，35–37
- information panel，86, 93
- Linux installation，23
    - APT，50
    - card driver and chipsets（卡驱动与芯片组），50–54
    - configure 命令，46–47
    - make dep, make, and make install 命令，47–49
    - server running，60–61
    - source code，43–45
- log files，27
- monitor installation，184
- ncurses/panels interface，84
- network list panel
    - color-coding（颜色编码），91, 113
    - column descriptions（列描述），88
    - Global Positioning System (GPS)，92, 94, 103
    - Service Sent Identifier (SSID)，88–89, 92
    - sort options（排序选项），87–88
- omni-directional antenna
    - gain levels（增益级别），68–69
    - with magnetic mount base（带磁吸底座），67–68
- panels interface，84–85, 104
- pigtails，70–71
- pop-up windows display
    - client details window（客户端详情窗口），99
    - client list window（客户端列表窗口），96, 106
    - columns description（列描述），105
    - network details window（网络详情窗口），95, 98, 105
    - network location display（网络位置显示），104
    - packet rate window（数据包速率窗口），99
    - packet type display（数据包类型显示），100
    - statistics display（统计显示），102
    - wireless card power display（无线网卡功率显示），103
- server connection，36
- source variable，26
- status panel，93–94
- third-party tools for，111
- user interface
    - file type，64
    - play sound，66
    - splash screen，65–66
- wardriving
    - client List，34
    - GPS data，249

hacking components，178–179

help Interface，35

ipkg 命令，181–182

LAN configuration，181

Law enforcement officers，247–248

network details，33

network detection，249

process ID file，30

router configuration，179–180

sort options，32

WiGLE.net online database，250

in Windows system

- installation，176–177
- troubleshooting，177

kismet_client 命令，143

kismet_conf 文件，25, 27, 56, 174, 176, 194, 204, 213

Kismet config file，116–117

kismet-dev 目录，174

kismet_drone.conf 文件，193–194, 213–214

kismet-drone 文件，120

Kismet drones

- buildroot installation
    - Message Digest 5 (MD5)，210
    - PKG_VERSION，210
    - target system and Makefile，206
- troubleshooting，211–212
- channel hopping，196–198
- cross compiling process，205
- Kamikaze OpenWRT，198–200
- Linksys WRT54G，188
- OpenWRT and buildroot tool，205
- PC drone configuration
    - channel hopping，216
    - command-line switches，220
    - defaultchannels 参数，219
    - hostap-compatible cards，216
    - kismet_drone.conf 文件，214
    - make install 命令，212
- sourcechannels 参数，217–220
- server configuration
    - hop channels and command line，196
    - run and config file，194–195
    - troubleshooting，197–198
    - wl 命令，196–197
- Whiterussian OpenWRT
    - BOOT_WAIT 参数，192
    - ipkg 命令，192–193
    - jffs and squashfs 文件系统，191
    - wl 命令，193

Kismet Earth, mapping tool，235

Kismet parameters. See Kismet server

Kismet-Sep-26-2006-1.gps，141

Kismet server，116–117

- airjack tools，131
- alert patterns，129
- allowedhosts 参数，152
- channel hopping，120, 122–124
- client line parameters，161–164
- column line parameters，153–160
- command-line parameters，117, 134, 164–165
- command-line switches，143, 146
- configdir 参数，143
- decay 参数，152–153
- default channels 参数，124
- enableessources 参数，145
- festival line parameters，166
- fuzzydecrypt 参数，141
- GPSD interfaces，127
- gpsdrive 目录，138
- hostap-compatible cards，120
- limitations，120
- logdefault 参数，141, 144
- logexpiry 参数，133–134
- scripts
    - /etc/init.d/gps，183
    - /etc/init.d/kismet，183–184
- serwaname 参数，117
- sourc channels 参数，125
- speech_encrypted 和 speech_unencrypted 参数，167–168
- speech_unencrypted 参数，137
- traffic decay，152
- types of log files，138, 145

Kismet's native mapping tool. See GPSMap

kismet_ui.conf 文件，25, 64–65, 84, 89, 105, 126, 134–135, 150, 168

Knoppix, Live 发行版，41

KWrite, 文本编辑器，56

## L

Law enforcement officers，247–248

LibPcap 包，42

Linksys WRT54G，178, 188

Linux-based Kismet front end，108

Linux 操作系统

- GPSD installation，24
- kernel configuration，17–22
- Kismet installation，23

lischan.pl 脚本，124, 218

“Live Distros”，41

Local Area Network (LAN)，6

lsmod 命令，20

## M

MAC addresses，128–129, 137

Madwifi driver，55–56

Madwifi-ng，121–122

madwifi.org，55

make 命令，43

make dep 命令，47–48

make install 命令，47–49

make menuconfig 命令，21

make swinstald 命令，48

mapping tools，224, 228, 235

-max-packets switch，145

Media Access Control (MAC) address，97

Metasploit 项目，132

MMCX 连接器，70

MySQL，231–233

## N

National Marine Electronics Association (NMEA) protocol，75

ndiswrapper driver，53

network discovery tools，131

North American datum of 1927 (NAD27) data，75
