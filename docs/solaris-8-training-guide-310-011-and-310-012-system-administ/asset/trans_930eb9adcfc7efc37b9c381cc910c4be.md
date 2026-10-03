
- Sun MediaCenter One
- Sun WebServer
- Sun Management Console

这些软件包在更新时大小偶尔会发生变化，因此请联系 Sun 以获取每个软件包当前的磁盘空间需求。

> 您可以通过本地 CD 或通过连接到网络的系统上的 CD-ROM 安装软件。但是，为了提高速度，我建议从本地 CD-ROM 驱动器加载软件。

## 使用交互式安装程序安装软件

您现在可以安装软件了。我建议使用两种方法之一安装操作系统：交互式或 Web Start。本章描述了交互式安装过程。此选项在安装操作系统时为您提供最大的灵活性。Web Start 在附录 A“Web Start”中描述。

## 逐步操作

### 15.1 安装交互式软件

以下步骤概述了交互式软件安装过程：

1. 将 Solaris 8 安装 CD 插入 CD-ROM 驱动器。
2. 在 OpenBoot ok 提示符下，输入以下内容：

```
boot cdrom
```

系统将从 CD-ROM 启动，并开始配置设备。几分钟后，您将进入安装的系统识别部分。安装程序将开始对话，询问您有关系统的各种问题。最好提前收集这些信息。请参阅第 3 章“安装 Solaris 8 软件”中的“ Solaris 安装过程”部分，以获取需要收集的信息列表。按照系统提示输入信息：系统会要求您选择语言和区域设置。您还需要输入系统的主机名、IP地址和网络信息，因此请准备好这些信息。

3. 系统识别部分之后，您将看到以下对话：

Solaris 交互式安装：

```
This system is upgradable, so there are two ways to install the Solaris software.

The Upgrade option updates the Solaris software to the new release, saving as many modifications to the previous version of Solaris software as possible. Back up the system before using the Upgrade option.

The Initial option overwrites the system disks with the new version of Solaris software. This option allows you to preserve any existing file systems. Back up any modifications made to the previous version of Solaris software before starting the Initial option.
```

选择选项并完成后续任务后，将显示您的操作摘要。

```
F2_Upgrade    F4_Initial    F5_Exit    F6_Help
```

4. 按 F4 选择完整重新安装软件。您将看到以下对话框：

```
You'll be using the initial option for installing Solaris software on the system. The initial option overwrites the system disks when the new Solaris software is installed.
```

在以下屏幕上，您可以接受默认值，也可以自定义 Solaris 软件的安装方式：

- 选择要安装的 Solaris 软件类型
- 选择用于存放已选软件的磁盘
- 指定磁盘上文件系统的布局

完成这些任务后，将显示您的选择摘要（称为配置文件）。

5. 按 F2 继续。

> 警告
操作系统分区上的所有数据都将丢失。这些分区包括 /（根）、/usr、/opt 和 /var。

> 注释
由于您想要完整重新安装软件，您将选择 F4。如果您当前正在运行 Solaris 7 并希望升级到 Solaris 8，则可以使用升级选项。使用升级选项，您在 Solaris 7 中所做的所有自定义设置都将被保存。

系统会要求您选择要安装支持的地理区域，例如亚洲、东欧等。如果您想选择英语以外的语言，请在此处选择，然后按 F2 继续。

6. 系统会询问您是否要在该系统上安装 Solaris 64 位软件包。如果您的系统是 UltraSparc（sun4u）系统并且支持 64 位架构，请选择此选项以在该系统上安装 Solaris 64 位软件包，然后按 F2 继续。您将看到以下对话框：

```
Select Software

Select the Solaris software to install on the system.

NOTE: After selecting a software group, you can add or remove software by customizing it. However, this requires understanding of software dependencies and how Solaris software is packaged. The software groups displaying 64-bit contain 64-bit support.

[ ] Entire Distribution plus OEM support 64-bit 1158.00 MB
[ ] Entire Distribution 64-bit ............... 1218.00 MB
[ ] Developer System Support 64-bit ........... 1169.00 MB
[X] End User System Support 64-bit ............ 855.00 MB
(F4 to Customize)
[ ] Core System Support 64-bit ............... 269.00 MB

F2_Continue  F3_Go Back  F4_Allocate  F5_Exit  F6_Help
```

7. 选择要安装的软件集群，然后按 F2。对于服务器，我建议选择 Entire Distribution 集群，以便加载所有内容。

按 F2 后，您将看到以下对话：

选择磁盘：

在此屏幕上，您必须选择用于安装 Solaris 软件的磁盘。首先查看“建议最小值”字段；该值是安装您所选软件所需的近似空间。继续选择磁盘，直到“已选总计”值超过“建议最小值”。

> 注释
默认情况下选择 End User System Support 集群。在前面的示例中，我选择了 Entire Distribution 集群，这在服务器上很常见。选择要安装的软件集群后，如果按 F4，您将看到一个交互式菜单，允许您在特定集群中选择和取消选择软件包。

> 注释
我总是选择服务器上的整个发行版，因为稍后不得不返回安装另一个软件包很烦人，尤其是在支持许多用户的服务器上。有时，由于磁盘空间不足，整个发行版集群未被安装。随着今天磁盘空间变得如此便宜，请添加更大的磁盘并安装整个发行版。

磁盘设备（大小） | 可用空间
---|---
[X] c0t0d0 (4102 MB) 启动磁盘 | 4102 MB (F4 to edit)

已选总计：4102 MB
建议最小值：851 MB

```
F2_Continue  F3_Go Back  F4_Edit  F5_Exit  F6_Help
```

8. 选择您的磁盘，然后按 F2。您将看到以下对话：

```
Preserve Data?
Do you want to preserve existing data? At least one of the disks you've selected for installing Solaris software has file systems or unnamed slices that you may want to save.
```

```
F2_Continue  F3_Go Back  F4_Preserve  F5_Exit  F6_Help
```

9. 按 F2，所有文件系统上的数据将被擦除。您将看到以下对话：

```
Automatically Layout File Systems?
Do you want to use auto-layout to automatically layout file systems? Manually laying out file systems requires advanced system administration skills.
```

```
F2_Auto Layout  F3_Go Back  F4_Manual Layout  F5_Exit
F6_Help
```

10. 按 F2。系统会自动布局文件系统。大小由您选择的软件包决定。如果您计划添加其他软件，可以在后面的步骤中修改文件系统大小。您将看到以下对话：

自动布局文件系统

在此屏幕上，您必须选择所有希望自动布局创建的文件系统，或接受显示的默认文件系统。

注释：对于小型磁盘，自动布局可能需要将您请求的一些文件系统拆分为更小的文件系统以适应可用磁盘空间。因此，自动布局完成后，您可能会在布局中找到未从下面列表中选择的文件系统。

```
File Systems for Auto-layout
================================
[X]  /
[ ]  /opt
[ ]  /usr
```
