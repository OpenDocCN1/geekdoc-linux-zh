
如果你在 `xterm`（即在 Windows 中）运行上述命令，SATAN 将启动 Netscape Navigator 浏览器（`/usr/bin/netscape`）。如果你没有这个 Web 浏览器并想使用文本浏览器 Lynx，请修改 `/root/satan/config/paths.pl` 脚本，将 `MOSAIC` 变量设置为 Lynx 浏览器的完整路径。现在如果你启动 SATAN，它将使用指定的浏览器。在这里我假设你会使用 Netscape Navigator。

取决于你的 Netscape Navigator 版本，你可能遇到的另一个问题是当你点击 SATAN 主界面上的链接（如图 19-1 所示）时，它们可能无效。

例如，我使用的是 Netscape Navigator Web 浏览器 4.0 版本，当我点击 SATAN 主页上的任何链接时，会得到如图 19-2 所示的屏幕。

# 第 19 章：网络安全

609

![](img/cbfef09f620ba4100baa62876f6f02b1_638_0.png)

图 19-1：SATAN 主界面屏幕

![](img/cbfef09f620ba4100baa62876f6f02b1_638_1.png)

图 19-2：Navigator 请求下载 SATAN 脚本。

这是由于 Navigator 缺少 MIME 配置不当或缺失而无法运行脚本所导致的。如果你遇到这个问题，请按照以下步骤操作：

- 1. 在 Netscape Navigator 的 Edit（编辑）菜单中，选择 Preference（偏好设置）选项，并点击图 19-3 所示的 Applications（应用程序）。
![](img/cbfef09f620ba4100baa62876f6f02b1_639_0.png)

图 19-3：配置 Netscape Navigator 与 SATAN 配合使用

- 2. 现在点击 New（新建），将 `.pl` 扩展关联到 `/usr/bin/perl`（或你存放 Perl 解释器的地方）。你会看到如图 19-4 所示的对话框。
- 3. 在 Description（描述）字段中，你可以输入任何你想的内容（例如 Perl Script）；在 MIMEType 字段中，输入 `application/x-perl`；在 Suffixes（后缀）字段中，输入 `.pl`。
- 4. 现在选择 Application（应用程序）为 `.pl` 文件分配处理程序，并在如图所示的输入框中输入 Perl 解释器的完全限定路径名。
- 5. 点击 OK 完成此过程并像往常一样关闭 Preference 窗口。

一旦你执行了这些步骤，SATAN 脚本将按预期方式运行。

## 第 19 章：网络安全

611

![](img/cbfef09f620ba4100baa62876f6f02b1_640_0.png)

图 19-4：将 `.pl` 与 Perl 解释器关联

当你启动 SATAN 时，可能会感到惊讶。大多数安全工具的用户界面都非常简陋。SATAN 非常重视用户交互。现在是直接进入第一次网络安全探测的好时机。点击图 19-1 所示的主菜单屏幕上的“SATAN Target selection”（SATAN 目标选择）链接。你会被带到如图 19-5 所示的下一个屏幕。

![](img/cbfef09f620ba4100baa62876f6f02b1_640_1.png)

图 19-5：选择要探测的主机

## 第 VI 部分：安全与监控

在这里，你可以命名想要探测的主机或网络，告诉 SATAN 你是否也想探测子网中的其他主机，并设置你想要探测的级别。我建议从对一个主机进行轻量扫描（light scan）开始。从那里你将对 SATAN 有感觉，然后转向更强大的探测。为了进行快速测试，选择你自己网络上的主机；选择“Scan the target only”（仅扫描目标）选项，并选择“Light”（轻量）选项进行轻量扫描。现在点击“Start the scan”（开始扫描）开始探测。

当 SATAN 完成对主机（或网络）的探测时，它会显示一个类似于图 19-6 所示的屏幕。

![](img/cbfef09f620ba4100baa62876f6f02b1_641_0.png)

图 19-6：SATAN 数据收集完成屏幕

要查看探测结果，点击“View primary target results”（查看主目标结果）链接，你将在一个类似于图 19-7 的屏幕中看到 SATAN 的探测结果。此图中显示 SATAN 在此次探测中没有发现任何问题。

轻量探测使用 `ping`、`nslookup`、`rcping` 和 `showmount` 来收集有关 DNS、RPC 服务和 NFS 的信息。如果轻量探测没有检测到问题，你尝试尝试常规探测（normal probe）。常规探测将尝试确定 UDP 和服务的信息。然而，在图 19-8 中，你会看到 SATAN 检测到我的测试服务器 `picasao.nitec.com` 的受信任主机（Trusted host）配置存在问题。

## 第 19 章：网络安全

613

![](img/cbfef09f620ba4100baa62876f6f02b1_642_0.png)

图 19-7：对主机的轻量探测结果

![](img/cbfef09f620ba4100baa62876f6f02b1_642_1.png)

图 19-8：对主机的常规探测结果

注意，在常规探测中，SATAN 发现我的测试服务器配置存在问题。点击结果中的“Trusted host(s)”（受信任主机）链接将显示图 19-9 所示的更多详细信息。

![](img/cbfef09f620ba4100baa62876f6f02b1_643_0.png)

图 19-9：潜在问题的细节

进行更耗时的深度扫描可能会揭示更多问题。如你所示，SATAN 提供了相当良好的文档，概述了所遇到的漏洞（或缺乏漏洞），显示了你可以如何处理。一旦你执行了这些步骤，SATAN 脚本将按预期运行。一旦你执行了这些步骤，SATAN 脚本将按预期运行。

# 第 20 章：内核破解

621

| 软件包 | RPM 中找到的描述 |
| --- | --- |
| `kernel-pcmcia-cs-2.x.xx.i386.rpm` | 标准的、版本 2 以及相关的可执行格式。许多笔记本电脑（以及其他一些设备）支持 PCMCIA 卡进行扩展。PCMCIA 卡也称为“信用卡适配器”，PCMCIA 卡是用于从 SCSI 到调制解器等各种设备的小型卡片。它们支持热插拔（可以在不重启系统的情况下更换），非常方便。此软件包包含了对各种型号的 PCMCIA 卡的支持，并提供了一个允许它们进行热插拔的守护进程。 |
| `kernel-source-2.x.xx.i386.rpm` | 这是 Linux 内核的源代码。编译大多数 C 程序时都需要它，因为它们依赖于此处定义的常量。你也可以构建一个针对你的特定硬件进行优化的自定义内核。 |
| `mknitrd-x.xx-x.src.rpm` | 对于任何允许 SCSI 驱动程序作为模块的 SCSI 适配器，都可以构建不带这些驱动程序的通用内核。为了解决内核能够读取模块但无法寻址 SCSI 适配器的问题，使用了初始内存盘（initial ramdisk）。该内存盘由操作系统加载器（如 LILO）加载，并在其一加载后即可供内核使用。该镜像负责加载正确的 SCSI 适配器并允许内核挂载根文件系统。此程序使用来自 `/etc/conf/modules` 的信息创建这样一个 ramdisk 镜像。 |
| `SysVinit-r.xx.src.rpm` | SysInit 是 Linux 内核在系统启动时启动的第一个程序，控制所有其他程序的启动、运行和关闭。 |
| `initscripts-r.xx-r.xx.src.rpm` | 此软件包包含了用于启动系统、更改运行级别（run levels）和安全关闭系统的脚本。它还包含了激活和禁用大多数网络接口的脚本。 |

现在让我们来看看我们当前正在使用哪个内核来启动系统。实现此目的的一种非常可靠的方法是查看 `/etc/lilo.conf` 文件。例如，在 Red Hat 5.2 系统上，我的 `/etc/lilo.conf` 包含以下行：

```
boot=/dev/hda

map=/boot/map

install=/boot/boot.b

prompt

timeout=50

image=/boot/vmlinux-2.0.36-0.7

label=linux

root=/dev/hd1

initrd=/boot/initrd-2.0.36-0.7.img

readonly

append=mem=128M
```
