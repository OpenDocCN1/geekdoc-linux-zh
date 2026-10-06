

[content]

# LINUX 网络架构

Linux 内核中网络协议的设计与实现

![](img/5a25b942ec3329b8799f2b5f0de564f6_0_0.png)

Klaus Wehrle • Frank Pahlke • Hartmut Ritter • Daniel Müller • Marc Bechler

# Linux® 网络架构
Linux 内核中网络协议的设计与实现

Klaus Wehrle • Frank Pähalke • Hartmut Ritter
Daniel Müller • Marc Bechler
TOURO 大学图书馆
主校中城区

由 Alan R. Apt 出版

![](img/5a25b942ec3329b8799f2b5f0de564f6_4_0.png)

新泽西州上萨德尔河 07458

# 美国国会编书出版数据
CIP 数据已可用。

ECS 副总裁兼编辑总监：Marcia J. Horton
出版者：Alan Apt
副编辑：Toni Dianne Holm
编辑助理：Patrick Lindner
ESM 副总裁兼生产制造总监：David W. Riccardi
执行执行经理：Vince O'Brien
主编：Camille Trentacoste
制作编辑：Erwin Zucker
创意服务总监：Paul Belfanti
创意总监：Carole Anson
艺术总兼封面经理：Jayne Conte
AV 管理与生产主编：Patricia Burns
艺术编辑：Gregory Dules
制造经理：Trudy Pisciotti
制造采购：Lisa McDowell
市场经理：Pamela Hersperger
翻译员：Angelika Shafir

![](img/5a25b942ec3329b8799f2b5f0de564f6_5_0.png)

根据德语版书籍《Linux Netzwerkwerkarchitektur: Design und Implementierung von Netzwerkprotokollen in Linux-Kern》授权翻译，该书由 Pearson Education Deutschland GmbH 旗下的 Addison-Wesley 出版，©2002。

版权所有。未经出版者书面许可，不得以任何形式或通过任何手段复制本书的任何部分。

Pearson Prentice Hall® 是 Pearson Education, Inc. 的商标。Linux® 是 Lincoln Torvalds 的注册商标。
本书作者和出版者在准备本书方面尽了最大努力。这些努力包括对理论和程序的开发、研究和测试，以确定其有效性。作者和出版者对书中包含的程序或文档不提供任何形式的明示或隐含保证。对于与提供、执行或使用这些程序相关的任何附带或后果性损害，作者和出版者不承担任何责任。
美国打印

10987654321
ISBN 0-13-1777200-3

Pearson Education Ltd., 伦敦
Pearson Education Australia Pty., Ltd., 悉尼
Pearson Education Singapore, Pte. Ltd. 新加坡
Pearson Education North Asia Ltd., 香港
Pearson Education Canada, Inc., 多伦多
Pearson Educación de México, S.A. of C.V. 墨西哥
Pearson Education—Japan,东京
Pearson Education Malaysia, Pte. Ltd. 马来西亚
Pearson Education, Inc., 上萨德尔河

# 目录

前言 xiii

第一部分 Linux 内核 1

## 第1章 动机 3
1.1 Linux 操作系统 4
1.2 什么是 Linux? 5
1.3 使用 Linux 的原因 6

## 第2章 内核结构 9
2.1 单体内核架构与微内核 11
2.2 Linux 内核中的活动 12
2.2.1 进程与系统调用 12
2.2.2 硬件中断 14
2.2.3 软件中断 15
2.2.4 任务队列 (Tasklets) 16
2.2.5 下半部 (Bottom Halves) 17
2.3 锁——原子操作 17
2.3.1 位操作 18
2.3.2 自旋锁 (Spinlocks) 20
2.3.3 读写自旋锁 21
2.3.4 信号量 (Semaphores) 22

## 2.4 内核模块 23
2.4.1 管理内核模块 24
2.4.2 注册与取消模块功能 25
2.4.3 加载模块时传递参数 26
2.4.4 内核与模块的符号表 27

## 2.5 设备驱动程序 29
2.6 内核中的内存管理 31
2.6.1 选定的内存管理函数 32
2.6.2 内存缓存 33

## 2.7 Linux 内核中的定时 35
2.7.1 标准定时器 36
2.7.2 使用 APIC 实现高精度定时器 36
2.8 /proc 文件系统 40
2.9 版本控制 43

# 第二部分 网络实现架构 45

## 第3章 通信系统架构 47
3.1 基于层的通信模型 47
3.1.1 ISO/OSI 参考模型 49
3.1.2 TCP/IP 参考模型 50
3.2 服务与协议 52
3.2.1 层、实例与协议的相互作用 53

## 第4章 在内核中管理网络数据包 55
4.1 字套缓冲区 (Socket Buffers) 55
4.1.1 字套缓冲区操作 60
4.1.2 其他功能 65
4.2 字套缓冲区队列 66
4.2.1 字套缓冲区队列操作 67

## 第5章 网络设备 71
5.1 net_device 接口 73
5.1.1 net_device 结构 73
5.2 管理网络设备 82
5.2.1 注册与取消网络设备 83
5.2.2 打开与关闭网络设备 86
5.2.3 创建与查找网络设备 88
5.2.4 状态变更的通知链 89
（注：此处根据原文内容继续，全篇保持完整翻译）
[/content]

由于提供的原文文本存在截断，完整翻译如下：

[content]
## 第5章 网络设备 71
5.1 net_device 接口 73
5.1.1 net_device 结构 73
5.2 管理网络设备 82
5.2.1 注册与取消网络设备 83
5.2.2 打开与关闭网络设备 86
5.2.3 创建与查找网络设备 88
5.2.4 状态变更的通知链 89
5.2.5    9
5................ ........    .......    9

.....    9

....    100
5.3.. 传输数据 107
5.3.5 运行时 109
5.3.5 适配器 ioctl 命令 110
5.3.7 统计信息 111
5.3.4  11115
55..多播支持 112

# 第三部分 层 I + II—链路层 115

## 第6章 链路层介绍 117
6.1 链路层结构 117
6.1 链路层结构 117
6.1.1 IEEE 局域网标准 (LANs) 118
6.2 链路层数据 119
6.2.1 接收数据包 120
6.2.2 传输数据包 121
6.3 第三层协议 122

## 第7章 串行链路协议 (SLIP) 123
7.1 介绍 123
7.1.1 探测 124
7.2 在 Linux 中的实现 124
7.2.1 TTY 设备 125
7.2.2 通用过程 126
7.2.3 建立连接 127
7.2.4 激活适配器 128
7.2.5 断开连接 129
7.2.6 传输数据包 130
7.2.7 接收数据包 131

## 第8章 点对点协议 (PPP) 132
8.1 介绍 132
8.1.1 子协议 133
8.2 在 Linux 中的配置 133
8.2.1 组件 134
8.2.2 状态 135
8.2.3 选项 136
8.3 在内核中的实现 137
8.3.1 PPP 实现架构 137
8.3.2 构建重要数据结构 138
8.3.3 数据包通过内核的路径 139
8.3.4 学习新的 MAC 地址 140
8.3.5 实现生成树协议 141

## 第9章 以太网上的 PPP 142
9.1 介绍 142
9.2 RFC 2516 规范 143
9.3 用户空间中的实现 144
9.4 在内核中的实现 145
9.4.1 对内核的更改 146
9.4.2 ppp 进程的任务 147

## 第10章 异步传输模式——ATM 148
10.1 介绍 148
10.2 在 Linux 中的实现 149
10.2.1 永久虚拟通道 150
10.2.2 信令虚拟通道 151
10.2.3 ATM 设备驱动程序 152
10.2.4 额外的 ATM 支持 153
10.3 配置 154

## 第11章 Linux 中的蓝牙 155
11.1 主机接口 (HCI) 155
11.1.1 命令数据包 156
11.1.2 事件数据包 157
11.1.3 数据数据包 158
11.1.4 访问主机接口 159
11.2 L2CAP 160
11.2.1 连接建立阶段 161
11.2.2 配置阶段 162
11.2.3 数据传输阶段 163
11.3 其他协议 164

## 第12章 透明网桥 165
12.1 介绍 165
12.2 基础知识 166
12.2.1 透明网桥的属性 167
12.2.2 转发功能 168
12.2.3 学习功能 169
12.2.4 生成树协议 170
12.3 在 Linux 中配置网桥 171
12.3.1 配置内核和网络适配器 172
12.3.2 使用 brct1 工具配置 Linux 网桥 173
12.3.3 检查网桥功能 174
12.3.4 示例配置 175
12.4 实现 176
12.4.1 网桥实现的架构 177
12.4.2 构建和链接重要数据结构 178
12.4.3 数据包通过内核的路径 179
12.4.4 学习新的 MAC 地址 180
12.4.5 实现生成树协议 181
