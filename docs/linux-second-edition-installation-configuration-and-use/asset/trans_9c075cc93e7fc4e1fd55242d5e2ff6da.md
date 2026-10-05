

![](img/b30873dd3d753687a59253fb9ad26a0b_315_0.png)

图 8.12 KDE 磁盘导航器。

以及菜单中 PERSONAL（个人）和 SHARED（共享）区域的项目可以通过 OPTIONS 命令进行自由配置。

## KDE 内部

### rc 文件

大多数 KDE 程序将状态设置（字体大小、选项等）存储在文件 /.kde/share/config/name` 中。这是一个文本文件，其结构类似于 Windows 3.1 中常见的 *.ini 文件。例如，显示在 KPanel 上的程序图标存储在 `~/.kde/share/config/kpanelrc` 中。顺便提一下，包含屏幕保护设置的文件名不是 namerc，而是 kssrc。

### 应用程序特定目录

某些 KDE 程序拥有如此多的配置数据，单个文件会过于臃肿。程序通常会在 `~/.kde/apps` 中创建一个单独配置目录，例如 `~/.kde/apps/klynx`。

### kdelink 文件

KDE 中的链接或以图标表示的对象（在桌面、开始菜单、面板上）存储在扩展名为 .kdelink 的文本文件中。例如，整个 KDE 开始菜单由许多个包含 .kdelink 文件的目录组成（`path/opt/kde/share/appink`）。在 .kdeink 目录中，.kdeink 文件扮演了 .kdelink 文件的角色。

.kdelink 文件可以包含大量信息，例如多种语言的对象名称、图标名称、关于文件类型的信息等。KDE 识别 .kdelink 文件的多种对象类型：程序、目录、设备（指向设备或分区的链接）、FTP 和 URL 链接以及 MIME 数据类型。

## KDE 目录

以下列表总结了最重要的 KDE 目录位置：

- /kde/share/appink 个人菜单
- /kde/share/apps 应用程序特定数据
- /kde/share/config 本地配置设置
- /kde/share/icons 本地图标
- /kde/share/mime MIME 数据类型
- /Desktop 桌面信息
- /Desktop/Autostart 程序自动启动
- /Desktop/Templates 新 kde 对象的模板
- /Desktop/Trash 垃圾箱
- /opt/kde/bin 程序
- /opt/kde/appink 开始菜单
- /opt/kde/apps 应用程序特定数据
- /opt/kde/config 全局配置设置
- /opt/kde/doc 在线文档（多语言）
- /opt/kde/icons 菜单和对话框文本（多语言）
- /opt/kde/locale MIME 数据类型
- /opt/kde/toolbar 工具栏图标
- /opt/kde/wallpapers 背景位图

## KDE 显示管理器 (kdm)

如果你希望在计算机启动后立即看到 KDE 对话框，可以使用 KDE 显示管理器 kdm 代替 xdm（第 270 页）。该程序允许非常方便的登录。你甚至可以选择自己的窗口管理器。kdm 的配置在 KDE 控制中心的 APPLICATION/DESKTOP MANAGER 中进行。（然而，在线文档中描述的单独选项必须直接在 kdmrc 中设置。）

通过 LOGOUT（退出）按钮，你可以在确认后启动关机（即你可以终止 Linux）。

> 在 SuSE 中，你可以使用 vast 来为 kdm 设置环境变量 DISPLAYMANAGER。通过这样，在运行级别 3 中会自动使用 kdm（而不是 xdm）。在其他发行版中，你需要手动修改相应的 Init 文件（通常为 /etc/rc.d/init.d/xdm 或 /etc/init.d/xdm）。

## KDE 窗口管理器的鼠标和键盘快捷键

下表提供了 KDE 窗口管理器默认快捷键概述。（与其他许多事物一样，这些快捷键也可以配置。在 KDE 1.0 中，需要直接修改 kwm；自 KDE 1.1 起，你可以使用控制中心。）

### 桌面上的鼠标快捷键

| 操作 | 结果 |
| :--- | :--- |
| 中键 | 显示所有运行程序的列表菜单 |
| 右键 | 显示包含几个基础命令的菜单 |

### 窗口标题中的鼠标快捷键

| 操作 | 结果 |
| :--- | :--- |
| 中键 | 将窗口移动到最底部 |
| 右键 | 窗口菜单（最大化、最小化、移动） |
| 双击 | 最大化窗口 |

### 窗口内部的鼠标快捷键

| 操作 | 结果 |
| :--- | :--- |
| 左键 + `Alt` | 移动窗口 |
| 中键 + `Alt` | 将窗口移动到最底部 |
| 右键 + `Alt` | 更改窗口大小 |

### 键盘快捷键

| 快捷键 | 结果 |
| :--- | :--- |
| `Ctrl`+Esc` | 所有运行程序的列表 |
| `Alt`+Tab` | 切换活动程序 |
| `Ctrl`+`Tab` | 切换虚拟桌面 |
| `Ctrl`+`Alt`+Esc` | 杀死窗口 (xKILL) |
| `Alt`+`F2` | 启动程序 |
| `Alt`+`F3` | 显示窗口菜单 |
| `Ctrl`+`F1` 到 `F8` | 激活虚拟桌面 1 到 8 |

## 8.5 GNOME

本节对 GNOME 的核心组件进行初步介绍。描述的基础是 RedHat 6.0 的默认配置（即 GNOME 1.0 结合 Enlightenment 0.15）。

本节仅限于 GNOME 基础知识。独立于 GNOME 使用的 Linux 程序将在其他章节中描述。以下列表了重要的程序及其对应的页码：

- gnome-help-browser 系统帮助，79 页
- gmc 文件管理器，499 页
- knee 图形格式转换，517 页
- gftp FTP 客户端，338 页
- gimp 图像处理，659 页
- gnome-linuxconf 系统配置，730 页
- ggnorm 包管理，732 页

![](img/b30873dd3d753687a59253fb9ad26a0b_318_0.png)

## 生存规则

- 与 KDE 不同，GNOME 操作（如启动程序）通过双击触发。
- 在许多程序或 GNOME 组件中，可以使用右键调用上下文菜单。

几乎所有 GNOME 程序都支持拖放。例如，你可以从文件管理器中拖出一个文本文件并将其放到编辑器 (gedit) 或开始菜单。除了左键外，按 Ctrl 复制对象。图标的管理由文件管理器负责。因此，必须先启动程序才能使用桌面图标。

GNOME 程序通常可以通过菜单进行配置。（某些 GNOME 组件在 GNOME 控制中心进行配置——见下文）。通常，也可以手动更改配置文件，但很少需要——例如针对某个选项没有配置对话框。

不要使用 Ctrl+Alt+Backspace 进入 GNOME。相反，请使用开始菜单中的 OUT 命令。然后 GNOME 会存储运行程序的信息，并尝试在下次启动时尽可能恢复当前状态。（然而，这仅对某些程序有效。）

尽管 GNOME 在许多方面方便了程序处理，但显然存在一些缺陷，例如对键盘的支持不佳。大量的操作只能通过鼠标执行。在许多程序中，甚至通过 Alt 和首字母调用菜单。

![](img/b30873dd3d753687a59253fb9ad26a0b_319_0.png)

## 配置

GNOME 提供了极其可能的配置。花些时间尝试——这绝对值得的！当桌面配置为用户的个人喜好时，工作会愉快得多。

重要的 GNOME 组件通过 GNOME 控制中心进行配置。该程序通过 GNOME 面板的开始菜单启动：SYSTEM | GNOME CONTROL CENTER。它的操作非常简单，此时不需要进一步解释。

语言

GNOME 控制中心没有为设置菜单、对话框等所需的语言提供独立实体。系统会评估环境变量 LANG 和 LC_ALL 的设置。（这些变量最好设置在 /etc/profile 中）。

窗口管理器

所有不直接涉及 GNOME 但涉及窗口器的设置必须通过窗口管理器自身的配置程序或直接修改其配置文件来设置。

