
该程序输出节点标识符信息，并且每 60 秒（如图 13-16b 配置所示）XBee2 路由器设备会读取其 ADC 输入并将值传输到 XBee 协调节点。你可以看到接收到的值为 617（即来自 10 位 ADC），并且按钮 (`DIO2`) 已被按下。

每当接收到一个新的数据帧时，`xbeeAPI.on()` 函数就会被调用并并将该帧传递过去。该帧描述了：

- `type` 指的是帧类型。在这种情况下，它是 146 (`0x92`)，表示“IO 数据采样接收指示器 (IO Data Sample Rx Indicator)”。

- `remote64` 是传输数据的节点地址，对应于图 13-15(b) 中的 XBee2 地址。

- `remote16` 是传输数据的设备网络地址，在本例中为 `0x8855`。

`XCTU` 的工具 (`Tools`) 菜单中提供了交互式 XBee API 生成器工具。它可以详细描述此类帧的内容。

你可以看到 Node.js 的输出是 JSON 格式。可以使用 `JSON.parse()` 方法将字符串转换为可用的数据值。

## XBee 和 C/C++

有一个名为 `libxbee` 的 C++ 库支持 Nodejs XBee API 模式。使用 Nodejs 模块并不简单，但它对 API 模式有完全支持。要开始使用该库，可以通过以下步骤下载并构建：

```bash
pi@ $ git clone https://github.com/attie/libxbee
pi@ $ cd libxbee
```

运行 `make configure` 会在主目录生成一个通用配置文件。在 RPI 上构建之前，应通过注释 `XEE_NO_RTS` 行来禁用 RTS/CTS 支持：

```bash
pi@~/libxbee $ make configure
pi@~/libxbee $ nano config.mk
pi@~/libxbee $ make config.mk | grep RTSCTS
OPTIONS += XEE_NO_RTS
pi@~/libxbee $ make
pi@~/libxbee $ make install
```

使用图 13-15 中相同的配置，可以执行 `/ch13/xbee/cpp/simple.c` 来测试库（记得设置 XBee UART 设备）：

```text
- rx.c:202 xbee_rxHandler() received 'I/O' packet...
- rx.c:211 xbee_rxHandler() connectionless 'I/O' packet...
- rx.c:181 xbee_rxHandler() address @0x767...
```

`libxbee/C++` 库需要详细研究以解析产生的数据。可以在 `tiny.cc/xbee/` 获取入门指南，并在 `github.com/attie/libxbee` 获取完整文档。

## 近场通信

近场通信 (`NFC`) 是一种允许物理距离的两个设备进行双向通信的无线技术。`NFC` 是射频识别 (`RFID`) 的一种特殊版本，支持安全通信和点对通信。例如，`NFC` 是移动设备非接触支付的核心技术，也用于手机之间的信息共享（例如通过碰碰）。`NFC` 工作频率与高频 `RFID` (`13.56 MHz`) 相同，这意味着许多 `NFC` 设备也可以连接无源或主动设备。常见的 `RFID` 卡没有电源，而是包含天线。`NFC` 设备利用磁场在天线中产生功率。

开发 `NFC/RFID` 软件的困难之一是开源 `libnfc` (`nfc-tools.org`) 是一套跨平台的低级软件套件，可以安装在 RPi 上。然而，你还需要 `NFC/RFID` 硬件。图 13-17 所示的电路可用于此任务——它使用了 `PN532` 控制器。

![](img/8d9725cf07daded8aced3920e81_599_0.png)

**图 13-17:** 用于 RPi 的 Adafruit NFC/RFID 接口以及无源 RFID 标签

Philips `PN532` 控制器 (`tiny.cc`) 支持 `13.56 MHz` 下的 `ISO1443A/MIFARE/FeliCa` 方案通信。它支持 `SPI`、`I2C` 和 `UART` 接口；然而，它只有贴片封装，且需要外部天线。坦率地说，Adafruit 开发了简化该技术开发的开发板。有一个 Arduino 扩展板和一个独立板，售价均为 40 美左右。还有廉价的 `PN532` 控制器可用——确保你购买支持 `UART` 连接的型号，如图 13-18(a) 所示。此外，廉价的 `13.56 MHz` 无源 `RFID/NFC` 贴纸、钥匙扣、按钮、塑料钉、手环和洗衣标签，这开启了应用可能性——见图 13-18(b)。

![](img/8d9725cf07daded8aced3920e81_600_0.png)

最新版本的 `libnfc` 可以如下进行下载和配置：

```bash
pi@pi ~ $ git clone https://github.com/nfc-tools/libnfc
pi@pi ~ $ cd libnfc
pi@~/libnfc $ sudo apt install libusb-dev
pi@~/libnfc $ sudo mkdir /etc/nfc/
pi@~/libnfc $ sudo cp libnfc.sample /etc/nfc/libnfc.conf
```

此示例的最后一步是将示例配置文件复制到 RPi 上，可用于识别 NFC 设备配置。在图 13-17 中，使用 USB 转 UART 设备来指定到 RPi 的接口，这必须在配置文件中指定：

```bash
pi@pi /etc/nfc $ more libnfc.conf
allow_autoscan = true
device.name = "MicroBuilder.eu"
device.constraining = "pn532_uart:/dev/ttyUSB0"
```

# 第三部分 — 高级索引与交互

```bash
libnfc.so 5.0.1  libnfc.so.5
@erpi ~/libnfc ls /usr/local/bin/nfc*
nfc-scan-device  nfc-list
  ...
```

如果现在板已如图 13-17 所示连接，那么你就可以使用 `libnfc` 提供的二进制工具来测试你的配置：

```bash
@erpi ~ $ sudo nfc-list
nfc-list uses libnfc 1.7.1
nfc device: pn532_uart:/dev/ttyUSB0 opened
```

如果你遇到共享库错误，请检查 `ldconfig`（你可以参考第 5 章“静态与动态编译”中使用的 `ldd` 工具来测试共享库依赖关系）。当电路中使用两张不同的 RFID 卡片时，你将看到呈现不同但一致的 ID：

```bash
@erpi ~ $ sudo nfc-poll
nfc-poll uses libnfc 1.7.1
nfc reader: pn532_uart:/dev/ttyUSB0 opened
nfc service will poll during 30000 ms (20 polls of 300 ms for 5 modifications)
ISO/IEC 14443A (106 kbps) target:
ATQA (SENS_RES): 00 44
UID (FCID): 04 60 28 4a 32 80
SAK (SEL_RES): 00
nfc_initiator_is_present: Target Released
Waiting for card reading....
```

```bash
@erpi ~ $ sudo nfc-poll
ATQA (SENS_RES): 00 04
UID (FCID): 0e 3f 04 03
SAK (SEL_RES): 08
```

在 `chp13/libnfc/nfc_test.c` 中提供了一个示例程序，你可以它来构建自己的 RFID 访问控制程序。该 C 程序将 UID 存储为字符数组（`char secretCode[] = {0x8e, 0x3f, 0x04}`），这些值是从不同的 RFID 卡片中读取的。如下面的测试示例所示，检测到带有“secret”的卡片时，程序不会授予访问：

```bash
@erpi ~/exploringrpi/chp13 $ ./build
@erpi ~/exploringrpi/chp13 $ ./nfc_test
ERPI nfc reader: pn532_uart:/dev/ttyUSB0 opened
Waiting for you to use an RFID card or tag....
The following tag was found:
UID (FCID): 04 60 28 4a 32 80
*** ERPI Access NOT allowed! ***
```
