

## 表 39.1 续

| 名称 | 描述 |
| :--- | :--- |
| 融合 MPT 设备支持 | 配置对 LSI 逻辑融合消息传递技术（Fusion Message Passing Technology）的支持。该技术支持高性能 SCSI 和局域网接口。 |
| IEEE1394（火线）支持 | 对火线设备的实验性支持。 |
| I20 设备支持 | 支持智能输入/输出（Intelligent Input/Output）架构的选项。此架构允许将硬件驱动程序与操作系统驱动程序分离，从而使多种硬件设备能够通过一种实现与操作系统兼容。 |
| 网络选项 | 内核中网络配置的若干选项。这些选项涉及支持的协议类型以及这些协议的可配置选项。 |
| 业余无线电支持 | 配置支持 AX25 协议的设备的选项。 |
| IrDA（红外）支持 | 配置支持红外数据协会（Infrared Data Association）协议套件及使用这些协议的设备的选项。 |
| 蓝牙支持 | 对蓝牙无线协议的支持。包括支持蓝牙协议和硬件设备的选项。 |
| ISDN 子系统 | 支持综合数字业务网（Integrated Services Digital Networks）协议和设备的选项。ISDN 是一种通过经过调理的电话线路以数字方式连接广域网的方法，主要用于将用户连接到 ISP。 |
| 电话支持 | 支持使用普通电话线来运行 VOIP 应用程序的设备。本节不处理调制解调器的配置。 |
| 输入核心支持 | 配置通用串行总线（USB）人机接口设备（HID）的选项。这些设备包括键盘、鼠标和摇杆。 |
| 字符设备 | 配置以顺序字符方式与服务器通信的设备的选项。这是一个较大的子部分，包含多个主板芯片的驱动程序。 |
| 多媒体设备 | 视频和声音设备硬件实现的驱动程序，例如视频采集卡、电视卡和 AM/FM 收音机适配器卡。 |
| 图形支持 | 配置 VGA 文本控制台、视频模式选择以及对帧缓冲卡的支持。 |
| 声音 | 用于配置内核支持的声音卡驱动程序和芯片组支持的大型子部分。 |
| USB 支持 | 通用串行总线（USB）配置选项。包括 USB 设备的配置，以及特定厂商版本的 USB。 |
| 文件系统 | 支持的文件系统类型的配置选项。有关内核支持的文件系统的描述，请参阅第 38 章。 |
| 其他设备驱动程序支持 | 第三方补丁。 |
| 性能分析支持 | 对内核行为信息进行分析，以辅助调试和开发。 |
| 内核黑客工具 | 确定内核是否包含高级调试选项。大多数用户不希望在生产内核中包含此选项，因为它会增加内核大小并通过添加额外例程降低性能。 |
| 安全选项 | 确定是否启用国家安全局安全增强型 Linux（SELinux）。 |
| 加密选项 | 对加密硬件的支持（Fedora 补丁未出现在 vanilla 内核源代码中）。 |
| 库例程 | 包含 zlib 压缩支持。 |

![](img/2045828cf45e5632bf056f9ca99d6755_1016_0.png)

选定所有期望的选项后，你可以保存配置文件，并继续执行前文所示的内核编译检查清单中的步骤 7。

### 创建初始 RAM 磁盘镜像

如果你需要加载特殊的设备驱动程序才能挂载根文件系统（例如用于 SCSI 驱动器、网卡或奇异文件系统），则必须创建名为 `boot/initrd.img` 的初始 RAM 磁盘镜像。对于大多数用户来说，创建此文件并非必要，但如果你不确定，创建它也无妨。我们在第 38 章中介绍了 `initrd.img`。要创建 `initrd.img` 文件，请使用 shell 脚本 `/sbin/mkinitrd`。

该命令的格式如下：

```
/sbin/mkinitrd file_name kernel_version
```

其中 `file_name` 是你想要创建的镜像文件的名称。

`mkinitrd` 会查看 `/etc/fstab`、`/etc/modprobe.conf` 和 `/etc/raidtab` 以获取确定启动期间应加载哪些模块所需的信息。对于我们的系统，我们使用：

```
# mkinitrd initrd-2.6.7-1.img 2.6.7-1
```

### 当出现问题时

在编译和安装内核期间可能会出现各种问题，而若干线索会指向真正的问题所在。你会在屏幕上看到打印的错误消息，某些错误消息会写入文件 `/var/log/messages`，可以通过文本编辑器查看该文件。如果你按照我们的说明修补了内核，还需要查看一个特殊的错误日志。不要担心错误，因为许多问题只需你进行一些研究即可轻松修复。然而，根据你的技能水平和可用技术信息的丰富程度，某些错误可能无法修复。

### 编译期间的错误

虽然内核无法编译的情况很少见，但总有某种回归测试遗漏问题的可能性。让我们看看一个在编译过程中可能出现的问题示例。

内核编译可能会崩溃且未能成功完成，特别是在你尝试使用实验性补丁、添加未经测试的功能或在较旧的系统中构建较新且可能不稳定的模块时。例如，在旧的 Red Hat 7.2 默认安装上使用 2.4.9 内核时，如果选择 NTFS 文件系统（无论是作为可加载模块还是内联），内核编译将会失败，如下所示：

```
gcc -O -KERNEL__ I/usr/src/kernels/linux_2.4.9/include -Wall -Wstrict-prototypes -Wno-trigraphs -O2 -fomit-frame-pointer -fno-strict-aliasing -fno-common -pipe -mprefered-stack-boundary-2 -march=pentium -DMODULE -DMODVERSIONS -include /usr/src/kernels/linux_2.4.9/include/linux/modversions.h - -DNFTS_VERSION='1.1.16' -A\ -c -o unistr.o unistr.c

unistr.c: In function 'ntfs_collate_names' :

unistr.c:99: warning: implicit declaration of function 'min'

unistr.c:99: parse error before 'unsigned'

unistr.c:99: parse error before ')'

unistr.c:97: warning: 'cl' might be used uninitialized in this function

unistr.c: At top level :

unistr.c:118: parse error before 'if'

unistr.c:123: warning: type defaults to 'int' in declaration of 'cl'

unistr.c:123: 'name1' undeclared here (not in a function)

unistr.c:123: warning: data definition has no type or storage class

unistr.c:124: parse error before 'if'

make[2]: *** [unistr.o] Error 1

make[2]: Leaving directory '/usr/src/kernels/linux_2.4.9/fs/ntfs'

make[1]: *** [_mods subdir_ntfs] Error 2

make[1]: Leaving directory '/usr/src/kernels/linux_2.4.9/fs'

make: *** [_mod_fs] Error 2
```

在此情况下，你有两个选项：

- 修复错误并重新编译
- 移除有问题的模块或选项，并等待内核团队修复这些错误

由于内核代码的复杂性，大多数用户无法修复某些错误，尽管你不应该排除这个选项。有可能其他人已经在测试内核期间发现了相同的错误并开发了用于解决该问题的补丁：请检查 Linux 内核邮件列表存档。如果那里没有提到该问题，在 Google 上搜索可能会找到相关内容。

第二个选项，即移除代码，是最简单的，在那些非必需的代码出问题的情况下，大多数人都会这样做。对于 NTFS 模块失败的情况，这几乎是可以预期的，因为 NTFS 支持仍被视为实验性的且容易出错。这主要是因为该文件系统的代码是通过逆向工程实现的，而不是通过文档化的标准实现的。在较新的内核中，只读支持有所改善；写支持仍然是实验性的。

最后，如果你愿意承担尝试自行修复该问题的任务，这是参与 Linux 内核并做出有助于许多其他用户的贡献的好机会。

如果你精通编码和内核事务，你可能希望在内核源代码目录 `/usr/src/kernels/linux 2.6/` 中的 `MAINTAINERS` 文件中查找该代码的维护者。建议的行动步骤是联系维护者，看看他是否知道你所遇到的问题。如果没有针对特定错误的文档记录，向内核邮件列表提交错误也是一个选项。这样做准则位于内核源代码基础目录下的 “If Something Goes Wrong”（当出现问题时）部分中的 `README` 文件中。

### 运行时错误、引导加载器问题和内核崩溃（Oops）

运行时错误发生在内核加载期间。错误消息会显示在屏幕上或写入 `/var/log/messages` 文件。引导加载器问题会在屏幕上显示消息，因此不会生成日志文件。内核崩溃（Oops）是运行中的内核发生的错误，错误消息会写入 `/var/log/messages` 文件。

互联网上存在出色的文档，用于排除 Lilo、GRUB 或内核在启动过程中可能出现的几乎所有类型错误的故障。查找这些文档的最佳方法是前往你喜欢的搜索引擎，输入你收到的错误的关键字。随着你聚焦搜索范围，你需要调整使用的关键字。

在此类别中，最常见的问题涉及 LILO 配置问题。可以在 Linux 文档项目网站 http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/LILO.html 上找到 LILO mini-HOWTO 中对这些问题的诊断和解决方案。

如果你有 GRUB 问题，GRUB 手册在线位于 http://www.gnu.org/software/grub/manual/。

> **提示**
>
> 为了获得最佳结果，请访问 http://www.google.com/linux 以在互联网上查找所有 Linux 相关内容。Google 特别创建了一个 Linux 数据库区域，这应该比任何其他搜索引擎都能更快地访问有关 Linux 的信息。
>
> 可以在 http://www.google.com/grph 搜索 Usenet 新闻组帖子。
>
> 可以在 Mailing list Archives (MARC) http://marc.theaimsgroup.com/ 中搜索邮件列表讨论。

