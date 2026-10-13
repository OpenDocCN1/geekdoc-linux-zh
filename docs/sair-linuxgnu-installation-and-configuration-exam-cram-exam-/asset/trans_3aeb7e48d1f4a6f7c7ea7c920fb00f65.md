
## 问题 8

你有以下网络地址：192.168.33.0。你使用网络掩码 255.255.255.0。网关地址是 192.168.33.1。以下哪个是可分配给网络上计算机的 IP 地址范围？

- a. 192.168.33.0 到 192.168.33.255
- b. 192.168.33.1 到 192.168.33.254
- c. 192.168.33.2 到 192.168.33.255
- d. 192.168.33.2 到 192.168.33.254

## 问题 9

你有一台较旧的计算机想要转换为 Linux，其中包含一台通过声卡连接到计算机的老式 CD-ROM。在 Linux 中安装该 CD-ROM 需要什么驱动程序？

- a. 声卡驱动程序
- b. 声卡驱动程序和 CD-ROM 驱动程序
- c. 更新的 CD-ROM 驱动程序
- d. 一个同时适用于声卡和 CD-ROM 的组合驱动程序

## 问题 10

你想将运行级别更改为单用户模式。以下哪种步骤应采取以进入该模式？

- a. 运行 init S 命令。
- b. 检查你的 /etc/inittab 文件以找到与单用户模式关联的运行级别。使用与单用户模式关联的数字或字母运行 init 命令。
- c. 检查你的 /etc/inittab 文件以找到与单用户模式关联的运行级别。进入 root 或超级用户模式。使用与单用户模式关联的数字或字母运行 init 命令。
- d. 进入 root 或超级用户模式。运行 init 1 命令。

## 问题 11

你在网关计算机上设置 Linux，因此需要安装两块网卡。当你启动 Linux 时，它只能识别位于内存地址 0x320 的其中一块卡。该卡已被分配给设备 eth0。你可以做什么让 Linux 识别另一块卡？假设你知道 IRQ 12 和内存地址 0x280 可用。

- a. 在你的 /etc/lilo.conf 文件中输入以下命令：append="ether=12,0x280,eth1"
- b. 在 LILO 启动提示符处输入以下命令：append="ether=12,0x280,eth1"
- c. 在你的 /etc/lilo.conf 文件中输入以下命令：append="ether=12,0x320,eth1"
- d. 在 LILO 启动提示符处输入以下命令：eth1=12,0x320

## 问题 12

你已作为用户 rt 登录。你有挂载 CD-ROM 驱动器的适当权限。为此目的你创建了一个名为 cdrom 的子目录。如果你运行 mount /dev/cdrom cdrom 命令，你会在哪里找到 CD 上的文件？你仍在 rt 的主目录中。

- a. /home/cdrom
- b. /home/rt/cdrom
- c. /cdrom
- d. /mnt/cdrom

## 问题 13

你运行 ps 命令并得到以下输出：

```
PID TTY TIME CMD
682 tty1 00:00:00 bash
983 ttyp2 00:00:00 bash
1235 tty4 00:00:00 ps
```

其中哪个进程是由远程登录的用户运行的？

- a. PID 682
- b. PID 983
- c. PID 1235
- d. 以上都不是

## 问题 14

以下哪个命令允许你启动图形用户界面登录屏幕？

- a. startx
- b. X
- c. xdm
- d. XF86Setup

## 问题 15

以下哪个答案会影响你为 X Window 设置的分辨率？

- a. 计算机上的 RAM。
- b. 显示器中的内存。
- c. 分辨率受显示器中的内存和视频控制器上的内存组合限制。
- d. 视频控制器上的内存。

## 问题 16

你创建了一个名为 Live Again Shell（lash）的新 shell。你将与该 shell 相关的文件安装在你的主目录的 bin/lash 子目录中。你的用户名是 la。你将如何设置其他用户默认进入你的 shell？

- a. 打开 /etc/passwd 文件。导航到包含所需用户登录信息的行。用 /a/lash 替换最后一列显示的目录。
- b. 打开 /etc/passwd 文件。导航到包含所需用户登录信息的行。用 /bin/lash 替换最后一列显示的目录。
- c. 打开 /etc/passwd 文件。导航到包含所需用户登录信息的行。用 /home/bin/lash 替换最后一列显示的目录。
- d. 打开 /etc/passwd 文件。导航到包含所需用户登录信息的行。用 /home/la/bin/lash 替换最后一列显示的目录。

## 问题 17

以下哪项是 Linux 中数据的三个标准通道？

- a. stdin, stdrel, stderr
- b. stdent, stdout, stdlog
- c. stdin, stdout, stderr
- d. stdent, stdex, stderr

## 问题 18

以下哪个命令会删除 /usr/sbin/WordProcessor 目录中的所有文件和目录？假设有大量文件，但只有一个 /usr/sbin/WordProcessor/docs 子目录，并且你不想在每次删除前被提示。假设你已在 /usr/sbin 目录中。

- a. rm -i WordProcessor
- b. rmdir -p WordProcessor/docs
- c. rm -r WordProcessor
- d. rmdir -r WordProcessor

## 问题 19

你在 X Window 中打开了两个屏幕。你有一个双按钮鼠标。你已从一个屏幕中突出显示了文本并想将其复制到第二个屏幕。你如何复制文本？

- a. 将光标移动到所需位置并按下鼠标中键。
- b. 将光标移动到所需位置并同时按下两个鼠标按钮。
- c. 将光标移动到所需位置并右键单击。当弹出菜单出现时，单击粘贴。
- d. 你不能在 Linux 中使用鼠标复制和粘贴文本。

## 问题 20

假设有大量用户同时登录。以下哪个命令可用于识别用户 jsmith 登录的次数？

- a. who | grep jsmith
- b. who | grep jsmith | wc -l
- c. who | sed jsmith
- d. who | grep jsmith > logins

## 问题 21

你需要有关配置文件更多信息。以下哪对实用程序可以帮助你找到所需的信息？[勾选所有正确答案]

- a. man, xinfo
- b. tk info, info
- c. man --help, xinfo
- d. info, xinfo

## 问题 22

以下哪些是标记语言？[勾选所有正确答案]

- a. TeX
- b. emacs
- c. nroff
- d. HTML

## 问题 23

你在 /etc/profile 文件中设置了一系列 shell 变量。你希望其中一些变量在你仍登录时适用于其他 shell。以下哪个命令将变量从一个 shell 应用到另一个 shell？

- a. apply
- b. export
- c. move
- d. env

## 问题 24

你刚刚从 Linux 连接到 FTP 服务器。当你运行 mget . 命令时，什么类型的文件会被下载到你的计算机？

- a. 当前服务器目录中的所有隐藏文件
- b. 当前服务器目录中的所有文件
- c. 名称中包含点的所有文件，例如 example.txt
- d. 没有文件被下载

## 问题 25

你在启动 Linux 时遇到问题。当你打开计算机时，BIOS 检查内存和基本硬盘连接。然后你看到的就是以下内容：

```
LIL
```

以下哪个可能是问题？

- a. 你有损坏的 MBR。
- b. 你缺少二级引导加载程序，/boot/boot.b。
- c. 你的 vmlinuz 文件可能位于柱面 1023 以上。
- d. 有人未经你同意更改了你的 MBR。

## 问题 26

你在启动 Linux 时遇到问题。当你打开计算机时，BIOS 检查内存和基本硬盘连接，然后你的计算机似乎卡住了。假设你知道这是 MBR 的问题。你可以采取哪些步骤来恢复你的 MBR？[勾选所有正确答案]

- [ ] a. 使用 /sbin/lilo 命令将 /etc/lilo.conf 文件的内容发送到你的 MBR。
- [ ] b. 使用 MS-DOS 启动盘启动计算机，并运行 fdisk /mbr 命令。
- [ ] c. 使用 Linux 启动盘启动计算机，并在 LILO 启动提示符处输入 linux single 命令。
- [ ] d. 使用你的 Linux 安装 CD 启动计算机。如果可用，输入救援模式。
