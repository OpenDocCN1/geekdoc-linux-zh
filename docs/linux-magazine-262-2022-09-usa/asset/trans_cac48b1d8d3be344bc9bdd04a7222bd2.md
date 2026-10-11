
## 创客空间
### 温馨的家园
Home Assistant 通过 MQTT 控制微控制器

实现居家自动化并不一定需要商用解决方案。只要具备一定的技术技能，你只需少量预算即可开发自己的项目。*作者：Gerhard Schauer*

家庭自动化提供了许多可能性，但也伴随着诸多风险。如果你能成功摆脱对商业产品的依赖，不仅能节省开支，还能完全掌控数据流向。在这种情况下，消息队列遥测传输（Message Queuing Telemetry Transport, MQTT）协议显得非常有用。

之前一篇关于 Z-Wave [1] 的文章展示了如何利用 Home Assistant 和市场上现有的组件，快速将 Raspberry Pi 接入自动化环境，从而在不需人工干预的情况下实现家居自动化。Home Assistant 可以管理大量组件，甚至无需依赖云端。唯一的限制在于你的预算和想象力。

本文作为续篇，将讲解如何同时降低组件的成本和 DIY 难度。从 Raspberry Pi 3 代开始，其内置的无线接口在许多微控制器模块中同样常见，这有望打开更多应用之门。将这一切与上一篇文章中介绍的 Home Assistant 环境连接起来的“胶水”，是一种支持 IP 的协议，它早在物联网（IoT）热潮兴起之前就已经问世，即：MQTT。

MQTT 协议于 1999 年推出，是一种基于文本、运行在任何 IP 网络 TCP 之上的协议。可选使用传输层安全（TLS）进行加密。传感器和执行器作为客户端与消息代理（broker）通信，而消息代理充当通信枢纽。寻址依赖于所谓的“主题”（topics）。发送方被称为发布者（publishers），接收方被称为订阅者（subscribers）。

### 测试 MQTT

要在 Raspberry Pi 上实现该协议，首先需要安装 *mosquitto* 包。对于下文的小型实现测试，你还需要对应的客户端。可以使用以下命令在 Raspberry Pi 上安装这两个组件：

```
$ sudo apt-get install mosquitto
$ sudo apt-get install mosquitto-clients
```

如果安装完成后代理正在运行，你可以使用客户端登录各个主题，并通过指定代理运行所在主机（在 `-h` 选项中）的命令行调用获取主题列表：

```
$ mosquitto_sub -h localhost -t "#"
```

在此例中，主机是 localhost。例如，若要向名为 test/test1 的主题发送值 *10* 并作为订阅者接收该值，可以使用以下命令：

```
$ mosquitto_pub -v -h 192.168.3.7 -t test/test1 -m 10
$ mosquitto_sub -h 192.168.3.7 -t test/test1
```

为了更实际的示例，我将使用 MQTT 将连接到 Raspberry Pi 的 DS18x20 单总线温度传感器的测量值传输到监听在另一台 Raspberry Pi 上的代理。为此，你需要提前在 `/boot/config.txt` 文件中启用单总线支持：

```
dtoverlay=w1-gpio
```

将传感器连接到标准单总线 GPIO 端口后，可以在 `/sys/bus/w1/devices/28-0417c1b1ff/w1_slave` 中以四位整数形式查询温度值。数值 28-0417c1b1f7ff 是传感器在总线上的唯一 ID。完整的命令序列如下：

```
$ mosquitto_pub -h 192.168.3.7 -t wohn/temp/28-0417c1b1f7ff -m $value
$ mosquitto_sub -h localhost -t wohn/temp/28-0417c1b1f7ff
```

要将这些值传输到 Home Assistant 环境，需要在 configuration.yaml 文件中输入你使用的代理（在此例中，它运行在同一主机上（清单 1，第 1-2 行））。接下来几行的条目负责订阅相应主题并在 Home Assistant 中处理传感器数据；最后一行还指定摄氏度为单位。

![](img/b40e8bf6cf651f8eebf36f5265123095_71_0.png)

### ESP8266 控制器

理论部分已经覆盖，但为每个远程执行器或传感器使用单独的 Raspberry Pi 在实践上似乎有点不现实。ESP8266 控制器在此处将派上用场。一方面，你可以找到价格低廉且实用的使用该控制器的开发板；另一方面，该芯片被远东地区的许多产品采用，你只需刷入免费可用的固件即可掌控其中许多设备。

![](img/b40e8bf6cf651f8eebf36f5265123095_72_0.png)

图 1：带有温度传感器的 Sonoff Basic WiFi 智能开关。

在此测试中，我使用了一款 Sonoff Basic WiFi 智能开关 [2]（图 1）。这款可控制的继电器开关具有 220V 市电的螺丝接线端子，并带有可切换的输出。

*注意：如果未正确使用该硬件，存在生命危险。在本文中，我将模块的供电电压限制在 3.3V。*

固件为 Tasmota。该软件允许你在控制器现有的 GPIO 端口上配置各种受支持的传感器和组件，例如我之前提到的温度传感器。Tasmota 使用 MQTT 传输传感器数据。

![](img/b40e8bf6cf651f8eebf36f5265123095_72_1.png)

图 2：将 Sonoff Basic 连接至 Raspberry Pi 的接线方式。

所需的接线如图 1 和图 2 所示。PiOS 仓库中的 esptool.py 工具提供了软件支持。

![](img/b40e8bf6cf651f8eebf36f5265123095_73_0.png)

Tasmota 固件以及大量信息可在项目的 GitHub 仓库 [4] 中找到。由于我想集成温度传感器，因此下载了传感器版本进行测试：

```
$ wget -c https://ota.tasmota.com/tasmota/release-9.4.0/tasmota-sensors.bin
```

你还需要为 Web GUI 分配密码并启用 MQTT（图 4），这将用于向 Home Assistant 传输数据。

代理和主题在 Web 界面的相应条目中配置，在那里你还可以找到 Tasmota 控制台，它允许你直接发出命令并设置参数化。

按照图示连接模块后，需要在通电时按住 Sonoff 模块上的按钮；此时 LED 不会亮起。接下来，使用命令

### 刷写 Tasmota

```
$ esptool --port /dev/ttyAMA0 chip_id
```

检查是否可以使用该 Sonoff。必须显示一个 ID。

刷写 Tasmota 的几种方法中，一种流行的做法是使用 USB 串口适配器。相关说明可在项目的入门页 [3] 上找到。由于 Raspberry Pi 自带串口接口，我将直接通过 GPIO 进行刷写。

```
$ esptool --port /dev/ttyAMA0 write_flash -fm dout 0x0 tasmota-sensors.bin
```

最后，使用以下命令刷写 Tasmota：

此操作大约需要一分钟。模块重启后，它会作为新的 WiFi 接入点报告就位，你可以通过 `http://192.168.4.1` 访问它，并在其中配置要使用的 WiFi 网络。之后所有的设置步骤都将通过你自己的 WiFi 网络分配的 IP 地址进行。

在进行下一步之前，你首先需要将温度传感器连接到用于刷写的其中一个 GPIO（RX/TX），现在该端口已空闲。你可以使用上拉电阻以及 3.3V 和 GND 连接 [5] 来完成接线。布线完成后，即可配置传感器；其名称可能已经出现在 GUI 中（图 3）。

最迟在此时，我建议仔细阅读 Tasmota GitHub 仓库中优秀的文档。在此项目中，我使用了一条命令，让 Tasmota 通告所有可用主题（Setoption19 on），这使得后续通过自动发现集成到 Home Assistant 变得非常容易。最终，Tasmota 在 GUI 中显示为一个带温度传感器的 Web 开关（图 5）。你还可以查看

![](img/b40e8bf6cf651f8eebf36f5265123095_73_1.png)

图 3：便捷的 Web GUI 帮助你设置温度传感器。

![](img/b40e8bf6cf651f8eebf36f5265123095_73_2.png)

图 4：只需几个参数即可准备 Tasmota 向 Home Assistant 传输数据。

![](img/b40e8bf6cf651f8eebf36f5265123095_73_3.png)

图 5：几乎与商用产品无异：Tasmota 基于 Web 的用户界面。

### 配置 Tasmota

图 6：只需几个简单步骤即可将 MQTT 协议集成到 Home Assistant。

清单 1: configuration.yaml
```yaml
01 mqtt:
02   broker: localhost
03
04 sensor:
05   - platform: mqtt
06     name: templ
07     state_topic: "/living/temp/28-0417c1b1f7ff"
08     unit_of_measurement: '°C'
```

