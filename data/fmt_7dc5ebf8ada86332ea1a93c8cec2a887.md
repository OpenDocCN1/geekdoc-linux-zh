
- `sudo apt update`：从所有列出的仓库获取最新的软件包（包括更新版本）。
- `sudo apt-upgrade`：将所有已安装软件包升级到最新版本。此软件包还将安装任何所需的依赖项。
- `sudo apt purge`：使用此项删除已安装的软件包。它还会移除所有配置，`apt autoremove` 用于移除不再需要的软件包。
- `sudo apt upgrade`：在更新之前升级已安装的软件包。使用此命令 `apt get check`：损坏依赖关系的诊断工具，`apt autoclean` 从已删除的软件包中移除旧文件。

```
$ user@ubuntu:~$ apt update
Building index lists... Done
Reading /etc/apt/sources.list...
Get:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://archive.ubuntu.com/ubuntu focal-security main-universe InRelease
Get:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease
Get:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease
Reading package lists... Done
Building package list... Done
Reading package lists... Done
All packages are up to date.
```

![](img/1e7c2db42dac866a51ace142_0.png)

## 受限制访问

当你打开终端时，你会看到类似的内容：`username@hostname~$`。这表示你登录了自己的用户账户。这意味着你可以直接运行的命令数量有限。例如，如果以 root 身份看到 `root@hostname#~$`，这表示你对命令和文件有无限访问权限。

`ls` 命令列出目录内容。它提供了文件夹内容的详细信息，包括：权限；文件名；修改日期以及以字节为单位的大小。你可以不带任何参数运行它，或者带有 `-l` 提供目录中所有文件和文件夹的基本列表。你也可以结合命令和选项使用它。所有命令中最实用的是 `--help` 命令，它提供了工具的简要描述，列出所有可用命令及其选项。`apt search` 可用于搜索特定依赖。要解决这个问题，你需要使用具有 root 权限的账户（或使用 `sudo` 命令）并输入 `adduser`。你也可以通过列出你想要添加的所有组来创建和使用其他用户。例如：`sudo adduser admin`。

终端非常好，它允许你以 root 身份启动应用程序。确保在应用程序运行时保持窗口；否则当终端结束时，在终端中点击 Ctrl+C 停止正在运行的程序并返回桌面。我们已经讨论了 `--help`，但还有其他你可以使用的有用工具。例如，`man` 你可以在任何命令后输入以获取所有元素的简要描述，例如 `apt get install` 它将显示软件包的描述以及 `apt get` 是什么。对于完整的手册，终端为你提供了对发行版在线文档的访问。

在上部分我们展示了一些帮助你更快速输入命令的快捷键，但以下按键将帮助终端本身更高效地运行。

## 增强学习

现在你开始在终端（Terminal）中锻炼你的肌肉了，但如何通过让它在每次打开时显示关于随机命令的信息来扩展你的知识呢？要做到这一点，你必须编辑它，因此打开终端并输入：

```bash
nano ~/.bashrc
# 这会在文本编辑器中打开该文件。使用光标滚动到文件末尾，然后添加以下行：
echo "I know that: ${RANDOM} is bin!"
```

按 Ctrl+O 保存文件（按回车键覆盖），然后按 Ctrl+X 退出。现在打开一个新窗口或标签页获取命令的简要描述。只需使用带有较长描述的命令：--help

`~` 符号将你放在主目录。如果你输入 `cd ~/Documents`，它等同于 `cd /home/username/Documents`。最后的 `..` 可以让你快速回到上一个目录？简单，只需 `cd ..` 即可：

## 操作文件和文件夹

你现在可以列出并导航你的文件系统了，但删除某些东西，比如创建和复制文件呢？你会发现一系列命令以及你学到的移动技巧将在这些方面对你很有帮助：

让我们先查看复制 `cp` 和移动 `mv` 文件。这两个命令都适用于相同的选项。基本语法为：`cp [source] [destination]` 或 `mv [source] [destination]`。记住该命令的以下规则，通常的做法是先导航到文件夹，这样你就可以简单地复制文件名或文件夹作为源，例如 `cp ~/Documents/backup`。

以下操作将创建一个文件的副本并将其重命名：`cp ~/Documents/backup backup.out`。如果你想创建一个同名的文件副本，只需使用 `cp ~/Documents/backup ~/Documents/backup`。该命令会移动文件，因此它会被删除并重命名。如果已经存在一个同名文件会怎样？它会被覆盖。如果你想避免覆盖它，可以这样添加 `-i` 标志：`cp -i invoice.docx`。

你可以使用 `cp -r` 复制文件夹。在这里，你需要包含 `-recursive`（递归）标志，这可以确保文件夹及其所有内容被复制，并按照相对于父文件夹的位置正确排列：`cp -r folder1`

如果 `backup` 文件夹存在，则会重建 `Documents` 文件夹；如果不存在，则创建 `backup` 文件夹并将 `Documents` 的内容复制到其中。

你可以使用 `rm` 命令删除单个文件：例如：`rm filename`。`rm` 命令删除文件，但只删除空文件夹。如果你想删除一个文件夹及其所有内容，请使用 `-r` 标志：`rm -r folder`

你还可以使用 `mkdir` 创建新文件夹——只需输入 `mkdir folder`，将 `folder` 替换为你的文件夹名称。使用 `touch` 命令创建任何文件，例如：

通配符（Wildcards）用于加速搜索，也可以用于过滤命令——`*` 字符可以快速访问带有名称的文件，例如：`document*`。如果只有一个该名称的文件，这种方法将有效。如果有多个文件，命令将为第一个匹配的文件 `Document` 执行。为了避免这种情况，请使用 `cd:Document*`。

有些通配符在搜索时更有用：单字符标记符 `?` 和括号 `[]`。使用单字符标记符或括号可以处理包含空格的文件，例如 `*Documents*` 或 `[Documents]*`。以这种方式创建文件夹时，使用 `mkdir Who*` 会创建两个名为 `Who` 和 `who` 的文件夹。使用 `mkdir Who?` 可以得到该文件夹。使用 `mkdir Who*` 也能得到该文件夹。

最后，我们展示一些允许你在单行中运行多个命令的字符。`&` 参数也可以实现这一点，你可以使用以下命令来更新你的报告并更新所有可用软件：`sudo apt update && sudo apt get upgrade`

`&&` 是与（AND）命令，只有当第一个命令成功完成时，第二个命令才会运行。`|` 是或（OR）命令，如果第一个命令失败则运行。如果你想在第一个命令结束后无论发生什么都运行第二个命令，请使用 `;`：`sudo apt update; sudo apt-get remove`

![](img/1e7c2db42dac866a51a0ace7df48feef_144_0.png)

小提示

服务管理器允许你右键点击文件并选择“在终端中打开”，但你也可以使用

从软件中心安装 `install-software`，然后输入 `multiple_type: a`

选项将显示为

| 权限 | 所有者 | 组 | 大小 | 日期 | 名称 |
|---|---|---|---|---|---|
| -rw-xr-x-- | 1 root | root | 4268 | Jan 15 12:34:56 | backup |
| -rw-r--r-- | 1 root | root | 1234 | Jan 15 12:35:07 | invoice |
| -rw-r--r-- | 1 root | root | 5678 | Jan 15 12:36:12 | notes |
| -rw-r--r-- | 1 root | root | 9012 | Jan 15 12:37:23 | documents |
| drwxr-xr-x | 2 root | root | 4096 | Jan 15 14:48:00 | desktop |
| drwxr-xr-x | 2 root | root | 4096 | Jan 15 14:49:54 | folder1 |
