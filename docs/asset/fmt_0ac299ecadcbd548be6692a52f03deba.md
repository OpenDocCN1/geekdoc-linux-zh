
+ A. `sudo system-config-xserver`
+ B. `sudo dpkg-reconfigure xserver-xorg`
+ C. `sudo Xorg -configure`
+ D. `sudo Xorg`

+ 11. 标准的 X 服务器配置文件是什么（包括完整路径）？

+ 12. 运行 `Xorg -configure` 命令时，下列哪个文件包含输出？假设本地目录为 `/tmp`，日期为 2008 年 6 月 17 日。

+ A. `/tmp/xorg.conf`
+ B. `/etc/X11/xorg.conf`
+ C. `/tmp/xorg.conf.20080617103059`
+ D. `/tmp/xorg.conf.new`

# 426 第二二章：配置和本地化 GNOME

+ 13. 下列哪个命令可以为当前用户在本地系统配置基本字体设置？

A. `sudo fontconfig-fontconfig`
B. `sudo dpkg-reconfigure fontconfig-fontconfig`
C. `sudo font-properties`
D. `sudo gnome-appearance-properties`

+ 14. 下列哪些因素可能需要不同的字体配置？（两个答案正确。）

A. 从 CRT 系统升级到 LCD 显示器
B. 新版本的 OpenOffice.org Writer
C. 在本地系统中安装中文

+ 15. 下列哪个运行级别最适合运行 `Xorg -config` 命令？

A. 0
B. 1
C. 2
D. 6

## 实验问题

### 实验 I

本实验说明了与 X 服务器更简单的重新配置相关的选项。步骤应该比练习 11-1 中所示的更简单。无论如何，第一步都应该是备份当前的 X 服务器配置文件。此外，你应该知道如何在启动本地系统时从 GRUB 菜单访问“恢复模式”。要打开 GRUB 菜单，你需要在启动过程中按一个键。然后你可以选择“恢复模式”，这会将 Ubuntu Linux 启动到级别 1，从该句级你可以恢复原始的 X 服务器配置文件。

+ 1. 使用以下命令将当前的 X 服务器配置文件备份到你的家目录：

```
$ cp /etc/X11/xorg.conf ~
```

+ 2. 使用以下命令开始重新配置过程：

```
$ sudo dpkg-reconfigure -phigh xserver-xorg
```

3. 重新配置 X 服务器需要多少步？（一个大概数字即可）。文件保存在哪里？文件扩展名有意义吗？

4. 将结果保存到 `/etc/X11/xorg.conf` 配置文件。

5. 使用以下命令启动运行级别 1，这应该以 root 用户身份访问文本模式屏幕：

```
$ sudo init 1
```

6. 启动运行级别 2（这是默认级别），这也应该重启 X 服务器。如果新配置有效，应该出现 Ubuntu Linux 的常规 GUI 登录界面。

7. 如果没有出现 Ubuntu Linux 的常规 GUI 登录界面（即使出现了），也请恢复原始的 X 服务器配置文件。请按 CTRL-ALT-FI 访问命令行终端，并正常登录。然后你应该能够使用以下命令恢复原始的 X 服务器配置文件：

```
$ sudo cp ~/xorg.conf /etc/X11
```

如果你无法访问命令行终端，你可能需要重启本地系统并按照本实验介绍中的描述启动恢复模式。

8. 重复步骤 5 和 6。你应该能看到原始的 GUI 登录界面，带有原始的 X 服务器配置。

### 实验 2

在本实验中，你将使用低优先级重新配置字体。

+ 1. 使用以下命令开始重新配置过程：

```
$ dpkg-reconfigure -plow fontconfig-config
```

+ 2. 重新配置字体需要多少步？与没有 `-plow` 关的重新配置相比有什么区别？你能解释为什么吗？

# 428 第二二章：配置和本地化 GNOME

# 自测答案

## 配置桌面环境

+ 1. D. 你不想调用管理权限来使用 `gconf-editor` 编辑本地账户的设置。

`gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

2. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

3. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

4. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

5. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

6. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

7. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

8. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

9. B. `gconftool-2` 命令可以在命令行运行，不会打开任何 GConf 编辑器。`sudo gconf-editor` 命令编辑 root 用户的设置。因此，答案 A、B 和 C 是错误的。

10. B 和 C. `system-config-xserver` 命令在 Ubuntu 中不存在，且 `sudo Xorg` 只是启动 X 服务器。因此，答案 A 和 D 是错误的。

11. `/etc/X11/xorg.conf`。这是标准的 X 服务器配置文件。

12. D. `Xorg -configure` 命令在本地目录 (`/tmp`) 创建了一个建议的 `xorg.conf.new` 文件。答案 C 包含了日期和时间，是通过 `sudo dpkg-reconfigure xserver` 生成的。因此，答案 A、B 和 C 是错误的。

13. B. `sudo dpkg-reconfigure fontconfig-config` 在此情况下为本地系统配置基本集。

14. A 和 C. LCD 和 CRT 显示器渲染字体的方式不同。新语言（尤其是非欧洲字母）需要不同的字体配置。

15. B. 运行级别 1 不包含 GUI，最适合运行 `Xorg -configure` 命令。运行级别 2 是 GUI 的默认级别。如果安装了 GUI 且处于该级别，`Xorg -configure` 命令不起作用。运行级别 0 和 6 与关机和重启系统相关。因此，答案 A、C 和 D 都是错误的。

## 屏幕功能与字体

10. B 和 C. `system-config-xserver` 命令在 Ubuntu 中不存在，且 `sudo Xorg` 只是启动 X 服务器。因此，答案 A 和 D 是错误的。

![](img/8521db60567337b3b9ca1b288c5d36b6_449_0.png)

# 12 自定义 GNOME

## 认证目标

- 12.01 设置显示管理器
- 12.02 使用 Evolution 邮件客户端
- 两分钟强化演练
- 问答自测

# 432 第 12 章：自定义 GNOME

本章包含两个基本主题：GNOME 显示管理器和 Evolution 邮件客户端。GNOME 显示管理器是 Ubuntu Linux 默认显示的图形化登录界面；你将学习如何通过多种方式对其进行配置。虽然 Evolution 是一个功能上类似于 Microsoft Outlook 的个人信息中心，但 UCP 课程的重点是将 Evolution 作为邮件客户端来介绍。你将学习 Evolution 作为邮件客户端的一些功能，包括它如何连接到 Microsoft Exchange 服务器。

## 认证目标 12.01

### 设置显示管理器
