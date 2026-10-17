
`sudo beaver /usr/share/edna/edna.conf`

## 第 13 章 在 DSL 中制作 Edna 服务器

![](img/f6eecb623fe812080d8ad148db9eda3a_283_0.png)

图 13-2 打开了 `edna.conf` 文件的 Beaver。

配置文件的默认值适用于大多数人。你需要编辑的行是第 56 行和第 57 行。

该部分看起来应该是这样的：

```
# Unix 示例：
dir1 = /mnt/cdrom = MP3 CDROM
dir2 = /opt/mp3s = Jukebox
```

如果你不打算从 CD 运行 MP3，可以在行首使用符号（`#`）来注释掉 `dir1`。你可以自由地在服务器路径内添加和删除目录，Edna 会自动调整以包含或排除它们。然而，在 Edna 运行之后，如果你更改了文件路径，必须重启服务器以重新读取配置文件。最简单的方法是给出一个重启服务器的命令行命令。此过程也会重启你运行的其他 Python 脚本。注意：Damn Small Linux 没有任何原生的 Python 脚本，除非你是一个 Python 黑客，否则应该是安全的；如果你确实是黑客，你还在读这本教程吗？

要重启 Edna，输入：

```
sudo killall -HUP python
```

如果你将音乐保存在特定的驱动器上，你希望配置 Edna 查找该驱动器上的目录。请注意，需要先挂载驱动器。

以下是配置文件中访问硬盘音乐的示例条目：

```
dir3 = /mnt/hda1/music/ = Hard Drive Tunes
```

这是一个存储在优 盘上的音乐文件夹示例：

```
dir4 = /mnt/sda1/mp3_and_oggs/ = My Portable Music
```

如果你从一台兼作 MS Windows 机器的电脑上使用 DSL，并将音乐存储在 Windows 侧，你应该能够挂载你的 Windows 分区并将 Edna 指向音乐的正确路径。只需记住，路径应该是 `/mnt` 加上 Windows 操作系统所在的驱动器和分区通往音乐的物理路径（而不是 MS Explorer 资源管理器中的虚拟路径）。如果你对 Windows 分区上音乐的真实路径有任何疑问，可以挂载驱动器并在文件管理器 Elmfem 中导航到该目录。你会发现 Elmfem 在你导航时显示完整路径——你可以将其作为参考。在尝试导航之前一定要挂载驱动器，否则你什么都看不见！

### 设置演示

在本次演示中，我将使用从 archive.org 获取的公领域音乐。顺便说一下，archive.org 有非常丰富的免费音乐，可以合法且免费地添加到你的音乐收藏中。这也是发现新音乐的一种很棒方法。好了，回到正题。

对于这次演示，我将在硬盘的第一分区上创建一个目录树。它将原始并命名为 `music`。因此，目录的初始路径是：

`/mnt/hda1/music`

接下来，我在 `music` 目录内部创建了几个子目录：`Live_Music`、`Grateful_Dead` 和 `Jazz`。为了这次演示，我们保持简单。这些目录的完整路径看起来如下：

```
/mnt/hda1/music/Live_Music
/mnt/hda1/music/Grateful_Dead
/mnt/hda1/music/Jazz
```

因此，在 Edna 配置文件中，我的路径条目看起来如下：

```
dir1 = /mnt/hda1/music/Live_Music = Live Music
dir2 = /mnt/hda1/music/Grateful_Dead = Grateful Dead
dir3 = /mnt/hda1/music/Jazz = Jazz
```

在注释掉原始目录并添加我的条目后，使用 `sudo killall -HUP python` 重启服务器。为了确认一切顺利，请重新检查服务器中的显示。

![](img/f6eecb623fe812080d8ad148db9eda3a_285_0.png)

图 13-3 显示了新类别的 Edna。

获取初始目录路径后，你可以按照自己喜欢的方式填充它。你可以将音乐组织得深层层，也可以让目录保持浅而宽。你也可以混合使用，将一些音乐文件放在顶层目录，并使用广泛的子目录树来组织更有条性的音乐。在从 Archive.org 下载了几场音乐几分钟后，当你放入新的音乐或文件夹时，你可以看到 Edna 自动更新其音乐树。![](img/f6eecb623fe812080d8ad148db9eda3a_286_0.png)

图 13-4 显示了...

### 在 DSL 中制作 Edna 音乐服务器

以下是使用的语法：

```
# sshfs user@remote_address:/path/to/music/ /mnt/test/
```

接下来，按下回车键并像使用 SSH 或 SCP 一样输入密码。完成后，你的远程音乐（MP3、Ogg 文件等）就可以通过 `/mnt/test/path/to/music/` 访问了。你只需要将此路径添加到 Edna 配置文件并（重新）启动 Edna 即可。大搞定！现在，你可以访问你的曲子了，尽管那家伙试图阻碍你 :) 使用 SSHFS 和 Edna 的最大好处之一，是你还可以与网络上的其他人共享你的音乐。

以下是与之前的示例条保持一致的配置：

```
dir4 = /mnt/test/path/to/music/ = Remote Tunes
```

如果 Edna 已经在运行，你需要重新启动它才能识别远程文件。让我们向进程发送一个 HUP 信号来实现重启：

```
sudo killall -HUP python
```

现在，你应该能够在运行 DSL 的计算机上通过本地访问访问 `http://127.0.0.1:8080/Remote%20Tunes/` 上的远程文件了。局域网上的其他人也可以通过你的本地 IP 访问你的音乐。如果你不知道它，可以查看桌面右上角的 Torsmo 显示，或者打开终端窗口并输入 `/sbin/ifconfig`，寻找 `inet addr:` 之后不是“本地环回（local loopback）”或“lo”列表的四段数字。

例如，如果你的地址实际上是 `192.168.1.200`，局域网的人可以通过将浏览器指向 `http://192.168.1.200:8080/Remote%20Tunes` 来访问你的远程音乐。

### 总结

这些应该足够让你完成基础的 Edna 设置。你可以看到，有许多方法可以使用 Edna 来享受你的音乐或任何类型的音频文件。最后一个提示：如果你在音乐所在的目录中包含一张图片，Edna 在你访问时会显示该图片。这可能是为你的音乐服务器增添个性的方法。

## 在 DSL 中使用 Skype VoIP 服务

通过向 Damn Small Linux (DSL) 中添加 Skype 软件，你可以免费从电脑拨打给另一台电脑（DSL）上的人，或者拨打世界上任何一个电话（需要花一点钱）。你还可以使用文字聊天与其他 Skype 用户通信。

Skype 软件不仅适用于 Linux，还提供 Windows、Mac OS X 和 Pocket PC 版本。因此，如果你能找出一群朋友或同事注册 Skype 账户，你就可以在这些人群之间拨打电话、发送文件并参与聊天，即使他们没有使用相同类型的计算机。

由于 Skype 软件已经针对 Damn Small Linux 进行了封装，你可以使用 MyDSL 功能轻松地安装 Skype。然后，你可以将 DSL 的所有优势应用到你的 Skype 应用程序，这样你就可以拥有运行在低端 PC 或自定义便携式 USB 闪盘或 CD 上的通话工具了。

本章描述了如何使用适用于 DSL 的 Skype 软件包通过互联网向他人拨打电话。它还描述了如何扩展对 Skype 的使用以包含免费和廉的服务。尽管本章描述了如何从你可能拥有的任何最新 DSL 版本设置 Skype，但请参阅附 A 获取有关书中包含的 DSL 软件的信息。

> 注意
>
> 虽然本章描述了一些可以使用为 Linux 创建软件提供的免费服务，但它也涉及了一些 Skype 提供的付费服务。本书的作者与 Skype 无关，我们对其产品的报道不代表对 Skype 的认可。如果你对这些服务感兴趣，你应该研究它们对你是否合适。

### Skype 和 VoIP 简介

为了鼓励人们购买其越网协议电话（VoIP）互联网电话产品，Skype Limited (`www.skype.com`) 为注册免费用户账户的人们提供了多种免费的互联网通信服务。通过下载并安装 Skype 软件、设置用户账户并进行一些简单的配置，你可以在几分钟内通过互联网向他人拨打电话。

Skype 将其基于互联网的电话业务描述为去中心化的点对点网络。点对点（P2P）网络应用程序的概念由文件共享应用程序（如 KaZAA (`www.kazaa.com`)）普及，其中客户端可以直接向其他客户端提供和共享文件（包含文档、音乐、视频或其他内容）。在它的 P2P VoIP 服务中，Skype 强调了其实现通信服务的去中心化特征。
