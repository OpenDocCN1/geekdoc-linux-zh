
8. 图像压缩是否影响了质量？你可以通过图形查看程序查看两个图像。输入 `gqview`。GQView 程序如图 13-1 所示。

![](img/3bd24ceeed5983554c0123729814a2d6_219_1.png)

## 实验 13.4 安装与卸载软件包

### 目标
大多数 Linux 发行版使用红帽包管理器（RPM）来安装和卸载软件。在本实验中，你将：
- 显示所有已安装的软件包
- 从 CD-ROM 安装软件包
- 卸载软件包

### 所需材料
本实验需要以下材料：
- 运行 Linux 的计算机的 root 用户权限
- Red Hat Linux CD-ROM

### 活动步骤
1. 按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并以 root 用户身份登录终端。
2. 要查看计算机上安装的所有软件包列表，输入 `rpm -qa`。你会看到安装了许多软件包，其中大多数在屏幕上快速滚动。请注意，它们并不是按字母顺序排列的。若要按字母排序并逐页显示，请输入 `rpm -qa|sort|more`。向下滚动列表，注意这里没有名为 zebra 的包。
3. 将第3 号 Red Hat Linux CD-ROM 插入 CD-ROM 驱动器。输入 `mount /dev/cdrom` 挂载 CD-ROM。输入 `cd /mnt/cdrom/RedHat/RPMS` 进入 RPMS 目录。
4. 输入 `rpm -i zebra*` 查找 zebra 包的完整名称。它的名为 `zebra-092a-3.i386.rpm`。
5. 输入 `rpm -i zebra*` 安装 zebra 包。由于没有名称冲突，你可以使用通配符代替输入整个名称。或者，你也可以使用之前章节中描述的 Tab 键自动补全。
6. 输入 `rpm -qp zebra-092a-3` 可以看到 zebra 包现已安装。
   `zebra-092a-3`
7. 输入 `rpm -qi zebra-092a-3` 获取该包的信息。遗憾的是，在此处不能使用通配符。

| 软件包 (Name) | 重定位次数: (不可重定位) |
| :--- | :--- |
| 名称 (Name): zebra | 版本 (Version): 0.92a |
| 供应商 (Vendor): Red Hat, Inc. | 发布版本 (Release): 3 |
| 构建日期 (Build Date): Wed 2003年4月10日 下午02:58:03 PDT | 安装日期 (Install Date): Sat 2003年12月12日 下午07:17:25 PS |
| 构建主机 (Build Host): stripples.devel.net | 许可证 (License): GPL |
| 分组 (Group): System Environment/Daemons | 源 RPM (Source RPM): zebra-092a-3.src.rpm |
| 大小 (Size): 3306444 | |
| 打包器 (Packager): Red Hat, Inc <http://bugzilla.redhat.com/bugzilla> | |
|  URL: http://www.zebra.org/ | |
| 摘要 (Summary): 路由守护进程 (Routing daemon) | |

**描述 (Description):**
GNU Zebra 是一项免费软件，用于管理基于 TCP/IP 的路由协议。它采用多服务器和多线程的方法来解决当前互联网的复杂性。GNU Zebra 支持 BGP4、BGP4+、OSPF2、OSPF3、RIPv1、RIPv2 和 RIPpng。

8. 现在使用 `-e` (erase) 命令行选项卸载软件包。输入 `rpm -e zebra-092a-3`。如果卸载成功，屏幕上不会显示任何内容。

与 Windows 不同，RPM 在卸载软件包时永远不会混淆哪些文件需要被删除。你不会被提示决定是否删除某个文件，因为因为它可能被其他软件包使用。包管理器已经知道了这一点。

9. 输入 `cd; umount /dev/cdrom; eject` 卸载 CD-ROM。

## 实验 13.5 检测并替换缺失的软件包文件

```
/usr/share/man/man1/gzexe.1.gz

/usr/share/man/man1/gzip.1.gz

/usr/share/man/man1/zcat.1.gz

/usr/share/man/man1/zcmp.1.gz

/usr/share/man/man1/zdiff.1.gz

/usr/share/man/man1/zforce.1.gz

/usr/share/man/man1/zgrep.1.gz

/usr/share/man/man1/zless.1.gz

/usr/share/man/man1/zmore.1.gz

/usr/share/man/man1/znew.1.gz
```
