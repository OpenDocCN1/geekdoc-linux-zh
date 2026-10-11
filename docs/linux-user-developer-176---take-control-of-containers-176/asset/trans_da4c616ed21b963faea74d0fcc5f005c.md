
退出。若要使用现有目录作为沙箱的主目录，并在主目录上创建持久沙箱，请执行以下命令：

```bash
$ firejail /etc/init.d/apache2 start
```

要在 Firejail 中启动服务器，需要 root 权限。要启动 Apache 服务器，请执行以下命令：

```bash
$ firejail /etc/init.d/apache2 start
```

请注意，如果不带任何参数运行 Firejail，它将启动常规的 /bin/bash shell。只有 Bash 会话及其子进程在沙箱内可见。

## 03 使用 Firejail（续）

要查看正在运行的沙箱列表，请使用以下命令：

```bash
$ firejail --list
```

你将看到格式为 PID:用户名:命令 的列表。要查看每个沙箱内的进程树，请输入：

```bash
$ firejail --tree
```

如果你想要加入一个已经运行的沙箱，请使用 `--list` 选项获取该沙箱的 PID。然后将此 PID 传入以下命令：

> 如果不带任何参数运行 Firejail，它将启动常规的 /bin/bash shell。只有 Bash 会话及其子进程在沙箱内可见 [19]

```bash
$ firejail --join=3974
```

如果你正在 Firejail 中启动 Firefox 并希望使用浏览器特定的 iptables 过滤器，请执行：

```bash
$ firejail --net=eth0 firefox
```

这将为 Firefox 会话创建一个新的 TCP/IP 栈，分配一个 IP 地址，并安装浏览器特定的 iptables 过滤器。如果在 Firejail 中启动的程序不需要网络访问，请执行：

```bash
$ firejail --net=none vlc
```

控制流入和流出沙箱的数据量：

```bash
$ firejail --name=browser --net=eth0 firefox &
$ firejail --bandwidth=browser set eth0 70 30
```

此示例将接收侧带宽设置为每秒 70 千字节，将发送侧带宽设置为每秒 30 千字节。你可以使用以下命令在运行时更改这些设置或清除它们：

```bash
$ firejail --bandwidth=browser clear eth0
```

## 04 Firetools

Firetools 是 Firejail 的 GUI（图形用户界面）。它作为单独的包分发，并使用 Qt4/Qt5 库构建。它带有系统托盘的沙箱启动器选项，以及沙箱编辑、管理和统计功能。它不在标准软件仓库中，但有官方的 DEB 包可用。下载相关的 Firetools DEB 文件，然后导航到文件下载的文件夹并执行：

```bash
$ sudo dpkg -i firetools*.deb
```

这将安装 Firetools。但是，如果遇到依赖性问题，请使用以下命令解决：

```bash
$ sudo apt-get install -f
```

使用以下命令启动它：

```bash
$ firetools &
```

### 沙箱应用程序的网络设置

沙箱应用程序的网络连接可以是直接的，也可以是路由的。在直接设置中，沙箱使用内核 MAC VLAN 设备连接到网络；在路由设置中，它使用网桥设备。直接设置如下所示：

```bash
$ firejail --net=eth0 firefox
```

在路由设置中，首先设置网桥，然后在上述命令中通过 `--net` 参数传入网桥名称。

## 教程

![](img/6866071e033820549b214c239744aaa0_43_0.png)

你可以看到 Firetools 窗口以及系统托盘中用于运行该应用的指示器。要启动任何应用，请双击它，或者右键单击并选择“运行”。要监控正在运行的应用，请在 GUI 的任意位置右键单击并选择“工具”；所有正在运行的应用将列在其中。要在 Firetools 中添加新应用，请右键单击 GUI 并点击“编辑”。填写相关详细信息，并将“命令”部分的值设为 Firejail 应用名称。

## 05 Firejail 特性

Firejail 背后的核心技术是 Linux 命名空间。这种轻量级可视化技术被用作隔离应用程序的第一步。

应用容器在沙箱启动时自动构建，并在沙箱关闭时销毁。该容器基于当前安装的文件系统。Firejail 可以为沙箱附加一个新的 TCP/IP 网络栈，该栈拥有自己的路由表、防火墙和接口集。此栈独立于主机网络栈。Firejail 支持的网络操作包括：创建新接口、移动现有接口、分配地址、主机名支持、DNS 支持、Linux netfilter 支持以及流量整形。安全配置文件位于 `/etc/firejail` 目录中，它描述了文件系统容器、安全过滤器和网络配置。Firejail 中的 Appimage 执行原生格式打包。添加 `--appimage` 以挂载包并在沙箱内运行。Firejail 提供沙箱审计和监控。它可以指出安全配置文件中的漏洞。它可以提供选项来跟踪沙箱化应用程序的所有方面。可以使用 Firetools 来监控 CPU/内存/带宽使用情况、跟踪系统调用、监控 exec 和 fork 事件。

![](img/6866071e033820549b214c239744aaa0_43_1.png)

## 06 构建自定义配置文件

所有自定义配置文件都存储在 `~/.config/firejail` 目录中。使用配置文件将 Firejail 命令行配置选项传递给程序。要为任何应用构建自定义配置文件，首先在你的主目录中创建 `.config/firejail` 目录：

```bash
$ cd ~
$ mkdir -p .config/firejail
$ cd .config/firejail
```

使用以下命令将 Firejail 使用的默认安全配置文件复制到该目录中：

```bash
$ cp /etc/firejail/app_name.profile app_name.profile
```

在这里，`app_name` 是你正在创建自定义配置文件的应用的名称。现在编辑新配置文件。你可以注释掉行、将目录加入黑名单、将文件加入白名单等。修改完成后，保存并关闭文件，然后使用以下命令启动你的应用程序：

```bash
$ firejail app_name
```

由于在 `~/.config/firejail` 目录中存在一个与应用程序同名的配置文件，因此它会加载该文件。你也可以在 `/etc/firejail` 目录中创建配置文件。如果两个目录中都存在带有应用名称的配置文件，`~/.config/firejail` 的优先级高于 `/etc/firejail`。也可以在其他位置创建配置文件，并在启动应用程序时指定该位置。

## 07 构建白名单配置文件

白名单配置文件是限制更严格的配置文件，使用 Firejail 的白名单功能构建。我们在上一节中创建的自定义配置文件也称为黑名单配置文件，在那里你将应用程序不允许使用的文件列入黑名单。在此处，列出应用程序运行所需的文件，而其他所有内容均不可访问。要创建白名单配置文件，首先使用 `--private` 创建一个简单的 Bash 沙箱：

```bash
$ firejail --private
```

现在在此 Bash 会话中启动应用，并使用以下命令列出其中所有文件：

```bash
$ find .
```

定位需要加入白名单的目录/文件，然后退出并关闭沙箱。然后，像之前一样，在 `~/.config/firejail` 目录中创建名为 `app_name.profile` 的新配置文件。输入以下内容作为文件内容：

```
$ app_name profile
mkdir ~/, directory_name
whitelist ~/directory_name
include /etc/firejail/whitelist-common.inc
include /etc/firejail/default.profile
```

在这里，我们将 `directory_name` 加入白名单，它位于 `app_name` 目录结构内。会话配置从 `whitelist-common.inc` 中包含。

## 08 Firefox 沙箱化

通过执行以下命令启动 Firefox 进程：

```bash
$ firejail firefox
```

Firefox 的单个实例可以有多个浏览器窗口。因此，如果 Firefox 已经在运行，并且你想在 Firejail 中启动一个新会话，请执行：

```bash
$ firejail firefox --no-remote
```

沙箱仅允许 Firefox 访问少量文件和目录。如果 Firefox 试图访问被列入黑名单的文件，日志消息将发送到 syslog。默认启用的安全过滤器减少了内核的攻击面。seccomp 过滤器通常默认使用。如果你不信任浏览器中安装的扩展和插件，请使用 **--private** 选项并在沙箱级别配置 DNS。这可以防止来自重新配置 DNS 的攻击。

```bash
$ firejail --private --dns=8.8.8.8 --dns=8.8.4.4 firefox --no-remote
```

要创建新的 TCP/IP 栈，连接到你的以太网网络并指定明确的 IP 地址：

```bash
$ firejail --net=eth0 --ip=192.168.1.207 firefox
```

Firejail 用 Xpra 或 Xephyr 服务器替换常规 X11 服务器，防止 X11 键盘记录器和截图实用程序访问主 X11 服务器。

```bash
$ firejail --x11 --net=eth0 firefox
```

## 09 Seccomp 过滤器

Firejail 默认使用 Seccomp-bpf。它代表*安全计算模式*，以 Berkeley 数据包过滤器 (BPF) 格式表示。使用 Firejail 沙箱构建白名单 seccomp 过滤器并将其附加到用户程序。Firejail 需要 seccomp 过滤器的系统调用详细信息。我们使用 strace 来获取系统调用。让我们以 VLC 媒体播放器为例：

```bash
$ strace -qc vlc
```

这会打开 VLC；一旦你关闭它，strace 就会打印系统调用列表。将所有系统调用的列表复制到文本编辑器中，并将它们转换为无空格的逗号分隔形式。现在将此逗号分隔的系统调用字符串用于 **--seccomp**。保留以下值：

```bash
$ firejail --shell=none --seccomp=keep=poll,futex,[...] vlc
```

该命令看起来很长，但请确保包含所有系统调用。如果出现错误，添加遗漏的系统调用。现在在 **/etc/firejail** 中创建一个白名单配置文件。将默认的 VLC 配置文件复制到这里，并添加以下两行：

```
shell none
seccomp keep poll,futex,rt_sigreturn,stat,read,[...]
```

请注意，点号表示其余的逗号分隔的系统调用名称。

## 10 AppImage 支持

AppImage 是由 Simon Peter 开发的通用软件打包格式。
使用以下命令在 Firejail 中启动你的 AppImage 应用程序：

```bash
$ firejail --appimage=Firefox-50.1.0.g1ibc2.3.3-x86_64.AppImage
```

所有沙箱选项都可用，例如 **--private** 或 **--x11**。假设你已从 AppImage 项目仓库下载了 Firefox；要启动沙箱，请使用：

```bash
$ firejail --appimage --private --net=eth0 --x11 ~/Downloads/Firefox-50.1.0.g1ibc2.3.3-x86_64.AppImage
```

**--appimage** 用于进入 AppImage 模式，**--private** 创建空主目录，**--net=eth0** 创建新的网络命名空间，**--x11** 用于基于 Xpra 的沙箱化。
要验证安全参数，打开 Firetools 并点击 Firefox 沙箱以获取统计信息。查看 seccomp 统计信息已启用，以及 capability 字段为零？对于沙箱而言，这两个参数最为重要，其他一切均构建在此之上。如果有多个沙箱在运行，请按如下方式限制每个沙箱的带宽：

```bash
$ firejail --bandwidth=32119 set eth0 80 20
```

> Firejail 可以为沙箱附加一个新的 TCP/IP 网络栈，该栈拥有自己的路由表、防火墙和接口集。此栈独立于主机网络栈 [19]

## Firejail 对 X11 的沙箱化

Xpra 和 Xephyr 受 Firejail X11 沙箱化支持。常规 X11 由这些 X11 软件包替换：

```bash
$ firejail --x11=xpra --net=eth0 program-and-arguments

$ firejail --x11=xephyr --net=eth0 program-and-arguments
```

另一个选项是使用：

```bash
$ firejail --x11 --net=eth0 program-and-arguments
```

这样，Firejail 首先尝试使用 Xpra，如果未安装，则尝试查找 Xephyr。请注意，是以 root 用户身份启动 Xpra。不支持 X11 沙箱化功能。

