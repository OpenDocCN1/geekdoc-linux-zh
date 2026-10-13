
- 版本文件, 225

- `-version` 选项 `patch` 命令, 95

- `vfork` 函数, 176

- `vprintf` 函数, 167-168

- 视频属性 (`ncurses`), 444

- 视频卡, 19-22

- 查看器, `XMLviewer` 实现的, 530-536

- 运行, 536

- 查看表内容, 710

- `v-ideo`, 444

- `v-man`, 427

- `v-ideo`, 444

- `vcm`, 453

- `-w` 选项 (`gcc` 命令), 44

- `waitch` 函数, 424

- `waitstr` 函数, 424

- `waitid`, 184-185

- `wait`, 188-189

- `wait`, 189

- `wait`, 185

- `wait`, 188

- `wait`, 188

- `wait`, 569-571

- `wait`, 186, 190

- `wait`, 185

- `wait`, 527

- `wait`, 530-537

- `wait`, 264-265

- `wait`, 260

- `wait`, 261-262

- `wait`, 260

## 零知识系统

## 817

- 事件处理, 468-469

- 事件处理, 473

- `XSelectInput` 函数, 468-469

- 图形初始化, 469-470

- `main` 函数, 471-472

- `XSetWindowAttributes` 结构, 467

- 在线资源, 466

- 示例程序, 471-474

- 窗口，创建, 466-467

- `XtAppInitialize` 函数, 483

- 窗口管理, 466-469

- 映射, 468, `mapping/mapping`, 467

- `XtAppMainLoop` 函数, 481

- `Xfree`, 19

- `XLoadQueryFunction`, 469

- `XtCreatedWidget` 函数, 488

- `X10` 系统, 33

- `XML` (外部标记语言), 528

- `XtDestroyApplicationContext` 函数, 487

- `XCreateGC` 函数, 470

- `XCreateSimpleWindow` 函数, 466-467

- `Expat` 解析器, 529-530

- `text.xml` 示例文件, 529

- `XtGetValues` 函数, 477

- `XtInitialize` 函数, 481

- `XCreateWindowFunction`, 466-467

- 实现 `XMLviewer` 程序, 530-536

- `XtRealizeWidget` 函数, 481

- `XDestroySubWindows` 函数, 486

- `XtValues` 函数, 476

- `XtCreatedManagedWidget`, 486

- `XDestroyWindowfunction`, 486

- 实施 `XMLviewer`, 531, 534

- `endElement` 函数, 531, 470

- `XDrawLine` 函数, 470

- 执行流, 536

- `handleElementName` 函数, 531

- `XDrawString` 函数, 470

- `item_signal_callback`, 531

- `main` 函数, 534

- `XEmacs` (`Lucid Emacs`), 117

- `qtk_container_border_width` 函数, 535

- `qtk_main_quit` 函数, 535

- Y 坐标 (`OpenGL`), 600-601

- `qtk_tree_new` 函数, 535

- `qtk_widget_set_use` 函数, 534

- Z 坐标 (`OpenGL`), 600-601

- 事件处理, 468-469

- `XNextEvent` 函数, 469, 470-470

- `x-y |y|-side-by-side` (`diff` 命令), 95

- `Xlib` 显示指针, 266

- 绘图函数, 470-471

- `-z` 选项 (`tar` 命令), 708

- `XSelectInput` 函数, 468-469

- 图形初始化, 468-470

- 在线资源, 466

- 示例程序默认

- `startElement` 函数, 531-533

- 运行, 536-537

- `XOpenDisplay` 函数, 466

- `draw_bifurcation` 函数, 474

- `XParseColor` 函数, 470

- `xprint` 函数, 167

- Y-Z

## 从 DOS 分区安装

可以从同一台机器上已经安装的 DOS 分区中安装 Debian。

1. 将以下文件拷贝到你 DOS 分区的目录中：`resc140.bin`, `drv140.bin`, `base2_1.tgz`, `root.bin`, `linux`, `install.bat` 和 `loadlin.exe`。

2. 启动到 DOS（而不是 Windows），且不加载任何驱动程序。要做到这一点，你必须在准确的时机按下 F8。

3. 在 DOS 目录中执行 `install.bat`。

## 从 DOS、Windows 或 OS/2 写入磁盘镜像

你可以在软磁盘镜像文件相同的目录下找到 `rawwrite2.exe` 程序。还有一个名为 `rawwrite2.txt` 文件，其中包含使用 `rawwrite2` 的说明。

要将软磁盘镜像文件写入软磁盘，请先确保你已启动到 DOS。许多报告提到，尝试在 Windows 内部的 DOS 窗口中使用 `rawwrite2` 时会出现问题。据报道，在 Windows 资源管理器中双击 `rawwrite2` 也无法工作。如果你不知道如何启动到 DOS，只需在启动时按 F8。

1. 一旦启动到纯 DOS，使用命令 `rawwrite2 -f file`，其中 `file` 是一个软磁盘镜像文件之一，且 `drive` 为 `a:` 或 `b:`，取决于你正在写入哪个驱动器。你将使用 `resc140.bin` 和 `root.bin` 镜像来设置你的启动盘。

2. 使用带有 A 盘的启动盘重启电脑。安装程序将自动启动。

## 安装 Debian GNU/Linux 2.1

启动 Debian 安装系统（第一步）可以通过以下媒体之一完成：

- 可启动的光盘 (`CD-ROM`)

- 运行在另一个操作系统中的启动程序

- 可启动的软磁盘

首先，选择启动媒体。接下来，选择你将用于安装基础系统的方法。如果你有一张可启动的光盘，并且你的系统支持从光盘启动。

## 关于作者

Kurt Wall 自 1993 年起一直使用 Linux。他住在犹他州的盐湖城，是 Salt Lake Group 的成员。他是一位自学计算机工程师。他的工作涵盖了学术、企业和军事领域，包括安全、网络管理、开发应用程序、设备驱动程序、客户端/服务器应用程序以及仿真。他不使用 Windows。Mark Watson 住在亚利桑那州的塞德纳，和他的妻子一起散步。他喜欢音乐、烹饪和下棋。他拥有自己的公司 Free Labs，并在 Digital Design 工作。他是一名人工智能工程师，使用 Linux 超过十年。他是 International User Group 的成员，是总裁。他和他的妻子一起在塞德纳徒步，喜欢电子产品。Mark Whitis 是 Intelligences 的高级软件工程师。他是许多可用软件的作者。

## 献辞

Kurt Wall: 献给 Ashleigh Rae 和 Zane Thomas。

Mark Watson: 致 Julie、Josh 和 Calvin。

Mark Whitis

## 致谢

Kurt Wall：我要感谢所有对这本书负责的人。感谢 Nick Wells 让我参与了这条看似无害的帖子。感谢 `comp.linux.*`、`comp.lang.c` 和 `comp.unix.programmer` 的各位回答了无尽的问题。Thomas Dickie 慷慨地审阅了关于 `curses` 的章节。

我的家人，爸爸、Rick、Amy、Morgan、Jennifer、Candy、Chris、Marty、Ashleigh、Zane 和 Patsy，在我写书期间生活混乱时支持了我。对于持续的支持和精神鼓励，我深谢 Tricia、Joan、Steve、Allen、Tineke、Renee 和各位。我现在理解为什么作者总是感谢他们的编辑了（我不知道竟然涉及这么多编辑！）。
