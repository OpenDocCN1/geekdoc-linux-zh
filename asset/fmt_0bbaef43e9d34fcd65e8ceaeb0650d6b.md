
它并不依赖你的打字技巧；命令行可能是一个耗时且令人沮丧的体验。终端配备了许多节省时间的快捷键。在本节中，让我们看看如何访问之前的命令和历史、命令以及建议：

- 上/下箭头：使用此键查看命令历史
- `History`：使用这些键
- `Ctrl+R`：搜索命令历史。输入字母向下搜索，显示最近的命令，按 `Ctrl+R` 查找其他匹配项
- `Tab`：查看建议，或如果只存在一个建议则自动补全单词或部分。按一次 `Tab` 自动填充用户名，按两次 `Tab` 自动填充主机名。

## 终端命令

虽然可以通过结合软件中心和 `Ubuntu` 的“软件与更新”面板来安装和管理软件，但使用免费的高级软件包工具（`APT`）通常更快。以下是你可以使用的一些关键命令（见下方列表）：

- `sudo apt update` 列出 `/etc/apt/sources.list` 中列出的所有可用软件包源。
- `sudo add-apt-repository` 添加新存储库。
- `sudo apt upgrade` 从所有列出的存储库获取最新软件包（包括更新）。
- `sudo apt install` 安装新软件包。
- `sudo apt remove` 移除已安装的软件包。
- `sudo apt autoremove` 移除不再需要的配置文件。
- `sudo apt-upgrade` 更新所有安装的软件包。

```
ubuntu@desktop:~$ sudo apt-get update
[Reading package lists... Done]
Building package lists... Done
Get:1 http://archive.ubuntu.com/ubuntu focal In [11.4 kB] amd64 main (focal-backports-updates-1)
Get:2 http://archive.ubuntu.com/ubuntu focal-updates In [11.4 kB] amd64 main (updates-1)
Get:3 http://archive.ubuntu.com/ubuntu focal-security In [114 kB] amd64 main
Get:4 http://archive.ubuntu.com/ubuntu focal-updates In [116 kB] amd64 universe (updates-1)
Get:5 http://archive.ubuntu.com/ubuntu focal In [11.4 kB] amd64 restricted (focal-backports-updates)
Get:6 http://archive.ubuntu.com/ubuntu focal In [11.4 kB] amd64 universe (focal-backports-updates)
Get:7 http://archive.ubuntu.com/ubuntu focal-security In [114 kB] amd64 restricted
Get:8 http://archive.ubuntu.com/ubuntu focal-security In [114 kB] amd64 universe
Reading package lists... Done
Building package lists... Done
All packages are up to date.
ubuntu@desktop:~$
```

![](img/f2b7b)

## 终端：文件操作

是时候将注意力到通过喜爱的终端（`Terminal`）导航文件系统以及操作文件和文件夹了。

我们之前向你介绍了使用终端的基础知识。通过像你的 Linux shell 显示命令结构（`--option`）那样来揭示它，这为你提供了管理软件包包和文件的工具。这一次，我们将查看如何导航文件系统、处理文件和文件夹，并顺便学习更多节省时间的快捷键。

当你打开一个新窗口时，命令提示符会自动将你置于主目录。你可以通过列出当前文件夹的内容来验证这一点。`ls` 显示应用程序名称、文件和目录，之间用空格分隔。`ls` 命令可以显示所有文件，包括以点（`.`）开头的文件，这些文件通常是隐藏的。然后 `--recursive` 基本上意味着子文件夹的内容也会被显示。

如果你想获取关于文件内容的详细信息——权限、所有者、组，以及文件大小和最后修改日期。如果你想以 `KB` 为单位列出文件，可以使用 `-k` 选项，或使用 `--block` 以 `GB` 为单位。

文件还有许多选项，你可以使用 `--help` 选项来了解它们。

导航文件系统是使用 `cd` 命令完成的——从当前目录进入一个子文件夹，使用 `cd <folder>`，将 `<folder>` 替换为你想要访问的文件夹名称。记住文件和文件夹是区分大小的，所以

## 更快的导航

![](img/f2b72995a1be50e1613a2c5b8b47f2e9_137_0.png)

在最后部分，我们展示了一些实用的快捷键来帮助你快速输入命令，以下按键将帮助你高效地导航终端本身：

- `Home` 键将光标跳转到当前行的开头或结尾。
- `Ctrl+left/right` 快速移动。
- `Ctrl+u` 清空整行并重新开始。
- `Ctrl+k` 删除光标位置之后的所有内容。
- `Ctrl+w` 删除光标前的单词。不小心删除了命令中的 `sudo` 吗？只需输入 `!!` 并按回车即可重复上一个命令，并带有 `auto` 进行编辑。如果你在输入命令时中错了，与其重试整个命令，不如使用以下语法修复拼错的单词（在本例中，`apply` 原在参数之间）。

### 当路径包含空格或特殊字符时，使用 ' 和 \` 字符。

如果文件夹以大写字母开头——如你的 `Documents` 文件夹，如果文件不存在或它是小写的，你将收到错误，例如 `cd documents`。你也可以使用 `cd ../folder/subfolder` 同时向上移动几级。要返回一级，使用 `cd ..`，或使用 `cd ../` 移动二级，以此此类推。

你想去其他地方怎么办？使用 `cd /` 进入根目录，或通过输入路径导航网络上的任何系统，包括使用 `~` 字符导航到主目录，例如 `cd ~/Downloads`。

`-` 的工作方式与 `!` 类似，它带你回到上一个目录。所以使用 `cd -`。`Documents` 等同于你输入 `~/Documents`。

## 提升学习

现在你开始在终端中大显身手了，如果通过指令在每次需要时显示随机命令的信息来扩展你的知识又如何？如果你需要编辑文件，打开终端并输入以下内容：

```
nano <filename>
```

这会在 `nano` 编辑器中打开文件。使用光标键滚动到文件底部。要退出，按 `Ctrl+O`，然后按 `Enter` 保存，再按 `Ctrl+X` 退出 `nano`。关闭终端窗口并打开新窗口执行下一个命令，或者使用实际命令获取详细描述：`<command>--help`

```
echo "Did you know?; what is $(whoami -u -n))"
```

`(*)` 可以快速访问长名称的文件，例如 `Document.txt`。如果后面只有一个文件，这会生效。如果有两个（`Document` 和 `Documents`），终端将打开第一个匹配的文件。要此操作，你可以使用 `cd Doc` 来启动（除非你有一个名为 `Documents` 或 `Directories` 的文件夹）。使用唯一的通配符 `*` 来搜索包含某些字符的文件，例如 `Doc*`——`Documents/Work`。如果有多个文件匹配你的通配符，你必须完整输入文件名，例如 `mkdir Directory*` 来创建两个名为 `Directory` 和 `Work` 的独立文件夹。要进入它们，使用 `cd Directory*`。要移动，使用 `ls -Directory*`。

## 文件操作

你现在可以导航目录并管理你的文件系统了，做些实用的事情怎么样，比如创建一系列命令和你学到的技巧，这些将帮助你今天脱颖而出。

让我们先查看用于（复制）和（移动）文件的命令。语法是 `cp <source> <target>`。源和目标路径遵循与 `cd` 命令相同的规则，但它更容易，因为你只需要提供要复制或移动的文件路径。否则，你只需指定相同目录下的文件或文件夹名称。

```
cp <source> <target>
```

这将创建一个同名文件的副本。复制的文件存储在指定的目录中，如果存在则重命名。`mv <source> <target>` 移动文件或对其重命名。

```
mv <source> <target>
```

在上述任何命令中替换 `<source>` 和 `<target>`，文件将被移动、重命名或复制。如果目标已存在，它将被覆盖，除非你使用 `-i` 标志。无论你想如何，在覆盖之前只需这样添加 `-i` 标志：

```
cp -i <source> <target>
```
