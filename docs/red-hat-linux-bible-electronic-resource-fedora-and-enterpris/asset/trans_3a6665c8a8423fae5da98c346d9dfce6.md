

![](img/27a85d56d393921ced6412ae6e8336bf_63_0.png)

图 2-1：使用“添加/删除软件”窗口在安装 Red Hat 后更改软件包。

**注意：** 要使用 HTTP、FTP 或 NFS 安装，您的计算机必须连接到一个能够访问包含 Red Hat Linux 发行版的计算机的 LAN。您不能使用直接拨号连接。对于本地硬盘安装，发行版必须已被复制到一个不用于安装的本地磁盘上。有关复制发行版并使其可用的详细信息，请参阅“设置 HTTP、FTP 或 NFS 安装服务器”部分。

## 开始安装

要开始这些类型中的任意一种安装，您需要从软盘引导安装过程。请参阅本章后面关于创建引导盘的部分。您还需要知道安装服务器的位置——您网络上拥有 Red Hat Linux 发行版的 Red Hat Linux 系统。

手持引导盘（`bootdisk.img`，网络安装可能需要 `drvnet.img`，笔记本电脑安装可能需要 `pcmsiadd.img`），按如下方式开始这些安装类型的安装：

**注意：** 在随附此书的 Red Hat Linux 版本中，您也可以使用 CD #1 来启动网络或硬盘安装。您可以插入 Red Hat Linux 安装 CD #1，重新引导计算机，然后输入 `linux askmethod`，而无需使用软盘，如下所述。然后您可以继续执行下面所示的步骤。

1. 插入软盘引导盘。
2. **重新引导计算机。** 您应该会看到“Welcome to Red Hat”引导屏幕。
3. **按 Enter 键。** 系统提示您选择语言。
4. **选择语言。** 系统提示您选择键盘类型。
5. **选择您的键盘类型。** 系统提示您选择安装方法。
6. **选择安装方法。** 选择以下任意安装方法：NFS 镜像、FTP、HTTP 或硬盘。
7. **配置网卡。** 对于任意网络安装，系统会要求您从显示的列表中选择您的以太网卡。（这可能会被自动检测到。）如果您的网卡不在列表中，您需要从 `drvnet.img` 文件创建一张软盘，其中包含其他网卡的驱动程序。（要使用 `drvnet.img` 文件，请按 F2，插入包含该镜像的软盘，然后单击“确定”。从列表中选择您的网卡，再次单击“确定”。）
8. **配置 TCP/IP。** 对于任意网络安装类型（NFS、FTP 和 HTTP），系统会提示您为您的计算机配置 TCP/IP。（有关如何填写这些字段的信息，请参阅本章前面关于配置网络的部分。）
9. **指明 Red Hat Linux 发行版的位置。** 您必须指明包含发行版的 Red Hat 目录所在的 NFS 服务器名称、FTP 站点名称或 Web 站点名称。或者，如果您是从硬盘安装，则必须指明包含发行版的分区以及实际包含 Red Hat 目录的目录。

**注意：** 对于 FTP 安装，如果您不是从匿名 FTP 站点下载，则在指明服务器和目录时必须选择“使用非匿名 FTP”。您将需要一个有权访问共享目录的用户名和密码。

10. **执行校验和。** 系统会询问您是否要对该目录中找到的第一个磁盘镜像（第一张安装 CD 的 `.iso` 文件）执行校验和。如果要执行，请选择“测试”。这将在开始安装前验证镜像是否损坏。对每个磁盘镜像重复此操作。
11. **继续安装。** 如果在您指明的位置找到了发行版，请继续安装，如上一节所述。安装过程是基于文本的。

下一节介绍如何设置您自己的服务器来安装 Red Hat Linux。

## 设置 HTTP、FTP 或 NFS 安装服务器

如果您的计算机通过 LAN 连接到一台拥有约 2.5GB 磁盘空间并提供 NFS、FTP 或 Web 服务的计算机，您可以从该服务器安装 Red Hat Linux。同样，您也可以通过使用硬盘安装，从一个备用磁盘分区进行安装。以下过程可让您通过复制三张 CD 的所有文件或复制三张 CD 的镜像来设置 Linux 安装服务器。

### 使用文件配置安装服务器

要执行 FTP 或 HTTP 安装，您必须将安装 CD 上的文件复制到一个可供网络访问的目录中。因为 Red Hat Linux 发行版中有三张安装 CD，所以您不能只指明一个已挂载 CD 的位置。您必须将所有三张 CD 的内容安装在服务器硬盘上的相同目录结构中。例如，您可以执行以下操作：

```
# mkdir /tmp/rh
# mount /mnt/cdrom	插入第一张 CD
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom	插入第二张 CD
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom	插入第三张 CD
# cp -r /mnt/cdrom/* /tmp/rh/
```

当询问是否覆盖某些文件时，只需输入 y。发行版目录必须至少包含 RPMS 和 base 目录，它们必须包含所有必需的软件包。在本示例中，复制了所有文件。设置 NFS 安装服务器需要将 CD 镜像复制到共享的 NFS 目录中。

### 使用磁盘镜像配置安装服务器

您可以将三张安装 CD 中每张的完整镜像复制到硬盘上，用于 NFS 或硬盘安装，而不必复制所有文件。要执行此操作，请插入第一张安装 CD 并输入以下命令：

```
# mkdir /tmp/rh
# dd if=/dev/cdrom of=/tmp/rh/disk1.iso	插入第一张 CD
# mount /mnt/cdrom ; eject /mnt/cdrom
# dd if=/dev/cdrom of=/tmp/rh/disk2.iso	插入第二张 CD
# umount /mnt/cdrom ; eject /mnt/cdrom
# dd if=/dev/cdrom of=/tmp/rh/disk3.iso	插入第三张 CD
# umount /mnt/cdrom ; eject /mnt/cdrom
```

### NFS 服务器

向 `/etc/exports` 文件添加一个条目以共享您创建的发行版目录。请记住，对于 NFS 安装，此目录必须包含 CD ISO 镜像。以下条目将使该目录以只读形式对任何计算机可用：

```
/tmp/rh	(ro)
```

接下来，以 root 用户身份输入以下命令重新启动 NFS：

```
# /etc/init.d/nfs restart
```

要永久开启 NFS 服务（默认情况下它是关闭的），请以 root 身份输入以下命令：

```
# chkconfig nfs on
```

### Web 服务器

如果您的计算机配置为 Web 服务器，您只需使发行版目录可用即可。例如，在按上述方法创建发行版目录后，输入以下命令：

```
# ln -s /tmp/rh /var/www/html/rh
```

如果您的计算机名为 `pine.hansonhistory.com`，您将把安装服务器指明为 `pine.hansonhistory.com`，目录指明为 `rh`。

### FTP 服务器

如果您的计算机配置为 FTP 服务器，您需要使发行版目录可用，方式与 Web 服务器非常相似。例如，在按上述方法创建发行版目录后，输入以下命令：

```
# ln -s /tmp/rh /var/ftp/pub/rh
```

如果您的计算机名为 `pine.hansonhistory.com`，您将把安装服务器指明为 `pine.hansonhistory.com`，目录指明为 `pub/rh`。

### 硬盘安装

将每张 CD 的 ISO 镜像复制到一个不用于 Red Hat Linux 安装的磁盘分区后，您可以使用硬盘安装。如果 ISO 镜像存在于您的 IDE 硬盘第一个分区的 `/tmp/rh` 目录中，您可以将设备指明为 `/dev/hda1`，将保存镜像的目录指明为 `/tmp/rh`。

## 执行 Kickstart 安装

如果您要在多台计算机上安装 Red Hat Linux，可以通过预先配置安装过程中所提问题的答案来省去一些麻烦。这种自动化安装过程的方法称为 *kickstart* 安装。

> **警告：** 根据您在 `ks.cfg` 文件中提供的信息，kickstart 将在无干预的情况下静默地完成 Red Hat Linux 的安装。如果此文件不正确，您可能会轻易地删除主引导记录并擦除硬盘上的所有内容。请仔细检查 `ks.cfg` 文件，并在关键数据计算机上尝试之前，先在非关键计算机上进行测试。

执行 kickstart 安装的一般步骤如下：

1. **创建 kickstart 文件。** Kickstart 文件名为 `ks.cfg`，包含提供给安装过程的问题回答。
2. **安装 kickstart 文件。** 您必须将 `ks.cfg` 放在软盘上、本地硬盘上或网络上可访问的位置。
3. **启动 kickstart 安装。** 当您引导安装过程时，需要指明 `ks.cfg` 文件的位置。

