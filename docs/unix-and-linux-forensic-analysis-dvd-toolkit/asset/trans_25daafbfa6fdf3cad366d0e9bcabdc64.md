

# 初始分检与现场响应：数据分析 • 第 91 章

对于未连接的套字，如果其对应的进程正在等待连接请求。其他标志位通常不予关注。

- **类型 (Type)**：套字访问的类型：
    - **DGRAM** 用于数据报（无连接）模式
    - **STREAM** 流式（连接）套字
    - **RAW** 原始套字
    - **RDM** 可靠递送的消息
    - **SEQPACKET** 顺序数据包套字
    - **PACKET** 原始接口访问套字

- **状态 (State)**：
    - **FREE** 未分配
    - **LISTENING** 正在监听连接请求。这些套字套字仅在设置了 -a 开关时才会显示。
    - **CONNECTING** 正在建立连接。
    - **CONNECTED** 已连接。
    - **DISCONNECTING** 正在断开。
    - **(empty)** 未连接到另一个套字。

最后两列是 I-Node 和路径（Path），它们标识附加到套字上的进程。由于可能会出现大量条目，而你无法判断哪些是正常的、哪些不是，请务必联系客户的系统和网络管理员，帮助你建立“正常”运行参数的基准。此外，仅使用互联网搜索引擎就可以为你提供有关进程性质的良好信息。由于进程非常多，这应该仅用于那些看起来可能超出客户管理员团队判定的正常范围的进程。

带有“-rn”开关的 `netstat` 命令将显示主机的路由表。（见图 4.10。）

## 图 4.10 显示主机路由表

```
root@Forensic3:#
root@Forensic3:# -netstat -rn
Kernel IP routing table
Destination     Gateway      Genmask      Flags  MSS Window  irtt Iface
192.168.10.10   0.0.0.0      255.255.255.0   U       0             0       0 eth0
0.0.0.0         192.168.10.100  0.0.0.0        UG      0             0       0 eth0
root@Forensic3:# 
```

如图 4.10 所示，你可以看到路由的去向以及在使用哪个网关。在没有使用网关的情况下，该列将显示一个星号 (*)。下一列显示路由的“通用性”，换句话说，就是该特定路由的网掩码。再一列显示可以设置的标志。标志分解如下：

- Gateway（网关）
- 正在使用的接口已启用（Up）
- 通过该路由只能到达单个主机，例如环回地址
- 路由路由是动态创建的（Dynamically）
- 已由互联网控制消息协议 (ICMP) 重定向修饰
- ! 该路由为拒绝（reject），数据包将被丢弃

## 运行进程 (Running Processes)

了解你正在分析的主机上运行了什么是非常重要的。这可以通过几个不同的命令来实现。在本书中，我只涵盖了“ps aux”和“top”（见图 4.11。）

## 图 4.11 "ps aux" 和 "top"

| USER | PID | TTY | PRIME | %MEM | %CPU | VSZ | RSS | STAT | START | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | 2 | | | 0 | 0 | 0 | 16888 | S | Apr 10 | 0 | [kthread] |
| root | 3 | | | 0 | 0 | 0 | 16888 | S | Apr 10 | 0 | [kthread/2] |
| root | 4 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [kthread/3] |
| root | 5 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [kthread/4] |
| root | 6 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [kthread/5] |
| root | 7 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [kthread/6] |
| root | 8 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [kthread/7] |
| root | 9 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [kthread/8] |
| root | 10 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/1] |
| root | 11 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/2] |
| root | 12 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/3] |
| root | 13 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/4] |
| root | 14 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/5] |
| root | 15 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/6] |
| root | 16 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/7] |
| root | 17 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/8] |
| root | 18 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/9] |
| root | 19 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/10] |
| root | 20 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/11] |
| root | 21 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/12] |
| root | 22 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/13] |
| root | 23 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/14] |
| root | 24 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/15] |
| root | 25 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/16] |
| root | 2114 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [unknown] |
| root | 2115 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [unknown] |
| root | 2116 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [unknown] |
| root | 2117 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [unknown] |
| root | 2118 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/bin] |
| root | 2119 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/lib/firefox-bin] |
| root | 2120 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/lib/firefox-bin] |
| root | 2121 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/lib/firefox-bin] |
| root | 2122 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/lib/firefox-bin] |
| root | 2123 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/lib/firefox-bin] |
| root | 2124 | | | 0 | 0 | 0 | 31564 | S | Apr 10 | 0 | [/usr/lib/firefox-bin] |
| root | 2221 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/17] |
| root | 2222 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/18] |
| root | 2223 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/19] |
| root | 2224 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/20] |
| root | 2225 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/21] |
| root | 2226 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/22] |
| root | 2227 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/23] |
| root | 2228 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/24] |
| root | 2229 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/25] |
| root | 2230 | | | 0 | 0 | 0 | 10234 | S | Apr 10 | 0 | [events/26] |
| root | 2501 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [journald] |
| root | 2502 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [daemon] |
| root | 2503 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [cron] |
| root | 2504 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [klogd] |
| root | 2505 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-udev] |
| root | 2506 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-udev] |
| root | 2507 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-resolve] |
| root | 2508 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-resolve] |
| root | 2509 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-timesd] |
| root | 2510 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-timesd] |
| root | 2511 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-logd] |
| root | 2512 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-logd] |
| root | 2513 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-logd] |
| root | 2514 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-logd] |
| root | 2515 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [systemd-logd] |
| root | 2516 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2517 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2518 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2519 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2520 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2521 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2522 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2523 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2524 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2525 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2526 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2527 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2528 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2529 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2530 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2531 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2532 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2533 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2534 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2535 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2536 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2537 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2538 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2539 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2540 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2541 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2542 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2543 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2544 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2545 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2546 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2547 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2548 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2549 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2550 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2601 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2602 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2603 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2604 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2605 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2606 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2607 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2608 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2609 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2610 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2611 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2612 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2613 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2614 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2615 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2616 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2617 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2618 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2619 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2620 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2621 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2622 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2623 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2624 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2625 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2626 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2627 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2628 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2629 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |
| root | 2630 | | | 0 | 0 | 0 | 7696 | S | Apr 10 | 0 | [dlogd] |

了解你正在分析的主机上运行了什么是非常重要的。这可以通过几个不同的命令来实现。在本书中，我只涵盖了“ps aux”和“top”（见图 4.11。）

`ps aux` 命令以 BSD 语法显示所有运行的进程，如图 4.11 所示，输出被分为 11 列。在取证调查中，这些列中最重要的“USER”、“TTY”和“COMMAND”。取决于你想要确定的，每一列都有其重要性，并且可以使用文本工具（如 Textpad!）或从命令行中使用 `grep` 进行解析。无论情况如何，这些条目都会告诉你是谁启动了进程、从哪里启动、何时启动以及使用了什么命令。

