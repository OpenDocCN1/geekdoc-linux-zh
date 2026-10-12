
这里有一个活跃的用户论坛和许多用户贡献的扩展。`Ken Porter` 管理并与用户社区互动，以支持用户贡献扩展库。

`Damn Small Linux` 还有一个非常活跃的论坛，你可以在其中参与（`http://damnsmallinux.org/cri-bin/forums/ikonboard.cgi`）。如果你想支持该项目，`DSL` 有一个在线商店（`http://damnsmallinux.org/store`），你可以在那里购买 `CD` 或 `U` 盘版的 `DSL`，还可以购买 `Mini ITX` 系统。

## 选择 `U` 盘

为了从 `Damn Small Linux` 创建定制的 `Linux` 安装，我选择使用 `U` 盘作为介质有几个原因。首先是介质是可重写的，因此操作系统和数据都可以携带在同一个介质上。尺寸非常有吸引力（它们可以比打火机小），而且价格在最近几个月内大幅下降。（我花 50 美元买了一个 1GB 的 `U` 盘，它看起来运行良好。）

158 第三部分 — 家庭项目

在选择用于定制 `DSL` 的 `U` 盘时，有几点你需要知道：

- `U` 盘（`Pen drive`）只是固态 `USB` 存储设备的一种，其形状通常像一包口香糖。你可能还会听到人们称之为闪存盘（`flash drives`）、钥匙盘（`key drives`）、`USB sticks`、内存 `U` 盘（`memory thumb drives`）或类似的名称。它们还有不同的形状。
- `U` 盘的所有电源都来自它连接的 `USB` 端口。
- 因为 `U` 盘通常采用塑料外壳，它们可能会受到划痕或污垢的影响，就像 `CD`、`DVD` 和软盘一样。
- 可用的 `U` 盘版本有 1.0、1.1 和 2.0。1.0 和 1.1 版本的速度为 1.5 Mbit/s 或 12 Mbit/s。2.0 版本的速度可可 480 Mbit/s（尽管最高读取速度约为 100 Mbit/s）。
- `Linux` 将 `U` 盘视为大容量设备。

成本、便利性和可用性的结合使得 `U` 盘成为一种良好的介质。

# 制作 `Damn Small Linux`

除了安装创建 `Linux II` 项目的软件外，随书的 `CD` 还包含可启动的 `Damn Small Linux` 发行版。在 `U` 盘上创建定制 `Damn Small Linux` 的程序如下：

1. 将 `Linux II CD` 插入电脑的 `CD` 驱动器。正如我之前提到的，你也可以使用官方版的 `Damn Small Linux`（`dsl-1.3.1.iso` 在 `CD` 上可用）。
2. 重启你的电脑。出现 `DSL` 启动界面。

# 第 6 章 — 定制实时 `U` 驱动器 159

`Linux II CD`

将 `Damn Small Linux` 安装到 `U` 盘

从 `U` 盘启动 `Damn Small Linux`

- 添加自定义应用程序
- 配置系统设置
- 添加音乐、图像和文档
- 跨重启保存更改

一个可以启动 `Linux` 并包含你所有东西的酷 `U` 盘！

`图 6-1`： 在 `U` 盘上定制你的实时 `Linux`。

由于 `Linux II CD` 包含定制的 `Damn Linux`，它比 50MB 的 `DSL` 大。如果你在小型 `U` 盘上安装，或者不想要 `Linux II` 的定制功能，可以将 `DSL` 的原始 `ISO` 镜像刻录到 `CD` 并用它代替该项目。镜像位于 `Linux II CD` 的 `isos/ch06 damnsmall/1.3.1.iso`。关于如何刻录 `ISO` 镜像到 `CD`，请参见第 5 章。此外，当你读到这里时，将有更高版本的 `DSL`。因此你可以从 `www.damnsmallinux.org` 下载并刻录新的 `ISO` 镜像来执行此程序。

# 160 第三部分 — 本地项目

3. 按回车键启动 `Damn Small Linux`。如果你的 `PC` 配置为从 `CD` 启动（大多数电脑都是如此），`DSL` 将从 `CD` 启动，尝试检测你的硬件，启动桌面系统并连接到网络。（如果你的 `PC` 上有有线或无线网卡，且你的网络中有一个可用的 `DHCP` 服务器，`DSL` 应该会自动在线。）

如果你看到的是 `DSL` 启动界面，或者看到了启动界面但启动失败了，请参考“如果我无法启动 `Damn Small Linux`”侧栏。

`DSL` 配置为启动到图形化桌面（初始状态 5）。如果你看到了 `DSL` 桌面，你现在已经准备好配置你的 `DSL` 盘了。

## “如果我无法启动 `Damn Small Linux`？”

虽然 `Damn Small Linux` 在大多数 `PC` 上都能正常启动，但在某些情况下，你可能需要给它一点帮助。这里是一些你可以尝试的方法：

- `检查 BIOS`——如果过程完全跳过了你的 `CD`，请检查你 `PC` 的 `BIOS` 是否支持从 `CD` 启动。在电脑首次启动时进入 `Setup`，检查启动顺序，并确保 `CD` 在硬盘之前。
- `启动选项`——如果你看到了 `DSL` 启动提示，但启动失败了，尝试在提示处按 `F2` 或 `F3`。你将看到可用的启动选项。如果显示乱码，尝试 `dsl vga=normal`（最小 `VGA`）或 `dsl fb8006`（笔记本电脑或其他 `fb` 选项）。如果 `DSL` 无法检测某些设备，可以通过输入以下命令之一进入 `dsl` 来禁用它们：`nosci, popcmia, nousb, noaop, noswasp, noapic, nomce, 或 oddnoc`。使用 `dsl failsafe` 模式可以从 `CD` 启动且不损坏任何硬件。
- `启动软盘`——如果你完全无法从 `CD` 启动，可以从软盘开始启动过程。`DSL` 项目包含了 `bootfloppy.img` 和 `bootfloppy-img` 文件，你可以使用它们从软盘启动 `DSL`，然后分别从 `CD` 或 `USB` 驱动器继续启动过程。我将这些镜像放在 `Linux Toys II (isochch6-dammsall 目录)` 中，你也可以从 `damsmalllinux.org` 下载。因此，从任何 `Linux` 系统，只要当前目录下有 `bootfloppy` 且第一个软盘驱动器有一个空白软盘，输入以下命令将 `DSL` 软盘镜像拷贝到：

```
# dd if=/dev/fd0
```

如果你无法从 `U` 盘启动 `DSL`，可以使用相同的概念。要使用来自 `U` 盘的启动软盘，请将 `bootfloppy.img` 重命名为 `bootfloppy-usb.img` 以创建一个软盘。

如果你的电脑无法以图形显示启动 `Damn Small Linux`，你应该考虑在另一台电脑上运行该项目。虽然 `DSL` 可以以文本模式运行，但本章中的某些步骤将让你有一个可用的 `GUI`。

`![](img/1b8a24a162893627b8005ac678b79236_184_0.png)`

# 第 6 章 — 定制 `Live Linux` 驱动器 161

## 步骤 2：准备在 `U` 盘上安装 `DSL`

在开始在 `U` 盘上安装之前，请检查并确保：

- 你已准备好完全删除你的 `U` 盘。（如果 `U` 盘上有任何你想保留的内容，请进行备份。）
- 你的 `PC` 有一个与你的 `U` 盘匹配的 `USB` 端口（`DSL` 1.1 或 `USB` 2.0）。
- 驱动器未挂载。（你可以等到过程稍后再插入 `U` 盘，或者将其卸载，可能可以通过输入 `sudo mount /dev/sda` 或通过 `DSL` 面板中的 `mount.app` 工具进行卸载。）

`![](img/1b8a24a162893627b8005ac678b79236_185_0.png)`

要执行本章中的许多步骤，你需要 `root` 权限。像 `KNOPPIX` 一样，`DSL` 没有提供密码来获取 `root` 权限。但是，它会让你请求 `root` 权限。这里有几种获取 `root` 权限的方法：右键点击桌面，选择 `Xshells -> Root Access`（打开一个具有 `root` 权限的 `shell`）；使用 `sudo` 命令以 `root` 用户身份获取命令（如之前所示的 `sudo mount /dev/sda` 命令）。你还可以以超级用户身份运行 `elFM`，正如 `Robert Shinglelecker` 告诉我，未来的 `DSL` 将允许普通 `DSL` 用户自动拥有 `root` 权限（在较后版本的 `DSL` 中，你可能需要为本章获取 `root` 权限）。

在选择在 `U` 盘上安装 `DSL` 之前，考虑你将启动的电脑类型。以下是你的选择：

- `USB-ZIP` — 大多数支持从 `USB` 设备启动的 `PC` 都能启动 `USB-ZIP` 设备。但由于 `USB-ZIP` 是一个旧标准，它具有局限性。`USB` 驱动器上的分区必须符合特定的 `DSL` 大小规范。为了解决这个问题，`DSL` 的 `USB-ZIP U` 盘会小型分区，并将 `U` 盘的其余部分分配到单独的分区。在需要从许多不同的电脑启动的情况下，`USB-ZIP` 是你的最佳选择。
- `USB-HDD` — 较新的电脑可以使用 `USB-HDD` 启动样式启动 `U` 盘。然而，许多旧电脑没有 `USB-HDD` 启动选项。配置了 `USB-HDD` 的 `U` 盘在启动后可以访问，你可以从软盘或 `CD` 开始 `USB-HDD` 驱动器的进程，然后。

`![](img/1b8a24a162893627b8005ac678b79236_185_0.png)`
