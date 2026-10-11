
要禁用端口，使用 `setserial` 将其设置为 `none`。`/etc/serial.conf` 的格式看起来像是命令行上 `serial` 后每个端口的一行。如果你不使用 `autosave`，你可以手动编辑 `/etc/setserial.conf`。对于 2.15，Debian 发行版在启用 `autosave` 时安装系统，但 Redhat 6.0 仅有一个 `/usr/doc/setserial-2.15/rc`，你需要将其移动到 `/etc/init.d`。

**BUG**：截至 1999 年，由于问题，在使用 `AUTOSAVE` 时，通过 `setserial -G /dev/ttyS?` 其中 0, 1, 2... 显示的参数会被保存，但其他参数不会。这只会影响极少数参数未保存的用户。这被报告为一个错误，现在可能已经修复。

为了强制将 `setserial` 的当前设置保存到配置文件 `serial.conf` 而无需关机，请在关机时执行 `/etc/init.d/setserial`。该命令会保存当前配置，但串口仍然工作。在某些情况下，你可能安装了旧、新配置方法，但希望其中一个在启动时运行。标记为 ... 已经过时。

## B 部分：Linux Modem 解调指南

旧配置方法：在 2.15 1999 之前，没有 `/etc/serial.conf` 文件来配置 `setserial`。因此，你需要找到启动时运行 `setserial` 的文件并编辑它。如果它不存在，你需要创建一个或放置启动时运行的命令。如果当前使用了此类文件，它可能在 `/etc` 目录某处。Redhat <6.0 在 `/usr/doc/setserial` 中提供了它，尽管在使用之前你需要在 `/etc` 中找到它。你可以使用 `locate` 来查找此类文件。例如，你可以输入：`locate "*serial*"`。你在寻找名为 `rc.serial` 或 `setserial` Debian。如果提供了此类文件，它应该包含一些被注释的示例。通过取消这些注释并/或修改它们，你应该能够正确设置。确保你为 `setserial` 使用了有效的路径和有效的设备名称。你可以通过手动执行此文件以超级用户身份运行文件名来测试它是否工作。测试这个比反复重启以正确设置快得多。当然，你也可以通过命令行输入 `setserial` 命令进行测试。过去常用脚本 `/etc/rc.d/serial`。Debian 发行版使用了 `/etc/boot/0setserial`。另一个曾经使用过的文件是 `/etc/rc.d/rc.local`，但这不是一个好主意，因为可能不够早。据报道说，其他进程在 `rc.local` 运行之前可能会打开串口，导致通信失败。

默认情况下，`ttyS0` 和 `tty2` 共享 IRQ 4，而 `tty0` 和 `tty3` 共享 IRQ 3。除非满足以下条件，否则不允许共享串口中断：

- 使用内核 2.2 或更高版本；
- 已编译支持；
- 你的串口硬件支持它。

如果你只有两个串口，`ttyS0` 和 `ttyS1`，只要不存在针对不存在设备的 IRQ 共享冲突，你仍然没问题。如果你添加了内部调制解调器并保留了 `ttyS0` 和 `ttyS1`，那么你应该尝试找到一个空闲的 IRQ 并在串口或调制卡上设置它，然后使用 `setserial` 将其分配给设备驱动程序。如果 IRQ 5 未被声卡使用，这可能是你可以用于调制解调器的一个。要在硬件中设置 IRQ，你可能需要使用 `isapnp` 资源附录、PnP BIOS 或补丁 Linux 以使其 PnP。为了帮助你确定可能有的空闲 IRQ，输入 `man setserial` 并搜索例如：`IRQ 1`。

### 什么是 isapnp？

`isapnp` 是一个配置 ISA 总线上即插即用 PnP 设备的程序。它包含在一个名为 `isaptools` 的包中，并包含另一个程序 `pnpdump`，它可以找到你的 ISA PnP 设备并显示配置它们的选项格式，该格式可以添加到 PnP 配置文件：`/etc/isapnp.conf`。它也可以配合 `-dump` 选项使用以显示 `setserial` 的当前 IO 地址和 IRQ。`isapnp` 命令可能会被放入启动文件，以便在启动时运行，即使你的 BIOS 不支持 PnP。参见即插即用-HOWTO。

### 什么是 wvdial？

`wvdial` 会尝试找到带有调制解调器的串口。它还会为 `setserial` 创建配置。`wvdial` 用于使用 PPP 协议进行拨出。但不需要安装 PPP 即可使用 `wvdial`。这只会影响很少使用的串口。由于此命令行没有选项，但你必须给它一个文件名。例如，输入：`wvdial my_file`。

# 450

# 资源附录

调制解调器电话线连接了吗？你可能需要将电缆连接到真实的电话，以确保它可以产生拨号音。

现在，你需要选择一个通信拨号程序来拨出。拨号程序包括：`minicom`、`seyon` X-window 和 `kermit`。关于某些通信程序，请参阅“通信程序”。接下来将介绍两个示例：“使用 Minicom 拨出”和“使用 Kermit 拨出”。

## 使用 Minicom 拨出

`Minicom` 随大多数 Linux 发行版一起。要进行配置，你必须是 root 用户。输入 `type minicom -s` 进行配置。这会直接带你进入配置设置菜单。或者，你也可以直接运行 `minicom` 然后按 `^A` 查看底部的状态行。它会显示输入 `^A Z` 来获取帮助你已经输入了 `^A`，只需输入 `z` 即可。从帮助菜单进入配置 Configuration 菜单。

对于仅仅拨号出，大多数选项不需要设置。要进行配置，你必须提供几项基本项目：调制解调器所在的串口端口名称如 `/dev/tty2` 以及速度如 `115200`。这些在串口菜单中设置。进入并设置它们。还可以如果可能的话设置硬件流控 `RTS/CTS`。然后保存。在输入速度时，你应该会看到类似 `8N1` 的内容，你应该保持原样。它的意思是：8 位字节、无奇偶校验、每个字节后附加 1 个停止位。如果你找不到想要的速度，对于测试来说，较低的速度总是可以用的。完成后退出按 `<return>` 并使用菜单将配置保存为默认 `dfl`。你可能想再次使用 `minicom` 并重新开始，这样你现在就可以找到串口并初始化调制解调器，或者你也可以进入帮助让 `minicom` 初始化调制解调器。

现在你已经准备好拨号了。但首先，在第一次输入 `minicom` 后进入的主界面，通过输入 `AT` 然后按 `<enter>` 键来测试调制解调器。它应该显示 `OK`。如果没有报错，说明没有必要尝试拨号。

如果你收到了 `OK`，返回帮助并选择拨号目录。你可以编辑它并在目录中输入电话号码等，然后选择拨号 `dial` 进行拨号。或者，你也可以手动拨号选择 `manual` 然后在键盘上输入数字。如果不起，请仔细记录任何错误信息并尝试找出哪里出了问题。

## B 部分：Linux 调制解调器 HOWTO

## 使用 Kermit 拨出

你可以在 `<http://www.columbia.edu/kermit/>` 找到最新版本的 `kermit`。例如，假设你的调制调器位于 `tty3`，速度为 `115200 bps`。你应该这样操作：

```
linux# kermit
C-Kermit 6.0.192, 6 Sep 96, for Linux
Copyright (C) 1985, 1996,
Trustees of Columbia University in the City of New York.
Default file-transfer mode is BINARY
Type ? or HELP for help.
C-Kermit>set line /dev/tty3
C-Kermit>set carrier-watch off
C-Kermit>set speed 115200
/dev/tty3> Connecting to /dev/tty3, speed 115200.
The escape character is Ctrl-\ (ASCII 28, 25)
type the escape character followed by C to get back,
or followed by ? to see other options.
ATE1Q0V1 ; 你输入这个然后按回车键
OK ; 调制调器应该响应这个
```

如果你的调制解调器对 AT 命令有响应，你可以假设调制解调器在 Linux 侧工作正常。现在尝试通过以下命令调用另一个调制调器：

```
ATDT765421
```

其中 `765421` 是电话号码。如果你有脉冲线路，使用 `ATDP` 代替 `ATDT`。如果通话通过，说明你的调制调器工作正常。要返回 `kermit` 提示符，按住 `Ctrl` 键，按下反斜键，然后松开 `Ctrl` 键，再按 `C` 键：

```
Ctrl-\C
(Back at linux)
kermit>quit
linux>
```
