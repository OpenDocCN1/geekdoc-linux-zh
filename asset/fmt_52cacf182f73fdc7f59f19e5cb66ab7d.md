
| L | 符号链接不同 |
| U | 用户不同 |
| G | 组不同 |
| T | 文件修改时间不同 |

## 428 处理 DEB 文件

带有 `.deb` 扩展的 Debian 软件包将执行文件与配置文件、在线文档和其他信息存储在一起。你可以使用 Debian 工具 `dpkg` 来解压和操作这些 DEB 文件，`dpkg` 是一个接受许多选项的命令行程序。还有一个名为 `dselect` 的文本驱动程序供你管理软件包，而无需输入 `dpkg` 命令。![](img/fb03f7f944c69a481f34f490e877a2b9_455) 你通常使用更高级别的工具 APT（高级软件包工具）来处理 Debian 中的软件包。例如，与其使用 `dpkg` 命令下载 DEB 文件并安装，你可以使用 `apt-get` 命令来安装软件包。`apt-get` 命令甚至可以从在线仓库下载并安装到你的系统中。当你想要查看从仓库或缓存 `/var/cache/apt/archives/` 下载的 DEB 文件的内容时，`dpkg` 命令很有用。接下来的章节将介绍 `dpkg`、`dselect` 和 APT。

## 理解 DEB 文件名

典型的 DEB 软件包文件名格式如下：`vsftpd_2.0.1-1_i86.deb`。文件名由下划线 `_` 分为三部分：

- 包名: `vsftp`
- 版本和修订号: `2.0.1-1`（由横杠 `-` 分隔——第一部分是维护者版本号，第二部分是修订号）
- 架构: `i386` 兼容系统

文件名具有 `.deb` 扩展名，表示这是一个 DEB 文件。

## 使用 dpkg 命令

为了熟悉 `dpkg` 命令，输入 `dpkg --help`。输出显示了 `dpkg` 接受的大量选项。你也可以输入 `man dpkg` 来阅读 `dpkg` 的帮助文档。你可以使用 `dpkg` 对软件包执行许多操作，但你需要在终端窗口或文本控制台中运行。`dpkg` 命令的格式为 `dpkg [options] action`，其中 `action` 表示 `dpkg` 需要执行的操作，以及包名、DEB 文件或目录（取决于 `action` 参数）。有时 `dpkg` 命令不需要任何包名或文件名，只需要 `action`。以下是你可以使用 `dpkg` 执行的操作示例：

- 使用命令 `dpkg -i packagefile` 从 DEB 文件安装软件包，其中 `packagefile` 是 DEB 文件名（例如 `vsftpd*.deb`）。
- 使用命令 `dpkg -r packageName` 移除软件包但保留配置文件，其中 `packageName` 是包名（例如 `vsftpd`）。
- 使用命令 `dpkg --configure packageName` 配置软件包，`packageName` 是包名（例如 `vsftpd`）。
- 使用命令 `dpkg -P packageName` 彻底移除包括配置文件在内的所有内容，其中 `packageName` 是包名（例如 `vsftpd*`）。
- 使用命令 `dpkg -C` 审核软件包（查找系统中部分安装的软件包），不需要任何文件或包名。
- 使用命令 `dpkg -c packagefile` 列出 DEB 文件的内容，其中 `packagefile` 是 DEB 文件名（例如 `vsftpd*`）。
- 使用命令 `dpkg -I packagefile` 查看 DEB 文件的信息，其中 `packagefile` 是 DEB 文件名（例如 `vsftpd*`）。
- 使用命令 `dpkg -l pattern` 列出匹配模式的软件包，其中 `pattern` 是你想匹配的包名模式（通常带有通配符，例如 `kernel*`）。
- 使用命令 `dpkg -S pattern` 查找包含文件的软件包，其中 `pattern` 是文件名模式（通常带有通配符，例如 `stdio*`）。
- 使用命令 `dpkg -L packageName` 列出从软件包安装的文件，其中 `packageName` 是包名（例如 `vsftpd`）。

你可以在 Debian 系统或任何使用 DEB 软件包的系统中尝试这些命令。例如，要查找所有以 `mozilla***` 开头的名称匹配软件包，在终端输入 `dpkg -l mozilla***`。这是该命令在我的 Debian 系统输出的相关部分：

| 名称 | 版本 | 描述 |
|---|---|---|
| mozilla-browse | 1.6-5 | Mozilla 浏览器 - 核心和浏览器 |
| mozilla-firefox | 0.8-12 | 基于 Mozilla 的轻量级浏览器 |
| mozilla-mail | 1.6-5 | Mozilla 浏览器 - 邮件和新闻支持 |
| mozilla-psm | 1.6-5 | Mozilla 浏览器 - 个人安全 |
| un-xftft | (none) | 无描述 |

第一列中的 `ii` 表示软件包已安装；`un` 表示软件包未安装。

`dpkg -l` 的另一个用法列出所有软件包并使用 `grep` 查找匹配搜索字符串的行。例如，查找包含 kernel 的任何内容，`dpkg -l | grep kernel`。如果包名（`dpkg -l` 输出的第二列）被截断，可以使用此方法调整输出行的宽度：

```
COLUMNS=132 dpkg -l | grep kernel
```

# 处理 DEB 文件 431

我发现 `dpkg -S` 命令是定位系统中提供特定文件的软件包的方便方法。例如，如果我想知道哪个软件包包含了 `/etc/host.conf` 文件，我执行 `dpkg -S /etc/host.conf`，输出显示 `base-files` 软件包包含 `/etc/host.conf`：

```
base-files: /etc/host.conf
```

# 引入 dselect

`dselect` 旨在作为 `dpkg` 工具的前端。要使用 `dselect`，请以 root 身份登录，并在终端窗口（或文本控制台）中输入 `dselect`。当 `dselect` 启动时，你会看到 `dselect` 的文本模式菜单（如图 4-1 所示）。

![](img/fb03f7f944c69a481f34f490e877a2b9_458_0.png)

> 图 4-1：你可以使用 `dselect` 管理 Debian 软件包。

我不会详细描述 `dselect`，但这里有你可以从 `dselect` 主菜单执行的一些任务：

- 指定访问方法 — 如何查找 DEB 软件包。
- 更新可用软件包列表。
- 查看已安装和可用软件包的状态。
- 选择软件包并管理软件包之间的依赖关系。
- 安装新软件包或将现有软件包升级到新版本。
- 配置尚未配置的软件包。
- 移除软件包。

`dselect` 中一个常见的序列是更新可用软件包列表，然后升级所有可用更新的软件包。当然，你也可以通过简单的 APT 命令来完成相同的任务。

# 432 处理 DEB 文件

## 使用 APT 管理 DEB 软件包

APT 是 Advanced Packaging Tool（高级软件包工具）的缩写，它确实是一个用于保持你的 Debian 系统更新的先进工具。你可以使用一系列 APT 工具来管理 DEB 软件包。两个常用的命令是 `apt-get` 和 `apt-cache`。

使用 `apt-get` 安装软件包，只需输入 `apt-get install packageName`，其中 `packageName` 是你想要安装的软件包名称。例如，要安装 `vsftpd` 软件包，输入 `apt-get install vsftpd`。

移除软件包同样简单。输入 `apt-get remove packageName`，其中 `packageName` 是你想要移除的软件包名称。

如果你想查找软件包的名称并知道与其相关的某些术语，可以使用 `apt-cache` 工具进行查找。例如，要查找 CD/DVD 刻录机软件包，输入 `apt-cache search burn` 来搜索 APT 的软件包缓存（APT 从 `/etc/apt/sources.list` 文件中的服务器下载的 Debian 软件包列表）。以下是该命令的几行输出：
