
`fdisk /dev/sda`

```
显示一条消息，指示磁道数大于1024，在某些情况下可能会导致问题。
```

2. 输入 `p` 查看当前分区表。

3. 通过以下操作创建一个使用整个磁盘空闲空间的扩展分区：

   a. 输入 `n` 创建新分区。
   b. 输入 `e` 表示扩展分区。
   c. 条件：：当被询问分区号时，输入 `3`。
   d. 按回车接受建议的第一个磁道。
   e. 按回车接受建议的最后一个磁道。

4. 通过以下操作创建两个分区类型为 Linux（默认）的逻辑分区：

   a. 输入 `n` 创建新分区。
   b. 输入 `1` (小写 L) 创建逻辑分区。
   c. 按回车接受第一个磁道。
   d. 输入 `+1G` 指定分区大小为 1 GB。
   e. 输入 `n` 创建另一个新分区。
   f. 输入 `1` (小写 L) 创建逻辑分区。
   g. 按回车接受第一个磁道。
   h. 输入 `+1G` 指定分区大小。
   i. 输入 `p` 验证新分区的配置。

5. 输入 `w` 将新分区表写入硬盘并退出 `fdisk`。

你将看到一条警告消息，内核内核仍在使用旧分区表，新表将在下次重启时使用。

6. 输入以下命令查看内核使用的当前分区表：

```
cat /proc/partitions
```

注意你刚刚创建的三个新分区并未列出。

7. 要访问新分区，你必须更新存储在内存中的内核分区表。执行以下操作之一：

   - 输入 `partprobe` 让内核更新其分区表。
   - 输入 `reboot` 重启系统。

8. 输入以下命令再次查看分区表：

```
cat /proc/partitions
```

## 第二部分：从命令行管理文件系统

要从命令行管理文件系统，请执行以下操作：

1. 在 root 身份登录的终端中，执行以下操作：
   a. 在 `/dev/sda5` 上通过以下命令创建 ext3 文件系统：
```
mkfs.ext3 -v /dev/sda5
```
   b. 在 `/dev/sda6` 上通过以下命令创建 ext2 文件系统：
```
mkfs.ext2 -v /dev/sda6
```

2. 输入以下命令创建挂载点 `/export/data1` 和 `/export/data2`：
```
mkdir -p /export/data1 /export/data2
```

3. 编辑 `/etc/fstab` 文件以自动挂载创建的分区：
```
vi /etc/fstab
```
确保以下行存在：
```
/dev/sda5 /export/data1 ext3 defaults 0 0
/dev/sda6 /export/data2 ext2 defaults 0 0
```

4. 输入以下命令挂载分区：
```
mount -a
```

5. 输入以下命令验证挂载情况：
```
df -h
```

## 第三部分：运行 fsck

对挂载在 `/export/data1` 的 `/dev/sda5` ext3 文件系统运行 `fsck`：

1. 卸载分区：
```
umount /export/data1
```

2. 对分区运行 `fsck`：
```
fsck /dev/sda5
```

3. 重新挂载分区并验证：
```
mount /export/data1
df -h
```

## 第四部分：自定义文件系统

在练习的这一部分中，你将通过添加日志将 `/dev/sda6` 分区转换为 ext3 文件系统。你还为它添加了标签。

1. 卸载分区：
```
umount /export/data2
```

2. 通过添加日志将分区转换为 ext3：
```
ext2fs /dev/sda6
```

3. 为分区添加标签：
```
tune2fs -L data_label /dev/sda6
```

4. 重新挂载分区并验证标签：
```
mount /export/data2
lsblk /dev/sda6
```

## 第五部分：设置和配置磁盘配额

在练习的第五部分中，你将管理用户配额。你安装 `quota` 软件包并为挂载在 `/export/data2` 的 `/dev/sda6` 配置配额。

1. 安装软件包包：
```
yum install quota
```

2. 通过编辑 `/etc/fstab` 启用配额支持：
```
vi /etc/fstab
```
在 `/dev/sda6` 的条目中添加 `usrquota`。

3. 重新挂载文件系统并初始化配额：
```
mount -a
quotacheck -cum
quota
```

4. 为特定用户设置配额：
```
edquota -u [username] /export/data2
```

5. 验证配额：
```
repquota -a /export/data2
```

# 第五部分：设置和配置磁盘配额

完成以下操作：

- 1. 打开终端窗口，使用 `su -` 命令和 root 密码切换到 root 用户。
- 2. 输入 `yast -i quota` 安装配额包。
- 3. （条件条件）如果提示，请插入 *SUSE Linux Enterprise Server 11* 安装光盘。
- 4. 输入 `quota -vu geeko` 查看用户 `geeko` 的磁盘配额配置。

没有任何输出表示当前没有为 `geeko` 配置任何配额。

- 5. 通过执行以下步骤为 `/dev/sda6` 分区添加配额选项：
    a. 输入 `vi /etc/fstab` 在编辑器中打开 `/etc/fstab` 文件。
    b. 修改 `/etc/fstab` 中的 `/dev/sda6` 条目，使其看起来如下（一行）：

```
/dev/sda6 /export/data2 ext3
defaults,usquota,grpquota 1 2
```

- 6. 保存文件并退出 `vi`。
- 7. 输入 `mount -o remount /dev/sda6` 重新挂载文件系统，使系统读取 `/etc/fstab` 文件中的更改。

> 注意：如果收到错误消息 "/export/data2 mounted already, or bad option”，请检查 `/etc/fstab`文件的内容。你可能拼错了 `usquota` 或 `grpquota` 选项。

- 8. 输入 `quotacheck -mavug` 初始化配额数据库。

> 注意：你将收到几条关于旧配额文件的状态消息。这些表示这是一个新的配额数据库，系统上没有之前的配额文件。

- 9. 输入 `ls -l /export/data2` 验证 `/export/data2` 目录下是否存在 `aquota.user` 和 `aquota.groups` 文件。
- 10. 输入 `quotaon -av` 为所有挂载了这些选项的文件系统开启配额。
- 10. 输入以下命令使配额系统在重启后持续：

```
service boot.quota
```
- 11. 输入 `edquota -u geeko` 在 `/dev/sda2` 上为 `geeko` 设置配额，软限制约为 20 MB，硬限制为 30 MB：

```
edquota -u geeko
```

配额编辑器将在 `vi` 编辑器中出现。

- 12. 在 `soft` 下，删除 0 并输入 20000。
- 13. 在 `hard` 下，删除 0 并输入 30000。
- 14. 完成后，按 Esc 键，然后输入 `:wq`。
- 15. 输入以下命令查看所有已配置用户的配额信息：

```
repquota -av
```
- 16. （可选）如果你提前完成，为 `users` 组设置配额：软限制为 100 MB，硬限制为 150 MB。
- 17. 通过执行以下操作测试配额：
    a. 以 root 身份，创建一个名为 `/export/data2/geeko` 的目录，并通过执行以下操作将所有者更改为 `geeko`：

```
mkdir /export/data2/geeko
chown geeko:users /export/data2/geeko
```
    b. 切换到用户账户 `geeko` 并输入以下命令创建一个文件：

```
su - geeko
dd if=/dev/zero of=/export/data2/geeko/bigfile
```
