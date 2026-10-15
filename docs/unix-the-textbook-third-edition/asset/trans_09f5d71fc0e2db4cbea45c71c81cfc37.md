

处理 VirtualBox 时，以下基本术语很重要：

*Host OS:* 这是安装了 VirtualBox 的物理计算机的操作系统。在我们接下来的示例中，主机可以是 PC-BSD、Solaris、Ubuntu LINUX 或 Windows。

我们展示了在 LINUX 和 Windows 主机计算机上的 VirtualBox，因为使用这些系统作为主机有很多优势，并且将我们的 PC-BSD 和 Solaris UNIX 系统作为客户机部署在它们之上。我们稍后会谈到其中的一些优势。

*Guest OS:* 这是在 VM 内部运行的操作系统。VirtualBox 可以运行任何 Intel 或 AMD x86 操作系统，但仅正式支持并针对有限数量的操作系统进行了优化，Solaris 就是其中之一。FreeBSD 项目与 PC-BSD 一起，已将 VirtualBox 移植到这两个操作系统的最新版本，并且也可以成功部署在这两个系统上。正如我们在此所示，可以使用 LINUX 和 Windows 计算机作为主机，在其上部署 PC-BSD 和 Solaris 客户操作系统。

*VM:* 这是 VirtualBox 为正在运行的客户操作系统创建的特殊环境。你通过使用 VM 来运行客户操作系统。VirtualBox VM 在 PC-BSD 和 Solaris 上都显示为计算机桌面上的一个窗口。

如果你在 LINUX、Windows 或 Apple OS X 计算机上将 VirtualBox 安装为主机，你可以非常轻松地在该主机计算机上将 PC-BSD 和/或 Solaris 安装为 VM。事实上，我们展示了这种情况的示例。

控制 VM 设置的两种方式是通过 VirtualBox 管理器窗口，以及通过 VBoxManage 命令行程序。VM 本质上就是你可以通过这两种控制设施在其设置对话框中看到的内容。

*Guest additions:* 这指的是随 VirtualBox 一起提供的特殊软件包，但设计为安装在 VM 内部以提高客户操作系统的性能并添加额外功能。其中一个很好的例子是双向系统粘贴缓冲区设置，它允许你将文本复制到客户窗口中，并粘贴到主机窗口中，或反之亦然。我们以示例形式展示了如何执行此操作。

我们发现，在 PC-BSD 和 Solaris 中，我们需要在完全创建一个新的 VM 并启动它之后，才能为该 VM 启用客户机增强功能。这是在 VM 启动后通过选择 VirtualBox 菜单项“Devices > Insert Guest Additions CD”来完成的。然后 VirtualBox 会在 VM 的桌面上放置/挂载一个“虚拟”CD，如果你点击它来启动 CD，就可以使用虚拟 CD 的内容进行安装。

## 25.4.1 在 PC-BSD 主机操作系统上安装和运行 VirtualBox

截至本书撰写时可用的最新 PC-BSD，VirtualBox 并未预装在 PC-BSD 上。

安装 VirtualBox 的最简单方法是使用 App Café 下载并自动安装到你的系统。在 App Café 中，使用 App Café 窗口顶部的搜索图标并输入 VirtualBox 作为搜索条件。

然后你将看到 `pcbsd-meta-virtualbox-1429971087` 或 VirtualBox 的最新可用元包的选项。点击 App Café 中的“Install”按钮将此包安装到你的 PC-BSD 机器上。安装完成后，你需要注销并重新登录计算机，以便将你添加到 VirtualBox 组。

要运行 VirtualBox，你可以点击 PC-BSD KDE 桌面上的其图标，或在控制台窗口的命令行中输入 `VirtualBox`。

## 25.4.2 安装和运行 Solaris VirtualBox

以下示例展示了将 VirtualBox 安装在 Solaris 系统作为主机系统所需的步骤，以便在其内部安装客户系统。

### Example 25.6

目标：要在主机 Solaris 系统上安装和运行 VirtualBox VM。

介绍：我们从 www.virtualbox.org 获取最新 SunOS 版本的 VirtualBox，然后安装它。这可以以非常相似的方式完成，以支持其他操作系统，从而让你在这些操作系统上安装 VirtualBox。请在 www.virtualbox.org 上查看支持的操作系统，以及在这些操作系统上安装 VirtualBox 的方法。

先决条件：
- 1. 你必须在 Solaris 系统上工作。
- 2. 你必须在系统上拥有超级用户权限。

程序：按此处呈现的顺序执行以下步骤，以满足本示例的目标。

- 1. VirtualBox 的最新版本可以在 www.virtualbox.org 找到。在 Web 浏览器中下载它。例如，在本书撰写时，我们通过 Firefox Web 浏览器下载了 `VirtualBox-4.3.16-95972-SunOS.tar.gz`。在我们的例子中，它被下载到 /home/bob 的 Downloads 子目录中。
- 2. 找出系统上当前可用的区域名称。在我们这里，一开始只有全局区域可用。
  $ zonename
  global
- 3. 成为超级用户。
  $ su
  Password: xxx

