
- **编译并运行节点**：一旦创建了两个节点，你就需要编译并运行它们。你可以使用以下命令完成：

```
cd ~/catkin_ws
catkin_make
source devel/setup.bash
roscore
```

在新终端中，运行发布者节点：

```
rosrun beginner_tutorials talker
```

在另一个终端窗口中，运行接收者节点：

```
rosrun beginner_tutorials listener
```

你现在应该看到发布者节点在 `chatter` 话题上发布消息，接收者节点打印这些消息。以下是运行这些节点的步骤总结：

1. 创建 `ROS` 程序包。
2. 创建发布者节点。
3. 创建接收者节点。
4. 编译并运行节点。

你应该看到发布者节点在 `chatter` 话题上发布消息，接收者节点订阅该话题。发布者节点以 10 Hz 的频率在话题上发布消息，接收者节点打印收到的消息。接收者节点运行时，你应该看到类似下面的输出：

```
I heard: [0]
I heard: [1]
I heard: [2]
I heard: [3]
I heard: [4]
```

## ROS 工具

这里有一个关于常用 `ROS` 工具的表格，包括类似于 `echo` 的 `rostopic`：

| 工具 | 说明 |
|---|---|
| `roscore` | 提供节点间通信的核心服务。 |
| `rostopic` | 显示关于话题信息的工具，包括发布和订阅话题。 |
| `rostopic echo` | 打印话题上发布的消息。类似于 `echo` 命令。 |
| `rosrun` | 运行 `ROS` 节点的工具。 |
| `roslaunch` | 启动多个 `ROS` 节点并设置其参数。 |
| `rosbag` | 记录和回放 `ROS` 消息的工具。 |
| `rosmsg` | 显示 `ROS` 消息类型的工具。 |
| `rosparam` | 设置和获取 `ROS` 参数的工具。 |
| `rosservice` | 与 `ROS` 服务交互的工具，包括查询可用服务和调用。 |
| `roswho` | 用于诊断 `ROS` 系统问题的工具。它可以识别... |

这些工具对于使用 `ROS` 至关重要，可以用于调试、监控和管理 `ROS` 节点和话题。特别是 `rostopic echo` 工具，监控话题发布的消息对于调试和理解 `ROS` 节点之间的通信非常有帮助。

新兴技术与工厂自动化 (`ETFA`)，德国柏林，2016年9月6–9日：第 1–9 页。[Google 学术搜索]

- `Zhou`, `Z.`; `Yan`, `Y.`; `Ruppee`, `S.`; `Berger`, `M.` 时间敏感网络数据包抢占的分析与实现。见 2017 年 `IEEE` 第18 届高性能交换与路由国际会议 (`HPSR`) 论文集，巴西，2017年6月18–21日；第 1–6 页。[Google 学术搜索]
- `Simon`, `C.`; `Malios`, `M.`; `Mate`. 基于时间敏感网络的低延迟服务设计方面。`IEEE Commun. Stand. Mag.` 2018, 48–54。[Google 学术搜索] [CrossRef]
- `Pop`, `P.`; `Raagaard`, `M.L.`; `Crainagas`, `S.`; `Steiner`, `W.` 使用 `IEEE` 时间敏感网络的信息物理分布式系统设计。`IET Cyber-Phys. Syst. Theory` 2016年4月, 1, 86–94。[Google 学术搜索] [CrossRef][绿色版本]
- 以太网标准修订案 5：交错以太网流量的规范与管理参数-`IEEE Std 802.3br-2016`。在线可用于：`http://www.ieee802.1/pages/tsn.html` (访问于 2019年1月22日)。
- `https://www.autosar.org`
- 嵌入式微机系统实时接口第三版，`Jonathan W. Valvano`，德克萨斯大学奥斯汀分校。
- `MicroC/OS-II` 实时内核第二版 `j.labrosse`。
- `RTOS` 概念 `http://www.embeddeddecraft.org`。
- `OSEK/VDX` 操作系统规范 2.2.3
- `AUTOSAR` 分层软件架构
- `Trampoline` 手册，版本 2.0
- `Trampoline (OSEK/VDX)` 测试实现 - 版本 1.0。`Florent PAVIN` ; `Jean-Luc BECENNECH`
- `AUTOSAR` 架构（从零开始学习演示） `Udemy` `Udemy`

`Trampoline`:

一个基于 `OSEK/VDX` 和 `AUTOSAR` 的（小型）嵌入式系统开放平台 `http://trampoline.rts-software.org/` `Jean-Luc Béchennec`1;2, `Sébastien Fauceau`1;3 `IRCCYN` (南特通信与网络安全研究所) 2`CNRS` (法国国家科学研究中心) /3南特大学 第10 届卢瓦尔软件会议 `uReal Time Systems` (`RETSYS`) 会议

`Jean-Luc Béchennec@irccyn.ec-nantes.fr`

`Sébastien Fauceau` - `Sébastien.Fauceau@univ-nantes.fr`

周四 11月12日

`AUTOSAR` 操作系统规范 `V5.0.0` `R4.0` `Rev 3`

`OSEK` - 基础 `http://tainisnotes.blogspot.com/2016/07/osek-basic-task-vs-extended-task.html`

`OSEK OS` 会话演讲者 `Deepak V.`

`M.S Ramiah` 高级系统学院 - 班加罗尔 1

从零开始精通嵌入式系统

版权 © 2023 - `Keroles Khalli`, `eng.keroles.haram@gmail.com`

- `OSEK-OS` 简介 - `CIAA` 操作系统固件

嵌入式系统编程

`MSc. Ing. Mariano Cerdeiro`

- `AUTOSAR` 简介，`Stephen Waldron`，`Vector` 网络研讨会，2014年5月7日周三

`https://vector.com/portal/medien/cmc/events/Webinars/2014/Vector_Webinar_AUTOSAR_In_introduction_20140507_EN.pdf`

- `AUTOSAR` 简介，`Stephen Waldron`，`Vector` 网络研讨会，2015年5月5日周二

`https://vector.com/portal/medien/cmc/events/Webinars/2015/Vector_Webinar_AUTOSAR_In_introduction_20150505_EN.pdf`

- `AUTOSAR` 适应平台

`https://www.vector.com/conference_india/files/presentations/Day1/3_AUTOSAR_20Adaptive_Platform.pdf`

- `AUTOSAR` 诊断通信管理器规范

`https://www.autosar.org/fileadmin/user/upload/standards/classic/AUTOSAR_DCM.pdf`

- 汽车与嵌入式系统信息

`https://automotiveembedded.com/memory-stack/`

- 构建嵌入式 `Linux` 系统，第二版
- 精通 `Linux` 编程 - 第二版
- `Christopher Hall`, 嵌入式 `Linux` 入导, `Prentice Hall`, 2006.
- `Silberschatz`, `Galvin`, and `Gagne` 的《操作系统》，第八版。
- `Robert love` `linux` 内核开发第三版 2010
- `Mark Mitchell`, `Oldham`, `Alex Samuel` `Advanced Linux`
- 嵌入式系统中的 `OS` 与 `Linux` 内核原理
- 内存管理、分页、虚拟内存、文件系统及其实现、存储(`HDD`)
- `Yocto` 项目与 `OpenEmbedded` 开发
- `Linux` 内核和驱动开发
- 嵌入式 `Linux` 培训 `https://bootlin.com/training/` 内存管理文章

# 参考文献

- 操作系统入门第9课 - 内存管理
- 乌普萨大学计算机架构导论之虚拟内存
- `OS` 笔记 13 - 地址转换、缓存和 `TLB`
- `CSE 331` 操作系统设计
- `CSE 331` 虚拟内存
- `CSE 332` 计算机组织与体系文件系统：基础
- `Linux` 系统编程系统调用，`POSIX`
- `CSE 333` 2019年春季，`Justin Hsia`
- `Linux/Unix` 中的文件权限示例
- `Linux` 简介 -- 12.2 基础 `I/O` 概念
- 与硬件通信应用 `I/O` 接口
- `Linux` 操作系统，教师：`Junfeng Yang`

从零开始精通嵌入式系统

版权 © 2023 – `Keroles Khalil`, `karam@gmail.com`

# 结论
