
类似的规则在设备移除时进行清理：

```
ACTION=="remove", ATTRS{model}=="USB2FlashStorage", KERNEL=="sd[a-z]1", RUN+="/bin/umount -l /mnt/ate-flash?\n" ACTION=="remove", ATTRS{model}=="USB2FlashStorage", KERNEL=="sd[a-z]1", RUN+="/bin/rmdir /mnt/ate-flash?\n"
```

现在我们的规则已经就位，必须通知udevd我们所做的更改。udevadm的control命令是少数需要root权限的命令之一。

```
ubuntu$ sudo udevadm control --reload-rules
```

重新加载后，拼写错误会被静默忽略，即使使用`--debug`标志也是如此，所以务必仔细检查规则的语法。

就是这样！现在当闪存驱动器插入USB端口时，udevd会创建一个名为/dev/ate-flash1的符号链接，并将驱动器挂载为/mnt/ate-flash1。

```
ubuntu$ ls -l /dev/ate*
 lrwxrwxrwx 1 root root 4 2009-08-09 21:22 /dev/ate-flash1 -> sdb1
```

```
ubuntu$ mount | grep ate
 /dev/sdb1 on /mnt/ate-flash1 type vfat (rw)
```

## 13.9 推荐阅读

BOVET, DANIEL P. 和 MARCO CESATI。《理解Linux内核》（第3版）。Sebastopol, CA: O’Reilly Media, 2006.

CORBET, JONATHAN 等。《Linux设备驱动程序》（第3版）。Sebastopol, CA: O’Reilly Media, 2005. 本书也可在线获取：lwn.net/Kernel/LDD3.

LOVE, ROBERT。《Linux内核开发》（第2版）。Indianapolis, IN: Novell Press, 2005.

McDOUGALL, RICHARD 和 JIM MAURO。《Solaris内幕：Solaris 10和OpenSolaris内核架构》（第2版）。Upper Saddle River, NJ: Prentice Hall PTR, 2006.

## 13.10 练习

E13.1 描述内核的功能。解释将驱动程序作为模块加载与将其静态链接到内核之间的区别。

E13.2 某HP-UX系统上的一个进程崩溃并报告了一条令人费解的错误：“打开的文件太多：文件权限拒绝服务器访问。”这条错误可能是什么原因造成的？需要做出什么更改才能解决根本问题？

★ E13.3 AIX系统是否提供可加载内核模块？开发人员如何为AIX内核添加对新文件系统或新系统调用的支持？在什么情况下可能需要这种功能？

★ E13.4 在当地跳蚤市场，你以极低的价格买到一张通过并行端口提供以太网连接的笔记本电脑卡。要使Linux识别这张新卡，你需要执行哪些步骤？你应该将支持直接编译进内核，还是作为模块添加？为什么？（附加问题：如果你的时薪为80美元，估算让这个廉价以太网接口工作所需的劳动价值。）

★★ E13.5 在实验室中，使用xconfig或menuconfig配置Linux内核并构建内核二进制文件。安装并运行新系统。提交旧内核和新内核的dmesg输出，并突出显示差异。（需要root权限。）

## 第二部分
网络

![](img/14d78e3cecac4581d37024baf1e94cca_493_0.png)

此页有意留空

## 14 TCP/IP网络

![](img/14d78e3cecac4581d37024baf1e94cca_495_0.png)

无论怎样强调网络对现代计算的重要性都不为过，尽管这似乎并不能阻止人们试图这样做。在许多场所——也许是大多数——网页和电子邮件访问是计算机的主要用途。截至2010年，internetworldstats.com估计互联网拥有近15亿用户，占世界人口的21%以上。在北美，互联网普及率接近75%。

TCP/IP是支撑互联网的网络系统。TCP/IP不依赖于任何特定的硬件或操作系统，因此使用TCP/IP的设备尽管存在诸多差异，却都能交换数据（“互操作”）。

TCP/IP适用于任何规模或拓扑的网络，无论这些网络是否连接到外部世界。本章将在互联网的政治和技术背景下介绍TCP/IP协议，但独立网络在TCP/IP层面也是相当类似的。

## 14.1 TCP/IP及其与互联网的关系

TCP/IP和互联网有着共同的历史，可以追溯到几十年前。互联网的技术成功主要归功于优雅而灵活的设计。
