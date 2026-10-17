
# 第四部分：安装和配置桌面环境

`startkde` 或 `startxfce4` 命令会启动 KDE 或 Xfce4 桌面环境。该命令在你注销 DE 之前不会结束。通常情况下，shell 会等待 KDE 完成，然后运行下一条命令。该命令的 `exec` 前缀告诉 shell 这是最后一条命令，因此 shell 无需等待即可运行后续命令。

如果你在自动挂载方面遇到问题，请使用以下命令。将 `startxfce4` 替换为适用于你窗口管理器的命令。

```bash
exec ck-launch-session startxfce4
```

记住在你的 `~/.xinitrc` 中只保留一行未取消注释的 `exec` 行。

## 第 3 步：安装桌面环境

继续下方，安装你选择的 DE/WM。

- GNOME
- KDE
- Xfce
- LXDE
- Openbox
- Fluxbox
- fvwm2

# GNOME

## 关于 GNOME

GNU 网络对象模型环境。GNOME 项目提供了两项内容：GNOME 桌面环境（一个为终端用户设计的直观且吸引人的桌面）以及 GNOME 开发平台（一个用于构建集成到桌面其他部分的应用程序的扩展框架）。

## 安装

使用以下命令安装基础 GNOME 环境：

```bash
# pacman -S gnome
```

此外，你可以安装额外包：

```bash
# pacman -S gnome-extra
```

选择额外包中显示的所有包都是安全的。

## GNOME 的实用守护进程 (DAEMONS)

回想上述，守护进程是在后台运行、等待事件发生并提供服务的程序。某些用户倾向于使用 `hal` 守护进程。`hal` 守护进程会自动挂载磁盘、光驱以及 USB 驱动器/优存盘以供 GUI 使用。`fam` 守护进程允许实时访问最近安装的程序或文件系统的更改。`hal` 和 `fam` 都能让 GNOME 用户的生活变得简单。安装 GNOME 时会安装 `hal` 和 `fam` 包，但必须调用它们才能发挥作用。

你可能想要安装一个图形化登录管理器。对于 GNOME 来说，`gdm` 守护进程是一个很好的选择。

作为根用户：

```bash
# pacman -S gdm
```

启动 `hal` 和 `fam`：

```bash
# /etc/rc.d/hal start
# /etc/rc.d/fam start
```

将它们添加到你的 `/etc/rc.conf` 的 `DAEMONS` 部分，这样它们在启动时就会调用：

```bash
# nano /etc/rc.conf
DAEMONS=(syslog-ng network cron alsa hal fam gdm)
```

作为根用户，在 `/etc/custom.conf` 的 `[servers]` 部分中添加 `gdm`：

```ini
displaymanager=gdm
```

对于 GNOME 运行 `x`。你可以通过在 `/etc/pacman.conf` 中添加适当仓库来安装 Chakramod。

# Xfce

类似于根窗口应用、窗口管理器、文件管理器、面板等程序。Xfce 使用 `GTK` 工具包（类似于 GNOME）编写，并包含它自己的开发环境（库、守护进程等），这与其他大型桌面环境（DE）类似。与 GNOME 或 KDE 不同，Xfce 非常轻量，设计上更围绕 CDE 而非 Windows 或 Mac。它的开发周期较慢，但非常稳定且快速。Xfce 非常适合旧版硬件，在较新的机器上运行得同样出色。

## 安装

安装 Xfce：

```bash
# pacman -S xfce4
```

你可能还想安装主题和额外扩展：

```bash
# pacman -S xfce4-goodies gtk2-themes-collection
```

注意：`xfce4-xfapplet-plugin`（一个允许在 Xfce4 面板中使用 GNOME 应用程序的插件）是 `xfce4-goodies` 组的一部分，并依赖于 `gnome-panel`，而 `gnome-panel` 又依赖于 `gnome-desktop`。在安装之前你可能需要考虑这一点，因为它代表了大量的额外依赖。

如果你遇到关于 `dbus-launch` 的错误，那么你需要安装 `dbus`：

```bash
# pacman -S dbus
```

如果你想在登录时欣赏“提示与技巧”，请安装 `fortune-mod` 包：

```bash
# pacman -S fortune-mod
```

## 有用的守护进程 (DAEMONS)

回想，守护进程是在后台运行、等待事件发生并提供服务的程序。某些 Xfce 用户倾向于使用 `hal` 守护进程。`hal` 守护进程等功能会自动挂载磁盘、光驱器和 USB 磁盘/优存盘以供 GUI 使用。`fam` 守护进程允许在 GUI 中实时显示文件更改，允许立即访问最近安装的程序或文件系统的更改。`hal` 和 `fam` 包在安装 Xfce 时会被安装，但必须调用它们才能发挥作用。

启动 `hal` 和 `fam`：

```bash
# /etc/rc.d/hal start
# /etc/rc.d/fam start
```

> **注意：** `hal` 守护进程依赖并将自动启动 `dbus` 守护进程。

在 `/etc/rc.conf` 中编辑你的 `DAEMONS` 数组：

```bash
# nano /etc/rc.conf
```

将 `hal` 和 `fam` 添加到你的 `DAEMONS` 数组中，以便在启动时调用它们。

> **提示：** 安装和配置 Xfce 的高级指令可以在 Xfce 文章中找到。

如果你想安装，查看“添加登录管理器（KDM、GDM 或 XDM）以实现启动自动登录”。否则，你可以通过控制台登录并运行：

```bash
$ startxfce4
```

恭喜！欢迎来到你新 Arch Linux 系统上的 Xfce 桌面环境！你可能还会对“安装后提示”wiki 文章感兴趣。

# LXDE

## 关于 LXDE

`LXDE`（轻量级 X11 桌面环境）是一个新项目，专注于提供一种现代桌面环境，旨在保持低系统资源占用的同时轻量、快速、直观且功能齐全。`LXDE`与其他桌面环境完全不同，因为 `LXDE` 的每个组件都是离散且独立的应用程序，每个程序都可以被其他程序替换。这种模块化设计消除了所有不必要的依赖并提供了更大的灵活性。详情和截图可见：`http://lxde.org/`

`LXDE` 提供：

1. `OpenBox` 窗口管理器
2. `PCManFM` 文件管理器
3. `LXPanel` 系统面板
4. `LXSession` 会话管理器
5. `LXAppearance` `GTK+` 主题切换器
6. `GPicView` 查看器
7. `Leafpad` 简单文本编辑器
8. `XArchiver`：轻量、快速且独立平台的基于 `gtk+` 文件归档程序
9. `LXNM`（开发中）：支持无线连接的 `LXDE` 轻量级网络管理器

这些轻量且多功能的工具结合在一起实现了快速设置、模块化和简单。

使用以下命令安装 `LXDE`：

```bash
# pacman -S lxde
```

添加：

```bash
exec startlxde
```

- - 如果你计划运行 `nm-applet`，则应该使用以下命令

```bash
exec ck-launch-session startlxde
```

到你的 `~/.xinitrc` 中并使用 `startx` 或 `xinit` 启动。

> **提示：** 更多信息可在 `LXDE` wiki 文章获取。

# Fluxbox

`Fluxbox` © 是另一个用于 X 的窗口管理器。它基于 `Blackbox` `0.61.1` 代码。`Fluxbox` 看起来像 `blackbox`，并像 `blackbox` 一样处理样式、颜色、窗口放置和类似事项（100% 主题/样式兼容）。

使用以下命令安装 `Fluxbox`：

```bash
# pacman -S fluxboxconf
```

如果你使用 `gdm`/`kdm`，会自动添加一个新的 `fluxbox` 会话。否则，你应该修改用户的 `.xinitrc` 并向其中添加此：

```bash
exec startfluxbox
```

更多信息可见 `Fluxbox` 文章。

# Openbox

`Openbox` 是一个符合标准、快速、轻量级且可扩展的窗口管理器。

`Openbox` 与你的应用程序配合工作，让你的桌面更容易管理。这是因为它的开发方法与窗口管理器的通用情况相反。`Openbox` 最初的编写是为了符合标准并确保正常运行。只有在这些到位后，团队才转向界面。

`Openbox` 可以作为 GNOME、KDE 和 Xfce 的完全功能替代品。

使用以下命令安装 `openbox`：

```bash
# pacman -S openbox
```

额外的配置工具可用：

```bash
# pacman -S obconf obmenu
```

一旦安装了 `openbox`，你需要：

```bash
mkdir -p ~/.config/openbox
cp /etc/xdg/openbox/* ~/.config/openbox/
cp /etc/xdg/menu.xml ~/.config/openbox/
```

`rc.xml` 是 `Openbox` 的主配置文件。可以手动编辑（可以使用 `obconf`）。`menu.xml` 配置右键菜单。

对于 `KDM` 没什么需要做的；`openbox` 已在会话列表中。否则，将：

```bash
exec openbox
```

添加到你的 `~/.xinitrc`。如果你计划运行 `hal`（这是必须的），请确保你的 `xinitrc` 读取为：

```bash
exec dbus-launch --exit-session openbox
```

你也可以使用 `xinit` 从 shell 启动 `Openbox`：

```bash
$ xinit /usr/bin/openbox
```

- - `Openbox` 也可以作为窗口管理器用于。

一些实用的 `Openbox` 程序：

- 如果你需要面板，可以使用 `PyPanel`、`Tint2` 或 `LXpanel`
- 如果你想设置背景，可以使用 `feh`
- 如果你需要简单的文件管理器，可以使用 `ROX`
- `PcManFM` 轻量但多功能的文件管理器（也提供桌面图标）
- `iDesk`（在 AUR 中可用）提供桌面图标
- `Graveman` 用于刻录 CD 或 DVD

# fvwm2

`FVWM` 是一个用于 X 系统的强大的、符合 `ICCCM` 标准的多虚拟桌面窗口管理器。开发活跃，支持良好。

使用以下命令安装 `fvwm`：

```bash
# pacman -S fvwm
```

`fvwm` 会自动出现在 `kdm`/`gdm` 的会话列表中。否则，将：

```bash
exec fvwm
```

添加到你的 `.initrc`。

# 有用的应用程序

此页面永远是不可能的。它只是展示了针对日常用户的一些优秀应用程序。

可能也值得检查轻量级软件。

# Web 浏览器

# Firefox

流行的 `Firefox` 浏览器可以通过 `pacman` 获取，尽管它没有官方品牌。因此，程序打开时会显示为其开发代号 `Shiretoko`。

安装方法：

```bash
pacman -S firefox
```

# 插件

确保安装 `flashplugin` 和 `mplayer-plugin` 包以获得完整的网络体验：

```bash
pacman -S flashplugin mplayer-plugin
```

# Gecko Media Player

作为现在过时的 `mplayer-plugin` 的良好替代品是 `Gecko Media Player`。与 `MPlayer` `1.0RC2` 结合时更稳定。（不再有苹果预告片崩溃的问题。）

# Arch Linux 手册

```bash
pacman -S gecko-mediaplayer
```

（注意！如果已经安装了 `mplayer-plugin`，请务必将其移除。）

`Thunderbird` 适用于管理你的电子邮件。如果你正在使用 GNOME，可能想看看 `Epiphany` 和 `Evolution`；如果你正在使用 KDE，`Konqueror` 和 `KMail` 可能是你的选择。如果你想尝试完全不同的东西，仍然可以使用 `Opera`。最后，如果你在系统控制台——或在终端会话中工作，你可以使用 `eLinks`、`Links` 和 `Lynx` 等各种文本浏览器，并使用 `Mutt` 管理你的电子邮件。`Pidgin`（以前称为 `Gaim`）和 `Kopete` 分别是 GNOME 和 KDE 的良好即时通讯软件。如果你使用 `Jabber` 或 `Google Talk`，`PSI` 和 `Gajim` 是完美选择。

# 办公

全套 `LaTeX` 软件：`tetex` 已经流行了多年，它的继者 `Texlive` 可以从 `extra` 仓库获取。

`KOffice` 是一套革命性的办公套件。它正在向 `koffice2` 快速发展。

`OpenOffice.org` 是一个完整的办公套件（类似于 `Microsoft Office`）。`Abiword` 是一个良好且轻巧的替代文字处理器，`Gnumeric` 是 GNOME 桌面上的 `Excel` 替代品。

`GIMP`（或 `GIMPShop`）是一个基于像素的图形程序（类似于 `Adobe Photoshop`），而 `Inkscape` 是基于矢量的图形程序（如 `Adobe Illustrator`）。

# 视频播放器

# VLC

`VLC Player` 是多功能多媒体播放器，可以从磁盘或文件播放许多格式。它还提供了在局域网上流多媒体的能力。要安装它，只需输入下面的代码。

```bash
pacman -S vlc
```

# Mplayer
