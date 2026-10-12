
### FOG

不间断地执行重复任务，如运行检查、排查错误、更换故障硬盘、一遍又一遍地进行全新安装，这会耗尽任何系统管理员的精力，无论其网络规模大小。使用`FOG`，你可以从管理中心的舒适环境中对机器进行镜像和克隆。

`FOG` 是一个复杂的软件，提供大量选项，具有各种字段来描述主机镜像。它还可以将它们分组以便于管理。还有几个选项用于安排镜像过程。`FOG` 还可以用于调试镜像过的计算机，远程擦除主机等。服务器还处理常规管理任务，如安装软件，甚至可以管理网络中的打印机。`FOG` 服务器具有可扩展性，可以管理分布在同一建筑物内或地球另一端的大网络。`FOG` 服务器最有用的功能之一，尤其对于较大网络的管理员来说，是组播能力。使用此功能，你可以一次部署多台机器。为了在这样的大网络上补充它，你可以配置多个`FOG`安装作为存储服务器，以帮助在对计算机进行镜像时减轻主`FOG`服务器的负载。 [https://fogproject.org](https://fogproject.org)

### DUPLICATI

一款易于使用的备份应用程序，`Duplicati` 允许你通过定义过滤器或切换预定义选项来排除特定类型的文件，从而精细调整你想要保留的位置列表。你可以通过基于浏览器的界面管理该工具。该程序将关键任务分解为向导，并恰好提供手头工作需要数量的功能，而高级选项只需拉下一个菜单即可到达。文件使用`AES-256`加密，你也可以在将备份发送到目的地之前使用`GPG`。`Duplicati` 还会在加密之前压缩所有数据。它支持`Zip`和`7Z`压缩，并且可以跳过对已压缩文件（如`MP3`和`JPG`）的压缩。 [www.duplicati.com](http://www.duplicati.com)

### PHOTOREC

`Photorec` 是一个巧妙的基于命令行的小工具，可以恢复意外删除的文件。当你删除一个文件时，文件系统只是将其标记为已删除，并使该文件占据的空间可供其他文件使用。`Photorec` 的工作原理是恢复那些缺少常规元数据（如文件名）的文件。尽管名为`Photorec`，但该命令行工具可以嗅探各种格式的文件。 [www.cgsecurity.org/wiki/PhotoRec](http://www.cgsecurity.org/wiki/PhotoRec)

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_169_0.png)

`Photorec` 几乎每个恢复发行版的一部分，并随`TestDisk`一起分发。

### GPARTED

这是管理分区的最佳图形化工具之一，你可以使用`GParted`创建、删除、调整大小、移动和复制分区，同时保留其中存储的数据。该程序适用于各种硬盘、`SSD`和`RAID`设备，并支持所有流行的文件系统。 [https://gparted.org](https://gparted.org)

### SECURE-DELETE

`secure-delete` 软件包包含各种实用工具，用于安全地删除文件并清除磁盘空闲空间中数据的所有痕迹。有`shred`使任何已删除的文件无法恢复，`sfill`用于清除磁盘空闲空间中的所有数据，以及`sswap`用于清除交换分区中的数据。 [https://smr.sourceforge.net](https://smr.sourceforge.net)

### CDEMU

`CDEmu` 工具允许你挂载各种格式的磁盘镜像，包括`ISO`、`bin`和`img`。`CL`工具还针对`Gnome`和`KDE`桌面环境提供了多个图形前端。 [https://cdemo.sourceforge.io](https://cdemo.sourceforge.io)

### DUC

如果你想释放一些磁盘空间，首先使用`Duc`来更好地了解占用空间的文件。该工具在检查硬盘方面比文件管理器做得更好。 [https://duc.zew.nl](https://duc.zew.nl)

### DDRESUE

在尝试恢复之前，先尝试使用`ddrescue`对故障驱动器进行镜像。该实用工具不会向坏扇区写入零，并试图在不覆盖已恢复数据的情况下填补空白。 [www.gnu.org/software/ddrescue](http://www.gnu.org/software/ddrescue)

### PYDF

作为`df`的替代，`pydf`是一个高亮显示不同文件系统类型的`Python`脚本。它有一组大量可配置的参数和各种选项来控制其输出。 [https://pypi.org/project/pydf](https://pypi.org/project/pydf)

### SMARTCTL

作为`smartmontools`软件包的一部分附带，`smartctl`实用工具控制和监控内置于硬盘中的`SMART`系统。定期使用该工具对磁盘运行自检健康检查。 [www.smartmontools.org](http://www.smartmontools.org)

### 文件管理

掌控你的数据，决定其可访问的位置，并进行归档。

### Eiciel (45)

在`Linux`中，一切都以文件形式存在，而访问控制列表（`ACL`）有助于确定每个文件的访问权限。你可以通过命令行修改权限，也可以使用大多数发行版官方软件源中提供的图形化`Eiciel`工具。

https://rofi.roger-ferrier.org/eiciel

### Nextcloud

在线存储服务是在全球任何地方访问和共享数据的便捷选择。使用`Nextcloud`，你可以部署一个托管存储服务器，从而享受无处不在的存储服务的便利，而无需向第三方支付大量费用并交付你的数据。

安装和部署`Nextcloud`是一个相对简单且文档完善的过程。它拥有一个功能丰富且直观的`Web`界面，即使是首次用户也不难掌握其导航方式，考虑到它背后的庞大功能数量，这一点本身就值得称赞。该项目具有良好的可扩展性，既可用于家庭网络，也可用于企业网络。你可以使用其管理部分将其与其他相关的网络服务（如目录服务器）集成，以导入用户。

通过网络上的其他用户或公共`URL`共享文件非常简单。服务器确保对共享文件所做的更改同步到所有用户。它还可以访问存储在`Amazon`、`Google`和`Dropbox`等多种云服务上的文件。

https://nextcloud.com

### FSLint

你可以使用图形化的`FSLint`工具对文件系统进行全面清理。它可以删除重复文件、临时文件，以及其他难以定位和删除的文件，例如名称无效的文件、空目录和无效的`ID`。

www.pixelbeat.org/fslint

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_170_0.png)

### Open Media Vault

如果你对数据的安全保护需求超出了简单的备份方案，那么你需要将一台闲置的电脑（甚至树莓派）转换为基于`Debian`的`Open Media Vault` (`OMV`)服务器的专用网络附加存储（`NAS`）设备。

`OMV`部署简单，管理方便，这得益于其设计良好的基于浏览器的用户界面，使其甚至适合非技术用户。它支持所有流行的部署机制，包括多级软件`RAID`，你可以使用所有流行的网络协议（如`SSH`、`SMB/CIFS`、`FTP`和`Rsync`）访问其中存储的数据。服务器还拥有一个详尽的权限系统，用于控制对共享卷和文件夹的访问。该服务器采用模块化设计，可以通过各种官方和第三方插件进行扩展。例如，你可以将`NAS`变成一个`torrent`客户端，直接下载数据到`NAS`存储中，或者用它来在网络上流式传输存储的音乐。

www.openmediavault.org

### Syncthing

作为流行但专有的`BitTorrent Sync`的开源替代品，`Syncthing`可以在局域网内或全球范围内同步你的文件。该服务使用全球发现服务来连接互联网上的客户端。

https://syncthing.net

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_170_1.png)

### Catfish

作为`find`和`locate` CLI工具的图形化替代品，`Catfish`是一个多功能工具，具有各种选项，可帮助你筛选搜索结果并找到你正在寻找的文件。

www.twotoast.de/index.php/catfish

### PeaZip

该图形化压缩工具可以读取大多数归档格式，并拥有一些有用的数据安全功能，例如创建带有加密和双因素身份验证的归档文件。

www.peazip.org

### ExifTool

这是一个用于处理图像元数据的`CLI`工具，`ExifTool`帮助你基于元数据操作文件。用户还可以使用它在在线分享图像之前剥离所有元数据。

www.sno.phy.queensu.ca/~phil/exiftool/

### Tkdiff

这是`diff`工具的图形化前端，你可以使用`Tkdiff`来比较两个文件。该工具可以连接多种源代码管理系统，并具有其他多种功能。
