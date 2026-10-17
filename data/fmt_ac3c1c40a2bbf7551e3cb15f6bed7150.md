
现在你可以将你的更新指向本地镜像了。这是一个简单的过程。如果你想要更新的 SUSE 专业或 SUSE Linux 计算机是本地的，你只需要将 YaST 在线更新（YaST Online Update）指向正确的镜像目录即可。

如前一节所述，我在 `/mnt/i386/update/9.2` 目录下配置了我自己的 SUSE 专业 Linux 镜像站点。我知道这其中包含一个 `patches` 子目录。由于 YaST 在线更新查找 `i386/update/9.2/patches`，我只需要将它指向 `/mnt` 即可。

如果我在与更新镜像相同的同一台计算机上有一个 SUSE 专业 Linux 系统，我可以按照以下步骤配置更新：

1. YaST。如果你在图形界面中，点击主菜单按钮 -> 系统控制中心 (YaST)。
2. 在软件菜单下，选择“在线更新”（Online Update）。
3. 在“安装源”下拉框中，指定“自定义位置”（User-Defined Location）。
4. 在位置文本框中，指定包含 `i386/update/9.2/patches` 子目录的目录。使用之前定义的目录，即：
   ```
   dir:///mnt/
   ```
5. 选择“下一步”（Next）继续。你将看到一个类似于图 3-15 所示的 Ya 在线更新 (YOU) 补丁列表。检查可用补丁列表。你会注意到其中一些是升级；另一些是在之前的版本上安装新包。并非所有选项都会被选中。进行任何所需的更改。
6. 当你准备好所需的补丁时，选择“接受”（Accept）继续。
7. 在补丁下载过程中，如果有任何关键升级（例如与 Linux 内核相关的），将提供警告。

图 3-16 显示了警告的一个示例。针对你看到的任何警告做出适当的选择。

## 3.2 为局域网配置 YaST 补丁

![](img/e178bfcea0b6629d1234b59342d4d)

### 3.3.1 支持的客户端与服务器

如果您想安装 `ZLM` 6.6.1 服务器，您需要一台安装了 SUSE Linux Enterprise Server 9 的计算机（适用于 Intel 32 位或 64 位计算机）。或者，您也可以在适用于 Intel 32 位计算机的 Red Hat Enterprise Linux 3 AS 或 ES 上安装 `ZLM`。截至编写本文内容时，`ZLM` 7 仍在开发中，我们预计它将作为服务器安装在 Red Hat Enterprise Linux 4 上，并可用于 SUSE Linux Workstation 9.3 和 SUSE Linux 10.0（以及下文列出的其他客户端）的更新。如果您不想在网络上安装这任何一种发行版，则将不得不使用本章之前描述的技术来保持您的 SUSE 计算机为更新。

您可以使用 `ZLM` 管理多个不同客户端的更新。`ZLM` 6.6.1 客户端适用于以下发行版：

- 适用于 32 位系统的 SUSE Linux Enterprise Server 版本 8
- 适用于 32 位、许多 64 位 PowerPC 以及 S/390 系统的 SUSE Linux Enterprise Server 版本 9
- 适用于 32 位和许多 64 位系统的 SUSE Linux Professional Workstation 版本 9.1 和 9.2
- 适用于 32 位系统的 Red Hat Enterprise Linux 2.1 Workstation
- 适用于 32 位和许多 64 位系统的 Red Hat Enterprise Linux 3 Workstation
- 适用于 32 位系统的 Red Hat Enterprise Linux ES（入门级服务器）2.1
- 适用于 32 位和许多 64 位系统的 Red Hat Enterprise Linux ES 3
- 适用于 32 位系统的 Red Hat Enterprise Linux AS（高级服务器）2.1
- 适用于 32 位和许多 64 位系统的 Red Hat Enterprise Linux AS 3

### 3.3.2 安装 ZLM 服务器

运行 `ZLM` 需要一个许可许可。您可以从 `download.novell.com` 下载一张光盘；使用搜索词：`zenworks linux`。您可以下载 ISO 格式的最新可用版本，并将其写入光盘。

当您准备好 `ZLM` 光盘后，可以在其中支持的发行版之一上安装 `ZLM` 服务器。它包含一个安装脚本 `rce-install`，您可以使用它来安装 `ZLM` 服务器。要安装 ZENworks，插入并挂载 `ZLM` 光盘，然后运行 `rce-install` 脚本。如果光盘挂载在 `/media/cdrecorder` 目录，您可以使用以下命令运行脚本：

```
/media/cdrecorder/rce-install
```

## 3.3 ZENWorks Linux 管理

如图 3-17 所示，脚本会要求您接受许可协议。它会询问您的激活码、电子邮件地址以及您网络的任何代理信息。然后它将至少安装 Red Carpet 进程 `r` 和 Red Carpet 命令行客户端 `rc`。还会安装支持服务和服务包，并安装配置文件，允许您使用 Web 服务器控制 `ZLM`。

```
Session Edit: View Bookmarks Settings Help:
Would you like to skip this step? (y/n): m
Activation code: []
Email address: []
Does this mean to use a proxy server to access the internet? (y/n): y
Package "yum" is not installed
Package "yum" is installed, version '2.3.3'
Detect yum 2.3.3, using
Package "rc" is not installed
Package "rc" is installed
Running: rpm install /media/cdrom/packages/el-9-ZHEL-rc-2.4.0-1.el9.x86_64.rpm VPG BPG signature:
********************************************************************
Preparing:
0off 1off 2off 3off 4off 5off
Package "rc" is not installed
Package "rc" is installed
Running: rpm install /media/cdrom/packages/el-9-ZHEL-rc-2.4.0-1.el9.x86_64.rpm VPG BPG signature:
********************************************************************
Preparing:
: is install /media/cdrom/packages/el-9-ZHEL-rc-2.4.0-1.el9.x86_64.rpm VPG BPG signature:
********************************************************************
Preparing:
Package "rc" is not installed
Package "rc" is installed
Running: rpm install /media/cdrom/packages/el-9-ZHEL-rc-2.4.0-1.el9.x86_64.rpm VPG BPG signature:
********************************************************************
Preparing:
Would you like to leave rug after ZENWorks Management is? (y/n): [
```

现在 `ZLM` 已配置为使用经验过的 SSL 证书。更多信息，请参阅相关的 Linux HOWTO 文档：`www.tldp.org/HOWTO/SSL-Certificates-HOWTO`。如果你想使用 SSL 证书，可以在每个客户端上通过以下命令配置设置：

```
rug set require-verified-certificates false
```
