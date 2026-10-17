
更新你的系统需要添加 Cubic PPA 的内容。`sudo apt update --no-install-recommends cubic`

下一步是使用 Cubic 安装最新的 Ubuntu ISO。我们将使用 21.04，但 20.04 LTS（长期支持版）是一个很好的选择，因为它。Cubic 界面提供了一个让你与文件系统交互的环境。

![](img/1e7c2db42dac866a51a0ace7df48feef_127_1.png)

## 破解（Hacking）

硬件或任何更新的内核都可以工作。通过终端（*name of kernel* 页面）安装你想要使用的内核，如果它导致了任何问题，请选择其他内核。

你看到的是一个标准的 Ubuntu，但它会安装我们添加的额外内容（在本例中为 GIMP 和 Inkscape）。如果你选择“测试 Ubuntu（Test Ubuntu）”而不是“安装（Install）”，你可以使用现场环境并安装我们添加的额外内容。如果你在 Ubuntu 安装器选项中选择“最小（minimal）”，我们的更改会被添加，但安装速度会更快且更不臃肿。

> 快速提示
> 如果出现以下内核错误弹出窗口：“dialing /dev/sda1, check file system or disc.”，可以忽略。

Present 允许你在安装 Ubuntu 之后更改选择。关于是否预读，请参阅 [Debian Wiki](https://wiki.debian.org/DebianInstaller) 了解其细节以及它是如何工作的。“启动（Boots）”提供了与 GRUB 启动加载器无关选项，例如，我们可以更改此页面上的任何内容。该页面还允许你更改 SquashFS 使用的压缩方法，我们将保持原样。

## 生成 ISO

下一页是生成器，一旦你想要执行此操作，Cubic 就会开始构建安装、使用简单示例对系统进行测试，如果你在使用 Cubic，它会恢复此过程。压缩文件系统和构建 ISO 是一个漫长的过程，通常会让你的 CPU 和内存承受巨大压力。Linux 在处理大文件、大量文件或两者兼有时总是会使用大量内存；因此当你需要这一点时，考虑关闭其他程序，留出足够的内存保存。我们用于测试的 8GB 机器空间有点拥挤，因此如果计划出现任何问题，结果将是一个加载到虚拟机中的 ISO 以完成任务。

一旦安装完成，所有组装的内容都按预期工作，因此你可以在 Ubuntu Linux 中进行测试然后删除它。

我们只进行过一次测试安装，所以对使用 Cubic 能做的事情仅触了皮毛。这里有一些进一步的改进和想法，可以改进安装。要添加内容，你可以打开你正在使用的 Cubic 工作目录。这可以节省时间，并保持所有操作通过包系统完成。

## 桌面环境

我们可以通过输入终端安装 LXDE 桌面环境和 LightDM 登录管理器。在页面上，当你这样做时，你会看到一个列表让你选择想要加载的桌面环境。选择 LightDM。对于新用户，你可以使用 Cubic 编辑文本文件，将 LXDE 设置为新用户的默认环境。重启后，它现在将自动登录到 LXDE，此外，LXDE 将成为现场 ISO 的桌面环境。如果你选择‘Ubuntu’而不是‘Ubuntu’。

``` 
sudo apt-get install light-desktop
```

对于长期终端，使用 Cubic 表格来获取它并不坏。如果你希望重启后的部分读取 LXDE 而不是自动的，它就在那里。然后你可以

使用 apt 技巧从已安装的系统中复制安装（copy-install）包。`dpkg-selections`。然后你可以通过在 Cubic 的短终端中输入以下命令来安装这些包：

- `dpkg-selections > packagelist`

你也可以通过在安装的终端中输入第一个命令，来“保存”你在 Cubic 中用过的系统包。当然，你可以通过文本编辑器手动对其进行修剪。

![](img/1e7c2db42dac866a51a0ace7df48feef_129_0.png)

## 在虚拟机中运行

创建一个环境的缺点是，你通常需要反复执行安装这一过程中最耗时的部分。通常，你会在虚拟机（VM）中反复这样做，直到你对其熟于掌握。分配所需的最小内存。

与所有基于 Linux 的工作一样，增加可用内存会加快速度。分配更多内存意味着更合理的性能。尽可能分配尽可能多的核心，因为 Ubuntu 安装器将充分充分利用它们。如果使用 VirtualBox 作为虚拟化程序，在“设置 > 存储 > 使用主机 I/O 缓存（Use Host I/O Cache）”中有一个选项，当你发现它加快了安装时。使用此选项如果虚拟机崩溃会有数据丢失的轻微风险，但如果只需重新开始安装，也没大问题。

即使你必须重新进行完整安装，在 Ubuntu 安装器中选择“最小（minimal）”以加快测试 VirtualBox 设置表格时的速度。

VirtualBox（以及可能的其他虚拟机管理器）可以加快 I/O。

130 | 黑客手册

* 关于此内容

## 构建你自己的 Ubuntu 发行版

gnome-look.org 上的 Plymouth 主题。大多数主题都带有一个安装脚本。

选择你想要删除的包以进行最小化安装。

要使用 Cubic，下载主题并解压，然后使用复制图标将文件复制到环境中。在 Cubic 中，添加目录并运行安装脚本。一旦完成，使用 `rm -rf [name of directory]` 移除刚刚复制到 ISO 的目录。使用官方 Ubuntu Wiki (https://wiki.ubuntu.com/) 获取更多关于自定义你的 Ubuntu 主题的信息。这些指令中的大多数都不需要修改你的引导启动，可能只需要进行这些更改

| 类型 | 包 | 版本 |
|---|---|---|
| 典型 | accountservice-ubuntu-schemas | 0.7.15+ubuntu2.04 |
| | adwait | 3.26-2ubuntu1 |
| | ags-support | 1.0-ubuntu1 |
| | elementary-icons | 3.8.0-ubuntu2 |
| | elementary-theme | 3.8.0-ubuntu2 |
| | apt-base | 2.24-ubuntu1 |
| | apt-common | 2.24-ubuntu1 |
| | apt-files | 2.24-ubuntu1 |
| | ammonia-module | 0.19-ubuntu4 |
| | dkms | 5.22-ubuntu1 |
| | desktop-icons | 3.36-ubuntu1 |
| | desktop-theme | 3.36-ubuntu1 |
| | common-files | 2.24-ubuntu1 |
| | theme-icons | 3.38-ubuntu1 |
| | theme-theme | 3.38-ubuntu1 |
| | theme-module | 1.0-ubuntu4 |

> ISO 生成脚本。这是一个耗时的过程，在运行期间 CPU 使用率会达到峰值。

## 用户与壁纸

启动屏（如启动界面）Ubuntu 使用名为 Plymouth 的系统。Plymouth 是一种自定义启动过程的方法。有很多内容你可以修改并获得这些主题。开始自定义启动屏的最简单方法是

## 自定义 PPA

你可以根据需求在 Ubuntu 中添加和使用 PPA，除了在终端中自定义环境。例如，你可以使用 Inkscape PPA 并通过输入安装它：`apt-add-repository ppa:inkscape/dev && apt install inkscape`

这意味着在更新系统时将安装 Inkscape，并且它将从 PPA 而不是默认存储库获取。你也可以使用 `apt-cache policy` 并将其存入文本文件，如果你想保留添加到系统的存储库完整列表以备后参考。

将下载的内容添加到根环境并使用 `dpkg -i [name].deb` 安装它们。一切都能正常工作，但有时在自定义你的主目录时需要像早期那样提供一些。如果无法安装安装，你可以手动复制文件并添加一个小小的安装脚本，手动调用，安装。

祝愉快！

![](img/1e7c2db42dac866a51a0ace7df48feef_130_0.png)

## 黑客技术

## LTTng: 在 Linux 中跟踪应用程序

现在是时候介绍软件追踪的基础知识，以及如何使用 LTTng 来理解运行系统上发生了什么了。

![](img/1e7c2db42dac866a51a0ace7df48feef_131_0.png)

- Ubuntu 16.04 需要 `lttng`、`lttng-devel` 和 `libttng-ust-dev` 来使用 LTTng

```
$ sudo apt-get install lttng lttng-devel libttng-ust-dev

Reading lists... Done

Building dependency tree

Reading information... Done
```
