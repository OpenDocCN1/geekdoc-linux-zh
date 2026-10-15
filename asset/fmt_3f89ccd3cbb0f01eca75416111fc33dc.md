
patching file `linux/Documentation/SubmittingDrives...`

patching file `linux/net/unix/af_unix.c`

patching file `linux/net/wanrouter/wanmain.c`

patching file `linux/net/wanrouter/wanproc.c`

patching file `linux/net/x25/af_x25.c`

确切的文件列表随补丁而异，某些补丁比其他更改的文件更多。结果是内核源码树更新到了最新版本。

最后，执行以下两个命令以确保你工作的是原始源码树：

```bash
$ cd linux
$ make mrproper
```

```
make[1]: Entering directory "/home/linux/arch/i86/boot"
rm -f tools/build
rm -f setupselect zlimage compressed/mlinux.out
rm -f bsetupselect zlimage compressed/bmlinux.out
make[1]: Entering directory "/home/linux/arch/i86/boot"
rm -f tools/build
rm -f setupselect zlimage compressed/mlinux.out
rm -f bsetupselect zlimage compressed/bmlinux.out
make[1]: Leaving directory "/home/linux/arch/i86/boot"
make[2]: Leaving directory "/home/linux/arch/i86/boot"
```

`mrproper` 命令会移除之前编译留下的任何残留物。此时，你准备好：

## 定制内核

定制内核涉及两个步骤：选择如何包含支持，然后进行实际配置。

- 将支持直接编译到内核中。
- 根据需要使用模块。

在配置内核时，必须选择如何包含特定设备的支持。对于许多配置选项，你必须选择以下之一：

- 点击 `y` 将给定选项的支持编译到内核中或接受该配置选项。
- 点击 `m` 使用指定设备或选项的支持（并非所有配置项可用）。
- 点击 `n` 跳过对特定设备的支持或禁用该项。

例如，在 Code 级选项对话框中，如果你想启用实验性功能或不完整的设备驱动配置对话框，请点击 `y` 旁按钮。如果你不想看到这些对话框，请点击 `n` 按钮。注意在这种情况下，如果你选择了 `y` 然后点击 Main Menu（主菜单）返回主配置对话框，之前灰色的按钮（例如 IEEE 1394 (FireWire) 支持（实验性）和蓝牙支持按钮）现在可以使用。如果设备没有模块化设备驱动程序，你将看不到该选项。

Linux 支持的一些内容（如网络驱动程序、新硬件、网络协议等）尚未经过充分测试。在 Maturity（成熟）选项对话框中点击 `Y` 允许你选择和配置此类功能。点击 `N` 将禁用这些功能，且不会收到它们的提示。此选项还使得过时的驱动程序可用，这些驱动已被其他取代或计划在未来的内核发布中移除。除非你喜欢挑战极限或冒着系统崩溃的风险，否则你应该点击 `N`。

## 使用 MENUCONFIG 配置内核

要配置内核，点击对话框中的每个按钮并选择适合你需求的选项。稍等后，你将看到：

```bash
$ make menuconfig
```

`menuconfig` 命令为配置内核提供了一个基于文本的界面。它比 `makeconfig` 用户友好得多，因为它允许你使用方向键导航菜单。

一旦完成内核配置，选择 "Save"（保存）。将在内核源码根目录下创建一个 `.config` 文件。该文件随后可用于构建内核。

## 使用 CONFIG 配置内核

如果你更倾向于命令行界面，可以使用 `makeconfig` 命令。这将允许你手动编辑 `.config` 文件。

```bash
$ make config
```

`makeconfig` 命令会提示你设置的每个配置选项。这比 `menuconfig` 要耗费得多。

## 使用 XCONFIG 配置内核

如果你在图形环境中工作，可以使用 `xconfig` 命令。这将为内核配置提供一个图形界面。

```bash
$ make xconfig
```
