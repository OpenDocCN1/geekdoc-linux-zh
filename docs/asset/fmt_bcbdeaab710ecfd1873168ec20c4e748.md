
然而，仅在此设置上下文是不够的，因为你只将其写入了策略，而不是文件系统。要完成该命令，你现在需要将策略设置应用到文件系统，如下所示：

```
restorecon -R /mydir
```

你会看到新上下文已被应用，允许 `httpd` 进程访问该目录。

提示：`semanage` 命令并不是最容易记忆的命令。幸运的是，它有非常优秀的手册页（man pages）。输入 `man semanage` 并使用 `G` 跳到手册页的最底部。你会看到“参见”（see also）部分，其中提到了 `semanage-context`。使用 `man semanage-context, type /examples` 打开该手册页，你将看到包含了你所需要知识的很好的示例（参见列表 21.4）。

# 列表 21.4 手页中的 semanage 使用示例

```
示例
在设置文件上下文后记得运行 restore
为 /web 下的所有内容添加文件上下文
# semanage fcontext -a -t httpd_sys_content_t "/web/(.*)\*"
# restorecon -R /web

在设置文件上下文时将 /home/homel 替换为 /home
# semanage fcontext -a -e /home/homel
# restorecon -R -v /homel
```

对于顶层目录下的家目录，例如 `/ndisk6/home`，执行以下命令：

```
# semanage fcontext -a - t home_root_t "/disk6"
# semanage fcontext -a -e /disk6/home
# restorecon -R -v /disk6

# 参见
selinux (8), semanage (8)

# 作者
此手册页由 Daniel Walsh <dwalsh@redhat.com> 编写
20130617
semanage-fcontext (8)
```

现在是进行练习了。在练习 21.2 中，你将学习如何更改 Apache Web 服务器的文档根并正确地标记新的文档根。

# 练习 21.2 在 Web 服务器上设置上下文标签

- 创建新目录 `/var/www/test/`

- 在 `/var/www/test/` 中创建一个名为 `index.html` 的新 HTML 文件

- 创建子目录 `/var/www/test/images/`

- 将 `/var/www/test/` 目录的上下文设置为 `httpd_sys_content_t`

- 将 `/var/www/test/images/` 目录的上下文设置为 `httpd_sys_content_t`

- 使用 `ls -Z` 验证上下文

也可以对整个文件系统进行重新标记。这样做会将策略中定义的所有上下文应用到文件系统。由于策略始终应该是领先的，并包含上下文设置，因此重新标记文件系统可能是一个好主意。要重新标记文件系统，你可以使用 `restorecon -Rv` 命令，或者创建一个名为 `.autorelabel` 的文件。当你的服务器下次重启时，文件系统将会被重新标记。

重新标记操作有时会自发生。当你对服务器进行故障排除时，如果你在禁用 SELinux 的模式下启动了服务器并对文件系统进行了修改，SELinux 将检测到文件系统在没有 SELinux 监控的情况下发生了变化。这将导致文件系统的自动重新标记。请注意，在大型文件系统上重新标记可能花费大量时间。图 21.1 显示了当系统被自动重新标记时你应该看到的内容。

```
[ OK ] Started create device nodes in /dev.
[ OK ] Starting kernel Device Manager.
[ OK ] systemd-fsck[41]: /sbin/fsck.xfs file system.
[ OK ] Started Configured read-only root mount
[ OK ] Imported network configuration from initramfs.
[ OK ] Starting kernel Device Manager.
[ OK ] Started udev Wait For Generic Initialization.
[ OK ] Started Activation of RAID md.
[ OK ] Started LVM scan on device 0:2.
[ OK ] Started LVM scan on device 0:4.
[ OK ] Started Ubuntu Volume_1.
[ OK ] Starting File System Check on /dev/disk/by-uuid/a1d9b0c4-a274-4af7-b8d4-f7f8bcda03c...
[ OK ] Mounted Target Volumes.
[ OK ] Starting Activation of RAID md.
[ OK ] Started Monitoring of lvm-snapshots using dwdent and progress logging.
[ OK ] systemd-fsck[711]: /sbin/fsck.xfs file system.
[ OK ] Started File System Check on /dev/disk/by-uuid/a1d9b0c4-a274-4af7-b8d4-f7f8bcda03c...
[ OK ] Mounted /boot.
[ OK ] Found /dev/mapper/centos-swap.
[ OK ] Activated /dev/mapper/centos-swap.
[ OK ] Mounted Target Swap.
[ OK ] Started Activation of RAID md.
[ OK ] Started LVM scan on device 0:2.
[ OK ] Started LVM scan on device 0:4.
[ OK ] Found /dev/mapper/vg0/groups.
[ OK ] Started File System Check on /dev/mapper/vg0/groups.
[ OK ] Mounted /vg0.
[ OK ] Mounted /.
[ OK ] Reached target.
[ OK ] Starting Create Variable Files and Directories...
[ OK ] Triggered Flushing of Journal to Persistent Storage.
[ OK ] Starting Security Audit Service.
[ OK ] Started Tell Epoch To Write Runtime Data.
[ OK ] Triggered Flushing of Journal to Persistent Storage.
[ OK ] Started Tell Epoch To Write Runtime Data.
--- Warning -- SELinux targeted policy relabel is required.
--- This could take a very long time, depending on file
--- system size and speed of hard drives.
[ OK ] Reached Target Soft Drive.
```

图 21.1 重新标记文件系统。

## 练习 21.4 使用 restorecon 重新标记文件

- 1. 在 root shell 中，输入 `ls -Z /etc/hosts`。你会看到该文件具有 `net_config_t` 上文标签。

- 2. 使用 `cp /etc/hosts ~` 将文件复制到家目录。由于复制被视为创建了新文件，`~hosts` 文件的上下文设置被设置为 `admin_home_t`。使用 `ls -Z ~hosts` 验证此项。

- 3. 使用 `mv ~hosts /etc` 并确认要覆盖现有文件。

- 4. 输入 `ls -Z /etc/hosts` 确认上下文类型仍设置为 `admin_home_t`。

- 5. 使用 `restorecon -v /etc/hosts` 重新应用正确的上下文类型。`-v` 选项显示正在发生什么。

- 6. 输入 `touch /.autorelabel` 并重启你的服务器。重启时，确保按下键盘上的 Escape 键，这样你就能看到启动信息。你会看到文件系统被自动重新标记了。

# 使用布尔值修改 SELinux 设置

在 SELinux 策略中，有许多规则。其中某些规则允许特定活动，而另一些规则则拒绝该活动。更改规则并不容易，这就是为什么提供了 SELinux 布尔值（Booleans），以便方便地更改规则的行为。
