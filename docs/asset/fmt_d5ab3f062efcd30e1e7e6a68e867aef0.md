
## 安装用户权限

如基础 Kismet 安装章节所述，除非您以 Set User ID (`SUID`) `root` 方式构建 Kismet，否则您需要系统中有一个普通的非特权用户。这是出于安全原因。在此指定的用户必须对您存储捕获数据和日志的目录具有写权限。人们经常遇到的一个主要问题是他们以 `root` 运行 Kismet 并指定 `root` 为 `SETUID` 用户。除非您以 `SETUID root` 方式构建，否则这将导致 Kismet 无法启动。他们还犯的一个错误是以 `root` 登录，从 `/root` 运行 Kismet，由于 `SETUID` 用户没有 `/root` 目录的写权限，服务器无法启动。简单的解决方案是以普通用户登录，然后使用 `su` 切换到 `root` 或使用 `sudo` 启动 Kismet。

指定系统中一个非特权（非 `root`）用户的用户名，并确保您存储数据的任何地方都有写权限。逻辑上的位置是非特权用户的家目录。避免问题的最佳 Kismet 运行顺序是以普通用户登录，切换到您希望保存结果数据的目录，然后 `su` 切换到 `root`，再运行 Kismet。

## NetworkManager 睡眠配置

```
# Do we try to put networkmanager to sleep? If you use NM, this is probably # what you want to do, so that it will leave the interfaces alone while # Kismet is using them. This requires DBus support! networkmanagersleep=true
```

配置文件中的这一行告诉 Kismet 使用 `Dbus` 来禁用 Network Manager（常见的 gnome 桌面管理小部件），使其在 Kismet 会话期间自我禁用。Kismet 退出后，网络管理器将恢复控制。

### 注意

> 许多现代 Linux 发行版使用精美的 X 小部件来控制网卡。这是为了让系统更用户友好，避免用户必须去命令行连接无线网络的一种尝试。问题是，如果我们想对网卡做一些“奇怪”的操作，例如监听模式，这些网络监控程序会争夺网卡的控制权，从而给 Kismet 带来无尽的麻烦。
>
> 如果您遇到任何奇怪的扫描情况，例如随机停止扫描或卡在某个信道上不跳转，这很可能是一个罪魁祸首。在大多数情况下，您希望启用此选项。
>
> 在某些情况下，这可能会导致问题。最常见的情况是，当您使用一个接口进行扫描，但使用网络管理器控制另一个接口用于通信（例如，向服务器报告的入侵检测系统 (IDS) 设置）时。Kismet 会禁用所有接口（有线和无线）的网络管理器。如果您遇到网络管理器被禁用导致的问题，您可能希望完全不用网络管理器，并手动配置其他接口。

## 源配置

```
# Sources are defined as:
# source=sourcetype,interface,name[,initialchannel]
# Source types and required drivers are listed in the README under the
# CAPTURE SOURCES section.
# The initial channel is optional, if hopping is not enabled it can be used
# to set the channel the interface listens on.
# YOU MUST CHANGE THIS TO BE THE SOURCE YOU WANT TO USE
```

这可能是配置文件最重要的部分之一：我们从哪里获取数据。`source` 行告诉 Kismet 它需要知道什么才能将数据输入程序，以便我们可以开始扫描。每个源都有三个参数：特定类型卡片的 Kismet 源名称、接口名称，以及在 Kismet 客户端中找到的逻辑名称。Kismet 的 `README` 列出了兼容的源及其正确的接口名称。

| 驱动程序 | 描述 | 链接 / 接口 |
| :--- | :--- | :--- |
| `hostap` | Prism/2 Linux HostAP 0.4 | http://hostap.epitest.fi/ |
| | 捕获接口 | `wlanX` |
| | HostAP 驱动程序驱动作为接入点的 Prism/2 芯片组 | |

模式，但也可以驱动处于客户端模式和监听模式下的无线网卡。`HostAP` 驱动程序似乎频繁地改变其进入监听模式的方式，因此这个源码应该能够让这些网卡正常工作。

`README` 文件中有许多条目，例如针对兼容热点网卡的这一项。你需要找到对应你网卡类型的条目，并按照任何特殊说明进行操作才能使其正常工作（使用不同的驱动程序或补丁等）。

对于上述网卡，源配置行应为 `source=hostap,wlanx,hostap`，其中 `hostap` 是网卡类型名称（根据 `readme` 文件），`wlanx` 是该网卡的接口名称（通常会是 `wlan0` 或 `wlan1`）。最后一部分是一个逻辑名称，供你参考。客户端会显示每张网卡的当前状态以及其当前所在的信道。提供一个简短的描述性名称很有用，这样你就能知道哪个是哪个。识别板载网卡与附加网卡尤其有用，这样你就知道哪一个是活动的，以及它处于哪个信道上。

你也可以通过在逗号后添加第四个参数来指定 Kismet 启动时网卡开始的初始信道。如果你希望网卡从第 11 信道开始，只需在逻辑名称后添加 `,11` 即可。此时源配置行将变为 `source=hostap,wlanx,onboard,11`。如果你拥有多张网卡并希望监控不同的信道，这特别有用；你可以让 Kismet 设置信道，而无需手动操作。如果启用了信道跳转，此设置的影响不大，且仅适用于静态信道监控。

无人机（Drones）也在 `source=` 行中指定。无人机与其他源类似，除了我们指定无人机设备的远程地址而不是本地接口。如果在一台位于 `192.168.0.45` 的计算机上运行了无人机，`source=` 行看起来像这样：

```
source=kismet_drone,192.168.0.45:3501,Drone
```

就像本地接口一样，我们指定设备类型，在此情况下为 `kismet_drone`，设备地址和无人机运行的端口（默认是 `3501`），以及显示在客户端中的设备的逻辑名称。

无人机必须在启动 Kismet 服务器之前运行，否则服务器将启动失败。如果无人机因任何原因断开连接，你需要重新启动 Kismet 服务器才能重新连接到该无人机。`Kismet-Newcore` 的开发正在解决这一限制。

## 源特殊选项

```
# 每个源的特殊选项
# sourceopts=srcname:options
# srcname * 表示 “所有源”。个别源选项可以通过 “no” 关闭，例如 “noweakvalidate”。某些源可能有特殊选项。
# sourceopts=demo:fuzzcrypt,weakvalidate
# sourceopts=demo2:nofuzzcrypt
```

源可以具有关于要收集什么类型数据的特殊参数。如果我们拥有多个源，你可以指定某些源收集所有数据，而其他源忽略一些数据。在大多数情况下，修改这些设置并非必需，因为每个驱动程序都是独特的，且无法得知有哪些可用选项可供更改。

## 启用源

```
# 逗号分隔的要启用的源列表。仅当定义了多个源且只想启用其中几个时才需要此设置。默认情况下，所有已定义的源都是启用的。
# 例如：
# enableSources=primsour, ciscoSource
```

对于多源安装，或当你使用不同网卡进行不同类型检测的情况时，这是一个非常有用的参数。在上面的 `source=` 行中定义所有潜在的源（不同的网卡，或网卡的配置），根据你为每个源指定的逻辑名称，你可以在此处切换它们，通过编辑 `enableSource=` 行或设置多行具有不同网卡组合的行，并在不需要的行开头用 `#` 进行注释。请记住，一次只能取消注释一行 `enableSources=`。

例如，如果你有一个用于 wardriving（无线网络探测）且配备两张网卡的配置，你可以有一行写着 `enableSources=enginius1,enginius2`，另一行用于方向查找则为 `enableSources=proxim.` 在处理大量无人机时，这特别有用。通过设置多行并简单地注释和取消注释不同的行，你可以快速轻松地启用和禁用组。

## VAP 销毁

```
# 在多 VAP 接口（如 madwifi-ng）上自动销毁 VAP。
# 当存在非 rfmon VAP 时，Madwifi-ng 在 rfmon 模式下无法正常工作，但是
# 这对系统来说是一个相当侵入性的更改，因此可以被禁用。如果你禁用了它，
# 在大多数情况下，请预期事情不会正常工作。
vapdestroy=true
```
