
`New UNIX password: MyPrivatePassword`

`Retype UNIX password: MyPrivatePassword`

```
molloid@erpi:/home/pi$ whoami

molloid

molloid@erpi:/home/pi$pwd

/home/pi

molloid@erpi:-$ cd /home/molloid

molloid@erpi:-$ ls -1 test.txt

-rw-r-- 1 molloid molloid 0 Jun 18 23:26 test.txt

molloid@erpi:-$ more /etc/group | grep newgroup

newgroup:x:1003:molloid
```

每个用户的家目录由提示符表示。每个用户的家目录在账户创建时创建。每个用户的家目录是他们存储个人文件的地方。每个用户的家目录可以由 `root` 用户更改。每个用户的家目录通常位于 `/home/username`。每个用户的家目录在 `/etc/passwd` 文件中指定。每个用户的家目录也被 shell 用于设置 `$HOME` 环境变量。

每个用户的家目录是用户登录时的起始位置。每个用户的家目录是用户存储文件的私有空间。如果权限允许，其他用户可以访问每个用户的家目录。每个用户的家目录通常会被系统备份。

```bash
molloid@erpi:-$ ls -l test.txt

-rw-r-- 1 molloid molloid 0 Jun 18 23:26 test.txt
```

### 表 3-3: 用于用户、组和权限操作的命令

| 命令 | 说明 |
|---|---|
| `chown molloyd a.txt` | 更改文件所有者。 |
| `chown molloyd:users a.txt` | 同时更改所有者和组。 |
| `chown -Rh molloyd /tmp/test` | 递归更改 `/tmp/test` 的所有权。`-h` 影响符号链接而非指向的文件。 |
| `chgrp molloyd a.txt` | 更改文件的组所有权。 |
| `chgrp -Rh users /tmp/test` | 如上所示，使用相同的 `-h` 递归更改。 |
| `chmod 600 a.txt` | 更改权限，使所有户对文件有读/写权限；组或其他用户没有访问权限。 |
| `chmod u+go a.txt` | 为用户、组和其他人提供 `a.txt` 的读/写权限。 |
| `chmod a-w a.txt` | 移除所有使用 `a` 的用户的访问，`a` 代表（所有用户、组和其他人）。 |
| `chmod u=rw a.txt` | 设置所有人的权限为读/写。 |
| `umask` | 列出默认权限设置。`-s` 以更易读的格式显示 `umask`。 |
| `umask -S` | |
| `umask 022` | |
| `umask u=rw,g=rx,o=rx` | 更改所有新创建的文件和目录的默认权限。这里的两个 `umask` 命令是效的。如果你设置此值创建文件或目录，目录将变为 `drwxr-xr-x`，文件将变为 `-r-r--r--`。你可以在账户的登录文件中设置特定用户的 `umask`。 |
| `chmod u+s myexe` | 设置特殊的 `setuid`（执行时的用户 ID）和 `setgid`（执行时的组 ID）位，`s` 允许程序以另一个已登录用户的身份执行，但具有文件所有者或所属组的权限。例如，你可以用它来允许特定程序以 `root` 用户账户身份执行。如果该文件不可执行，则会出现大写的 `S`，表示应该是小写。 |
| `chmod 6750 myexe` | 在绝对路径中设置 `setuid`。这两个示例都为 `myexe` 赋予了 `-rwxr-s----` 权限，其中设置了 `setuid` 和 `setgid` 位。 |
| `chmod u=rwxs,g=rx,o= myexe` | 出于考虑，`setuid` 位不能应用于 shell 脚本。 |
| `stat /tmp/test.txt` | 为文件或目录提供有用的文件系统信息，例如物理设备和 inode 信息、最后访问时间以及修改/更改时间。 |

以下是表 3-3 中最后一个命令 `stat` 命令的示例：

```
molloyd@rpi:/$ stat test.txt

File: 'test.txt'

Size: 0            Blocks: 0      IO Block: 4096      regular empty file

Device: b02h/45826d  Inodes: 6723       Links: 1

Access: (0644/r-r-r--) Uid: (0/root) Gid: (0/root)

Access: 2015-06-19 00:28:55.1326384+0000

Modify: 2015-06-19 00:28:55.1326384+0000

Change: 2015-06-19 00:07:13.151016384+0000

Birth:-
```

注意，Linux 中的每个文件都保留了访问时间、修改时间和更改时间。你可以分别使用 `touch -a test.txt` 和 `touch -m test.txt` 人为地更新访问时间和修改时间。更改时间在这都会受到影响。更改时间还会受到 `chmod` 等系统操作的影响；修改时间受文件写入的影响；访问时间受文件读取的影响。然而，这种操作行为意味着读取文件会导致写入！Linux 的这一特性会对 RPi 的 SD 卡造成巨大的损耗，并导致 I/O 性能下降。因此，通常在 `/etc/fstab` 配置文件中使用 `noatime` 挂载选项禁用 RPi 启动 SD 卡上的访问时间。还有一个类似的 `nodatime` 选项可以仅禁用目录的访问时间；然而，`noatime` 选项禁用了-

完成对图 3-3 的讨论：图中的示例中该文件有 22 个链接。一个目录代表子目录的数量、父目录 (`.`) 自身 (`()`)。该条目由 `root` 所有并属于 `root` 组。接的条目 4096 是存储该目录内包含的文件元数据所需的大小。

最后一点：如果你在根目录下对目录 `ls -ld`，你将在 `/tmp` 目录的权限中看到一个位。这被称为“粘滞位”，意味着仅有写权限不足以删除文件。因此，在 `/tmp` 目录中，任何用户都可以创建文件，但没有用户可以删除他人的文件：

```
molloyd@rpi:/$ cd /
molloyd@rpi:/$ ls -dhl tmp

drwxrwt 7 root root 4.0K Jun 19 00:18:21 tmp
```

## 第3章 探索嵌入式 Linux 系统

在这个示例中，有一个 USB micro-SD 卡读取器，其中包含一张 32 GB 的卡，并插入了一个 USB 端口。它显示为块设备 `sda`，带有一个分区 `sda1`，如下：

```
pi@erpi ~ lsblk
NAME MAJ:MIN SIZE TYPE MOUNTPOINT
sda      8:0 29.8G 0 disk
└sda1     8:1 29.8G 0 part
mmcblk0 17:0 14.8G 0 disk
  └─mmblk0p1 179:1 500M part /boot
  └─mmblk0p2 179:2 14.8G 0 part /
```

显然，USB 端口可以用于额外的存储，如果你正在录制视频数据且系统 SD 卡容量不足，这将非常有用。你可以使用下面的示例测试 SD 卡的性能，以确保它们符合你的应用程序的需求。

### 示例：测试 SD 卡读取性能

你可以使用 `hdparam` 程序测试 SD 卡和控制器的性能。例如，在 RPI2：

```
pi@erpi ~ sudo apt install hdparam
pi@erpi ~ sudo hdparam -tT /dev/mmcblk0 /dev/sda
/dev/mmcblk0
Timing cached reads: 868 MB in 2.00 seconds = 433.95 MB/sec
Timing buffered disk reads: 56 MB in 3.11 seconds = 18.01 MB/sec
/dev/sda
Timing cached reads: 890 MB in 2.00 seconds = 444.34 MB/sec
Timing buffered disk reads: 74 MB in 3.09 seconds = 27.24 MB/sec
```
