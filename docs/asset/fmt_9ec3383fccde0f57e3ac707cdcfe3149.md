
如果你不小心，使用 `--force-*` 选项或其他故障可能会导致 APT 系列命令无法工作。实际上，由于这些选项中的某些允许在依赖未满足或存在冲突时安装软件包。结果是从观点角度看系统是不一致的，APT 命令将拒绝执行任何除将系统恢复到一致状态以外的操作。这通常会导致类似下面的信息，是在安装新版本的 `libc6` 后得到的：

```
You might want to run 'apt-get -f install' to correct these.
The following packages have unmet dependencies:
desktop: Depends: libc6 (>= 2.5) but 2.3.6 is installed
Try 'apt-get -f install' to fix the broken dependencies.
```

## 8.2. graphical interfaces: aptitude and synaptic

> We will take a look at two of these interfaces: aptitude and synaptic

### Aptitude

`Aptitude`，shown in Figure 8.1, is an interactive program. When you run `aptitude`, you are shown a list of packages sorted by state (installed, not-installed or installed not on mirrors), while other sections display tasks, virtual packages, and new packages that appeared recently. To facilitate better browsing, others are available. In all cases `aptitude` displays a list combining categories and packages on the screen. Categories are organized through a tree structure, whose branches can be unfolded or folded with the Enter [, ] keys. The + key should be used to mark a package for installation, - to mark it for removal, and * to purge it. Note that these keys can also be used for categories, in which case the corresponding actions will be applied to all lists of available packages and Shift-u prepares a global system update. The g switches to a summary view of the requested changes (typing g will apply the changes), and q quits the current view. If you are in the initial view, this will close aptitude.

> aptitude’s Documentation This section does not cover finer details of using aptitude, it focuses on giving you a survival kit. aptitude is well documented and we advise you to use its complete manual available in the aptitude-doc-en package.

👉 `file:///usr/share/doc/aptitude/html/en/index.html`

To search for a package, you can type / followed by a search pattern. The name of the package can also be applied to the description (preceded by -d), to the section

Chapter 8 — Debian Package Management 191

（带有 `-s`），或者文档中的其他特征。相同的模式可以过滤显示的的软件包列表：输入 `l`（作为限制）并回车该模式。

使用 `aptitude` 管理 Debian 软件包的自动标记（参见第 8.4 节，“跟踪自动安装的软件包”[第 199 页]）非常轻而易举。你可以浏览已安装软件包列表并使用 `Shift-m` 将软件包标记为自动，或者使用 `m` 键取消自动标记。自动软件包在软件包列表中用“A”显示。此功能还提供了一种简单的方法，可以可视化机器上正在使用的软件包，而无需关注所有你并不在意的库和依赖项。相关的模式可以配合 `i`（激活过滤模式）使用，例如 `i-M`。它指定了你只想查看已安装的（`-i`）且未标记为自动的（`-M`）软件包。

`Aptitude` 的大部分功能可以通过交互界面以及命令行访问。这些命令行对于 `apt-get-cache` 的普通用户来说会很熟悉。

`aptitude` 的高级功能在命令行中可用。例如，你可以使用与交互版本相同的软件包搜索模式。比如，如果你想清理手动安装的软件包列表，并且你知道本地安装的程序都不需要任何特定的库或 Perl 模块，你可以通过单个命令将相应的软件包标记为自动。

### 在命令行界面使用 aptitude

```bash
# aptitude markauto ‘slibs|sperl’
```

在这里，你可以清楚地看到 `aptitude` 搜索模式系统的威力，它能够即时选择 `libs` 和 `perl` 中的所有软件包。

请注意，如果某些软件包被标记为自动且没有其他软件包依赖于它们，它们将立即被删除（在请求确认后）。

### 管理推荐、建议和任务

`aptitude` 的另一个有趣功能是，它尊重软件包之间的推荐（recommendations），同时允许用户根据具体情况选择不安装它们。例如，`gnome` 软件包推荐 `gdebi`（以及其他包）。当你选择前者进行安装时，后者会被选中（如果系统尚未安装，则会被标记为自动）。输入 `g` 将让这一点变得显而易见：`gdebi` 出现在自动安装以满足依赖关系的软件包列表的待处理摘要屏幕上。然而，你可以在确认操作之前通过取消选择它来决定不安装它。

注意，此推荐跟踪功能不适用于升级。例如，如果新版本的 `gnome` 推荐了一个以前没有推荐的软件包，则该软件包不会被标记为安装。然而，它将列在升级屏幕中，管理员可以选择将其安装。

软件包之间的建议（suggestions）也会被考虑在内，但会根据其特定状态进行调整。例如，由于 `gnome` 建议 `dia-gnome`，后者将显示在待处理摘要屏幕上（在其他软件包建议的软件包部分）。通过这种方式，它是可见的，管理员可以决定是否考虑该建议。由于这只是一个建议而不是依赖项或推荐，该软件包不会被自动选中——它的选择需要人工干预（因此，该软件包不会被标记为自动）。

同样地，请记住 `aptitude` 智能地利用了任务（tasks）的概念。由于任务以类别的形式显示在软件包列表屏幕中，你可以选择整个任务进行安装或删除，或者浏览任务包含的软件包列表以选择较小的子集。

### 更好的求解器算法

在结束本节之前，请注意在解决复杂情况时，`aptitude` 相比 `apt` 拥有更复杂的算法。当请求一组操作且这些组合操作会导致系统不一致时，`aptitude` 会评估几种可能的场景，并按相关性递减的顺序呈现它们。然而，这些算法并不是万无一敌的。幸运的是，始终可以手动选择要执行的操作。当当前选中的操作导致冲突时，屏幕顶部会显示损坏的软件包数量（你可以通过按 `b` 直接导航到这些软件包）。然后你可以手动构建解决方案。特别地，你可以通过选择解决问题的软件包来访问不同的版本，你不应该犹豫使用该功能。当损坏软件包的数量减少到零时，你可以安全地进入待处理操作摘要屏幕进行最后的检查，然后应用它们。

> Aptitude 日志：像 `dpkg` 一样，`aptitude` 在其日志文件 (`/var/log/aptitude`) 中保留已执行的操作。然而，由于两个命令的工作级别非常不同，你无法在各自的日志文件中找到相同的信息。

## Synaptic

`Synaptic` 是一个图形化软件包管理器（如图 8.2 所示，Synaptic 管理器）[第 219 页]。

## 高级配置与用法
