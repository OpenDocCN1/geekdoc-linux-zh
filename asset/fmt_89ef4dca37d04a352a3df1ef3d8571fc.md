
点击面板菜单。许多 Linux 桌面在屏幕顶部或底部包含一个面板，你可以通过它启动应用程序。例如，在使用 GNOME 桌面的系统中，你可以选择 `Applications`（应用程序） > `System Tools`（系统工具）来打开终端窗口。

在所有情况下，你都应该像在没有 GUI 时一样输入命令。Linux 提供不同的终端模拟器。在 Fedora、红帽企业 Linux (`RHEL`) 以及其他使用 GNOME 桌面的 Linux 发行版中，默认的终端模拟器窗口是 GNOME Terminal（由 `gnome-terminal` 命令表示）。

GNOME Terminal 支持基础 shell 之外的许多功能。例如，你可以在 GNOME Terminal 之间进行复制和粘贴、更改字体、设置标题、选择颜色或图像作为背景，并设置当文本滚动出屏幕时保存多少文本。

要尝试 GNOME Terminal 的功能，请启动 Fedora 或 RHEL 系统并登录桌面。然后按照以下步骤操作：

1. 选择 `Applications` > `System Tools` > `Terminal`。你的桌面上应该打开一个终端窗口。
2. 选择 `Edit Profiles`（编辑配置文件），然后在高亮 `Default`（默认）时，选择 `Edit`（编辑）。
3. 在 `General`（常规）选项卡上，取消勾选 "`Use system fixed width font`使用系统固定宽度字体）"复选框。
4. 在 `Choose Font`（选择字体）窗口中，尝试不同的字体并选择 `OK`（确定）。新字体将出现在终端窗口中。
5. 重新勾选 "`Use system fixed width font`" 复选框。这将回到原始字体。
6. 在 `Colors`（颜色）选项卡上，取消勾选 "`Use colors from system theme`（使用系统主题颜色）"复选框。在这里你可以尝试不同的字体和背景颜色。
7. 重新勾选 "`Use colors from system theme`" 复选框以返回默认颜色。

## 第三章：使用 Shell

8. 进入 `Profile`（配置文件）窗口。还有其他你可能想要尝试的功能，例如设置背景图像、使背景透明或设置保留多少滚动数据。
9. 完成后关闭 `Profile` 窗口。你现在已经准备好使用你的终端窗口了。

如果你从图形化桌面使用 Linux，你可能最经常通过终端窗口访问 shell。

### 使用虚拟控制台

大多数包含桌面界面的 Linux 系统会在计算机上运行多个虚拟控制台（`virtual consoles`）。虚拟控制台是在你正在使用的图形界面之外，打开多个会话的一种方式。

你可以通过按住 `Ctrl` 和 `Alt` 键并按下 `F1` 到 `F7` 之间的功能键在虚拟控制台之间切换。例如，在 Fedora 中，按下 `Ctrl+Alt+F1`（对于大多数 Linux 系统按下 `F2`、`F3`、`F4` 等直到 `F7`）可以显示七个虚拟控制台之一。第一个虚拟工作区是基于文本的虚拟控制台。你可以通过 `Ctrl+Alt+F1` 返回到 GUI（如果它正在运行）。在某些系统中，GUI 运行在虚拟控制台 7 或 5 上。因此，你应该按下 `Ctrl+Alt+F5` 或 `Ctrl+Alt+F7` 返回 GUI。

现在试一下。按住 `Ctrl Alt` 键并按下 `F3`。你应该看到一个纯文本的登录提示符。使用你的用户名和密码登录。尝试几个命令。完成后，输入 `exit` 退出 shell。然后按下 `Ctrl+Alt+F1` 返回你的图形桌面界面。你可以根据需要在这这些图形控制台之间来回切换。

### 选择你的 Shell

在 Linux 系统中，你的默认 shell 是 `bash` shell。要查找你的默认 shell 是什么，请输入以下命令：

```bash
$ am 1
chris pts/0 2011-11-26 07:19 (::0)
$ grep /etc/password
cnegeus:x:13597:1359::Chris Negus:/home/cnegeus:/bin/bash
```

`who am` 命令显示你的用户名，`grep` 命令（将 `chris` 替换为你的名字）显示你在 `/etc/password` 文件中的用户账户定义。条目中的最后一个字段显示 `bash` shell (`/bin/bash`) 是你的默认 shell（即在你登录或打开终端窗口时启动的 shell）。

虽然可能不太可能，但你可能设置了不同的默认 shell。要尝试不同的 shell，只需输入该 shell 的名称即可（示例包括 `ksh`、`tish`、`csh`、`sh`、`dash` 等，假设它们已安装）。你可以在该 shell 中尝试几个命令，然后在你准备好返回 `bash` shell 时输入 `exit`。

你可能会因为以下原因选择使用不同的 shell：

- 你正在使用 UNIX System V 系统（通常默认为 `ksh`）或太阳微系统（Sun Microsystems）或其他基于 Berkeley 的发行版（通常默认为 `csh`），并且你更习惯于这些环境的默认 shell。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
- 你想运行为特定 shell 环境创建的 shell 脚本，你需要运行为这些脚本而创建的 shell，以便你可以测试或使用这些脚本。
