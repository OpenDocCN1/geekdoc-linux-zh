
这并不是说 ZFS 使用了革命性的技术。ZFS 的所有单独组成部分都是大家熟知的。哈希、数据树或索引没有任何神秘之处。但 ZFS 将这些充分理解的原则结合成一个单一、连贯且设计良好的整体。它是面向未来设计的。今天的哈希算法 15 年后可能不够用了，但 ZFS 的设计使得新的算法和技术可以添加到新版本中，而不失去向后兼容性。

本章不会涵盖关于 ZFS 的一切知识。ZFS 几乎是一个独立的操作系统，或者可能是一个专用数据库。已经有很多整本书专门讲述使用和管理工作 ZFS。不过，你将学习足够多的 ZFS 工作原理，以便在服务器上使用它，并理解其最重要的特性。

虽然 ZFS 预期直接安装在磁盘分区上，但你可以使用其他 `GEOM` 提供者作为 ZFS 存储。最常见的情况例如，当你使用加密磁盘进行安装时。`FreeBSD` 会在磁盘上放置一个 `geli(8)` `geom`，并在该 `geom` 之上安装 ZFS。本章将任何存储提供程序称为“磁盘”，即使它可能是一个文件或一个加密提供程序，或者是其他任何东西。

如果你从未使用过 ZFS，请在虚拟机上安装一个基于 ZFS 的 `FreeBSD` 系统并跟随操作进行练习。安装程序会自动处理先决条件，例如在 `loader.conf` 中设置 `zfs_load=YES`，以及在 `rc.local` 中设置 `zfs_enable=YES`；你只需要关心的是文件系统。

> **ZFS 代表什么？**
>
> `The Z File System`。是的，认真的。曾几何时，它的意思是 `Zettabyte File System`（泽塔字节文件系统），但那个首字母缩写已被弃用。

ZFS 将许多理解透彻的技术融合在一起，组合成一个卷管理器和文件系统的混合体。它期望处理从文件权限到跟踪哪些存储提供程序上的哪些块接收哪些信息等一切内容。作为系统管理员，你告诉 ZFS 你拥有什么硬件以及你希望如何配置它们，然后 ZFS 会接手后续工作。

ZFS 有三个主要组件：数据集、池和虚拟设备。

### 数据集

数据集被定义为 ZFS 数据的一个命名块。最常见类型的数据集类似于分区文件系统，但 ZFS 支持其他类型的数据集用于其他用途。快照（参见第 271 页的“Snapshots”）是一个数据集。ZFS 还包括用于虚拟化和 `iSCSI` 目标的块设备、克隆等；这些全部都是数据集。本书重点介绍文件系统数据集。传统的文件系统如 `UFS` 拥有各种小型程序来管理文件系统，但你通过 `zfs(8)` 管理所有的 ZFS 数据集。

使用 `zfs list` 查看你现有的数据集。输出看起来很像 `mount(8)`。

```
#### zfs list
NAME        USED  AVAIL  REFER  MOUNTPOINT
zroot      4.71G  894G   88K  none
zroot/ROOT 2.40G  894G   88K  none
zroot/ROOT/2018-11-17   8K   894G  1.51G /
zroot/ROOT/default 2.40G  894G  1.57G /
zroot/usr   1.95G  894G   88K  /usr
zroot/usr/home  520K   894G  520K /usr/home
--snip--
```

每一行以数据集名称开头，该名称以存储池（或 `zpool`）开头，即该数据集所在的池。第一个条目被称为 `zroot`。此条目代表池的根数据集。其余的数据集树都挂在这个数据集之下。

接下来的两列显示了已用空间和可用空间的大小。池 `zroot` 已使用 4.71GB，可用空间为 894GB。虽然可用空间肯定是正确的，但 4.71GB 看起来比实际复杂得多。数据集在 `USED` 列中显示的空间量包括该数据集及其所有子数据集上的所有内容。根数据集的子数据集包括该 `zpool` 中的所有其他数据集。

`REFER` 列是 ZFS 特有的。此列显示在此特定数据集中可访问的数据量，这并不一定等于已使用的空间量。某些 ZFS 功能，如快照，会在彼此之间共享数据。此数据集已使用 4.71GB 的数据，但仅引用 88KB。如果没有其子数据集，该数据集上仅有 88KB 的数据。

最后，我们有数据集的挂载点。这个根数据集没有挂载点；它未被挂载。

看看下一个数据集，`zroot/ROOT`。这是为根目录及相关文件创建的数据集。这看起来合情合理，但如果你查看 `REFER` 列，你会发现它内部也仅有 88KB 的数据，并且没有挂载点。难道根目录不应该存在吗？

接下来的两行解释了原因……大致如此。数据集 `zroot/ROOT/2018-11-17` 的挂载点为 `/`，因此它是一个真正的根目录。下一个数据集 `zroot/ROOT/default` 的挂载点也为 `/`。不，ZFS 不允许你将多个数据集挂载到同一个挂载点。一个 ZFS 数据集在数据集内部记录了大量设置。挂载点就是这些设置之一。

暂时考虑一下这四个数据集。`zroot/ROOT` 数据集是 `zroot` 数据集的子级。`zroot/ROOT/2018-11-17` 和 `zroot/ROOT/default` 数据集是 `zroot/ROOT` 的子级。每个数据集都会将其子数据集的空间使用情况计入自身。

为什么要这样做？当你启动一个 `FreeBSD` ZFS 主机时，你可以轻松地在多个根目录之间进行选择。每个可启动的根目录被称为一个*启动环境*（boot environment）。假设你应用了一个补丁并重启系统，但新系统无法启动。通过进入一个备用的启动环境，你可以轻松访问有缺陷的根目录并尝试找出问题所在。

下一个数据集 `zroot/usr` 是 `zroot` 的一个完全不同的子级。它有自己的子级 `zroot/usr/home`。`zroot/usr/home` 中使用的空间会记在 `zroot/usr` 账上，而两者都会记在其父级账上，但它们的分配不会影响 `zroot/ROOT`。

#### 数据集属性

除了某些记账技巧外，到目前为止，数据集看起来很像分区。但分区是磁盘的逻辑细分，在存储设备上填充非常特定的 `LBA`（逻辑块地址）。分区对分区上的数据没有感知。更改分区意味着摧毁其上的文件系统。

ZFS 将文件系统与底层存储层紧密集成。它可以动态地在各个文件系统之间分配存储空间，以满足需求。分区通过控制可用块的数量来限制磁盘使用，而数据集可以使用*配额*（quotas）达到相同的效果。不过，如果没有这些配额，如果池中有空间，你可以随意使用。

一个数据集可以使用的空间量是 ZFS 的一个*属性*（property）。ZFS 支持数十个属性，从控制数据集可以增长多快的 *quotas* 属性，到显示数据集是否已挂载的 *mounted* 属性。

#### 查看和更改数据集属性

使用 `zfs set` 更改属性。

```
##### zfs set quota=2G zroot/usr/home
```

使用 `zfs get` 查看属性。你可以指定某个特定属性，或使用 `all` 查看所有属性。你可以通过用逗号分隔来列出多个属性。如果你指定了一个数据集名称，你只影响该数据集。

```
##### zfs get mounted zroot/ROOT
```

| 名称 | 属性 | 值 | 来源 |
| :--- | :--- | :--- | :--- |
| zroot/ROOT | mounted | no | - |

在这里，我们有数据集的名称、属性、属性值，以及称为“来源”的东西。（我们将在第 261 页的“属性继承”中讨论最后这一点。）

我真正的问题是，哪个数据集被挂载为根目录？我可以检查那两个挂载点为 `/` 的数据集，但当我有几十个启动环境时，那会让我抓狂。通过添加 `-r` 标志来检查某个数据集及其所有子数据集的属性。

```
##### zfs get -r mounted zroot/ROOT
```

| 名称 | 属性 | 值 | 来源 |
| :--- | :--- | :--- | :--- |
| zroot/ROOT | mounted | no | - |
| zroot/ROOT/2018-11-17 | mounted | no | - |
| zroot/ROOT/default | mounted | yes | - |

在这三个数据集中，只有 `zroot/ROOT/default` 被挂载了。那是我们的活动启动环境。

#### 属性继承

许多属性是可继承的。你在父数据集上设置它们，它们会向下传递到子数据集中。对于像挂载点这样的属性，继承没有意义，但对于某些更高级的功能，它是正确的。虽然我们将在第 273 页的“压缩”中查看 `compression` 属性的作用，但我们在这里将其用作继承的例子。

```
##### zfs get compression
NAME PROPERTY VALUE SOURCE
zroot compression lz4 local
zroot/ROOT compression lz4 inherited from zroot
zroot/ROOT/2018-11-17 compression lz4 inherited from zroot
zroot/ROOT/default compression lz4 inherited from zroot
zroot/tmp compression lz4 inherited from zroot
-- snip --
```

根数据集 `zroot` 的 `compression` 属性设置为 `lz4`。来源是 `local`，意味着该属性是在此数据集上设置的。现在看看 `zroot/ROOT`。`compression` 属性也是 `lz4`，但来源是从 `zroot` 继承而来。这个数据集从其父级继承了此属性设置。

### 管理数据集

ZFS 使用数据集的方式与传统文件系统使用分区的方式类似。使用 `zfs(8)` 管理数据集。你将希望创建、删除和重命名数据集。

#### 创建数据集

使用 `zfs create` 创建数据集。通过指定池和数据集名称来创建文件系统数据集。在这里，我为我的包创建一个新数据集。（请注意，这会破坏启动环境，正如我们将在本章后面看到的。）

```
##### zfs create zroot/usr/local
```

每个数据集必须有一个父数据集。默认的 `FreeBSD` 安装有一个 `zroot/usr` 数据集，所以我可以创建 `zroot/usr/local`。我想为 `/var/db/pkg` 拥有一个数据集，虽然 `FreeBSD` 附带一个 `zroot/var`。

数据集方面，这里没有 `zroot/var/db`。我需要先创建 `zroot/var/db`，然后创建 `zroot/var/db/pkg`。

请注意，数据集是可以堆叠的，就像 `UFS` 一样。如果我在 `/usr/local` 目录中有文件，并针对该目录创建了一个数据集，ZFS 会将该数据集挂载到目录之上。我将无法访问那些文件。你必须移动文件以复制现有目录。

#### 销毁和重命名数据集

我之前创建的那个新的 `zroot/usr/local` 数据集？它隐藏了我 `/usr/local` 目录的内容。使用 `zfs destroy` 将其删除，然后重试。

```
##### zfs destroy zroot/usr/local
```

`/usr/local` 的内容重新出现了。或者，我可以使用 `zfs rename` 重命名该数据集。

```
##### zfs rename zroot/usr/local zroot/usr/new-local
```

不过，我更喜欢启动环境（boot environments），所以我不会动 `/usr/local`。尽管有时候你确实需要一个 `/usr/local` 数据集……

#### 未挂载的父数据集

作为一个 `Postgres` 用户，我希望为我的 `Postgres` 数据拥有一个独立的数据集。`FreeBSD` 的 `Postgres` 9.6 包使用 `/var/db/postgresql/data/96`。如果没有一个针对 `/var/db` 的数据集，我无法创建那个数据集；而且如果不破坏包的支持，我也无法拥有 *那个* 未挂载的父数据集。该怎么办？

解决方案是创建一个针对 `/var/db` 的数据集，但不使用它，方法是设置 `canmount` 数据集属性。该属性控制数据集是否可以被挂载。`FreeBSD` 正是出于这个原因，为 `/var` 使用了一个未挂载的数据集。新数据集默认将 `canmount` 设置为 `on`，因此通常你不需要担心它。使用 `-o` 标志可以在创建数据集时设置属性。

```
##### zfs create -o canmount=off zroot/var/db
```

`/var/db` 的数据集存在，但无法被挂载。检查你的 `/var/db` 目录内容以确认一切仍在那里。现在你可以为 `/var/db/postgres` 甚至 `/var/db/postgresql/data96` 创建数据集了。

```
##### zfs create zroot/var/db/postgres
##### zfs create zroot/var/db/postgres/data96
##### chown -R postgres:postgres /var/db/postgres
```

你为你的数据库拥有了一个数据集，并且 `/var/db` 本身的文件作为根数据集的一部分依然存在。现在初始化你的新 `Postgres` 数据库并继续吧！

在探索 ZFS 的过程中，你会发现许多场景，你可能希望在创建数据集时设置属性或使用未挂载的父数据集。

#### 将文件移动到新数据集

如果你需要为一个现有目录创建新数据集，你需要复制文件过来。我建议创建一个名称略有不同的新数据集，将文件复制到该数据集，重命名目录，然后重命名数据集。在这里，我需要一个针对 `/usr/local` 的数据集，所以我以不同的名称创建它。

```
##### zfs create zroot/usr/local/pgsql-new
```

使用 `tar(1)` 复制文件，正如你对新的 `UFS` 分区所做的那样（参见第 11 章）。

```
##### tar cfC - /usr/local/pgsql . | tar xpfC - /usr/local/pgsql-new
```

完成后，将旧目录移开并重命名数据集。

```
##### mv /usr/local/pgsql /usr/local/pgsql-old
##### zfs rename zroot/usr/local/pgsql-new zroot/usr/local/pgsql
```

我的 `Postgres` 数据现在位于其独立的数据集上。

### ZFS 存储池

ZFS 通过存储池（pool）而非磁盘来组织其底层存储。ZFS 存储池，或称为 `zpool`，是底层存储设备的抽象，允许你将物理介质与顶层对用户可见的文件系统分离。

使用 `zpool(8)` 查看和管理主机的 ZFS 存储池。这里，我使用 `zpool list` 来查看我其中一个主机的存储池。

```
#### zpool list
NAME      SIZE  ALLOC   FREE EXPANDSZ FRAG  CAP  DEDUP HEALTH ALTROOT
zroot     928G  4.72G   923G -        0%    0%   1.00x ONLINE -
jail      928G  2.70G   925G -        0%    0%   1.00x ONLINE -
scratch   928G  5.94G   922G -        0%    0%   1.00x ONLINE -
```

这个主机有三个存储池：`zroot`、`jail` 和 `scratch`。每个都占有一行。

`SIZE` 列显示了存储池的总容量。所有这些存储池都可以容纳 928GB。`ALLOC` 列显示了每个存储池的使用量，而 `FREE` 显示了剩余空间。这些磁盘几乎是空的，这很合理，因为我刚刚安装这个主机才大约三个小时。

`EXPANDSZ` 列显示了底层存储提供程序是否有空闲空间。当存储池具有虚拟设备冗余（我们在下一节中讨论）时，你可以替换存储池中的单个存储设备并扩大存储池的大小。这就像将 `RAID` 阵列中的 5TB 驱动器换成 10TB 驱动器以使其变大一样。

`FRAG` 列显示了该存储池的碎片程度。你听说过很多次碎片会降低性能。不过，ZFS 最小化了碎片的影响。

`CAP` 列显示了可用空间的使用百分比。

`DEDUP` 列显示了该存储池是否使用去重。虽然许多人推崇去重作为 ZFS 的一个功能，但它并不像你期望的那么有用。

`HEALTH` 列显示了存储池运行良好还是底层磁盘存在问题。

#### 存储池详情

通过运行 `zpool status`，你可以获取存储池或单个存储池的更多详细信息。如果你省略存储池名称，你将看到所有存储池的这些信息。这里，我检查我的 *jail* 存储池的状态。

```
##### zpool status jail
pool: jail
state: ONLINE
scan: none requested
config:
		NAME			STATE		READ WRITE CKSUM
		jail			ONLINE		0	0	0
		mirror-0		ONLINE		0	0	0
		gpt/da2-jail	ONLINE		0	0	0
		gpt/ada2-jail	ONLINE		0	0	0
	errors: No known data errors
```

我们从存储池名称开始。`state` 类似于 `HEALTH` 列；它显示存储池的任何问题。`scan` 字段显示关于数据清除（scrub）的信息（参见第 273 页的“存储池完整性和修复”）。

然后是存储池配置。配置显示了存储池中虚拟设备的布局。当我们创建存储池时，我们将深入探讨这一点。

#### 存储池属性

与数据集类似，`zpool` 也有属性来控制并显示存储池的设置。一些属性本质上是信息性的，例如 *free* 属性，它表达了存储池有多少空闲空间。你可以更改其他属性。

##### 查看存储池属性

要查看存储池的所有属性，使用 `zpool get`。添加属性 `all` 以查看每个属性。你可以添加存储池名称以仅包含该存储池。
