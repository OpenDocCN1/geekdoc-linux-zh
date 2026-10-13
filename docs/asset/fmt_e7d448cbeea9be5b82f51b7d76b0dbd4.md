
```
# cat /etc/fstab
/dev/VolGroup00/lvol1  ext3    defaults       1 2
/dev/VolGroup00/lvol2  /usr    ext3    defaults       1 2
/dev/VolGroup01/lvol2 /home   ext3    defaults       1 2
/dev/VolGroup01/var    ext3    defaults       1 2
/dev/VolGroup00/lvol3 /tmp     ext3    defaults       1 2
/dev/VolGroup00/lvol6 /opt     ext3    defaults       1 2
LABEL=/root          /boot   ext3    defaults       0 0
tmpfs                /dev/shm  tmpfs   defaults       0 0
devpts               devpts  gid=5,mode=662 0 0
sys                 /sys     sysfs   defaults       0 0
proc                 /proc    proc      defaults       0 0
/dev/VolGroup00/lvol7  swap    defaults       0 0
```

每行条目有六个字段，说明如下：

- 第一个字段定义文件系统所在地或与其关联的 `LABEL`（标签）。
- 第二字段定义挂载点或 `swap`（交换分区）。
- 第三个字段指定文件系统类型，例如 `ext2`、`ext3`、`vfat`、`iso9660` 或 `swap`。
- 第四个字段指定挂载文件系统时使用的任何选项。某些选项在表 14-2 中列出并描述。
- 第五个字段指定系统关机时是否将数据写入文件系统。值为 `0` 表示禁用，值为 `1` 表示启用。
- 最后一个字段指示在文件系统上运行 `fsck`（文件系统检查和修复）工具的序列号。默认情况下，`/` 为 1，其他本地文件系统为 2，基于内存、远程和可移动的文件系统为 0。

使用 `vi` 向 `fstab` 中添加 `/data1` 和 `/data2` 文件系统条目。更新后的文件将包含以下额外目：

```
# cat /etc/fstab
/dev/sdb1             /data0   ext3    defaults       1 2
/dev/VolGroup01/lvol1  /data1   ext3    defaults       1 2
/dev/VolGroup01/lvol2  /data2   ext3    defaults       1 2
```

制作条目后，运行以下命令挂载文件中列出但尚未挂载的文件系统：

```
# mount -a
```

要仅挂载 `/data1`，请执行以下操作之一：

```
# mount /data/1
# mount /dev/VolGroup01/lvol1
```

记得 `mount` 命令引用 `fstab` 文件来挂载文件系统。

## 移除文件系统

移除文件系统是一个破坏性操作。它会清除文件系统中的所有数据。

## 访问控制列表 (ACL)

访问控制列表 (`ACL`) 为用户和组提供了扩展权限。

### 列出 ACL

使用命令 `ll` 和 `getfacl` 可以确定是否设置了 `ACL`。

### 更改 ACL

让我们使用 `setfacl` 为 `file1` 设置 `ACL` 以了解其行为。

如果不是，运行以下命令以在激活 `ACL` 后重新挂载 `/home`：

```
# mount -o remount,acl /home
```

在由 `RHEL` 安装创建的文件系统上，您需要启用 `ACL` 支持，然后进行挂载或重新挂载。以下是在 `/dev/sdb1` 上启用该选项的方法：

```
# tune2fs /dev/sdb1 -o acl
```

现在，执行 `setfacl` 命令为 `user2` 设置权限：

```bash
$ setfacl -m u:user2:7 file1
```

`ll` 命令报告如下：

```
$ ll
-rw-rwx--+ 1 user1 0 Nov 27 10:11 file1
```

注意权限旁边的 `+` 号。这表示 `file1` 设置了 `ACL`。

`getfacl` 命令报告如下：

```
$ getfacl file1
# file: file1
# owner: user1
# group: user1
user::rw-
user:user2:rwx
group::r-
mask:rwx
other::r
```

为 `user2` 添加了一行，显示其具有 `rwx (7)` 权限。还添加了一行显示掩码（`mask`）的行，且同样设置为 `rwx (7)`。掩码的值决定了分配给特定用户或组的最大权限。在这种情况下，分配给 `user2` 的最大权限为 `rwx`，因此掩码也被设置为 `rwx`。

要修改这些条目使 `user4` 拥有读/写权限，执行以下操作：

```bash
$ setfacl -m u:user4:rw file1
```

`getfacl` 命令报告如下：

```
$ getfacl file1
# file: file1
# owner: user1
# group: user1
user::rw-
user:user2:rwx
group::r-
mask:rwx
other::r
```

要删除 `user2` 的 `ACL` 条目，使用 `setfacl` 的 `-x`：

```bash
$ setfacl -x u:user2 file1
$ getfacl
# file: file1
# owner: user1
# group: user1
user::rw-
user:user4:rw-
mask:rwx
other::r
```

注意最大权限现在减少为读/写，因为这是掩码定义的特定用户或组的最大值。要删除 `file1` 上设置的所有 `ACL` 条目，使用 `setfacl` 的 `-b`：

```bash
$ setfacl -b file1
```

要设置 `file1` 的 `ACL` 使所有者具有 `rwx`、组具有 `rw`、其他 `user3` 具有 `rwx`，使用 `setfacl` 的 `-m`：

```bash
$ setfacl -m u::rwx,g:rw,o:r,u:user3:rwx file1
$ getfacl
# file: file1
# owner: user1
# group: user1
user::rwx
user:user3:rwx
group::rw-
other::r
```

上述命令使用八进制表示为：

```bash
$ setfacl -m u::7,g:6,o:4,u:user3:7 file1
```

## 默认 ACL

有时，不同组的多个用户共享同一个目录的内容是必须的。他们希望设置权限，使得在该创建的文件和子目录继承父目录的权限。在目录上设置默认 `ACL` 可以满足这一需求。默认 `ACL` 可以描述为分配在目录上的最大任意权限。

例如，为 `/home/user3/project` 目录为 `user1` 和 `user2` 设置默认 `ACL`，使其具有读写权限，请执行以下操作：

```
# setfacl -m d:user1:6,d:user2:6 /home/user3/project
```

使用 `getfacl` 命令验证。

## 理解磁盘配额

默认情况下，只要有足够的空间，用户可以在系统中创建尽可能多的文件。这允许他们占用大量文件空间来存储文件，可能包括不必要的数据。通过配额管理，您可以控制哪个用户可以使用系统中的多少空间。配额可以设置为用户级别，也可以设置为组级别，以便组内所有用户共享空间。

表 14-5 列出了配额管理命令。

| 命令 | 描述 |
| --- | --- |
| `edquota` | 编辑/设置/复制用户配额设置。 |
| `quota` | 显示配额设置和使用状态。 |
| `quotacheck` | 检查配额使用情况。 |
| `quotaoff` | 禁用文件系统的配额。 |
| `quotaon` | 启用文件系统的配额。 |
| `repquota` | 报告配额使用情况。 |
| `setquota` | 在命令行设置磁盘配额。 |

表 14-5 配额管理命令

配额可以通过 `inode`（用户可以创建的文件数）或磁盘大小（用户可以使用的磁盘空间）来设置。内核默认支持配额管理。在 `/boot/config-uname -r` 中对 `CONFIG_QUOTA` 进行 `grep` 将显示该指令值为 "y"，表示配额已启用：

```
# grep CONFIG_QUOTA /boot/config-uname -r
CONFIG_QUOTA=y
```
