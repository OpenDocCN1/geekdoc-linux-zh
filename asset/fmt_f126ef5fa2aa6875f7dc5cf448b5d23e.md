
我们将进行的第一个测试是查看 PC 是否识别 USBtinyISP 为 USB 设备。将 USBtinyISP 插入 PC 的 USB 端口。如果 `JP1` 引脚 1 和 2 短接，则需要目标电路为 USBtinyISP 供电。当 USBtinyISP 上电并连接到 USB 端口时，USB LED 应该亮起。启动终端窗口并输入：

```
dmesg | tail
```

## 第 5 章. AVR 8 位微控制器

此处应显示一条类似于下面的内容的消息：

Bus 005 Device 007: ID 1781:0c9f Multiple Vendors USBtiny

这显示 VID 为 1781，PID 为 0c9f。

将 USBtinyISP 连接到 USB 端口和目标电路后，可以进行接下来两项测试。

要测试编程器是否工作正常并正确连接到目标电路，请在终端窗口中输入以下内容：

```bash
sudo avrdude -c usbtiny -p t2313
```

我们将其中一个测试程序 `blink.hex` 或 `blink2.hex` 加载到目标 AVR。启动终端窗口并切换到包含十六进制程序的目录。输入以下命令程序目标 AVR：

```bash
sudo avrdude -p t2313 -c usbtiny -e -U flash:w:blink.hex
```

### 5.2.5 Atmel AVRISP mkII USB 编程器

来自 Atmel 的标准 AVR 编程器是图 5.9 所示的 AVRISP mkII。该设备的订购代码为 `ATAVISP2`，在网上查询价格时可以使用该代码。

![](img/3c46617540546e0091f48cc286948fbe_161_0.png)

### 5.2.6 Atmel AVR Dragon

该编程器可用于所有带有 ISP 接口的 8 位 AVR。它支持 1.8V 到 5.5V 的目标电压，并由 USB 供电。

要用我们图 5.2 所示的测试电路测试 AVRISP mkII，请将编程器插入 PC 的一个 USB 端口，并将绿色 6 针接头连接到测试电路。当编程器连接到 USB 端口时，编程器上 USB 接口附近的绿色 LED 将亮起。当目标电源开启时，编程器上 6 针排线电附近的绿色 LED 将随之亮起。打开终端窗口并输入：

```bash
sudo avrdude -c avrispmkII -p t2313 -p USB
```

如果编程器正确连接到目标设备，电路 AVR 设备将初始化并读回设备签名。当编程器读取 AVR 时，6 针排线附近的 LED 将闪烁红光，然后变回绿色。

使用 AVRISP mkII 编程 AVR，请打开终端窗口并切换到包含十六进制测试程序的目录。在终端窗口中输入以下内容：

```bash
sudo avrdude -p t2313 -c avrispmkII -p USB -e -U flash:w:blink.hex
```

提高 AVRISP mkII 的访问/编程速度

AVRISP mkII 的初始速度相对较慢，因此你可能注意到它的编程速度比一个自制的编程器慢。为了加快速度，请在 `avrdude` 中使用 `-B` 关。现在从 AVR 读取设备签名并对其编程的命令变为：

```bash
sudo avrdude -c avrispmkII -p t2313 -p USB -B 3.0
sudo avrdude -p t2313 -c avrispmkII -p USB -e -U flash:w:blink.hex -B 3.0
```

### 5.2.6 Atmel AVR Dragon

AVR Dragon 看起来更像一个评估板而非编程器，如图 5.10 所示。它具有多种编程和调试功能。在本节中，我们仅用它进行系统内编程。AVR Dragon 以如图所示的盒子出售，不包含连接到目标板的 USB 线或排线。对于片内编程，你需要一根标准的 USB 线和一根两端带有 IDC 3 × 2 母头连接器的 6 针排线。

AVR Dragon 是一种成本较低的设备。AVR Dragon 的订购代码为 `ATAVDRAGON`，在网上购物价格时可以使用该代码。

网站：www.atmel.com/AVRDRAGON

![](img/3c46617540546e0091f48cc286948fbe_163_0.png)

图 5.10：AVR Dragon

Atmel 网站未提供 AVR Dragon 的 PDF 格式文档。它是 Windows AVR 编程环境 AVR Studio 中的 chm 帮助文件。为了方便起见，该文件已包含在附文件中，可以在此处找到：`CH05/AVRDragon.chm`

在 Linux Mint 中读取 chm 文件，你需要从软件管理器安装阅读器，搜索“chm”，例如 ChmSee。

使用 AVR Dragon 进行系统内编程

使用 USB 线将 AVR Dragon 连接到 PC，使用 6 针排线（两端带有 IDC 3 × 2 母头连接器）连接到目标板。当 AVR Dragon 连接到 USB 端口时，其丝印上的 ISP LED 将亮起。

### 5.2.7 关于 avrdude 的更多信息

要从 AVR 读取设备签名，打开终端窗口并输入：

```bash
sudo avrdude -c dragonisp -p t2313
```

要使用 AVR Dragon Dragon 编程 AVR，打开终端窗口并切换到包含十六进制测试程序的目录。在终端窗口中输入：

```bash
sudo avrdude -p t2313 -c dragonisp -p USB -e -U flash:w:blink.hex
```

AVR Dragon 尝试与测试电路通信的速度过快。使用 `-B 3.0` 选项可以降低速度。如果仍然存在问题，尝试将 `3.0` 增加到更高值。

无需 sudo 命令使用 avrdude

到目前为止，我们每次对 AVR 微控制器进行编程都需要通过使用 `sudo` 命令获取 root 权限。第一次使用该命令时需要输入密码。你可以设置 Linux 以无需 root 权限。

## 5.3 AVR 电路

在本节中，我们将介绍一些电路，以便与开头提到的 AVR 设备进行开发。提供了简单的 C 程序，包含输入输出示例。所有这些 AVR 都有内部振荡器，因此在精确计时不需要连接外部电路。

示例程序可以在附文件 `CH5/AVR_progs` 中找到。每个示例文件夹包含一个源码文件以及一个 `build` 和 `prog` 文件。`build` 文件是一个脚本文件，需要标记为可执行并运行以构建项目输出用于编程 AVR 的 hex 文件。`prog` 文件也是一个脚本文件，需要标记为可执行并运行以编程 AVR。此文件已设置为使用 USBisp 并包含了 `sudo` 命令，如果你将 Linux PC 设置为无需 `sudo` 命令的情况下操作编程器，请对其修改（即从文件中删除 `sudo` 命令）。如果你使用 USBisp 以外的编程器，也对其进行修改。

### 使用脚本文件

提醒一下——要将脚本文件标记为可执行，右键点击它并从弹出菜单中选择“属性”。在属性对话框中，点击“权限”选项卡。勾选“允许执行文件作为程序”，然后关闭对话框。或者在终端窗口中使用此命令：`chmod +x <filename>`

现在该文件可以通过双击它并点击弹出对话框中的“运行”来运行。在终端窗口中当切换到包含脚本文件的目录时，可以通过输入 `./<文件名>` 来运行它们，例如 `./build`

### 5.3.1 ATtiny2313

### 快速信息

- Flash 大小：2 KB，系统内可编程
- SRAM 大小：128 Bytes
- EEPROM 大小：128 Bytes
- 外部外设：4 × PWM, 1 × 模拟比较器, 1 × USART, 1 × USI（可配置为 TWI 或 SPI）
- 片内调试：debugWire
- 最大 I/O 引脚：18
- 工作电压：2.7V 至 5.5V
- 每个引脚电流：>10 mA 源电流或灌电流，但每个端口不得超过 60mA。

![](img/3c46617540546e0091f48cc286948fbe_166_0.png)

PWM 通道输出：

- `OC0A`
- `OC1A`
- `OC0B`
- `OC1B`

图 5.11：ATtiny2313 引脚图和面包板电路

## 第 5 章. AVR 8 位微控制器

### 示例程序

`CH05/AVR_progs/ATtiny2313_blink/`

闪烁图 5.11 中的 LED。

`CH05/AVR_progs/ATtiny2313_IO/`

读取引脚 `PD6` 上的开关并将开关状态写入图 5.11 电路中引脚 `PB0` 上的 LED 上。当开关关闭时，LED 将点亮。

### 5.3.2 ATtiny48

### 快速信息

- Flash 大小：4k Bytes，系统内可编程
- SRAM 大小：256 Bytes
- EEPROM 大小：64 Bytes
- 外部外设：6 通道 10 位 ADC, SPI, TWI, 模拟比较器
