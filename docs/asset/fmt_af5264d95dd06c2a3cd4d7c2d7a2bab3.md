
*   `XFree86-twm-4.0.1-1`

*   `XFree86-ISO8859-2-100dpi-fonts-1.0-12`

*   `XFree86-ISO8859-7-100dpi-fonts-1.0-7`

*   `XFree86-ISO8859-9-100dpi-fonts-2.1,2-13`

*   `XFree86-cyrillic-fonts-4.0.1-1`

然后，您可以使用 `rpm` 命令及其 `-e` 或 `erase` 选项，配合通配符 `.rpm` 软件包名称，一次擦除各种软件包，方法如下：

```bash
# rpm -e XFree\*ISO\*
```

接下来，插入第一张 Red Hat CD-ROM，并使用 `mount` 命令使其在您的系统上可用（它也可能自动挂载）：

```bash
# mount /mnt/cdrom
```

由于 Red Hat Linux 在文件系统表 `/etc/fstab` 中提供了一项条目，您也可以指定系统的 CD-ROM 设备 `/dev/cdrom`（指向您的 CD-ROM 设备的符号链接），在 `/mnt/cdrom` 目录下挂载 CD-ROM，方法如下：

```bash
# mount /dev/cdrom
```

在命令行中，使用 `rpm` 的方法如下：

```bash
# rpm -Uvh /mnt/cdrom/RedHat/RPMS/XFree86*.rpm
```

如果您没有安装 X，可以使用 Red Hat 的 `rpm` 命令来安装软件。但是，您应该知道该过程将涉及解决许多 `.rpm` 软件包依赖项！

### 注意

您也可以尝试使用 `gnorpm` 命令来安装软件。选择“首选项”（Preferences），然后将界面首选项 `RPM` 路径设置为已挂载的 Red Hat CD-ROM 上的 `RPMS` 目录。KDE 还包括一个名为 `kpackage` 的类似软件包管理器客户端。

根据安装的软件，这些目录可能会占用 40-400MB 的硬盘空间，如果您安装了大量的 X 窗口管理器、编程库或其他软件，占用空间甚至更多。（典型的 XFree86 完整安装大约为 80-123MB，具体取决于额外的客户端数量。）

## 选择配置工具

大多数新 X 用户在安装 XFree86 后面临的最大障碍是生成一个可用的 `XF86Config` 文件。此文件可以在安装过程中初始生成，但如果您有问题的图形芯片组，您可能需要在启动后“微调”配置，甚至可能希望在首次登录后再配置 X11。有时这是最安全的方法；尝试登录一个配置为直接启动到 X11 但系统未正确配置的 Linux 系统可能会令人困惑。幸运的是，如果遇到此问题，您只需按 `Ctrl+Alt+Delete`，重新启动，然后在 Red Hat LILO 登录界面按 `Ctrl+X`，或在 LILO 启动提示处传入内核参数 `linux single`，方法如下：

```bash
boot: linux single
```

如果您已经有一个可用的设置，您的旧 XFree86 3.3.6 `XF86Config` 可能也能工作，因为新服务器内置了一些兼容性。但是，新版本的 XFree86 使用新的布局结构用于 `XF86Config` 文件！

如果您从零开始，安装 X 之后、配置之前的第一件应该做的事情是尽可能多地阅读文档。虽然大胆无畏的人会直接开始配置 X11，但即使是经验丰富的用户也会受益于阅读有关最新 XFree86 发展的内容，并查阅 XFree86 文档中关于其特定硬件的提示。

撰写本文时文档仍然略显简略，但您可以在 `/usr/X11R6/lib/X11/doc` 目录下找到信息。表 4.1 包含 XFree86 4.0.1 此目录的详细信息。请注意，该版本的文档仍然略显简略；如果您看不到图形芯片组的 README 文件，并不意味着它不受支持！这对于 Cirrus Logic、NeoMagic、Tseng 和 Trident 芯片组都是正确的。您可以在 `/usr/share/doc/XFree86-doc-4.0.1` 目录下找到关于协议、库、客户端和其他服务的详细信息。

### 表 4.1 XFree86 文档

| 文件 | 描述 |
| :--- | :--- |
| `DESIGN` | 广泛的服务器设计信息 |
| `LICENSE` | 许可和版权声明 |
| `README` | 关于当前 XFree86 版本的一般信息 |
| `README.Deciga` | 面向 DEC 21030 用户的信息 |
| `README.DGA` | 如何为 XFree86 DGA 接口编程 |
| `README.DRI` | 关于 DRI 支持的信息 |
| `README.DRIcomp` | 关于 DRI 的编译信息 |
| `README.S3` | 面向 S3 芯片组用户的说明 |
| `README.s3virge` | 面向 S3 VIRGE、ViRGE/DX、ViRGE/GX、ViRGE/MX 和 ViRGE/VX 用户的说明 |
| `README.SIS` | 面向 SiS 芯片组用户的说明 |
| `README.apm` | 关于 Alliance Promotion 芯片组的说明 |
| `README.ati` | 关于 XFree86 ATI 适配器视频驱动程序的信息 |
| `README.chips` | 关于 Chips and Technologies 芯片组的说明 |
| `README.cyrix` | 面向 Cyrix MeidaGX 用户的信息 |
| `README.fonts` | 在 XFree86 中使用字体 |
| `README.i740` | 面向基于 Intel 740 显卡的信息 |
| `README.i810` | 关于 Intel 810 主板的信息 |
| `README.mouse` | 关于 XFree86 的 X11 鼠标支持的详细信息 |
| `README.r128` | ATI Rage 128 信息 |
| `README.rendition` | 关于 Rendition 芯片组用户的详细信息 |
| `RELNOTES` | XFree86 的权威发行说明 |
| `ServersOnly` | 构建 XFree86 X 服务器时目录应有的样子 |
| `Status` | 该版本中的驱动程序状态 |
| `videoBoardD8` | 关于 PC98 XFree86 服务器的信息 |

如果您是 X11 的新手，首先阅读 X 和 XFree86 的手册页，以获取 X 的概述。在开始配置 X 之前，您需要了解有关您的计算机以及您的计算机视频卡和监视器的一些技术细节。以下是将有所帮助的一些信息：

- 安装在您计算机中的视频卡类型、制造商、名称或型号
- 为您的卡安装了多少视频 RAM（而非系统 RAM）
- 您的视频卡芯片组使用的时钟芯片类型
- 您使用的鼠标类型（例如 PS/2、串行或 USB）
- 连接到您计算机的监视器类型、制造商、名称或型号
- 您监视器的垂直和水平刷新率（例如 55~100 垂直，30~60 水平）
- 您使用的键盘类型

掌握这些信息后，您必须选择配置 XFree86 的方法或工具，并为您的系统生成正确的 `XF86Config` 文件。有几种方法可以做到这一点：

- XFree86 主 X11 服务器的内置配置功能
- `Xconfigurator` Red Hat 的图形化 X11 设置工具
- `xf86config` XFree86 的传统纯文本工具
- `xf86cfg` XFree86 的图形配置客户端
- Manual 使用喜欢的文本编辑器创建自己的 `XF86Config`

所有这些方法都可以通过控制台命令行或终端窗口命令行来完成。

`Xconfigurator` 和 `xf86cfg` 的优势在于提供图形界面；`xf86config` 在文本模式屏幕上询问一系列问题；而 XFree86 自动执行配置。如果您幸运的话，您计算机的硬件将完全匹配这些程序生成的配置。如果设置无法正常工作、输入了错误信息，或者您的视频芯片组未完全被 XFree86 服务器所需的模块支持，可能会出现一些问题。

一般来说，使用几年的视频硬件比“最新款”的视频显卡表现要好得多，因为软件贡献者有时间处理这些视频芯片组。笔记本电脑用户也可能会遇到特殊问题，购买最新款笔记本电脑后发现嵌入式视频系统无法与 X 系统兼容，这可能会让人灰心——值得事先做些调查！

台式机用户可以选择安装一块新的、受支持的显卡。笔记本电脑用户应务必访问位于 `http://www.cs.utexas.edu/users/kharker/linux-laptop` 的 Linux 笔记本电脑用户站点。

如果你发现无法获得正确的设置，或者你的芯片组不受支持，你也可以从介绍中提到的供应商那里购买商业版 X 发行版。最后，你的最后手段是去抱怨、恳求、劝诱或贿赂一位熟练的程序员，让他们根据 XFree86 源码为你构建一个模块（但这很少奏效）。

请记住：目标是生成最适合你需求的 `XFree86Config` 文件！

## XFree86Config 文件
