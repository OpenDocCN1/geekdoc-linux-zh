
默认配置文件包含详细的注释。这些注释和 `cupsd.conf` 的帮助页已经足够详尽，因此我们不再在此详述相同的信息。

CUPS 仅在启动时读取其配置文件。如果你更改了 `cupsd.conf` 的内容，必须重启 cups 更改才能生效。如果你通过 cupsd 的 Web GUI 进行更改，它会自动重启。若要从命令行重启 cupsd，只需运行 `/etc/init.d/cups restart` 或 `/etc/init.d/cups restart`（取决于系统中存在哪一个）。

你也可以通过特定于桌面桌面的 GUI 工具来配置系统。例如，在 KDE 下，你可以通过 KDE 控制中心访问 KDE 打印管理器。然而，我们在测试中发现 KDE 打印管理器存在一些问题。例如，它会报错，说无法理解某些发行版默认 `cupsd.conf` 文件中的某些选项。浏览器 GUI 是安全的，且绝对具有权威性。

## 网络打印服务器设置

如果你在从网络打印时遇到困难，请进入基于浏览器的 CUPS GUI，确保你勾选了所有正确的选项框。可能的问题区域包括：未发布的打印机、未向网络广播打印机的 CUPS 服务器，或拒绝接受网络打印作业的 CUPS 服务器。

如果你直接编辑 `cupsd.conf` 文件，你需要进行几处更改。首先，将

``````
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
</Location>
```

更改为

``````
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From netaddress
</Location>
``````

将 `netaddress` 替换为你想要接受作业的网络 IP 地址（例如 `192.168.0.0`）。查找 `BrowseAddress` 关键字，并将其设置为该网络的广播地址加上 CUPS 端口；例如，

```
BrowseAddress 192.168.0.255:631
```

这些步骤告诉服务器接受来自指定子网上任何机器的请求，并向该网络上的每个 CUPS 守护进程广播关于它所服务的打印机信息。就这些！一旦你重启 cupsd，它就会以服务器的形式恢复。

## 第 26 章打印

### 打印机自动配置

你可以在没有打印机的情况下使用 CUPS（例如将文件转换为 PDF 或传真格式），但它的典型角色是管理真实的打印机。在本节中，我们将回顾处理打印机本身的方法。

在某些情况下，添加打印机是非常容易的。当 USB 打印机插入系统时，CUPS 会尝试自动检测并确定如何处理它们。

打印机制造商通常提供安装软件，为 Windows 甚至 Mac OS（后者也使用 CUPS）完成大部分设置工作。然而，很少厂商明确支持 Linux。

即使你必须进行配置工作，添加打印机的痛苦程度通常也不比插入硬件、连接到 `localhost:631/admin` 的 CUPS 接口并回答几个问题麻烦。KDE 和 GNOME 自带了打印机配置小部件，你可能更喜欢它们而不是 CUPS 界面。（我们更喜欢 CUPS GUI.）

如果其他人添加了打印机，并且网络上运行的一个或多个 CUPS 服务器知道了它，那么你的 CUPS 服务器就会发现它的存在。你不需要显式地将打印机添加到本地清单，也不需要将 PPD 文件复制到你的机器上。

## 网络打印机配置

网络打印机——即硬件接口为以太网的打印机——需要单独配置才能成为 TCP/IP 网络中的合格公民。特别是，它们需要知道自己的 IP 地址和子网掩码。这些信息通常通过两种方式之一传递。

现代打印机可以通过网络从 BOOTP 或 DHCP 服务器获取这些信息，这种方法在有很多打印机的环境中效果良好。有关 DHCP 的更多信息，请参阅第 469 页的 DHCP：动态主机配置协议。

或者，你可以从控制台为打印机分配静态 IP 地址，控制台通常由打印机前面板的一组按钮和一个单行显示组成。翻找菜单直到发现在哪里设置 IP 地址（如果有打印菜单的选项，请使用它并将打印机放在下面以备后参考）。

少数打印机允许通过串口访问虚拟控制台。这是一个好主意，但总工作量可能比忍受前面板界面要多。原理是相同的。

配置完成后，网络打印机通常有一个可以通过浏览器访问的 Web 控制台。然而，以此方式访问它们之前，打印机必须具有 IP 地址并且在网络上运行，因此在你可能需要它时，该接口是不可用的。

当你的打印机接入网络且你可以 ping 通它后，确保按照第 1081 页“安全你的打印机”节所述对其进行保护。

## 打印机配置示例

让我们从命令行添加并行打印机 `groucho` 和网络打印机 `fezmo`。

```
$ sudo lpadmin -p groucho -E -v parallel:/dev/lp0 -m pxicolor.ppd
$ sudo lpadmin -p fezmo -E -v socket:/192.168.0.12 -m laserjet.ppd
```

Groucho 连接到端口 `/dev/lp0`，fezmo 位于 IP 地址 `192.168.0.12`。我们以通用资源标识符 (URI) 的形式指定每个设备，并在 `/usr/share/cups/model` 中为它们选择合适的 PPD。

只要 cups 配置为网络服务器，它就会立即让网络上的其他客户端可以使用这些新打印机。不需要重启。

CUPS 接受各种用于打印机的 URI。以下是几个示例：

- ipp/zoe.canary.com/ipp
- lpd://riley.canary.com
- serial://dev/ttyS0?baudrate=9600+parity=even+bits=7
- socket/gillian.canary.com:9100
- usb:/XEROX/Phaser#206120?serial=YGG210547

某些类型接受选项（例如 serial），而其他则不。`lpinfo` 列出了你的系统可见的设备以及 CUPS 理解的 URI 类型。

## 打印机类设置

“类”（class）是一组共享一个队列的打印机。作业将在最先可用的打印机上执行。以下命令创建了类 `haemer` 并其中添加了三台打印机：riley、gilly 和 zoe。

```
$ sudo lpadmin -p riley -C haemer
$ sudo lpadmin -p gilly -C haemer
$ sudo lpadmin -p zoe -C haemer
```

只要 cups 配置为网络服务器，它就会立即让网络上的其他客户端可以使用这些新打印机。不需要重启。

CUPS 接受各种用于打印机的 URI。以下是几个示例：

- ipp/zoe.canary.com/ipp
- lpd://riley.canary.com
- serial://dev/ttyS0?baudrate=9600+parity=even+bits=7
- socket/gillian.canary.com:9100
- usb:/XEROX/Phaser#206120?serial=YGG210547

某些类型接受选项（例如 serial），而其他则不。`lpinfo` 列出了你的系统可见的设备以及 CUPS 理解的 URI 类型。

“类”是一组共享一个队列的打印机。作业将在最先可用的打印机上执行。以下命令创建了类 `haemer` 并其中添加了三台打印机：riley、gilly 和 zoe。

```
$ sudo lpadmin -p riley -C haemer
$ sudo lpadmin -p gilly -C haemer
$ sudo lpadmin -p zoe -C haemer
```

只要 cups 配置为网络服务器，它就会立即让网络上的其他客户端可以使用这些新打印机。不需要重启。

CUPS 接受各种用于打印机的 URI。以下是几个示例：

- ipp/zoe.canary.com/ipp
- lpd://riley.canary.com
- serial://dev/ttyS0?baudrate=9600+parity=even+bits=7
- socket/gillian.canary.com:9100
- usb:/XEROX/Phaser#206120?serial=YGG210547

某些类型接受选项（例如 serial），而其他则不。`lpinfo` 列出了你的系统可见的设备以及 CUPS 理解的 URI 类型。

“类”是一组共享一个队列的打印机。作业将在最先可用的打印机上执行。以下命令创建了类 `haemer` 并其中添加了三台打印机：riley、gilly 和 zoe。

```
$ sudo lpadmin -p riley -C haemer
$ sudo lpadmin -p gilly -C haemer
$ sudo lpadmin -p zoe -C haemer
```

只要 cups 配置为网络服务器，它就会立即让网络上的其他客户端可以使用这些新打印机。不需要重启。

CUPS 接受各种用于打印机的 URI。以下是几个示例：

- ipp/zoe.canary.com/ipp
- lpd://riley.canary.com
- serial://dev/ttyS0?baudrate=9600+parity=even+bits=7
- socket/gillian.canary.com:9100
- usb:/XEROX/Phaser#206120?serial=YGG210547

某些类型接受选项（例如 serial），而其他则不。`lpinfo` 列出了你的系统可见的设备以及 CUPS 理解的 URI 类型。

“类”是一组共享一个队列的打印机。作业将在最先可用的打印机上执行。以下命令创建了类 `haemer` 并其中添加了三台打印机：riley、gilly 和 zoe。

```
$ sudo lpadmin -p riley -C haemer
$ sudo lpadmin -p gilly -C haemer
$ sudo lpadmin -p zoe -C haemer
```

只要 cups 配置为网络服务器，它就会立即让网络上的其他客户端可以使用这些新打印机。不需要重启。

CUPS 接受各种用于打印机的 URI。以下是几个示例：

- ipp/zoe.canary.com/ipp
- lpd://riley.canary.com
- serial://dev/ttyS0?baudrate=9600+parity=even+bits=7
- socket/gillian.canary.com:9100
- usb:/XEROX/Phaser#206120?serial=YGG210547

某些类型接受选项（例如 serial），而其他则不。`lpinfo` 列出了你的系统可见的设备以及 CUPS 理解的 URI 类型。

## 服务关闭

如果你想删除打印机或类，可以使用 `lpadmin -x` 轻松完成。

```
$ sudo lpadmin -x fezmo
$ sudo lpadmin -x haemer
```

OK 服务智能，但如果你只是想临时禁用打印机呢？对于长时间停机接受作业是个坏主意。对于用户不可见的短暂中断（例如更换墨盒），请使用 `cupsdisable`。

## 其他配置任务

今天的打印机是无限配置的，CUPS 允许你通过 Web 界面以及 `lpadmin` 和 `lpoptions` 命令来调优各种功能。作为一个经验法则，`lpadmin` 用于系统级任务，而 `lpoptions` 用于用户级任务。

表 26.1 列出了随 CUPS 提供的命令并按其来源进行分类。

-1. 旧版本的 CUPS 使用 `enable` 和 `disable` 代替 `cuspenable` 和 `cupsdisable`。值得注意的是 `enable` 也是 `bash` 的一个内置命令，因此 `bash` 假设你指的是它自己的 `enable`，你指定了命令的完整路径。如果发生这种情况，*bash* 版本的 `enable` 用于启用和禁用内置命令，因此你可以使用 `enable -n enable` 来禁用它自身。

