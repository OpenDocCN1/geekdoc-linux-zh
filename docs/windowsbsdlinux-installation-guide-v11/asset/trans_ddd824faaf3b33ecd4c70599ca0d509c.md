

4. 这会显示一个确认屏幕，选择“是”并按回车。

5. 你的硬盘被检测到，NetBSD 会相应地为其命名。在我的电脑上，我的第一块 IDE 硬盘被命名为 wd0。按回车继续。

6. 接下来出现“磁盘几何结构”屏幕，在此将你的硬盘驱动器几何结构与 BIOS 几何结构进行匹配。如果 sysinst 无法将你选择的磁盘唯一地与 BIOS 已知的磁盘匹配，那么你必须手动设置磁盘几何结构。在我的例子中，该磁盘与以下 BIOS 磁盘匹配：

# BIOS# cylinders heads sectors

| BIOS# | cylinders | heads | sectors |
| 0 | 1023 | 255 | 63 |

7. 因此我选择“这是正确的几何结构”并按回车。接下来是让你选择是否要多启动系统而不是危险地独占系统的屏幕。选择“仅使用磁盘的一部分”而不是“使用整个磁盘”并按回车。

8. 继续选择“使用的大小单位”。我选择了“兆字节”作为我的大小指定单位。

9. 按常规继续安装，直到到达 NetBSD fdisk，在那里你可以查看计算机上的 DOS 分区表。我的计算机系统运行的是 Windows 98（SE）、NetBSD 1.6 和 FreeBSD 4.8-RELEASE。DOS 分区表如下：

# Total disksize 19541 MB.

| Start(MB) | Size(MB) | End(MB) | Kind |
| 0: 0 | 9774 | 9774 | Windows FAT32, LBA |
| 1: 9773 | 3001 | 12775 | NetBSD |
| 2: 12774 | 6766 | 19540 | old NetBSD/FreeBSD/386BSD |
| 3: | | | unused |

10. 通过将“Kind”设为“unused”来编辑分区 1 和 2，然后选择“Partition OK”并按回车。

11. 然后选择未使用的分区 1，然后选择“Kind”，然后选择“NetBSD”，最后选择“Start and size”。将“Start:”值设为“~0”，“size:”设为你想要设置的值。我选择了大约 4000 MB。确保你选择“Set active”并按回车，最后按“Partition OK”。

12. 我电脑上的新 DOS 分区表如下所示：

# Total disksize 19541 MB.

| Start(MB) | Size(MB) | End(MB) | Kind |
| 0: 0 | 9774 | 9774 | Windows FAT32, LBA |
| 1: 9773 | 4001 | 13774 | NetBSD |
| 2: | | | unused |
| 3: | | | unused |

13. 选择“Exit”并按回车。

14. 下一个屏幕会告诉你计算机上安装了多个操作系统。当被问及是否安装启动选择器时，回答“是”。

15. 这会带你进入“Bootselection menu items”屏幕。在这里，你可以更改用于匹配分区条目的简单菜单条目，这些条目在系统启动时会显示。此外，你还可以指定超时时间（以秒为单位）和默认操作（如果在启动菜单中未进行选择）。默认情况下，启动菜单超时设置为 10 秒，我将其更改为 100 秒。默认启动菜单操作设置为“Boot off partition 0”。

16. 然后编辑菜单条目 0 和 1，分别命名为“Windows”和“NetBSD”。然后退出。

17. 接下来出现 NetBSD Disklabel 屏幕。在这里你需要设置你的 NetBSD 磁盘标签。列出了四个选项：Standard、Standard with X、Custom 和 Use existing。

18. 我选择了安装类型：“Standard with X”，它需要大约 450.00 MB 的硬盘空间。

19. 下一个屏幕显示 BSD-disklabel 分区。由于对于大多数人在大多数情况下这最合适，请保持更改不变并选择“Partitions are OK”然后按回车。

20. 会提示你为 NetBSD 磁盘命名，我输入了“ghosh”并继续。

21. /sbin/newfs 运行以创建新的文件系统。

22. 在下一个屏幕中，你会被提示安装普通启动块或串行启动块。由于我们使用 BIOS 控制台设备作为控制台，你必须选择“Use normal bootblocks”并按回车。

23. 这完成了 NetBSD 安装程序的第一部分。Sysinst 已向目标磁盘写入磁盘标签，并对磁盘上的新分区执行了 newfs 和 fsck。下一步是获取并解包发行版文件系统。

24. 我选择了 NetBSD 发行版集的“Custom Installation”。

25. 在下一个屏幕中，选择你想要安装的所有内容并按“Exit”。

26. 输入安装介质类型。选择“cdrom”以及设备::cd0 和目录:/i386/binary/sets 然后继续。

27. 以下 .tgz 文件将被解包并安装到你的硬盘上：base.tgz、etc.tgz、comp.tgz、games.tgz、man.tgz、misc.tgz、text.tgz、xbase.tgz、xfont.tgz、xserver.tgz、xcomp.tgz 和 xcontrib.tgz。

28. 出现一条消息“All selected distribution sets unpacked successfully”。接下来，设备文件会自动创建，并提示你进行一些必要的安装后配置步骤。

29. 你需要设置时区，我选择了“Europe/Moscow”。

30. 接下来，选择密码加密方式。可用的选项有：DES 或 MD5。我更喜欢 MD5 而不是 DES。

31. 我设置了 root 密码，然后屏幕上最终出现一条消息，告诉你 NetBSD 1.6.1 操作系统已成功安装在你的计算机上。重新启动计算机以从硬盘启动。

32. 当我第一次重新启动时，屏幕上出现以下提示：F1 Windows，F2 NetBSD 各占一行。我按下 F1 功能键启动到 Windows 98（SE）并检查一切是否完美运行。正如所料，它确实可以！然后我重新启动，这次我按下 F2，这将我登录到 NetBSD 1.6.1。

33. 根据你的计算机配置，首次启动到 NetBSD 时屏幕上会出现启动消息。尽管消息滚动得相当快，无法读到任何有用的内容，但你始终可以使用“/sbin/dmesg | more”命令稍后阅读。最后，你将到达登录提示。使用安装期间设置的用户名/密码登录。检查一切是否就位并尝试探索新系统。

