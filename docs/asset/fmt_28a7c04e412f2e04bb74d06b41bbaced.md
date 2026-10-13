
你必须执行的第一件事是在系统中安装最新版本的 `AlphaBIOS`。这可以通过 Digital 的“System Software and Driver Updates”网页获取：

`http://www.digital.com/support/syst.htp` 下载 `ZIP` 文件，解压并安装：

- 将文件拷贝到 `FAT` 格式的软盘
- 启动系统并插入软盘。在启动界面，按 `F2` 进入设置模式
- 选择 `"Upgrade AlphaBIOS"`
- 按照屏幕指示操作

一旦你的 `AlphaBIOS` 达到最新修订版本，就可以按照以下步骤引导系统：

- 创建一个包含以下文件的 `FAT` 格式软盘：
  - `linload.exe`（来自此目录）
  - `milo`（适用于你系统的版本）
- 启动系统并插入软盘。在启动界面，按 `F2` 进入设置模式
- 选择 `"Utilities->OS Selection Setup..."`
- 按 `INSERT` 添加一个新的操作系统选择
- 对于 `"Boot Name"`，输入类似 `"Linux"` 的内容。按 `TAB` 跳到下一个字段。
- 按方向键直到 `"Boot File"` 选择为 `"A:"`。`TAB` 跳到下一个字段
- 输入 `"linload.exe"`。按两次 `TAB`（即跳过 `OS Path load device` - 它无关）
- 输入 `"\` 作为 `OS Path load file`
- 按 `ENTER` 添加选择。

此时，`AlphaBIOS` 可能会弹出一个巨大的不友好的对话框，显示“Warning: Operating System Selection not valid!”。忽略此错误（这对 `NT` 没有问题）并按 `ENTER` 继续。

- 按 `F10` 保存你做的更改；按 `ENTER` 确认更改
- 按两次 `ESC` 返回启动界面。

* 使用上下方向键选择您刚刚添加的启动项，并按 `ENTER` 键启动它。

* `AlphaBIOS` 将加载 `linload`，随后它将加载 `MILO`。当您看到 `MILO` 提示符时，请按照正常基于 `ARC` 的系统安装方法进行。

如果您将第一个硬盘的首个分区分配了一个较小的 `FAT` 分区用于启动（安装程序建议您这样做），那么一旦安装完成后，您应该将 `linload.exe` 和 `mimo` 拷贝到此分区。关机后，您可以如下修改 Linux 菜单选择，从此分区加载 `MILO`：

* 在启动屏幕上，选择 `F2` 进入设置模式。
* 选择 `"Utilities->OS Selection setup"`
* 标亮 `Linux` 条目，然后按 `F6` 进行编辑。
* 按 `TAB` 键到 `"Boot File"` 行的设备部分。使用上下方向键选择存放 `linload` 和 `mimo` 的硬盘分区（通常为 `"Disk 0 Partition 1"` 或 `"Disk 1 Partition 1"`）。按 `ENTER` 键确认选择。
* 如果您在 `MILO` 加载后自动启动 `Linux`，则按 `TAB` 键到 `"OS Options"` 行并输入启动系统的 `MILO` 命令，例如 `"boot sda2:vlinux.gz"`。按 `ENTER` 键确认选择。
* 按 `F10` 保存更改。按 `ENTER` 键确认。

完成这些操作后，在基于 `AlphaBIOS` 的系统上启动并运行 `Linux` 与在 `ARC` 系统上操作非常相似。

### E.5.3 从评估板调试显示器加载 MILO

评估板（以及通常从其克隆的设计）包含了对 `Alpha` 评估板调试显示器的支持。在考虑此方法加载 `MILO` 之前，请查阅您的系统文档。以下系统*已知包含*调试显示器支持：

* `AlphaPC64` (节 `E.5.7`)
* `EB64+` (节 `E.5.7`)
* `EB66+` (节 `E.5.7`)
* `EB164` (节 `E.5.7`)
* `PC164` (节 `E.5.7`)

在考虑此方法之前，您应该注意，早期版本的评估板调试显示器不包含视频或键盘驱动程序，因此您必须准备好通过串口连接另一个系统，以便使用调试显示器。它的界面非常简单，输入 `help` 会显示大量命令。其中最感兴趣的命令通常包含 `boot` 或 `load` 单词。

评估调试显示器可以通过网络 (`netboot`) 或软盘 (`floboot`) 加载镜像。无论何种情况，在启动镜像之前，将启动地址设置为 `0x200000` (> `bootaddr 200000`)。

如果镜像在软盘上（请注意仅支持 `DOS` 格式的软盘），您将需要输入以下命令：

```
AlphaPC64 flboot <MILO-image-name>
```

### E.5.4 从故障安全启动块软盘加载 MILO

只有 `AxpPCI33` 已知包含故障安全启动块软盘支持（节 `E.5.7`）。

如果您没有标准的预制 `MILO.dd` 镜像，那么您可能需要构建一个 `SRM` 启动块软盘。一旦构建了 `MILO`，您需要在 `Digital Unix` 上执行以下操作：

```
fdisk -fmt /dev/rfd0a
cat bootm > /dev/rfd0a
disklabel -rw rfd0a 'rx23' reboot bootm
```

或者在 `Linux` 机器上：

```
cat bootm bootm > /dev/fd0
```

如果您有标准的 `MILO` 镜像（例如 `MILO.dd`），则您可以使用以下命令创建启动块软盘：

```
dd if=MILO.dd of=/dev/fd0
```

### E.5.5 从 Flash 加载 MILO

许多系统可以将 `MILO` 烧入 `Flash` 并直接启动（而不是通过 `ARC` 固件）：

* `AlphaPC64` (节 `E.5.7`)
* `Noname` (节 `E.5.7`)
* `EB66+` (节 `E.5.7`)
* `EB164` (节 `E.5.7`)
* `PC164` (节 `E.5.7`)

### E.5.6 从 SRM 控制台加载 MILO

`SRM`（系统参考手册）控制台并不了解文件系统或磁盘分区，它仅期望二级引导程序占据从给定偏移量开始的连续磁盘范围。描述二级引导程序的信息（其大小和偏移量）位于第一个 `512` 字节块中。为了加载 `MILO`，`SRM` 必须在其可以访问的设备（如软盘）上生成该结构。这就是 `mboot`；`mboot` 是第一个块，而 `bootm` 是对齐到 `512` 字节边界的 `MILO` 镜像。

从启动块设备加载 `MILO`，使用以下命令将 `mboot` 和 `bootm` 推送到启动设备：

```
$ mboot bootm > /dev/fd0
```

或者，从网站获取适当的 `MILO.dd` 并使用 `RAWWRITE.EXE` 或 `dd` 将其写入启动设备。

## E.5 如何加载 MILO

完成这些操作后，在基于 `AlphaBIOS` 的系统上启动并运行 `Linux` 与在 `ARC` 系统上操作非常相似。

## EB66+

`EB66+` 与 `Digital` 构建的所有 `Alpha` 评估板（`Alpha Evaluation Boards`）一样，包含评估板调试监控器（`Evaluation Board Debug Monitor`），因此可以使用它加载 `MILO`（章节 `E5.3`）。经常（尽管并非总是）设计源自这些板卡也包含调试监控器。通常，这些板卡包含 `Windows NT ARC` 固件（章节 `E5.1`）。提供一个可以在 `MILO` 中运行的闪存管理程序，这样一旦 `MILO` 运行，就可以将其烧入闪存（章节 `E.7`）。该系统支持 `MILO` 环境变量。

这些系统在闪存中有若干个由跳线控制的启动镜像。两个跳线是 `J18` 和 `J16`，位于板卡底部的中间位置（当将其插入闪存槽时，`Alpha` 芯片位于顶部）。您使用跳线组合以及存储在 `TOY` 时钟 `NVRAM` 中的启动选项来选择启动选项（以及在插入闪存槽时选择 `MILO`）。

`J18` 的 `7-8` 跳线意味着启动启动选项描述的镜像。`J16` 的 `7-8` 跳线意味着启动评估板调试监控器。

通过评估板调试监控器将镜像烧入闪存的步骤与 `AlphaPC64` 完全相同（章节 `E5.7`）。

## EB64+/Aspen Alpine

该系统与 `AlphaPC64` 非常相似，不同之处在于不包含 `MILO` 可以加载的闪存。`EB64+` 有两个 `ROM`，其中一个包含 `Windows NT ARC` 固件（章节 `E5.1`），另一个包含评估板调试监控器（章节 `E5.3`）。

`Aspen Alpine` 略有不同，因为它只有一个 `ROM`；其中包含 `Windows NT ARC` 固件。

## 通用桌面箱 (Multitia)

这是一个非常紧凑的基于 `21066` 的预封装系统，包含一个 `TGA (21030)` 图形设备。虽然您可以在箱内放入一张半高 `PCI` 显卡，但最好等待 `XFree86` 对 `TGA` 的完全支持。它包含 `Windows NT ARC` 固件，因此该启动是首选方法（章节 `E5.1`）。

## E.5 加载 MILO

### EB164
