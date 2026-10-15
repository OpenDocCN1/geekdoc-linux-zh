
# dpkg 使用示例

`dpkg -i yourfile.deb`

这将提取软件包并将其安装到你的系统上。如果你只是想在不安装到系统的情况下提取软件包内容，可以使用 `--unpack` 参数，如下所示：

```
dpkg --unpack yourfile.deb
```

与其提取软件包，你也可以让 `dpkg` 通过使用 `-c` 参数列出其内容，如下所示：

```
dpkg -c yourfile.deb
```

一旦软件包被安装，你可以使用 `-r` 开关并提供软件包名称来卸载它。注意：你需要提供软件包名称，而不是你安装的 `.deb` 的文件名。例如：

```
dpkg -i libgtk2.0-0.deb

dpkg -r libgtk2.0-0
```

你可以通过运行以下命令获取当前已安装的所有软件包的完整列表：

```
dpkg --get-selections
```

这通常与 `grep` 结合使用来检查是否安装了某个特定程序。例如：

```
dpkg --get-selections | grep gnumeric
```

如果看到一行 "`gnumeric INSTALL`"，则表示你已安装 Gnumeric。`--get-selections` 参数也适用于安装预定义的软件包选择。`--get-selections` 导出的软件列表也可以导入到另一台机器的 `dpkg` 中，从而确保两台机器具有相同的软件。要将你的软件包选择导出到文件，运行以下命令：

```
dpkg --get-selections > packages.txt
```

要将该列表导入回系统，运行以下命令：

```
dpkg --set-selections < packages.txt
```

请注意，这并不会实际安装任何软件；它仅在 `dpkg` 内部设置“选择状态”，意味着你已要求安装这些软件包。你需要使用 `Aptitude` 来继续安装这些软件包——只需按 "`g`" 它会显示由 `dpkg` 标记为安装的缺失软件包，然后再次按 "`g`" 继续安装它们。

## Configuring APT

如果你无法访问 Synaptic 等图形工具，可以使用基于控制台的编辑器手动编辑 APT 要读取的服务器。这在你想要添加自定义仓库、想要使用特定版本的 Ubuntu（例如比你最初安装的更新的版本），或想要使用本地仓库以避免重复下载软件包时也很有帮助。

APT 的源存储在 `/etc/apt/sources.list` 文件中，因此你需要通过 `sudo` 启动编辑器才能进行更改。阅读 `sources.list` 文件起初可能令人困惑，但实际上非常简单——特别是运行自定义仓库的人通常会告诉你确切需要输入的内容。

你在 `sources.list` 中会找到的两种类型的行是 "`deb`" 和 "`deb-src`" 。前者是可下载并正常安装运行的程序软件包，而后者提供预打包的源代码。坦白说，`deb-src` 很少使用，但保留它们也无妨。以 `#` 开头的注释行会被 APT 忽略。因此，如果你想暂时禁用一个仓库，只需在其行开头插入一个 `#`，保存文件，然后重新运行 `apt-get update`。

### sources.list 行格式

每行由以下几部分组成：

```
[deb/deb-src]  url  distribution  [components...]
```

URL 看起来会像 "`http://gb.archive.ubuntu.com/ubuntu/`"，并指向 APT 索引和软件包存储的位置。此 URL 对所有版本的 Ubuntu 都是相同的；发生变化的是行中的 "`distribution`" 部分，其紧随其后。它设置为你使用的发行版的 Ubuntu 代号的第一部分——"`warty`" 代表 4.10，"Warty Warthog"；"`hoary`" 代表 5.04，"Hoary Hedgehog"；"`breezy`" 代表 5.10，"Breezy Badger"；"`dapper`" 代表 6.06，"Dapper Drake"。顺便说一下，Ubuntu 下一个代号是 "`Edgy Eft`" ，因此如果你想升级到它，你需要使用发行版名称 "`edgy`"。

发行版之后是你要选择的各个组件。默认情况下这通常是 "`main restricted`" ，意味着你想要下载主要的 Ubuntu 软件包，以及任何受限版权材料。受限版权下的软件包是诸如二进制驱动程序之类的东西，因此最好保持 "`restricted`" 启用。你可能——可能在不同的 `deb` 行上——有相同的 URL 和发行版，这次带有

"`universe multiverse`" 组件。我们强烈建议您启用这两个组件，因为它们打开了一个庞大的软件集合，可让您充分利用本书和 Ubuntu 本身。

在 `sources.list` 文件底部，通常有一些 `deb` 行来处理安全更新。它有一个特殊的 URL，`security.ubuntu.com`，以及一个特殊的发行版名称，`dapper-security`。这应始终保持启用状态。

如果您对 `sources.list` 文件进行了更改，则必须运行 `apt-get update` 以在运行任何进一步的 APT 命令之前下载新的软件包信息。

在更改 `sources.list` 文件之前，我们强烈建议通过运行以下命令保留原始文件的备份：

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```
