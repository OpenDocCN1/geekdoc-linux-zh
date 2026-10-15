
# `VBoxManage modifyvm "VMname" --natnet1 "192.168/16"`

where `"VMname"` is the name you gave the guest VM when you installed it. This ensures that when the Solaris guest VM is run, the IP address of the NIC will be in the range of 192.168.0.0 to 192.168.254.254. In this example, the guest VM is assigned an IP address of 192.168.0.28, and the host an IP address of 192.168.0.13.

## Steps

2. Launch VirtualBox on PC-BSD, and start the Solaris VM guest.
3. In the Solaris guest VM window, make the Solaris menu choice "System > Administration > Network". The "Network Preferences" window opens on screen, with the title "Network Preferences (Solaris)", as seen in Figure 25.9. Note the virtualized IP address of the Solaris guest, which is seen in this window as something like 192.168.0.28/16 (DHCP) for the first NIC. It was assigned within the range by the `VBoxManage` command from Step 1.

![](img/02e070097d401d3bf7de4bf1c470b267_1329_0.png)
图 25.9 VirtualBox 网络首选项显示。

![](img/02e070097d401d3bf7de4bf1c470b267_1329_1.png)
图 25.10 VirtualBox 网络设置窗口。

![](img/02e070097d401d3bf7de4bf1c470b267_1329_2.png)
图 25.11 网桥适配器设置。

换句话说，客户机和主机在同一个子网中，但会有不同的 IP 地址。

3. 从 VM 屏幕顶部的 VirtualBox 菜单中，选择菜单项“Devices > Network > Network Settings”。“Network Settings”窗口出现在屏幕上，名称为“Solaris-Settings”，如图 25.10 所示。
4. 在“Attached to:”下拉菜单中，点击“NAT”右侧的向下箭头。这是在图 25.10 中看到的适配器 1。
5. 将下拉选项“Attached to:”更改为“ Bridged Adapter”，如图 25.11 所示。
6. 在做出“ Bridged Adapter”选择后，点击“Network Settings”窗口底部的“OK”按钮。

7. 点击“OK”按钮退出“Network Settings”窗口。
到目前为止我们所完成的是：
- 为 VM 客户机分配了一个 IP 地址，该地址在地址范围内。
- 检查了分配给我们 VM 客户机的实际地址。
- 确保为 VM 客户机分配的 IP 地址已连接到主机上的网桥适配器。这意味着 `bge0`，即主机 NIC，现在可以处理两个 IP 地址，即 PC-BSD 主机 IP 地址和 Solaris VM 客户机 IP 地址。

8. 从连接到主机的 LAN 上的另一台机器，FTP 到你的 Solaris VM 客户机主机。在我们的例子中，沿用之前的步骤，我们使用了以下命令：

```
$ ftp 192.168.0.28
```

在 Solaris VM 运行的情况下，发往 192.168.0.28 的入站 FTP 流量将被路由到 Solaris VM 客户机，你将能够将其用作安全的 FTP 服务器。

结论：使用 VM 客户机上的网桥适配器允许你通过主机上的同一物理 NIC 从 LAN 或 Internet 访问客户机。使用这种安全技术，你可以将客户机 VM 上运行的服务与主机系统隔离开来。

## EXERCISES 25.7

对 SSH 服务重复示例 25.8，以便你能从网络上的另一台系统 `ssh` 到运行在 PC-BSD 主机上的 Solaris 客户机。

## EXERCISES 25.8

以 Solaris 为主机系统，PC-BSD 为客户机执行示例 25.8。

## EXERCISES 25.9

对 TELNET 服务重复练习 25.7，以便你能从网络上的另一台系统 `telnet` 到运行在 Solaris 主机上的 PC-BSD 客户机。

## 25.4.5 在 LINUX 或 Windows 主机上安装 PC-BSD 或 Solaris 作为客户机 VM

本节所示的方法展示了如何在运行 LINUX 或 Windows 的主机机器上安装 PC-BSD 或 Solaris 作为客户机 VM。它们提供了以下优势：
- 练习以可选方式安装 PC-BSD 或 Solaris 的绝佳机会
- 确定你的特定硬件是否都得到 PC-BSD 或 Solaris 支持
- 让你尝试 PC-BSD 或 Solaris 的多个版本

这些方法与第 25.4.3 节（示例 25.7）不同，后者展示了使用刻录到 DVD 的 ISO 映像进行客户机安装。本节中的方法使用预建的、在线的、易于下载的整个客户机操作系统的磁盘映像。从 ISO 创建的 DVD 安装操作系统的过程是我们第 23 章中为 PC-BSD 和 Solaris 详细说明的。

我们使用 Ubuntu LINUX 15.04 和 Windows 10 作为我们的主机操作系统。本节中应用于这些系统的 方法也可以应用于 OS X。

### 25.4.5.1 在 LINUX 主机上安装 PC-BSD 客户机

我们描述了如何在主机操作系统上为 PC-BSD 安装准备 VirtualBox，使用从 `http://www.pcbsd.org/en/download.html` 获得的可下载的 `.vdi` 和 `.ova` 映像。

在开始客户机安装之前，我们下载了 `PCBSD10.2-RELEASE-x64-desktop.vdi.xz` 用于 LINUX 和 `PCBSD10.2-RELEASE-x64-desktop.ova` 用于 Windows。

请注意，随着 PC-BSD 的后续版本作为预建 VirtualBox 客户机提供，网站上的这些文件名可能会更改。

在尝试本节之前，你应该已在 LINUX 主机机器上安装了 VirtualBox。执行此操作的说明可在 `www.virtualbox.org` 上获得。在本书撰写时，VirtualBox 5 可用于 LINUX 系统。安装预制 PC-BSD 客户机操作系统的最低系统要求为：
- 64 位处理器架构
- 1024 MB 基础内存大小
- 用于 PC-BSD 安装的至少 50 GB 大小的虚拟磁盘
- 一个网桥网络适配器

在主机 LINUX 系统上下载并安装 VirtualBox 后，使用以下步骤在该主机上构建 PC-BSD 客户机：
1. PC-BSD 提供了预建的 VirtualBox 磁盘，可创建已预装 PC-BSD 作为客户机的预制 VM 客户机。从给定的网站下载预制文件。VirtualBox 文件以 `.vdi.xz` 扩展名结尾。`.xz` 表示文件需要先解压缩，以便它仅以 `.vdi` 扩展名结尾。
2. 在 LINUX 系统上，例如 Ubuntu，要解压缩压缩文件，使用 `xz` 命令，如下所示，使用你下载的文件名作为命令参数：

```
# xz -d -k PCBSD10.2-RELEASE-x64-desktop.vdi.xz
```
