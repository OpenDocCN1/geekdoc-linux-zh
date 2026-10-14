
`C:\Users\USERNAME\AppData\Roaming\Thunderbird\Profiles`

你应该能够使用 Windows 资源管理器导航到此文件夹。此目录下的 Thunderbird 配置文件名称格式为 `xxxxxxxx.default`，其中 `xxxxxxxx` 并不是名称的实际部分，而是代表你第一次启动 Thunderbird 时创建的唯一八字符序列。Thunderbird 包含你所有的账户信息，包括一个包含你所有账户信息和文件的 `Mail` 子目录。

在 Linux 系统上，邮件存储在具有相同格式的目录中，但其位置取决于你使用的 Thunderbird 版本：

- 如果你下载并使用的是来自 Mozilla 项目的官方版 Thunderbird，而不是 Synaptic 或 Apt-Manager，你的配置目录和配置文件（`profiles.ini`）将位于家目录下一个名为 `.thunderbird` 的目录中。
- 如果你使用 Synaptic 或 Apt Manager 安装了 Thunderbird，你的配置目录和配置文件（`profiles.ini`）将位于名为 `.mozilla` 的目录中（等等，原文写道）如果你使用 Synaptic 或 Apt Manager 安装了 Thunderbird，你的配置目录和配置文件（`profiles.ini`）位于家目录下一个名为 `.thunderbird` 的目录。这是存放 Thunderbird 初始化文件的目录的旧名称，Ubuntu 和 Debian 的人员保留了该名称，以确保与旧版 Thunderbird 安装的兼容。

# 第 9 章：从 Windows 系统迁移

在我看来，Ubuntu 和 Debian 保留了存放 Thunderbird 初始化和配置信息的目录旧名称很遗憾，但没有人问过我。

## 提示

在 Mac OS X 系统上，你的 Thunderbird 配置目录存储在两个位置之一：`~/Library/Thunderbird/Profiles` 或 `~/Application Support/Thunderbird/Profiles`。■

# 安装或更新 Thunderbird

- 如果你是第一次安装 Thunderbird，请阅读下一节（“将邮件导入 Thunderbird：新用户”）了解需要从 Windows 系统复制哪些文件到你的 Ubuntu 系统中，以及你需要如何修改 Thunderbird 配置文件。
- 如果你之前已经在 Ubuntu 系统上安装并使用过 Thunderbird，你可能想要保留旧的 Thunderbird 配置，并应跳过本节，“将邮件导入 Thunderbird：现有用户”。

# 将邮件导入 Thunderbird：新用户

如果你以前从未在 Ubuntu 系统上使用过 Thunderbird，可以从 Windows 系统复制转换后的邮件和配置初始化信息，让 Thunderbird 立即使用。

要此操作，在启动 Thunderbird 之前创建 `~/.thunderbird` 目录。接下来，将 Windows 备份中的 `xxxxxxxx.default` 目录递归复制到你在 Ubuntu 家目录中创建的 `~/.thunderbird` 目录。你可以根据使用的 Thunderbird 版本，从 CD、DVD 或网络位置复制此目录。

```
C:\Documents and Settings\USERNAME\Application Data\Thunderbird\Profiles
C:\Users\USERNAME\AppData\Roaming\Thunderbird\Profiles
```

## 提示

如果你在新机器上安装 Ubuntu，可以使用 Samba 在你的 Ubuntu 系统上挂载共享的 Windows 驱动器并复制文件。请参阅第 25 节“连接到其他系统”，获取有关在 Ubuntu 系统上挂载共享 Windows 驱动器的信息。■

# 第二部分：桌面用户

根据你使用的 Windows 版本，你还应该从 Windows 系统的该目录备份中将以下文件到你的 `~/.thunderbird` 目录：

在 Windows XP 及更早系统上：

```
C:\Documents and Settings\USERNAME\Application Data\Thunderbird\profiles.ini
```

在 Windows Vista 及后续系统上：

```
C:\Users\USERNAME\AppData\Thunderbird\profiles.ini
```

从 Windows 系统复制后，该文件最初看起来如下所示：

```
[General]
StartWithLastProfile=1
[Profile0]
Name=default
IsRelative=1
Path=Profiles/hushy55.default
```

将其复制到 Ubuntu 系统后，使用文本编辑器修改你从 Windows 系统复制的文件版本，并从 `Path` 变量中删除 `Profiles` 目录。更新后的同类文件如下所示：

```
[General]
StartWithLastProfile=1
[Profile0]
Name=default
IsRelative=1
Path=hushy55.default
```

当你在 Ubuntu 上首次启动 Thunderbird 时，它将立即使用来自 Windows 系统的配置目录，一切看起来和那里完全一样。如果是这样，恭喜你！你的邮件已成功迁移，你现在可以使用 Thunderbird 作为你的默认邮件客户端，恢复正常的邮件生活。

## 提示

如果你之后想切换到使用 Evolution，可以像后文“将 Thunderbird 导入 Evolution”章节描述的那样，轻松地将 Thunderbird 邮件导入这些应用程序。

# 将邮件导入 Thunderbird：现有用户

如果你已经在 Ubuntu 上使用 Thunderbird，只是在从 Windows 系统迁移旧邮件，那么 Ubuntu 系统家目录下的 `~/.thunderbird` 目录已经存在。该目录将已经包含一个命名类似于 `xxxxxxxx.default` 的默认配置目录以及你的配置文件 `profiles.ini`。

# 第 9 章：从 Windows 系统迁移

在这种情况下，你可能希望使用 Thunderbird 的导入功能将 Windows 系统中的 Thunderbird 邮件导入到现有的 Thunderbird 邮件文件中。因此，你需要访问 Thunderbird 存储 Windows 邮件转换版本的的目录。该目录应该位于你备份到 CD、DVD、外部驱动器或网络位置的，路径为 `C:\Documents and Settings\USERNAME\Application Data\Thunderbird\Profiles` 或 `C:\Users\USERNAME\AppData\Thunderbird\Profiles`。

你的 Thunderbird 邮件实际上存储在该目录的子目录中，名称类似于 `xxxxx.default/Mail/Local Folders`，其中 `xxxxx` 是在你首次启动 Thunderbird 时生成的随机字符串。该目录包含邮件文件以及用于存储 Thunderbird 配置的辅助文件。要确定你需要导入 Thunderbird 的哪些文件，请启动 Ubuntu xterm 控制台或切换到 `xxxxx.default/Mail/Local Folders` 目录，并执行如下命令：

```bash
$ find -not -empty | grep -v '.msf$|.sbd|$dat|^$
./Personal Folders.sbd/Inbox
./Personal Folders.sbd/Personal
./Personal Folders.sbd/Writing
```
