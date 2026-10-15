
# 第 13 章：极简图形化环境

**表 13-1. 有用的 Xfce 软件包**

| 包 | 描述 |
| --- | --- |
| desktop-profiles | 帮助为不同用户配置桌面配置文件 |
| kdocker | 支持在系统托中固定应用程序 |
| mail-notification | 允许邮件管理器在收到新邮件时通知 |
| network-manager-gnome | 包含网络管理工具 |
| xfce4 | 添加一个包含其他软件包的元包 |
| xfce4-appender | 查找已安装的应用程序 |
| xfce4-cpugraph-plugin | 提供 CPU 系统负载的图形视图 |
| xfce4-net-plugin | 提供网络接口负载的图形视图 |
| xfce4-session | 支持在注销时保存运行应用程序的状态 |
| xfce4-taskmanager | 允许运行进程 |
| xfce4-terminal | 添加一个基于 GUI 的命令行终端 |
| xfprint4 | 包含 GUI 打印机管理器 |

**表 13-2. 适用于 Xfce 桌面环境的管理软件包**

| 包 | 描述 |
| --- | --- |
| gconf2 | 定制 GNOME 设置 |
| gnome-system-tools | 包含用于网络、用户和共享的管理工具 |
| policykit-gnome | 支持权限管理 |
| synaptic | 允许更新现有和可安装的软件包 |
| system-config-kickstart | 配置 Kickstart 配置文件 |
| system-config-printer | 配置打印机 |
| system-config-samba | 配置 Samba 服务器上的共享 |
| update-manager | 支持自定义更新 |
| virt-manager | 允许配置虚拟机 |

或者，还有与`X`命令相关的选项，它可以自动检测大多数硬件并在本地目录中创建建议的 X 服务器配置文件`xorg.conf`。基于`displayconfig-gtk`软件包，也有一个 GUI 工具来重新配置 X 服务器，该软件包可以通过以下命令安装：

```
$ sudo apt-get install displayconfig-gtk
```

## 使用图形工具配置 X Server

“屏幕和图形偏好”（Screen and Graphics Preferences）工具可以帮助配置 X 服务器。它可以通过`sudo displayconfig-gtk`命令启动。在图 13-5 所示的屏幕和图形偏好窗口中，如果硬件支持，你可以配置多个显示器。例如，带有外部视频接口的笔记本电脑将显示屏幕 1 和 2。

![](img/28cf881509dedde88f9e34e8cefb7020_367_0.png)

**图 13-5.** 屏幕和图形偏好工具

正如“位置”（Location）下拉框所示，此工具支持 X 服务器配置。它适用于可能连接到扩展坞的笔记本电脑等系统。使用上述配置，点击带有**向下箭头**的磁盘图标，并将配置保存到特定位置下。对第二个配置重复此过程。

该工具有两个标签页。“屏幕”（Screen）标签用于配置显示器，“显卡”（Graphics Card）标签用于配置与显卡相关的驱动程序和显存。

“图形”标签页下的“驱动程序”（Driver）选项会打开可用驱动程序的菜单，如图 13-6 所示。如果你点击“按名称选择驱动程序”（Choose Driver By Name）下拉框，允许让你从可用驱动程序列表中进行选择。如果你不确定哪个驱动程序最适合本地系统，通用的 VESA 和 VGA 驱动程序在大多数情况下都可以工作。然而，作为通用驱动程序，它们可能无法启用让现代显卡如此吸引人的功能。

> 注意：VESA 是 Video Graphics Array 的缩写，是一种旧式阴极管显示器的标准。VESA 也是 Video Electronics Standards Association 的缩写，提供了许多标准；在 Linux 中引用时，该标准与 Super VGA 硬件相关。

或者，如果你选择“按型号选择驱动程序”（Choose Driver By Model），你可以从 40 个不同制造商的一个或多个显卡中选择。一旦选中，如果显卡和相关的 Linux 驱动程序支持，你可能可以选择显存。

显卡配置后，就可以按照“屏幕”标签下描述的方法配置显示器。要选择显示器，点击“型号”（Model）旁边的按钮。它会打开“选择屏幕”（Choose Screen）窗口，如图 13-7 所示，支持支持按品牌和制造商选择显示器。可以根据需要配置宽屏显示器。如果需要，

![](img/28cf881509dedde88f9e34e8cefb7020_368_0.png)

**图 13-6.** 选择显卡驱动程序

![](img/28cf881509dedde88f9e34e8cefb7020_368_1.png)

**图 13-7.** 选择屏幕（显示器）

点击“检测”（Detect）按钮来检测当前的显示器硬件并建议合适的驱动程序。

完成更改并关闭工具后，更改将保存到 X 服务器配置文件`/etc/X11/xorg.conf`中。提示所有用户必须注销的消息是重启 X 服务器的前提条件，此时`xorg.conf`的更改将会被应用。

## 从命令行配置 X Server

熟悉其他 Linux 发行版的人可能熟悉 X 服务器的命令行配置。在较旧的发行版中，它被称为`f86config`；在最新的发行版中，它被称为`xorgconfig`。`dpkg-reconfigure xserver-xorg`命令将引导管理员通过一系列步骤。

使用上述命令配置 X 服务器 是一个直观的过程。在开始此过程之前，请备份 X 服务器配置文件`/etc/X11/xorg.conf`。事实上，你可能想打印该文件作为参考。在记住这一点，以下命令将 X 服务器配置保存到用户主目录：

```
$ cp /etc/X11/xorg.conf ~
```

如果你随时需要启动该工具，请打开一个新的命令行窗口，并通过`ps aux | grep dpkg-reconfigure`查找进程 ID。进程 ID 在第二列；这里是运行上述命令的示例：

```
root      4986 2.4 3.1 13444 7988 pts/0 S+ 18:23
0:00 /usr/bin/perl -w /usr/bin/dpkg-reconfigure xserver-xorg
```

在这种情况下，进程 ID 为 4986，此时我可以使用以下命令启动过程：

```
$ sudo dpkg-reconfigure xserver-xorg
```

如果你希望以不详细的方式配置 X 服务器，可以包含`-phigh`选项，它会自动创建一个新的`xorg.conf`文件而无需提问。但对于此，请使用以下命令启动过程：

现在执行以下步骤：

1. 命令将打开一个类似于图 13-8 所示并在后续步骤描述的低级图形界面。这些屏幕无法通过“点击”选项；可以使用 TAB、ENTER 和箭头键选择选项。

2. 选择是否使用帧缓冲。为了最佳性能可能需要进行尝试。选择 Yes 或 No 并按回车键继续。

*348 Ubuntu 服务器管理*

![](img/28cf881509dedde88f9e34e8cefb7020_370_0.png)

**图 13-8.** 在此界面选择是否启用内核帧缓冲（Framebuffer）

3. 你可以选择自动检测键盘布局；为了本次练习，请选择 No 并按 ENTER 继续。

4. 检查与键盘布局相关的描述；通常美式英语键盘的用户会输入 us。说明中描述的备用语言的 ISO 代码位于`/usr/share/iso-codes`目录下的`iso_3166.tab`文件中。输入所需的键盘代码或 ISO 代码并选择 OK 继续。

5. 现在你可以选择一个 X 键盘扩展规则集，它在菜单中显示为 XKB。通常情况下，你应该直接接受`xorg`的默认设置。其他选项列在`/usr/share/X11/xkb/rules/`目录中。如果需要，输入不同的选择并选择 OK 继续。

6. 阅读与 XKB 规则集相关的选项。阅读后，选择 OK 继续。

7. 如果合适，输入相关的键盘型号。美式键盘的用户通常应该接受默认的`pc105`，除非已知精确的型号。选项列在`/usr/share/X11/xkb/symbols/`目录中。如果需要，输入不同的选择并选择 OK 继续。

8. 阅读与键盘变体相关的选项。如果你需要键盘变体，请在文本框中输入它。如果不确定，变体选项列在`/usr/share/X11/xkb/symbols/`目录中。通常，美式键盘不需要变体，此项可以留空。输入任何所需的选择并选择 OK 继续。

9. 阅读针对“Meta” 键等选项提供的可用额外键盘选项的描述，写下任何需要的选项，并选择 OK 继续。

10. 根据步骤 9 中的信息，输入任何所需的键盘选项，并选择 OK 继续。
