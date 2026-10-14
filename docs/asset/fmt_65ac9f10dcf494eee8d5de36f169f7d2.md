
![](img/078622fac3fd61e5a0c895da1d3eff96_221_0.png)

图 11.13 使用“备份文件夹”字段和“定时文档”复选框，在使用 WordPerfect 9 时启用备份文档的自动保存。

### 设置备份偏好

要创建备份文档，请勾选始终创建备份（Always Create Backup）复选框。你可以指定 StarOffice 自动保存文档的时间间隔（分钟），可以让 StarOffice 提示保存文档。你还可以使用“选项”对话框更改 Internet、浏览、文字处理（如显示特性）、HTML 编辑、电子表格、演示文稿和图形的设置。

## 免费应用程序套

`GUILG00.GZ` `b_ins00` `b_req01` `g_req01` `g_us00`

`Readme` `b_ins01` `b_us01` `g_req02` `g_us01`

`Runme` `b_req00` `g_req00` `g_req03`

要开始安装，请以 `root` 身份登录，并如下使用 `.Runme` 脚本：

```
### .Runme
```

按下回车键后，安装脚本开始运行。如果你的系统支持图形化安装，将看到一个对话框，引导你完成安装过程。如果你的系统不支持图形化安装，程序将使用文本界面向你提问，如图 11.14 所示。

如果你的系统支持图形化安装，你将看到如图 11.15 所示的启动屏幕。

安装程序要求你接受许可条款，允许你指定安装目录（大多数用户选择使用 `/opt/wp8`）和安装类型。完整安装大约需要 70MB 的硬盘空间。

![](img/078622fac3fd61e5a0c895da1d3eff96_222_0.png)

**图 11.14** 免费 WordPerfect 8 安装界面可以是图形化或文本的，取决于你的系统。

## 安装 WordPerfect 遇到问题？

如果你发现 WordPerfect 安装程序失败，请确保你的 Linux 系统已安装 `libc5-compatibility libraries`。WordPerfect 依赖于旧版本的软件库，而某些现代 Linux 发行版并未安装这些库。

## 第 11 章：流行的 X11 客户端

### 安装配置

![](img/078622fac3fd61e5a0c895da1d3eff96_223_0.png)

图 11.15 适用于 Linux 的免费 WordPerfect 8 图形化安装提供了一种更简单的 Linux 版 WordPerfect 8 安装方法。

继续进行安装，并安装任何所需的打印机驱动程序。此时你可以安装所有打印机驱动程序而不会浪费硬盘空间，尽管许多 Linux 系统只需要一个名为 Passthrough Post-Script 的打印机驱动程序。完成安装选择后，安装进度非常快，并根据你的系统在一或两分钟内完成编译。安装完成后，你可以像这样启动你的 WordPerfect 版本：

```
# /opt/wp8/wpbin/xop &
```

按下回车键后，你将看到如图 11.16 所示的 WordPerfect 主窗口。

屏幕要求你输入许可密钥，以便在你的系统上无限使用 WordPerfect。你可以通过访问 http://venus.corel.com/nasaps/wp8linuxux/register.html 获取此免费密钥。应用程序要求你输入某些信息并立即显示许可密钥。

### 设置打印

要在你的 Linux 系统上启用打印功能，启动 WordPerfect，然后从 File（文件）菜单中选择 Print（打印）项。你将看到如图 11.17 所示的打印对话框。

点击对话框顶部的 Select（选择）按钮。你会看到 Select Printer（选择打印机）对话框。点击其 Printer Create/Edit（打印机创建/编辑）按钮，然后在 Printer Create/Edit 对话框中点击 Add（添加）按钮。在 Add Printer Drive 驱动中选择 Passthrough PostScript 打印机驱动程序，一直点击 OK 直到进入 Printer/Create 对话框。

![](img/078622fac3fd61e5a0c895da1d3eff96_224_0.png)

**图 11.16** 你可以从 Corel, Inc. 为你的 Linux 版 WordPerfect 8 获取免费的许可密钥。

![](img/078622fac3fd61e5a0c895da1d3eff96_224_1.png)

**图 11.17** 使用打印对话框在 Linux 版 WordPerfect 8 下设置打印。

随后你将选择目标为 None 的 Passthrough PostScript 驱动。点击 Setup（设置）按钮，然后点击 Destination（目标）按钮并选择系统的默认打印机。随后出现 Select Printer 对话框，如图 11.18 所示，显示为你的打印机选了 Passthrough PostScript 驱动。

### 效率客户端

KDE 环境包含了许多你可以使用的客户端。最流行的工具之一 `pilot-link` 软件套件为许多 XFree86、Palm 和 Linux 的图形化客户端提供了基础。

### KDE 客户端

本节介绍了若干用于 Palm 的客户端。

### GNOME 客户端

Linux 的 GNOME 桌面也包含许多客户端。表 11.3 列出了常见客户端。

### 表 11.3 KDE 客户端

| 名称 | 描述 |
| :--- | :--- |
| `kab` | 地址簿客户端 |
| `ketime` | 时间跟踪客户端 |
| `kcalc` | 计算器客户端 |
| `kminfo` | 系统信息 |
| `kedit` | 简单文本编辑器 |
| `kfinger` | GUI 客户端 |
| `fsstatus` | 文件系统监控 |
| `gless` | GNOME 文本浏览器 |
| `klipper` | 剪贴板 |
| `kmag` | 显示放大 |

### Palm PDA 客户端

在 Linux 下有许多适用于 Palm PDA 的 Linux 程序和客户端。由于 Palm Computing 良好的硬件设计、与开发者的开放关系、文档、源码以及操作系统接口的可用性，Palm PDA 已成为手持计算市场的巨大成功。

### 表 11.5 pilot-link Palm 效率程序

| 名称 | 描述 |
| --- | --- |
| `addresses` | 创建 PDA 地址的文本文件 |
| `install-datebook` | 将日历数据更新到 PDA |
| `install-memo` | 将备录上传到 PDA |
| `install-todos` | 将待办事项列表更新到 PDA |
