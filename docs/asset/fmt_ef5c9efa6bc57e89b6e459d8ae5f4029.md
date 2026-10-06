
# Caldera Open Linux 使用指南

![](img/d858127fcfbd3123294590b5f47a0447_0_0.png)

> CD-ROM 包含：
> Caldera OpenLinux 2.2 带有 Bootmagic 和 Partition Magic，
> Caldera 版本

Que 的 Caldera OpenLinux 特别版提供了以下主题的专家见解：
- OpenLinux 的图形化安装
- KDE 桌面的导航与自定义
- 使用 TCP/IP、Samba 和 NetWare 进行 Linux 网络配置
- 将系统连接到互联网
- 设置常见的 Air/Internet 服务，如邮件和 Web 服务器
- 使用防火墙和“封装器 (wrappers)”保护您的 Linux 系统
- 使用 SSH 和 PGP 确保在线信息交换
- 全面的硬件兼容列表
- 针对随新版 OpenLinux 的各种驱动程序的详细启动/模块参数列表

![](img/d858127fcfbd3123294590b5f47a0447_1_0.png)

Caldera 的 OpenLinux 软件为您提供以下功能：
- 无与伦比的便捷安装（您可以从 Windows、从可启动 CD-ROM 驱动器或磁盘启动安装）
- 自动检测现代 PC 硬件
- 稳固稳定的 32 位多任务处理（同时运行多个程序的能力）
- 熟悉且易用的图形化界面，拥有大量的工具、游戏和办公应用程序，帮助您的日常电脑使用
- 读写可与 Microsoft Office 应用程序交换的文档的能力
- 完整的软件开发环境，包含 C++ 等语言的编译器和调试器，以及 Python 和 Perl 等解释型/伪代码语言
- 无论是服务器还是工作站，连接互联网所需的一切

![](img/d858127fcfbd3123294590b5f47a0447_1_1.png)

![](img/d858127fcfbd3123294590b5f47a0447_2_0.png)

# 从 LIZARD (Linux 向导) 安装 OpenLinux

Caldera OpenLinux 提供了无与伦比的便捷安装。请按照以下步骤为 Linux 安装 OpenLinux：
1. 选择所需的语言。您的选项有英语、德语、法语和意大利语。
2. 缓慢移动您的鼠标；它将被自动检测。
3. 选择以下安装目标之一：
   - 整个磁盘
   - 准备好的分区（如果您选择了 Windows 选项，请使用此选项）
   - 自定义（仅限专家）
4. 选择您想要安装的包集（选择时请记住您的分区大小）。
5. 选择键盘（型号和布局）。默认为通用 101。
6. 视频适配器将被自动检测。默认为 256K 视频内存。选择 Probe（探测）以确定确切的视频内存。
7. 从大量的预设品牌和型号列表中选择显示器设置。
8. 选择所需的视频模式、色彩深度和分辨率。
9. 为 root 账户设置密码。

![](img/d858127fcfbd3123294590b5f47a0447_3_0.png)

![](img/d858127fcfbd3123294590b5f47a0447_3_1.png)

![](img/d858127fcfbd3123294590b5f47a0447_3_2.png)

## 设置 Root 密码

Root 密码：
确认拼写：
Root
默认设置了一个登录账户，登录后需要更改：root 账户。
该账户授予对安装系统的系统级“表观”访问权限。通过登录此账户的密码，可以破坏系统上的所有文件、所有异常之外的一切内容。

![](img/d858127fcfbd3123294590b5f47a0447_4_0.png)

图 4

10. 您可以添加额外的用户和密码。可以添加任意数量的用户。为每个用户设置密码。
11. 设置以下项之一作为您的网络选项：
    - 无网络
    - 使用 DHCP（启动时设置 IP 地址）
    - 静态分配（如果您在安装期间连接到网络，将自动检测相应的网络数字；您必须提供 IP 地址）

### 选择时区

时区
您可以通过从下拉菜单中选择附近的城市或区域位置来选择时区。
请务必使用屏幕底部的单选指示计算机钟显示的是格林尼标准时间 (GMT) 还是本地时间。
- 硬件时不使用 GMT 时间
- 硬件时按本地时间运行

![](img/d858127fcfbd3123294590b5f47a0447_4_1.png)

图 5

12. 通过在地图上找到正确的区域或在组合框中手动选择正确的区域来设置时区。

### 在安装完成前的娱乐。

![](img/d858127fcfbd3123294590b5f47a0447_4_2.png)

13. 出现安装娱乐界面。在屏幕上玩游戏，直到“牛回家（无结束）”。
LIZARD 安装是自动的。安装完成后，将出现 Caldera Systems 标志，随后是一系列需要用户输入的屏幕。

以下 Windows 指令仅用于为您的系统安装 OpenLinux 做准备：
以下 Windows 指令仅用于为您的系统安装 OpenLinux 做准备。根据前面的章节“从 LIZARD (Linux 向导) 安装 OpenLinux”，请按照以下步骤操作：
1. 插入 CD-ROM；安装会自动运行。
2. 点击 Install（安装）开始过程。
3. 遵循 OpenLinux 设置界面。
4. 在 OpenLinux 设置界面，执行以下操作：
    - 读取 README 文件
    - 浏览文档
    - 查看 Caldera 的特别优惠
    - 创建安装（仅当 CD-ROM 不支持供电）
    - 创建模块（仅当 CD-ROM 不支持供电）
5. OpenLinux 安装是自动的。安装完成后，将出现 Caldera Systems 标志，随后是一系列需要用户输入的屏幕。（等等，后面的页面 OCR 文本似乎乱了。我将根据提供的内容重构逻辑流。）

*根据上下文对混乱部分进行重构：*
以下 Windows 指令仅用于为您的系统安装 OpenLinux 做准备。根据前面的章节“从 LIZARD (Linux 向导) 安装 OpenLinux”，请按照以下步骤操作：
1. 插入 CD-ROM；安装会自动运行。
2. 点击 Install（安装）开始过程。
3. 遵循 OpenLinux 设置界面。
4. 在 OpenLinux 设置界面，执行以下操作：
    - 读取 README 文件
    - 浏览文档
    - 查看 Caldera 的特别优惠
    - 创建安装（仅当 CD-ROM 不支持供电）
    - 创建模块（仅当 CD-ROM 不支持供电）
5. OpenLinux 安装是自动的。安装完成后，将出现 Caldera Systems 标志，随后是一系列需要用户输入的屏幕。（等等，后面的页面 OCR 文本似乎乱了。我将根据提供的内容重构逻辑流。）

KDE 击键操作与全局击键操作

| 表 1 击键快捷（标准） |
| 操作 | 快捷键 | 操作 | 快捷键 |
|---|---|---|---|
| 关闭 | Ctrl+W | 下页 | PageDown |
| 复制 | Ctrl+C | 打开 | Ctrl+O |
| 切切 | Ctrl+X | 粘贴 | Ctrl+V |
| 结束 | Ctrl+End | 打印 | Ctrl+P |
| 查找 | Ctrl+F | 上页 | PageUp |
| 帮助 | F1 | 退出 | Ctrl+Q |
| 主页 | Ctrl+Home | 保存 | Ctrl+5 |
| 插入 | Ctrl+Insert | 撤销 | Ctrl+2 |

| 表 2 击键快捷（全局） |
| 操作 | 快捷键 | 操作 | 快捷键 |
|---|---|---|---|
| 执行命令 | Alt+F2 | 切换桌面 5 | Ctrl+F5 |
| 杀死窗口 | Ctrl+Alt+Esc | 切换桌面 6 | Ctrl+F6 |
| 弹出菜单 | Alt+F1 | 切换桌面 7 | Ctrl+F7 |
| 切换桌面 1 | Ctrl+F1 | 切换桌面 8 | Ctrl+F8 |
| 切换桌面 2 | Ctrl+F2 | 任务管理器 | Ctrl+Escape |
| 切换桌面 3 | Ctrl+F3 | 窗口关闭 | Alt+F4 |
| 切换桌面 4 | Ctrl+F4 | 窗口操作菜单 | Alt+F3 |

尽管 MS-DOS 和 Linux 有许多相似的命令，但 Linux 为大部分这些命令提供了额外的参数。

| 表 3 Linux 对比 DOS 命令 |
| Linux 命令 | MS-DOS 等效 | Linux 命令 | MS-DOS 等效 |
|---|---|---|---|
| .. | .. | mkdir | mkdir or md |
| . | . | mv | 移动或重命名 |
| > | > | none | find x y |
| cat x | type | path | none |
| cat y | copy x,y | pr x | none |
| cd | cd | ps | mem / c |
| chmod | chmod or attrib | rm | del x or erase x |
| chown | none | rmdir | rmdir or rd |
| cp | copy | spell | none |
| echo | echo | su | none |
| find x | none | tail x | none |
| head x | none | touch | none |
| lpr x | dir>pr | vi | edit |
| ls | dir | | |
| man x | whoami | | |

## KDE 功能摘要

以下是一些实用的 KDE 工具以及它们所在的菜单列表。

| 工具 | 描述 | 工具 | 描述 |
| --- | --- | --- | --- |
| 主菜单 | | 图形菜单 | |
| kdehelp | KDE 帮助系统 | kfax | 传真预览程序 |
| kcontrol | KDE 控制中心 | kdvi | Tex 预览程序 |
| kfind | 文件搜索工具 | kfract | 分形生成器 |
| 菜单 | | khostview | PostScript 视器 |
| kedit | 一个简单的文本编辑器 | kiconet | 图标编辑器 |
| kwrite | 带有语法高亮的高级编辑器 | kpaint | 绘图程序 |
| 工具菜单 | | ksnapshot | 屏幕截取工具 |
| konsole | 终端模拟器 | kiew | 图片查看器 |
| karm | 个人时间跟踪 | 互联网菜单 | |
| kfloppy | 软盘格式化程序 | kmail | 邮件客户端 |
| kjettool | HP LaserJet 管理工具 | korn | 邮件指示器 |
| kpliq | 打印队列管理 | kppp | 内部查询工具 |
| kmuedit | 任务栏菜单 | krn | 新闻阅读 |
| kworldwatch | 带地图的世界时钟 | karchie | Archie 客户端 |
| kjots | 笔记工具 | kbiff | 新指示器 |
| ark | 归档管理器 | knfer | 网络信息工具 | kmedia | 多媒体播放器 |
| kab | 通讯录 | kmdi | MIDI 文件播放器 |
| kcalc | 计算器 | kmix | 音频混合器工具 |
| kdewizard | KDE 安装向导 | kmid | 卡拉OK 混音器 |
| kdexit | 十进制导出编辑器 | kscd | Audio CD 播放器 |
| klipper | 剪贴板管理器 | 系统菜单 | |
| kmoon | 月相指示器 | arrange | 整理桌面图标 |
| notes | 便利签 | kfontmanager | 字体工具 |
| kodo | 鼠标跟踪器 | kmfsu | 用户模式下的文件管理器 |
| kpage | 软件软件包管理器 | 国际键盘设置 |
| kpm | 进程管理器 | kikbd | 桌面切换器 |
| kvt | 简单的终端模拟器 | pager ktop | 系统负载监控 |

答 使用 KDE 菜单中的 KOAS，或在命令提示符中输入 `useradd`。你也可以输入 `useradd` 或 `adder`。

答 使用 KOAS 用户管理，或在命令提示符中输入 `passwd` 并按回车。或者你可以输入 `passwd [username]` 然后按回车。

使用 KDE CD-ROM 图标，或者在以 root 登录时在命令提示符中输入 `/dev/cdrom /mnt/cdrom` 并按回车。你的 CD-ROM 挂载在 `/mnt/cdrom`，通过切换到该目录即可访问 CD-ROM。

或者，你可以切换到 `/auto/cdrom`，当你回到命令提示符时，你的 CD-ROM 已自动挂载在 `/auto/cdrom`。

如果你是从 `/auto/cdrom` 访问 CD-ROM 的，只需退出该目录即可移除你的 CD-ROM。

## 如何访问我的软盘驱动器？

使用 KDE 软盘图标或在命令提示符中输入 `-t /dev/fd0 /mnt/floppy`。你也可以挂载 `-a /dev/fd0 /mnt/floppy`。切换到 `/mnt/floppy`，你即可访问你的软盘。如果你不想挂载软盘且它是 MS-DOS 格式的文件，可以使用 `mtools`。例如，你可以在命令提示符中输入 `mid a:` 来列出软盘目录。

要使用拷贝，在命令提示符中输入 `mcp a:[filename] [destination_file]`。要删除，使用 `mdel a:[filename]`。

或者，你可以切换到 `/auto/floppy` 目录（就像切换到 `/auto/cdrom` 访问 CD-ROM 一样）。

## 软盘挂载后，移除它安全吗？

不安全！在卸载之前移除软盘会导致数据丢失。确保在移除软盘之前输入 `umount /mnt/floppy`。

阅读附录 B“硬件兼容性列表”第 909 页，或者访问网站 http://www.calderasystems.com/ 查看在线。Xfree86.org 在 http://www.xfree86.org 维护了一份显卡和服务器列表。

使用 `locate [filename]`。

使用 `mount -t type /dev/hda1 /mnt` 允许你从 `/mnt` 访问该分区。

使用以下命令之一：
- `cat [filename]`
- `less [filename]`
- `more [filename]`

使用 `which [command]`。

使用 `man [command]`。

## 在以普通用户登录时如何获取 root shell？

使用 `which [command]`。（注：OCR 文本在此处截断或重复，根据逻辑：可能是“Use which [command]”或类似。实际上，文本显示为：“Use which [command]”）

## 在以普通用户登录时如何获取 root shell？

使用 `which [command]`。（注：提供的 OCR 文本在该标题下显示为“Use which [command]”。）

使用 KOAS 用户管理，或在命令提示符中输入 `passwd` 并按回车。或者你可以输入 `passwd [username]` 然后按回车。

该文本受 Saber Publishing 版权保护。未经出版者明确许可，不得以任何形式复制或分发。联系方式：editor@saber.com

书中提到的所有已知为商标或服务标记的术语均已进行适当的大写处理。我们无法证明这些信息的准确性。在书中使用术语不应被视为对任何商标或服务标记有效性的影响。

我们已尽一切努力使本书尽可能完整和准确，但不隐含任何保证或适用性。所提供的信息基于“按现状”原则。作者和出版者对于因书中包含的信息或因使用随附的 CD 或程序而引起的任何损失或损害，对任何个人或实体均承担责任。

执行编辑
Jeff Koch

策划编辑
Gretchen Ganser

开发编辑
Maureen A. McDaniel

主编
Brice Gosnell

项目编辑
Sara Bosin

文字编辑
JoAnna Kremer

索引员
Heather Goens

校对员
Benjamin Berg

技术编辑
Eric Richardson
Aron Hsiao
Ed Orcutt

软件开发
Dan Sherf

内页与封面设计
Ruth Lewis

布局技术
Brandon Allen
Darin Crone
Stacey Rhiwine-DeRome
Liz Johnston
Timothy Osborn

## 目录

### 引言 1
### 安装要求 24
### 足够的磁盘空间 24
### 充足的内存 (RAM) 25
- 为什么有这么多的人转向 Linux？ 2
### CD-ROM 访问 25
- 稳定性 3
- 功能性 3
### 选择安装方法 25
- 支持 3
### 从 Windows 安装 26
- 自由 4

## 从 CD-ROM 或软盘安装
- 安全 4
### 磁盘 29
### 使用 Lisa 安装 29
- 事情已经发生了变化……很大 4
### LIZARD 安装步骤 29
- 参与进来！4
### 语言选择 30
- 不要害怕学习新东西
### 鼠标检测 31
- 成为新手 5
### 安装目标 31
### 软件包选项 31
- 本书使用的约定 5
### 键盘（型号和布局） 32
### 显卡 32
### 显示器 32
### 视频模式（分辨率和深度） 33
