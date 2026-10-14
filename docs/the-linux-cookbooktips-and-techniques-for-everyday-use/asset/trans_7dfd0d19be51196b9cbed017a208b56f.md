

## 《Linux  cookbook：日常使用的技巧与技术》：

在 Debian 系统上安装软件包有不同的方法：通过 `dselect`，从菜单中选择软件包；`dpkg`，用于安装软件包的命令行工具；以及 `apt-get`，是 Debian 新的“高级软件包工具”系统的一部分。

要安装已知名称的软件包，请挂载你的 Debian 发行版（例如，如果你通过 CD-ROM 安装 Debian，请将第一张 Debian CD-ROM 光盘放入 CD-ROM 驱动器）。然后使用 `install` 命令选项运行 `apt-get`，并将要安装的软件包名称作为参数给出。如果有必须先安装的额外软件包（称为依赖项），或该软件包与已安装的其他软件包冲突，将会提出一个修复操作，并提示你确认或中止操作。

- 要安装 `miscfiles` 软件包，输入：

```
apt-get install miscfiles RET
```

如果你已经有 `.deb` 文件，请使用 dpkg 安装它。使用 `-i` 选项并给出文件名称作为选项。任何冲突或依赖项都必须由你在使用软件包前解决。如果检测到问题，dpkg 将报告它并退出而不安装软件包。

- 要安装 `miscfiles-1.1.7.deb` 文件中的软件包，输入：

```
dpkg -i miscfiles-1.1.7.deb RET
```

最后，要浏览可用软件包并从菜单中选择它们，请使用 dselect，Debian 软件包选择工具。注意：它的菜单界面与你可能遇到的大多数程序不同，其使用方法不幸地是一种需要培养的技能。甚至 man 手册也提到这一点：“dselect 软件包选择界面对新用户来说令人困惑甚至令人不安。”

**NOTE：** 如果你刚开始使用 Debian，我建议查阅 [Dselect 初学者文档](#)。

### A.3.3 升级 Debian 软件包

人们不断为自由软件运动做出贡献。这意味着新的软件程序不断被添加到 Linux 发行版中，而当前软件程序也在不断改进——以匹配新硬件、更快的程序执行、安全性更新等等。因此，Linux 系统需要保持最新状态，以便获得最新自由软件的好处。

要升级单个软件包，请使用 `apt-get` 并使用 `install` 参数，然后跟上要升级的软件包名称。

- 要升级 `sview` 软件包，输入：

```
# apt-get install sview RET
```

此命令将把 `sview` 软件包升级到可用的最新版本，如果该版本高于你系统上已安装的版本。如果为了使此新软件包升级正常运行，必须先升级额外的软件包，此命令也会获取并升级这些软件包。在下载任何软件包之前，apt-get 会显示将要安装、替换或以其他方式更改的软件包列表，并先等待确认。

要使整个 Debian 系统保持最新，请使用以下命令参数使用 apt-get 工具。首先，使用 `update` 参数更新系统可用的软件包列表。然后再次运行 apt-get，使用 `upgrade` 参数将所有已安装软件包升级到最新可用版本，或在宣布 Debian 系统新版本时使用 `dist-upgrade` 参数升级到该新版本。

- 要将系统上的所有软件升级到最新版本，输入：

```
# apt-get update RET
...processing messages...
# apt-get upgrade RET
...processing messages...
#
```

- 要将你的 Debian 系统升级到最新发行版，输入：

```
# apt-get update RET
...processing messages...
# apt-get dist-upgrade RET
...processing messages...
#
```

### A.3.4 安装 Shell 脚本

Shell 脚本是一个包含用 shell 命令语言编写的命令的文件（参见章节 The Shell）。你运行（或“执行”）脚本的方式与运行任何其他命令相同（参见章节 Running a Command）。首先，确保脚本文件是可执行的；如果不是，你将无法执行它（参见章节 Making a File Executable）。

通常，管理员将新的 shell 脚本安装在 `/usr/local/bin` 目录中。如果你在一个多用户系统上，并且你是唯一可能运行某个特定脚本的用户，你可以将其放在主目录树中的一个特殊目录——`~/bin` 目录是这里的标准建议——然后将该目录添加到你的路径中（参见章节 Adding to Your Path）。

并非所有可执行脚本文件都是 shell 脚本。脚本的第一行包含用于解释和执行脚本的 shell 或其他程序的完整路径名；有时，该路径在你的系统上可能不同

