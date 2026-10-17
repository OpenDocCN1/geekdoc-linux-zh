
## /etc/init 中的 Plymouth 文件

Plymouth 是 Red Hat 图形启动（RHGB）系统的即插即用替代品。虽然 `rhgb` 指令仍在标准 GRUB 配置文件中使用，但 RHGB 相关软件包在 RHEL 6 中未使用。`rhgb` 指令现在启动 Plymouth 闪屏。三个相关文件通常存储在 `/etc/init` 目录中，与 GUI 停止时发生的情况相关：

- `plymouth-shutdown.conf` runs Plymouth splash screens as the system transitions from runlevel 5 to another runlevel.
- `splash-manager.conf` includes an appropriate message in the Plymouth splash screens when the system moves to runlevels 0 (halt) or 6 (reboot).
- `quit-plymouth.conf` quits the Plymouth service at the end of the boot process.

## /etc/init 中的预读文件

`readahead` 系统在启动过程中将关键文件中的信息移入 RAM，以便在需要时加快访问。收集的文件部分由 `/etc/sysconfig/readahead` 文件定义。三个相关文件通常存储在 `/etc/init` 目录中，与启动过程中发生的情况相关：

- `readahead-collector.conf` uses the settings in `/etc/sysconfig/readahead`.
- `readahead-disable-services.conf` disables those services that can be trouble for readahead services; the only one disabled by default is the `audit` daemon associated with SELinux.
- `readahead.conf` actually starts the readahead process, assuming sufficient RAM is available.

## /etc/init 中的终端文件

Linux 系统可以拥有串行和基于图形的终端。它们至少最初由 `/etc/init` 目录中的几个文件配置。`prefdm.conf` 文件在运行级别 5 中配置，并使用 `respawn` 命令设置。换句话说，如果 X 服务器崩溃，例如使用 CTRL-ALT-BACKSPACE 键组合，`respawn` 命令会重新启动 GUI 登录屏幕，如 `/etc/X11/prefdm` 文件中定义的那样。四个相关文件通常存储在 `/etc/init` 目录中，控制终端在启动过程中如何以及在哪里启动。

- `prefdm.conf` starts and maintains the noted GUI login screen in runlevel 5.
- `start-ttys.conf` starts all terminals. Note how the `X_TTY` environment variable starts the GUI in the first virtual terminal. Pay attention to the `ACTIVE_CONSOLES` directive in the `/etc/sysconfig/init` file. Which one determines what virtual terminals get started?
- `tty.conf` refers to a "getty," which is another name for the standard command line terminal. Note how it is disabled in runlevels 0, 1, and 6, which corresponds to the halt, single-user, and reboot runlevels.
- `serial.conf` is used when there's a remote connection over a serial port.

## 资源控制

在 Linux 中，资源控制与运行级别相关。不同的脚本可能在不同的运行级别中运行；例如，如果默认运行级别是 3，则其中一个文件确保 `/etc/rc3.d` 目录中的脚本在启动过程中执行。

基于 `/etc/inittab` 中定义的默认运行级别，四个相关文件通常存储在 `/etc/init` 目录中：

- `rcS.conf` runs the `/etc/rc.d/rc.sysinit` script only during the boot process.
- `rcS-sulogin.conf` starts the use of a terminal in single-user mode, and then moves to the standard runlevel
- `rc.conf` executes the scripts in the runlevel; it can be defined in `/etc/inittab` or the `init/telinit` commands. The executed scripts are in the `/etc/rcn.d/` directory, where `n` is the runlevel.

## 终端和登录屏幕

Linux 中的登录终端是虚拟控制台。大多数 Linux 系统，包括 RHEL 6，都配置了六个标准命令行虚拟控制台。这些控制台编号为 1 到 6。当配置了 GUI 和登录管理器时，其他 Linux 发行版包括第七个虚拟控制台，具有图形登录屏幕。这就是 RHEL 6 有点不同之处之一，因为在大多数情况下，它用图形登录屏幕替代第一个虚拟控制台。这仅适用于图形登录屏幕。如果你使用 `startx` 命令启动 GUI，则 GUI 在第七个虚拟控制台中运行。

这意味着什么？在 Linux 中，你可以使用 ALT-功能键组合在虚拟控制台之间切换。例如，ALT+F2 会带你到第二个虚拟控制台。你可以通过按 ALT-右箭头 或 ALT-左箭头 在相邻虚拟控制台之间切换。例如，要从虚拟控制台 2 移动到虚拟控制台 3，按 ALT-右箭头。如果你在 GUI 虚拟控制台中，请加上 CTRL 键。因此，在 RHEL 6 中，如果已安装 GUI 且你在第一个虚拟控制台中，你必须按 CTRL-ALT+F2 才能进入第二个虚拟控制台。

当你登录到常规虚拟控制台时，Linux 会返回一个命令行 shell。默认 shell 在第 6 章所述的 `/etc/passwd` 文件中定义。当你登录到 GUI 虚拟控制台时，Linux 会返回配置的 GUI 桌面。有关 Linux GUI 的更多信息，请参阅第 8 章。

直到 RHEL 5，虚拟控制台都在 `/etc/inittab` 中配置。现在 Upstart 已取代 SysVinit，虚拟控制台在 `/etc/sysconfig/init` 和 `/etc/init` 目录中的文件中配置，如本章前面所述。

虚拟控制台真正体现了 Linux 的多用户能力。在工作中（或在 Red Hat 考试期间），你可能在一个控制台上查看 `man` 手册，在另一个控制台上编译程序，在第三个虚拟控制台上编辑配置文件。通过网络连接的其他用户也可以同时做同样的事情。

# 认证目标 5.04

## 通过运行级别控制服务

尽管如上所述已从 SysVinit 迁移到 Upstart，但 Linux 仍然聚焦于运行级别。服务的管理通过运行级别进行自定义。由于 Upstart 包含与 SysVinit 相同的功能命令，你仍然可以使用 `init` 和 `telinit` 等命令来控制当前的运行级别。

Linux 具有高度可定制性。因此，每个运行级别中启动的服务都可以进行自定义。当然，如果你愿意进一步操作，甚至脚本本身也可以被自定义。虽然有图形界面工具帮助自定义脚本，但从命令行界面进行自定义通常快得多。

## 按运行级别划分的功能

如前所述，每个运行级别的基本功能列在 `/etc/inittab` 文件中，如表 5-2 所示。但那些只是概括性的描述。实际功能由在每个运行级别执行的脚本决定。而且，这是高度可定制的。例如，虽然运行级别 4 在 RHEL 6 中通常不使用，但没有什么阻止你在该运行级别设置一组自定义的服务。根据 `/etc/init/rc.conf` 文件，启动过程中会执行以下命令：

```bash
exec /etc/rc.d/rc $RUNLEVEL
```

查看 `/etc/rc.d` 目录中的那个文件，即 `rc`。通过以下命令，它会查找与运行级别关联的目录：

```bash
[ -d /etc/rc$RUNLEVEL.d ] || exit 0
```
