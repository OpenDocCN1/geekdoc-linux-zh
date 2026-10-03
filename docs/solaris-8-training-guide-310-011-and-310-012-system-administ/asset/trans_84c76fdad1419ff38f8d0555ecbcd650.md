
Solaris 8 引入了一项新功能，能够强制挂起的系统停止。停止系统的新的序列是 <RETURN> <TILDE> <CONTROL B>，等同于 Stop+A。字符之间必须间隔超过 0.5 秒，并且整个字符串必须在五秒内输入完毕。这仅适用于用作控制台的串行设备，而不适用于自带键盘的系统。如果你的控制台通过调制解调器连接到串行端口，你可以通过在 tip 窗口中输入 ~#（波浪号加井号）发送中断（Stop+A 或 L1+A）。

以下是如何从挂起的系统中脱出的示例：

## 逐步操作
### 1.4 脱离挂起的系统
- 1. 使用你系统的中止键序列（Stop+A 或 L1+A）。
监视器显示 ok PROM 提示符。
- 2. 输入 sync 命令以同步磁盘：
`ok sync`
- 3. 当你看到同步文件系统消息时，再次按下你系统的中止键序列。
- 4. 输入适当的 reset 命令以重置硬件并启动引导过程：
`ok reset`
- 5. 在收到 login: 消息后，登录并输入以下内容以验证系统是否已引导到指定的运行级别：
`# who -r`
- 6. 系统会以下列内容响应：
`run-level 3 Jun 9 09:19 3 0 S`

## 关闭电源

只有在关闭文件系统之后才应关闭硬件电源。系统关闭后，关闭所有设备的电源。如有必要，还请拔掉电源线。当可以恢复供电时，请使用以下步骤打开系统和设备。

## 逐步操作
### 1.5 关闭电源
- 1. 插入电源线。
- 2. 打开所有外围设备，如磁盘驱动器、磁带驱动器和打印机。
- 3. 打开 CPU 和显示器。

## 章节摘要

本章回顾了 Solaris 的启动和关闭程序。按正确顺序为系统供电、进入 OpenBoot PROM、引导系统以及加载内核进行了讨论。

接下来，描述了各种系统 init 状态，详细说明了 Solaris 进程和服务如何从引导开始启动并继续到多用户模式。系统管理员可以通过添加和删除运行控制脚本进一步控制这些服务。

最后，我描述了正确关闭系统的重要性，因为如果未执行正确的关闭步骤，数据完整性可能会受到损害。列出了用于有序关闭系统的各种命令。

在下一章中，我将更详细地描述 OpenBoot。在接下来的章节中，你将更多地了解 Solaris 操作环境以及——同样重要——计算机硬件。在能够充分排除系统启动问题之前，必须透彻了解这两个系统组件。

## 关键术语
- 自举
- 引导块
- 运行状态
- Init 状态
- 单用户模式
- 多用户模式
- 运行控制脚本
- 交互式引导
- 重新配置引导

## 应用你的知识
### 练习

警告：由于以下练习中涉及的一些步骤如果操作不当可能会导致系统无法引导，请勿在生产系统上执行这些练习。

### 1.1 引导系统

本练习引导你完成为系统供电和引导系统的步骤。

预计时间：5 分钟

- 1. 打开所有外围设备的电源（如果有）。
- 2. 如果 OpenBoot 参数 auto-boot 设置为 false，系统通电后不久你会看到 ok 提示符。如果系统设置为 auto-boot，你将在屏幕上看到类似以下的消息：
- 3. 在 ok 提示符下，输入 boot 以引导系统。

```
SunOS Release 5.8 Version Generic_108621-04 64-bit
```

```
Copyright 1983-2000 Sun Microsystems, Inc. All rights reserved.
```

你会看到系统开始引导过程。通过按下 Stop+A 键中断引导过程。ok 提示符将会出现。

### 1.2 引导备用内核

在本练习中，你将练习从备份的 /etc/system 文件引导。如果你的 /etc/system 文件损坏或无法引导，请使用此过程。

预计时间：15 分钟

- 1. 以 root 身份登录。
- 2. 通过输入以下命令创建 /etc/system 文件的备份副本：
- 3. 现在通过输入以下命令删除 /etc/system 文件：
- 4. 通过输入以下命令停止系统：
- 5. 在 ok 提示符下，使用交互选项引导系统以提供 /etc/system 文件的备份名称。这是通过输入以下命令完成的：
- 6. 系统会提示你输入内核的文件名和模块的默认目录。对每个问题输入 <return>。当提示使用默认的 /etc/system 文件时：
- 7. 稍后系统会要求你输入根文件系统类型和根设备的物理名称。对这两个问题都输入 <return>。
- 8. 系统准备就绪后，以 root 身份登录，并将原始的 /etc/system 文件放回原处。

```
cp /etc/system /etc/system.orig
```

```
rm /etc/system
```

```
/usr/sbin/shutdown -y -g0 -i0
```

```
boot -a
```

```
Name of system file [etc/system]:
```

输入以下内容：

```
/etc/system.orig
```

```
cp /etc/system.orig /etc/system
```

### 1.3 使用运行控制脚本

在本练习中，练习创建运行控制脚本并关闭系统。

预计时间：10 分钟

- 1. 以 root 身份登录，并切换到 /etc/init.d 目录。将名为 lp 的文件复制为 test。

```
cd /etc/init.d
```

```
cp lp test
```

- 2. 使用 vi 编辑器编辑名为 test 的文件。将第 16 行内容替换

```
[ -f /usr/lib/lpsched ] && /usr/lib/lpsched
```
为以下内容

```
echo ""; /usr/bin/banner "Ready"; echo ""
```
现在将第 20 行当前内容替换

```
[ -f /usr/lib/lpshut ] && /usr/lib/lpshut
```
为以下行：

```
echo ""; /usr/bin/banner "System going down"; echo ""
```

- 3. 验证 test 脚本是否能正确使用 start 和 stop 参数运行。

```
./test start
./test stop
```

- 4. 切换到 /etc/rc2.d 目录，并为你刚创建的 test 脚本创建一个硬链接。

```
cd /etc/rc2.d
ln /etc/init.d/test S22test
```

- 5. 切换到 /etc/rcS.d 目录，并创建另一个链接到 test 脚本，该脚本将在系统进入运行级别 S 时运行。

```
cd /etc/rcS.d
ln /etc/init.d/test K99test
```

- 6. 将系统关闭到单用户模式，并观察控制台输出。K99test 脚本的关闭消息是否出现？

```
init S
```

- 7. 现在停止系统。

```
/usr/sbin/shutdown -y -g0 -i0
```

- 8. 在 ok 提示符下，再次引导系统，并观察控制台上的系统消息。S22test 脚本的启动消息是否出现？

```
boot
```

## 复习问题

1. 选择最能描述引导过程的事件顺序。
A. Boot PROM 阶段、引导程序阶段、内核初始化阶段、init 阶段
B. 引导程序阶段、Boot PROM 阶段、内核初始化阶段、init 阶段
C. 引导程序阶段、Boot PROM 阶段、init 阶段、内核初始化阶段
D. Boot PROM 阶段、引导程序阶段、init 阶段、内核初始化阶段

2. 由一个小型静态核心和许多动态可加载模块组成的是什么？
A. kernel
B. ufsboot
C. shell
D. bootblock

3. 默认情况下，Solaris 8 有多少个可用的系统运行状态？
A. 3
B. 7
C. 6
D. 8

4. 在此运行状态下，所有文件系统仍然可用，任何已登录用户都可以保持登录状态。除了最基本的操作系统服务外，所有服务都已有序关闭。
- A. S
- B. 1
- C. 2
- D. 0

5. 内核启动的第一个任务是什么？
- A. sched
- B. init
- C. ufsboot
- D. 加载可加载模块

6. 如何在稍后查看引导时显示的系统消息？
- A. 通过发出 dmesg 命令
- B. 通过查看 /var/messages 文件
- C. 通过发出 sysdef 命令
- D. 通过查看 /etc/boot.log 文件

7. 要将系统引导到单用户状态，在 ok 提示符下输入什么命令？
- A. boot
- B. boot -s
- C. boot -a
- D. boot -n

8. 在 ok 提示符下输入的哪个命令会在引导过程中停止并请求输入？
- A. boot -i
- B. boot -a
- C. boot -v
- D. boot -s

9. 以下哪个程序检查 /etc/inittab 文件的内容以确定启动其他进程的顺序以及当其中一个进程结束时该做什么？
- A. init
- B. boot
- C. kernel
- D. swapper

10. 在挂起的系统上，如果系统无响应，正确的操作顺序是什么？
- A. Stop+A, sync, reset
- B. Stop+A, boot
- C. Stop+A, reset
- D. Stop+A, reset, sync, boot

11. 以下哪个命令等同于 init 5 命令？
- A. poweroff
- B. halt
- C. reboot
- D. boot -s
