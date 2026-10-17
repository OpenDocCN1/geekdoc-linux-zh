
```
author: Marcel Holtman <marcel@holtmann.org>

srcversion: FCDE9857FEA91A3DAFA9

depends: rfkill, crc16

intree: Y

vermagic: 4.6.0-kali-amd64 SMP mod_unload modversions

parm: disable_esco: Disable eSCO connection creation (bool)

parm: disable_ertm: Disable enhanced retransmission mode (bool)
```

如你所见，`modinfo`命令显示了关于该内核模块的重要信息，这些信息对于在系统上使用蓝牙是必要的。请注意，除其他外，它还列出了模块依赖项：`rfkill`和`crc16`。依赖项是蓝牙模块正常工作必须安装的模块。

通常情况下，在排查特定硬件设备无法工作的原因时，这些信息非常有用。除了注意依赖项等信息，你还可以获取模块版本以及该模块开发所需的内核版本，并确保它们与你正在运行的版本匹配。

## 使用 modprobe 添加和删除模块

大多数较新的 Linux 发行版（包括 Kali Linux）都包含了用于 LKM（可加载内核模块）管理的`modprobe`命令。要向内核添加模块，你可以使用带有`-a`（add）开关的`modprobe`命令，如下：

```
kali >modprobe -a <module name>
```

要删除模块，使用`modprobe`配合`-r`（remove）开关，后跟模块名称：

```
kali >modprobe -r <module to be removed>
```

使用`modprobe`代替`insmod`的主要优势是`modprobe`能理解依赖关系、选项以及安装和删除程序，并在做出更改之前考虑所有这些因素。因此，使用`modprobe`添加和删除内核模块更简单更安全。

## 插入和移除内核模块

让我们尝试插入和移除测试模块，帮助你熟悉这个过程。想象你刚刚安装了一块新的显卡，需要为它安装驱动程序。记住，设备驱动程序通常直接安装到内核中，以便它们获得正常运行所需的访问。这也使得驱动程序容易被恶意黑客安装 rootkit 或监听设备。

为了演示（请勿实际运行这些命令），假设我们想添加一个名为`HackersAriseNewVideo`的新显卡驱动。你可以通过以下命令将其添加到内核：

```
kali modprobe -a HackersAriseNewVideo
```

要测试新模块是否加载正常，你可以运行`dmesg`命令，该命令会打印内核的消息缓冲区，并过滤“video”以查找任何可能指示问题的警报：

```
kali dmesg | grep video
```

如果有任何包含“video”单词的内核消息，它们将显示在这里。如果什么都没有出现，说明没有包含该关键词的消息。

然后，要移除同一个模块，你可以输入相同的命令但使用`-r`（remove）开关：

```
kali >modprobe -r HackersAriseNewVideo
```
