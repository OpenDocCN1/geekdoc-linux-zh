
#define CONFIG_NEW_WINDOW_COMMAND "xterm"

...

***PD: End

```
你可以通过编辑文件的另一部分来选择颜色：
```

...

******PD: Begin

#define CONFIG_TAB_FOREGROUND "black"

#define CONFIG_TAB_BACKGROUND "gray80"

#define CONFIG_FRAME_BACKGROUND "gray95"

#define CONFIG_BUTTON_BACKGROUND "gray95"

#define CONFIG_BORDERS "black"

#define CONFIG_MENU_FOREGROUND "black"

#define CONFIG_MENU_BACKGROUND "gray80"

#define CONFIG_MENU_BORDERS "black"

...
```

编译 `wm2` 后，将 `wm2` 插入家目录下的 `.xinitrc` 文件。你也可以在启动 X 会话之前使用 `xsetroot` 命令设置背景，如下：

```
xsetroot -solid lightblue

wm2
```

### 资源信息

- http://www.fvwm.org—fvwm 窗口管理器主页。
- ftp://mitac11.uia.ac.be/html-test/fvwm95.html—fvwm95 窗口管理器主页。
- http://www.kde.org—K 环境的主页以及获取更多信息的地方。你也可以下载 beta 或更新（但更新）...
- http://www.enlightenment.org—Enlightenment 主页。
- http://www.gnome.org—GNOME 主页以及获取更多信息的地方。
- http://www.afterstep.org—AfterStep 主页。
- http://www.windowmaker.org—Window Maker 主页。
- http://www.lessTif.org—LessTif 主页。
- http://www.xfree86.org—XFree86 主页。
- http://www.sawfish.org—sawfish 主页。
- http://www.mlvm.org—mlvm 主页。
- http://www.wm2.org—wm2 主页。

### 安装 XFree86 开发组件

- 应用补丁。如果你需要自定义特定的驱动程序，请按照指示应用补丁。你将需要 `patch` 命令，可能还需要 `diff` 命令。通常会有一些你可能在构建之前想要应用的额外补丁。

- 配置。你需要对源码进行配置以供 Linux 使用。配置文件包含了你需要在开始构建之前指定的各种标志位（设置）。

- 编译。根据 Open Group 开放组织（The Open Group）的规定，你不能使用 GNU `gcc` 编译器版本 2.5、2.51 或 2.5.2 来构建软件。此外，Red Hat Linux 的版本包含 `gcc` 编译器的开发版本，即使在具有兼容软件库的情况下，它也可能无法构建可移植二进制文件。如果可能，你应该使用最新稳定版本。本章测试构建时使用的编译器是 `gcc` 2.95.2 版本，运行在内核为 2.2.14-15mdk 的 Mandrake Linux（Mandrake 7.0）上。

- 其他注意事项。如果你的 Linux 分发版具有损坏的运行时加载器，你可能会在链接库时遇到问题。GNU `make` 命令不兼容；XFree86 源码包含一个将被构建并使用的 `make` 命令。根据 Open Group 的规定，GNU `as` 汇编器和 `id` 链接器不受支持或无法用于重构 X（尽管构建和生成的二进制文件在本章的测试系统上运行良好）。重构服务器和 X 客户端将使用新的库名称，即使你构建的版本与安装的版本相匹配；根据 Open Group 的建议，推荐的方法是通过符号链接将旧库链接到新库来安装新库。

### 下载源码包

你可以通过多种方式获取 XFree86 的源码。最简单的方法之一是通过 FTP 从 http://ftp.xfree86.org/pub/XFree86/4.0.1/source 下载文件。你将找到以下文件：

- `FILES`—每个存档中所有文件的列表
- `SUMS.md5`—文件的校验和，以确保有效性
- `SUMS.md5sum`—存档的校验和，以确保完整性
- `X401src-1.tgz`—XFree86 服务器、客户端、文档、库和贡献客户端的源码
- `X401src-2.tgz`—XFree86 字体和字体实用程序
- `X401src-3.tgz`—XFree86 质印文档
- `doctools-1.2.tgz`—文档创建工具

# 第 17 章：构建 X11

XFree86 4.0.1 源码发行版包含超过 11,000 个文件。你至少需要 53MB 来存储压缩包和文件。解压后，源码需要 227MB 以上的硬盘空间。根据 XFree86 者的说法，如果你系统中已经安装了 X11 字体，可以只使用第一个存档（`X401src-1.tgz`）。文档工具包用于格式化 XFree86 文档（包括页面）。

获取最新进展版本（而不是像 4.0.1 那样的点发行）的另一种方法是使用 XFree86 的并发版本系统 CVS。虽然最新发布可能非常重要，特别是当你知道某个新功能或驱动程序的发布可以帮助你解决图形系统 X 中困扰已久的问题时，但并不总是建议从 CVS 仓库使用或构建 XFree86。除非标记为“stable（稳定）”，否则分发版将处于开发阶段，并可能存在一些棘手的 bug。

要直接从 XFree86 开发者的工作目录下载当前快照，请使用 `cvs` 命令登录远程 XFree86 CVS 目录：

```bash
$ cvs -d pserver:anoncvs@anoncvs.xfree86.org:/cvs log in
```

(登录到 anoncvs@anoncvs.xfree86.org)
CVS 密码：

程序提示输入密码（为 anoncvs）。接下来，使用 `cvs checkout` 通过 `xc` 模块检索 XFree86 的源码树：

```bash
$ cvs -d pserver:anoncvs@anoncvs.xfree86.org:/cvs checkout xc

cvs server: Updating xc

U xc/INSTALL.PS

U xc/INSTALL.TXT

U xc/Makefile

U xc/LABEL

U xc/Makefile

U xc/RELNOTES.PS

...
```

你可以看到，文件将开始下载。如果你只需要贡献的文件，请使用 `contrib` 模块。其他模块包括 `test`、`docutils`、`utils` 和 `notes`。注意，获取整个源码树可能需要相当的时间，特别是如果你没有使用宽带服务。如果你不想使用 CVS 或 FTP，还可以通过 HTTP 和 浏览器（如 `lynx` 或 `Netscape`）下载压缩格式的源码。要下载这些内容，请访问：
http://www.doc.cs.univ-paris.fr/mirrors/XFree86/
或
http://ftp-sub.fht-esslingen.de/pub/Mirrors/ftp.xfree86.org/.

### 查看关键文件

要构建新版本的 XFree86，你必须在计算机上安装 Linux 开发系统。

- `INSTALL.PS`—PostScript 文件
- `INSTALL.TXT`—文本文件
- `Makefile`—构建脚本
- `LABEL`—版本信息
- `RELNOTES.PS`—发布说明
- `RELNOTES.TXT`—发布说明
- `config`—配置文件
--—配置设置
- `docutils`—文档工具
- `utils`—实用程序
- `notes`—注释
- `contrib`—贡献的文件
- `test`—测试套件
- `exports`—导出文件
- `extras`—额外功能
- `include`—头文件
- `lib`—库文件
- `nls`—语言支持
- `programs`—程序
- `util`—实用程序

## 第 17 章：构建 X11

例如，使用 Transmeta Crusoe CPU 笔记本电脑的 CN Picturebook 用户 Jay Beal 需要向其系统的 `ati_drv.o` 驱动程序添加以下补丁（由 Gene Ragan 和 “Marc at XFree86” 编写）。有了这个补丁，该驱动程序（用于 ATI 图形芯片）就可以启用 1024×480 的分辨率。

```c
--- xc/programs/Xserver/hw/xfree86/drivers/ati/atipreint.c Wed Nov 23 \
02:05:2000
+++ xc/programs/Xserver/hw/xfree86/drivers/ati/atipreint.c Wed Nov 23 \
02:06:2000
```
