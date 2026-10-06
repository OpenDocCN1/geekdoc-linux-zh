
21. 保存更改并退出编辑器。

# 第 5 章 Linux 文件系统管理

22. 在命令提示符处，输入 `reboot` 并按回车。在 Linux 加载后，通过 `Ctrl+Alt+F5` 切换到命令行终端（tty5），并使用用户名 `root` 和密码 `LINUXroots` 登录终端。

23. 在命令提示符处，输入 `df -hT` 并按回车，验证你的 LV 是否在启动时已自动挂载。

24. 输入 `exit` 并按回车退出 Shell。

# 项目 5-5

预计耗时：20 分钟
目标：排查文件系统故障。

描述：在本次实践项目中，你将使用磁盘使用情况和 `Ctrl+F5` 检查错误。

- 1. 通过 `Ctrl+Alt+F5` 切换到命令行终端（tty5），并使用用户名 `root` 和密码 `LINUXrocks!` 登录终端。
- 2. 在命令提示符处，输入 `df -h` 并按回车。显示了哪些非虚拟文件系统？
- 3. 在命令提示符处，输入 `df -i` 并按回车。注意文件系统可用的 inode（节点）数量。
- 4. 在命令提示符处，输入 `fsck /dev/vg00/newdata` 并按回车。你收到了什么错误？为什么？
- 5. 在命令提示符处，输入 `umount /dev/vg00/newdata` 并按回车。接下来，输入 `fsck /dev/vg00/newdata` 并按回车。检查了多久时间？
- 6. 在命令提示符处，输入 `fsck -f /dev/vg00/newdata` 并按回车。检查了多久时间？
- 7. 在命令提示符处，输入 `e2fsck -c /dev/vg00/newdata` 并按回车。该命令的作用是什么？
- 8. 在命令提示符处，输入 `tune2fs -i 0 /dev/vg00/newdata` 并按回车。对于 ext4 文件系统这样做好吗？
- 9. 在命令提示符处，输入 `mount /dev/vg00/newdata` 并按回车。即使你没有指定类型，挂载是如何完成的？
- 10. 输入 `exit` 并按回车退出 Shell。

# 项目 5-6

预计耗时：20 分钟
目标：配置磁盘配额。

描述：在本次实践项目中，你将启用并查看 `/newata` 的磁盘配额。

- 1. 通过 `Ctrl+Alt+F5` 切换到命令行终端（tty5），并使用用户名 `root` 和密码 `LINUXrocks!` 登录终端。
- 2. 在命令提示符处，输入 `chmod 777 /newata` 赋予 `/newata` 创建文件的权限。
- 3. 通过 `Ctrl+Alt+F6` 切换到 tty6，使用用户名 `user1` 和密码 `LINUXrocks!` 登录终端。
- 4. 在命令提示符处，输入 `touch /newata/samplefile` 并按回车，创建一个由该用户拥有的的文件。
- 5. 输入 `exit` 并按回车退出 Shell。
- 6. 通过 `Ctrl+Alt+F5` 回到 tty5，注意你是以 root 用户身份登录的。
- 7. 在命令提示符处，输入 `vi /etc/fstab` 并按回车。查看挂载点的选项。将 `/newata` 修改为（其中 `device` 为设备文件）：

```
device /newata ext4 defaults,usrquota,grpquota 0 0
```

- 8. 保存更改并退出编辑器。
- 9. 输入 `mount -o remount,rw /newata` 并按回车将其重新挂载为读写。
- 10. 在命令提示符处，输入 `getquota -u user` 并按回车。输出是什么？接下来，在 `/newata` 创建大文件以填充配额。再次输入 `getquota -u user`。现在的输出是什么？
- 11. 输入 `exit` 并按回车退出 Shell。

# 项目 5-7

预计耗时：20 分钟
目标：创建和管理 XFS 文件系统。

描述：在本次实践项目中，你将使用 `cfdisk` 工具创建一个分区，并检查该分区上的 XFS 文件系统以及启动时带有 GUID 的文件系统。

- 1. 通过 `Ctrl+Alt+F5` 切换到命令行终端（tty5），并使用用户名 `root` 和密码 `LINUXroots` 登录终端。
- 2. 在命令提示符处，输入 `cfdisk device` 并按回车，其中 `device` 是项目 3 第 2 步中的块设备（例如 `/dev/sda`）。使用 `cfdisk` 工具选择 `New`。指定分区大小为 2G 并按回车。记新分区的设备文件。
- 3. 选择 `Write` 保存更改；在提示确认时按 `y` 并按回车。接下来，选择 `Quit` 保存更改并退出 cfdisk。
- 4. 在命令提示符处，输入 `partprobe` 并按回车。

## 第 5 章 Linux 系统管理

5. 在命令提示符下输入 `mkfs -t xfs device` 并按回车，其中 `device` 是你在第 2 步中创建的分区设备文件。接下来，输入 `mkdir /xfsmount` 并按回车为文件系统创建一个挂载点。随后，输入 `mount device /xfsmount` 并按回车，其中 `device` 是第 2 步创建的分区的设备文件。

6. 在命令提示符下输入 `df -hT` 并按回车，验证你的 XFS 文件系统是否成功挂载。接下来，输入 `ls /xfsmount` 并按回车。为什么没有 lost+found 目录？

7. 在命令提示符下输入 `umount /xfsmount` 并按回车。接下来，输入 `fsck -f device` 并按回车，其中 `device` 是第 2 步创建的分区的设备文件。为什么你收到了错误？然后，输入 `xfs repair device` 并按回车，其中 `device` 是第 2 步创建的分区的设备文件。

8. 在命令提示符下输入 `blkid` 并按回车。你的 XFS 文件系统的 UUID 为：

9. 在命令提示符下输入 `vi /etc/fstab` 并按回车。在文件末尾添加以下行，其中 `UUID` 是你在上一步中记录的 UUID：

```
UUID="filesystemUUID" /xfsmount xfs defaults 0 0
```
