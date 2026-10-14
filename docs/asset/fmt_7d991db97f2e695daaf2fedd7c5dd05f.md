
KOrganizer 是 KDE 提供的日历和待办列表小部件。它相当简单，工作方式与其他 Gnome Calendar 或 Ical 类似。KOrganizer 使用 vCalendar 文件格式作为其原生文件格式。这允许与其他程序进行日历交换。

用于同步日历的实用。KOrganizer 还提供了导入 Ical 日历的功能。

## 获取和安装 KOrganizer

KOrganizer 随 KDE 标准发行版捆绑。因此，当我在 SuSE 上使用 KDE 作为桌面环境时，我可以使用 KOrganizer。

## 使用 KOrganizer

由于 KOrganizer 是随 KDE 默认安装的，我也可以通过 KDE 菜单项启动该程序。你也可以从桌面图标通过 X-Terminal 终端的命令行启动 KOrganizer。该程序具有许多实用的命令行选项，例如 `-geometry` 选项，它允许你在打开 KOrganizer 时指定其 own。使用 `korganizer -h` 可以获取可用命令行选项列表。

图 28.23 显示了 KOrganizer 的用户界面，我在其中输入了一个派对的预约，还添加了几个“待办”事项。要输入预约，只需点击预约或会议时间所在区域的行内即可。然后你就可以输入关于 $a$ 会议的信息。在输入预约时添加更多细节，你可以从工具栏选择“操作 (Action)”，然后选择“新预约 (New Appointment)”。此选项将打开详细的预约窗口，如图 28.24 所示。

图 28.23

KOrganizer 的用户界面。

![](img/cbac72550c7126a22162e94d91a0c360_936_0.png)

图 28.24

Korganizer 的详细预约窗口。

在此窗口中，你可以为预约或事件添加广泛的细节和备注，并设置闹钟提醒自己。在底部，注意“类别 (Categories)”按钮允许你为事件分配类别。图 28.25 显示了为预约分配的类别。

图 28.25

KOrganizer 类别。

![](img/cbac72550c7126a22162e94d91a0c360_937_0.png)

![](img/cbac72550c7126a22162e94d91a0c360_937_1.png)

## KOrganizer 选项

与其他 KDE 小部件一样，它有一系列简单的配置选项。从工具栏选择“选项 (Options)”，然后选择“编辑选项 (Edit Options)”。图 28.26 显示了选项界面。要更改特定区域的选项（例如 KOrganizer 使用的字体或颜色），点击窗口左侧的相应选项。窗口右侧将显示可用选项。更改后，选择“应用 (Apply)”或“确定 (OK)”保存更改。“取消”将退出而不保存更改，除非你已经选择了“应用”按钮。

图 28.26

Korganizer 配置选项。

![](img/cbac72550c7126a22162e94d91a0c360_938_0.png)

## Gnome Calendar

Gnome Calendar 是一个非常基础的日历程序，有一个显著特性：它支持 vCalendar 标准。这允许在互联网上交换日历信息。Gnome Calendar 甚至使用 vCalendar 格式作为在硬盘上存储数据的格式（见图 28.27）。根据 Gnome 网站，Gnome Calendar 还处于起步阶段。未来，请期待许多新功能。

图 28.27

Gnome Calendar。

![](img/cbac72550c7126a22162e94d91a0c360_939_0.png)

## 获取和配置 Gnome Calendar

Gnome Calendar 作为我的 Gnome 桌面包的一部分提供的。它也可以从 Gnome 网站（http://www.gnome.org）获取。你可以在那里获取该程序的最新版本。

可用的配置较少。图 28.28 显示了简单的配置工具。使用“设置 (Settings)”，然后选择“偏好设置 (Preferences)”进入。

> 注意
>
> 请访问互联网邮件联盟网站（http://www.imc.org）以获取更多关于 vCalendar 标准的详细信息。

图 28.28

Gnome 日历偏好。

![](img/cbac72550c7126a22162e94d91a0c360_939_1.png)

## 使用日历

向日历添加条目非常简单——只需点击预约时间并开始输入。如要添加新条目并使用更多 Gnome Calendar 功能，可以点击工具栏上的“新建 (New)”图标，或者选择“编辑 (Edit)”，然后选择“新预约 (New Appointment)”。图 28.29 显示了正在创建一个新预约。

图 28.29

在 Gnome Calendar 中创建预约。

![](img/cbac72550c7126a22162e94d91a0c360_940_0.png)

查看日历时，使用工具栏下方的标签切换视图。你可以查看日、周、月或年的日历。

## Ical

Ical 是一个日历/预约工具，与 Gnome Calendar 程序非常相似。Ical 使用 C++ 结合 tcl 库实现。用户界面（见图 28.30）非常易用且运行良好。

使用“选项 (Option)”菜单项进行配置非常快速。一个很棒的特性是在许多配置屏幕中使用了滑块。（见图 28.31。）使用滑块进行数值调整。

图 28.30

Ical 日历。

![](img/cbac72550c7126a22162e94d91a0c360_941_0.png)

图 28.31

Ical 配置。

![](img/cbac72550c7126a22162e94d91a0c360_941_1.png)

## rclock

rclock 是一个非常简单的钟（见图 28.32），在 Linux 上可用并可以安装。

图 28.32

Windows 版 rclock。

![](img/cbac72550c7126a22162e94d91a0c360_942_0.png)

# 使用 DOSEMU 模拟 DOS

DOSEMU 基于 Matthias Lautner 的早期工作，目前由 Hans Lermen 维护。根据作者的说法，它不是一个模拟器，而是一个 DOS 虚拟机。这意味着该程序在你的系统内存中创建了一台虚拟计算机。使用 DOSEMU 需要购买 MS-DOS 吗？当然不需要！它包含了一份 Pat Villani 的 FreeDOS 副本（实际上是位于 `/var/lib/dosemu` 目录下的一组 DOS 命令集合）。你会发现其中包含了许多熟悉的 DOS 程序。

可以在 Linux 控制台的命令行中使用 DOSEMU，也可以在 X 会话期间在其窗口中启动它。主配置文件 `global.conf` 位于 `/var/lib/dosemu` 目录下。然而，要配置系统级设置，请编辑 `/etc/dosemu.conf` 文件。你可以自由配置 DOSEMU 的工作方式。

在 Linux 下，任何用户都可以启动 DOSEMU（版本为 dosemu-0.9.8.0，位于 `/usr/bin` 目录）。你可以从控制台命令行或 X11 窗口启动该程序。如果你正在运行 X11 会话，可以如下所示在终端内启动 DOS 会话：

```bash
# dos
```

你也可以使用以下任意命令行之一在独立的 X11 终端窗口中启动 DOS 会话：

```bash
# xdos
# dos -X
```

你将看到一个 DOS 会话免费启动，如图 29.1 所示。

![](img/cbac72550c7126a22162e94d91a0c360_946_0.png)

# 图形、多媒体和生产力工具

当 DOSEMU 启动时，它将使用 `/etc/dosemu.conf` 中指定的配置。

你会在 `/etc` 目录下找到三个 DOSEMU 文件和一个符号链接：

- `dosemu.conf`：系统级 DOSEMU 运行时配置文件，包含近 100 个控制 DOSEMU 运行的设置。
- `dosemu.users`：指向 `dosemu.users.secure` 的符号链接。
- `dosemu.users.easy`：用户配置文件，允许大多数用户访问 DOSEMU 功能。
- `dosemu.users.secure`：用户配置文件，限制用户对文件或卷的读写权限。

基本上，访问权限定义在 DOSEMU 用户配置文件中，而运行时选项定义在 DOSEMU 的配置文件中。你还可以在家目录下定义一个 `.dosemu` 文件来包含本地配置设置（例如拥有私有的 DOS 启动盘或硬盘镜像）。要为你的系统自定义配置 DOSEMU，请使用你喜欢的文本编辑器以 root 身份编辑 `dosemu.conf` 文件。该文件中的设置包括：

- CPU 类型和速度
- 内存可用性
- 扬声器声音控制
- 终端颜色控制
- X11 窗口配置（如颜色深度、光标和鼠标）
- 硬件配置（软驱、鼠标、串口、并行口）
- 硬盘镜像设置

DOSEMU 硬盘镜像设置开始于

```
$_hdimage =
```
