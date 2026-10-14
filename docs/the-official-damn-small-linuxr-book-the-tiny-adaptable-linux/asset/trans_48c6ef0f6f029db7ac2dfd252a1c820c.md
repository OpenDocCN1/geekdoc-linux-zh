

![](img/af53325d7f44568e4ab8_282_0.png)

图 13-1 在 DSL 中通过 Firefox 浏览器看到的 Edna 的默认配置。

另一个列出的目录是 Jukebox。它指向 /opt/mp3s，而该目录位于 DSL 启动时创建的 ramdisk 内。这意味着 /opt/mp3s 的大小受限于 DSL 分配的 RAM 空间。显然，这不是存放大量音乐的合适位置。大多数时候，用户希望访问硬盘上的音乐。幸运的是，有一个配置文件可以轻松编辑音乐路径。

## 编辑音乐路径

要让 Edna 指向正确的目录，你需要编辑 edna.conf 文件。该文件位于 /usr/share/edna/edna.conf。

你可以使用自己喜欢的编辑器打开它。在本示例中，你使用 Beaver 作为编辑器。你需要拥有超级用户 root 权限才能编辑此文档，如图 13-2 所示。

打开一个终端窗口并输入以下命令：

```
sudo beaver /usr/share/edna/edna.conf
```

# 图 13-2 打开 edna.conf 文件的 Beaver。

![](img/af53325d7f44568e4ab8_283_0.png)

对于大多数人来说，配置文件的默认值是可以的。你需要编辑的是第 56 行和第 57 行。

该部分应如下所示：

```
# Unix example:
dir1 = /mnt/cdrom = MP3 CDROM
dir2 = /opt/mp3s = Jukebox
```

如果你不打算从 CD 运行 MP3，可以在行首加上井号 # 来注释掉 dir1。你可以自由地在服务器文件路径中添加和删除目录，Edna 会自动调整以包含或排除它们。但是，在 Edna 运行后，如果你更改了文件路径，就必须重启服务器才能使其重新读取配置文件。最简单的方法是给出一个命令行命令来重启服务器。此过程也会重启你正在运行的任何其他 Python 脚本。注意：Damn Small Linux 没有任何原生 Python 脚本，所以除非你是一个 Python 黑客，否则应该是安全的；如果你是，那你为什么要读这篇 How To？

要重启 Edna，输入：

```
sudo killall -HUP python
```

如果你将音乐保存在特定驱动器上，就需要配置 Edna 去查找该驱动器上的目录。请注意，驱动器需要先挂载。

以下是配置文件中访问硬盘音乐的示例条目：

```
dir3 = /mnt/hda1/music/ = Hard Drive Tunes
```

以下是音乐存储在 U 盘上的示例：

```
dir4 = /mnt/sda1/mp3s_and_oggs/ = My Portable Music
```

如果你使用 DSL 的电脑同时也是 MS Windows 机器，并且将音乐存储在 Windows 那一边，你应该能够挂载 Windows 分区并让 Edna 指向音乐的正确路径。只需记住路径应为 /mnt 加上驱动器和 Windows 操作系统所在的分区路径，再加上音乐的物理路径，而非 MS Explorer 给出的虚拟路径。如果你对 Windows 分区上音乐的真实路径有任何疑问，可以挂载驱动器，然后在文件管理器 Emelfm 中导航到该目录。你会注意到 Emelfm 在导航时会显示完整目录路径——你可以用它作为参考。务必在尝试导航前先挂载驱动器，否则你将看不到任何内容！

## 设置演练

在本演练中，我将使用从 archive.org 获取的公共领域音乐。顺便说一下，archive.org 有一个非常不错的免费音乐收藏，可以合法且免费地添加到你的音乐收藏中。这也是发现新音乐的好方法。好吧，回到正题。

在本演示中，我将在硬盘的第一个分区上创建一个目录树。我将很有创意地将其命名为 music。

因此，目录的初始路径为：

/mnt/hda1/music

接下来，我在 music 目录内创建几个目录：Live_Music、Grateful_Dead 和 Jazz。本演示我们保持简单。

