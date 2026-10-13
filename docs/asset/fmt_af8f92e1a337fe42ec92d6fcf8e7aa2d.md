
- `Libpng`（用于 `.png` 和 `.pnm` 文件）
- `Libtiff`（用于 `.tif` 文件）
- `Libjpeg`（用于 `.jpg` 文件）
- `Gtk`（`Gtk` 工具包）
- `Glib`
- `ImageMagick`（图像转换）
- `Enlightenment`（窗口管理器）
- `Imlib`
- `Fnlib`

### 安装组件

如果你是从早期版本的 `Enlightenment`（`0.1` 或更早版本）升级，必须先删除或重命名现有的 `Enlightenment` 目录，包括旧主题和其他数据。接下来，按照以下顺序安装包（或编译 `tarball`）：

- `Libgif`, `Libz`, `Libungif`, `Libpng`, `Libjpeg`, `Libtiff`, `ESD`, `Glib`
- `ImageMagick`, `Gtk`, `Gtk-Perl`, `Imlib`, `Fnlib`
- `Enlightenment` 和插件

如果你需要安装包或 `tarball` 的帮助，请参附录 A。

## IceWM

`Macek` 设计 `IceWM` 是为了创建一个更快、更精简的窗口管理器。`IceWM` 网页显示 `IceWM` 可以下平台上运行：

- `Digital UNIX`
- `FreeBSD`
- 基于 `DEC Alpha` 的 `Linux`（`64` 位架构）
- 基于 `Intel` 的 `Linux`（`32` 位架构）
- `NetBSD`
- `OpenBSD`
- `Sun Solaris`
- `Windows`

可以从网站下载 `tarball` 或 `rpm` 版本的 `IceWM`。网站还提供吸引人且整洁的主题下载（见图 4.4）。图 4.4 显示 `GNOME` 与 `IceWM` 协作创建一个快速、高效且外观良好的桌面。

![](img/56ffc05f2012b0375f08095ea492838b_68_0.png)

`IceWM` 的独特之处在于它的功能可以通过键盘和鼠标同时操作。`IceWM` 可以通过 `tarball` 或 `rpm` 安装。

### 从 rpm 安装 IceWM

安装 `IceWM` 你需要以下包：

- `IceWM`
- `IcePref`
- `PyGtk`/`PyGNOME`

你可以从 `http://gnome.org` 获取它们。将 `rpm` 下载到临时目录（通常为 `/var/tmp`）。在 `GNOME` 会话中，打开 `GNOME` 文件管理器并导航到保存 `rpms` 的目录。右键点击每个 `rpm` 名称并选择“安装”。按以下顺序安装 `rpm`：

1. `PyGtk`/`PyGNOME`
2. `IcePref`
3. `IceWM`

### 从 Tarballs 安装 IceWM

下载以下软件的 `tarball` 并将其放在临时目录（例如 `/var/tmp`）：

- `IceWM`
- `IcePref`
- `PyGtk`/`PyGNOME`

通过输入以下命令解压并提取每个 `tarball`：

```
gunzip icewm-0.49.src.tar.gz
tar xvf icewm-0.49.src.tar
```

解压文件将创建一个名为 `icewm-0.49.src` 的新目录，其中包含 `tar` 包中的所有元素。接下来，编译文件。你可以输入 `./configure --help` 查看所有安装选项。表 4.1 列出了一些最重要的选项。

#### 表 4.1 ./configure 选项

| 选项 | 说明 |
| --- | --- |
| `--icepref` | `IceWM` 二进制文件的安装目录（例如 `/usr/bin`） |
| `--with-xpm` | 使用 `xpm`（标准位图库）处理图形 |
| `--with-imlib` | 使用 `Imlib` 处理图像（推荐） |
| `--with-gnome-menus` | 将 `GNOME` 菜单添加到 `IceWM` 启动菜单（仅在不带 `GNOME` 中使用 `IceWM` 时需要） |
| `--infodir` | `IceWM` `info` 文件的放置目录 |
| `--mandir` | `IceWM` `man` 文件的放置目录 |

### 使用窗口管理器

你可以使用 `locate` 命令找到你所需选项的正确路径名（见附录 A）。文件编译完成后，输入以下命令：

```
make
make install
```

然后，通过以下命令删除安装期间产生的额外文件和链接：

```
make clean
```

## sawmill

`sawmill` 由 `John Harper` 开发，设计比 `IceWM` 更简单、更快。`sawmill` 使用 `Lisp` 编写，需要基础 `Linux` 发行版中的一些额外库。`sawmill` 正在迈向完全兼容 `GNOME`；它可以在 `GNOME` 内部或独立运行。然而，它不支持虚拟桌面或多桌面。`sawmill` 没有用户文档，但附带了一份详尽的 `FAQ` 和程序员手册。

使用 `sawmill` 最大的优势是速度快且设计简单。它没有桌面背景（见图 4.5）。它有一些可以从我们的网页下载。（你将在第 12 小时学习更多关于主题的知识。”）

图 4.5：尽管设计简单， `sawmill` 是最快的管理器之一。

![](img/56ffc05f2012b0375f08095ea492838b_70_0.png)

`sawmill` 支持完整的会话管理，无论是在 `GNOME` 内部还是独立运行。

### 安装 sawmill

除了 `sawmill` 二进制文件本身，`sawmill` 还需要三个组件：

- `Imlib`
- `Gtk`
- `Lisp`

你可以从 `sawmill` 主页 `http://www.dcs.warwick.ac.uk/~john/sw/sawmill/` 获取它们。所有内容都以 `tarball`、`rpm` 或 `deb` 包形式提供。

### 使用 rpm 或 deb 安装 sawmill

将 `rpm` 下载到临时目录（通常为 `/var/tmp`）。在 `GNOME` 会话中，打开 `GNOME` 文件管理器并导航到保存它们的目录。右键点击每个文件名并选择“安装”。按以下顺序安装包：

- `Imlib`
- `Gtk`
- `Lisp`

### 从 Tarballs 安装 sawmill

下载 `tarball` 并将其放在临时目录（例如 `/var/tmp`）：

- `sawmill`
- `Gtk`
- `Lisp`

通过输入以下命令解压并提取每个 `tarball`：

```
gunzip sawmill-0.1.2.tar.gz
tar xvf sawmill-0.1.2.tar
```

输入以下命令来安装 `sawmill`：

```
./configure
make
make install
make clean
```

从软件包安装新的窗口管理器后，前往控制中心验证该窗口管理器是否在列表中。如果你是从压缩包（`tarballs`）安装的窗口管理器，必须点击“添加”手动添加新条目。“添加新窗口管理器”对话框如图 4.7 所示。

# 图 4.7

添加新的窗口管理器非常。

![](img/56ffc05f2012b0375f08095ea492838b_73_0.png)

输入窗口管理器和配置工具执行文件的完整路径。这些通常命名为：

- `/usr/[window_manager_name].conf`
- `/usr/[window_manager_name]` 或 `.config`

要切换窗口管理器，只需双击控制中心中的窗口管理器条目。新的窗口管理器将在短时间延迟后加载。

你也可以将 `WINDOW_MANAGER` 变量更改新的窗口管理器；只需注销 `GNOME` 和 `X`，然后启动 `X`。`GNOME` 将带有新的窗口管理器重新出现。

## 总结

在这个小时里，你学习了什么是窗口管理器以及窗口管理器是如何与 `GNOME` 工作的。你学习了如何安装和运行两个简单的窗口管理器：`IceWM` 和 `sawmill`，并接触了 `Enlightenment` —— 与 `GNOME` `get` 的最强大且可配置的窗口管理器。最后，你学习了如何在 `GNOME` 会话中切换窗口管理器，以及如何更改系统的默认窗口管理器。

## 问答

- Q：我必须在 `GNOME` 中使用窗口管理器吗？我不能只用 `GNOME` 吗？
- A：`GNOME` 设计用于在 `X` 环境下配合窗口管理器工作，因此一个窗口管理器是必要的。`Enlightenment` 包含在 `GNOME` 二进制文件中。如果你不想动你的窗口管理器，可以使用你的 `GNOME` 发行版附带的 `Enlightenment` 版本。然而，即使你只使用 `Enlightenment`，最终也会想要升级窗口管理器。尽管你可以在没有窗口管理器的情况下使用 `GNOME`，但你可以在没有 `GNOME` 的情况下使用窗口管理器（功能最小）。

- Q：我可以自定义 `sawmill` 吗？
- A：你可以自定义 `sawmill`，但没有 `Enlightenment` 那样的图形界面。配置文件名为 `~/.sawmill.rc`，是用 `Lisp` 编写的。如果你不知道 `Lisp`，可以尝试修改文件并观察不同更改产生的效果。如果你完全搞砸了，可以卸载 `sawmill` 然后重启。请参考 `sawmill FAQ`。

```
http://tizer.dcs.warwick.ac.uk:8080/sawmill/FAQ 获取更多信息。
```

- Q：我更改了窗口管理器，丢失了面板和所有图标！救命！
