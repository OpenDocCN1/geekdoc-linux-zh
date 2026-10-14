
`/home` 文件夹可以放在单独的分区中。你不需要这样做，但如果发生故障并需要重新安装 Ubuntu，这将非常有用——你的个人文件和配置设置将保留在 home 分区，而 Ubuntu 将重新安装在根分区。这在恢复系统时可以节省大量工作。如果你没有单独的 home 分区，home 文件夹将与其他所有内容一起放在根分区。你访问主文件夹的方式（例如通过“位置”菜单）无论你是否将其放在单独的分区中都是完全一样的。

# 共享分区

如果你想用一种简单的方法在 Windows 和 Ubuntu 之间共享文件，可以创建一个共享分区。在两个操作系统中，它都将作为一个独立的硬盘出现，你可以用它来存储任何想要的内容。

根据你认为需要的大小来设置分区大小：如果你只是在 Ubuntu 和 Windows 之间传输一些小文件，那么 1GB 到 2GB 就足够了；如果你想将所有的 Windows 和 Ubuntu 文件永久地存储在其中（类似于一个共享文件夹），请将其设置得尽可能大越好。你应该选择 `FAT32` 作为文件系统，但挂载点可以使用几乎任何名称——`/windows` 是默认建议之一，但如果你喜欢，也可以在挂载点框中输入类似 `/shared` 或 `/blackhole` 的内容。只需确保使用的名称不包含任何空格即可。

# 分区布局示例

如果你以前从未做过分区，可能会感到困惑，我提供了一些分区布局示例，这应该会让情况变得更清晰。在所有这些示例中，我都使用了一个 100GB 的硬盘，但你可以根据第 416 页“分区的种类”中的建议，按你的硬盘放大或缩小所有分区的大小。

## 标准仅限 Ubuntu 安装

磁盘上将只安装 Ubuntu，只需要根分区和交换分区（swap partition）（图 C-5）。因为我有 4GB 内存，所以我将交换分区设为 4.2GB。根分区填充了磁盘的剩余空间，以便为文件和程序留出尽可能的空间（在这种情况下，没有必要手动划分磁盘；Ubuntu 安装程序的“删除并使用整个磁盘”选项也可以实现相同的结果）。

## 带有独立 Home 分区的仅限 Ubuntu 安装

只安装 Ubuntu，但会有一个独立的家（home）分区，以防我可能需要重新安装系统时保持我的数据安全（图 C-6）。我计划在其中存储家录电影，这意味着会有很多非常大的文件，所以我选择了一个较小的 10GB 根分区和一个略微偏小的 4GB 交换分区。这为家 分区（以及我的视频）留下了更多空间，它占据了磁盘剩余的 86GB 空间。

![](img/58abec7ac6c22ade6357fd77ea421da3_455_0.png)

图 C-5：简单的仅限 Ubuntu 分区布局

![](img/58abec7ac6c22ade6357fd77ea421da3_455_1.png)

图 C-6：带有独立家 分区的 Ubuntu 分区布局

手动划分你的硬盘 419

## 带有共享分区的 Ubuntu 和 Windows

Ubuntu 将与 Windows XP 一起安装，我想要一个共享分区，以便在两个操作系统之间复制文件（图 7）。我现有的 Windows 安装占用了磁盘的 7.3GB，因为我在上面安装了文件和程序。我将 Windows 安装调整大小为 15GB，留下了 7.7GB 的空间以备未来扩展。请注意，Windows 分区不会被格式化，该分区上的所有文件将保持完好。我创建了一个 40GB 的 Ubuntu 根分区和一个 4.2GB 的交换分区，然后在剩余的约 40GB 磁盘空间创建了一个共享的 `FAT32` 分区。

![](img/58abec7ac6c22ade6357fd77ea421da3_456_0.png)

图 7：Ubuntu、Windows 和共享分区

# 完成

完成后，点击 `Forward`（向前）以完成并应用你的更改。如果你正在删除或格式化分区，更改将写入磁盘。这是一个不可逆的更改，所以请确保你已经备份了受影响分区上的任何价值数据！

# D

# 资源

![](img/58abec7ac6c22ade6357fd77ea421da3_457_0.png)

由于 Linux 的增长和发展很大程度上归功于互联网，因此在网上可以找到关于 Linux 各种发行版（包括 Ubuntu）的丰富信息，这并不意外。除了常见的新、教程和下载网站外，你还会发现各种教程、论坛、博客和其他有用信息的来源——在你在使用和更多地学习系统时，都可以向这些资源寻求帮助。

## 论坛

当你寻找建议、尝试解决某个特定问题，或只是在寻找一些通用技巧时，在线论坛是最好的选择。坦率地说，Ubuntu 有它自己的论坛，而且由于 Ubuntu 主要是一个面向桌面的 Linux 发行版，你很可能在那里发现许多同为新手以及对新手友好的发帖者，而不是在某些其他网站上可能看到的硬核极客风格。当然，还有其他对新手友好的论坛，虽然它们不是专门针对 Ubuntu 的，但也能为你提供很多有用的信息。

无论你在哪个论坛发帖，请务必提到你正在使用 Ubuntu（如果你忘记了，版本是 Lucid Lynx），以及你是 Linux 新手。记住，当你得到一个你不理解的答案时，要请求进一步说明。同一个发帖者会回来为你解释清楚。在大多数这些网站上，你都会感到宾至如归，尽管你可能比比其他网站更地熟悉其中一或两个。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。

http://ubuntuforums.org/ 这是官方的 Ubuntu 社区论坛。
