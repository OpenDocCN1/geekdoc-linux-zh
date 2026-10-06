

# 高级 Bash 脚本指南

模式 (1)，在多用户模式 (2 或 3) 下，在 X Windows (5) 下或重启时 (6)。此命令访问 /var/run/utmp 文件。

halt, shutdown, reboot

用于关闭系统的命令，通常在关机之前执行。

# 网络

## ifconfig

网络接口配置和调优工具。它最常用于启动时设置接口，或在重启时关闭接口。

```bash
# 摘自 /etc/rc.d/init.d/network 代码片段
#
# 检查网络是否已启动。
$ $(NETWORKING) = "no" && exit 0

 -x /sbin/ifconfig | exit 0

for i in $Interfaces; do
  if ifconfig $i 2>/dev/null | grep -q "UP" >/dev/null 2>&1; then
    action "Shutting down interface $i: /sbin/ifconfig"
    # grep 的 GNU 特有 "-q" 选项意味着“静默”，即不产生输出。
    # 因此，将输出重定向到 /dev/null 并不是绝对必要的。
  fi
done
```

```bash
echo "Currently active devices:"
echo /sbin/ifconfig | grep '[a-z]*' | awk '{print $1}'
# 以下方法同样有效。
echo $(sbin/ifconfig) | awk '/[a-z]*/ { print $1 }'
echo $(sbin/ifconfig) | sed -e 's/..*//
# 感谢 S.C. 的额外注释。
```

另见 [示例 3-5](#)。

# route

显示或修改内核路由表信息。

| bash$ route | 网关 | Genmask | Flags | MSS | Wtt | Inace |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| pm3-67.bosozisip | | 255.255.255.255 | UH | 40 | 0 | eth0 |
| 127.0.0.0 | | 255.0.0.0 | U | 40 | 0 | lo |
| default | | pm3-67.bosozisip | 0.0.0.0 | | 40 | 0 | eth0 |

# chkconfig

检查网络配置。此命令列出并管理 /etc/rc.d 中启动时启动的网络服务。

13. 系统和管理命令

chkconfig 原本是从 IRIX 移植到 Red Hat Linux 的，某些 Linux 发行版可能不是核心安装的一部分。

| bash$ chkconfig --list | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| atd | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| rwhod | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |

## tcpdump

网络数据包“嗅探器”。该工具通过转储符合特定标准的数据包头，来分析和排查网络流量。

转储主机 bozoville 和 caduceus 之间的包流量：

```bash
bash$ tcpdump ip host bozoville and caduceus
```

当然，tcpdump 的输出可以使用之前讨论过的某些文本处理工具进行解析。

# 文件系统

## mount

挂载文件系统，通常在外部设备上，如软盘或 CD-ROM。文件 /etc/fstab 提供了可用文件系统、分区和设备的列表，包括可能自动或手动挂载的选项。/etc/mtab 文件显示当前已挂载的文件系统和分区（包括虚拟分区，如 /proc）。

mount -a 挂载 /etc/fstab 中列出的所有文件系统和分区，但带有 auto 选项的除外。在启动时，/etc/rc.d 中的启动脚本（rcsysinit 或类似脚本）会调用此命令以完成所有挂载。

```bash
mount -t iso9660 /dev/cdrom /mnt/cdrom
# 挂载 CD-ROM
/mnt/cdrom
# 快捷方式，如果 /mnt/cdrom 已在 /etc/fstab 中
```

这个多功能命令可以在块设备上创建一个普通条，该文件将表现像文件系统一样。mount 配合回环设备对该文件进行组装。其应用之一是在将 ISO9660 镜像刻录到 CDR 之前，对其进行挂载和检查。[40]

# 示例 13–5。检查 CD 镜像

```bash
# 作为 root 用户...
# 准备挂载点，如果尚不存在。
mdir -r -t iso9660 -o loop cd-image.iso /mnt/cdtest # 挂载镜像
# -o loop "loop" 选项等于 "losetup /dev/loop0"
cd /mnt/cdtest # 现在检查镜像。
```

第 13 章 系统和管理命令

```bash
ls -alR               # 列出该目录树中的文件。
                      # 以此类推。
```

卸载当前挂载的文件系统。在物理移除之前挂载的软盘或 CD-ROM 驱动器之前，必须先卸载设备，否则可能会发生文件系统损坏。

```bash
umount /mnt/cdrom
# 现在你可以可以操作了。
```

