
在本章中，我将向你展示一些故障排除安装问题的方法。你将了解如何配置 X Window 系统以启动图形用户界面（GUI）屏幕以及如何配置打印机。

你可能还需要安装额外的软件包，因此本章将指导你如何安装不同格式的软件包，例如 Red Hat Package Manager（RPM）和 Debian 软件包——这是大多数 Linux 软件分发的两种格式。

## 使用文本模式安装

大多数 Linux 安装程序尝试使用 X Window 系统（X）显示图形安装屏幕。例如，如果安装程序无法检测到显卡，X 就不会启动。如果由于此或其他原因安装程序无法启动 X，你始终可以回退到文本模式安装。然后你可以手动指定显卡或稍后使用单独的配置程序配置 X。你也可以通过编辑其文本配置文件来配置 X。

表 3-1 列出了你如何进入文本模式安装屏幕。通常，文本模式安装序列与本迷你书第 2 章概述的图形安装相似。你响应提示并执行安装。

TABLE 3-1 Text Mode Installation in Some Linux Distributions

| Distribution | How to Get to the Text Mode Installer |
|---|---|
| Debian | 默认以文本模式运行。 |
| Fedora | 从 Fedora CD 或 DVD 启动电脑后，在 `boot:` 提示符下输入 `text`。 |
| Knoppix | 在 `boot:` 提示符下输入 `knoppix 2` 以文本模式启动 Knoppix（因为 Knoppix 是一个 Live 发行版，你无需安装它）。 |
| SUSE | 在第一个安装屏幕，按 F3，使用方向键选择文本模式选项，然后按 Enter。 |
| Ubuntu | 默认以文本模式运行。 |

## 故障排除 X

每次我在旧电脑上安装 Linux 时，GUI 安装在安装期间都运行良好，但在安装后第一次重新启动电脑时，图形登录屏幕却没有出现。相反，我得到的是文本登录屏幕或中间有一个小 X 的黑屏，或者启动过程似乎

卡在灰屏上。如果这个问题发生在你身上，以下是如何排查它：

- 1. 按 `Ctrl+Alt+Delete` 重新启动 PC。

电脑开始启动。你会看到一个屏幕，其中 `GRUB`（GRand Unified Bootloader）提示你选择要启动的操作系统。（如果发行版使用 `LILO` 作为引导加载程序，你会看到一个文本提示。）

- 2. 对于 `GRUB`，按 `A` 键添加一个选项，告诉 Linux 内核启动到提示符；对于 `LILO`，跳过此步骤。

`GRUB` 引导加载程序显示 Linux 内核的命令行并提示你添加想要的内容。

- 3. 对于 `GRUB`，输入一个空格后跟单词 `single` 并按 Enter；对于 `LILO`，输入 `linux single` 并按 Enter。

Linux 内核以单用户模式启动并显示一个以井号结束的提示符，如下所示：

```
#
```

现在你可以配置 X 了。

X 使用配置文件（根据发行版不同为 `XF86Config-4` 或 `xorg.conf`）来确定你的显示卡、显示器以及想要的屏幕分辨率类型。Linux 安装程序会准备配置文件，但有时配置不正确。

要快速创建一个可用的配置文件，请按照以下步骤操作：

- 1. 输入以下命令：

X 服务器运行并创建配置文件。屏幕变空白；然后 X 服务器在显示一些消息后退出。在 Fedora 中，消息的最后一行如下所示：

- 2. 使用 `vi` 等文本编辑器编辑 `/etc/xorg.conf.new` 文件，并在行 `Section "Files"` 之后插入以下行：

在 Fedora 中，你还必须将 `/dev/mouse` 改为 `/dev/input/mice`。

```
X -configure
```

```
To test the server, run 'X -config /etc/xorg.conf.new'
```

```
FontPath "unix/:7100"
```

- 3. 输入 `xfs &` 以启动 X 字体服务器。

- 4. 通过输入以下行来尝试新的配置文件：

```
X -config /etc/xorg.conf.new
```

如果你看到一个空白屏幕并带有 X 形光标，配置文件工作正常。

- 5. 按 `Ctrl+Alt+Backspace` 终止 X 服务器。

- 6. 使用以下命令将新配置文件复制到 `/etc/X11` 目录：

```
cp /etc/xorg.conf.new /etc/X11/xorg.conf
```

- 7. 通过按 `Ctrl+Alt+Delete` 或输入 `reboot` 重新启动 PC。

如果一切顺利，你应该会看到图形登录屏幕。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_58_0.png)

使用 X 服务器的 `-configure` 选项创建的 X 配置文件不会以最佳分辨率显示。要微调配置文件，你必须在重新启动系统后运行一个实用程序来调整显示设置。你使用的实用程序取决于 Linux 发行版，但大多数发行版都包含一个实用程序，可通过 GUI 配置显卡、显示器和显示设置。

## 解决其他安装问题

我确信我没有穷尽所有潜伏在外的安装问题。没有人能做到。Intel x86 PC 中存在如此多的组件，以至于墨菲定律几乎要求存在某种硬件组合，安装程序无法处理。在本节中，我列出了一些已知问题。对于其他问题，我建议你前往 Google 群组（https://groups.google.com）并输入故障的一些症状。假设其他人也遇到类似问题，你可以得到一些提示，了解如何排除你特定困境的故障。

## 使用 Knoppix 启动命令

Knoppix Live CD 可以成为一个很好的故障排除工具，因为 Knoppix 擅长检测硬件，并且可以直接从启动介质（CD/DVD/USB）运行。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_59_0.png)

如果你启动 Knoppix 时遇到问题，请尝试在 `boot:` 提示符下输入 Knoppix 启动命令。例如，如果 Knoppix 在尝试检测 SCSI 卡时似乎挂起，你可以通过在 `boot:` 提示符下输入 `knoppix noscsi` 来禁用 SCSI 探测。或者，如果你希望 X 服务器加载 *nv* 模块（用于基于 NVIDIA 芯片组的显卡），你可以在 `boot:` 提示符下输入 `knoppix xmodule=nv`。

表 3-2 列出了一些常用的 Knoppix 启动命令。

### 表 3-2 一些常用的 Knoppix 启动命令

| Boot Command | What It Does |
|---|---|
| expert | 以 *专家模式* 启动，可让用户交互式设置和配置 Knoppix。 |
| failsafe | 以安全模式启动，而不尝试检测硬件（除启动 Linux 所需的最低限度之外）。 |
| fb1280x1024 | 使用指定分辨率的固定帧缓冲图形。（指定你想要的分辨率，例如 1024 x 768 或 800 x 600。） |
| knoppix 1 | 在运行级别 1（单用户模式）下启动 Knoppix，可用于执行救援操作。 |
| knoppix 2 | 在运行级别 2 启动，仅提供文本模式 shell 提示符。 |
| knoppix acpi=off | 禁用 ACPI（高级配置和电源接口）。 |
| knoppix atapicd | 使用 ATAPI CD-ROM 接口，而不是为 IDE CD-ROM 驱动器模拟 SCSI 接口。 |
| knoppix desktop=wmname | 使用指定的窗口管理器代替默认的 KDE 桌面= *wmname*（其中 *wmname* 为 fluxbox、icewm、kde、larswm、twm、wmaker 或 xfce）。 |
| knoppix dma | 为所有 IDE 驱动器启用直接内存访问（DMA）。 |
| knoppix floppyconfig | 从软盘运行名为 knoppix.sh 的 shell 脚本。（shell 脚本包含你想要运行的 Linux 命令。） |
| knoppix fromhd=/dev/hda1 | 从指定硬盘分区中先前复制的 Live CD 映像启动。 |
| knoppix hsync=80 | 为 X 使用 80 kHz 水平刷新率。（输入你希望 X 使用的水平刷新率。） |
| knoppix lang=xx | 设置键盘语言，如两字母代码 xx 所指定（其中 xx 为 cn = 简体中文、de = 德语、da = 丹麦语、es = 西班牙语、fr = 法语、it = 意大利语、nl = 荷兰语、pl = 波兰语、ru = 俄语、sk = 斯洛伐克语、tr = 土耳其语、tw = 繁体中文 或 us = 美国英语）。 |

*(continued)*

### 表 3-2（续）

| Boot Command | What It Does |
