

## 项目 5-2

在这个动手项目中，你将在软盘上创建一个文件系统，并练习将其挂载到目录树上。

- 1. 通过按**Ctrl+Alt+F2**切换到命令行终端（tty2）。使用用户名**root**和密码LNXrocks!登录到终端。在命令提示符下，键入**poweroff**并按**Enter**键关闭你的虚拟机。在你的虚拟化软件中，创建一个新的虚拟软盘并将其附加到你的虚拟机。接下来，启动你的虚拟机。Linux系统加载完成后，通过按**Ctrl+Alt+F2**切换到命令行终端（tty2）。使用用户名**root**和密码LNXrocks!登录到终端。在命令提示符下，键入**fdformat /dev/fd0**并按**Enter**。这将格式化你的新虚拟软盘。在命令提示符下，键入**mformat -i /dev/fd0 floppy**并按**Enter**，以在软盘上创建一个新的FAT文件系统。`floppy`参数是新文件系统的名称。
- 2. Linux系统加载完成后，通过按**Ctrl+Alt+F2**切换到命令行终端（tty2）。使用用户名**root**和密码LNXrocks!登录到终端。在命令提示符下，键入**poweroff**并按**Enter**以关闭你的虚拟机。
- 3. 在你的虚拟化软件中，创建一个新的虚拟软盘并将其附加到你的虚拟机。接下来，启动你的虚拟机。Linux系统加载完成后，通过按**Ctrl+Alt+F2**切换到命令行终端（tty2）。使用用户名**root**和密码LNXrocks!登录到终端。
- 4. 在命令提示符下，键入**fdformat /dev/fd0**并按**Enter**。这将格式化你的新虚拟软盘。在命令提示符下，键入**mformat -i /dev/fd0 floppy**并按**Enter**，以在软盘上创建一个新的FAT文件系统。`floppy`参数是新文件系统的名称。
- 5. 在命令提示符下，键入**mount -t vfat /dev/fd0 /mnt**并按**Enter**，将新文件系统挂载到/mnt目录。在命令提示符下，键入**ls /mnt**并按**Enter**。你看到了哪些文件？为什么？接下来，键入**cd /mnt**并按**Enter**。键入**mkdir newdir**并按**Enter**以创建一个新目录。在命令提示符下，键入**ls /mnt**并按**Enter**。你现在看到了哪些文件？为什么？
- 6. 在命令提示符下，键入**mkdir /mnt/newdir1**并按**Enter**以创建一个新目录。接下来，键入**touch /mnt/newdir1/file1**并按**Enter**以创建一个新文件。在命令提示符下，键入**ls -a /mnt/newdir1**并按**Enter**。你看到了哪些文件？为什么？
- 7. 在命令提示符下，键入**umount /mnt**并按**Enter**以卸载文件系统。接下来，键入**ls /mnt**并按**Enter**。你现在看到了哪些文件？为什么？
- 8. 在命令提示符下，键入**fdformat /dev/fd0**并按**Enter**。这将再次格式化你的新虚拟软盘。在命令提示符下，键入**mformat -i /dev/fd0 floppy**并按**Enter**，以在软盘上创建一个新的FAT文件系统。`floppy`参数是新文件系统的名称。
- 9. 在命令提示符下，键入**mount -t vfat /dev/fd0 /mnt**并按**Enter**，将新文件系统挂载到/mnt目录。在命令提示符下，键入**ls /mnt**并按**Enter**。你看到了哪些文件？为什么？接下来，键入**cd /mnt**并按**Enter**。键入**mkdir newdir2**并按**Enter**以创建一个新目录。在命令提示符下，键入**ls /mnt**并按**Enter**。你现在看到了哪些文件？为什么？
- 10. 在命令提示符下，键入**mkdir /mnt/newdir2/next**并按**Enter**以创建一个新的子目录。接下来，键入**touch /mnt/newdir2/next/file2**并按**Enter**以创建一个新文件。在命令提示符下，键入**ls -a /mnt/newdir2/next**并按**Enter**。你看到了哪些文件？为什么？
- 11. 在命令提示符下，键入**cd /mnt/newdir2/next**并按**Enter**。在命令提示符下，键入**ls**并按**Enter**。你看到了哪些文件？为什么？接下来，键入**cat file2**并按**Enter**。屏幕上显示了什么？为什么？
- 12. 在命令提示符下，键入**cd /mnt**并按**Enter**。在命令提示符下，键入**ls**并按**Enter**。你看到了哪些文件？为什么？接下来，键入**ls -l**并按**Enter**。屏幕上额外显示了什么信息？为什么？
- 13. 在命令提示符下，键入**du -sh**并按**Enter**。屏幕上显示了什么？为什么？接下来，键入**du -sh /mnt**并按**Enter**。屏幕上显示了什么？为什么？
- 14. 在命令提示符下，键入**df -h**并按**Enter**。屏幕上显示了什么？为什么？接下来，键入**df -h /mnt**并按**Enter**。屏幕上显示了什么？为什么？
- 15. 在命令提示符下，键入**umount /mnt**并按**Enter**以卸载文件系统。接下来，键入**ls /mnt**并按**Enter**。你现在看到了哪些文件？为什么？
- 16. 在命令提示符下，键入**fdformat /dev/fd0**并按**Enter**。这将最后一次格式化你的新虚拟软盘。在命令提示符下，键入**mformat -i /dev/fd0 floppy**并按**Enter**，以在软盘上创建一个新的FAT文件系统。`floppy`参数是新文件系统的名称。
- 17. 在命令提示符下，键入**mount -t vfat /dev/fd0 /mnt**并按**Enter**，将新文件系统挂载到/mnt目录。在命令提示符下，键入**ls /mnt**并按**Enter**。你看到了哪些文件？为什么？
- 18. 在命令提示符下，键入**umount /mnt**并按**Enter**以卸载文件系统。接下来，键入**ls /mnt**并按**Enter**。你现在看到了哪些文件？为什么？
- 19. 在命令提示符下，键入**poweroff**并按**Enter**以关闭你的虚拟机。虚拟机关闭后，断开你的新虚拟软盘并将其从虚拟机中移除。

## 项目 5-3

在这个动手项目中，你将DVD挂载到目录树上并查看其内容。

- 1. 通过按**Ctrl+Alt+F1**切换到图形终端（tty1），并使用用户名*user1*和密码*LNXrocks!*登录到GNOME桌面。
- 2. 点击**Activities**菜单并选择**Files**图标以打开文件应用。
- 3. 在你的虚拟化软件中，将Fedora Linux的DVD ISO映像（Fedora-Live-Desktop-x86_64-20-1.iso）附加到虚拟机的DVD驱动器。完成此操作后，查看你的文件应用。左侧窗格中是否有代表你的Fedora Live Desktop DVD的图标？将鼠标悬停在此图标上以查看挂载点目录。你的DVD被自动挂载到了哪个目录？
- 4. 花一点时间在文件应用中探索DVD的内容。完成后，点击Fedora Live Desktop DVD图标旁边的弹出按钮以弹出DVD。
- 5. 通过按**Ctrl+Alt+F2**切换到命令行终端（tty2），并使用用户名*root*和密码*LNXrocks!*登录到GNOME桌面。（注：此处原文可能有误，通常命令行终端登录不涉及GNOME桌面图形界面，但译文需忠实于原文逻辑，原文表述为log in to the GNOME desktop，可能是指登录系统后处于GNOME环境下或原文笔误，此处按直译处理，或者理解为登录终端用户root）
- 6. 在你的虚拟化软件中，将Fedora Linux的DVD ISO映像（Fedora-Live-Desktop-x86_64-20-1.iso）附加到虚拟机的DVD驱动器。完成此操作后，键入`mount`并按`Enter`。DVD是否被自动挂载？
- 7. 接下来，在命令提示符下键入`mount /dev/cdrom /mymount`并按`Enter`。你收到了什么警告？DVD是否成功挂载到了/mymount目录？
- 8. 在命令提示符下，键入`ls -F /mymount`并按`Enter`。你看到的文件是否与步骤4中的一致？为什么？
- 9. 在命令提示符下，键入`ls -l /dev/cdrom`并按`Enter`。/dev/cdrom符号链接指向哪个目标文件？
- 10. 在命令提示符下，键入`mount`并按`Enter`。注意底部列出了你已挂载的DVD的行。之前挂载DVD时自动检测到的文件系统是什么？设备文件是否与步骤9中显示的目标文件相同？
- 11. 接下来，在命令提示符下键入`umount /mymount`并按`Enter`。DVD是否成功从/mymount目录卸载？在命令提示符下键入`mount`命令并按`Enter`以验证这一点。
- 12. 在你的虚拟化软件中，将Fedora Linux的DVD ISO映像（Fedora-Live-Desktop-x86_64-20-1.iso）从虚拟机的DVD驱动器中移除。（原文为detach... to...，逻辑上应为detach... from...，译文按“移除/断开”处理）此操作等同于从物理DVD驱动器中弹出DVD。
- 13. 键入`exit`并按`Enter`以注销你的shell。

![](img/c27875544958897d817484d558c208c8_276_0.png)

## 项目 5-4

在这个动手项目中，你将处理标准硬盘分区。首先，你将使用fdisk工具创建硬盘分区。接下来，你在分区上创建ext4文件系统并将其挂载到目录树上。最后，你使用/etc/fstab文件在启动时自动挂载该分区。

- 1. 通过按**Ctrl+Alt+F2**切换到命令行终端（tty2），并使用用户名*root*和密码*LNXrocks!*登录到终端。

