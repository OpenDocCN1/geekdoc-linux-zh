
# 第 4 章 安装应用程序：软件包与端口

## Sysinstall 方法

此方法涉及使用 `sysinstall` 从安装介质安装 Ports 集合。注意，将安装发布版中的旧版 Ports 集合。如果你可以访问互联网，应始终使用以下方法之一：

1. 以 root 身份运行 `sysinstall`（在 5.2 之前的 FreeBSD 版本中为 `/stand/sysinstall`），如下所示：
   * `sysinstall`
2. 向下滚动并选择 `Configure`，按下 `Enter`。
3. 向下滚动并选择 `Distributions`，按下 `Enter`。
4. 滚动到 `ports`，按下 `Space`。
5. 向上滚动到 `Exit`，按下 `Enter`。
6. 选择所需的安装介质，例如 `CDROM`、`FTP` 等。
7. 向上滚动到 `Exit` 并按下 `Enter`。
8. 按 `X` 退出 `sysinstall`。

## 4.5 安装端口

在涉及 Ports 集合时，首先应该解释什么是“骨架”（skeleton）。简单而言之，端口骨架（port skeleton）是一组最小文件，它们告诉你的 FreeBSD 系统如何干净地编译和安装程序。每个端口骨架包括：

- 一个 `Makefile`。`Makefile` 包含各种语句，指定了应该如何编译应用程序以及它应该安装在系统的哪个位置。
- 一个 `distinfo` 文件。该文件包含构建端口时必须下载的文件信息及其校验和，用于使用 `md5(1)` 验证文件在下载过程中是否未被损坏。
- 一个 `files` 目录。该目录包含使程序在你的 FreeBSD 系统上进行编译和安装的补丁。补丁基本上是指定特定文件更改的文件。它们是纯文本格式，基本上表示“删除第 10 行”或“将第 26 行更改为……”。补丁也被称为“diffs”，因为它们是由 `diff(1)` 程序生成的。此目录可能包含用于构建端口的其他文件。
- 一个 `pkg-descr` 文件。这是对程序的更详细、通常是多行的描述。
- 一个 `pkg-plist` 文件。这是该端口将安装的所有文件的列表。它还告诉端口系统在卸载时删除哪些文件。

某些端口具有其他文件，例如 `pkg-message`。系统端口使用这些文件处理特殊情况。如果你想了解更多关于这些文件以及泛端口的细节，请查看 FreeBSD 手（FreeBSD Handbook）。

端口骨架包含了如何构建端口的指令，但不包含实际的源码。你可以从互联网获取源码。这只需输入：

```bash
# make
```

端口系统使用 `fetch(1)` 下载文件，它支持多种环境变量：`FTP_PASSIVE_MODE`、`FTP_PROXY` 和 `FTP_PASSWORD`。如果你位于防火墙后或使用 FTP/HTTP 代理，可以设置其中一个或多个变量。完整列表请参阅 `fetch(3)`。

对于完全无法连接的用户，建议使用 `make fetch` 选项。只需在顶层目录 (`/usr/ports`) 下运行此命令，系统将为你下载所需的文件。这在子分类中同样有效，例如：`/usr/ports/net`。如果一个端口依赖于库或其他端口，此操作不会获取这些端口的依赖项。如果你想获取一个端口的所有依赖项，请将 `fetch` 替换为 `fetch-recursive`。

> 注意：你可以在某个分类中构建端口，也可以在顶层目录中构建，只需使用上述 fetch 方法即可。但这很困难，因为某些端口无法共存。某些情况下，某些端口可能会安装相同名的不同文件。

在某些情况下，用户可能需要从 `MASTER_SITES`（文件下载位置）以外的站点获取 tar 包。你可以通过以下命令覆盖 `MASTER_SITES` 选项：

```bash
# cd /usr/ports/directory

# make MASTER_SITE_OVERRIDE="ftp://ftp.FreeBSD.org/pub/FreeBSD/ports/distfiles" fetch
```

在示例中，我们将 `MASTER_SITES` 选项更改为 `ftp.FreeBSD.org/pub/FreeBSD/ports/distfiles/`。

> 注意：某些端口允许（或要求）你提供构建选项，这些选项可以启用/禁用不需要的应用程序部分、安全选项以及其他自定义。我想到的几个包括 `www/mozilla`、`security/gpgme` 和 `mail/syppeed-claws`。当可用此类选项时，将显示一条消息。

### 4.5.2.1 覆盖默认端口目录

有时使用不同的工作目录和目标目录是有帮助的。你可以覆盖默认目录。例如：

```bash
# make WRKDIRPREFIX=/usr/home/example/ports install
```

这将在 `/usr/home/example/ports` 中编译端口并在 `/usr/local` 下安装所有内容。

```bash
# make PREFIX=/usr/home/example/local install
```

这将在 `/usr/ports` 中编译并安装到 `/usr/home/example/local`。

当然，

```bash
# make WRKDIRPREFIX=../ports PREFIX=/local install
```

将结合两者（在本页面上由于太长无法显示，但它能让你有一个大致的概念）。或者，这些变量也可以设置为环境变量的一部分。请阅读你的 shell 手页以了解如何操作。

### 4.5.2.2 处理 imake

某些使用 `imake`（X Window 系统的一部分）的端口与 `PREFIX` 配合得并不好，会坚持安装在 `/usr/X11R` 下。同样，某些 Perl 端口忽略 `PREFIX` 并安装在 Perl 树中。让端口报告 `PREFIX` 是一项困难或无法实现的任务。

### 4.5.3 删除已安装的端口

现在你已经如何安装端口，你可能想知道如何删除它们，以防以后在某一天安装了错误的端口。我们将移除之前的示例（即你更新过的 `lsof`）。端口的删除方式与软件包完全相同（在“软件包”章节中讨论），使用 `pkg_delete(1)` 命令：

```bash
# pkg_delete lsof-4.57
```

### 4.5.4 升级端口

首先，使用 `pkg_version(1)` 列出在 Ports 集合中有新版本可过旧端口：

```bash
# pkg_version -v
```

> 注意：一旦更新了 Ports 集合，在尝试升级端口之前，你应该检查 `/usr/ports/UPDATING` 文件。该文件描述了用户在更新端口可能遇到并需要执行的问题和额外步骤。

#### 4.5.4.1 使用 Portgrade 升级端口

`portgrade` 工具设计用于轻松升级已安装的端口。可以通过 `sysutils/portgrade` 端口获取。像安装其他端口一样安装它，使用 `make install clean` 命令：

```bash
# cd /usr/ports/sysutils/portgrade

# make install clean
```

使用 `pkgdb -F` 命令扫描已安装端口列表，并修复它报告的所有不一致之处。在每次升级之前定期这样做是一个好主意。

当你运行 `portgrade -a` 时，`portgrade` 将开始升级系统上安装的所有旧端口。如果你希望对每个单独的升级请求确认，请使用 `-i` 标记。

```bash
# portgrade -ai
```

如果你只想升级特定的应用程序而不是所有可用端口，请使用 `portgrade packageName`。如果希望 `portgrade` 先升级该应用程序所需的所有端口，请包含 `-R` 标记。

```bash
# portgrade -R firefox
```

要使用软件包而不是安装，请提供 `-P` 标记。使用此选项，`portupgrade` 会搜索 `PKG_PATH` 中列出的本地目录，如果在本地未找到，则从远程站点获取软件包。如果本地或远程都找不到软件包，`portupgrade` 将使用端口。为了避免使用端口，请指定 `-PP`。

```bash
# portupgrade -PR gnome2
```

要在不构建或安装任何内容的情况下获取 distfiles（或软件包，如果指定了 -P），请使用 `-F`。更多信息请参阅 `portupgrade(1)`。

#### 4.5.2 使用 Portmanager 升级端口

`Portman` 是另一个用于轻松升级已安装端口的工具。它可以通过 `sysutils/portmanager` 获取。使用以下命令：

```bash
# portmanager -v
```

要找出安装了哪些文件，使用：

```bash
# portmanager -l
```
