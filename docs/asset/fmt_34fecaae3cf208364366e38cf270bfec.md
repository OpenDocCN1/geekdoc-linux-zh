
`echo nameserver 192.168.0.6 >> /etc/resolv.conf`

注意，这里使用的地址都是私有 IP 地址。如果你正在配置公网服务器，你需要分配公网 IP 地址，或者使用某种从公网 IP 地址到防火墙/路由器后机器的端口转发。

### 2. 在 USB 闪盘上创建 DSL
将你准备好擦除并用于 Web 服务器的 USB 闪盘插入电脑的 USB 端口（不要挂载它）。接下来，从桌面的 DSL 菜单中选择 Apps、Tools、Install to USB Pendrive。然后，选择 For USB-ZIP Pendrive（如果你预计在旧款 PC 上运行服务器）或 For USB-HDD Pendrive（在较新的 PC 上运行服务器）。

此过程将擦除 DSL 驱动器上的所有内容！请确保你已经从驱动器中删除了所有内容。按照提示回答问题（有关将 DSL 安装到优盘的详情，请参见第 6 章“运行原生优盘安装”）。

### 3. 选择要备份的文件/目录
你需要列出的 DSL 备份文件和目录应位于 `/home/ds1/.filetool.1st` 文件中。服务器条目已在该文件中。使用任何文本编辑器打开该文件，并添加此处所示加粗的最后几行：

```text
opt/ppp
opt/bootlocal.sh
opt/powerdown.sh
opt/.dslrc
opt/.mydsl_dir
opt/lampp/
opt/rc.firewall
```

### 4. 备份文件和目录
要将你刚刚在 `.filetool.1list` 文件中添加的文件备份到 USB 闪盘，请从桌面选择 DSLpanel、Backup/Restore。系统会提示你输入要备份文件的设备。获取正确的设备至关重要。

对于没有其他 SCSI 或 SATA 驱动器的系统，USB 闪盘设备可能是 `sda1`（对于 USB-HDD 驱动器）或 `sda2`（对于 USB-ZIP 驱动器）。在输入设备名后，选择 Backup。

结果是在你输入的 USB 设备根目录下的一个 `tar.gz` 文件。

### 5. 保存 MyDSL 软件包
任何你恢复的 MyDSL 软件包也可以拷贝到 USB 闪盘中。如果你刚刚下载了它们，它们应该仍在 `/tmp` 目录中。

你将在重启 DSL 时获得机会拷贝 MyDSL 软件包。或者你可以手动拷贝它们。例如，你可以使用屏幕右下角的挂载工具挂载 USB 闪盘。然后，例如为了将此项目所需的文件拷贝到 `sda1` 上的 `mysql` 目录，你可以在终端窗口中输入以下命令：

```bash
# cd /tmp
# mkdir /mnt/sda1/mydsl/*
# cp gnu-utils* rcfirewall* /mnt/sda1/myd/
```

此时，你需要的所有内容都应该安装在你的 USB 闪盘上了。在添加网站内容之前，你的 XAMPP 安装为 DSL 需要 50MB 空间，XAMPP 以及我添加的其他软件包需要 61MB 空间。在 256MB 的 USB 闪盘上，这将留下...

# 336 官方 Damn Small Linux 教程

`boot: dsl nodhcp myds1-hdal=myd1 restore-hdal secure`

另一种重启 DSL 以包含存储在硬盘上的软件的方法（也见侧边栏中的描述）是，你可以在硬盘分区上创建一个持久的 `/opt` 目录。例如，如果你的持久性 `/opt` 目录位于第一个 IDE 硬盘的第二个分区上，你可以按照以下方式启动 DSL：

`boot: dsl nodhcp myds1-hdal=myd1 opt=hda2 secure`

如果你的电脑上有大量 RAM，你还可以考虑在启动提示符中添加 `toram` 选项。这有助于让你的丝滑的 XAMPP 服务器运行极快。

## 备份你的 XAMPP 服务器

XAMPP 服务提供了一项功能，让你安全地备份 XAMPP 数据库、配置文件、日志和内容（htdocs）文件。要执行此操作，如下所示运行带有备份选项的 `lampp` 命令：

```bash
# /opt/lampp/lampp backup mysecretpwd
正在备份数据库...
正在备份配置、日志和 htdocs 文件...
正在计算校验和...
正在构建最终备份文件...
备份完成。
```

确保 `/opt/lampp/xampp-backup-12-02-07.sh` 已复制到 `/opt/lampp/backup` 目录，你可以从中将其复制到备份介质。密码（此处显示为 `mysecretpwd`）是你 MySQL 服务器的 root 密码。

如果你的数据在任何时候损坏或销毁，可以通过运行该 shell 脚本来恢复备份存档。例如，使用前面的示例，你可以输入：

```bash
# sh /opt/lampp/xampp-backup-22-01-04.sh mysecretpwd
正在检查文件完整性...
正在恢复配置、日志和 htdocs 文件...
正在检查版本...
已安装：XAMPP 1.6
来自：XAMPP 1.6
正在恢复 MySQL 数据库...
正在恢复 MySQL 用户数据库...
备份完成。玩得开心！
```
