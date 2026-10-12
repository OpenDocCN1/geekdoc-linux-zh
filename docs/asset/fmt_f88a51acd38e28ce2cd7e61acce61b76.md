
## phrasendrescher

**用法** 增量模式：`phrasendrescher -i 8 key-file`（生成 8 字符长的单词）

**用法** 增量模式：`phrasendrescher -i 8:12 key-file`（指定范围）

**用法** 字典模式：`phrasendrescher -d wordlist key-file`

**用法** 字典模式：`phrasendrescher -d wordlist directory-containing-keys`（如果您指定目录而不是单个密钥文件，将读取并尝试多个密钥）

```
/phrasendrescher -vd wordlist.txt my.key
```

## thc-pptp-bruter

描述 一个针对 pptp vpn 端点的暴力破解程序。该工具的使用非常简单：只需将字典文件通过到 `thc-pptp-bruter`，并指定你要攻击的用户和主机。请注意，连接到设备时，你将看到有关所连接主机的简要信息，例如“Hostname ~c2611wooter, Vendor ~Cisco Systems, Inc., Firmware: 4608.”这是一种有效的远程应用层指纹识别。

更多信息：http://flylib.com/books/en/3.418.1.83/1/

用法 `thc-pptp-bruter [options]<remote ip>`

- `-v` 详细输出 / 调试输出
- `-W` 禁用 windows hack [默认：启用]
- `-u <user>` 用户 [默认：administrator]
- `-w <file>` 字典列表文件 [默认：stdin]
- `-p <>` PPTP 端口 [默认： ]
- `-n <>` 尝试次数 [默认： 5]
- `-l <>` 限制 [默认： 100]

示例 `thc-pptp-bruter -99`

## scarab

**描述** WebScarab 是一个用于应用程序的框架，使用 Java 编写并可移植到许多平台。它可以作为代理来查看请求和响应。它有多个插件。

更多信息：https://www.owasp.org/Getting_Started/

用法 n/a

示例 n/a

## zaproxy

**描述** OWASP Zed Attack Proxy (ZAP) 是一个易于使用的漏洞查找工具，为新手和丰富的测试人员设计。更多信息：https://code.google.com/p/zaproxy/

用法 n/a

示例 n/a

## 无线攻击：蓝牙工具

- `bluelog`
- `bluemaho`
- `blueranger`
- `btscanner`
- `fang`

## bluelog

**描述** Bluelog 是一个蓝牙扫描器，用于告诉你区域内的发现设备。它是用 python 编写的。

用法 `bluelog [options]`

https://github.com/MS3FG/Bluelog

## bluemaho

**描述** BlueMaho 是测试蓝牙安全的工具集 Shell。它是免费开源、用 python 编写的。

更多信息：http://wiki.thc.org/BlueMaho

用法 n/a

示例 n/a

## blueranger

**描述** BlueRanger 是一个简单的 Bash 脚本，利用链路质量定位无线设备。它通过发送 l2cap（蓝牙）ping 来建立连接，因为大多数设备在没有任何身份验证或授权的情况下允许 ping。链路质量越高，距离越近（理论上）。使用蓝牙 Class 1 适配器进行远程定位。切换到 Class 3 适配器进行更精确的短距离定位。精度取决于蓝牙适配器的质量、干扰以及远程设备的响应。即使两个设备都没有移动，也可能波动。

用法 `blueranger.sh [options] <device address>`

示例 `blueranger.sh hci0 6C:D6:8A:B1:30:BC`（提供本地接口和要尝试的设备地址）

## btscanner

描述 `btscanner` 是一种专门设计的工具，无需配对即可从蓝牙设备提取尽可能的信息。详细信息屏幕提取 HCI 和 SDP 信息，并保持打开连接以监控 RSSI 和链路质量。`btscanner` 基于现代 Linux 内核包含的 BlueZ 蓝牙栈以及 BlueZ 工具集。`btscanner` 还包含完整的 IEEE OUI 列表和类查找表。通过这些来源收集的信息，可以对主机设备类型做出合理的推断。

用法 `btscanner [options]`

+ 选项
  - `--help` 显示帮助
  - `--cfg=<file>` 使用 `<file>` 作为配置文件
  - `--no-reset` 在扫描前不重置蓝牙适配器

示例 `btscanner --help`

## fang

描述 n/a

用法 n/a

示例 n/a

![](img/5d79c1ec781b24792cca2ae58b309760_274_0.png)

## spoofotooph

**DESCRIPTION** Spoofotooph 旨在自动化伪造和克隆蓝牙设备的名称、类别和地址。有效地克隆这些信息可以允许蓝牙设备在众目睽睽下隐藏。当范围内的多个设备在*可发现模式*下（具体为具有相同的地址）共享相同的设备信息时，蓝牙扫描软件将仅列出其中一个设备。

- **选项 1：** Incognito 可以扫描区域内的蓝牙设备。在列表中选择一个要克隆的设备。此选项还允许对扫描到的设备进行记录。
- **选项 2：** 随机生成并分配蓝牙接口信息。*类别*（class）和*地址*（address）是随机生成的，*名称*源自美国前 100 个常用名称列表和设备类型。例如，如果随机生成的*类别*是手机，SpoofTooth 可能会生成名称“Bob's Phone”。
- **选项 3：** 指定用户希望蓝牙接口拥有的*名称、类别、地址*。
- **选项 4：** 读取之前扫描的日志并选择一个设备进行克隆。用户可以手动向这些日志文件添加蓝牙配置文件。
- **选项 5：** *Incognito 模式。* 根据用户分配扫描新的克隆设备。

**USAGE** `spoofotooph [options] -device address`

```
EXAMPLE spoofotooph -i hci0 -n new_name -a 00:11:22:33:44:55 -c 0x1c010c (指定 名称、类别 和地址)
```

```
EXAMPLE spoofotooph -i hci0 -R (随机生成 名称、类别 和 地址)
```

```
EXAMPLE spoofotooph -i hci0 -w file.csv (扫描范围内的设备并选择一个设备进行克隆。理想情况下将设备信息转储到指定的日志文件中)
```

```
EXAMPLE spoofotooph -i hci0 -r file.csv (从日志文件中加载设备信息并指定要克隆的设备信息)
```

```
EXAMPLE spoofotooph -i hci0 -t 1 (每 X 秒克隆范围内的一个随机设备信息)
```

Kali Linux 2013 276 工具列表

## [34] 其他无线工具

- `zbassocflood`
- `zbconvert`
- `zbdsniff`
- `zbdump`
- `zbfind`
- `zbgoodfind`
- `zbid`
- `zbreplay`
- `zbstumbler`

## zbassocflood

**DESCRIPTION** KillerBee 包含了几个用于攻击 ZigBee 和 IEEE 802.15.4 网络的工具，这些工具使用 **KillerBee** 框架构建。每个工具都有自己的用法说明，通过在运行工具时使用 "-h" 参数进行记录，并摘要如下。

**zbassocflood** - 重复关联到目标 PANID，试图由于连接的站点过多而导致设备崩溃。

**KillerBee** 的 API 以 epydoc 格式记录，并在此发行版的 doc/ 目录中带有 HTML 文档。如果你安装了 epydoc，根据需要，你还可以生成一个方便打印的 PDF，如下所示：$ cd killerbee mkdir pdf $ epydoc --pdf -o pdf killerbee/ pdf/ 目录将包含一个名为 "**api.pdf**" 的文件，其中包含了框架文档。

**USAGE** n/a

**EXAMPLE** n/a

## zbconvert

**DESCRIPTION** KillerBee 包含了几个用于攻击 ZigBee 和 IEEE 802.15.4 网络的工具，这些工具使用 **KillerBee** 框架构建。每个工具都有自己的用法说明，通过在运行工具时使用 "-h" 参数进行记录，并摘要如下。

**zbconvert** - 将数据捕获文件转换为 SNA 格式，反之亦然。
