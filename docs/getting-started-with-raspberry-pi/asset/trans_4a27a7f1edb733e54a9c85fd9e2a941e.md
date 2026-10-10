

## 网络

请追踪图 16.2 中 *telnet/ftp/ssh* 框中的代码路径，以查看网络是如何基于 BlueZ 蓝牙进行架构设计的。正如你所见，通过蓝牙进行网络通信有两种不同的方式：

- 1. 直接在 BNEP 上运行 TCP/IP。由此产生的网络被称为*个人局域网* (PAN)。
- 2. 在基于 RFCOMM 的 PPP 上运行 TCP/IP。这被称为*拨号网络* (DUN)。

蓝牙网络的内核实现可能不会引起设备驱动程序编写者的兴趣，因此不予探讨。然而，表 16.2 展示了使用 PAN 将两台笔记本电脑联网所需的步骤。使用 DUN 进行网络通信与此类似，此处不作详细检查。这两台笔记本电脑分别使用之前讨论过的 Sharp CF 卡和 Belkin USB 适配器实现了蓝牙功能。你可以使用无源 CF 转 PCMCIA 适配器将 CF 卡插入第一台笔记本电脑的 PCMCIA 插槽。结合图 16.2 和表 16.2 来理解与相应 BlueZ 组件的映射关系。表 16.2 使用 *bash-sharp>* 和 *bash-belkin>* 分别作为两台笔记本电脑的 shell 提示符。

- 1. 启动 HCI 和服务发现守护进程：

```
bash-sharp> hcid
bash-sharp> sdpd
```

由于该设备拥有 UART 接口，你必须将 BlueZ 协议栈附加到适当的串行端口。在此情况下，假设 `serial_cs` 已为卡分配了 `/dev/ttyS3`：

```
bash-sharp> hcitattach ttyS3 any
```

- 2. 验证 HCI 接口是否已启用：

```
bash-sharp> hci1:  Type: UART
BD Address: 08:00:1F:10:3B:13 ACL MTU: 60:20  SCO MTU: 31:1
UP RUNNING PSCAN ISCAN
...
Manufacturer: Silicon Wave (11)
```

- 3. 验证基本的 BlueZ 模块是否已加载：

```
bash-sharp> lsmod

Module        Size    Used by
hci_uart      16728   3
l2cap         26144   2
bluetooth     47684   6 hci_uart, l2cap
...
```

- 4. 插入实现网络封装的 BlueZ 模块：

```
bash-sharp> modprobe bnep
```

- 5. 监听传入的 PAN 连接：[1]

```
bash-sharp> pand -s
```

在装有 Belkin USB 蓝牙适配器的笔记本电脑上

- 1. 启动守护进程，如 hcid 和 sdpd，并插入必要的内核模块，如 `bluetooth.ko` 和 `l2cap.ko`。

- 2. 由于这是一个 USB 设备，你不需要调用 hcitattach，但请确保已插入 `hci_usb.ko` 模块。

- 3. 验证 HCI 接口是否已启用：

```
Code View:
bash-belkin> hci1:  Type: USB BD Address: 00:02:72:B0:33:AB ACL MTU: 192:8  SCO MTU: 64:8
UP RUNNING PSCAN ISCAN
```

- 4. 搜索并发现附近的设备：

```bash
bash-belkin> hcitool -i hci0 scan --flush
Scanning....
08:00:1F:10:3B:13 bash-sharp
```

- 5. 与第一台笔记本电脑建立 PAN。你可以从其 `hciconfig` 输出中获取其蓝牙地址 (08:00:1F:10:3B:13)：

```bash
bash-belkin> pand -o 08:00:1F:10:3B:13
```

此时如果你查看两台笔记本电脑上的 `ifconfig` 输出，你会发现一个名为 `bnep0` 的新接口已在两端出现。为这两个接口分配 IP 地址，准备好进行 telnet 和 FTP！

[1] `pand` 的一个有用命令行选项是 `--persist`，当连接断开时会自动尝试重新连接。请查阅 man 页面以获取更多调用选项。

## 人体学接口设备

请查阅第 7 章“输入驱动程序”中“USB 和蓝牙键盘”和“USB 和蓝牙鼠标”章节，以了解有关蓝牙人体学接口设备的讨论。

## 音频

让我们以 Sony Ericsson HBH-30 蓝牙耳机为例，来理解蓝牙 SCO 音频。在耳机开始与 Linux 设备通信之前，后者的蓝牙链路层必须先发现前者。为此，请按下耳机上标有设备发现功能的按钮，使耳机进入发现模式。此外，你必须通过将耳机的人格识别码（PIN）添加到 `/etc/bluetooth/pin` 来配置 BlueZ。使用 BlueZ SCO API 的 Linux 设备上的应用程序现在可以向耳机发送音频数据。音频数据的格式必须是耳机能够理解的格式。HBH-30 使用 A 律 PCM (*脉冲编码调制*) 格式。有公共领域的实用程序可将音频转换为各种 PCM 格式。

蓝牙芯片组通常除了 HCI 传输接口外，还具有 PCM 接口引脚。如果某个设备支持例如 *全球移动通信系统* (GSM) 和蓝牙，GSM 芯片组的 PCM 线路可能会直接连接到蓝牙芯片的 PCM 音频线路。在这种情况下，你可能需要配置蓝牙芯片，使其通过 HCI 接口而不是 PCM 接口来接收和发送 SCO 音频数据包。

## 调试

有两个用于调试的 BlueZ 工具非常有用：

- 1. *hcidump* 截获往返的 HCI 数据包，并将它们解析为人类可读的形式。以下是一个设备查询过程中的示例转储：

```
bash> hcidump -i hci0
HCIDump -- HCI packet analyzer ver 1.11
device: hci0 snap_len: 1028 filter: 0xffffff
	HCI Command: Inquiry (0x01|0x0001) plen 5
	HCI Event: Command Status (0x0f) plen 4
	HCI Event: Inquiry Result (0x02) plen 15
	...
	HCI Event: Inquiry Complete (0x01) plen 1 < HCI Command:
Remote Name Request (0x01|0x0019) plen 10
...
```

- 2. 虚拟 HCI 驱动程序 (*hci_vhci.ko*)，如图 16.2 所示，如果你没有实际硬件，它可以模拟蓝牙接口。

## 查看源代码

在 *drivers/bluetooth/* 内部查找 BlueZ 低级驱动程序。探索 *net/bluetooth/* 以深入了解 BlueZ 协议实现。

蓝牙应用程序根据其行为方式分为不同的*配置文件*。例如，无线电话配置文件规定了蓝牙设备如何实现无绳电话。我们讨论了 PAN 和串行访问的配置文件，但还有更多配置文件，如传真配置文件、*通用对象交换配置文件* (GOEP) 和 *SIM 访问配置文件* (SAP)。可从 www.bluez.org 下载的 *bluez-utils* 包为几种蓝牙配置文件提供了支持。

官方蓝牙网站是 www.bluetooth.org。它包含蓝牙规范文档和关于*蓝牙特殊兴趣小组* (SIG) 的信息。

*Aflix* 是 Linux 上的另一种蓝牙协议栈。你可以从 http://affix.sourceforge.net/ 下载 Aflix。

## 红外

红外 (IR) 射线是位于可见光和微波区域之间的电磁波谱中的光学波。红外的一种用途是点对点数据通信。使用红外，你可以在 PDA 之间交换名片，为两台笔记本电脑联网，或将文档发送到打印机。红外在 30 度锥体内（从 -15 度到 +15 度传播）的作用距离最大可达 1 米。

红外通信有两种流行类型：标准红外 (SIR)，支持最高 115.20 Kbaud 的速度；以及快速红外 (FIR)，带宽为 4Mbps。

图 16.4 显示了笔记本电脑上的红外连接。Super I/O 芯片组中的 UART1 支持红外，因此红外收发器直接连接到它。如果笔记本电脑的 Super I/O 芯片不支持红外，则可能依赖于外部红外接口卡（参见“设备示例：红外接口卡”部分），类似于连接到 UART0 的那个。图 16.5 显示了一个内置红外接口卡连接到系统 UART 的嵌入式 SoC 上的红外连接。

### 图 16.4. 笔记本电脑上的 IrDA。

![](img/07cc6f9c8c74622020874f66bfb53dc4_441_0.png)

### 图 16.5. 嵌入式设备上的 IrDA（例如 EP7211）。

