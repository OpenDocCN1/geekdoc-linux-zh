
# linuxcare login:

使用用户名 `root` 登录，并使用 `linuxcare` 作为密码。按下 Enter 后，文件 `CREDITS-README.txt` 将会显示。请仔细阅读此文件！

使用向上或向下箭头键滚动浏览文件。阅读完毕后，按 q 键退出阅读。然后你就位于 Linux 控制台的根操作员提示符下。若要在会话期间启用 PCMCIA 支持，请使用 pcmcia shell 脚本（位于 `/bin` 目录下）并使用 start 关键字，如下所示：

```
root@linuxcare:~$ pcmcia start
```

这将加载 David Hinds 的 Card Services 3.1.3 版本，并启动 `cardmgr` 守护进程。如果你需要网络支持，请使用 `trivial-net-setup` 脚本来初始化内部或 PCMCIA 以太网适配器。

可启动商务卡的 Debian Linux 系统配置为自动识别并挂载在 `/mnt` 目录下找到的任何 Linux 文件系统。例如，你的笔记本可能在多个分区上安装了 Linux，例如：

```
/dev/hda5          /boot
/dev/hda6          /d2
/dev/hda8           /
```

在此示例中，`/boot` 目录（包含 Linux 内核、系统映射及其他信息）位于 `/dev/hda5`。其余的 Linux 文件系统位于 `/dev/hda8`，而一个备用卷 `/d2` 位于 `/dev/hda6`。当你使用这张卡启动时，这些分区可能会显示出来（使用 `df` 命令）如下：

| 文件系统 | 1k 块 | 已用 | 可用 | 使用% | 挂载于 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/root | 7931 | 2187 | 5335 | 29% | / |
| /dev/hdc | 45076 | 45076 | 0 | 100% | /mnt/cdrom-real |
| /dev/c-loop | 99184 | 63388 | 35796 | 64% | /mnt/cdrom |
| /dev/hda5 | 7746 | 970 | 6376 | 13% | /mnt/0 |
| /dev/hda6 | 2039792 | 8 | 1936168 | 0% | /mnt/1 |
| /dev/hda8 | 2000204 | 1295376 | 602220 | 68% | /mnt/2 |

这表明笔记本的 `/boot`、`/d2/` 和 `/` 目录已被挂载在 `/mnt/0`、`/mnt/1` 和 `/mnt/2` 目录下。请注意，出于安全和保护目的，任何找到的 Linux 文件系统都以只读方式挂载；这意味着你将无法创建、编辑或删除文件。你必须先取消挂载，然后以读写模式重新挂载任何所需文件系统。例如，如果你希望在你笔记本的根 Linux 分区（在我们示例中是 `/dev/hda8`）上创建、编辑或删除文件，请先使用 `umount` 命令取消挂载该分区，如下所示：

```
root@linuxcare:~$ umount /mnt/2
```

然后使用 `mount` 命令重新挂载 `/` 目录，如下所示：

```
root@linuxcare:~$ mount -t ext2 /dev/hda8 /mnt/2
```

然后你可以导航到你的笔记本根目录，以创建、编辑或删除文件。这种方法在修复笔记本初始化表 `/etc/inittab`、文件系统表 `/etc/fstab` 或 `/etc/rc.d`/`init.d` 目录下的启动脚本（如果你使用的是基于 Red Hat 的 Linux 系统）中的错误时特别有用。

### 令人惊喜的发现

当你使用这张卡启动时，你会发现可以使用四个不同的虚拟控制台。登录后，按 Alt+F2 跳转到另一个基于文本的会话。然后你会看到另一个登录提示符（你必须使用 `root` 作为用户名，并使用 `linuxcare` 作为密码）。使用 `logout` 或 `exit` 命令退出控制台会话，然后按 Alt+F1 返回到原始控制台。

这张商务卡还充满了宝藏。你会发现卡上包含了 424 个不同的 Linux 命令。其中包括几个文本编辑器，如 `pico`、`vim` 和 `jedit`，以及 Midnight Commanders 图形文件接口命令，还有复杂的网络实用工具，如 `nmap` 和 `hping2`。

### 使用 X11

CD 上甚至还有一份 XFree86 的 X11 发行版 3.3.5 的子集副本！这意味着你可以在启动会话期间尝试使用 `startx` 命令启动 X11，如下所示：

```
root@linuxcare:~# startx
```

如果你笔记本的图形芯片组与包含的 XF86_SVGA 或 Xf86_VGA16 服务器兼容，并且在 CD-ROM 的 `/etc/XF86Config` 文件中找到了兼容的模式行，你将直接进入使用 `fvwm` X11 窗口管理器的 X11 会话。如果初始的 `startx` 命令不起作用，请确保手指放在 Ctrl+Alt+Backspace 键上，以便快速终止服务器！你还可以使用 `startx` 命令的 `-- -bpp` 选项尝试不同的颜色深度，如下所示：

```
root@linuxcare:~# startx -- -bpp 24
```

此命令尝试使用 24 位平面启动 X11 会话，即数百万种颜色（有趣的是，在 IBM ThinkPad 390X 上，当所有其他模式（如 `-bpp 15` 和 `-bpp 16`）都失败后，这种模式运行得非常好）。然而，更好的方法是在线创建一个指向适当 XF86Config 文件的链接！如果你查看 `/etc/X11` 目录，你会看到：

```
XF86Config
XF86Config-Dell-gx1-1cd
XF86Config-Dell-opti-1cd
XF86Config-Matrox-g200
XF86Config-crt-lcd
XF86Config-old
XF86Config-neomagic
XF86Config-dell_gx1_lcd
```

如果您的笔记本可以使用上述任一专用的 XF86Config 文件，则可以将 XF86_SVGA 服务器强制使用该文件。请使用 `ln` 命令在 `/root`（而非 `/`）目录中创建一个名为 XF86Config 的符号链接，指向正确的 XF86Config 文件。例如，如果您的笔记本使用 NeoMagic 图形芯片组，请像这样使用 `ln` 命令：

```
root@inxware:~# ln -s /etc/X11/XF86Config-neomagic XF86Config
```

然后，您可以使用 `startx` 命令进入一个合适的 X11 会话！请注意，该链接仅在当前运行的会话中有效；当您重启笔记本时，该文件将消失。您会发现 CD-ROM 上附带了一些 X11 和 Internet 客户端，例如 `Amaya` 和 `lynx` 网页浏览器，`rxvt-xterm` 终端客户端，以及 `ftp` 和 `telnet` 命令。要退出 X 会话，请在桌面的空白区域点击并选择 `Exit Fvwm` 菜单项，或者按 Ctrl+Alt+Backspace 终止 X 服务器。

另外，作为一个特别的惊喜，CD-ROM 上还藏有一个彩蛋（Easter egg）！在控制台命令行输入：

```
root@inxware:~# SVGATextMode | egg
```
