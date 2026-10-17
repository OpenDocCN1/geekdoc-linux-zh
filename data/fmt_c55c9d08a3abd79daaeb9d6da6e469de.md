
17. 输入 `exit` 并按 `Enter` 退出你的 shell。

## 项目 6-2

在实实践项目中，将为你的 Ubuntu Server 18 虚拟机添加硬盘，配置软件 RAID 5 卷，并模拟硬盘故障和恢复。在项目结束时，你将移除 RAID 配置。

1. 在你的 Ubuntu Server 18 虚拟机上，使用用户名 `root` 和密码 `LINUXrocks!` 登录命令行终端 `tty1`。
2. 在命令提示符处，输入 `poweroff` 并按 `Enter` 关闭虚拟机的电源。在你的虚拟化软件中，为你的虚拟机配置添加四个新的 1GB 动态分配 SATA/SAS 硬盘。完成后，启动你的 Ubuntu Server 18 虚拟机。
3. 当你的 Ubuntu Server 18 虚拟机启动后，使用用户名 `root` 和密码 `LINUXrocks!` 登录命令行终端 `tty1`。
4. 在命令提示符处，输入 `lsblk` 并按 `Enter`。注意额外磁盘设备 `sdb`、`sdc`、`sdd` 和 `sde` 的名称。
5. 在命令提示符处，输入 `mdadm --create /dev/md0 --level=5 --raid=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde --verbose` 并按 `Enter`。
6. 在命令提示符处，输入 `cat /proc/mdstat` 并按 `Enter`。你的 RAID 5 卷是否成功创建了？
7. 在命令提示符处，输入 `cat /etc/mdadm/mdadm.conf` 并按 `Enter`。你的 RAID 5 卷是否根据定义列在该配置文件文件中？
8. 在命令提示符处，输入 `mdadm --detail --scan --verbose >/etc/mdadm/mdadm.conf` 并按 `Enter`。接下来，输入 `cat /etc/mdadm/mdadm.conf` 并按 `Enter`，查看你的启动配置。
9. 在命令提示符处，输入 `mkfs -t ext4 /dev/md0` 并按 `Enter`，使用 ext4 文件系统格式化你的 RAID 5 卷。
10. 在命令提示符处，输入 `mkdir /data` 并按 `Enter` 为你的 RAID 5 卷创建一个挂载点，然后输入 `mount /dev/md0 /data` 并按 `Enter` 将你的 RAID 5 卷挂载到那里。
11. 在命令提示符处，输入 `cp /etc/hosts /data` 并按 Enter。接下来，输入 `ls -F /data` 并按 Enter 验证 hosts 文件已复制到你的文件系统。在该文件系统上创建了什么目录？为什么？
12. 在命令提示符处，输入 `df -ht` 并按 Enter。你的 RAID 5 卷的总大小有多大？为什么不是 4GB `4 x 1GB` 磁盘？
13. 在命令提示符处，输入 `lsblk` 并按 Enter。注意每个磁盘的 md0 设备关联。接下来，输入 `blkid` 并按 Enter。`dev/md0` 是否有一个可以在 `/etc/fstab` 中使用的文件系统 UUID，以便在启动时自动创建 RAID 卷？
14. 在命令提示符处，输入 `mdadm --detail /dev/md0` 并按 Enter。RAID 卷中的所有设备都激活并正常工作了吗？
15. 在命令提示符处，输入 `mdadm --manage --set-faulty /dev/md0 /dev/sdc` 并按 Enter 模拟 `/dev/sdc` 磁盘损坏。接下来，输入 `mdadm --detail /dev/md0` 并按 Enter。注意 RAID 卷的状态是否列为 `clean` 或 `degraded`。
16. 输入 `ls -F /data` 并按 Enter。你的文件仍然可用且活跃吗？
17. 在命令提示符处，输入 `mdadm --manage /dev/md0 -r /dev/sdc` 并按 Enter 将 `/dev/sdc` 设备恢复到 RAID 卷中。在生产环境中，这就是你物理上从服务器上移除硬盘并更换新硬盘的地方。
18. 在命令提示符处，输入 `mdadm --manage /dev/md0 -a /dev/sdc` 并按 Enter 将 `/dev/sdc` 设备添加到 RAID 卷中。接下来，输入 `mdadm --detail /dev/md0` 并按 Enter。注意驱动器状态是否列为 `spare`。重建 RAID 卷就是在该磁盘上重建数据。几分钟后，运行你之前的命令。状态应该列出 `active sync`，这表明添加的设备现在可以工作并是你的 RAID 卷的一部分。
19. 在命令提示符处，输入 `umount /data` 并按 Enter 卸载你的 RAID 卷。接下来，输入 `mdadm --stop /dev/md0` 并按 Enter 移除你的 RAID 卷。
20. 在命令提示符处，输入 `fdisk /dev/sdb` 并按 Enter。接下来，输入 `w` 并按 Enter 保存更改，这将移除 `/dev/sdb` 上现有的 RAID 签名。对 `/dev/sdc`、`/dev/sdd` 和 `/dev/sde` 重复此操作三次。
21. 最后，输入 `rm -f /etc/mdadm/mdadm.conf` 移除配置。
22. 输入 `exit` 退出你的 shell。

## 项目 6-3

在这个实实践项目中，你将在你的 Ubuntu Server 18 虚拟机上安装并配置 ZFS 系统。在项目结束时，你将移除 ZFS 配置。

1. 在你的 Ubuntu Server 18 虚拟机上，使用用户名 `root` 和密码 `LINUXrocks!` 登录命令行终端 `tty1`。
2. 在命令提示符处，输入以下命令（按顺序）添加存储库并在系统上安装 ZFS 支持：
   - `apt-get update`
   - `add-apt-repository main`
   - `add-apt-repository restricted`
   - `add-apt-repository universe`
   - `apt-get install zfsutils-linux`
Ubuntu 使用与 Fedora不同的包管理器。`apt-get` 命令等同于从存储库下载并安装软件的 `dnf` 命令。`apt-get` 和 `dnf` 在第1章中讨论过。
3. 在命令提示符处，输入 `zpool create /dev/sdb` 并按 Enter 在 `/dev/sdb` 上创建一个名为 data 的具有项目6-2签名的简单 ZFS 卷。接下来，在命令提示符处输入 `zpool list` 并按 Enter 查看你的配置。
4. 在命令提示符处，输入 `df -h` 并按 Enter。注意 ZFS 卷自动挂载到 `/data`。接下来，在命令提示符处输入 `zpool status` 并按 Enter。注意 ZFS 为数据 `/dev/sdb1` 和配置 `/dev/sdb2` 创建了分区。
5. 在命令提示符处，输入 `cp /etc/hosts /data` 并按 Enter 将 hosts 文件复制到新的 ZFS 文件系统。接下来输入 `ls -F /data` 验证 hosts 文件已成功复制。
6. 在命令提示符处，输入 `zpool create mirror /dev/sdb /dev/sdc` 并按 Enter 在 `/dev/sdb` 和 `/dev/sdc` 上创建一个名为 data 的镜像 ZFS 卷，它挂载到 `/data` 目录。接下来，在命令提示符处输入 `zpool list` 和 `zpool status` 并按 Enter。你的镜像是否有问题？
7. 在命令提示符处，输入 `zfs list` 并按 Enter。注意 ZFS 为每个硬盘 `/dev/sdb1` 和 `/dev/sdc1` 的数据以及配置 `/dev/sdb2` 和 `/dev/sdc2` 创建了分区。
8. 在命令提示符处，输入 `dd if=/dev/zero of=/dev/sdb1 count=100` 并按 Enter 使用 dd 命令覆盖 `/dev/sdb1` 的部分模拟磁盘损坏。接下来，在命令提示符处输入 `zpool scrub data` 并按 Enter 更新 ZFS 文件系统的状态，并在命令提示符处输入 `zpool status` 并按 Enter。你的镜像列出问题吗？
9. 在命令提示符处，输入 `zpool detach data /dev/sdb` 并按 Enter 从镜像中移除坏磁盘 `dev/sdb`。在命令提示符处输入 `zpool status` 并按 Enter 验证它不再列出。
10. 在命令提示符处，输入 `zpool attach data /dev/sdc /dev/sdd -f` 并按 Enter 将 `/dev/sdc` 上的数据镜像到新磁盘，然后在命令提示符处输入 `zpool status` 并按 Enter。镜像是否使用了 `/dev/sdc` 和 `/dev/sdd`？
11. 在命令提示符处，输入 `zpool iostat -v data` 并按 Enter 查看镜像的输入和输出统计。接下来，输入 `zpool destroy data` 并按 Enter 移除数据镜像。
12. 在命令提示符处，输入 `zpool create raidz /dev/sdb /dev/sdc /dev/sdd /dev/sde -f` 并按 Enter 使用来自 `/dev/sdb`、`/dev/sdc`、`/dev/sdd` 和 `/dev/sde` 的数据创建一个 RAID-Z 卷，然后在命令提示符处输入 `zpool status` 并按 Enter。接下来，输入 `zpool iostat -v data` 并按 Enter 查看 RAID-Z 卷的输入和输出统计。
13. 在命令提示符处，依次以下命令并按 Enter 为 `/data` 创建三个子目录：
   - `mkdir /data/webstorage`
   - `mkdir /data/databases`
   - `mkdir /data/filestorage`
14. 在命令提示符处，输入 `zfs list` 并按 Enter。`webstorage`、`databases` 和 `filestorage` 目录列出了吗？为什么？接下来输入以下命令并按 Enter 创建三个文件系统：
   - `zfs create /data/webstorage`
   - `zfs create /data/databases`
   - `zfs create /data/filestorage`
15. 在命令提示符处，输入 `zfs list` 并按 Enter。`webstorage`、`databases` 和 `filestorage` 目录列出了吗？为什么？
16. 在命令提示符处，输入 `zfs get all data/webstorage` 并按 Enter 查看 webstorage 文件系统的可用选项。接下来，在命令提示符处输入 `zfs set quota=1gb data/webstorage` 并按 Enter 为文件系统内存储的文件设置 `zfs compression=lz4` 数据压缩。最后，输入 `zfs get all data/webstorage` 并按 Enter 验证你的设置是否已更改。
17. 在命令提示符处，输入 `zpool destroy data` 并按 Enter 移除数据卷。
18. 在命令提示符处，输入 `fdisk /dev/sdb` 并按 Enter。接下来，输入 `d` 并按 Enter 再次按 Enter 删除 ZFS 配置分区。接下来，输入 `d` 和

## 第 6 章 Linux 服务器部署

按下 `Enter` 进入 ZFS 数据分区。最后，输入 `w` 并按 `Enter` 保存你的更改。对 `/dev/sdc`、`/dev/sdd` 和 `/dev/sde` 重复此操作三次。

- 20. 输入 `exit` 并按 `Enter` 退出 shell。

## 项目 6-4

在手实践项目中，你将在你的 Ubuntu Server 18 机器上配置 BTRFS 文件系统。项目结束时，你将移除 BTRFS 配置。

- 1. 在你的 Ubuntu Server 18 虚拟机上，使用用户名 `root` 和密码 `LINUXrocks` 登录命令行终端 `tty1`！
- 2. 在命令提示符处，输入 `mkfs.btrfs -m raid-0 -d raid0 /dev/sdb /dev/sdc /dev/sdd -f` 并按 Enter 创建一个跨三块磁盘的 RAID 0 BTRFS 卷。对于 `/dev/sdb`、`/dev/sdc` 和 `/dev/sdd`，不需要 `-f` 参数，因为它们来自项目 6-3 中的 ZFS 签名。从输出可以看出，系统配置、数据和文件系统元数据是不容的。接下来，输入 `btrfs filesystem show /dev/sdb` 并按 `Enter`。注意输出。
- 3. 在命令提示符处，输入 `mount /dev/sdb` 并按 `Enter` 将你的新 BTRFS 卷挂载到 `/data` 目录。
- 4. 在命令提示符处，输入 `df -ht` 并按 `Enter`。注意卷大小为 3GB，而 BTRFS 文件系统跨越了 1GB 的 sdb、sdc 和 sdd 设备，仅显示 sdb 已挂载到 `/data` 目录。最后，输入 `btrfs filesystem df /data` 并按 `Enter`。注意输出。
- 5. 在命令提示符处，输入 `btrfs add -f /dev/sde` 并按 `Enter` 将 `/dev/sde` 添加到你的 BTRFS 卷。接下来，输入 `btrfs filesystem balance /data` 并按 Enter 将现有数据和系统元数据扩展到新设备。
- 6. 在命令提示符处，输入 `df -hT` 并按 `Enter`。注意卷大小为 4GB。接下来，输入 `btrfs filesystem df /data` 并按 `Enter`。注意输出。
- 7. 在命令提示符处，输入 `btrfs subvolume list /data` 并按 `Enter`。列出了任何子卷吗？接下来，输入 `btrfs subvolume create /data/archive` 并按 Enter 在 archive 下创建一个子卷和子目录。最后，输入 `btrfs subvolume list /data` 并按 Enter 查看你的新子卷。
- 8. 在命令提示符处，输入 `cp /etc/hosts /data/archive` 并按 `Enter` 在 archive 卷中创建文件的副本。
- 9. 在命令提示符处，输入 `mkdir /archive` 并按 `Enter`。接下来，输入 `mount subvol=archive,compress=lzo /dev/sdb /archive` 并按 `Enter` 启用自动压缩并将你的子卷挂载到 `/archive` 目录。
- 10. 在命令提示符处，输入 `df -hT` 并按 `Enter`。接下来，输入 `ls -F /archive` 并按 `Enter`。你的 hosts 在列表中吗？
- 11. 接下来，输入 `umount /archive ; umount /data` 并按 `Enter` 卸载你的 BTRFS 子卷和卷。
- 12. 在命令提示符处，输入 `mkfs.btrfs -m raid1 -d /dev/sdb /dev/sdc /dev/sdd /dev/sd -f` 并按 Enter 创建跨四块磁盘的 RAID 1 BTRFS 卷。注意输出，系统配置、数据和文件系统元数据是容错性的。接下来，输入 `btrfs filesystem show /dev/sdb` 并按 Enter。注意输出。
- 13. 在命令提示符处，输入 `mount /dev/sdb /data` 并按 Enter 将你的新 BTRFS 卷挂载到 `/directory`。
- 14. 在命令提示符处，依次输入以下命令并按 Enter。将输出与你在步骤 4 中看到的输出进行比较：
   - a. `df -hT`
   - b. `lsblk`
   - c. `btrfs filesystem df /data`
- 15. 接下来，输入 `umount /data` 并按 Enter 卸载你的 BTRFS 卷。
- 16. 在命令提示符处，输入 `mkfs.btrfs -m raid5 -d raid5 /dev/sdb /dev/sdd /dev/sde -f` 并按 Enter 创建跨四块磁盘的 RAID 5 BTRFS 卷。注意输出，系统配置、数据和文件系统元数据是容错性的。接下来，输入 `btrfs filesystem show /dev/sdb` 并按 Enter。
- 17. 在命令提示符处，输入 `mount /dev/sdb /data` 并按 Enter 将你的新 BTRFS 卷挂载到 `/directory`。
- 18. 在命令提示符处，依次输入以下命令并按 Enter。将输出与你在步骤 4 中看到的输出进行比较：
   - a. `df -hT`
   - b. `lsblk`
   - c. `btrfs filesystem df /data`
- 19. 接下来，输入 `umount /data` 并按 Enter 卸载你的 BTRFS 子卷。
- 20. 在命令提示符处，输入 `btrfs filesystem show /dev/sdb` 并按 Enter 检查你的 BTRFS 卷。
- 21. 输入 `exit` 并按 `Enter` 退出 shell。

## 第 6 章 Linux 服务器部署

## 项目 6-5

在这个手实践项目中，你将在你的 Ubuntu Server 18 机器上配置 BTRFS 文件系统。项目结束时，你将移除 BTRFS 配置。

- 1. 在你的 Ubuntu Server 18 虚拟机上，使用用户名 `root` 和密码 `LINUXrocks` 登录命令行终端 `tty1`！
... 

# 第6 章 Linux 服务器部署

- 15. 在命令提示符下，输入 `journalctl -b | less` 并按回车。这些信息与上一步相比有什么不同？输入 `q` 退出 less 工具。
- 16. 输入 `poweroff` 并按回车，关闭你的 Ubuntu Server 18 虚拟机。

## 项目 6-6

在动手项目中，你将使用实盘安装介质在 Fedora Linux 虚拟机上进行系统救援，检查根文件系统是否存在错误并更改 root 用户的密码。

- 1. 在你的虚拟化软件中，确保 Fedora 虚拟机的 DVD 已挂载了 Fedora 28 Live 的 ISO 镜像 `Fedora-Workstation-Live-x86_64-28-1.1.iso`。然后，使用你的虚拟化软件连接到 Linux 虚拟机。
- 2. 在 Fedora Live 界面上，选择 `Start Fedora-Workstation-Live 28` 并按回车。
- 3. 在图形桌面和 Fedora 屏幕加载后，根据提示选择 `Try Fedora and Close`。
- 4. 在 GNOME 桌面中导航到 Activities、Show Applications、Terminal 以打开一个 BASH 终端。
- 5. 在命令提示符下，输入 `su - root` 并按回车切换到 root 用户。
- 6. 在命令提示符下，输入 `mount -t proc` 并按回车查看已挂载的文件系统。硬盘上的根文件系统？
- 7. 在命令提示符下，输入 `fsck -f /dev/sda3` 并按回车检查你的 `/` 根分区是否存在错误。
- 8. 在命令提示符下，输入 `mount /dev/sda3 /mnt` 并按回车，将硬盘上的 `/` 根文件系统挂载到 Fedora 系统的 `/mnt` 目录。接着，输入 `mount /dev/sda1 /mnt/boot` 并按回车，将硬盘上的 `/boot` 文件系统挂载到 Fedora 系统的 `/mnt/boot` 目录。
- 9. 在命令提示符下，输入 `mount -t proc /proc /proc` 并按回车，挂载 `/proc` 文件系统。
- 10. 在命令提示符下，输入 `chroot /mnt` 并按回车，将你的 Live 系统的根文件系统切换到根磁盘。输入 `ls /root` 并按回车。你认识这些文件吗？
- 11. 在命令提示符下，输入 `password root` 并按回车。根据提示提供新的 root 密码 `Secret123` 并按回车。两次。在接收到 `Secret123` 密码时你看到了什么？
- 12. 点击右上角的电源图标，选择出现的电源图标，并点击 `Power Off` 关闭你的 Fedora Linux 安装系统。
- 13. 在你的虚拟化软件的虚拟机设置中，确保 DVD 驱动器不再挂载到 Fedora ISO 镜像。
- 14. 最后，使用你的虚拟化软件启动 Fedora 虚拟机。在系统加载后，按 `Ctrl+Alt+F5` 切换到命令行终端 `tty5`，并使用用户名 `root` 和密码 `Secret123` 登录终端。你成功了吗？
- 15. 在命令提示符下，输入 `passwd root` 并按 `Enter`。根据提示提供新的 root 密码 `LINUXrocks!` 并按 `Enter` 两次。
- 16. 在命令提示符下，输入 `poweroff` 并按 `Enter` 关闭你的 Fedora Linux 虚拟机。

## 项目 6-7

在这个动手项目中，你将在 Windows 电脑虚拟机内安装 Ubuntu Server 14.04 LTS Linux，并在之后检查 LVM 分区配置。

- 1. 在你的虚拟化软件中，创建一个名为 "Ubuntu Server 14" 的新虚拟机，具有以下特征：
   a. 2GB 内存
   b. 通过电脑的网卡连接互联网
   c. 一个 50GB 的 SATA/SCSI/SAS 虚拟硬盘
   d. 虚拟机的 DVD 驱动器已挂载了 Ubuntu Server 14.04 安装介质的 ISO 文件 `ubuntu-14.04.5-server-amd64.iso`
- 2. 使用你的虚拟化软件启动并连接到你的 Ubuntu Server 14 虚拟机。
- 3. 在语言界面上，确保选中了 `English` 并按 `Enter`。
- 4. 在 Ubuntu 欢迎界面上，检查选项。确保选中了 `Install Ubuntu Server` 并按 `Enter`。
- 5. 在选择语言页面，确保选中了 `English` 并按 `Enter`。
- 6. 在选择位置界面上，确保选中了 `United States` 并按 `Enter`。
- 7. 在配置键盘界面上，选择 `Yes` 并按 `Enter`。按照提示继续检测。当检测过程发现“us”键盘布局时，选择 `Continue` 并按 `Enter`。
- 8. 在配置网络界面上，输入主机名 `Ubuntu14`，选择 `Continue` 并按 `Enter`。
- 9. 在设置用户和密码页面，输入 `user1` 作为全名，选择 `Continue` 并按 `Enter`。在提示输入用户名时，确保选中了 `user1`，选择 `Continue` 并按 `Enter`。在提示为 user1 设置密码时，输入 `LINUXrocks!`，选择 `Continue`，再次并按 `Enter`。在提示加密 user1 的家目录时，确保选中了 `No` 并按 `Enter`。
- 10. 在配置时钟界面上，确保显示了正确的时区并按 `Enter`。
- 11. 在分区界面上，选择使用整个磁盘并设置 LVM，按 `Enter`。注意：将创建一个具有 ext4 文件系统的根卷和一个用于交换的卷。
- 12. 在摘要界面上，注意将使用卷组，选择 `Continue` 并按 `Enter` 开始安装核心包。
- 13. 在配置软件包界面上，可选选择你的代理地址，选择 `Continue` 并按 `Enter`。
- 14. 在配置任务界面上，确保选中了自动更新并按 `Enter`。
- 15. 在软件选择界面，使用空格键选择所有包，选择 `Continue` 并按 `Enter`。
- 16. 在配置 mysql-server-5.5 界面，提供密码 `LINUXrocks!`，选择 `Continue` 并按 `Enter`。在提示确认密码时，输入 `LINUXrocks!`，选择 `Continue` 并按 `Enter`。
- 17. 在 Postfix 配置界面，确保选择了 `Internet Site` 并按 `Enter`。在提示系统名称时，确保列出了 `Ubuntu14`，选择 `Continue` 并按 `Enter`。
- 18. 在配置 dovec-cert 界面，确保选中了 `Yes` 并按 `Enter` 创建 SSL 证书。在提示证书名称时，输入 `Ubuntu14`，选择 `Continue` 并按 `Enter`。
- 19. 在磁盘上的 GRUB 引导程序界面上，确保选中了 `Yes` 并按 `Enter`。
- 20. 在完成安装界面，确保选中了 `Continue` 并按 `Enter` 重启系统。
- 21. 系统启动后，以用户 user1 登录 tty1。在命令提示符下，输入 `who` 并按 `Enter`。
- 22. 在命令提示符下，输入 `sudo root` 并按 `Enter`。在提示时输入 user1 的密码 `LINUXrocks!` 并按 `Enter`。在提示输入 root 用户密码时，输入 `LINUXrocks!` 并按 `Enter`。通过 `who` 确认 root 用户。
- 23. 在命令提示符下，输入 `su - root` 并提供密码 `LINUXrocks!` 以切换到 root 用户。
- 24. 在命令提示符下，输入 `lsblk` 并按 `Enter`。检查输出。硬盘上创建 `/boot` 分区了吗？`/` 文件系统是由 LVM 管理的吗？
- 25. 在命令提示符下，输入 `fdisk -l` 并按 `Enter`。注意硬盘剩余部分是一个扩展分区 `/dev/sda2`，它包含一个专门供 LVM 使用的逻辑分区 `/dev/sda5`。
- 26. 在命令提示符下，输入 `lvdisplay` 并按 `Enter`。注意 Ubuntu14-vg 卷组中为根文件系统和交换分区创建的逻辑卷。
- 27. 在命令提示符下，输入 `poweroff` 并按 `Enter` 关闭你的 Ubuntu Server 14 虚拟机。

## 探索练习

- 1. 你已经在你的 Ubuntu Server 18 虚拟机上执行了项目 6-5。请使用你的 Fedora Linux 虚拟机执行相同的项目，并记录任何差异。
- 2. 现代 Linux 发行版通常允许你在安装期间创建具有容错能力的 BTRFS 卷，以用于托管 Linux 操作系统和应用程序。只要你的宿主机操作系统有足够的存储空间，创建一个名为 Fedora BTRFS 的新虚拟机，并具有以下特征：
   - a. 4GB 内存
   - b. 两个 50GB SATA/SCSI/SAS 硬盘
   - c. 虚拟机 DVD 驱动器已挂载到 Fedora 28 实时启动介质的 ISO 文件 `Fedora-Workstation-Live-x86_64-28-1.1.iso`

接下来，执行 Fedora Linux 安装，其中包含 `/` 文件系统使用 BTRFS RAID 1 容错机制，利用两个虚拟硬盘上的空间同时处理数据和元数据。为了在 Fedora 安装程序中配置此项，你需要在“安装目标”屏幕上选择“高级自定义”。还要注意，`/boot` 文件系统不能使用 BTRFS。安装完成后，使用相应的命令验证你的 BTRFS 配置。完成后，删除你的虚拟机和两个硬盘文件。
- 3. 对于操作系统和应用程序的容错，BTRFS RAID 1 的替代方案是软件 RAID 1。再次执行探索练习 2，但不要为 `/` 文件系统使用 BTRFS RAID 1 卷，而是选择适当选项创建一个格式化为 ext4 的软件 RAID 1 卷。
- 4. LVM 也可以为逻辑卷提供 RAID，前提是底层卷组由多个物理卷组成。查看 `lvraid` 手页以学习如何使用 `lcreate` 命令实现 LVM RAID 0 和 RAID 5。接下来，为你的 Fedora 虚拟机添加三个 10GB SATA/SCSI/SAS 虚拟硬盘，并将它们配置为单个 LVM RAID 5 逻辑卷。
- 5. 在互联网上搜索与本章描述的描述不同的 Linux 安装问题。其他人是如何解决这些问题的？如果你在安装过程中遇到类似的困难，该如何寻求帮助？
- 6. Linux 服务器通常存储在锁的机柜中以防止未经授权的人员物理访问。根据你在项目 6-6 中执行的步骤，描述为什么这些物理限制是合理的。

# 第 7 章
## 使用 BASH SHELL

在完成本章后，你将能够：

- 重定向命令的输入和输出
- 识别并操作常见的 shell 环境变量
- 创建并导出新的 shell 变量
- 编辑环境文件以便 shell 启动时创建变量
- 描述 shell 脚本的作用和性质
- 创建并执行基础 shell 脚本
- 在 shell脚本中有效使用结构、特殊变量和函数
- 使用 Git 对 shell脚本进行版本控制

对 shell 特性的良好理解对于必须每天与 shell 交互的管理员和用户至关重要。本章的第一部分描述了 shell 如何使用重定向和管道 shell 元字符来操纵命令的输入和输出。接下来，你将探索登录后 BASH shell 中不同类型的变量以及它们的用途和用法。之后，你将学习如何创建和执行 BASH shell 脚本。最后，本章介绍了如何使用 Git 为随时间修改的系统文件（如 shell 脚本）提供版本控制。

## 命令输入与输出

BASH shell 负责提供用户界面并解释在命令行输入的命令。此外，只要用户在命令行命令的同时指定了某些 shell 元字符，BASH shell 就可以操纵命令的输入和输出。命令的输入和输出由称为文件描述符的标签表示。对于可以被 BASH shell 操纵的命令，都有三个描述符：

- 标准输入 `stdin`
- 标准输出 `stdout`
- 标准错误 `stderr`

标准输入 `stdin` 指命令在执行期间处理的信息；这通常以用户在键盘上输入的输入形式存在。标准输出 `stdout` 指命令的正常输出，而标准错误 `stderr` 指命令生成的任何错误信息。`stdin` 和 `stderr` 默认显示在终端屏幕上。所有三个组件如图 7-1 所示。

虽然三个描述符对任何命令都可用，但并不是所有命令都使用每个描述符。图 7-1 中的 `ls /etc/hosts /etc/h` 命令向终端提供了状态和 stderr，如下：
