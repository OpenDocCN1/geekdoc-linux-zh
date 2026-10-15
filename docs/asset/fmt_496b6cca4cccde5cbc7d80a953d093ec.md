
在深入对现有硬盘进行分区之前，了解你拥有的资源是个好主意。如果你已经在现有硬盘上运行了 Microsoft Windows，你可以使用 Windows 自带的实用工具来检查你的系统。

Windows 计算机管理控制台提供了一个图形化工具，用于查看工作站上安装的硬盘。该工具在 Windows 2000 Workstation、XP 和 Vista 中可用。你可以通过以下步骤访问它：

1. 右键单击桌面上的我的电脑图标或开始菜单中的我的电脑条目。
2. 从 resulting 菜单中选择管理。这将启动计算机管理工具窗口。
3. 从计算机管理工具窗口中，选择磁盘管理条目。

磁盘管理工具，如图 3-3 所示，出现，显示当前安装在 PC 上的硬盘。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_84_0.png)

磁盘管理工具显示 Windows 识别的所有硬盘，并显示它们是否已格式化并使用。每个硬盘在列表中作为单独一行出现，并显示已识别的分区和格式类型。

许多较新的工作站利用隐藏分区来存储重要的恢复信息。隐藏分区是硬盘上被操作系统分区但未分配驱动器号的部分。即使你在 Windows 设置中只看到 C: 驱动器，你的硬盘仍可能包含两个分区，如图 3-3 中的示例所示。隐藏分区不能用于 Ubuntu，否则你将失去在 Windows 系统崩溃时恢复系统的能力。

如果你在硬盘上看到标记为未分配的区域，这意味着硬盘上有未属于 Windows 分区的空闲空间。你可以将此空间用作 Ubuntu 分区的一部分。如果它大于或等于 4 GB，那么你无需对现有的 Windows 分区做任何操作。你可以直接将 Ubuntu 安装到未分配的硬盘区域，而无需更改现有的 Windows 分区。

如果你的硬盘上只有一个分配给 Windows 的分区，你将需要继续分区过程以释放 Ubuntu 的空间。

### 确定可用空间

分区过程中的下一步是确定现有硬盘上有多少可用空间。请记住，你至少需要 4 GB 的可用空间用于 Ubuntu，而且你可能还想为原始操作系统保留一些额外的可用空间。

要了解 Windows 分区上可用多少可用空间，你可以再次使用 Windows 计算机管理工具。磁盘管理窗口的上部显示每个硬盘分区的详细统计信息。

显示的统计信息包括分区的总大小和可用空间量。请记下分区上可用的可用空间。这就是你将在现有 Windows 分区和新的 Ubuntu 分区之间分配的空间量。

> 一个常见的错误是将硬盘上的所有可用空间分配给新的 Ubuntu 分区。你需要为 Windows 分区保留一些可用空间；否则，已安装的 Windows 操作系统可能无法正常启动。即使你不打算添加任何新软件或数据，也最好在 Windows 分区上至少保留 1 GB 的可用空间。

一旦你确定了可用于 Ubuntu 的空间量，下一步就是确保磁盘上的空间确实是空的。

### 文件碎片整理

在正常使用工作站的过程中，Windows 倾向于将文件写入硬盘上的随机位置。这可能会使数据分散在整个磁盘空间区域。当你将硬盘分割成分区时，你需要确保不会丢失 Windows 系统中使用的数据，包括系统文件和数据文件。

为了对硬盘进行干净的分区，你需要确保所有 Windows 数据都移向硬盘的一端。此过程通常使用碎片整理工具完成。

# Part 1: Starting Out with Ubuntu

## Select a Language

When you start the Ubuntu installation, the first window you get is the Language window, shown in Figure 3-5.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_87_0.png)

**Figure 3-5:** The Ubuntu language selection window.

This window asks you to select the language Ubuntu uses to display text messages during the installation process, and it sets the default language used when the operating system runs. However, this doesn't necessarily mean that all of the applications running on the system will use that language. Individual applications may or may not detect the default language configured in Ubuntu.

## Select a Time Zone

The second window in the installation process, shown in Figure 3-6, allows you to select the time zone for your area.

This window allows you to select your location via map or a drop-down list. Although selecting the time zone from the map sounds like a good idea, it can often be a challenge, depending on how many cities Ubuntu recognizes near your particular city.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_88_0.png)

### Figure 3-6: The time zone configuration window

Where are you?

Select a city in your country and time zone. If the indicated current time is incorrect even after selecting the correct time zone, you can adjust it after rebooting into the installed system.

Selected city: New York

Selected region: United States

Time zone: EDT (GMT-4:00)

Current time: 08:24:26 PM

Step 2 of 7

## Select a Keyboard

Next in the installation process is identifying the keyboard you'll use with the Ubuntu system. Although this may sound like a simple option, it can get complicated if you have a keyboard that includes special keys. Ubuntu recognizes hundreds of keyboard types and lists them all in the Keyboard Configuration window, shown in Figure 3-7.

### Figure 3-7: The Keyboard Configuration window.

Keyboard layout

Which layout is most similar to your keyboard?

- Syria
- Tajikistan
- Thailand
- Turkey
- USA
- Ukraine
- United Kingdom
- Uzbekistan
- Vietnam
- USA
- USA - Alternative international (former us_intl)
- USA - Classic Dvorak
- USA - Lolemak
- USA - Dvorak
- USA - Dvorak international
- USA - Group toggle on multiply/divide key
- USA - International (AltGr dead keys)
- USA - International (with dead keys)

You can type into this box to test your new keyboard layout.

Step 3 of 7

![](img/39e65eeb4f54001ede08c6114ae3cc6c_88_1.png)
