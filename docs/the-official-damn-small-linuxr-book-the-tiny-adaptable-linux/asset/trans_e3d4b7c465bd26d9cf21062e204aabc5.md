

## 基于终端的应用程序

Damn Small Linux 也有许多基于终端的程序。许多新手 Linux 用户对基于文本的应用程序感到畏惧，但很多人发现有些事情在终端窗口中做起来更简单。如果你是 Linux 新手，不妨给自己一个机会试试这些应用程序。你可能会发现它们的简洁令人愉快。

### ftp—一个基础的基于终端的 FTP 程序

ftp 工具其实非常容易使用。许多导航和观察命令与常规终端功能相同。例如，输入 ls 可以列出目录中可用的文件，或输入 pwd 查看当前工作环境。如果卡住了，只需输入 help 即可获得命令列表。如果需要了解某个命令的作用，只需输入 help command（将 command 替换为你感兴趣的命令名称）。

### index—个人数据库管理系统

Index 是一个极简的数据库管理系统。作者希望 Index 能被那些想要维护个人信息的数据库的用户使用。Index 易于设置和使用。只需简单输入 index 命令即可启动。

默认情况下，Index 开始时提供四个空数据库。有企业电话数据库（bphone）、用于保存你的 CD 收藏的数据库（cdlist）、用于保存你想要的 CD 的数据库（cdwantlist），以及个人电话数据库（pphone）。

输入你想要使用的数据库名称。然后你可以使用 Index 添加条目（a）、在数据库中查找条目（f）、以及逐条读取数据库（r）。完成后，输入 s 保存修改，q 保存并退出，或 x 退出。

### CDW CD 刻录应用程序

CDW 是使用 cdrecord 和 mkisofs 的更友好方式，它具有基于 ncurses 的 GUI。虽然熟悉命令后使用起来很容易，但 CDW 的用户应参考 README 以学习所有关键功能。要启动 CDW，输入 cdw 命令。

图 3-9 显示了 CDW 界面的示例。我们在 http://damnsmalllinux.org/docs/cdw_README.txt 有可用的主要 README 页面。

图 3-9 使用 CDW 界面复制和刻录 CD。

![](img/af53325d7f38f1cdafca9f44568e4ab8_84_0.png)

### Microcom 串行终端仿真器

Microcom 是一个类似 Minicom 的串行仿真器，支持脚本。Microcom 非常小巧（14k），因为它是为了适应基于软盘的 Linux 发行版而编写的。你可以通过输入 microcom 命令启动 Microcom。有关 Microcom 的更多信息，请访问其主页：

http://microcom.port5.com

### Midnight Commander 文件管理器

Midnight Commander（或简称为 mc）是一个非常强大且流行的文本模式文件管理器。由于 mc 既可本地也可远程使用，它深受 Linux 爱好者的喜爱。记得 Norton Commander 的老 DOS 用户会发现 MC 非常舒适，因为它采用双面板布局。

图 3-10 显示了 Midnight Commander 界面的示例。请在此处参考 Midnight Commander 信息页面：www.ibiblio.org/mc。

图 3-10 使用 Midnight Commander 在文本模式下管理文件。

![](img/af53325d7f38f1cdafca9f44568e4ab8_84_1.png)

### Naim—一个基于控制台的 AIM、ICQ、IRC 和 Lily CMC 客户端

Naim 是一个用户友好的基于文本的即时消息和 IRC 客户端。你可以从桌面启动它（选择 Apps、Net、AIM/IRC/ICQ、AIM）或从命令行启动（输入 naim 命令）。我们在 Fluxbox 菜单中有 IRC 命令，可让你直接接入 DSL IRC 频道。因此，如果你有快速问题，请选择 Apps、Net、AIM/IRC/ICQ、nIRC #DamnSmallLinux。

快速开始 Naim，请查看 http://naim.n.ml.org/quickstart。

### Nano—一个简单的基于终端的文本编辑器

Nano 是著名 Pico 编辑器的 GNU 克隆，不过有一些改进使其更适合编码。改进包括正则表达式搜索和替换以及自动缩进。与 Pico 一样，Nano 异常易于使用。

Nano 的主页位于 www.nano-editor.org。

### Netrik—一个极简文本浏览器

根据作者的说法，“Netrik 是 ANTRIK Internet 查看器/浏览器/资源管理器/导航器/无论什么。” Netrik 对我们的 net-man 和 web-dictionary 应用程序至关重要。我们需要一个能够渲染 HTML，同时又足够小以不挤占其他应用程序的东西。Netrik 证明非常适合这项工作。令我们 DSL 惊讶的是，Netrik 的大小仅为 79.3Kbytes。

访问 Netrik 主页 http://netrik.sourceforge.net/。

### smbclient—Windows 文件共享的命令行客户端

smbclient 允许你以类似 FTP 的交互方式连接到 Microsoft Windows 共享网络。

有关 smbclient 的信息，请参考其手册页：

http://samba.org/samba/docs/man/manpages-3/smbclient.1.html

### SQLite—一个小型、自包含的 SQL 关系数据库管理系统

SQLite 小巧、稳定、可嵌入且快速。SQLite 附带一个独立的命令行程序，可在 DSL 中整合到 Bash 或 Perl 脚本中。我们还通过 murgaLua 为 SQLite 提供了 Lua 绑定。

我们有一个用 Perl 编写的个人信息管理器，它依赖 SQLite 进行后端数据库管理。

有关更多信息，请参考 SQLite 主页：www.sqlite.org。

### Vi(m)—一个高级基于终端的文本编辑器

许多人声称使用 Vim 是编辑文档最高效的方式。确实，Vim 的高级功能需要时间掌握，但在你将其记在脑中后，如此多的编辑能力触手可及，你无需将手指移离键盘。

Vim 的基本命令其实并不复杂。要查看基本命令的良好列表，请参考此 URL：http://www.selectorweb.com/vi.html。

