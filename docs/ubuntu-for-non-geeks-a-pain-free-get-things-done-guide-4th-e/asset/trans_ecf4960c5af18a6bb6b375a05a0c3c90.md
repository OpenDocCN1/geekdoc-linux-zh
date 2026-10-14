

另一种方法是安装一些额外软件来为 Windows 添加对 Linux 分区的支持。不幸的是，这类软件的状态相当糟糕：对老式的 ext2 格式的支持还算不错，但 Ubuntu 现在使用的是 ext4，这完全是另一回事。据我所知，人们所能做到的最好结果就是以只读模式在 Windows 中挂载 ext4 分区。虽然你无法向分区中添加新文件，但至少你可以查看其中的内容并将其复制到 Windows 中。参见 http://www.soluvas.com/read-browse-explore-open-ext2-ext3-ext4-partition-filesystem-from-windows-7/ 以了解如何操作的示例。

## 项目 18B：安装 Microsoft Windows 核心字体

喜欢与否，计算世界仍然基本上是微软的世界，这意味着绝大多数用户，甚至是 Mac 用户，都在使用微软字体。既然如此，处理使用 Georgia、Verdana、Times New Roman 和 Courier 等字体的文档在所难免，当然，你的系统可以为文档中使用的字体代换它所拥有的字体。但为了让你能够精确地看到事物本来的样子，并让他人以你所期望的方式查看你的文档，你最好在自己的系统上安装这些微软核心字体。

幸运的是，你有两种方法可以获得这些字体。一种是通过 Ubuntu 软件中心下载并安装它们，而另一种，对于那些采用双系统启动的用户，则是直接从 Windows 分区复制它们。在前一种情况下，你只需使用 Ubuntu 软件中心安装 Microsoft Core Fonts 软件包即可。这是来自 Windows XP 的旧版字体集，因此安装此软件包不会获得随后期 Windows 版本捆绑的那些花哨的新字体。安装过程完成后，你的新微软字体将被成功安装，并可供机器上的每个用户账户立即使用。

如果你是双系统启动用户，可以直接从 Windows 安装中复制字体。这样做的好处是能将所有 Windows 字体，包括较新的字体（如果你安装了 Vista 或 Windows 7），都带入 Ubuntu。以下是你需要做的操作：

- 1. 挂载你的 Windows 分区，如“项目 18A：访问你的 Windows 分区上的文件（面向双系统启动用户）”第 324 页所述。
- 2. 在 Nautilus 中打开 Windows 分区，并浏览到 Windows/Fonts 文件夹。
- 3. 现在来个小技巧：选择 Edit ▸ Select Items Matching，在出现的框中输入 *.ttf，然后单击 OK（图 18-3）。这将选择文件夹中所有文件名以 .ttf 结尾的文件，这些都是 TrueType 字体文件。
- 4. 将文件复制到一个方便的位置（放在你的主文件夹中即可）。

![](img/f7cef0df22f9dba5a41777808c98eece_364_0.png)

图 18-3：在 Windows/Fonts 文件夹中选择所有 TrueType 字体

- 5. 现在，返回 Windows/Fonts 文件夹，并再次选择 Edit ▸ Select Items Matching。这次，在框中输入 *.TTF。这将选择剩余的字体文件——项目选择功能区分大小写，而出于某种原因，文件名使用了不同的大小写。像之前一样复制所选文件。
- 6. 将所有字体文件复制到 Ubuntu 后，你现在可以像安装任何其他字体一样安装它们。最简单的方法是将文件复制到主文件夹中的隐藏 .fonts 文件夹，但你应参阅第 143 页的“项目 8C：安装 TrueType 字体”以获取完整细节。

## 双系统启动：更改启动顺序和超时

如果你选择在“双系统启动”设置中与 Windows 并排安装 Ubuntu，那么到现在你应该已经习惯看到 GRUB 启动菜单屏幕了（图 18-4）。这是每次启动计算机时出现的屏幕，可让你选择运行 Windows 或 Ubuntu。

如果在几秒钟内不选择其他选项，Ubuntu 将自动启动。这对于主要使用 Ubuntu 但偶尔需要进入 Windows 的人来说是合适的。然而，如果你花更多时间在 Windows 上，你可能更喜欢将其设为默认操作系统。要进行更改，首先使用 Ubuntu 软件中心安装 StartUp-Manager，然后通过选择 System ▸ Administration ▸ StartUp-Manager 打开它。你可能会被要求输入密码，输入后等待片刻让其加载。单击 StartUp-Manager 窗口中的 Boot options 选项卡（图 18-5），并从 Default operating system 下拉列表中选择 Windows。Windows 选项的实际名称将

