
# 使用 Linux 和 Python 破解手机

手机是一个非常酷的可以玩玩的设备，尤其是当我可以在上面运行我最喜欢的编程语言（不用猜也知道是什么！）时！正是这种逻辑使我购买了一部诺基亚 Series 60 智能手机，即 N-Gage QD。本文描述了我对这台手机进行的实验 - 建立蓝牙通信链路、运行 Python/C 以及模拟串口端口。

## Linux 上的蓝牙

蓝牙是一种短距离通信标准。它通常用于在 PC 和手机/PDA 之间辅助进行数据传输。为 PC 提供蓝牙连接的硬件是一个名为 _USB 蓝牙适配器 (dongle)_ 的微型设备，你可以将其插入机器的空闲 USB 端口。我向当地的电子店索要了这样一个设备，买到了一个没有厂家名称的设备。随附的驱动程序 CDM 只包含 Windows 软件。决定碰碰运气，我插上设备并启动了我的 Fedora Core 3 系统 - 通过执行以下命令启动蓝牙服务：

```bash
sh /etc/init.d/bluetooth start own
```

这里是我执行 `hciconfig` 命令（类似于用于配置 TCP/IP 网络接口的 `ifconfig` 命令）时的输出：

```
hci0: Type: USB
BD Address: 00:11:B1:07:A2:B5 SCO MTU: 64:8
UP RUNNING PSCAN SCAN
RX bytes:378 acl:0:0 events:16 errors:0
TX bytes:309 acl:0:0 commands:16 errors:0
```

我的无名蓝牙适配器已被检测到并正确配置！数字 `00:11:B1:07:A2:B5` 是该设备的蓝牙地址。

## 检测手机

下一步一步是检查 Linux 是否能够感知到手机的临近性。如果你的手机禁用了蓝牙，请开启它并运行以下命令（在 Linux 机器上）：

```bash
hcitool scan
```

以下是在我的机器上获取的输出：

```
Scanning ...
00:E6:6D:9A:57:48 Dijkstra
```

运行在我的 GNU/Linux 上的 _Bluez 协议栈_“发现”了附近的诺基亚 N-Gage，并将其蓝牙地址打印为分配给：“Dijkstra”的地址。

## 配对手机

出于安全考虑，与手机的某些交互需要设备与其交互的设备进行“配对”。首先，在 `/etc/bluetooth/pin` 文件中设置数字（或多个数字，例如 `12345`）。通过以下操作停止并重启蓝牙服务：

```bash
sh /etc/init.d/bluetooth stop
sh /etc/init.d/bluetooth start
```

现在在手机上发起“配对”操作（手机会告诉你如何操作）。手机上的软件将检测到支持蓝牙的 Linux 终端并要求输入代码 - 你应该在 PC 上输入你在 `/etc/bluetooth/pin` 中存储的那个数字 - 配对过程将成功。

## 传输文件

使用一种名为 OBEX（对象交换，最初设计为红外链路设计）的高级协议传输到 Linux 机器。首先，你需要确认手机是否支持基于 OBEX 的消息传输。在 Linux 机器上尝试运行以下命令（数字是手机的蓝牙地址）：

```
sdptool browse 00:ee:6d:9a:57:48
```

你可能会得到大量的输出 - 以下是我获取的部分内容：

```
Service Description: OBEX Object Push
Service RecordListHandle: 0x10005
Service Class ID List: (0x1105)
"OBEX Object Push"
Protocol Descriptor List:
"LCG" (0x0010)
"RFCOMM" (0x0003)
Channel: 9
"OBEX" (0x0008)
```

OBEX 构建在一个名为 RFCOMM 的低级协议之上。“对象推送”服务使用 RFCOMM “通道” 9。让我们尝试向手机上传一个文件；在 Linux 机器上运行以下命令：

```bash
obex_push 00:ee:6d:9a:57:48 a.txt
```

手机将做出响应，询问你是否接受通过蓝牙链路发送的消息。在不带任何选项的情况下调用该命令，可以通过蓝牙链路从手机接收文件（更多详情请参考相应的 `man` 页）。

## 安装 Python

诺基亚已将 Python 移植到运行 Symbian 系统的“Series 60”手机上。Python 解释器以及几个重要的模块被封装成单个 `.sis` 文件（类似于 Linux 的 RPM 文件），该文件可以从 `http://www.forum.nokia.com/main/0_034-821.html` 获取。要安装的文件为 `PythonForSeries60_pre_SDK20.sis`。第一步是通过 `obex_push` 将此文件传输到手机。尝试在运行的诺基亚安装程序中打开它 - 它会要求你是在手机有限的内存上安装 Python，还是安装到额外的 MMC 卡上（如果有）。一旦安装完成，你将在手机的主菜单上看到一个不那么可爱的 Python Logo - 图 1 是我拍摄的主菜单截图。

![](img/b2912f82085f2b2d61cbed8cf3a429c5_1_0.png)

图 2 显示了交互式 Python 提示符，你可以在那里尝试输入 Python 脚本！

## Python

![](img/b2912f82085f2b2d61cbed8cf3a429c5_2_0.png)

```python
symbian_s60
Type 'copyright', 'credits'
or 'license' for more
information.
(InteractiveConsole)
>>>
>>>

Exit
```

## 运行 Python “Hello, World”

你可以在 Linux 手机上编写 Python 脚本并使用 `obex_push` 上传到手机。如果你尝试打开这些脚本（在手机上），“应用程序管理器”将询问你头文件是否为 Python 脚本。一旦作为脚本安装，你就可以从菜单打开“Python”应用程序时按照屏幕上显示的指令执行它们。

图 3 显示了在手机上安装并运行以下脚本获取的输出：

```python
import appuifw # 应用 UI 框架
appuifw.app.title = 'Cool Python'
appuifw.note(u'OK', 'info')
```

![](img/b2912f82085f2b2d61cbed8cf3a429c5_2_1.png)

Python for Series 60 -

OK

## Socket 编程

运行在手机上的应用程序以及 Linux 接口通过 socket API 与蓝牙协议栈交互。列表 1 显示了一个运行在手机上的简单客户端程序，它连接到运行在 Linux 机器上的服务器并向其发送消息；服务器代码在列表 2 中显示。

运行在手机上的 Python 客户端连接到 Linux 机器上的服务器并向其发送一条消息；服务器代码显示在列表 2。

你在屏幕上看到了什么？一个 Python 交互式解释器提示符！你现在可以使用 Python 代码段并在手机上即时执行！这难道不酷吗？

我曾好奇微软以“易用性”闻名的 Windows 操作系统是如何运作的，并尝试在我的 Ngage QD 上将其与 Linux 的交互进行对比。我为我的无名 USB 蓝牙适配器安装了 Windows 驱动，并尝试在 XP 机器上运行 Nokia PC 套件——也许是因为我对 GNU/Linux 的经验比对 MS 操作系统要丰富得多，我发现 XP 的体验并没有微软所承认的那么“友好”。我相信，微软操作系统的大部分“用户友好性”实际上源于硬件供应商和应用程序开发者将产品与平台紧密集成，而不是操作系统本身的任何内在品质。

关于蓝牙技术的一般介绍，请参阅：`http://www.dell.com/downloads/vectors/2003_bluetooth.pdf`。关于蓝牙安全的一篇有趣论文可以在 `http://www.nikula.cs.ht.fi/-jiiw/bluesec.html` 找到。

`http://www.holtmann.org/` 有大量关于蓝牙和 Linux 的信息；我觉得《Linux 蓝牙编程》（`http://www.holtmann.org/papers/bluetooth/wic2003_slides.pdf`）文档非常有参考价值。

关于 Series 60 模块上 Python 的大量信息可以在 `http://www.postneo.com/postwiki/moin.cgi/PythonForSeries60/` 找到。ObexFTP 似乎是一个有趣的工具——你可以从 `http://triq.net/obex/` 获取它。网上有一些文档描述了如何对手机文件系统进行 NFS 挂载——可以尝试 Google 搜索获取更多信息。

关于本文的来源/勘误可以在 `http://pramode.net/ify-jun` 获取。
