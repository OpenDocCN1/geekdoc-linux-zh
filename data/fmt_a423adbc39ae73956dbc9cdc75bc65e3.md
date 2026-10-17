
多年来，网络文件系统 (`NFS`) 是系统间共享文件的首选方法。`Mac OS Connect to Server` 允许目录就像存在于你的 `Mac` 上一样。如果你无法访问服务器，需要手动请求（我将在节末尾描述手动操作过程）。

# 连接到 NFS

要在 `Linux` 上按照第 18 章描述的创建一个共享目录并连接它：

为了让 `Mac OS` 能够使用共享目录，你必须确保添加 `insecure` 选项。例如，从名为 `jukebox.linxtoys.net` 的服务器共享 `/var/music` 目录，可以在 `/exports` 中添加以下行：

```
/var//    *(ro,insecure)
```

此示例允许所有计算机共享 `/var/music` 目录，并提供只读权限。`insecure` 选项允许从 1024 以上的端口请求挂的导出。。很重要，，因为 `Connect Connect Server Server` 窗口 1024 以上的端口来挂载共享目录。

在 `Linux` 服务器上，验证 `NFS` 服务正在运行，并通过输入以下命令重新导出共享目录（使用 `root`）：

```
# exports -a
```

在 `Mac OS X` 客户端上，前往屏幕顶部的 `Finder` 栏，选择“连接服务器”。出现 `Connect to Server` 窗口。

在客户端客户端，在地址框中输入共享目录的地址。例如，从 `jukebox.linxtoys.net` 连接到共享 `NFS` 目录 `/var/music`，你可以输入地址 `nfs://jukebox.linxtoys.net/var/music`（参见图 26-5）。

如果一切正常，代表服务器的图标应该出现在你的 `Mac OS X` 桌面上。根据你使用的 `Mac OS X` 版本，窗口可能会直接弹出显示目录内容，或者你可能需要打开它查看共享目录的内容。你可以像使用存在于 `Mac` 一样使用这些共享文件和目录

图 26-5：从 `Connect to Server` 窗口连接到 `NFS` 服务器。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_1053_0.png)

位于你的 `Mac` 上（如果服务器权限允许你这样做的话）。完成后，将图标拖入废纸篓。

> 注意：如果你无法连接到共享目录，请更仔细地查看第 18 章中的 `NFS` 步骤。特别是，请确保服务器上的防火墙端口已打开，并且用户和主机权限已设置为允许你所需的访问级别。

## 从命令行连接到 NFS

你可能完全无法控制 `Linux NFS` 服务器的配置。因此，如果没有设置 `insecure` 选项，你将无法从 `Mac` 的“连接到服务器”挂载目录。一种可能的变通方法是在 `Mac OS X` 上使用安全端口从手动挂载 `NFS` 目录。方法如下：

- 1. 在 `Mac OS X` 上，按照以下步骤获取 `root` 用户账户的访问权限：

    a. 选中文件夹图标，选择 访问 $\rightarrow$ 应用程序 (`Applications`)。将出现应用程序文件夹。

    b. 打开实用工具 (`Utilities`) 文件夹，然后打开 `NetInfo Manager` 实用。

    c. 点击 `NetInfo Manager` 窗口上的锁头图标进行解锁。

    d. 选择 $\rightarrow$ `Root User` (`Root User`)。如果看到 `NetInfo` 错误，点击确定）。

    e. 输入并验证新的 `root` 密码，然后点击验证。（记住那个密码！）

    f. 点击已打开的锁头图标将其关闭，以防止进一步更改。

- 2. 在 `Mac OS X` 上，点击终端 (`Terminal`) 图标打开 `shell` 并以 `root` 身份登录：

```bash
$ su -
Password: *************
```

- 3. 创建一个允许想要在 `Mac` 上使用共享 `NFS` 目录的用户账户访问的目录。例如，对于用户 `chris`，你可能输入：

```bash
# mkdir /Users/chris/music
# chown chris /Users/chris/music
```

- 4. 在你创建的目录上挂载 `NFS` 共享目录。例如：

```bash
# mount -o "-P" jukebox.linuxtoys.net:/var/music /Users/chris/music
```

`-P` 表示使用特权端口。将 `jukebox.linuxtoys.net` 和 `/var/music` 分别替换为服务器名称和共享目录。用户现在可以从 `Mac OS X` 客户端上的 `/Users/chris/music` 目录访问 `/var/music`。

## 在基于 Intel 的 Mac 上安装 Fedora

`Apple` 电脑采用 `Intel` 计算机架构。`Fedora` 项目已经增强了 `Fedora`，使其能够（通过自身安装或与 `Mac OS X` 双启动）安装在这些新硬件上。你可能想在任何这些“Macel”电脑上安装 `Fedora` 的原因：

- 双启动 —— 你可能喜欢 `Mac OS X` 的桌面（`Aqua`）以及专有应用程序（如 `iPod` 或 `iTunes`）供自己或家人使用。然而，你可能希望访问服务器应用程序、管理工具、开发环境或通过 `Fedora` 获取的数千个免费应用程序。

- 仅 `Fedora` —— 虽然你为 `Apple` 硬件支付了溢价（尽管以前那么贵），但你可能足够喜欢这些功能以及可爱的 `Apple Mac` 电脑，愿意多花钱将其作为主桌面电脑。

本节描述了如何从基于 `Intel` 的 `Apple Mac` 电脑开始（我在此使用了一台 `Mac Mini`）并将其配置为与 `Mac OS X` 双启动或运行在 `Fedora` 上。

> 警告：在 `Intel` 硬件上安装 `Fedora` 在 `Fedora` 社区中仍然是一项实验性技术。某些硬件仍然需要额外的调整，或者根本无法工作。如果你无法承担磁盘可能被抹除且从头开始重新安装风险，我建议你不要执行此程序。

### 在你的 Mac 上安装 Fedora 之前

首先提醒一下，此程序仅适用于基于 `Intel` 架构的 `Apple Mac` 电脑。我在这台新的 `Mac Mini 1.1`（`Intel Core Duo CPU`，`512MB RAM`）上运行了此程序。然而，相同的程序也适用于基于 `Intel` 的 `iMac`、`MacBook`、`MacBook Pro` 或 `Mac Pro` 电脑。

此程序不适用于 `PowerPC` 架构的 `Mac`。`Fedora` 支持此类配置，但你需要从 `Fedora` 下载 `pcs` 安装介质，而不是使用随附的 `DVD`。（获取用于在 `PowerPC` 上安装的介质，请访问 http://fedaproject.org/wiki/Distribution/）。当你购买 `Mac` 时，硬盘被专门用于 `Mac OS`。为了保留你的[此处缺失]，你需要减少 `Mac OS X` 占用的空间。然后，你需要使用该空间创建一个或多个分区来安装 `Fedora`。

尽管调整磁盘大小和重新划分分区的操作相当安全，但仍存在损坏你的 `Mac OS X` 分区或使机器（临时）无法启动的风险。因此，在开始接下来的步骤之前，请……备份任何重要数据！

`Mac OS X Leopard` 提供了一个名为 `Boot Camp` 的工具，可以调整 `Mac` 硬盘的大小（使用默认的 `HFS+` 文件系统）。在 `Leopard` 发布之前，`Boot Camp` 的测试版本可以从 `Apple` 免费下载。以下步骤描述了如何更新固件、调整磁盘大小并安装 `Fedora`。

> 注意：由于 `Leopard` 之前的 `Mac OS X` 版本不再提供 `Boot Camp`，因此没有官方方法可以调整你的磁盘以允许在 `Mac` 上进行多系统启动。然而，从理论上讲，你应该能够使用支持 `HFS+` 调整的分区工具来准备磁盘，以便在与 `Mac OS` 并存的同时安装 `Fedora`。请参阅第 2 章有关如何使用 `GPTart` 调整分区（如 `HFS+` 分区）的信息。如果你决定尝试，其结果不作任何保证。（换句话说，后果自自负。）

- 插入 `Fedora DVD` —— 完成分区后，，不要按照要求插入 `Windows` 安装光盘，而是插入 `Fedora` 安装光盘或 `DVD` 并重启 `Mac OS X` 或安装 `Windows` 以重启电脑。重启时，你应该能看到 `Fedora` 安装程序的启动界面。

- 重启并按住 `Alt` 键 —— 当 `Fedora` 安装完成后，重启。在机器重启时按住 `Alt` 键。当你看到 `Boot Camp` 菜单时，选择 `Windows`，电脑将启动到 `Fedora`。只需使用 `Fedora` 的默认启动项，因为尝试更改 `GRUB` 可能会导致电脑锁定。

如果由于某种原因你手头没有 `DVD`，可以从 `Fedora` 项目网站 http://fedaproject.org 下载镜像和安装 `CD` 及 `DVD`。如果你局域网内的另一台电脑上有 `DVD` 驱动器，请参阅第 2 章有关设置 `Fedora` 安装程序的信息，以便通过局域网在目标机器上安装 `Fedora`。

### 总结

## 26 章：将 Fedora 与 Apple Mac 集成
