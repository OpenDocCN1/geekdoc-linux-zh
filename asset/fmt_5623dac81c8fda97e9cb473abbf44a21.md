
Command (m for help): `d`

Partition number (1-5): `5`

Command (m for help): `d`

Partition number (1-5): `4`

Command (m for help): `d`

Partition number (1-4): `3`

Command (m for help): `d`

Partition number (1-4): `2`

Command (m for help): `d`

Selected partition `1`

Command (m for help): `w`

```
# partprobe /dev/sdb
```

### 4. 要在 USB 闪盘上添加一个 100MB Linux 交换分区和一个 500MB LVM 分区，输入以下命令：

```
# fdisk -cu /dev/sdb
```
Command (m for help): `n`

Command action

e extended

primary partition (1-4): `1`

First sector (2048-15667199, default 2048): `<ENTER>`

Last sector, +sectors +size(K,M,G) (default 15667199): `+100M`

Command (m for help): `n`

Command action

e extended

primary partition (1-4): `2`

First sector (616448-8342527, default 616448): `<ENTER>`

Last sector, +sectors +size(K,M,G) (default 15667199): `+200M`

Command (m for help): `n`

Command action

e extended

primary partition (1-4): `3`

Partition number (1-4): `3`

First sector (616448-15667199, default 616448): `<ENTER>`

Last sector, +sectors +size(K,M,G) (default 15667199): `+500M`

Command (m for help): `t`

Partition number (1-4): `2`

Hex code (type to list codes): `82`

Changed system type of partition `2` to `82` (Linux swap)

Command (m for help): `t`

Partition number (1-4): `3`

Hex code (type to list codes): `82`

Changed system type of partition `3` to `82` (Linux LVM)

Command (m for help): `w`

```
# partprobe /dev/sdb
# grep sdb /proc/partitions
```
| 8 | | |
| :--- | :--- | :--- |
| 8 | 17 | 102400 sdb1 |
| 8 | 18 | 204800 sdb2 |
| 8 | 19 | 51200 sdb3 |

### 5. 在 Linux 分区上创建 ext3 文件系统，输入：

```
# mkfs -t ext3 /devdb1
```

### 6. 创建名为 `/mnt/mypart` 的挂载点并在其创建 Linux 分区，执行：

```
# mkdir /mnt/mypart
# mount -t ext3 /devdb1 /mnt/mypart
```

### 7. 启用交换分区并开启，输入：

```
# mkswap /devdb2
# swapon /devdb2
```

### 8. 从 LVM 分区创建卷组 `abc`，在该组中创建一个名为 `data` 的 200MB 逻辑卷，在其上 VFAT 文件系统，将其挂载到新目录 `/mnt/test` 并检查是否挂载成功，输入：

```
# pvcreate /devdb3
# vgcreate abc /devdb3
# lvcreate -n data -L 200M abc
# mkfs -t vfat /mapper/abc-data
# mkdir /mnt/test
# mount /mapper/abc-data /mnt/test
```

### 9. 将逻辑卷从 200MB 扩展到 300MB，输入：

```
# lvextend -L +100M /mapper/abc-data
# resize2fs /mapper/abc-data
```

### 10. 从计算机上移除 USB 闪盘，执行：

```
# umount /devdb1
# swapoff /devdb2
# umount /mnt/test
# lvremove /mapper/abc-data
# vgremove abc
# pvremove /devdb3
```

你现在可以从计算机上移除 USB 闪盘了。

## 第 13 章：理解服务器管理

### 1. 使用 `ssh` 命令登录另一台计算机的账户，输入以下命令并在提示时输入密码：

```
$ ssh joe@localhost
joe@localhost's password:
```

### 2. 使用 `ssh` 命令远程执行远程 `/etc/system-release` 文件的内容并在本地系统显示，执行：

```
$ ssh joe@localhost "cat /etc/system-release"
Fedora release 16 (Verne)
```

### 3. 为了在本地系统通过编辑窗口显示一个文件并将其保存到远程主目录，执行：

```
$ ssh -X joe@localhost "gedit newfile"
joe@localhost's password:
$ joe@localhost "cat newfile"
joe@localhost's password:
```

这是我保存在 `joe` 远程主目录中的文件内容。

### 4. 将远程系统 `/usr/share/selinux` 的所有文件递归复制到本地系统的 `/tmp` 目录，使文件的修改时间更新为复制时的时间，执行：

```
$ cp -r joe@localhost:/usr/share/selinux /tmp
joe@localhost's password:
```
```
irpc.bz2               100% 9673      9.5KB/s 00:00
dcc.bz2                100% 15KB      15.2KB/s 00:01
$ ls -l /tmp/selinux | head
drwxr-xr-x. 3 root 4096 Apr 18 05:52 devel
drwxr-xr-x. 2 root 4096 Apr 18 05:52 packages
drwxr-xr-x. 2 root 4096 Apr 18 05:52
```

### 5. 将远程系统 `/usr/share/log` 目录的所有文件递归复制到本地系统的 `/tmp` 目录，并保持文件的修改时间，执行：

```
$ rsync -av joe@localhost:logwatch /tmp/
```

### 6. 为 SSH 通信创建公/私钥对（密钥不设置密码保护），使用 `ssh-copy-id` 将公钥拷贝到远程用户的账户，并在无需输入密码的情况下通过 "`ssh joe@localhost`" 登录机器，使用以下命令：

```
$ ssh-keygen
Generating public/private key pair.
Enter file in which to save the key (/home/.ssh/id_rsa): <ENTER>
/home/.ssh/id_rsa already exists.
Enter passphrase (empty for no passphrase): <ENTER>
Enter same passphrase again: <ENTER>
Your identification has been saved in /home/.ssh/id_rsa.
Your public key has been saved in /home/.ssh/id_rsa.pub.
The key fingerprint is:
58ab:c5:b6:10:aa7c:c5abcd:bd3:f4:89:e2:joe@cusb
The key's random image is:
$ ssh-copy-id -i ~/.ssh/id_rsa joe@localhost
joe@localhost's password:
```
