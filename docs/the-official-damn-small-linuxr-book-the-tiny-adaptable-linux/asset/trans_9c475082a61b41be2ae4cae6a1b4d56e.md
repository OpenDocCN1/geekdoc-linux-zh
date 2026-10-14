

此时，你的工作目录应包含以下文件和目录：

- .bash_profile
- bootfloppy.img
- ds1.vmx.txt
- gnu/
- iso/
- makecd
- makeimage
- makeqemu
- makesys
- makevmx
- master/
- qemu/
- release.txt
- setupFromCD
- source/
- vmware/

## Making Modifications, Additions, and Removals

有两种方法可以访问 DSL 系统进行修改、添加或删除。第一种方法是直接方法；第二种方法称为 chroot。

## Changing Content with the Direct Method

使用完整路径来标识你的 KNOPPIX 源的位置，或将该目录更改为你的当前工作目录。例如，如果你的 remaster 目录位于 /mnt/hda4 分区上，你可以输入：

```
# cd /mnt/hda4/remaster/source/KNOPPIX
```

通常，我会更改我挂载的磁盘分区上的工作目录（例如，cd /mnt/hda4/remaster），然后我为访问新源映像文件的前缀命令加上 source/KNOPPIX。从这一点开始，我的讨论将始终使用相对于工作目录的路径——即包含脚本、master、source 和 iso 目录的目录。

我主要使用直接方法。DSL 并非纯 Debian。许多软件包、二进制文件和脚本都不是来自 Debian 仓库。由于这一点，以及使用 Debian 通常会添加许多其他不需要的软件包的事实，直接方法通常被使用。

大多数时候，新应用程序、脚本和修改首先应用于一个 live DSL CD-ROM 或 frugal 系统。通常，这些添加可以制作成 MyDSL 扩展，并且在完全测试后，只需使用 tar -C source/KNOPPIX 选项即可直接提取。另一个我经常使用的方法是将新的 tar 文件复制到 source/KNOPPIX，然后稍后 chroot 进入并像往常一样进行 tar 解压。只需确保不要忘记删除位于 chroot 环境根目录（/）的 tar 文件。

使用这种风格可以非常严格地控制添加到 50MB 核心 DSL 系统中的内容、更改的内容或删除的内容。

## Changing Content with the chroot Method

你现在准备好发出 chroot 命令了。chroot 方法会将根（/）目录更改为包含源文件的目录：

```
# chroot source/KNOPPIX
```

此时，新的根目录现在指向 DSL 映像的“根”。所有复制、移动或删除文件的操作都相对于此目录。请务必在继续 remastering 过程之前退出此 chroot 环境！

最常见的是，当讨论 KNOPPIX remastering 时，通常使用的是 chroot 方法。使用此方法，你可以访问源目录，就好像它实际上是根文件系统一样。这意味着你会看到 /mnt/hda4/remaster/source/KNOPPIX 就好像它是 /。你现在可以完全以 root shell 访问将成为新映像根目录的内容。

要安装某些软件包，你需要挂载 proc 文件系统：

```
# mount -t proc /proc proc
```

很可能，你想从 Debian Woody 仓库安装软件。为此，你需要 Internet 访问。通过 ping 一个知名服务器来测试你的 Internet 连接：

```
# ping www.yahoo.com
```

现在，你准备好安装 Woody 软件包了。如果你知道你想要来自其他 Debian 仓库的软件包，请编辑 `/etc/apt/sources.list` 文件。以下是 `sources.list` 文件内容的示例：

```
deb http://archive.debian.org/debian-archive/ woody main contrib non-free
#deb http://mirror.arrnet.edu.au/debian oldstable main contrib non-free
#deb http://mirror.linux.org.au/debian oldstable main contrib non-free
#deb http://mirrors.usg.edu/pub/linux/distributions/debian oldstable
main contrib non-free
```

软件包 Zile 在第 10 章中被用作示例，说明如何使用 MyDSL 设施在 Damn Small Linux 中安装软件包。MyDSL 是在 DSL 中安装软件的正常方法。另一种在 DSL 中安装 Zile 软件的方法是使用以下命令：

```
# apt-get install zile
```

上述过程在 KNOPPIX 风格的 live CD-ROM 系统中最为常见。在 DSL 中通常不使用它。原因与第 5 章和第 10 章中所述相同。使用软件包管理器可能会迅速违背 DSL 的“小而美”格言。

正如第 10 章所示，许多 Debian 软件包首先被精简为 MyDSL 扩展，然后通过直接方法加载到 DSL 核心映像中。

> **NOTE**
> 
> 如果你已挂载 proc 文件系统，请务必在退出 chroot 环境之前卸载它。

## Adding Common Elements: Menu and Icon

由于 DSL 通常不使用 Debian 软件包，菜单项和图标必须手动创建。这一区域在第 10 章中已进行了详细讨论。这次，与基于 `/tmp` 和 `/home/dsl/.xtdesktop` 不同，你必须编辑以下文件：

```
/etc/skel/.fluxbox/menu
/etc/skel/.jwmrc
/etc/skel/.xtdesktop/
```
