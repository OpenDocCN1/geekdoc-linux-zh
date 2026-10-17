
# 周六晚间复答案

1. 与 `Windows 95/98/NT` 一样，`GNOME` 桌面窗口底部有一个状态栏，并有一个类似于 `Windows` 开始按钮的主菜单按钮。此外，我可以像在 `Windows 95/98/NT` 中那样，在桌面上放置文件和图标。

2. 我通过 `GNOME` 控制中心（`GNOME Control Center`）来自定义 `GNOME` 桌面的外观和感受。我可以自定义背景、窗口管理器，或者为用户界面选择用户。

3. `Sawfish` 是一个窗口管理器。它是 `GNOME` 的默认窗口管理器。要配置 `Sawfish`，我在 `GNOME` 控制中心菜单中选择“桌面窗口管理器”（`Desktop Window Manager`）。

4. 要将默认桌面从 `GNOME` 切换到 `KDE`，我选择主菜单中的“桌面切换工具”（`Desktop Switching Tool`），然后选择 `KDE` 作为桌面。在 `KDE` 中，我也可以使用相同的切换工具将默认桌面切换回 `GNOME`。

5. 我使用 `KDE` 控制中心来自定义 `KDE` 桌面的各个方面。

# 练习答案

6. 要从 `GNOME` 桌面选择并尝试屏幕保护程序，我通过点击 `GNOME` 面板上的工具箱图标启动 `GNOME` 控制中心，并在控制中心的树状菜单中选择“桌面”（`Desktop`）->“屏幕保护程序”（`Screensaver`）。

7. “锁定屏幕”意味着在输入密码之前，屏幕保护程序不会关闭。在 `GNOME` 中配置屏幕保护程序时，我勾选“需要密码”（`Require Password`）复选框并启用它。然后屏幕保护程序就会锁定屏幕。

8. 我选择 -> `KDE` 控制中心。然后我在 `KDE` 控制中心的树状菜单中选择“桌面”（`Desktop`）->“屏幕保护程序”（`Screensaver`）。从那里我可以选择并配置屏幕保护程序。

9. `AisleRiot`、`Gnome-Stones` 和 `GNOME` 麻麻将是 `GNOME` 中的游戏。`AisleRiot` 是一个纸牌游戏程序，可以玩 30 种不同的纸牌游戏，包括接龙（`Freecell`）和纸牌牌（`Klondike`）等著名游戏。

10. 扫雷（`Minesweeper`）、纸牌（`Patience`）和四棋（`Shisen-Sho`）是 `GNOME` 中的游戏。

11. 我通过 `Ctrl+Alt+F1` 切换到文本模式控制台。然后登录 `root` 并输入 `/usr/sbin/sdconfig` 来启动声音配置程序。然后我按照程序的提示配置声卡。

12. 要播放音频 CD，我可以使用 `playcd` 或 `GNOME` 或 `KDE` 中的 CD 播放器。为了允许普通用户播放音频 CD，我登录 `root` 并输入 `chmod o+r /dev/cdrom`。

13. `GNOME` CD 播放器从 `CDDB` 获取歌曲——这是一个互联网上的 CD 数据库。假设有活跃的网络连接，`GNOME` CD 播放器会从 CD 数据库下载信息。

14. `GIMP` 和 `Pix` 是 `Red Linux` 自带的两个图像处理程序。`GIMP` 是用于查看图像以及执行照片修复、图像合成和图像创建任务的程序。`Pixpaint` 是模仿 `MacPaint` 的位图绘画程序。

15. 我使用 `Ghostview` 查看 `PostScript` 文档。

16. 电子表格、拼写检查器、日历和计算器是本书 `Red Hat Linux` CD-ROM 中的一些办公实用程序。CD-ROM 不包含任何完整的办公效率套件。

17. 电子表格应用程序的名为 `Gnumeric`。`Gnumeric` 的默认文件格式是 `XML`（可扩展标记语言）。`Gnumeric` 可以与 `Microsoft Excel` 交换文件。

# 附录 A

18. `ispell report.txt`

19. `Linux` 版 `WordPerfect 2000`、`Linux` 版 `Applicware Office` 和 `StarOffice` 是 `Linux` 的商业办公套件。可以通过访问它们的网站了解更多关于这些商业应用程序。

20. `StarOffice` 是一个跨平台解决方案。它包含了用于文字处理的 `StarOffice Writer`、用于电子表格的 `StarOffice Calc`、用于演示的 `StarOffice Impress` 以及用于数据库的 `StarOffice Base`。

# 周日晨复答案

1. 启动时的 `init` 进程取决于运行级别、`/etc/initab` 文件的内容以及许多 shell 脚本（位于 `/etc/rc.d` 目录及其子目录中）。

2. 我寻找第三字段中包含 `initdefault` 关键字的行（字段之间用冒号分隔）。该行的第二个字段指定了我们系统的默认运行级别。

3. `init` 进程根据运行级别顺序运行 `/etc/rc.d` 脚本。

4. 许多开源软件包以源码的形式分发。

5. 开源软件通常以压缩包（也称为 `tarballs`）的形式分发。

6. 下载 `tar` 包后，我寻找带有 `README` 或 `INSTALL` 字样的文件以获取如何构建的说明。

7. `RPM` 指红帽软件包管理器（`Red Hat Package Manager`），这是一个用于打包必要文件的系统。

# 练习答案

要检查系统是否安装了某个软件包，我输入命令 `rpm -q package_name`，其中 `package_name` 是 `RPM` 的名称。例如，检查是否安装了 `samba`，我输入 `rpm -q samba`。

8. 我使用图形界面程序或 `rpm` 命令行工具安装 `RPM`。要使用命令行工具安装 `RPM`，我切换目录到 `RPM` 目录（通常为 `/mnt/cdrom/RedHat/RPM`）并输入 `rpm -i filename`，其中 `filename` 是 `RPM` 的名称。

9. 一个典型的 `RPM` 格式为 `Free86-3.3.6-20.i386.rpm`。到第一个横线之前的内容都是 `RPM` 名称（`Free86`）；两个横线之间的数字构成了版本号（`3.3.6`）；下一个数字是 `RedHat` 的发布版本（`20`）；下一个扩展名（`i386`）表示这是一个 `RPM` 文件。

10. 在对内核进行补丁处理、直接在内核中添加 `SCSI` 支持或为某些实验性硬件添加支持后，可能会重新编译 `Linux` 内核。

11. 我登录 `root` 并使用命令 `/mnt/cdrom/RedHat/RPM` 挂载 CD-ROM，然后输入以下命令：

```
cd rpm -ivh kernel-source*
```

12. 为了重新编译内核，必须配置内核、内核、制作模块并安装内核和其他几个文件。

13. 我可能想在晚上备份文件、晚上下载大文件，或者在未来的某个时间给自己发送邮件提醒。我可以使用命令提交要执行的命令。我可以使用 `crontab` 功能按间隔自动运行程序。

14. 关于调度单个任务的示例，假设我想在晚上 23:35 执行 `/usr/local/bin/ppp-off` 脚本；我登录 `root` 并输入以下命令：

```
at 23:35

/usr/local/bin/ppp-off
```

（按下 `Ctrl+D`）

15. 我首先创建一个包含我要定期执行的命令的 shell 脚本。准备一个包含我想要执行该 shell 脚本的时间信息的文本文件。然后通过 `crontab` 命令提交此文件。

# 附录 A

16. 我创建 `/etc/at.allow` 文件，其中包含允许提交一次任务的用户名。对于周期性任务，我创建 `/etc/cron.allow` 文件，其中包含允许使用 `crontab` 命令提交周期性任务的用户名。

17. 软磁盘、`SCSI Zip` 磁盘和 `SCSI` 磁带是我用来备份文件的某些介质。软磁盘驱动器的设备名称为 `/dev/fd0`，`SCSI Zip` 驱动器为 `/dev/sda`（假设它是第一个驱动器），`SCSI` 磁带驱动器为 `/dev/st0`。

18. 我可以使用 `tar` 工具备份文件和目录。要备份 `SCSI` 磁带驱动器上的整个文件系统，我输入：

```
tar cvf /dev/st0 /
```

19. 为了将 `/home/share` 目录下的几个大文件备份到多块软磁盘上，我使用以下命令：

```
tar cvm /dev/fd0 /home/share
```

20. 为了在单个磁带上存储多个归包，我使用非回绕磁带设备，并使用如 `tar cvf /dev/nst0 /home` 的命令，然后使用类似的 `tar` 命令逐一个创建一个归包。我可以使用以下命令回绕磁带：

```
mt -f /dev/nst0 rewind
```

我可以使用以下命令跳过一个归包：

```
mt -f /dev/nst0 fsf 1
```
