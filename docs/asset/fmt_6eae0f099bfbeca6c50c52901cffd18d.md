
# 列表 6: show_gpio.ex

```elixir
01 #-
02 # Show_Show_gpio.ex - 在 Zenity 列表对话框中显示 Mnesia
03 #-
04 defmodule show_gpio do
05   def getdata() do
06     result = :mnesia.dirty_match_object({P13, _..}) | Enum.sort
07     create = a presentable string for output
08     output = Enum.map(result, fn x ->
09       "#{elem(x,1)}\#zenity list --title=P13_Table --column=Values #end"
10     end)
11     feedback
12     if ("feedback") then "Refresh" do
13       getdata()
14     end
15   end
16   # 启动 Mnesia
17   # :mnesia.start()
18   # 等待表格更新
19   # :timer.sleep(1000)
20   # 显示一个 Zenity 列表对话框。
21   # 刷新按钮继续，其他按钮退出
22   Show_gpio.getdata()
```

为了测试功能是否正常，请使用第一个项目 (`Zen2gpio.ex`) 切换 GPIO 引脚值；然后，可以刷新 `Show_gpio.ex` 来检查新值。

在最后运行时，你将看到一个 Elixir 并发性的示例。`P13` 节点填充了一个 Mnesia 表格，它正在处理 GPIO 值并写入 CPU 温度。

# 结语

通过 Elixir，我们拥有许多开箱即用的功能。接下来的步骤将是查看节点消息以及创建导入了 Elixir 库的项目。

# 信息

- [Elixir](https://elixir-lang.org/)
- [Elixir](https://www.elixir.org/)
- [Elixir] 安装指南：https://elixir-lang.org/install.html
- [GPIO] 使用方法：http://wiringpi.com/the-gpio-utility/
- [Zenity](https://help.gnome.org/users/zenity/2.32/)

# 逛商店

# shop.linuxnewmedia.com

# 错过了某一期？

你运气真不错。

大多数案例仍然可用。在它们售罄之前立即订购！

shop.linuxnewmedia.com

![](img/dda1c68e5613db309d70a0ab080ae51a_60_0.png)

# 制作空间 (MakerSpace)
适用于 Raspberry Pi 400 的 Amiga 模拟器
Mimic

![](img/dda1c68e5613db309d70a0ab080ae51a_61_0.png)

将 Raspberry Pi 400 转换为一台行为像流行的 Amiga 500 的复古电脑。作者：Hans-Georg Eiser

市用级 Amiga 不仅仅是一个游戏平台；它的图形界面 Workbench 远超时代。Amiga 型号 [1] 位列 20 世纪 80 年代和 90 年代的流行计算机之列。A500、A1200 以及其他型号 Amiga 将主板和软驱器集成在键盘中。根据维基百科 [1]，Amiga 500 是开创性型号，它促使 Retro Games Ltd. 发布了针对其他计算机的复制品，例如 C64（现代格式和全尺寸）和 VC20（仅全尺寸）。

为了获得良好的 Amiga 模拟，你不需要等待 Amiga 500。模拟器适用于所有平台（甚至是老旧的 MS-DOS），它们可以通过不同程度的努力将 Amiga 的体验带到其他硬件上。在树莓派的世界里，Pi 400 是 Amiga 模拟器的良好选择，因为原始的 Amiga 键盘将键盘、主板和存储设备整合在单个外壳中。

PiMiga [3] 的开发者构建了一个直接启动到 Amiga 模拟器 [4] 的 Raspberry Pi OS 发行版。配备了 PiMiga 的 400 在重启后需要 35 秒

![](img/dda1c68e5613db309d70a0ab080ae51a_61_1.png)

图 1：Amiga A500 Mini 将于 2022 年推出。Retro Games Ltd.

在 Amiga Benchmark 接口上以高分辨率（1920x1080）显示（图 2）。目前的（发布时）PiMiga v1.5 使用内核为 5.10.17 的 Raspberry Pi OS 10。

# 安装

PiMiga 是一个种子文件，你可以直接从供应商 (1) 获取，分为小型或大型变体。对于 PiMiga 1.5 Lite，下载 `pimiga15Lte.tar` 存档；对于直到 1993 年的 PiMiga 1.5MF，下载 `pimiga15MF.tar`，它有 42GB，涵盖 77GB 的 Amiga 5MF 镜像。下载存档、解压并将其挂载到足够大的 microSD 卡（32GB 或 128GB）可能需要一段时间。

要启动 Amiga，你需要一个引导 ROM。这些 ROM 的某些版本适用于各种 Amiga 计算机。对于 Amiga 1200，PiMiga 需要 Kickstart 3.1。开发者设置得非常方便用户检查。

# Kickstart ROM

对于良好的 Amiga 模拟，你不需要等待 Amiga 500。模拟器适用于所有平台（甚至是老旧的 MS-DOS），它们可以通过不同程度的努力将 Amiga 的体验带到其他硬件上。在树莓派的世界里，Pi 400 是 Amiga 模拟器的良好选择，因为原始的 Amiga 键盘将键盘、主板和存储设备整合在单个外壳中。

# 关于

- 路径
- 快速上手
- 配置
- CPU 和 FPU
- 内存 (RAM)
- 软驱器
- 硬盘/HDD
- USB 卡
- 显示器
- 音频
- 自定义控制
- 其他
- 优先级
- 新状态

| B 部分：鼠标 | 默认 |
| :--- | :--- |
| 第 1 部分：IHC664 摇杆 | IHC664 摇杆 |
| 任何时候都不自动连发 | 摇杆 |
| 交换部件 | 鼠标/摇杆自动切换 |
| 第 2 部分：（无） | |
| 第 3 部分：（无） | 在右下角 |
| 鼠标摇杆: 8 | 数字鼠标速度: 180 |
| 鼠标摇杆: 1 | 模拟鼠标速度: 180 |
| 自动连发：快速 | 鼠标速度: 180 |
| 虚拟鼠标驱动程序 | 鼠标解捕 (untrap) |
| 出生：原生 | 仅限主机 |

**图 6：** 配置您的摇杆或游戏控制器，以避免使用键盘控制。

F+2) 点击左侧的 Input（输入），然后在下拉菜单的 Drop 1 中选择设备。直接将下拉菜单从 Default（默认）更改为 Joystick（摇杆）或 Gamepad（游戏控制器）（图 6）。切换到左侧的 Settings 并点击 Save 保存您的更改。返回桌面后，您的摇杆在所有游戏中都能工作。

# 复杂系统

AmigaWork 不仅仅是一个出色的游戏启动器。可以使用各种应用程序和工具。AmigaAMP 是一款 MP 播放器，其工作方式类似于 Amiga Linux 上的经典 WinAMP。

PiMiga 使用的版本比 Commodore 交付的官方 Workbench 更现代，它利用了当前系统的性能。如果你想查看其他 Amiga 的基准测试，可以使用模拟器（如 1）。

桌面上的文件夹可以通过双击打开。通过点击这些文件夹，用户使用的命名法与世界其他地方不同。桌面被称为 Amiga，所有磁盘都有分级文件系统，文件夹被称为抽屉 (drawers)，子文件夹被称为子抽屉 (sub drawers)。

![](img/dda1c68e5613db309d70a0ab080ae51a_64_0.png)

如果树莓派连接到网络，Amiga 程序就可以访问互联网。这是否可行取决于你使用的服务。例如，安装在 PiMiga 上的版本中的标准 AWE8 浏览器不支持 SSL，无法与不提供加密版本的网站一起工作。

尽管如此，它对某些任务仍然很有用。例如，你可以使用 Amiga [13]，它提供了一个全面的软件集合。作为测试，我下载了 Amiga 版本的 shell C 作为一个 LHA-

**图 7：** 你可以使用 AWeb 从 Aminet 下载额外的软件，然后解包并启动程序。

# MAKERPACE PiMiga 1.5

chive，在 Directory Opus 中解包，最后在终端程序 (7) 中启动了它。

# 登录和 SSH

树莓派不会启动 Linux 桌面。Workbench 界面是设置的固定部分，无法运行 Linux 应用程序。但是，如果你在树莓派上安装 VNC 服务器，就可以使其协同工作。

首先，你需要一个 Linux shell。如果你在另一台不在网络上的计算机上运行带有安全外壳 (SSH) 客户端的程序，登录树莓派的方法是：

```
ssh pi@pmiga
```

如果登录密码不起，你需要找到树莓派的 IP 地址。此最快的方法是按 F12 打开 Workbench 菜单并点击顶部的 Quit（退出）。当你进入那里时，你就以 pi 用户身份登录了。输入命令：

```
$ hostname -i
192.168.1.118 192.168.1.177
2001:b8a3:ffad0:edf0:297b:bfd0:bf02:67c5:9bd9:9206
```

用于 Raspberry Pi OS，我当时无法直接从源代码编译它。以 pi 用户身份运行，输出中的第一个地址显示该命令是分配给网卡的 IPv4 地址。后面可能还有另一个 IPv4 地址或 WLAN。

```
vnserver
vncpassword
```

让你设置一个 VNC 密码并启动服务器。如果你为了这种设置而退出 Amiga 模拟器，可以重启模拟器：

```
cd; ./amiberry
```
