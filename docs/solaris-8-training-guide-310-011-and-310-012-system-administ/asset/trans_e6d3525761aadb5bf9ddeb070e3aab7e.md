
## 应用你的知识

4. 以下哪个命令用于在未挂载的磁盘文件系统上写入或显示标签？
+   - A. format
- B. prtvtoc
- C. newfs
- D. labelit

5. 管理员（root）使用以下哪个命令将带标签的文件系统从一个磁盘复制到另一个磁盘？
+   - A. volcopy
- B. ufsdump
- C. tar
- D. 以上全部

6. 以下哪个命令用于确定文件系统是否为 UFS 文件系统？
+   - A. fstyp
- B. prtvtoc
- C. format
- D. newfs -v

7. 以下哪个命令用于更改文件系统的 minfree 值？
+   - A. mkfs
- B. tunefs
- C. newfs
- D. format

8. 以下哪个命令用于查看文件系统参数的完整列表？
+   - A. fstyp
- B. mkfs
- C. newfs
- D. prtvtoc

9. 大文件是指大小大于或等于以下哪个值的普通文件：
+   - A. 100MB
- B. 1GB
- C. 5GB
- D. 2GB

10. 以下哪个不是大文件感知的？
+   - A. labelit
- B. vi
- C. mkfs
- D. mount

11. 以下哪种类型的实用程序能够处理大文件作为输入并生成大文件作为输出？
+   - A. 大文件兼容
- B. 大文件安全
- C. 大文件感知
- D. 大文件功能

## 应用你的知识

12. mount 命令的以下哪个选项提供与之前文件系统行为的完全兼容性，强制执行 2GB 的最大文件大小限制？
A. -o compat
B. -largefiles
C. -nolargefiles
D. -o large

13. 以下哪个选项与 mount 命令一起使用以以 /etc/vfstab 格式显示已挂载文件系统的列表？
A. -p
B. -v
C. -f
D. -a

14. 以下哪个示例使用 mount 命令将目录映射为可读写的文件系统，禁止 setuid 执行，并启用大文件的创建：
A. mount -o rw,nosuid,large
   /dev/dsk/c0t0d0s0 /home2
B. mount -o rw,nosuid,largefiles
   /dev/dsk/c0t0d0s0 /home2
C. mount -o rw,nosuid,largefiles
   /dev/rdsk/c0t0d0s0 /home2
D. mount -o rw,suid,largefiles
   /dev/dsk/c0t0d0s0 /home2

15. 当文件系统被挂载时，条目维护在哪里？
A. /etc/mnttab
B. /etc/vfstab
C. /etc/fstab
D. /mnt

16. 以下哪些任务可以在已挂载的文件系统上执行？
A. labelit
B. fsck
C. tunefs
D. shutdown

17. 如果有东西导致文件系统繁忙，以下哪个命令可用于列出访问文件系统的所有进程？
A. fuser
B. mount
C. ps
D. finger

18. 以下哪个命令会停止所有使用 /home2 文件系统的进程？
A. fuser -c -k /home2
B. fuser -k /home2
C. kill -9 /home2
D. umount /home2

## 应用你的知识

19. 以下哪个是管理可移动媒体（如 CD-ROM 和软盘驱动器）的机制？
A. autofs
B. NFS
C. vold
D. init

20. vold 执行以下所有操作，除了什么？
A. 为网络上的其他系统提供对用户插入系统中的任何磁盘和 CD 的自动访问
B. 自动挂载磁盘和 CD
C. 使用户能够在无需以 root 登录的情况下访问磁盘和 CD
D. 当访问该文件系统时自动挂载位于另一系统上的文件系统

21. 以下哪个目录为主要软盘驱动器中的媒体提供字符设备访问？
A. /vol/dev/diskette0
B. /dev/rdiskette
C. /vol/dev/aliases/floppy0
D. /floppy/floppy0

22. 以下哪个包含 vold 使用的卷管理配置信息？
A. /etc/init.d/volmgt
B. /etc/vfstab
C. /etc/vold.conf
D. /etc/inittab

23. 系统管理员可以修改以下哪个文件来指定如果发生媒体事件（如弹出或插入）应调用哪个程序？
A. /etc/vold.conf
B. /etc/rmmount.conf
C. /etc/inittab
D. /etc/mnttab

24. 如果尝试访问已不在驱动器中的 CD 或磁盘，以下哪个操作会通知用户？
A. vold
B. volcheck
C. volmissing
D. rmmount

25. 以下哪个命令用于格式化软盘并添加卷标？
A. format -d
B. labelit
C. format
D. fdformat

26. 以下哪个命令用于停止卷管理守护进程？
A. vold stop
B. /etc/init.d/volmgt stop
C. ps -ef|grep vold, then kill the process ID for vold
D. volcancel

## 应用你的知识

27. 以下哪个命令显示每个已挂载文件系统的容量信息？
A. du
B. format
C. prtvtoc
D. df

28. 以下哪个命令用于使系统自动挂载软盘？
A. volcheck
B. vold
C. mount
D. automount

29. 如果存在以下哪个条件，您可以在命令行键入 mount /opt 而不会收到错误消息？
A. /opt 列在 /etc/rmtab 中。
B. /opt 列在 /etc/mnttab 中。
C. /opt 列在 /etc/vfstab 中。
D. /opt 列在 /etc/dfs/dfstab 中。

30. 卷管理器通过以下哪个目录提供对 CD-ROM 和软盘设备的访问？
A. /vol/dev
B. /dev/vol
C. /dev
D. /vold

31. 以下关于卷管理器的说法哪个是不正确的？
A. 卷管理器通过 /etc/init.d/volmgt 脚本启动。
B. 卷管理器自动挂载 CD 和软盘。
C. 卷管理器在启动时读取 /etc/vold.conf 配置文件。
D. 卷管理器在启动时自动挂载文件系统。

## 复习问题的答案

1. A. 通常，创建大量小文件会导致高度碎片化。解决方案是创建更大的文件系统或减小块大小（更细的粒度）。

2. B. df 命令不显示碎片化的百分比。

3. D. newfs 是 mkfs 命令的友好前端。newfs 命令会自动确定传递给 mkfs 以构建新文件系统所需的所有参数。newfs 在 Solaris 中添加是为了使创建新文件系统更容易。强烈建议使用 newfs 命令创建文件系统。

4. D. 使用 newfs 创建文件系统后，您可以使用 labelit 实用程序在未挂载的磁盘文件系统上写入或显示标签。

## 应用你的知识

5. D. 使用 volcopy、ufsdump、cpio、pax 或 tar 将带标签的文件系统从一个磁盘复制到另一个磁盘。

6. A. 使用 fstyp 命令确定文件系统类型。例如，使用它来检查文件系统是否为 ufs 文件系统。

7. B. 使用 tunefs 命令更改文件系统的 min-free 值。

8. A. 使用 fstyp 命令查看文件系统参数。使用 -v 选项获取文件系统参数的完整列表。

9. D. 大文件是指大小大于或等于 2GB 的普通文件。

10. B. 如果实用程序能够以处理小文件相同的方式处理大文件，则称为大文件感知。大文件感知实用程序可以处理大文件作为输入，并可以生成大文件作为输出。vi 命令不是大文件感知的。

11. C. 如前一问题和答案所述，如果实用程序能够以处理小文件相同的方式处理大文件，则称为大文件感知。大文件感知实用程序可以处理大文件作为输入并可以生成大文件作为输出。

12. C. mount 命令的 -nolargefiles 选项提供与之前文件系统行为的完全兼容性，强制执行 2GB 的最大文件大小限制。

13. A. 使用 -p 选项键入 mount 命令以以 /etc/vfstab 格式显示已挂载文件系统的列表。

14. B. 以下命令：
```
mount -o rw,nosuid,largefiles \
/dev/dsk/c0t0d0s0 /home2
```
使用 mount 命令将目录映射为可读写的文件系统，禁止 setuid 执行，并启用创建大于 2GB 的大文件。

15. A. 当文件系统被挂载时，会在名为 /etc/mnttab 的已挂载文件系统表中维护一个条目。该文件实际上是一个只读文件系统，其中包含当前已挂载设备的有关信息。

16. D. 不要在已挂载的文件系统上执行以下命令：fsck、tunefs 和 labelit。

17. A. 如果有东西导致文件系统繁忙，您可以使用 fuser 命令列出访问文件系统的所有进程，并在必要时停止它们。

18. A. 以下命令通过向每个进程发送 SIGKILL 来停止所有使用 /home2 文件系统的进程：fuser -c -k /home2

19. C. vold 守护进程是管理可移动媒体（如 CD-ROM 和软盘驱动器）的机制。

20. D. vold 不会在访问该文件系统时自动挂载位于另一系统上的文件系统。负责该任务的设施是 AutoFS。

21. B. /dev/rdiskette 和 /vol/dev/rdiskette0 是为主要软盘驱动器中的介质提供字符设备访问的目录，通常为驱动器 0。

22. C. vold 在启动时读取 /etc/vold.conf 配置文件。vold.conf 文件包含 vold 使用的卷管理器配置信息。
