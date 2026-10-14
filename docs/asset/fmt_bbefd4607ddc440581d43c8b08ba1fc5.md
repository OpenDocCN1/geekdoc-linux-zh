
# 第四部分 额外章节

另一个常见问题，特别是当你尝试多种虚拟化技术时，是不同的虚拟化解决方案兼容性不佳。例如，在写作期间，如果你在已加载 KVM 虚拟机可加载内核模块的系统中尝试启动 VirtualBox 虚拟机，你将看到类似图 B7-21 所示的错误对话框。

### 图 B7-21

关于虚拟化解决方案冲突的错误对话框

![](img/e3248f698da647444405a34229bd9df5_1434_0.png)

幸运的是，这个对话框具有某种误导性，它告诉你必须重新编译内核。这哪里是二十世纪了？要解决这个特定问题，你所做的就是使用如下命令删除 VirtualBox 报错的可加载模块。

```
sudo /sbin/rmmod kvm_intel kvm_amd
```

你的系统仅使用了 `kvm` 和 `kvm_intel` 模块之一（因为你的系统里可能只有一种类型的处理器），因此它只会对其中一个进行报错。然而，在运行此命令后，你应该能够清除 VirtualBox 虚拟机窗口，点击 VirtualBox 窗口中的“启动”图标，并继续在虚拟机中安装操作系统。如果你在虚拟机窗口中看到关于找不到任何引导介质的消息，请使用“设备”菜单为虚拟机重新挂载安装程序，并选择虚拟机的 Windows 重置命令以重新启动引导过程。

![](img/e3248f698da647444405a34229bd9df5_1435_0.png)

- 如果你的系统启动时自动加载了另一种虚拟技术的可加载模块，那么该技术的启动脚本可能在启动期间正在运行。检查 `/etc/modules.d` 中的符号链接——你可以删除指向“其他”虚拟技术的符号链接（例如本例中的 KVM），以防止其模块在下次启动时被加载。

## 安装和使用 VMware Server

VMware (`www.vmware.com`) 是通用硬件虚拟化领域的“巨头”，自 90 年代后期以来，它一直主导着商业虚拟化领域，并为 Linux 和 Windows 系统提供了卓越、稳定且可靠的客户操作系统虚拟化。我从 1999 年就开始拥有 VMware Workstation 1.6 版本（那是很久以前了），多年来一直关注他们的产品，对他们的产品只有好评。他们将 VMware Player 和 Server 作为免费软件发布（不要与开源软件混淆），这对 SOIHO（小型办公家庭办公室）、SMB（中小企业）以及其他机构来说是一个福音，也是一次高明的市场策略。如果商业软件也能看到这种方法的好处，那就就太晚了。

![](img/e3248f698da647444405a34229bd9df5_1435_1.png)

> 这一点小插曲并没有削弱我对 Xen 是更优解决方案的信念。开源是“正确的事”，我相信 Xen 的监视器就是 VMware ESXi 产品中使用的那一个（微软 Hyper-V）。现在可以从 VMware 网站获取免费版本的 VMware ESXi，就像微软一样免费。有这么多的人访问了它……

VMware 拥有广泛的产品线，涵盖多种语言、不同的支持级别以及管理工具的各种组合，其复杂程度仅略低于人类基因组图谱。请访问其网站获取更多信息。

通常情况下，VMware 的虚拟化产品分为两类：工作站版和服务器产品。两者都支持安装和运行未经修改的 x86 操作系统，包括 BSD、Linux 发行版、所有版本的 Microsoft Windows、x86 Solaris 实现，甚至经过修改的 Mac OS 版本（尽管目前尚不支持）。Workstation 产品支持按需执行各种虚拟机，尽管你可以同时运行多个虚拟机。免费版和 ESX Server 产品具有在引导启动时自动执行虚拟机的功能，尽管标准免费版更多的是是一个客户操作系统解决方案，而不是 ESX 所提供的高性能、裸金属虚拟化环境。

## 使用虚拟机和模拟器

所有 VMware 虚拟化产品都采用集成的虚拟机管理程序（hypervisor），它提供了一个客户操作系统可以利用而无需任何修改的抽象视图。VMware 的虚拟化产品可以原生执行非特权操作系统代码，提供了内在性能改进，并在可能的虚拟机之间提供了良好的代码共享机会。

内部，VMware Workstation 和免费版服务器使用可加载内核模块在虚拟机与你的物理硬件之间建立接口。它们还包含一个 DHCP 服务器以及集成的 NAT 和桥接网络支持团队，简化了虚拟机的网络管理和分段。

关于 VMware 的更多信息：

- VMware 网站 (`www.vmware.com`)：有关 VMware 产品线和特定 VMware 产品的终极信息源。特定 VMware 产品的文档可以在 `www.vmware.com/support/pubs/` 获取。
- VMware 社区 (`http://communities.vmware.com/index.jsp`)：关于 VMware 产品的用户驱动信息、使用技巧和窍门以及更多内容。

接下来的章节将解释如何安装和配置 VMware Server，以及如何创建一个具有可用网络支持的虚拟机。关于 VMware 的设置和配置有大量的书籍和文章（包括其卓越的产品文档），但接下来的章节将帮助你快速上手 VMware Server 和虚拟机，让你看到这一切到底在折腾什么。

## 下载和安装 VMware Server

虽然网页上将 VMware 列为合作伙伴并说明你可以通过常用仓库下载 VMware Server，但我似乎找不到它。这在之前的 Ubuntu 版本中确实如此，但也许情况已经发生了变化。这其实并不重要，因为你可以轻松地从 VMware 网站下载并安装 VMware Server，但缺点是你必须手动安装，而不是通过大多数 Linux 发行版提供的标准软件包管理工具安装 DEB 包。

> VMware 安装过程的一部分是构建两个可加载内核模块……（提供的 OCR 文本在后半部分似乎损坏/重复了，请参考下方安装过程的逻辑流）。

执行此操作。配置脚本的第一步是接受另一份 EULA（最终用户许可协议）。在浏览完协议后，输入 `yes` 接受 EULA 并按 Enter/Return 继续实际配置过程。

配置脚本将提示你想要安装一些额外文件的位置，如下例所示：

你想在哪个目录中安装 mime 图标？

```
[/usr/share/icons]
```

哪个目录包含你的桌面菜单条目文件？这些文件具有 `.desktop` 扩展名，[/usr/share/applications]

你想在哪个目录中安装图标？

```
[/usr/share/pixmaps]
```

我通常通过在响应每个提示时按 Enter/Return 来接受默认设置。

接下来，好戏开始了。VMware Server 配置脚本会检查它是否为你的内核提供了预构建的内核模块（实际上并没有，相信我）。这并不是什么坏事——Canonical 的人员经常更新更新 Ubuntu 和 Kubuntu 使用的内核版本，你不能期望一个外部软件包能一直跟上这种更新速度。在过程中，你会看到类似下面的消息：

```
Trying to find a suitable vmmon module for your running kernel.

None of the pre-built vmmon modules for VMware Server is suitable for your running kernel. Do you want this program to try and build the vmmon module for your system (need to have a compiler installed on your system)? [yes]
```

你会说 `yes`（或按 Enter/Return）。脚本将识别它正在使用的 C 编译器的位置，并提示你与系统当前运行的内核相关的头文件位置。你通常可以接受它的建议，因为它是通过检查你的系统得出的。安装脚本将尝试构建虚拟机与 Linux 内核之间交互的 `vmmon` 内核模块。所有输出看起来如下：

```
Using compiler /usr/bin/gcc. Use environment variable CC to override.

What is the location of the directory of C header files that match your running kernel? [/lib/modules/2.6.24-19-386/build/]

Extracting the sources of kernel

Building the vmmon module.

making -C /tmp/vmware-config0/vmmon-only

smake -C /lib/modules/2.6.24-19-386/build/..
```
