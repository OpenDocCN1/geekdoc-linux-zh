
```
16:11:41 up 10:27, 2 users, load average: 1.60, 0.51, 0.18

Tasks: 107 total, 2 running, 103 sleeping, 0 stopped, 2 zombie

Cpu(s): 16.6us, 6.5by, 0.0ni, 0.76wa, 0.0hi, 0.0si, 0.0%

Mem: 252424k total, 249224 used, 3200 free, 23606 buffers

Swap: 102088k total, 102088k free, 8628k cached
```

| PID | USER | PR | NI | VIRT | RES | SHR | %CPU | TIME | COMMAND |
|---|---|---|---|---|---|---|---|---|---|
| 4242 | chris | 15 | 18 | 37m | 25m | 19.9 | 0.0 | 01:35 | chrome.browser |
| 4217 | chris | 15 | 0 | 137m | 31m | 17s | 0.0 | 01:27 | firefox-browser |
| 4244 | chris | 15 | 0 | 39148 | 18m | 7664 | 0.0 | 04:94 | beagle-helper |
| 4138 | chris | 15 | 0 | 101m | 14m | 9.8m | 0.0 | 00:66 | baboxab || |

## 监控笔记本电脑的功耗

为了有效使用笔记本电脑，你需要能够监控和管理笔记本的功耗。使用 Fedora 或 RHEL 提供的工具，你可以配置笔记本以：

- 监控电池电量。
- 在低电量时通知。
- 在电池充满电时通知。
- 当笔记本插电时。
- 挂起会话。

### 高级电源管理 `APM`

使用 Fedora 或 RHEL 提供的工具，你可以配置笔记本监控：

### 高级配置和电源接口 `ACPI`

Fedora 和 RHEL 提供了两种方式：`APM` 和 `ACPI`。为了有效使用笔记本电脑，通过使用 Fedora 或 RHEL 提供的工具，你可以配置笔记本以：

- 监控电池电量。
- 在低电量时通知。
- 在电池充满电时通知。
- 当笔记本插电时。
- 挂起会话。

### 使用电源管理器

1. 右键点击电池图标并选择“首选项（Preferences）”。弹出电源管理窗口。

2. 修改与电池相关的任何值：

- `On AC Power`：在 AC 电源选项卡中，你可以选择在将电脑放入睡眠之前空闲的分钟数。你还可以设置笔记本关闭时发生的情况（黑屏、挂起或无）。对于显示器，你可以设置在关闭显示前等待多久（默认为 40 分钟）或是否在空闲时关闭。
- `On Battery Power`：接通电源时的选项也适用于电池供电。你可以设置在空闲一段时间后 CPU 和显示器发生的情况。
- `General`：在通用选项卡中，你可以设置按下笔记本电源按钮或挂起按钮时发生的通知类型。你还可以设置何时显示电池图标（当电池存在、电池电量低或正在充电/放电时）。

# 第 10 章：理解系统管理 451

## 使用 `acpi_listen` 监控 ACPI 事件

如果你的系统正在运行 `ACPI`，你可以使用 `acpi_listen` 命令监控 `ACPI` 事件。作为 root 用户，在终端窗口中输入以下命令：

```
# acpi_listen
_adapter AC 00000080 00000000

processor CPU 00000080 00000000

processor CPU 00000081 00000000

battery BATO 00000080 00000001

_adapter AC 00000080 00000001

processor CPU 00000080 00000000

processor CPU 00000081 00000000

battery BATO 00000080 00000001

button/lid LID 00000080 00000001

button/lid LID 000000080 00000002
```

上述消息在 AC 电源断开、电源重新连接、笔记本盖子关闭后再次打开时出现。

## 使用 FirstAidKit 修复你的系统

从 Fedora 10 开始，一个名为 `FirstAidKit` 的新软件包帮助你修复可能出现在系统中的任何问题。`FirstAidKit` 基于可插架构构建，是一个自动化恢复工具，它应用常用技术来尝试救援你的系统。

要使用 `FirstAidKit`，你首先需要安装该包：

```
# yum install firstaidkit
```

运行该程序最常见的方法是让它执行它认为应该执行的操作——这是恢复工具的整个自动化部分。为此，请运行以下命令：

```
# firstaidkit -a
```

该程序会报告它发现的内容以及所采取的行动。

要查看可用插件列表，请使用以下命令：

```
# firstaidkit --list
```

访问 `https://fedorahosted.org/firstaidkit/` 了解更多关于 `FirstAidKit` 的信息。

## 选择软件替代方案

由于 Linux 中的每种主要服务（如邮件、打印、Java 环境等）都有多个软件包可用，在使用系统时人们可能会倾向于使用某一个服务而非另一个。设计用于配合替代系统（alternatives）工作的软件包可以在 Fedora 或 RHEL 中进行配置，让管理员选择想要默认使用的特定服务的哪种替代方案。

## 选择 Java 替代方案

如果你正在开发 Java 应用程序，`alternatives` 功能的附加功能允许你在使用专有的 Java 虚拟机 `JVM` 和使用 GNU Java 编译器 `gsj` 之间切换。输入以下内容查看系统当前正在使用哪种 Java 实现：

```
# alternatives --display java
```
