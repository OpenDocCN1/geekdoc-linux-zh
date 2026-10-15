
$ cat /etc/fstab 的输出如下：

```
# 设备 挂载点 类型 选项 频率 路径号
/dev/hda3 / ext3 defaults 1 1 *根文件系统*
/dev/hda5 /data ext3 defaults 1 2
none /dev/pts devpts gid=5,mode=620 0 0
none /proc proc defaults 0 0
none /dev/shm tmpfs defaults 0 0
# Windows 分区：
/dev/hda1 /win vfat noauto,defaults,user,uid=2076,gid=10 0 0
/dev/hda3 swap swap defaults 0 0
/dev/cdrom /mnt/cdrom iso9660 noauto,owner,ro 0 0 *世界可挂载*
/dev/fd0 /mnt/floppy auto noauto,owner 0 0 *软盘，相同*
```

允许以 `#` 开头的注释。对各种选项的讨论将在稍后的 8.2.1 节“使用挂载选项”（第 239 页）中提供。

相同的文件格式用于 `/etc/mtab`，这是 `mount` 在文件系统挂载时写入信息的地方；`umount` 在文件系统卸载时从该文件中删除信息：

```
$ cat /etc/mtab
/dev/hda2 / ext3 rw 0 0
none /proc proc rw 0 0
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/hda5 / ext3 rw 0 0
none /dev/pts devpts rw,gid=5,mode=620 0 0
none /dev/shm tmpfs rw 0 0
none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0
/dev/hda1 /win vfat rw,noexec,nosuid,no,uid=2076,gid=10,users=n roold 0 0
```

内核以相同的格式在 `/proc/mounts` 中提供（几乎）相同的信息：

```
$ cat /proc/mounts
rootfs / rootfs 0 0
/dev/root / ext3 rw 0 0
/proc /proc proc rw 0 0
```

脚注 5：在 GNU/Linux 和大多数系统上。Solaris 和一些基于 System V Release 4 的系统使用 `/etc/vfstab`，可能采用不同的格式。

## 8.2 文件系统管理文件

```
usbdevfs /proc/bus/usb usbdevfs rw 0 0
/dev/hda5 /d ext3 rw 0 0
none /dev/pts devpts rw 0 0
none /dev/shm tmpfs rw 0 0
none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0
/dev/hda1 /win vfat rw,nosuid,nodev,noexec 0 0
```

请注意，`/etc/mtab` 包含一些 `/proc/mounts` 中没有的信息（例如，查看 `/win` 挂载点的那一行）。反过来说，使用 `mount -f` 也可以向 `/etc/mtab` 中写入并非真实存在的条目（这种做法有其用途，参见 `mount(8)`）。总之，`/proc/mounts` 始终描述实际挂载的内容；然而，`/etc/mtab` 包含了 `/proc/mounts` 中没有的挂载选项信息。因此，为了获得完整的情况，您可能需要读取这两个文件。

### 8.2.1 使用挂载选项

`mount` 命令支持控制内核允许或禁止对文件系统执行哪些操作的选项。这些选项有很多。只有两个在命令行中真正有用：

- `ro`

  以只读方式挂载文件系统。这对于 CD-ROM 和 DVD 等只读介质是必需的。

- `loop`

  使用回环设备将普通文件作为文件系统处理。我们在前面已经展示过此操作的示例（参见第 8.1.3 节“挂载文件系统：mount”，第 236 页）。

选项通过 `-o` 命令行选项传递，并且可以组合使用，以逗号分隔。例如，以下是之前使用的命令行：

```
mount -t iso9660 -o ro,loop shrink6-1386-disc1.iso /mnt/cdrom
```

其余选项旨在用于 `/etc/fstab`（尽管也可以在命令行上使用）。以下列表列出了我们认为在日常使用中最重要的选项。

- `auto, noauto`

  标记为 `auto` 的文件系统将在系统启动时通过 `mount -a`（挂载所有文件系统）进行挂载。`noauto` 文件系统必须手动挂载。

  这些文件系统仍然会出现在 `/etc/fstab` 中，与其他文件系统并列。（例如，参见我们 `/etc/fstab` 文件中之前显示的 `/win` 条目。）

- `defaults`

  使用默认选项 `rw, suid, dev, exec, auto, nouser` 和 `async`。（`async` 是一个高级选项，可增加 I/O 吞吐量。）

- `dev, nodev`

  允许（或禁止）在文件系统上使用字符设备或块设备文件。

- `exec, noexec`

  允许（或禁止）执行文件系统上的二进制可执行文件。

- `user, nouser`

  允许（或禁止）任何用户挂载此文件系统。这对 CD-ROM 很有用；即使在单用户工作站上，不切换到 root 用户就能挂载 CD 也是方便的。只有挂载文件系统的用户才能卸载它。`user` 隐含 `noexec, nosuid` 和 `nodev` 选项。

- `suid, nosuid`

  支持（或不支持）文件系统上可执行文件中的 `setuid` 和 `setgid` 位。

- `rw`

  以读写方式挂载文件系统。

`nodev, noexec` 和 `nosuid` 选项对于软盘和 CD-ROM 文件系统的安全性特别有价值。考虑一种学生环境，其中允许学生挂载自己的软盘或 CD。制作一个包含 `setuid-root` shell 或具有全系统写权限的硬盘设备文件的文件系统是很简单的，这可能会让一些精明的用户修改系统文件的权限。

每个文件系统都有特定的额外选项。对于 `ext2` 和 `ext3`，一个重要的选项是 `grpid`。我们将对该选项的讨论推迟到第 11.5.1 节“新文件和目录的默认组”，第 412 页。所有受支持文件系统的详细信息可在 `mount(8)` 手册页中找到。

作为一个具体的例子，让我们重新考虑我们系统中 Windows 分区的那一行：

```
# device mount-point type options freq
/dev/hda1 /win vfat noauto,defaults,user,uid=2076,gid=10 0 0
```

`noauto` 选项防止 Windows 分区在启动时挂载。`defaults` 选项等同于 `rw, suid, dev, exec, async`。`user` 选项允许我们在不是 root 的情况下挂载文件系统。`uid=` 和 `gid=` 选项强制 `/win` 中的文件属于我们普通用户，这样我们在处理该分区时就不需要 root 权限。

### 8.2.2 处理已挂载的文件系统：getmntent()

可以通过 `getmntent()` 例程组以编程方式读取 `/etc/fstab`、`/etc/mtab` 和 `/proc/mounts` 中的任何一个：

```c
#include <stdio.h>
#include <mntent.h>
```

*(Glibc)*

```c
FILE *setmntent(const char *filename, const char *type);
struct mntent *getmntent(FILE *filep);
int addmntent(FILE *filep, const struct mntent *mnt);
int endmntent(FILE *filep);
char *hasmntopt(const struct mntent *mnt, const char *opt);
```

`setmntent()` 打开包含挂载点条目的文件。`filename` 参数是要打开的文件名。`type` 参数类似于 `fopen()` 的第二个参数，指示读、写或读写访问。（考虑到 `mount` 命令，它必须为每个挂载的文件系统向 `/etc/mtab` 添加一个条目，而 `umount` 必须删除一个。）返回的 `FILE *` 类型值随后用于其他例程。

`getmntent()` 遍历文件，返回指向静态 `struct mntent` 的指针，该结构被填充了相应的值。这个静态存储每次调用时都会被覆盖。当没有更多条目时，它返回 `NULL`。（这与读取密码文件和组文件的例程类似；参见第 6.3 节“用户和组名”，第 195 页。）

调用 `addmntent()` 向打开的文件末尾添加更多信息；它旨在供 `mount` 使用。
