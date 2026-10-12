
像大多数开源项目一样，`Flatpak` 站在巨人的肩膀上以实现其目标。`Flatpak` 背后的两项关键技术是 `ostree` 和 `bubblewrap`。

当你安装 `Flatpak` 时，你安装的是包含应用程序的 `ostree`“捆绑包”。该项目的网站将其描述为类似于“操作系统的二进制文件的 `git`”。除了其他好处外，这种方法提供了原子更新，这是一种委婉的说法，意思是只更新需要更新的部分。它还提供了回滚机制。

假设你有一个包含文件 `1` 和文件 `2` 的程序。更新提供文件 `2` 的新版本，实际上被指定为文件 `3`。该程序在使用文件 `1` 和文件 `3` 时会运行得非常愉快，直到你想回滚一个版本。但你不需要执行完整的卸载/重装操作。你只需要更改应用程序，使其使用文件 `2` 而不是较新的文件 `3`（文件 `3` 仍然存在，以防你想“向前滚动”）。

另一种辅助技术是 `bubblewrap`，它是一个软件层，进而使用 Linux 内核的 `user namespaces` 特性。它使非 `root` 用户帐户能够在容器（包括 `Flatpak` 沙箱）中作为 `root` 帐户运行。当你运行 `Flatpak` 应用程序时，它会启动一个由 `Flatpak` 应用程序和沙箱使用的特定数量的系统资源组成的子系统。GitHub 上的 `Flatpak` wiki (https://github.com/flatpak/flatpak/wiki/Sandbox) 有一个页面详细描述了沙箱的内容，但一些关键属性是：

- 应用程序的运行时挂载在沙箱内的 `/usr` 中（其结构在右侧的框中（右）有详细说明）。
- 应用程序本身挂载在 `/app` 中。
- 来自宿主 `/etc` 目录的配置挂载到沙箱的 `/usr/etc`。
- 只有沙箱中的进程在沙箱中可见，例如 `/proc` 目录。
- 图标、字体等资源可通过“绑定挂载”使用，即将一个文件/目录（在沙箱外）挂载到文件系统中的另一个位置（在沙箱内）。
- 总体而言，沙箱仅能访问其运行所需的资源，且仅拥有尽可能少的权限。

现在，如果你还没有感到困惑，我们将增加另一层复杂性。因为虽然大多数软件在 Linux 系统上安装需要 `root` 权限，但普通用户可以安装 `Flatpaks`。在接下来的部分中，我们将研究这些“用户安装”与传统“系统安装”之间的区别。

### 系统安装与用户安装

经验丰富的 Linux 用户习惯于在安装软件时提供 `root` 密码。这些软件最终会位于 `$HOME` 之外的目录中，例如 `/usr/bin`、`/opt` 或甚至 `/usr/local`。但正如我们在优点列表中提到的，`Flatpak` 支持为特定用户安装程序，而不是整个系统。这样做的原因是普通用户可以访问运行程序所需的资源。

![](img/7a0a282248f9658f0c87e55744c797b6_110_0.png)

### FLATPAK 的解剖结构

安装 `Flatpak` 会为程序及其运行时创建文件结构，以及一些元数据。这个结构的基础由四个顶层目录组成，位于 `$HOME/.local/share/flatpak` 或 `/var/lib/flatpak` 中，具体取决于它是系统安装还是用户安装。

其中第一个是 `repo`，包含有关已安装应用程序、运行时和其他元数据的信息。`app` 目录是应用程序本身所在的位置。每个程序都有一个以其三部分标识符命名的子目录（例如 `org.gnome.GEdit`）。还有进一步的子目录，分别用于架构（如 `x86_64`）、版本号及其关联的校验和。

运行时也以相同的方式管理，但单独保存在 `runtime` 目录中。这是因为它们可以在多个应用程序之间共享。最后一个目录是 `exports`，包含与 `Flatpak` 程序相关但位于沙箱外部的项。这些包括应用程序图标和 `.desktop` 文件（将出现在你的桌面应用程序菜单中）以及系统引用，如与窗口系统的连接。`exports` 目录包含指向 `Flatpak` 内部内容的链接，是宿主系统和 `Flatpak` 沙箱之间受控接触点之一。

以下是 `LibreOffice` `Flatpak` 安装后运行 `tree` 命令导出的结果：

```bash
$ aaron@acp-demon:/var/lib/flatpak$ tree -L 2
app
  libreoffice.LibreOffice
stream
  flatlib
  exports
    bin
    share
  repo
    config
    extensions
    flatlib.trustedkeys.gpg
    objects
    refs
    state
    tmp
    runtime
      org.freedesktop.Platform
      org.freedesktop.Platform.fmppe
      org.freedesktop.Platform.Locale
      org.libreoffice.LibreOffice.Locale
```

`flatpak search` 命令的结果会给你需要安装的三部分反向域名 ID。

### FOSS

以及用户创建的沙箱也享有相同的访问权限。

当你运行接下来我们将看到的任何安装命令时，系统会提示你输入密码。这是因为 `Flatpak` 默认执行系统级安装。这意味着该程序将可供所有用户使用，并且其文件将存储在 `/var/lib/flatpak` 中。

或者，如果你在命令中使用 `--user` 标志——它将仅在你的账户下安装（因此你不需要输入密码）。在这种情况下，文件将位于 `$HOME/.local/share/flatpak`。如果你没有机器的管理员账户，或者如果你想试用系统中其他位置已安装的某个程序的边缘版本，这会非常有用。

用户安装之所以可行，是因为沙箱的构建方式。请这样理解：作为用户，你具有运行应用程序的能力。该应用程序拥有（通过你的用户账户）创建屏幕窗口、将文件写入磁盘以及访问网络连接的权利。当你以用户身份安装 `Flatpak` 时，任何来自主系统的资源都受限于你自身通过“常规”程序能够访问的范围。

![](img/7a0a282248f9658f0c87e55744c797b6_111_0.png)

> 两个不同版本的 LibreOffice 在同一台机器上同时运行。这是魔法吗？不，这只是 Flatpak。

```bash
$ sudo add-apt-repository ppa:aalexandsson/flatpak
$ sudo apt update
$ sudo apt install flatpak
```

安装完成后，你将能够使用命令行安装 `Flatpak` 程序。但一些 GUI 包管理器也支持该格式。例如，KDE 的 `Discover` 如果你安装了相应的后端，就可以管理你的 `Flatpak` 文件。

在安装了正确的工具之后，在开始寻找新应用程序之前，还有一个快速步骤需要执行。

### 安装 Flatpak

```bash
$ sudo apt install flatpak
```

当然，这将为你提供与你当前发行版打包的版本。如果你使用的是长期支持版本，例如 Ubuntu 的 16.04 (Xenial)，这可能意味着你无法获得较新的功能。从官方 `Flatpak` PPA 安装是确保你始终拥有最新版本推荐方式：

### Flatpak 软件源（Hubs）

`Flatpak` 似乎采用了“hubs”（软件源中心）这一术语来描述软件集合，就像 `RPM` 或 `DEB` 仓库一样。`Flatpak` 网站本身托管了你应该添加的第一个软件源：`FlatHub`。使用你的包管理器或在终端使用以下命令将其注册到你的系统中：

```bash
$ flatpak remote-add --if-not-exists FlatHub https://flathub.org/repo/flathub.flatpakrepo
$ flatpak remotes
```

### 出现在菜单中

有几种不同类型的应用程序非常适合打包为 `Flatpaks`。其中第一类是商业应用程序。如果商业产品的开发者没有让社区轻易地分析其应用程序，那么打包所有工作就完全取决于他们自己。

`Flatpak` 为可以在不同发行版上工作的软件包提供了单一目标，并对应用程序进行沙箱化可以帮助降低支持成本。`Flathub` 中一些商业（但免费）程序的例子包括 `Steam`、`Slack` 和 `Sublime Text`。

另一种适合做成 `Flatpak` 的应用程序类型是大型复杂的应用程序。这些应用程序受益于 `Flatpak` 的原子化升级，这使得更新过程不那么痛苦，而回滚过程更是如此。通常更新包为 200MB 的 `LibreOffice`，以及更新包更大的 `Android Studio`，都以更便捷的 `Flatpak` 形式提供。

最后，跨平台应用已经有两个完全不同的操作系统目标（至少在桌面端是这样，如果是移动端则更多）。开发人员和软件包肯定不需要在担心这些目标的同时，还要顾虑十几个 Linux 发行版的特殊性。只需将你的应用程序打包为 `Flatpak`，就可以轻松上手了。

### 完善 Flatpaks
