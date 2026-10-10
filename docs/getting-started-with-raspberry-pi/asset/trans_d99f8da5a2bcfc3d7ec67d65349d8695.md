

```c
}

/* Reset */
static int
mydongle_reset(struct sir_dev *dev)
{
	/* Reset the dongle as per the spec, for example,
	   by pulling DTR low for 50 us */
	sirdev_set_dtr_rts(dev, FALSE, TRUE);
	udelay(50);
	sirdev_set_dtr_rts(dev, TRUE, TRUE);
	dev->speed = 19200; /* Reset speed is 19200 baud */
	return 0;
}

/* Close */
static int
mydongle_close(struct sir_dev *dev)
{
	/* Power off the dongle as per the spec,
	   for example, by pulling DTR and RTS low.. */
	sirdev_set_dtr_rts(dev, FALSE, FALSE);
	return 0;
}

/* Dongle Driver Methods */
static struct dongle_driver mydongle = {
.owner	= THIS_MODULE,
.type	= MY_DONGLE,			/* Add this to the enumeration
					   in include/linux/irda.h */
.open	= mydongle_open,	/* Open */
.reset	= mydongle_reset,	/* Reset */
.set_speed = mydongle_change_speed, /* Change Speed */
.close	= mydongle_close,	/* Close */
};

/* Initialize */
static int __init
mydongle_init(void)
{
	/* Register the entry points */
	return irda_register_dongle(&mydongle);
}

/* Release */
static void __exit
mydongle_cleanup(void)
{
	/* Unregister entry points */
	irda_unregister_dongle(&mydongle);
}

module_init(mydongle_init);
module_exit(mydongle_cleanup);
```

如需查看实际案例，请参阅 `drivers/net/irda/tekcram.c` 和 `drivers/net/irda/ep7211_ir.c`。

既然物理层已经运行起来，让我们进一步探索 IrDA 协议。

## IrComm

IrComm 模拟串行端口。诸如终端模拟器等应用程序以及诸如 PPP 等协议可以不加修改地运行在由 IrComm 创建的虚拟串行界面上。IrComm 由两个相关模块实现，即 `ircomm.ko` 和 `ircmm_tty.ko`。前者提供核心协议支持，后者负责创建和管理模拟串行端口节点 `/dev/ircmmX`。

## 网络

通过 IrDA 运行 TCP/IP 应用程序有三种方式：

- 通过 IrComm 的异步 PPP
- 通过 IrNET 的同步 PPP
- 通过 IrLAN 的以太网模拟

通过 IrComm 进行网络通信等效于通过串行端口运行异步 PPP，因此在此场景中没有什么特别之处。

异步 PPP 需要使用诸如字节填充等技术来标记帧的起始和结束，但如果 PPP 运行在以太网等数据链路上，则无需承担帧协议带来的额外开销。这被称为同步 PPP，并用于配置 IrNET 上的网络。^[3] 穿过 PPP 层可以提供按需 IP 地址配置、压缩和身份验证等功能。

[^3]: 如需查阅关于通过 IrNET 进行网络通信的学术讨论，请阅读 www.hpl.hp.com/personal/Jean_Tourrilhes/Papers/IrNET.Demand.html。

要启动 IrNET，请插入 `irnet.ko`。这同时也会创建字符设备节点 `/dev/irnet`，这是一个控制通道，你可以在其上附加 PPP 守护进程：

```bash
bash> pppd /dev/irnet 9600 noauth a.b.c.d:a.b.c.e
```

这会在两端生成 `pppX` 网络接口，并将相应的 IP 地址分别设置为 a.b.c.d 和 a.b.c.e。此时，这些接口即可传输 TCP/IP 数据包。

IrLAN 在 IrDA 上提供原始以太网模拟。若要通过 IrLAN 将笔记本电脑组网，请在两端执行以下操作：

- 插入 `irlan.ko`。这将创建网络接口 `irlanX`，其中 `X` 为分配的接口编号。
- 配置 `irlanX` 接口。若要设置 IP 地址，请执行以下操作：

```bash
bash> ifconfig irlanX a.b.c.d
```

或者，通过向 /etc/sysconfig/network-scripts/ifcfg-irlan0 添加以下行来实现自动化：^[4]

[^4]: 该文件的位置因发行版而异。

```
DEVICE=irlanX IPADDR=a.b.c.d
```

此时，你可以通过 irlanX 接口在笔记本电脑之间使用 telnet 进行通信。

## IrDA 套接字

若要开发基于 IrDA 的自定义应用程序，请使用 IrSock 接口。若要创建基于 TinyTP 的套接字，请执行以下操作：

```c
int fd = socket(AF_IRDA, SOCK_STREAM, 0);
```

若要创建基于 IrLMP 的数据报套接字，请执行以下操作：

```c
int fd = socket(AF_IRDA, SOCK_DGRAM, 0);
```

请参阅 irda-utils 包中的 irsocks/ 目录以查找代码示例。

## Linux 红外遥控

LIRC 项目的目标是让你通过遥控器控制你的 Linux 计算机。例如，你可以使用 LIRC 通过遥控器上的按钮来控制播放 MP3 音乐或 DVD 电影的应用程序。LIRC 的架构如下：

1. 一个名为 lirc_dev 的基础 LIRC 模块。
2. 硬件特定的物理层驱动程序。通过串行端口接口的红外硬件使用 lirc_serial。为了让 lirc_serial 在没有内核串行驱动程序干扰的情况下正常工作，请如前文 FIR 部分所述，将后者分离：

```bash
bash> setserial /dev/ttySX uart none
```

根据你的红外设备，你可能需要用更合适的低级 LIRC 驱动程序替换 lirc_serial。

3. 一个名为 lirctd 的用户模式守护进程，它运行在低级 LIRC 驱动程序之上。Lircd 解码来自遥控器的信号，是 LIRC 的核心。对许多遥控器的支持以用户空间驱动程序的形式实现，它们是 lircd 的一部分。Lircd 向更高层的应用程序导出了一个 UNIX 域套接字接口 /dev/lircd。通过 /dev/lircd 连接到 lircd 是编写支持 LIRC 的应用程序的关键。
4. 一个名为 lircmd 的 LIRC 鼠标守护进程，它运行在 lircd 之上。Lircmd 将来自 lircd 的消息转换为鼠标事件。这些事件可以从命名管道 /dev/lircm 读取，并输入到诸如 gpm 或 X Windows 等程序中。
5. 诸如 *irecord* 和 *irsnd* 等工具。前者记录从遥控器接收的信号，并帮助你为新的遥控器生成 IR 配置文件。后者从你的 Linux 机器流式传输 IR 命令。

请访问托管在 www.lirc.org 的 LIRC 主页下载所有这些内容，并了解其设计和使用的详细信息。

## IR 字符驱动程序

如果你的嵌入式设备仅需要简单的红外接收功能，它可能使用的是微型化红外接收器（例如 Vishay Semiconductors 的 TSOP1730 芯片）。一个应用设备示例是安装在病房内的红外定位器，用于读取护士佩戴的红外徽章发出的数据。在此场景中，由于不存在 IrDA 协议交互，IrDA 协议栈并不相关。如果定位器使用精简的专有协议来解析接收到的数据，那么将 LIRC 移植到定位器上可能也是杀鸡用牛刀。一个简单的解决方案可能是实现一个微小的只读字符或杂项驱动程序，通过 /dev 或 /sys 接口将原始红外数据导出到合适的应用程序。

## 查看源代码

在 drivers/net/irda/ 中查看 IrDA 低级驱动程序，在 net/irda/ 中查看协议实现，并在 include/net/irda/ 中查看头文件。实验 proc/sys/net/irda/* 以调整 IrDA 协议栈，并探索 /proc/net/irda/ 以获取与不同 IrDA 层相关的状态信息。

表 16.3 列出了本部分使用的主要数据结构及其在源代码树中的位置。表 16.4 列出了本部分使用的主要内核编程接口及其定义的位置。

### 表 16.3. 数据结构摘要

| 数据结构 | 位置 | 描述 |
| --- | --- | --- |
| dongle_driver | drivers/net/irda/sir-dev.h | Dongle 驱动程序入口点 |
| sir_dev | drivers/net/irda/sir-dev.h | SIR 设备的表示 |
| qos_info | include/net/irda/qos.h | 服务质量信息 |

### 表 16.4. 内核编程接口摘要

| 内核接口 | 位置 | 描述 |
| --- | --- | --- |
| irda_register_dongle() | drivers/net/irda/sir_dongle.c | 注册一个 dongle 驱动程序 |
| irda_unregister_dongle() | drivers/net/irda/sir_dongle.c | 取消注册一个 dongle 驱动程序 |
| sirdev_set_dtr_rts() | drivers/net/irda/sir_dev.c | 操作连接到 IR 设备的串行端口上的调制解调器控制线 |
| sirdev_raw_write() | drivers/net/irda/sir_dev.c | 写入连接到 IR 设备的串行端口 |
| sirdev_raw_read() | drivers/net/irda/sir_dev.c | 从连接到 IR 设备的串行端口读取 |

