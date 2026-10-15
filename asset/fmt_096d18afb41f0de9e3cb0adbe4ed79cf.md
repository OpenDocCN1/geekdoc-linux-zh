
![](img/a3584dae761d2e3abed8bf40d7637389_288_0.png)

## 使用 dSLIP 软件包实现的 SLIP 服务器

Matt Dillon <dillon@appollo.west.oic.com> 编写了一个软件包，它不仅可以拨入 SLIP，还可以拨出 SLIP。Matt 的软件包是一组用于管理你连接的小型程序和脚本的组合。你需要安装 `tcsh`，因为至少其中一个脚本需要它。Matt 提供了一个 `expect` 实用程序的二进制副本，因为该程序也被其中一个脚本所需要。你很可能需要一些 `expect` 的经验才能使这个软件包按你喜欢的方式运行，但不要因为这一点而却步。

Matt 在 `README` 文件中编写了一套很好的安装说明，所以我不必重复了。

你可以从其官方网站 `appollo.west.oic.com/pub/linux/dillon_src/dSLIP203.tgz` 获取 `dSLIP` 软件包

或从：`MetaLab.unc.edu`

`/pub/Linux/system/Network/serial/dSLIP203.tgz`

阅读 `README` 文件，并在执行 `make install` 之前创建 `/etc/passwd` 和 `/etc/group` 条目。

## 其他网络技术

以下小节针对特定的网络技术。包含在这些部分中的信息不一定适用于其他类型的网络技术。主题按字母顺序排序。

### ARCNet

ARCNet 设备名称为 `"arc0e"`、`"arc1e"`、`"arc2e"` 等，或 `"arc0s"`、`"arc1s"`、`"arc2s"` 等。内核检测到的第一张卡被分配为 `"arc0e"` 或 `"arc0s"`，其余则按检测顺序依次分配。末尾的字母表示你选择的是以太网封装数据包格式还是 RFC1051 数据包格式。

**内核编译选项：**

网络设备的配置 ---

[*] 网络设备支持

<*> ARCnet 支持

[ ] 启用 `arc0e` (ARCNet 'Ether-Encap' 数据包格式)

[ ] 启用 `arc0s` (ARCNet RFC1051 数据包格式)

一旦你正确编译内核以支持你的以太网卡，配置该卡就很简单了。

通常你可以使用类似这样的命令：

```
root# ifconfig arc0e 192.168.0.1 netmask 255.255.255.0 up
root# route add -net 192.168.0.0 netmask 255.255.255.0 arc0e
```

请参见 `/usr/src/linux/Documentation/networking/arcnet.txt` 和 `/usr/src/linux/Documentation/networking/arcnet-hardware.txt` 文件以获取更多信息。

ARCNet 支持由 Avery Pennarun <apenwarrr @foxtel.net> 开发。

### Appletalk (AF_APPLETALK)

Appletalk 支持没有特殊的设备名称，因为它使用的是现有的网络设备。

**内核编译选项：**

```
Networking options -->
<*> Appletalk DDP
```

Appletalk 支持使你的 Linux 机器能够与 Apple 网络协同工作。其重要用途之一是在你的 *Linux* 计算机和 Apple 计算机之间共享打印机和磁盘等资源。这需要额外的软件，称为 *netatalk*。Wesley Craig <netatalk@umich.edu> 代表密歇根大学的一个名为 "Research Systems Unix Group" 的团队，他们开发了 *netatalk* 软件包，该软件包提供了实现 Appletalk 协议栈及一些实用工具的软件。*netatalk* 软件包可能已随你的 Linux 发行版一起提供，或者你需要从其在密歇根大学的官方网站（参见 `ftp://terminator.rs.itd.umich.edu/unix/netatalk/`）通过 FTP 下载。

要构建并安装该软件包，请执行类似以下操作：

```
user% tar xvfZ .../netatalk-1.4b2.tar.Z
user% make
root# make install
```

你可能需要在实际使用 `make` 编译软件之前编辑 "`Makefile`" 。具体来说，你可能想要修改 `DEST-DIR` 变量，该变量定义了文件稍后将安装的位置。默认的 `/usr/local/atalk` 是相当安全的。

#### 配置 Appletalk 软件

为了让一切正常工作，你需要做的第一件事是确保 `/etc/services` 文件中存在适当的条目。你需要的条目是：

- `rtmp 1/ddp` # 路由表维护协议

- `nbp 2/ddp` # 名称绑定协议

- `echo 4/ddp` # AppleTalk 回声协议

- `zip 6/ddp` # 区域信息协议

下一步是在 `/usr/local/atalk/etc` 目录中（或你安装该软件包的位置）创建 Appletalk 配置文件。

第一个需要创建的文件是 `/usr/local/atalk/etc/atalkd.conf` 文件。最初，此文件只需要一行，该行给出支持你 Apple 机器所在网络的网络设备名称：

```
eth0
```

Appletalk 守护程序在运行后会自动添加更多详细信息。

#### 通过 Appletalk 导出 Linux 文件系统

你可以将 Linux 机器上的文件系统导出到网络，以便网络上的 Apple 机器可以共享它们。

为此，你必须配置 `/usr/local/atalk/etc/AppleVolumes.system` 文件。还有一个名为 `/usr/local/atalk/etc/AppleVolumes.default` 的配置文件，其格式完全相同，用于描述以访客权限连接的用户将接收哪些文件系统。

关于如何配置这些文件以及各种选项的详细说明可以在 `afpd` 手册页中找到。

一个简单的示例可能如下：

```
/tmp Scratch
/home/ftp/pub "Public Area"
```

这将把你的 `/tmp` 文件系统作为 AppleShare 卷 "Scratch" 导出，把你的 FTP 公共目录作为 AppleShare 卷 "Public Area" 导出。卷名称不是强制性的。守护程序会为你选择一些名称，但明确指定它们也无妨。

#### 通过 Appletalk 共享你的 Linux 打印机

你可以非常简单地将你的 Linux 打印机与 Apple 机器共享。你需要运行 `papd` 程序，它是 Appletalk 打印机访问

协议守护进程

运行此程序时，它将接受来自 Apple 机器的请求，并将打印任务排队发送到您本地的行式打印机守护进程进行打印。

您需要编辑 `/usr/local/atalk/etc/papd.conf` 文件来配置该守护进程。该文件的语法与您通常使用的 `/etc/printcap` 文件相同。您为定义赋予的名称将注册到 Appletalk 命名协议 NBP 中。

一个示例配置可能看起来像这样：

```
TricWriter:\n\tp=r:lp:op=cg:
```

这将使名为“TricWriter”的打印机在您的 Appletalk 网络上可用，所有接受的任务都会使用 `pd` 打印到 Linux 打印机“lp”（如 `/etc/printcap` 文件中定义）。条目“op=cg”表示 Linux 用户“cg”是该打印机的操作员。

#### 启动 Appletalk 软件

好的，现在您应该准备好测试这个基本配置了。`netatalk` 包附带了一个 `rc.atalk` 文件，应该可以正常工作，因此您只需要做的是：

```
root# /usr/local/atalk/etc/rc.atalk
```

然后所有服务都应该正常启动和运行。您应该看不到任何错误信息，软件会在启动过程中向控制台发送消息，指示每个阶段。

#### 测试 Appletalk 软件

要测试软件是否正常工作，请前往您的一台 Apple 机器，下拉 Apple 菜单，选择选择器（Chooser），单击 AppleShare，您的 Linux 机器应该会出现在列表中。

#### Appletalk 软件的注意事项

- 您可能需要在配置 IP 网络之前启动 Appletalk 支持。如果启动 Appletalk 程序时遇到问题，或者启动后 IP 网络出现问题，请尝试在运行 `/etc/rc.d/rc.inet1` 文件之前启动 Appletalk 软件。

- `afd`（Apple 文件协议守护进程）会严重搞乱您的硬盘。它在挂载点下方创建名为“Apple Desktop”和网络回收站文件夹的目录。然后，对于您访问的每个目录，它都会在下方创建一个 `.AppleDouble`，以便存储资源分叉等。因此，在导出 `/` 之前请三思。之后您将花大量时间清理。
