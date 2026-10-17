
a. `echo "November 5, 2003" > /tmp/audit`

b. `find -nouser >> /tmp/audit`

c. `ls -l | /tmp/audit`

d. `cat /tmp/audit`

- 2. 哪个命令通过覆盖文件中的现有数据来将数据保存到文件中？

a. `echo "November 5, 2003" > /tmp/audit`

b. `find -nouser >> /tmp/audit`

c. `ls -l | /tmp/audit`

d. `cat /tmp/audit`

- 3. 哪个命令允许所有用户访问名为 bboard 的目录？

a. `chmod 754 bboard`

b. `chmod 777 bboard`

c. `chmod 1754 bboard`

d. `chmod 4754 bboard`

- 4. 如果用户对目录具有写权限，但没有设置粘滞位（sticky bit）权限，则任何用户都可以删除目录中的任何文件，无论所有者如何。正确或错误？

- 5. 你想为 elvis 设置粘滞位。哪两个命令可以做到？

a. `chmod 4000 elvis`

b. `chmod 1000 elvis`

c. `chmod o+t elvis`

d. `chmod o+s elvis`

### 实验 5.5 使用 slocate 的高级功能

#### 目标

本实验的目标是让你熟悉 `slocate` 程序的功能。`slocate` 是 GNU locate 程序的高版本，具有额外的安全功能。使用 `slocate`，如果用户没有某些文件的权限，他们将看不到文件系统中存在的文件。

### 所需材料

本实验需要以下条件：

- 在运行 Linux 的计算机上具有普通用户访问权限
- 在运行 Linux 的计算机上具有 root 用户访问权限

预计完成时间：45 分钟

#### 活动

1. 按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用 root 账户登录终端。

2. 回到你的主目录。你可以在任何地方通过输入 `cd ~` 或直接 `cd` 来实现。

3. 检查是否有一个名为 `test` 的子目录。你可以使用命令 `ls test` 查看。该子目录可能存在于之前的实验中。如果不存在，使用 `mkdir` 命令创建它。

4. 使用命令 `echo "Hello World" > sample99` 在此目录中创建一个名为 `sample99` 的文件。

5. 检查 `locate` 命令是否能找到此文件。除非你的计算机上其他目录中恰好有一个同名文件，否则它找不到该文件。这是因为你刚刚创建了文件，而你的计算机每天只更新一次数据库。

6. 你现在可以强制计算机更新数据库。要这样做，请运行此命令：

7. 步骤 6 中的命令可能需要一段时间才能运行，因为它正在扫描你的几乎整个硬盘。你可以通过使用 `-e` 从扫描中排除目录来防止 `updateddb` 扫描你的整个硬盘，从而缩短更新数据库的时间。是从扫描中排除 `/root` 和 `/home` 目录的示例：

```
updateddb
updateddb -e "/tmp,/etc,/usr,/var,/bin,/sbin,/boot"
```

### 实验 5.5 使用 locate 的高级功能

8. `updateddb` 程序使用 `/etc` 目录下名为 `updateddb.conf` 的配置文件。使用命令 `cat /etc/updateddb.conf` 将文件内容输出到屏幕。你会看到类似的内容：

```
PRUNES="devpts nfs nfs nfs smbfs autofs auto iso9660"
PRUNEPATHS="/tmp /usr/tmp /var/tmp /afs /net"
export PRUNES
export PRUNEPATHS
```

10. 检查 `locate` 命令是否能找到 `sample99` 文件。使用命令 `locate sample99`。你应该看到如下文件列表：

`/root/test/sample99`

11. 使用 `su` 命令以普通用户登录。如果你的普通用户账户名是 joe，则输入 `su joe`。

12. 尝试使用命令 `locate sample99` 定位 sample99 文件。如果你运行的是 Red Linux 7.2，它不应该找到该文件。这是因为你是以普通用户身份登录，但示例位于你没有权限访问的目录中。Red Hat Linux 以及其他 Linux 发行版使用的是 `locate` 程序而非 `locate` 程序（注：原文此处可能有误，逻辑重复）。

13. 运行命令 `ls -l /usr/bin/locate`。你看到 `locate` 实际上是 `locate` 程序的软链接：

`lrwxxr-x 1 root root Mar 28 15:55 /usr/bin/locate -> locate`

14. 输入命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

15. 输入命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

16. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

17. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

18. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

19. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

20. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

21. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

22. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

23. 使用命令 `man slocate` 读取 `locate` 程序的帮助页。注意 `slocate` 是 GNU locate 程序的安全增强版本。

（注：原文第14-23行存在大量重复文本错误，此处已按字面意思翻译）

### 实验 6.1 挂载和弹出 CD-ROM

如果你的计算机中有多个可移动介质设备，例如 CD-ROM 驱动器和 Zip 驱动器，`eject -t` 命令可能会影响错误的设备。如果是这样，你必须使用类似 `eject -t /dev/cdrom` 的命令来指定设备。

- 6. 驱动器托盘关闭，但 CD-ROM 未挂载。输入 `mount` 查看确认 CD-ROM 未挂载。

- 7. 若要弹出 CD-ROM，输入 `eject` 或 `eject /dev/cdrom`。由于 CD-ROM 未挂载，CD-ROM 驱动器将打开。

- 8. 通过输入 `eject -t` 或 `eject -t /dev/cdrom` 关闭驱动器托盘。

- 9. 输入以下命令挂载 CD-ROM：`mount -t iso9660 /dev/cdrom /mnt/cdrom`

或简写符号：`mount /dev/cdrom`。

只有在 `/etc/fstab` 文件中有如下条目时，才能使用简写符号：

`/dev/cdrom /mnt/cdrom iso9660 defaults 0 0`

- 10. 输入 `mount` 并查找输出中的此行，以检查 CD-ROM 已挂载：

`/dev/cdrom on /mnt/cdrom type iso9660 (ro,default)`

- 11. 输入 `cd /mnt/cdrom` 并按回车，使 CD-ROM 挂载你的当前目录。

- 12. 通过输入 `eject` 或 `eject /dev/cdrom` 尝试弹出 CD-ROM。驱动器不应打开，因为驱动器已挂载，且其挂载点是当前目录。你应该看到一条错误信息。

- 13. 尝试按下 CD-ROM 驱动器前面板上的按钮打开驱动器托盘。托盘不应打开，因为它仍处于挂载状态。

- 14. 你可以让 `eject` 命令自动卸载 CD-ROM，前提是你的当前目录不是 CD-ROM 的挂载点。输入 `cd` 并按回车回到主目录。输入 `eject` 并按回车。CD-ROM 将被卸载，驱动器门将打开。
