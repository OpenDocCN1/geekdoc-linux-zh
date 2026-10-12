
### 30. 添加内核模块
添加任何你需要在启动时添加的额外内核模块。你通常只有在某些硬件没有被检测到且所需的模块没有自动加载时才需要这样做。编辑`kernel-2.4`或`kernel-2.6`文件，取决于你使用的是哪个内核。

```
nano -w /etc/modules.autoload/kernel-<version>
```

你可以输入`uname -a`查看你的内核版本是什么。

### 31. 配置引导加载程序
你需要安装并配置引导加载程序（在本例中为`grub`）。它对你的设置做出了以下假设：

- Gentoo 安装在你的第一块 IDE 磁盘（`/dev/hda`）上。
- 你在`/dev/hd1`上有一个独立的启动分区。
- 你`/boot`目录下的`initrd`文件是`initrd-2.4.26-gentoo9`。
- 你`/boot`目录下的内核文件是`kernel-2.4.26-gentoo-r9`。

如果你的设置与上述任何信息有所不同，你需要适当地调整以下步骤。要配置`grub`，请用`emerge`安装它，运行`grub`命令，并如下所示创建`grub.conf`文件：

```
# emerge grub

# grub

gub> root (hd0,0)
gub> setup (hd0)
gub> quit

# nano -w /boot/grub/grub.conf

default 0
timeout 15
splash=(hd0,0)/grub/splash.gz

title=Gentoo Linux
root (hd0,0)
kernel /kernel-2.6.13-gentoo-r3 root=/dev/hd0
initrd /initrd-2.6.13-gentoo-r3
```

### 32. 重启
通过运行`umount`卸载分区并退出 root 分区，按如下方式重启：

```
# exit; cd /
# umount /mnt/gentoo/proc /mnt/gentoo
# reboot
```

移除安装盘并允许电脑从硬盘启动。几个月后，你应该能看到`GRUB`启动界面。选择`Gentoo Linux`（按回车）。

从这里开始你将从硬盘启动并直接在操作系统运行。如果你遇到错误，例如缺少内核驱动，我建议你访问`http://forums.gentoo.com`并搜索导致问题的驱动。很有可能其他人遇到过相同的问题并能为你提供解决方案。

![](img/a123b4f2456cac935474ae2401b95b01_428_0.png)

### 33. 安装桌面
对于我们大多数人来说，在命令行工作并不好玩。以下命令安装了一套基础桌面包，包括`X Window`系统（`xfree`）、`KDE`桌面（`kde`）、`Mozilla`浏览器（`mozilla`）和`Openoffice`办公套件（`openoffice-bin`）。在网络上安装这些需要很长的时间！

```
# emerge xfree kde mozilla openoffice-bin
```

作为替代，如果你在`CD-ROM`上有这些包，可以使用以下命令来识别包的位置并安装它们：

```
export PKGDIR="/mnt/cdrom"
# emerge -k xfree kde mozilla openoffice-bin
```

如果你只想安装`X Window`系统，也可以通过只安装它来节省时间：

```
# emerge only xfree
```

### 34. 配置 X 服务器
现在你的`X Window`系统已安装，你需要配置显卡以正常工作。输入以下命令来配置`X`：

```
# nano /etc/X11/xorg.conf
```
