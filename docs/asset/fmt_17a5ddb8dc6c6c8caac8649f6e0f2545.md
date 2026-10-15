
挂载听起来可能很复杂，但不用担心——它几乎总是自动完成的，要么在启动时对永久连接到电脑的设备进行，要么在将可移动存储设备连接到电脑时进行，例如 USB 棒。事实上，你可能根本不会注意到它的发生；用户在插入 USB 记忆棒后看到的只是桌面上出现一个新图标，双击后即可浏览 USB 棒上的文件。当然，如果用户仔细观察，她会看到自己实际上是在浏览 USB 记忆棒被挂载到的文件夹。

### 文件和文件夹名称

文件和文件夹名称可以包含空格，就像 Windows 一样，但在 Linux 中大小写字母很重要。一个文件夹完全可以包含名为 `Report.doc`、`REPORT.doc`、`report.doc`、`REPORT.doc` 等等的文件。

请参阅图 4-1，了解其实际操作的示例。屏幕截图的上半部分显示了在 Windows 中尝试将文件重命名为 `REPORT.doc` 的尝试，而该文件夹中已存在名为 `report.doc` 的文件。这是不允许的，因为 Windows 无法区分大小写字母——就它而言，`report.doc` 与 `REPORT.doc` 是同一个文件。屏幕截图的下半部分显示了 Ubuntu 系统上的一个文件夹，其中包含多个具有 `report.doc` 大小写变体的文件。

![](img/48d064407ff591f0b5365c2d2919ee6e_68_0.png)

> 注意 操作系统区分大小写字母的能力称为大小写敏感。

此外，Ubuntu 下的文件和文件夹名称可以包含几乎任何字母、数字或符号，除了正斜杠（`/`）。

> 注意 虽然 Windows 称之为文件夹，许多 Linux 用户称之为目录。讨论的是完全相同的东西。目录一词几乎总是在命令行中使用，而在 Ubuntu 桌面上使用时则更喜欢文件夹一词。

### 重要文件系统位置

系统上的每个用户都会在 `/home` 文件夹内获得自己的文件夹来保存个人数据。例如，用户 Jane 是 given the folder `/home/jane`. The `/home` folder is akin to `C:\Documents and Settings` under Windows.

TIP Linux users often refer to their folder within `/home` as their "home folder", saying things like, "I couldn't find the file but I remembered I'd saved it in my home folder."

Users aren't permitted to save their personal files outside of their `/home` folder. This is rigidly enforced using ownerships and file permissions, as I explain in the Understanding Users section below.

Outside of the `/home` folder, the Ubuntu filesystem is a little more complicated than Windows, and it isn't quite a case of program files being in one location, and system files in another.

A cursory rundown of the Ubuntu filesystem can be found in Table 4-1, although this is not essential knowledge and is provided largely for reference purposes.

Perhaps the most important locations for the majority of users are `/home`, as described above; `/usr/bin`, where practically all software is located; and `/etc`, where system configuration files are found.

NOTE Like many versions of Linux, Ubuntu broadly follows the Filesystem Hierarchy Standard (FHS) to decide where things should go in the filesystem. For more details, including in-depth descriptions of each location, see www.pathname.com/fhs/.

## Hidden files and folders

Windows lets users hide files and folders by setting a file attribute.

Linux takes a simpler approach. Any file or folder that has a period (`.`) at the beginning doesn't appear in file listings, unless the user specifically requests all files/folders be listed.

In other words, if you rename `report.doc` to `.report.doc`, it will instantly become invisible and will seem to disappear from the file browsing window (you might have to hit the Refresh button in the file browser window to update the listing before the file actually vanishes).

A user's personal configuration files are stored in his or her `/home` folder and are hidden in this way. To view them, and other hidden files, click View ⇨ Show Hidden Files in a file browsing window.

NOTE Any file or folder that has a tilde (`~`) at the end of its filename (i.e. `report.doc~`) will be hidden in file listings provided by the Nautilus file manager, and on the desktop. They will be visible everywhere else, including at the command-line.

## Table 4-1. Key locations in the Ubuntu filesystem.

| Location | Details |
|---|---|
| `/bin` | Essential software, typically needed to get the system running |
| `/boot` | Files related to the boot menu/loader |
| `/dev` | Virtual files representing hardware devices |
| `/etc` | System (global) configuration files |
| `/home` | Users' personal folders |
| `/lib` | Support (library) files required by software |
| `/media` | Contains subfolders where storage devices can be mounted |
| `/proc` | Virtual folder containing files representing stats and settings |
| `/root` | Personal folder of the root user |
| `/sbin` | Essential software for system maintenance, usually used only by the root user |
| `/tmp` | Temporary files/folders |
