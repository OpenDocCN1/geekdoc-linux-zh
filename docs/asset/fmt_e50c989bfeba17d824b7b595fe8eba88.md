
我使用这种方法将从数码相机下载的图像添加到 live CD 中，而不改变其结构（参见第 10 章“自定义演示 Linux”，查看挂载目录的示例）。

## 向 ISO 卷头添加信息

在制作 live Linux CD 时，可以使用 `mkisofs` 命令添加其他有趣实用的选项。你可能希望使用这些选项中的几个为 live CD 的卷头添加更多信息：

- `p "preparer-id"`—将 `preparer_id` 替换为你（负责 live CD 的组织）的信息。你可以在此选项中使用 `-p "www.example.com"` 或类似内容。
- `publisher "name"`—使用此选项识别发布者名称。例如，可以使用 `-p "Acme Widgets"` 作为值。
- `V "Vol1_ID"`—将 `Vol1_ID` 替换为你想要分配给卷的卷名称。这很重要，因为在许多 Linux 系统中，它将作为 live CD 的挂载点名称。例如，可以使用选项 `-V "LivelinuxCD"`，这样当生成的 live CD 插入 Linux 系统时，它可以自动挂载到 `/media/LiveLinuxCD` 目录。
- `volset "ID"`—指定卷集 ID。由于你可以输入最多 128 个字符，因此它为卷集提供了更详细描述的空间。

该选项可以像示例所示设置：
- `-volvolset "This is 1 of 5 live CDs showing live Linux solutions"`

如果你按照本章后面介绍的那样使用 K3b 将 ISO 刻录到 CD，你可以看到此信息被添加到卷头中。如果你使用了前面章节中所示的选项，当你将镜像加载到 K3b 进行刻录时，卷头信息将如图 B-1 所示。

![](img/6b7a4aaf8c4f76728e9b63b90222dd8e_407_0.png)

图 B-1 在 K3b 中显示的通过 `mkisofs` 添加到卷头中的信息。

如你所见，系统自动填充了镜像类型（Iso9660 镜像）、镜像大小（633.4MB）和系统 ID（LINUX）。系统 ID、卷 ID、卷集 ID、发行者 ID 和制备 ID 均来自你描述的 `mkisofs` 选项。其他信息包括应用程序 ID（指示 `mkisofs` 创建了 ISO）和 MD5SUM（当 K3b 读取 ISO 镜像时会进行检查）。

如果你正在准备大量的光刻 CD——例如，为你的公司或组织——你可能希望在制作的所有光刻 CD 中包含相同的的卷头信息。你可以使用 `.mkisofsrc` 文件来设置这些值。`mkisofs` 命令会检查当前目录、你的主目录以及命令所在的目录以寻找 `.mkisofsrc` 文件。

此 `.mkisofsrc` 文件示例包含了可以替代 `mkisofs` 命令行选项的标签。要查看如何使用这些标签提供图 B-1 所示的相同信息，已将这些信息添加到此处显示的标签中：

```
PREP="www.example.com"
PUBL="Acme Widgets"
VOLI="LiveLinuxCD"
VOLS="Acme Widgets Live CD set. This is 1 of 5 live CDs showing live Linux solutions."
```

你在 `.mkisof` 文件中可以作为管道使用的其他标签包括 `APPI`（用于设置多达 128 个字符的应用程序标识）、`COPY`（添加最多 37 个字符的版权信息）、`ABST`（识别磁盘上包含磁盘内容摘要的文件）、`BIBL`（最多 37 个字符的文献引用信息）以及 `SYSI`（将 SYSI 更改为 LINUX 除的任何内容）。

这里是你可能需要的 `mkisofs` 命令的最后一个额外用途：如果你打算将 `mkisofs` 的输出直接管道到 `cdrecord`，某些 CD 刻录机（以及写入模式）需要提前知道 ISO 镜像的大小。那么该命令的格式将如下所示：

```bash
# mkisofs options | cdrecord options
```

除了你输入的其他 `mkisofs` 和 `cdrecord` 选项外，你还需要使用 `size=#s` 选项将镜像的大小传递给 `cdrecord`，其中 `#` 被替换为生成的 ISO 镜像的大小数字。要获取 `cdrecord` 需要的数字（2048 字节扇的数量），请在你即将运行的 `mkisofs` 命令中添加 `print-size` 选项。例如：

```bash
# mkisofs -R -b isolinux/isolinux.bin -c isolinux/boot.cat \
-no-emul-boot -boot-load-size 8 -boot-info-table -print-size \
Using ".mkisofsrc"

Total extents scheduled to be written = 324323
```

使用此示例，当你运行 `cdrecord`（或当将 `mkisofs` 的输出管道到 `cdrecord` 时），你可以在 `cdrecord` 命令行中添加以下值：

```
size=324323s
```

`mkisofs` 命令还有许多其他可用选项。要读取这些选项，请参阅 `mkisofs` 的 man 页 (`man mkisofs`)。或者，你可以运行带有 `-help` 选项的 `mkisofs` (`mkisofs -help`)。

# 附录 B 构建、测试和刻录 ISO

## 使用 QEMU 测试 ISO 镜像

通过模拟 PC 处理器和系统组件，QEMU 处理器模拟器 (`http://fabric.bellar.free.fr/qemu`) 可以启动磁盘镜像，以便你可以在 Linux 桌面面的窗口上运行早期的可启动操作系统。

被模拟的系统可以是带有 IDE 总线的标准 PC，也可以是带有 ISA 总线的 PC（通过添加 `-M ispc` 选项）。

QEMU 可以在用户模式（允许其在不同的 CPU 类型上运行为一种 CPU 创建的进程）或全系统模拟（CPU 和外设）下运行。人们经常在用户模式下将 QEMU 用于 `WINE`，允许他们安装并运行 Windows 应用程序，或用于 `DOSEMU` 以运行 DOS 应用程序。然而，为了测试光刻 CD 镜像的目的，本书描述了全系统模拟模式下的 QEMU。

对于书中描述的 Linux 发行版，QEMU 提供了预发布二进制文件。有了 Internet 连接，你可以使用以下命令分别从 Debian/Knoppix、Fedora 和 Gentoo 安装 QEMU 二进制包：

- 基于 Debian 的系统：`# apt-get install qemu`
- 基于 Fedora 的系统：`# yum install qemu`
- Gentoo 系统：`# emerge qemu`

如果你愿意，也可以从源代码安装 QEMU。QEMU 源代码可以从 QEMU 下载页面获取 (`http://fabric.bellar.free.fr/qemu/download`)。

## 启动 QEMU

使用带有 `-boot` 选项的 QEMU 命令非常简单。例如，对于启动 镜像：

```bash
# mkisofs -R -b isolinux/isolinux.bin -c isolinux/boot.cat \
-no-emul-boot -boot-load-size 8 -boot-info-table -print-size \
Using ".mkisofrc"

Total extents scheduled to be written = 324323
```

### 现场 Linux CD

监视器（来自 QEMU 文档）包括移除和插入可移动介质（CD、DVD 或软盘）、从磁盘文件恢复虚拟机状态（在冻结和取消冻结虚拟机后），以及使用外部调试器检查虚拟机。

你可以配合 QEMU 监视器使用一些命令。在显示监视器（按下 Ctrl+Alt+2）时，你可能想尝试这些命令：

- `- help`—列出所有可用命令。
- `- info ??`—将 `??` 替换为组件名称以查看关于该组件的附加信息。你可以了解与网络设备 (`network`)、块设备 (`block`)、CPU 寄存器 (`registers`)、命令行历史 (`history`)、模拟 PCI 设备 (`pci`)、虚拟 USB 总线上的设备 (`usb`) 以及 USB 主机设备 (`usbhost`) 相关的 VLAN 信息。你还可以查看 QEMU 版本号 (`version`)。
- `- screendump file.ppm`—将目标系统的显示（换句话说，就是你输入 Ctrl+Alt+1 时看到的内容）捕获到当前目录下的 pnm 文件。将 `file.ppm` 替换为你想要使用的名称。
- `- eject`—弹出与指定设备关联的介质。例如，将 `device` 替换为 `cdrom` 以弹出从你的 CD 驱动器运行的现场 Linux，或替换为 `fd` 以弹出你的软盘。
- `- savevm`—将整个虚拟机状态保存到文件。
- `- loadvm file`—从文件恢复整个虚拟机状态。
- `- quit`—关闭现场 CD 并退出 QEMU。

QEMU 监视器还提供其他命令。要了解其他命令，请参考 QEMU 页面 (`man qemu`) 或 QEMU CPU 模拟器用户文档 (`http://fabricrice.bellard.free.fr/qemu/qemu-doc.html`)。

# 在 Windows 中使用 QEMU

假设你有一个完成或下载好的现场 CD 镜像，并希望从运行的 Windows 系统中启动它。关于你的硬盘，QEMU 网站引用了一个 Windows 页面（`http://www.dion.ne.jp/~qemu-win`），你可以在那里下载一个包含 QEMU linux-test 软件包中 Small Linux 的二进制文件。

我使用了以下步骤将 QEMU 下载到 Windows，以便我从 Windows 桌面启动 Linux 现场 CD。我是在带有互联网连接的 Windows XP 上执行此步骤：

1. 使用 Windows 上的浏览器（或其他下载工具）从 `http://www.dion.ne.jp/~qemu-win` 下载 `qemu-windows.zip` 文件。（当我访问该网站时，该文件名为 `qemu-0.8.2-windows.zip`）。
2. 右键点击 qemu zip 包并选择“提取 (Extract)”。
3. 提示时，选择一个文件夹存储提取出的 qemu。
4. 将 ISO 文件保存到 Windows 系统上可访问的文件夹中。我将其保存在保存 qemu 文件夹的父目录中。
5. 运行 qemu 命令启动现场 CD。在我的示例中，我打开了一个命令提示符 (DOS) 窗口并进入提取 qemu 的目录。然后我运行了以下命令，从当前目录的父目录启动 Small Linux：

```
qemu.exe -L -boot d -cdrom dsl-3.0.iso
```
