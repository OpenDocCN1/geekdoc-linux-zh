
这种发行版支持从 ISO 启动，但语法可能很复杂。你只需要创建一个 40 案例——

这里这里是 Ubuntu live CD

注意变量 `isofile` 的使用，两种方法都可行，但这种方法更容易维护。

# 多启动

在使用 Windows 时，你可以通过在 `/etc/default/grub` 中使用以下设置来防止这些菜单项：
`GRUB_DISABLE_OS_PROBER=false`
作为 Windows 的另一种选择，如果你不想让它启动 Windows，可以重命名出现在其他条目之前的链式加载处理器（chainloader handler），例如通过编辑 `grub.cfg` 来禁用或删除你的 Windows 条目以更改文件的禁用状态。

![](img/1e7c2db42dac866a51a0ace7df48feef_126_0.png)

## 共享空间

我们有多个和谐共存的发行版，但我们的数据呢？我们需要为每个发行版单独分离 `/home` 吗？简单来说的回答是：不需要。虽然我们可以为 `/home` 创建独立的文件系统并共享相同的用户名和目录，但这运行良好良好。程序将其配置存储在 `/home` 目录中，如果你有两个拥有相同程序不同版本的发行版，它会乐意地读取一个版本的设置并更新它们，而当你切换回旧版本的发行版时，可能会导致问题。

如果你希望数据完全分离，一种解决方案是为数据分离你的文件。你也可以在主目录下创建一个独立的 `/home` 目录，但在这种情况下，你将在发行版之间进行大量的切换，这可能不再符合你的习惯。

> 你发现通过在 GParted 中调整分区大小来使用所有可用空间进行安装更加简单。

要做到这一点，我们需要进入 GParted 并调整分区大小，为数据创建一个大分区。然后在每个发行版上编辑 `/etc/fstab` 来挂载该分区，并为其他发行版添加条目，例如在 `/mnt/data` - 它看起来像这样：

所以现在，当你文档（Documents）中有一个文件时，它将位于 `/mnt/common/Documents` 并供你所有的发行版使用。这假设你在所有发行版上使用相同的用户名。

## 归所有

现在我们必须处理文件权限和所有权问题。为了让 `/mnt/common` 工作，我们需要运行：
`sudo chown -R user:user /mnt/common`

你可能认为如果你在每个发行版中创建了同名的用户，这适用于所有用户，但 Linux 并不关心名称，而是关心用户 ID (`UID`)。你使用的第一个发行版会给你用户的 UID，所以你应该检查每个发行版中的 ID，并让它们匹配。

找到你用户所在的行，它看起来像这样：
`uid=1000(user) /home/user`

接下来是 ID。将其更改以匹配其他发行版和文件。我们需要将所有由旧 ID 拥有的文件改为新 ID。在你的主目录下，该目录应该属于你，采取粗暴的方法并选择其中的所有内容。

![](img/1e7c2db42dac866a51a0ace7df48feef_126_1.png)

`/etc/fstab`

```
# 使用 "uuid" 打印设备的通用唯一标识符；这可能使用 UUID 作为根挂载方法，当磁盘连接和移除时该方法有效。(fstab)

# 文件系统 <mount> <options> <dump> <pass>

# 安装期间的 /dev/sda5

UUID=550e8400-e29b-41d4-a716-446655440000 / ext4 0 0

errors=root=ro

安装期间的 /dev/sda6

UUID=7b82a4f5-c2e4-4572-b2d3-88fbd9ff2e0544 / ext4 0 0

/dev/sd0 /media/photo rw,noauto,exec,utf8 0 0

/dev/sda2 /mnt/common noatime 0 0

/dev/sda7 /home noatime 0 0

/dev/sda8 /mnt/party noatime 0 0

/dev/sda9 /fedora defaults 0 0

/dev/sda1 /windows ntfs 0 0
```

> 对于额外的条目编辑 `/etc/fstab` 到你发行版的分区。

# 极客技巧

## 如何构建你自己的自定义 Ubuntu 发行版

为什么不满足发行版所提供的的内容呢？Michael Reed 探索了 Cubic，这是一个基于 Ubuntu 创建自己的自定义重制版（respin）的工具。

![](img/1e7c2db42dac866a51a0ace7df48feef_127_0.png)

Linux 的美之处在于发行版提供的部署自由，但当事情……时。所以，为什么不制作你自己的，或者重制一个呢？Cubic 是标准的 Ubuntu 界面，允许为你自己或你想要更改、修改的标准 Ubuntu ISO 安装它，并从 ISO 启动。

专家
Michael Reed 自从像个回光灯一样就开始使用 Linux 了。对，对，圆。

至于难度，如果你能从命令行安装软件包并在虚拟机中从 ISO 启动，你会发现开始使用 Cubic 非常简单。

根据我们的经验，我们将从最简单的示例开始，添加一些新软件包并重新构建 Cubic ISO，用作或桌面环境。

一旦运行正常，我们将向你展示如何通过将 Cubic 设置为默认环境、自定义该环境并添加 PPA，让你的重制版完全符合你的喜好。

快速上手
当你修改一个发行版创建一个现场环境时，使用 Cubic。这个 Cubic 非常适合制作一个包含你所需工具的可启动 ISO。启动时只需“尝试 Cubic”。

### Cubic

Cubic 允许你运行任何选择的 Ubuntu 或 Linux Mint 发行版。如果你正在运行不同的发行版，可以通过在虚拟机中运行 Ubuntu 来使用 Cubic 分发你自己的。

```
查找 Cubic，在 Launchpad (https://launchpad.net/cubic-project) 上通过复制并粘贴页面上的命令：sudo apt-add-repository ppa:cubic-release && sudo apt install cubic
```
