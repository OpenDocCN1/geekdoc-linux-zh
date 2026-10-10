

这是一种在笔记本电脑上启用漫游访问（受无线网卡限制）的简便方法。其他商用网卡可能具有更远的传输距离能力，但通过使用这种方法，你可以以不到 170 美元（美国）的成本构建一个小型无线网络。

## 无线调制解调器

如果你需要在旅途中连接到你的 ISP（互联网服务提供商），也可以尝试使用 Metricom 的 Ricochet 调制解调器。虽然它目前仅支持 28.8Kbps 的无线连接速度，但该服务计划在 2000 年末升级至 128Kbps。Ricochet 调制解调器的体积大约相当于两副扑克牌，并连接到笔记本的串行端口。该设备重约 14 盎司，使用 NiMh（镍氢）可充电电池，可提供大约六小时的连接时间。

移动 Linux 用户报告在使用 Ricochet 设备时取得了巨大成功，但服务区仅限于美国的主要城市、机场、大学和 corporate campuses（企业园区）。你还需要向 Metricom 注册服务，因为 Ricochet 被设计为仅与 Metricom 的网络和服务器连接。该服务提供动态 IP 地址分配、电子邮件和新闻源。通过有线线路拨号连接到 Metricom 的服务器是作为一个可选项提供的。

## 无线蜂窝连接

如果你需要在旅途中无线访问互联网，但找不到电话插孔，你可以使用几种基于蜂窝网络的系统和手机来拨打你的 ISP。你所使用的技术类型、服务和手机可能由当地电话服务提供商、服务区（地理）覆盖范围、功能和价格决定。基本上，普通移动用户通常可以使用四种类型的服务，每种服务都有其优点和缺点。

### CDMA

码分多址（CDMA）是另一种结合扩频频率管理和小单元半径来提供数据传输的蜂窝技术。与 TDMA 或 GSM（稍后讨论）相比，这种数字服务的速度较慢，但其优势在于你可以将手机用作调制解调器，并使用直接插入笔记本串行端口的连接器。虽然手机内部没有实际的调制解调器，但从你的计算机拨号时会免提拨打手机，连接网络上的调制解调器会为你完成连接和传输，通常速度为 19.2Kbps。

### IDEN

集成数字增强网络（IDEN）结合了数字手机、无线电、寻呼机和调制解调器技术。此服务使用内置调制解调器的手机，并且可以直接与你的笔记本电脑配合使用。

### GSM

最初于 1982 年命名为 Groupe Speciale Mobile（特别移动组），GSM 现在代表全球移动通信系统（Global System for Mobile Communications）。它还允许全球漫游。此服务允许直接将 GSM 手机连接到你的笔记本串行端口，或通过 PCMCIA 蜂窝调制解调器进行连接。

### TDMA

时分复用（TDMA）使用不同的时隙来传输多个数据流。使用这种模拟服务通常可以获得更高的传输速度，但大多数手机需要带有蜂窝连接器和线缆的外部 PCMCIA 调制解调器卡。

例如，使用 Spring PCS 服务（基于 CDMA）和 Motorola StarTAC 及连接线，你可以设置 kppp 以 19.2kbps 的速度拨号连接到你的 ISP。然而，在配置直接通过笔记本串行端口进行蜂窝连接的调制解调器速度时，你必须使用 setserial 命令以确保使用严格的传输速率，否则呼叫可能无法接通。

为此，请使用 setserial 命令的 `spd_normal` 选项，并加上你将要使用的串行端口的设备名称。连接你的手机和笔记本电脑，打开手机，并像这样使用 setserial：

```bash
# setserial /dev/ttyS0 spd_normal
```

在此示例中，手机连接到笔记本的 COM1 端口。然后，你需要配置 kppp（也许创建一个"roaming"漫游账户！）以使用 /dev/ttyS0 和适当的连接速度。

### 网络连接策略

如果你在旅途中或远离局域网（LAN）需要建立连接，首先检查你的 ISP 是否有 800 号码。如果没有，请在出发前检查你的 ISP 覆盖区域，并获取本地电话号码列表以匹配你的行程。没有什么比试图在互联网无法连接时浪费时间寻找本地接入号码更糟糕的了！

如果你需要访问你的局域网（LAN），并且不介意支付长途电话费（或者如果你的蜂窝服务提供商提供免费的长途通话），你可以将 Linux 系统配置为拨号访问。

## 设置拨号接入

将 Linux 系统设置为支持拨号接入非常容易。你需要一台带有调制解调器和电话线的计算机来接听电话。如果你的计算机连接了两条电话线，登录之后，你可以拨出连接到你的 ISP 以发送和接收软件。

编辑系统的初始化表 /etc/inittab，并查找以下行：

```bash
# Run getty in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

每一行代表不同的 Linux 运行级别。当你不使用 X11 而使用 Linux 时，你在运行级别 3 下运行 Linux。当你使用带有 Red Hat 或 Mandrake Linux 的 X11 时（注意其他发行版可能使用不同的运行级别），你使用运行级别 5。你的 /etc/inittab 文件中的第一行之一显示了默认的运行级别；它可能看起来像这样：

```bash
id:5:initdefault:
```

为了让 Linux 接听电话并允许你登录，你需要使用 `agetty` 命令而不是 `/sbin/mingetty` 命令来监控运行级别 3。你还需要指定调制解调器使用的串行端口。将这一行：

```bash
3:2345:respawn:/sbin/mingetty tty3
```

更改为：

```bash
3:2345:respawn:/sbin/agetty -w -I "ATE0Q1&D2&C1S0=1\015" 115200 ttyS0 vt100
```

`agetty` 命令会自动初始化你的调制解调器以接听电话，使用你的调制解调器的 S0 寄存器（在此示例中设置为第一次响铃时接听）。请注意，调制解调器连接到计算机的 COM1 端口。

### 需要查找 agetty？

如果你的 Linux 发行版不包含 agetty，你可以浏览以下地址快速找到一份副本：

```
ftp://metalab.unc.edu/pub/Linux/system/serial/getty/
```

Alan Wendt 的 agetty 命令非常简单但运行良好。如果你不想使用 agetty，也可以使用 mgetty 或 ugetty。在 /usr/doc/mgetty+sendfax 目录下查看有关设置拨号接入的详细信息。如果你需要更多信息，还可以查阅 Serial-HOWTO，通常可以在 /usr/doc/HOWTO 目录下找到。

保存你的更改，然后使用 shutdown 命令及其 -r（重启）选项重启你的系统，例如：

```bash
# shutdown -r now
```

Linux 将在启动后启动 agetty 命令，agetty 将监控你的 /dev/ttyS0 串行端口以接收传入的呼叫。当你拨入时，agetty 将接听电话，并且在你（可能）按下回车键后，你将看到一个 login: 提示符。务必在出发前测试你的设置！

### 额外服务

通过为 PPP 创建特殊用户账户或编辑 /etc/inittab 中的 gettry 条目，你也可以提供通过拨号连接的 PPP 服务。这样做的好处是允许你直接通过电话使用 FTP，或者直接将电子邮件发送回你的笔记本电脑。首先，启用拨号接入服务，然后创建一个 ppp 用户。但是，你需要将默认的 /etc/passwd 条目从：

```
ppp:x:501:501::/home/ppp:/bin/bash
```

更改为：

```
ppp:x:501:501::/home/ppp:/usr/sbin/pppd
```

然后，你应该在 /home/ppp 目录中创建并编辑一个名为 .ppprc 的文件，其中包含以下内容：

```
detach
modem
crtcts
lock
192.168.2.50
```

保存该文件并重启你的计算机。当你登录时，pppd 服务器会将 IP 地址 192.168.2.50 分配给你的笔记本电脑（确保你的服务器有不同的 IP 地址！）。然后你可以检索电子邮件、使用 FTP，或者如果已启用，通过 telnet 登录到服务器以进入你的主目录。

## 免费服务

在旅途中保持连接的另一种方法是使用 Web 浏览器注册免费互联网邮件账户，例如在 http://www.yahoo.com。然后，你可以使用任何开放的终端，例如在公共图书馆或网络咖啡馆，通过基于 Web 的电子邮件账户发送和接收邮件。

如果你可以访问电话，并且在美国大多数主要城市内部或周围旅行，你可以在 http://www.teledyn.com/products/PreseMD/ 注册免费的面向 Linux 的拨号 PPP 互联网服务。

你需要注册，但之后你将获得一个本地接入号码。（如果你需要其他号码，请在注册期间记下。）这是一项完整的全国 ISP 服务！

## 资源信息

- [http://pcmcia.sourceforge.org/](http://pcmcia.sourceforge.org/)
  有关 Linux 对 PCMCIA 支持的最新信息。

- [ftp://sourceforge.org/pcmcia/](ftp://sourceforge.org/pcmcia/)
  获取适用于 Linux 的最新 PCMCIA 驱动程序（内核模块）的地方。

- [http://www.linmodem.org](http://www.linmodem.org)
  关于使用软件调制解调器与 Linux 的替代观点，以及指向技术详情、软件驱动程序和源代码的链接。

- [Serial-HOWTO](http://www.linuxdoc.hq)
  David S. Lawver 编写的关于使用串行端口和 Linux 的指南。可在 /usr/doc/HOWTO 目录下或 http://www.linuxdoc.hq 找到。

- [http://www.computercraft.com/docs/hayescom.html](http://www.computercraft.com/docs/hayescom.html)
  大多数标准 Hayes AT 调制解调器命令的交叉参考列表。

