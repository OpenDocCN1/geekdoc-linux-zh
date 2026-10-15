
```
Pass 5: Checking group summary information
Block bitmap differences: +238277 +238278 +238279
Fix<y>? yes

Free blocks count wrong for group #29 (7486, counted=7483).
Fix<y>? yes

Free blocks count wrong (219063, counted=219060).
Fix<y>? yes

Inode bitmap differences: +68 +69 +58085 +58086 +58087 +58088 +58089 +58090
Fix<y>? yes

Free inodes count wrong for group #0 (1933, counted=1931).
Fix<y>? yes

Free inodes count wrong for group #29 (1916, counted=1910).
Fix<y>? yes

Directories count wrong for group #29 (11, counted=14).
Fix<y>? yes

Free inodes count wrong (60589, counted=60581).
Fix<y>? yes

/dev/hdb: ***** FILE SYSTEM WAS MODIFIED *****
/dev/hdb: 3419/64000 files (0.5% non-contiguous), 36468/255528 blocks
```

最后，看起来一切都好。请注意系统已从拥有 11 个文件变为拥有 3,419 个文件。

![](img/5ced0c78d748bd190e9027e5549a3622_203_0.png)

### 3. 大多数系统管理员会告诉你，如果遇到 `fsck` 错误，你应该一遍又一遍地运行该命令，直到它最终报告没有错误。这几乎是一种迷信，但也很惊人的是，第二遍检查经常会发现由上一次修复引入的新错误。这种情况也不例外（我在运行这些后续检查之前终于卸载了磁盘）：

```
# fsck -V /disk2
Parallelizing fsck version 1.23 (15-Aug-2001)
[/sbin/fsck.ext2 ... /disk2] fsck.ext2 /dev/hdb
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
/dev/hdb: clean, 3419/64000 files, 36468/255528 blocks
```

使用 `fsck` 的一个经典挫败感：它假设因为我们最近才运行过该命令，所以没有理由再次运行，于是它简单地报告“clean”。但事实并非如此！

`-f` 标志强制运行磁盘完整性检查，这次我还要加上 `-y` 标志，它告诉 `fsck` 假设我对所有非绝对关键的问题都回答 yes：

```
# fsck -fy /disk2
Parallelizing fsck version 1.23 (15-Aug-2001)
[/sbin/fsck.ext2 ... /disk2] fsck.ext2 /dev/hdb
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Inode 2 ref count is 11, should be 10. Fix<y>? yes

Pass 5: Checking group summary information
Block bitmap differences: -238277 -238278
Fix<y>? yes

Free blocks count wrong for group #29 (7483, counted=7485).
Fix<y>? yes

Free blocks count wrong (219060, counted=219062).
Fix<y>? yes

Inode bitmap differences: -58085 -58086 -58088 -58090
Fix<y>? yes

Free inodes count wrong for group #29 (1910, counted=1914).
Fix<y>? yes

Directories count wrong for group #29 (14, counted=12).
Fix<y>? yes

Free inodes count wrong (60581, counted=60585).
Fix<y>? yes
```

`/dev/hdb`: **** FILE SYSTEM WAS MODIFIED ****

`/dev/hdb`: 3415/64000 files (0.5% non-contiguous), 36466/255528 blocks

熟悉的错误？请注意它们并不完全与上一次运行相同（第一次运行报告 inode 计数 11 错误地为九，而这里报告的是 inode 引用计数为 11 应该为 10）。

再做一次检查以求好运：

```
# fsck -fvy /disk2
Parallelizing fsck version 1.23 (15-Aug-2001)
[/sbin/fsck.ext2 -v /disk2] fsck.ext2 -fy /dev/hdb
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/hdb: 3415/64000 files (0.5% non-contiguous), 36466/255528 blocks
```

好。磁盘世界里又一切安好。

### 4. 我们可以用 `mount` 重新挂载磁盘：

```
# ls /disk2
#
# mount -t ext2 /dev/hdb /disk2
# ls /disk2
games/ include/ kerberos/ lost+found/
```

虽然 `mount` 命令本身将在下一小时讨论，但值得指出的是，`fsck` 程序创建了 `lost+found` 目录。从可选的 Linux 命令 `mklost+found` 的手册页中，这里是关于最终会出现在那里的内容的确切描述：

> `mklost+found` 预先为 `lost+found` 目录分配磁盘块，
>
> 因此在运行 `e2fsck(8)` 恢复文件系统时，它不需要在文件系统中分配块来存储大量未链接的文件。这确保了 `e2fsck` 在恢复期间无需在文件系统中分配数据块。

### 5. 每个 `ext2` 文件系统都有一个名为 `lost+found` 的目录，孤立的或其它异常的目录块、文件块和文件材料有时会最终出现在那里。

在我经验中，在 `lost+found` 目录中找到任何半可理解的东西是很少见的。事实上，几乎总是完全空的。以下是一个每秒每分每秒都被访问的实时 Web 服务器系统的例子：

```
$ mount
/dev/sda5 on / type ext3 (rw)
none on /proc type proc (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/sda1 on /boot type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda3 on /home type ext3 (rw)
none on /dev/shm type tmpfs (rw)
/dev/sdb1 on /usr type ext3 (rw)
/dev/sdb2 on /var type ext3 (rw)
```

不带任何选项，`mount` 列出附加到文件系统的磁盘和设备。每个挂载点（别担心，你将在下一小时学习这些）都有自己的 `lost+found` 目录，正如我们所期望的：

```
$ ls -a /lost+found
./  ../
$ ls -a /boot/lost+found
./  ../
$ ls -a /home/lost+found
./  ../
$ ls -a /usr/lost+found
./  ../
$ ls -a /var/lost+found
./  ../
```
