
## 其他设备如何处理 SYN

其他边界设备（如防火墙）也可以提供针对 SYN 洪水的某些保护，例如 Check Point Software Firewall-1 `SYNDender`。它提供了两种 SYN 洪水保护方法，分别名为 `SYNDender Relay` 和 `SYNDender Gateway`。与 `TCP Intercept` 类似，`SYNDender Relay` 在三次握手完成之前充当中间人。只有在收到 Firewall-1 的 `SYN/ACK` 回复后，才会向防火墙后的服务器。

`SYNDender Gateway` 解决方案采用了不同的方法，让 `SYN` 直接通过防火墙到达服务器。当服务器发送 `SYN/ACK` 时，`SYNDender` 响应 `ACK`。这意味着服务器认为握手已完成，随后连接就会被移出连接队列。

> 你是蓝精灵（Smurf）攻击吗？为了确保您的网络不是 Smurf 攻击的违愿参与者，请在边缘设备上配置适当的出口和入站过滤器。对于 Cisco 设备，IOS 版本...

## 定位和移除僵尸连接的方法

有许多工具可以协助识别和恢复。还有人编写了停止攻击的程序。好消息是，这些工具大部分都是免费的。

## DDoS 攻击：目的、工具与防御

`TFN2K` 客户端、`TFN2K` 守护进程、`trino` 守护进程、`trino` 主、`TFN` 守护进程、`Stacheldrakt` 守护进程、`Stacheldrakt` 客户端以及 `Trinity v3`。

该工具通过将文件与 DDoS 程序进行对比，甚至可以检测是否有程序正在运行。与大多数软件一样，它并不是 100% 万无一失，可能会产生误报，但它仍然是一个非常有价值且值得投入的工具。你可以从 `www.nipc.gov` 下载 `Find_ddos`。

## 使用 Zombie Zapper

`Zombie Zapper` 由著名的安全公司 `Bindview` 开发，它为管理员提供了一种简单的方法，可以指令正处于攻击中的守护进程停止运行。`Zombie Zapper` 有两个版本——一个适用于 UNIX，另一个适用于 Windows。

通常情况下一样，UNIX 版本是命令行驱动的，而 Windows 版本具有图形化前端。`Zombie Zapper` 可以指令 `trino`、`TFN`、`Stacheldrakt`、`Wintrinoo` 和 `Shaft` 守护进程停止攻击。使用 `Zombie Zapper` 有几点注意事项，如下：

- 它假设在编译相关二进制文件时使用了默认密码。
- 它会完全停止 `trino` 守护进程，但对于所有其他守护进程，它只是停止正在进行的攻击（这有助于定位这些守护进程）。
- 它不支持 `TFN2K`。
- 如果你是攻击的接收者，并尝试关闭第三方网络上的守护进程，请记住，由于数据包欺骗，你可能误将 `Zombie Zapper` 指向了错误的网络，或者 `Zombie Zapper` 发出的指令可能会被路由器和防火墙等安全设备过滤。
- 它需要 `libnet 1.0` 或更高版本。`Libnet` 是一系列例程和函数，便于创建感知网络状态应用程序和实用程序。

请参阅图 2.9 查看 `Zombie Zapper` 的 UNIX 版本。UNIX 版 `Zombie Zapper` 二进制文件名为 `zz`，具有多个参数可以微调其运行。Windows 版本提供了一个友好的界面，但经验丰富的管理员可能更倾向于查看使用 `-vv` 提供的详细信息。使用 UNIX 版本，你甚至可以伪造 `Zombie Zapper` 生成的守护进程包（非常调皮！）。

可以从 `www.packetfactory.net/libnet` 下载 `libnet`，从资源丰富的 `Bindview Razor` 团队的 `razor.bindview.com/tools` 下载 `Zombie Zapper`。

### 图 2.9 Zombie Zapper 的 UNIX 版本

执行此命令提供所有 `Zombie Zapper` 参数的完整列表。

编译 `Zombie Zapper`，请安装 `libnet 1.0` 或更高版本。完成后，运行截图所示的命令来编译 `Zombie Zapper`。

```
C:\Windows\system32>cmd 12:15

gcc 24March2002 -I/include -`libnet-config --defines -o zz zz.c -linet

24March2002 -I/include -o zz zz.c -linet

Zombie Zapper

Bugs/comments to the zombierazzer.bindview.com

More information is available at http://www.bindview.com/razor/bindview.com

Copyright (c) 2000 Bindview Development

./zz [-a 0-5] [-c class C] [-d de] [-h] [-n host] [-s src] [-u udp] [-v] hosts

  -antiddos type to kill

    - all

    - blackhole

    - trident

    - cronos

    - windows

  - class C in x.v.w form

  -f time all packets (default 0)

  - grab host IP from them (default 0)

  - help

  - show (details, only one host)

  - spoof source address (cast in case)

  - mid-address target for more targets

  - use mask mode (for more verbosity)

  - host and then handle (ending -c)

24March2002 -zz -c class C 192.168.1.1

Bugs/comments to the zombierazzer.bindview.com

More information is available at http://www.bindview.com/razor/bindview.com

Copyright (c) 2000 Bindview Development
```

使用 `-option` 允许 `Zombie Zapper` 瓦灭整个 C 类网络。

## 使用 tfn2kpass

`TFN2K` 编译时的一个选项使其不受 `Zombie Zapper` 及其类工具的影响。在编译 `TFN2K` 时，它会要求一个密码用于加密，允许 `TFN2K` 绕过 `Zombie Zapper` 的默认密码漏洞。但别担心，`tfn2kpass` 提供了随随随帮助。

`tfn2kpass` 由 `Simple Nomad` 开发，以源码形式分发，可以在 `Solaris`、`Linux` 和 `FreeBSD` 上编译。编译后的代码可从 `TFN2K` 二进制文件或 `tfn` 中提取密码。这在许多场景中非常有用：

- 如果你发现网络上的主机已被攻破，可以使用恢复的密码重新编译一组新的 `TFN2K` 二进制文件。使用这个新编译的 `tfn` 版本，管理员可以命令运行守护进程 `td` 的主机停止攻击。
- 在信息收集阶段，密码可以作为证据，或者可能被攻击者用于其他受密码保护的代码。

`tfn2kpass` 的源码可以在 `http://razorbindview.com/tools/` 下载。通过运行以下命令可以轻松实现源码的编译和运行：

```
gcc -o tfn2kpass tfn2kpass.c
```
