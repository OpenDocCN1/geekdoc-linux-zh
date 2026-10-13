
你可以通过直接运行 `xinit` 来决定在没有窗口管理器的情况下运行 X Window；然而，大多数人会发现窗口管理器是在 X Window 下工作的必备工具。流行的 X Window 管理器包括 `fvwm2`、`fvwm`、`afterstep`、`twm`、`wmaker` 和 `wmx` 等。每个窗口管理器都有自己的外观和感觉，因此对不同用户提供不同的吸引力。我建议你通过安装必要的 RPM 文件来安装流行的窗口管理器并试用它们。

由于窗口管理器数量众多，充分利用它们需要了解每个包，而这反过来又需要你花费大量时间。几乎似乎你需要一个窗口管理器的管理器。

## 自定义客户端应用程序的外观和感觉

当你运行 `xterm` 或计算器（`xcalc`）等 X 客户端应用程序时，应用程序的默认外观和感觉通常来自 `/usr/X11R6/lib/X11/app-defaults` 中的一个文件。例如，`xcalc` 计算器的默认外观和感觉来自 `/usr/X11R6/lib/X11/app-defaults/XCalc` 文件。你可以修改这些默认值，为你和/或你的用户提供自定义的外观和感觉。请务必备份你要修改的每个文件。

如果你只对为自己更改几个应用程序的外观和感觉感兴趣，你可以在主目录中创建一个 `.Xresources` 文件，并使用以下语法添加行：

```
application_and_resource_key: resource_value
```

例如，在下面的示例中，我通过将此行放在我的 `.Xresources` 文件中更改了 `xcalc` 程序数字显示的默认背景颜色（黑色）：

```
XCalc*bevel.Background: red
```

为了确定哪个资源负责更改此特定颜色，我首先查看了 `/usr/X11R6/lib/X11/app-defaults/XCalc` 文件。在我找到资源（`bevel.Background`）后，我在 `.Xresources` 文件中创建了上述行，该行以应用程序名称（`XCalc`）作为资源名称的前缀。如果你使用主目录中的 `.xinitrc` 文件，你应该在加载任何客户端应用程序之前在其中放入 `xrdb -merge $HOME/.Xresources`。任何时候你在 `.Xresources` 文件中添加或修改资源，你都可以从命令行运行此命令以将资源更改集成到当前的 X 环境中。

## 使用 xdm，X 显示管理器

如果你已安装 Red Hat Linux 并选择了适当的复选框以启用图形登录，你无需手动设置 `xdm`。在这种情况下你可以跳过本节。如果你想提供基于 GUI 的用户身份验证界面，X Display Manager，即 `xdm`，就是你的答案。使用 `xdm`，你可以通过图形登录屏幕对用户进行身份验证，并直接将他们带到其 X Window 环境。该程序的目的是提供类似于 `getty` 和 `login` 的服务。你可以按如下方式启动显示管理器：

```
xdm &
```

`xdm` 配置文件位于 `/usr/X11R6/lib/X11/xdm` 目录中。文件 `xdm-config` 用于配置登录屏幕对用户显示的方式，而 `Xsetup_0` 用于告诉 `xdm` X 启动时应启动哪些程序。默认的 `Xsetup_0` 如下所示：

```
#!/bin/sh
# Xsetup for Red Hat Linux
# Copyright (c) 1999, 2000 Red Hat, Inc.

pidof -s kdm > /dev/null 2>&1
if [ $? -eq 0 -a -x /usr/bin/kdmdesktop ]; then
    /usr/bin/kdmdesktop
else
    /usr/X11R6/bin/xsetroot -solid "#356390"
fi

# only set the background if the xsri program is installed
if [ -x /usr/bin/xsri ]; then
    /usr/bin/xsri -geometry +5+5 -avoid 300x250 -keep-aspect \
        /usr/share/pixmaps/redhat/redhat-transparent.png
fi
```

当用户经过身份验证时，此文件启动 `xconsole` 和 `xbanner` 程序。对于大多数用户来说，这些几乎毫无用处。因此你应该将其修改为适当的内容。例如，你可能会使用 `xv` 程序将 X 环境的背景设置为适合你组织的背景。或者你也许可以启动一些大多数用户通常运行的应用程序，例如 `xmailbox`。

The `xdm` can be run automatically after boot by changing the default run level to 5. To change the run level of your system to 5, modify the following line in the `/etc/inittab` file:

```
id:3:initdefault:
```

To change the default run level, simply replace the 3 with 5. And make sure that you have the following lines in the same file:

```
# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
```

## 第 6 章

### 设置网络

#### 本章内容

- 手动配置网络接口卡（NIC）
- 使用 `netcfg` 配置 NIC
- 了解默认网关
- 将网络划分为子网

很可能，如果你想使用 Red Hat Linux 系统连接到任何网络，你需要网络功能。你的网络可能很简单，例如将一台系统连接到 Internet，或者你的网络可能非常庞大，覆盖多个位置和数百名用户。在本章中，我将向你展示如何让 Linux 在网络上运行。

## 配置网络接口

大多数管理员可能需要将 Linux 计算机连接到以太网。这样的以太网可以是你自己的局域网（LAN），也可以是 ISP 处的局域网（例如，共置服务器）。在本节中，我假设你已经安装了一张与 Red Hat Linux 兼容的以太网适配器卡（即网络接口卡，或 NIC）。要了解哪些 NIC 与你的 Red Hat Linux 版本兼容，请参阅 Red Hat 网站的硬件兼容性部分。总体而言，大多数流行的 NIC 卡都能很好地与 Red Hat Linux 配合使用。

![](img/9eb7e89292d2f85707b4d49102c865b7_143_0.png)

你可能在 Red Hat Linux 安装阶段已经配置了网络，但我仍然建议你阅读本节，因为你以后可能需要更改网络配置。

你可以通过多种方式配置网络。首先我将讨论命令行方法，因为它是功能最强大的（在不需要依赖除你喜欢的文本编辑器之外的任何特殊工具的意义上），然后我将讨论网络配置器（或简称为 `netcfg`），这是一个 GUI 工具，可用于更轻松地创建网络接口。

![](img/9eb7e89292d2f85707b4d49102c865b7_143_1.png)

使用传统方法或 `netcfg` 方法设置网络接口时，你必须提供默认网关 IP 地址。在下一节中，我将讨论为什么需要默认网关。

### 手动配置网络接口卡

配置 NIC 的传统方法是手动从命令行界面进行操作。这是我进行各种配置的最喜欢的方法，因为它迫使我确切地知道配置某事物所需的条件。我的座右铭是：一旦你知道如何以“老式”方式做事，你就可以以任何方式做事。

### 配置新的网络接口

在做任何事情之前，运行 `dmesg` 程序（或查看 `/var/log/dmesg` 文件）以确定当前 Linux 内核是否识别你的网卡。如果没有，请阅读第 2 章中的模块配置部分。如果 Linux 内核确实识别了你的卡，你应该会在 `dmesg` 输出中看到一些与内核发现你的网络设备相关的行。例如，当我在具有通用（NE2000 兼容）以太网卡的 Red Hat Linux 系统上运行 `dmesg | grep -i eth` 命令时，我得到以下输出：

```
NE2000 ethercard probe at 0x340: 00 c0 f6 98 37 37
eth0: NE2000 found at 0x340, using IRQ 5.
```

此输出告诉我内核已找到我的 NE2000 兼容网卡，并为其使用中断请求线（IRQ）5，并且 I/O 地址空间从 `0x340` 开始。还请注意，此设备称为 `eth0`（即以太网设备 0）。
