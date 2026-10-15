
在某些情况下——例如如果你使用 `tar` 而不是 `rpm` 安装单个包——尽管缺失的文件存在，`rpm` 仍然会抱怨未满足的依赖关系（它们只是在 `rpm` 数据库中缺失）。在这种情况下，

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_644_0.png)

| 路径: | | 查询 | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 守护进程 | Shell | X | 文档 | 应用程序 | 卸载 |
| 开发 | 基础 | 库 | 工具 | 网络 | 可用 |
| 已选包: 0 | | | | | 退出 |

图 A.2 `glint` 按类别对包分组。

# 620 附录 A：`REDHAT` 4.1

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_645.png)

图 A.3 包列表。

你可以使用 `--nodeps` 强制安装或卸载。但请仅在你确切知道做什么时使用此选项！

# 图形化 Linux 安装工具 (`glint`)

虽然 `rpm` 并不容易处理，但有一个更优雅的解决方案！`X` 程序 `glint` 允许通过鼠标点击安装/卸载。`glint` 显示所有已安装的包，包按层级结构排列，有时很难跟进。

当你找不到某个包，但确定它已安装时，可以通过 `rpm` 了解 `glint` 的层级结构。例如，`rpm -ai pert` 提供了已安装 Perl 包的简短描述。组行指定了 Perl 的位置（实际上在 `Utilities/Text` 下，而不是你预期的位置）。此外，`glint` 的层级结构与你在首次安装时可以选择的组件无关！

在主窗口中，你现在可以使用鼠标在 `glint` 层级结构中移动。可以通过点击选择单个包。再次点击取消选择。通过右键，你还可以选择/取消选择所有组（例如，所有 `X11` 包）。

你可以对选定的包应用三种不同的操作：`QUERY`、`VERIFY` 和 `UNINSTALL`。

`QUERY` 显示此包中所有文件的列表。配置文件用字母 `C` 标记，包含在线文档的文件用 `D` 标记。`D` 标记有时是不完整的；文本经常被排除。）未记录 `Details`。包窗口包含了有关包的附加信息（空间范围、来源、版本和发行号等）。

通过 `VERIFY`，你可以检查与原始安装相比是否有文件发生了变化或缺失。然而，`glint` 并没有提供（重）安装单个文件的方法。你只能卸载整个包然后从头开始安装。

# 图形化 Linux 安装工具 621

`UNINSTALL` 移除所有属于选中包的文件。（多个包同时使用的文件只有在最后一个包卸载时才会被删除。）

如果你想进行更新，不要执行 `UNINSTALL`。选择包的新版本，安装并执行 `UPGRADE`。这样做的好处是为所有修改的配置文件创建备份（扩展名为 `*.rpmsave`）。

# 使用 `glint` 安装新包

到目前，`glint` 的描述专门指代已安装的包。如果你想安装新包或更新现有包，必须首先使用 `AVAILABLE` 命令生成所有可用包的列表。这会导致 `glint` 列出 `/cdrom/RedHat/RPMS`。可能会出现依赖列表、库名、包名以及所谓的虚拟包名。因此，搜索所需包的方法如下：

(Wait, the text is highly redundant/repeated in the source provided).

# `Caldera Network Desktop` 1.0

# `APPENDIX B`

The `Caldera` 1.0 Linux distribution is the same as `RedHat` 2.1, improved with a more elegant installation and a number of commercial components. During installation, `Caldera` 1.0 behaves just like `LST` 2.1 (only boot diskette, generic kernel) – therefore much of the information also applies to `LST` distribution. After installation, the tools known from `RedHat` 2.1 are available for further configuration (see Appendix A).

### `Caldera Open Linux`

When this reaches the bookshelves this appendix will unfortunately be out date. The new version of `Caldera LINUX` will then be called ‘`Caldera Open Linux`’ (in short, `COL`). Unfortunately, `Caldera` was not able (or willing) to supply a version in good for updating this appendix. `COL` will no longer be based on `RedHat`, but on a new version of the German `LST` distribution. The essential advantage will be that the excellent `LISA` installation program can also be used as a configuration tool during normal `Caldera` operation. `COL` will be available in several versions: base, workstation, and server. More up-to-date information can be found under the following addresses:

`www.redhat.com`
`www.lst.de`

# Installation

`Caldera LINUX` comes with two diskettes, one for systems with `IDE` hard disks (possibly `PCMIA` cards), the second for systems with `SCSI` hard disks (without `PCMIA`). Usually, you boot with one of the two diskettes. During booting, you can specify additional boot parameters, if required (see page 46). Prior to login, you can activate a non-US keyboard table.

As soon as the login prompt appears, you can log in as `install`. (Parallel to this, you can log in on a second console as `help` and read various help texts or play a round of Tetris. This is a luxury that other distributions should think about offering!)

### `LISA`（Linux 安装与系统管理）安装程序

`LISA`（Linux 安装与系统管理）安装程序会显示硬件信息。你现在必须指定从何处读取安装数据（本地 CD-ROM 驱动器、硬盘或 `NFS`）。如果你选择 CD 变体，`LISA` 现在将加载必要的内核模块。如果发生问题，你可以为相关模块指定启动参数（如果第一次运行不起，请重试——通常系统不会崩溃）。

当你必须为 `LISA` 的安装创建一个根分区时，情况将会变得更加复杂；在这种情况下，你必须使用 `LISA` 和 `fdisk`（参见第 33 页）。返回 `LISA` 后，你可以指定 `Caldera` 要安装在哪个分区中。`警告：`此分区将被细分；所有可能存在的数据都将被彻底删除。随后将创建一个 `LISA` 文件系统。

接下来，你可以指定安装大小：（最小 `minimal`、标准 `standard` 或完整 `complete`），仅需提供三种变体（最小 `minimal`、600/200 兆字节），并强烈建议使用标准变体。如果有疑问，安装得少总比安装得多要好——你可以在以后的任何阶段单独安装任何包。`LISA` 现在调用 `rim` 进行包安装，并通过进度条在屏幕上显示安装状态。

安装的最后一部分允许你执行各种基础配置步骤：计算机名称、时间、交换分区、网络配置、创建启动软盘、`Xside` 服务器配置、`LILO` 配置。这些配置步骤中的大多数可以在以后在 `Caldera LINUX` 正常运行期间的后期阶段完成。（特别是，你应该推迟 `LILO` 配置——参见第 165 页。）

`LISA` 仅在首次安装时可用的事实令人恼恼。当 `Caldera` 运行后，`LISA` 无法再次使用（缺少了几个菜单）。使用启动软盘重启并不会导致预期的结果，因为只有在完全安装后你才能使用 `LISA` 进行配置。显然，对于 `Caldera` 的大部分配置工作，提供了易于处理的 `X` 程序供使用（特别是针对用户、网络和打印机配置），但在某些情况下，你将不得不手动编辑配置文件（参见第 6 章）。无论如何，从 `LISA` 突然切换到完全不同的工具在逻辑上是不连贯的。恢复原始配置文件只能通过重新安装来实现。

完成安装后，计算机将重启（使用新的启动软盘）。如果你以 `root` 身份登录，则必须为 `root` 指定一个密码并注册一个额外的用户（带有密码）。

然后你可以开始启动 `X` 窗口系统，你会发现自己处于由“`Looking Glass`”桌面工具主导的图形界面中。本质上，`Looking Glass` 是一个易于处理（但也有些独特）的程序和程序管理器。

当你以 `root` 身份启动 `X` 时，桌面提供了各种用于系统配置的 `X` 程序：`ftools`, `glint`, `netcfg`, `printtool`, `timetout` 和 `usercfg`。这些程序来自 `RedHat` 2.1，描述在第 61 页。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_648_0.png)

# 配置

### 键盘、特殊字符

尽管到目前为止安装非常顺利，但仍有几件事需要完成。文本控制台和 `X` 窗口 (`xterm`) 中的键盘支持都非常有限（没有变音符号和重音，没有 `Del`、`Home`、`End` 等）。显示外语言特殊字符更少，`Emacs` 既不显示也不允许输入它们，等等。修复这些恼人缺点的配置步骤在第 6 章中从第 125 页开始。

`Caldera` 基于的 `RedHat` 发行版中的一个 Bug 防止了在 `netcfg`、`fsoot` 等配置程序中支持 `Del` 键。两次使用 `/usr/lib/rhs/config-panel/bindings` 会导致指令 `bind <Del> Edit <Backspace>`。当你注释掉这些 `Backspace` 指令时，`Del` 就能正常工作。（前提是你最初已经正确设置了键盘。）

# 在文本模式下工作

除了 `Crisp`（可以通过 `cr` 在文本模式下启动）之外，标准安装只设置了难以处理的 `vi` 编辑器。如果你不想用 `Crisp` 进行工作，你应该现在使用 `glit` 来设置另一个编辑器（`/etc/distrib` 包含了 `jed`, `joe` 和 `emacs`）。你还应该在 `/etc/rc/rc.local` 中启动 `gpm` 程序（参见第 133 页），以便使用鼠标处理文本。

如果你想使用 50 行模式，你必须忽略 `XInside` 服务器而改为配置 `XFree8` 服务器（第 190 页），因为 `XInside` 服务器在从 `X` 切换到控制台时总是切换到 25 行模式。

# 登录

如果你对文本模式不感兴趣，也可以这样配置 `Caldera`，使得在计算机启动时直接出现 `X` 登录。只需更改 `/etc/initabb` 中的一行即可（默认设置是 3 而不是 5）。
