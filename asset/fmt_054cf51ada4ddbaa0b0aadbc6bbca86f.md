
如果你的文件系统已挂载，且你想让你的系统成为根分区，请使用命令 `chroot /mnt/sysimage`。当你需要运行如 `rpm` 这种要求根分区挂载为 `/` 的命令时，这非常有用。要退出 `chroot` 环境，输入 `exit` 返回到提示符。

## 在救援模式下运行的命令

在 `bash` 下，你可以运行许多有用的命令，包括以下命令：

| anaconda | gzip | mkfs.ext2 | probe |
| badblocks | head | mkknod | ps |
| bash | hwclock | mkraid | python2.2 |
| cat | ifconfig | mkswap | raidstart |
| chatter | init | label | raidstop |
| chmod | mmd | rcp |
| chroot | less | mount | login |
| clock | ln | move | rm |
| collage | loader | modprobe | rmmod |
| cp | ls | mount | route |
| cpio | lsattr | mpartition | rpm |
| dd | lsmod | mrd | rsh |
| ddcprobe | mattrib | mread | sed |
| depmode | mbadlocks | mren | sh |
| df | mcd | mehowfat | sync |
| e2fsck | mcopy | mt | tac |
| fdisk | mdel | mtools | tail |
| fsck | mdeltree | mtype | tar |
| fsck.ext2 | mdir | mv | touch |
| fsck.ext3 | mdu | mzip | traceroute |
| ftp | mformat | open | umcount |
| gnome-pty-helper | minfo | parted | uncpio |
| grep | mdir | pico | uniq |
| gunzip | mke2fs | ping | zat |

## 启动单用户模式

你可能可以直接启动单用户模式。如果你的系统启动但在启动完成后不允许你登录，请尝试单用户模式。

## 在 GRUB 中进入单用户模式

如果你正在使用 GRUB，使用以下步骤进入单用户模式：

- 1. 如果你配置了 GRUB 分区，输入 `p` 并输入密码。
- 2. 选择你想要启动的版本的 Red Hat Linux 并输入 `e` 进行编辑。你将看到所选标题的配置文件列表。
- 3. 选择以 `kernel` 开头的行并输入 `e` 编辑该行。
- 4. 转到行末尾并输入 `single`。
- 5. 回到 GRUB 界面，输入 `b` 进入单用户模式。

## 在 LILO 中启动单用户模式

如果你使用 LILO，在 LILO 提示符处指定以下选项之一：

```
boot: linux single

boot: linux emergency
```
