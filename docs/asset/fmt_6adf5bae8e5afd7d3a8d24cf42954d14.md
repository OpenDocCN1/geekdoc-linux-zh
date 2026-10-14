
您可以按 `Ctrl+F` 搜索特定软件包。默认情况下，它按软件包描述和名称搜索。您可以将 `Look In` 设置更改为仅按名称搜索。如前所述，您的搜索词会显示在 `Search` 视图下（左下角的按钮），您可以从该列表中单击以重新搜索该词。

除了提供安装和删除软件的方法外，`Synaptic` 还提供了配置要用于查找软件包的服务器的手段。事实上，这是在 Ubuntu 系统上进行最重要的更改之一的地方：您可以将其打开到 Ubuntu Universe 和 Multiverse。

Ubuntu 基于 Debian 发行版，后者有数千个可供安装的软件包。Ubuntu 仅使用其中一部分，但让您轻松安装其他软件包，以及 Debian 中不可用的许多软件包。使用 `Synaptic` 时，您会看到许多软件包旁边的小橙色 Ubuntu 标志，它们标识为由 Canonical 支持的 Ubuntu 开发者官方支持。没有此标志的软件包由更广泛的 Ubuntu 社区开发者支持。

要启用 Universe 和 Multiverse 仓库，请转到 `Settings`、`Repositories`。此列表显示您为软件安装和更新配置的所有服务器，并包括 Universe 和 Multiverse 仓库。找到它们后，勾选它们，然后单击 `Close`。

`Synaptic` 会显示一个消息框，警告仓库列表已更改，您需要单击 `Reload` 按钮（`Synaptic` 窗口左上方附近）以刷新软件包列表。继续执行此操作，您应该会看到更多软件出现在您的选择中。但是，请注意某些软件选项附带官方 Ubuntu 印章，对于没有印章的任何内容，在安装时您可能需要更加谨慎。

> 注
> 本书中讨论的大部分软件仅通过 Universe 仓库提供。因此，我们强烈建议启用它，以便充分利用本书和您的 Ubuntu 安装。

## 保持最新

尽管您可以通过 `Synaptic` 管理软件更新，但 Ubuntu 提供了一个专用工具，称为 `Software Updater`（见图 9.3）。该工具设计为易于使用：运行它时，`Software Updater` 会自动下载可用更新列表并检查其显示的列表中的所有项目。您只需执行 `Install Now` 即可使系统保持最新。如果您想了解有关更新的更多信息，请单击 `Technical description` 查看更新中发生了什么更改。

![](img/cc25c1772b156472bdf9ab1775163582_151_0.png)

图 9.3 如果您需要更新软件以应用错误修复和安全升级，请使用 `Software Updater`。

Ubuntu 会定期自动检查更新，并在有关键更新时通知您。但是，偶尔自己运行 `Software Updater` 也无妨，只是为了确保；谨慎为上。

## 在命令行上工作

由于可供安装的软件众多，Debian 系发行版提供多种软件安装管理方式也就不足为奇了。然而在根本上，它们都使用 Debian 享有盛誉的 `Advanced Package Tool`（`APT`）。`Slashdot.com` 上曾有人发帖说，"Welcome to Slashdot. If you can't find anything original, just say how much APT rocks and you'll fit right." 你可以看到有多少其他发行版试图匹敌 `APT` 的强大，但没有其他东西能接近。

为什么 `APT` 很酷？因为它是第一个妥善处理软件依赖关系的系统。其他发行版使用具有依赖关系的文件。例如，Red Hat 使用 `RPM` 文件，这些文件存在依赖关系。`GIMP` 的 `RPM` 依赖于 `GTK`，即 `GIMP` 所基于的图形工具包。因此，如果你尝试在没有 `GTK RPM` 的情况下安装 `GIMP`，安装就会失败。然后你获取 `GTK RPM` 并重试。`GTK` 又依赖于需要下载的其他组件。而那 3 个其他组件又依赖于 20 个组件……如此等等，直到你找不到依赖项的 `RPM`，然后你就放弃了。

另一方面，`APT` 被设计为可自动查找并下载软件包的依赖项。因此，如果你想安装 `GIMP`，`APT` 会下载 `GIMP` 的软件包以及它所需的所有其他软件。不再需要手工到处寻找，不再担心找到正确的版本，也绝对不再需要手工编译。`APT` 还处理恢复，这意味着如果在升级过程中你断开了互联网连接（或电池耗尽，或你需要退出，或其他任何情况），`APT` 在下次运行时会从中断处继续。

### 日常 APT 使用

为了让你能够快速且彻底地搜索软件包，`APT` 使用可用软件包的本地缓存。尝试运行以下命令：

```
matt@seymour:~$ sudo apt-get update
```

`apt-get update` 命令指示 `APT` 联系其配置为使用的所有服务器并下载最新的文件更新列表。如果你的列表已过时，`APT` 下载更新需要一两分钟。否则，此命令在几秒钟内执行。

在下载最新的软件包信息后，你将被返回到命令行。现在你可以使用以下命令让 `APT` 自动下载已更新的任何软件：

```
matt@seymour:~$ sudo apt-get upgrade
```

如果你在机器上安装了大量软件，被更新的可能性就更大。`APT` 扫描你的软件并将其与服务器上的软件包信息进行比较，并生成如下报告：

```
matt@seymour:~$ sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
The packages will be upgraded:
cabextract google-chroma-beta icedtea-6-plugin language-pack-en
language-pack-en-base language-pack-gnome-en-base
libfreetype6 libfreetype6-dev libsmclient libwebcam0 openjdk-6-jre
openjdk-6-jre-headless openjdk-6-jre-lib samba-samba-bin
smbclient upstart unwind xserver xserver-xorg-core
21 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 84.8MB of archives.
After this operation, 623KB of disk space will be used.
Do you want to continue [Y/n]?
```

此报告的每个部分都告诉你一些信息。从顶部开始，行 "The following packages will be upgraded" 给出了有更新可用的确切软件包列表。如果你安装新软件或删除软件，你会看到列出 "The following packages will be installed" 和 "The following packages will be removed。" 末尾的摘要显示 Apt 将升级 21 个软件包，0 个新软件包，0 个待移除且 0 个未升级。这是升级而不是新软件的安装，所有新软件包仅占用 623KB 的空间。软件包正在覆盖现有文件。

必须理解，基本的 `apt-get upgrade` 不会删除软件或添加新软件。因此，使用此命令来保持系统完全修补是安全的，并且永远不会破坏系统。然而，有时你会看到 "0 upgraded" 状态发生变化，这意味着某些内容无法升级。这发生在某些软件必须安装或删除以满足更新软件包的依赖关系时，而如前所述，`apt-get upgrade` 从不这样做。在这种情况下，你需要使用 `apt-get dist-upgrade`，因为它旨在允许用户从一个版本的 Debian/Ubuntu 升级到更新的版本——一次升级不可避免地会改变系统上的几乎所有内容，删除过时的软件——并安装最新的功能。这是 Debian 最受喜爱的特性之一，因为它使你能够在版本之间移动，而无需下载和安装新的 CD。将常规升级和发行版升级分开非常有用，可以确保安全更新和简单的错误修复不会更改你可能依赖的软件配置，尤其是在需要持续可用和正常工作的机器上，例如服务器。
