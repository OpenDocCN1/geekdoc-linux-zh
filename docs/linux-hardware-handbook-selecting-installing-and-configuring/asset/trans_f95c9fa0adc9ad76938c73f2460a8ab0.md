
在发布之前，您应该在 Deja News (http://www.deja.com/usenet/) 上搜索类似的问题。该网站归档了 Usenet News 帖子，并允许您搜索近期和较旧帖子中的关键字。

## 安装 Linux

在已包含 Windows 的计算机上安装 Linux，需要为 Linux 提供磁盘空间。实现这一目标的一种方法是购买第二块硬盘。然后，您可以将一块磁盘专门用于 Windows，另一块用于 Linux。但是，如果您不想购买新的硬盘，则必须重新分配 Windows 占用的磁盘空间，以便 Linux 可以使用该空间。最简单的做法是彻底移除 Windows。然而，如果您希望保留 Windows 和 Linux 两者，则必须找到一种方法来缩小 Windows 安装所占的空间，以便安装 Linux。

> **注意**
>
> 某些 Linux 发行版可以安装到 Windows 分区中，从而免去了重新划分硬盘分区的必要。但是，我不建议您使用此选项。以这种方式安装时，Linux 的磁盘性能会受到影响，而且通常不如安装到专用 Linux 分区时可靠。正如我稍后将要描述的那样，由于重新划分分区的工具已随处可得，将 Linux 安装到 Windows 分区的理由几乎很少。

## 移除 Windows

如果您希望将该计算机完全用于 Linux，您可以从机器上移除 Windows。实现此目的的最简单方法是使用 Linux 发行版在安装过程中提供的任何分区工具。例如，图 21.2 显示了 Corel Linux 1.0 安装中的分区工具。要移除 Windows 所在的 FAT-32 分区，请单击其名称（`/dev/hda1`），然后单击删除。然后，您可以选择整个硬盘（`/dev/hda`）并单击添加，以创建新的 Linux 分区。

具体如何执行这些操作因 Linux 发行版而异，因此上述描述的细节可能不适用于您的发行版。不过，基本原理是相同的。

一些发行版包含选项，使发行版自动接管整个硬盘。如果您希望快速安装 Linux，并采用发行版偏好的默认分区方案，此功能可能很方便。但是，如果您想要更精细的控制，应选择自定义分区选项。

![](img/860d0c38bd76c9ded976e9d1e179ef25_587_0.png)

大多数 Linux 发行版允许您在安装期间删除和添加分区。

有关 Linux 安装的更多详细信息，请参阅您发行版的文档或关于您想要使用的发行版的书籍。

## 缩小 Windows

如果您希望在计算机上保留 Windows，最佳选择是使用分区调整程序缩小 Windows 分区，以为 Linux 腾出空间。目前有多种这样的程序可用，包括：

- **FIPS** 首个非破坏性交互分区大小调整（FIPS）程序是一个简单的 DOS 实用工具，可以将 FAT 分区拆分为两个分区。要使用它，您必须将计算机引导到 DOS 模式。FIPS 很有用，但在许多方面受到限制。其用户界面简陋，且只能将一个主分区拆分为两部分。您不能使用 FIPS 来增加分区大小，也不能处理非 FAT 分区，而新计算机如果预装 Windows 2000 可能就需要这样做。大多数 Linux 发行版都附带 FIPS，这是一个开源程序。
- **PartitionMagic** 图 21.3 中显示的 PartitionMagic 程序是一个非常灵活的分区调整器。您可以使用它来缩小、扩展、移动、复制、创建和删除 FAT、NTFS、HPFS 和 ext2fs 分区。5.0 版可以处理 Windows 2000 的 NTFS 5，但早期版本只能处理 Windows NT 4.0 及更早版本使用的旧版 NTFS。如果您希望维护多操作系统计算机，PartitionMagic 非常值得拥有。它是商业软件，可从 PowerQuest (http://www.powerquest.com) 获取。

![](img/860d0c38bd76c9ded976e9d1e179ef25_588_0.png)

图 21.3

PartitionMagic 为高级分区操作工具提供了易于使用的界面。

- System Commander 2000 V Communications (http://www.v-com.com) 提供两款与 PartitionMagic 竞争的产品：System Commander 2000 和 Partition Commander。前者更为完整；它可以调整 FAT、NTFS 和 ext2fs 分区的大小，而 Partition Commander 只能调整 FAT 分区的大小。这两款产品都无法处理 OS/2 的 HPFS 分区。System Commander 2000 包含一个功能强大的引导加载程序，因此您可以在安装于单台计算机上的多个操作系统之间进行选择。与 PartitionMagic 类似，这些也是商业产品。
- Ranish Partition Manager 该程序可从 http://www.users.interco.com/-ranish/part/ 获取，是一款共享软件分区管理器，其功能大致相当于 Partition Commander。它可以调整 FAT 分区的大小，但不能移动它们，也不能处理 Linux 的 ext2fs 分区。
- Linux 安装实用工具 Linux Mandrake 7.0 的安装例程中包含分区调整功能。您可以在安装期间调整 FAT 或 Linux ext2fs 分区的大小，这可以大大简化安装过程。

一些发行版，如 Corel Linux 1.0 (http://linux.corel.com) 和 SuSE Linux 6.3 (http://www.suse.com)，坚持创建它们自己的 Linux 分区。其他发行版，如 Linux Mandrake 7.0 (http://www.linux-mandrake.com)，则乐意安装到现有的 Linux 分区中，例如您可能在 PartitionMagic 中创建的分区。如果您不确定您的发行版有何要求，您应该为 Linux 留空空间，而不是创建分区。

> **警告**
>
> 在您缩小其分区之前，我强烈建议您完全备份您的 Windows 安装。虽然分区缩小程序通常可靠，但偶尔仍会出现问题。当然，如果您刚刚收到该计算机，您可能有能力并愿意从紧急恢复 CD 中恢复系统。不过在继续之前，请务必确保您有恢复 CD。一些 PC 制造商为了节省制造成本而省略了此 CD。

## 获取 Linux 发行版

根据您对“主要”的定义不同，Linux 可从三家或多达十几家主要 Linux 供应商处获取。每家供应商都会获取一个 Linux 内核和大量关键 Linux 程序，将它们与安装程序捆绑在一起，并分发此捆绑包。由此产生的软件包被称为 Linux *发行版*。大多数发行版可通过多种方式获取：

- **作为互联网下载** 您可以从互联网下载站点获取大多数发行版，例如 `ftp://sunsite.unc.edu/pub/linux/distributions` 和 Linuxberg (`http://tzo.linux.twcous.com/distribution.html`)。以这种方式获取 Linux 的最简单方法是下载 CD-ROM *映像文件*并将其刻录到 CD-R 上，然后您可以使用它来安装 Linux。（您必须使用 CD-R 软件中称为“从映像文件创建 CD”或类似名称的选项。）当您以这种方式下载 Linux 时，您无法获得来自发行版供应商的技术支持。
- **低成本 CD-ROM** 许多 Linux 零售商，如 Linux Mall (`http://www.linuxmall.com`) 和 CheapBytes (`http://www.cheapbytes.com`)，以 $13-$3 的价格出售 CD 版 Linux。即使算上典型的 $5 运费，因此您也可以花不到 $10 买到一个 Linux 发行版——甚至两三个。与从互联网下载的版本一样，您以这种方式获取 Linux 时，也得不到技术支持或打印文档。
- **随书附带的 CD-ROM** 许多 Linux 入门书籍都附带一个 Linux CD-ROM。杂志偶尔也会通过 CD-ROM 分发 Linux。由于附带书籍，以这种方式购买 Linux 可能是学习操作系统的好方法。缺点是，出版延迟通常会导致书架上的书籍比最新的 Linux 发行版落后一个或两个版本。此类软件包通常也不附带技术支持。

