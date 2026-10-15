
+   5. 删除包含 `hiddenmenu` 参数的行行。保存对 `grub.conf` 文件的更改，并关闭编辑器。
+   6. 重启你的电脑。
+   7. 当 GRUB 菜单显示时，按 `p`。系统会提示你输入用于保护 GRUB 的密码。输入密码以解锁更改 GRUB 参数的模式。
+   8. 你现在会看到 GRUB 菜单要求你按 `a`、`c`、`e` 来将更改应用于启动过程。在下一节中，你将学习更多关于你可以使用的有用启动选项。现在，按 `Enter` 继续正常的启动过程。

## 更改启动选项

在上一节中，你学习了如何从运行中的系统更改 GRUB 配置文件。有时，你的服务器可能无法正常启动，你需要进入 GRUB 提示符从那里更改 GRUB 参数。以下是一些常见原因：

- 你在 `grub.conf` 文件中犯了错误，导致服务器无法启动。
- 服务器启动过程中出现问题，你需要以维护模式启动。

如果你在启动服务器时遇到困难，有几个选项可以更改 GRUB 的加载方式。要使用这些选项，你需要在启动时进入 GRUB 菜单（见图 19.3）。启动时进入 GRUB 菜单的具体步骤取决于 GRUB 的配置。

- 如果使用了 `hidden` 选项，在电脑通电自检（POST）之后、操作系统开始加载之前按 `Escape` 键。
- 如果 GRUB 菜单受密码保护，按 `p` 并输入 GRUB 密码以解锁编辑功能。
- 从 GRUB 菜单进入，如果你只想更改内核的启动参数，请按 `a`。这非常有用，例如，如果你不想进入默认的运行级别 5，而是想进入另一个运行级别，如运行级别 3。

## 使用 GRUB 配置启动

- 从 GRUB 菜单进入，按 `e` 编辑来自配置文件的行。如果你知道 GRUB 配置文件中某处有错误，这非常有用。
- 按 `c` 打开 GRUB 命令行。这是最困难的选项，但也是你可以使用的强大的选项。它在手动输入 GRUB 参数以对服务器进行手动启动时非常有帮助。

### GRUB 19.3 更改 GRUB 启动选项

```
GNU GRUB version 0.97 (672K lower / 1048576K memory)

Red Hat Enterprise Linux (2.6.32-220.el6.x86_64)

Use the +/- arrow keys to select which entry is highlighted.

Press enter to boot the selected OS, 'e' to edit the

commands before booting, 'a' to modify the kernel arguments

before booting, or 'c' for a command line.
```

修改 GRUB 参数最通用的方法是从 GRUB 提示符进入编辑模式。要这样做，首先选择你想要修改的 GRUB 菜单项，然后按 `e`。这将显示图 19.4 所示的编辑菜单。

在编辑菜单中，你首先选择想要更改的行，然后按 `e` 以编辑模式打开此行。默认情况下，编辑器在行末尾打开。你可以使用方向键移动到需要更改的位置。也可以使用类似 Bash 的快捷键，如 `Ctrl+a` 跳到行首，或 `Ctrl+e` 跳到行尾。`Tab` 键补全同样有效。接下来应用你想做的更改，并按 `Enter`（注意不是 `Escape`!）返回主编辑菜单。从那里，你可以按 `b` 启动你的服务器。在练习 19.2 中，你将学习如何使用替代选项启动。

你在 GRUB 编辑器界面更改的任何内容都不是永久的。在通过 GRUB 菜单应用 GRUB 更改启动服务器后，别忘了也将修改应用到 `grub.conf` 文件中！

从图 19.4 所示的主编辑菜单中，还有其他可用选项。其中一些包括 `d` 删除一行、`o` 打开一行，或 `Escape` 返回主 GRUB 菜单，如图 19.3 所示。

512 第 19 章 • 理解和排除启动过程的故障

## 图 19.4 编辑 GRUB 选项

```
GNU GRUB version 0.97 (672K lower / 1048576K memory)

Red Hat Enterprise Linux (2.6.32-220.el6.x86_64)

Use the +/- arrow keys to select which entry is highlighted.

Press enter to boot the selected OS, 'e' to edit the

commands before booting, 'a' to modify the kernel arguments

before booting, or 'c' for a command line.
```

### 练习 19.2 使用替代选项启动

在本次练习中，你将学习使用替代选项启动。这在 `grub.conf` 文件损坏时非常有用。

- 1. 重启电脑；当 GRUB 菜单显示时，按 `p` 输入密码。输入密码后，按 `c` 打开 GRUB 壳。
- 2. 选择内核行并按 `e`。
- 3. 修改内核行以包含 `init=/bin/bash` 或进入单用户模式。
- 4. 按 `Enter` 启动系统。
- 5. 系统启动后检查并修复 `grub.conf` 文件。

## 使用 GRUB 命令行

在上一节中，你从界面更改了 GRUB。这对于修复 `grub.conf` 的小问题很方便。在其他情况下，问题可能严重得多。在这种情况下，知道也可以打开 GRUB 壳来手动输入一切是有用的。

要打开 GRUB 壳，在系统启动时显示 GRUB 菜单时按 `c`。对于运行中系统的 GRUB 维护，你也可以通过输入 `grub` 命令打开 GRUB 界面。

### 图 19.5 GRUB 壳界面

```
GNU GRUB version 0.97 (672K lower / 1048576K memory)

Minimal GRUB like line editing is supported. For the first word, TAB

lists possible command completions. Nowhere else TAB lists the

completions of a device/filename. ESC at any time exits.
```
