
| COMMAND | PID | USER | FD | TYPE | SIZE | NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bash | 2337 | root | cwd | DIR | 22,1 | 2 | /opt/backup |
| lsof | 4815 | root | cwd | DIR | 22,1 | 2 | /opt/backup |
| lsof | 4816 | root | cwd | DIR | 22,1 | 2 | /opt/backup |

你可以联系用户，也可以自己终止任何打开的连接。

## 杀死打开的连接

步骤 6. 为了杀死打开的连接，你可以再次使用 `fuser` 命令：

```bash
# fuser -ck /opt/backup
```

## 卸载文件系统

步骤 7. 现在你应该能够卸载文件系统了：

```bash
# umount /opt/backup
```

**警告：** 通过杀死所有打开的连接，你实际上终止了用户打开的所有内容。如果他们正在处理未保存的内容（例如 Word 或 PowerPoint 文档），所有更改都会丢失。良好的做法是在进行文件系统维护时向用户发送通知提醒他们；这样他们就可以提前保存并关闭所有文档。

现在你已经知道如何卸载文件系统，但还有其他事情你需要查看。如果你现在重启系统，你刚刚挂载的所有文件系统在系统启动后将不再可用。为什么？`mount` 命令不是持久的，所以通过它挂载的任何内容在系统重启后都会失效。我想你想知道如何修复，对吧？系统会查看两个配置文件。一个处理启动过程中文件系统的挂载，另一个跟踪当前挂载的系统：

- `/etc/mtab`: 包含所有已挂载文件系统的列表
- `/etc/fstab`: 在启动时按给定的选项挂载所有列出的文件系统

让我们来看 `/etc/mtab` 文件。每当你挂载或卸载文件系统时，该文件都会更新，以始终反映当前挂载到系统。

### 查看 /etc/mtab

步骤 1. 查看 `/etc/mtab` 文件：

```bash
# cat /etc/mtab
```
/dev/mapper/vg_rhel01-lv_root / ext4 rw 0 0

/proc /proc rw 0 0

sysfs /sys rw,5,mode=620 0 0

devts /dev/pts devpts rw

tmpfs /dev/shm rw,rootcontext="system_u:object_r:tmpfs_t:s0"

0 0

/dev/sda11 /boot ext4 rw 0 0

none /proc/sys/fs/binfmt_misc binfmt_misc rw 0 0

sunspc /var/lib/nfs/rpc_ppefs rpc_ppefs rw 0 0

/dev/hdb1 /opt/company_data ext4 rw 0 0

/dev/hdc1 /opt/backup ext3 rw 0 0

步骤 2. 你可以使用 `grep` 命令查询检查特定的文件系统是否已挂载：

```bash
# cat /etc/mtab | grep backup
```
/dev/hdc1 /opt/backup ext3 rw 0 0

### 查看当前挂载

# 第 3 步。

因为你不想在每次查看挂载的文件系统时都搜索该文件，可以使用不带选项的 `mount` 命令来查看当前已挂载的所有文件系统：

```
# mount
```
/dev/vg_rhel01-lv_root on / type ext4 (rw)

proc on /proc type proc (rw)

sysfs on /sys type sysfs (rw)

devpts on /dev/pts type devpts (rw,gid=5,mode=620)

tmpfs on /dev/shm type tmpfs

(rw,rootcontext="system:u_object:tmpfs:t0:0")

/dev/sda1 on /boot type ext4 (rw)

none on /proc/sysfs/binfmt_misc type binfmt_misc (rw)

sunprpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)

/dev/hdb1 on /opt/company_data type ext4 (rw)

/dev/hdc1 on /opt/backup type ext3 (rw)

### /etc/fstab 语法

# 第 4 步。

检查 `/etc/fstab` 文件。该文件遵循以下语法：

```
<设备> <挂载点> <文件系统> <挂载选项>
<关机时写入数据> <检查顺序>
```

### 查看 /etc/fstab

# 第 5 步。

查看 `/etc/fstab`

```
# cat /etc/fstab
```
/dev/vg_rhel01-lv_root / ext4 defaults 1 1

UUID=5485df3d-7b48-42f1-b3d3-3d844c6560fb / ext4 defaults 1 2

/dev/vg_rhel01-lv_swap / swap defaults 0 0

tmpfs /dev/shm tmpfs defaults 0 0

devpts /dev/pts devpts gid=5,mode=620 0 0

sysfs /sys sysfs defaults 0 0

proc /proc proc defaults 0 0

前三个字段应该显而易见，因为你在整个章节中一直在操作它们。不过，后三个字段需要一些解释。第四个字段定义了用于挂载文件系统的选项。你已经看到 `defaults` 默认选项实际上包含了许多针对文件系统的不同选项。以下是可用选项的完整列表：

```
rw      将文件系统挂载为读/写
suid 允许运行设置和设置组 ID
dev     解释文件系统上的设备
```

```
exec 允许执行二进制文件
auto 当指定了 -a 选项时挂载文件系统
ouser 不允许任何普通用户（卸）挂载文件系统
async 允许所有文件系统 I/O 异步发生
```

第五个字段定义了在关机或重启之前是否应该备份数据（也称为转储）。该字段通常使用值 1。如果文件系统是用于文件的临时存储空间（如 `/tmp/`），则可以使用值 0。最后一个字段定义了文件系统检查的顺序。对于根文件系统，值应为 1；其他所有项应为 2。如果你有可移动文件系统（如 CD-ROM 或外部硬盘），你可以定义值为 0 并完全跳过检查。由于你希望之前创建的两个文件系统在系统启动时挂载，你可以为它们添加两个定义。

- 第 6 步。打开 `/etc/fstab` 文件进行编辑：

```
# nano /etc/fstab
```

- 第 7 步。为 `/dev/hdc1` 文件系统添加以下行：
`/dev/hdc1 /opt/backup ext3 defaults 0 0`

在编辑此文件时，你还应该定义交换分区文件系统（你认为我没有忘记那个吧？）。你有一个分区和一个交换文件。交换文件的顺序很重要，因为它指示了系统本身使用设备的顺序。

- 第 8 步。为交换分区添加以下行：
`/dev/hdc2 swap defaults 0 0`

现在你可以保存文件并退出。你不需要重启即可测试！

- 第 9 步。你可以使用带有 `-a` 选项的 `mount` 命令重新挂载 `/etc/fstab` 文件中定义的所有文件系统：

```
# mount -a
```

现在你的所有文件系统都应该已经挂载并可以可以使用。

> 注意：虽然我们讨论了许多关于磁盘驱动器的文件系统，但 `mount` 命令也可以用于挂载其他类型的文件系统。例如，你通常会在根分区之外有一个 `/media` 目录，通常用于挂载 CD/DVD-ROM 驱动器。你可以使用带有 `-o` 选项的 `mount` 命令。将 `/dev/cd-rom` 设备挂载到 `/media` 目录：

```
# mount -o loop /dev/cd-rom /media
```

## 额外的文件系统命令

你需要定期对文件系统进行维护，以确保可靠性和最佳性能。通常，对于任何维护目的，你通过卸载文件系统来使其离线。假设你的老板刚刚告诉你，你需要在周末对 `/dev/hdb1` 文件系统进行维护。

- 第 1 步。将你的文件系统下线：

```
# unmount /dev/hdb1
```

现在让我们来看一些维护任务。以下是你可以使用维护命令：

| 命令 | 描述 |
| :--- | :--- |
| blkid | 显示文件系统属性 |
| df | 显示文件系统使用情况 |
| e2fsck | 检查文件系统 |
| e2label | 修改文件系统标签 |
| find | 允许查找文件系统 |
| resize2fs | 调整文件系统大小 |
| tune2fs | 调整文件系统参数 |

首先，你需要对系统标记。

- 第 2 步。使用：

```
# e2fsck -f /dev/vg_group01/lvol0
```

- 第 3 步。如果你有剩余空间：

```
# resize2fs /dev/vg_group01/lvol0
```

第 10 步。现在维护工作已完成，请重新挂载文件系统：

第 11 步。你可以使用该命令验证是否挂载成功：

```bash
# mount LABEL=CData /opt/company_data
```
/dev/mapper/vg_rhel01-lv_root on / type ext4 (rw)

proc on /proc type proc (rw)

sys on /dev/sys type sysfs (rw)

devpts on /dev/devpts type devpts (rw,gid=5,mode=620)

tmpfs on /dev/shm type tmpfs

/dev/hda1 /boot type ext4 (rw)

none on /dev/sys/fs/binfmt_misc type binfmt_misc (rw)

sunprpc on /var/lib/nfs/rpc_pipefs rpc_pipefs (rw)

/dev/hdc1 /opt/backup type ext3 (rw)

/dev/hdb1 /opt/company_data type ext4 (rw)

你也可以使用 `df` 命令来获取文件系统的使用信息。这应该也会反映出你刚刚为 CData 文件系统添加的空间。

语法：`df [options]`

选项：

- - h 指定人类可读的格式
- l 仅指示本地文件系统
- - T 打印文件系统类型

第 12 步。检查你还有多少可用剩余空间：

```bash
# df -h
```
| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/mapper/vg_rhel01-lv_root | 16G | 2G | 13G | 16% | /dev/shm |
| tmpfs | 1004M | 0 | 1004M | 0% | / |
| /dev/hda1 | 485M | 30M | 430M | 7% | /boot |
| /dev/hdc1 | 4.0G | 13.7M | 3.7G | 4% | /opt/backup |
| /dev/hdb1 | 7.9G | 146M | 7.4G | 2% | /opt/company_data |

## 使用 LUKS 进行加密

Linux 统一密钥设置（Unified Key Setup, LUKS）是一种用于 Linux 的磁盘加密。LUKS 使用块设备加密，可以在系统关闭时保护系统（特别是当硬盘被移除或被盗时）。在首次安装 RHEL6 时，你会进入分区创建界面，在那里你也可以选择对分区使用加密。如果你选择了此选项，会被要求输入密码。每次系统启动时，系统都会提示你输入此密码以解密分区供系统使用。

> 警告：不要丢失此密码！如果丢失了，你加密的任何内容将完全无法访问。

仅仅因为你的分区使用 LUKS 加密，并不意味着它们在系统开启时受到保护。LUKS 仅在系统关闭时保护你的系统（如果分区没有在单用户模式下挂载）。当系统启动且分区由 LUKS 解密后（为了能够访问数据必须这样做），你可以将文件级加密与 LUKS 结合使用，在系统运行时提供额外的安全性。在本章稍后部分中，我们将讨论 GnuPG，这是一种使用 PGP 的开源文件级加密。

### 创建加密分区

即使在安装了 Red Hat 后，你仍然可以创建加密分区。默认情况下，RHEL 使用 128 位 AES 加密和 256-SHA 哈希算法。还有其他加密算法：

- AES
- Twofish
- Serpent
- Cast5
- Cast6

本节介绍了在系统安装并启动后如何对分区加密。作为示例，我在 RHEL02 上创建了一个大小为 4GB 的新虚拟硬盘（`/dev/hdb1`）。

> 警告：创建加密分区会擦除分区上的所有数据。在继续之前，请确保已备份了任何数据。

- 第 1 步。在 RHEL02 上，你需要引导到运行级别 1 以创建加密分区（类似于执行文件系统维护）：
  `# telinit 1`

- 第 2 步。系统启动后，确保该分区未被挂载：
  `# umount /dev/hdb1`

- 第 3 步。
  验证分区确实已卸载：
  `# mount | grep /dev/hdb1`

- 第 4 步。
  用随机数据填充你的分区；这可能需要很长时间才能完成：
  `# dd if=/dev/random of=/dev/hdb1`

- 第 5 步。
  随机数据写入完成后，你需要初始化分区：
  `# cryptsetup -verbose -verify-passphrase luksFormat /dev/hdb1`

  警告！
  =======
  这将不可撤回地覆盖 `/dev/hdb1` 上的数据。

  你确定吗？（输入大写的 yes）：YES
  输入 LUKS 密码：
  验证口语：
  命令执行成功。

- 第 6 步。
  打开新加密的设备并为其命名（示例中为 opt_data）：
  `# cryptsetup luksOpen /dev/hdb1 opt_data`
  输入 `/dev/hdb1` 的密码：

- 第 7 步。
  验证加密分区是否存在：
  `# ls -l /mapper | grep opt_data`
  `lrwx------ 1 root root 7 Jan 27 18:36 opt_data -> ../opt_data`

- 第 8 步。
  创建一个新文件系统：
  `# mkfs.ext4 /dev/mapper/opt_data`

- 第 9 步。
  创建完成后，你需要挂载它：
  `# mount /dev/mapper/opt_data`

- 第 10 步。现在维护完成后，重新挂载文件系统：
  `# mount /opt_data`

- 第 11 步。
  你可以使用该命令验证是否挂载成功：
  `# mount LABEL=CData /opt_data`
  /dev/mapper/vg_rhel01-lv_root on / type ext4 (rw)
  proc on /proc type proc (rw)
  sys on /dev/sys type sysfs (rw)
  devpts on /dev/devpts type devpts (rw,gid=5,mode=620)
  tmpfs on /dev/shm type tmpfs
  /dev/hda1 /boot type ext4 (rw)
  none on /dev/sys/fs/binfmt_misc type binfmt_misc (rw)
  sunprpc on /var/lib/nfs/rpc_pipefs rpc_pipefs (rw)
  /dev/hdc1 /opt/backup type ext3 (rw)
  /dev/hdb1 /opt/company_data type ext4 (rw)

你也可以使用 `df` 命令来获取文件系统的使用信息。这应该也会反映出你刚刚为 CData 文件系统添加的空间。

语法：`df [options]`

选项：

- - h 指定人类可读的格式
- l 仅指示本地文件系统
- - T 打印文件系统类型

第 12 步。检查你还有多少可用剩余空间：

```bash
# df -h
```
| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/mapper/vg_rhel01-lv_root | 16G | 2G | 13G | 16% | /dev/shm |
| tmpfs | 1004M | 0 | 1004M | 0% | / |
| /dev/hda1 | 485M | 30M | 430M | 7% | /boot |
| /dev/hdc1 | 4.0G | 13.7M | 3.7G | 4% | /opt/backup |
| /dev/hdb1 | 7.9G | 146M | 7.4G | 2% | /opt/company_data |
