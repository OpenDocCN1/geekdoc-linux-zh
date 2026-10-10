

`*dkms*` 包已安装（可通过 `dpkg -l *dkms* | grep -ii` 进行检查）。其他包通常是不需要的（除非你知道自己为什么需要它们！）。

## 9.3. 构建自定义 Kali Live ISO 镜像

Kali Linux 开箱即具备强大的功能和高度的灵活性。安装 Kali 后，只需稍加指导、发挥创造力、保持耐心并多加练习，你就能完成各种令人惊叹的操作。此外，你还可以自定义 Kali 构建，使其包含特定的文件或包（以提升或降低性能和功能），并能自动执行某些功能。例如，Kali ISO of Doom⁵ 和 Kali Evil Wireless Access Point⁶ 都是依赖于 Kali Linux 自定义实现的优秀项目。让我们来看看制作自定义 Kali Linux ISO 镜像的过程。

官方的 Kali ISO 镜像是使用 live-build⁷ 构建的，这是一组脚本，允许完全自动化和自定义 ISO 镜像创建的所有方面。live-build 套件使用整个目录结构作为其配置的输入。我们将此配置和一些相关的辅助脚本存储在一个 live-build-config Git 仓库中。我们将以这个仓库为基础来构建自定义镜像。

在继续之前，你必须知道本节中显示的命令旨在在最新的 Kali Linux 系统上运行。如果在非 Kali 系统上运行或系统已过时，它们很可能会失败。

### 9.3.1. 安装先决条件

第一步是安装所需的包并获取包含 Kali *live-build* 配置的 Git 仓库：

```bash
# apt install curl git live-build
[...]
# git clone git://git.kali.org/live-build-config.git
[...]
# cd live-build-config
# ls
auto build_all.sh build.sh kali-config README
```

此时，你只需运行 `./build.sh -verbose` 即可创建一个已更新（但未修改）的 Kali ISO 镜像。构建过程需要较长时间才能完成，因为它将下载所有需要包含的包。完成后，你会在 `images` 目录中找到新的 ISO 镜像。

### 9.3.2. 使用不同的桌面环境构建 Live 镜像

我们提供的 `build.sh` live-build 封装器负责设置 live-build 期望找到的配置目录。它可以根据其 `--variant` 选项设置不同的配置。

该封装器通过将 `kali-config/common` 和 `kali-config/variant-X` 中的文件结合起来创建配置目录，其中 X 是通过 `--variant` 参数给出的变体名称。当未显式给出该选项时，它使用 `default` 作为变体名称。

`kali-config` 目录包含用于最常见桌面环境的目录：

- `e17` 对应 Enlightenment；
- `gnome` 对应 GNOME；
- `i3wm` 对应相应的窗口管理器；
- `kde` 对应 KDE；
- `lxde` 对应 LXDE；
- `mate` 对应 Mate 桌面环境；
- `xfce` 对应 XFCE。

`light` 变体有些特殊；它基于 XFCE，用于生成官方的“light” ISO 镜像，这些镜像包含精简的应用程序集。

你可以使用以下单个命令轻松创建一个使用 KDE 作为桌面环境的 Kali 实时镜像：

```bash
# ./build.sh --variant kde --verbose
```

这种变体概念允许一些高级的预定义自定义，但如果你花点时间阅读 [Debian Live System 手册](http://www.debian.org/doc/current-manuals/debian-live-system-manual/)⁶，你会发现许多其他通过更改 `kali-config` 相应子目录的内容来自定义镜像的方式。以下部分将提供一些示例。

### 9.3.3. 更改已安装包的集合

启动后，live-build 会安装 `package-lists/*.list.chroot` 文件中列出的所有包。我们提供的默认配置包含一个 `package-lists/kali.list.chroot` 文件，该文件列出了 `kali-linux-full`（主要的元包，拉取所有需要包含的 Kali 包）。你可以注释掉此包并放入另一个你选择的元包，或者包含一组精确的其他包。你还可以通过结合两种方法来实现：从元包开始，然后添加你选择的补充包。

使用*包列表*，你只能包含已在官方 Kali 仓库中可用的包。但如果你有自定义包，可以通过将 `.deb` 文件放入 `packages.chroot` 目录（例如，如果你构建 GNOME 变体，则是 `kali-config/config-gnome/packages.chroot`）来将它们包含在实时镜像中。

元包是空包，其唯一目的是依赖于许多其他包。它们使得安装你通常希望一起安装的包集合变得更加容易。`Kali-meta` 源代码包构建 Kali Linux 提供的所有元包：

- **kali-linux**：基础系统（被所有其他元包拉取）
- **kali-linux-full**：默认的 Kali Linux 安装
- **kali-linux-all**：所有元包和其他包的元包（几乎包含 Kali 提供的所有内容，因此真的很大！）
- **kali-linux-sdr**：软件定义无线电（SDR）工具
- **kali-linux-gpu**：由 GPU 驱动的工具（利用你的图形卡可用计算力的工具）
- **kali-linux-wireless**：无线评估和分析工具
- **kali-linux-web**：Web 应用程序评估工具
- **kali-linux-forensic**：取证工具（查找发生了什么事件的证据）
- **kali-linux-voip**：VoIP（网络语音传输）工具
- **kali-linux-pwtools**：密码破解工具
- **kali-linux-top10**：十大最受欢迎的工具
- **kali-linux-rfid**：RFID 工具

在创建 `live-build` 的自定义包列表时，你可以利用这些元包。可用元包的完整列表及其包含的工具可以在 `http://tools.kali.org/kali-metapackages` 找到。

| | |
| :--- | :--- |
| **已安装包的 Debian 引导** | 你可以提供 Debian 预置文件（有关解释，请参阅第 4.3.2 节，“创建预置文件” [第 93 页]）作为 `preseed/*.cfg` 文件。它们将用于配置实时文件系统中安装的包。 |

### 9.3.4. 使用钩子调整镜像内容

`live-build` 提供了可在构建过程的不同步骤中执行的钩子。Chroot 钩子是作为 `hooks/live/*.chroot` 文件安装在你的配置树中的可执行脚本，并在 chroot 内执行。虽然 chroot 是让你临时更改操作系统根目录到你选择的目录的命令，但它也被引申用来指代托管完整（替代）文件系统树的目录。在这里使用 live-build 时也是如此，chroot 目录是正在准备实时文件系统的目录。由于在 chroot 中启动的应用程序无法看到该目录之外的内容，因此对于 chroot 钩子也是如此：你只能使用和修改在该 chroot 环境中可用的任何内容。我们依赖这些钩子来执行多个 Kali 特定的自定义（参见 `kali-config/common/hooks/live/kali-hacks.chroot`）。

二进制钩子（`hooks/live/*.binary`）在过程的末尾执行，且在构建过程的上下文中（不在任何 chroot 中）。你可以修改构建的 ISO 镜像的内容，但不能修改实时文件系统，因为此时它已经生成完毕。我们在 Kali 中使用此功能来对 `live-build` 生成的默认 isolinux 配置进行一些更改。例如，参见 `kali-config/common/hooks/live/persistence.binary`，我们在其中添加了启用持久性的启动菜单项。

### 9.3.5. 在 ISO 镜像或实时文件系统中添加文件

另一个非常常见的自定义是在实时文件系统或 ISO 镜像中添加文件。

你可以通过将文件放在 `includes.chroot` 配置目录下的预期位置来向实时文件系统添加文件。例如，我们提供 `kali-config/common/includes.chroot/usr/lib/live/config/0031-root-password`，它最终成为实时文件系统中的 `/usr/lib/live/config/0031-root-password`。

**Live-Boot 钩子**

安装为 `/lib/live/config/XXXX-name` 的脚本由 live-boot 包的 init 脚本执行。它们重新配置系统的许多方面，使其适合实时系统。你可以添加自己的脚本来在运行时自定义你的实时系统：例如，这被用来实现自定义启动参数。

你可以通过将文件放在 `includes.binary` 配置目录下的预期位置来向 ISO 镜像添加文件。例如，我们提供 `kali-config/common/includes.binary/isolinux/splash.png` 以覆盖 Isolinux 引导加载程序使用的背景图像（该图像存储在 ISO 镜像文件系统的 `/isolinux/splash.png` 中）。

## 9.4. 使用 USB 键为 Live ISO 添加持久性

### 9.4.1. 持久性功能：解释

接下来，我们将讨论为 Kali USB 键添加持久性所需的步骤。实时系统的本质是短暂的。存储在实时系统上的所有数据以及所做的所有更改在重启时都会丢失。为了解决这个问题，你可以使用 `live-boot` 的一个称为持久性的功能，当启动参数包含 `persistence` 关键字时启用。

