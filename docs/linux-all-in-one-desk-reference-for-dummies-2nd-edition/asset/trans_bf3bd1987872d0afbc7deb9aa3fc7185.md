

## 使用文本模式安装

大多数 Linux 安装程序都会尝试使用 X Window System 来显示图形化安装界面。例如，如果安装程序未能检测到显卡，X 将无法启动。如果——出于这个原因或其他任何原因——安装程序无法启动 X，你始终可以退回到文本模式安装。这样，你可以手动指定显卡，或者稍后使用独立的配置程序来配置 X。你还可以通过编辑其文本配置文件来配置 X。

表 3-1 列出了如何从本书 DVD 中包含的 Linux 发行版的初始安装界面进入文本模式安装。通常，文本模式安装流程与本小册子第 2 章中我概述的图形安装流程相似。你只需响应提示并完成安装即可。

| 发行版 | 如何进入文本模式安装程序 |
| :--- | :--- |
| Debian | 支持文本模式 |
| Fedora Core | 从 Fedora Core CD 或 DVD 启动 PC 后，在 `boot:` 提示符处输入 **text** |
| Knoppix | 在 `boot:` 提示符处输入 **knoppix 2** 以文本模式启动 Knoppix（由于 Knoppix 是 Live CD 发行版，你无需安装它） |
| SUSE | 在第一个安装界面上，按 F3 并使用箭头键选择文本模式选项。按 Enter。 |
| Ubuntu | 基于 Debian 安装程序，支持 **text mode** |
| Xandros | 启动 CD 时按住 Shift 键并选择 Rescue Console。当出现 `bash-3.00#` 提示符时，输入 **quick_install** 并按照说明操作。 |

## 排查 X 故障

在我的一台较旧的 PC 上，每次安装 Linux 时我都会遇到这个问题：安装过程中，GUI 安装运行正常，但在安装后首次重启 PC 时，图形登录界面并未出现。相反，我最终得到了一个文本登录界面，或者启动过程似乎挂起并显示灰色屏幕。如果你遇到这个问题，以下是排查故障的方法：

1. 按 Ctrl+Alt+Delete 重启 PC。

PC 开始启动。你会看到一个 GRUB 引导加载程序提示你选择要启动的操作系统的界面。（如果该发行版使用 LILO 作为引导加载程序，你会看到一个文本提示符。）

2. 对于 GRUB，按 A 键为 Linux 内核添加一个选项。对于 LILO，跳过此步骤。

GRUB 引导加载程序随后显示 Linux 内核的命令行，并提示你添加所需内容。

3. 对于 GRUB，输入空格后跟单词 `single` 并按 Enter。对于 LILO，输入 `linux single` 并按 Enter。

Linux 内核以单用户模式启动，并显示如下类似的提示符：

```
sh-3.00#
```

现在你可以开始配置 X 了。

X 使用配置文件（根据你的发行版，该文件名为 `XF86Config-4` 或 `xorg.conf`）来确定显示卡类型、监视器以及你想要的屏幕分辨率。Linux 安装程序会准备配置文件，但有时配置并不正确。

要快速创建可用的配置文件，请遵循以下步骤：

1. 输入以下命令：

   ```
   X -configure
   ```

2. 使用文本编辑器（如 `vi`）编辑 `/etc/xorg.conf.new` 文件，并在 `Section "Files":` 行后插入以下行：

   ```
   FontPath "unix/:7100"
   ```

   在 Fedora Core 上，你还必须将 `/dev/mouse` 更改为 `/dev/input/mice`。

3. 输入 `xfs &` 以启动 X 字体服务器。

4. 在 Debian 和 MEPIS 上，通过输入 `X -xf86config /XF86Config.new` 来尝试新的配置文件。在 Fedora Core、SUSE、Ubuntu 和 Xandros 上，通过输入 `X -config /etc/xorg.conf.new` 来尝试新的配置文件。

5. 按 Ctrl+Alt+Backspace 终止 X 服务器。

6. 使用以下命令将新的配置文件复制到 `/etc/X11` 目录（在 Debian 和 MEPIS 上，将第一个文件名更改为 `XF86Config.new`，第二个更改为 `XF86Config-4`）：

   ```
   cp /etc/xorg.conf.new /etc/X11/xorg.conf
   ```

7. **按 Ctrl+Alt+Delete 或输入 `reboot` 重启 PC。**

如果一切顺利，你应该能看到图形登录界面。

![](img/792720823146d68f19fd50c99ebfce4b_108_0.png)
![](img/792720823146d68f19fd50c99ebfce4b_109_0.png)

使用 X 服务器的 `-configure` 选项创建的 X 配置文件并不会显示最佳可能的分辨率。要微调配置文件，你必须在重启系统后运行一个实用程序来调整显示设置。具体使用的实用程序取决于你的 Linux 发行版，但大多数发行版都包含一个允许你通过图形用户界面配置显卡、监视器和显示设置的实用程序。

## 解决其他安装问题

我确信我并没有穷尽所有潜伏在安装中的问题。没有人能做到。Intel x86 PC 中组件的组合方式如此之多，以至于墨菲定律几乎必然要求存在某种安装程序无法处理的硬件组合。本节列出了一些已知问题。对于其他问题，我建议你去 Google Groups（[http://groups.google.com](http://groups.google.com)）并输入一些故障症状。假设其他人也遇到类似的问题，你可以从中得到一些如何排查并走出特定困境的指示。

### 使用 Knoppix 启动命令

Knoppix Live CD 可以是一个出色的故障排查工具，因为 Knoppix 擅长检测硬件，并且你可以直接从 CD 运行它。当然，有时你可能在启动 Knoppix 本身时也会遇到问题。如果发生这种情况，你可以尝试在 `boot:` 提示符处输入 Knoppix 启动命令。例如，如果 Knoppix 似乎在尝试检测 SCSI 卡时挂起，你可以通过在 `boot:` 提示符处输入 `knoppix noscsi` 来禁用 SCSI 探测。或者，如果你希望 X 服务器加载 `nv` 模块（用于基于 NVIDIA 芯片组的显卡），你可以输入 `knoppix xmodule=nv` 在 `boot:` 提示符处。表 3-2 列出了一些常见的 Knoppix 启动命令。

**表 3-2 常见的 Knoppix 启动命令**

| 启动命令 | 作用 |
| :--- | :--- |
| `expert` | 以*专家模式*启动，允许用户交互式和配置 Knoppix |
| `failsafe` | 不尝试检测硬件即可启动（除了启动 Linux 所需的最基本条件） |
| `fb1280x1024` | 使用指定分辨率的固定帧缓冲图形（指定你需要的分辨率，如 1024 x 768、800 x 600 等） |
| `knoppix 1` | 以运行级别 1（单用户模式）启动 Knoppix，可用于执行救援操作 |
| `knoppix 2` | 以运行级别 2 启动，仅提供文本模式 shell 提示符 |
| `knoppix acpi=off` | 完全禁用 ACPI（高级配置和电源接口） |
| `knoppix atapicd` | 使用 ATAPI CD-ROM 接口，而不是为 IDE CD-ROM 驱动器模拟 SCSI 接口 |
| `knoppix desktop=wmname` | 使用指定的窗口管理器，而不是默认的 KDE（`wmname` 可以是：`fluxbox`、`icewm`、`kde`、`larwm`、`twm`、`wmaker` 或 `xfce`）。 |
| `knoppix dma` | 为所有 IDE 驱动器启用直接内存访问（DMA） |
| `knoppix floppyconfig` | 从软盘运行名为 `knoppix.sh` 的 shell 脚本（该 shell 脚本包含你希望运行的 Linux 命令。） |
| `knoppix fromhd=/dev/hda1` | 从位于指定硬盘分区中之前复制的 Live CD 镜像启动 |
| `knoppix hsync=80` | 为 X 使用 80 kHz 的水平刷新率（输入你希望 X 使用的水平刷新率） |
| `knoppix lang=xx` | 将键盘语言设置为由两位字母代码 `xx` 指定的语言（对于 `xx` 使用以下之一：`cn` = 简体中文、`de` = 德语、`da` = 丹麦语、`es` = 西班牙语、`fr` = 法语、`it` = 意大利语、`nl` = 荷兰语、`pl` = 波兰语、`ru` = 俄语、`sk` = 斯洛伐克语、`tr` = 土耳其语、`tw` = 繁体中文，或 `us` = 美式英语） |
| `knoppix mem=256M` | 指定 PC 具有说明中的内存量（以兆字节为单位） |
| `knoppix myconf=/dev/hda1` | 从 `/dev/hda1` 分区运行 shell 脚本 `knoppix.sh`（输入拥有 `knoppix.sh` 文件的分区名称。） |
| `knoppix myconf=scan` | 让 Knoppix 搜索名为 `knoppix.sh` 的文件并执行该文件中的命令（如果有） |
| `knoppix no eject` | 在你终止 Knoppix 后不会弹出 Live CD |
| `knoppix noprompt` | 在你终止 Knoppix 后不会提示移除 Live CD |
| `knoppix no wheelmouse` | 强制 PS/2 鼠标或触控板使用 PS/2 协议（而不是自动检测） |
| `knoppix no xxxx` | 让 Knoppix 跳过硬件检测的特定部分（其中 `xxxx` 标识了不应探测的硬件或服务器：`apic` = 高级可编程中断控制器、`apm` = 加速图形端口、`apm` = 高级电源管理、`audio` = 声卡、`d&c` = 显示数据通道、`dhcp` = 动态主机配置协议、`fstab` = 文件系统表、`firewire` = IEEE 1394 高速串行总线、`pcmcia` = PC 卡、`scsi` = 小型计算机系统接口、`swap` = 用于虚拟内存的硬盘空间、`usb` = 通用串行总线） |

