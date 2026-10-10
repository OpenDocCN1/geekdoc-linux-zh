
3. 在图 9.8 所示的 COAS 名称打印机对话框中为远程打印机指定一个名称。给远程打印机起一个既能表明它是远程的、又能标识其实际物理位置的名字是非常好的主意。特别是当所谓的“远程”打印机实际上位于本地，但通过网络连接时，这一点尤为重要。

![](img/df365d352a104b50fea29e59a052de4d_261_0.png)

4. 告知 spooler 控制此打印机的远程主机是哪个，以及远程主机如何称呼此打印机。（参见图 9.9。）

![](img/df365d352a104b50fea29e59a052de4d_261_1.png)

5. 从出现的确认屏幕保存、丢弃或取消此打印机条目。

## 通过网络打印第一页

我们现在准备通过网络打印第一页了。根据你使用的网络协议类型以及网络的连接方式，你可以使用多种方法来实现这一点。

如果你正试图通过局域网使用 Samba 进行打印，可以使用以下命令测试 Samba 挂载的配置：

```
# testprns remoteIp
```

这里你需要将 `remoteIp` 替换为 `/etc/printcap` 文件中远程打印机的实际名称。

你应该执行其他几个 Samba 测试，这些测试在第 16 章关于 Samba 的部分中有详细讨论。不过，如果前面的测试成功，那么你的远程打印机很可能也能正常工作。

要在连接到 Samba 的打印机上打印，请输入以下命令：

```
# smbclient //servername/printernane
```

系统会提示你在 *servername* 上输入密码，在某些情况下必须使用大写字母。完成此操作后，你就可以开始使用通过网络可用的打印机了。

如果我们试图通过 TCP/IP 网络进行打印，输入以下命令应在远程打印机上产生一些打印输出：

```
# lpr -P RemotePrinterName /etc/profile
```

这将在远程打印机 *RemotePrinterName* 上打印文件 *etc/profile*（一个始终存在的文件）。

## 格式化打印

如果你只是随便打印一些无用内容（junk printing），那么我们目前所做的一切都足够了，但我猜通过限制我们进行的无用打印，我们可以为保护森林节省几棵树。

无用打印的替代方案是格式化打印（也称为非无用打印）。当我们拥有长长的打印输出，且需要页码（玩过“357 捡拾”游戏吗？）或页眉和页脚时，格式化打印很有用。另一个希望为打印输出的每一页添加信息的场景是，我们希望每页都打印“仅供传阅”或“机密”通知。

如果你使用的是文字处理软件，这通常非常容易实现。然而，你通常不会用文字处理软件打印财务记录或客户名单。

解决这些问题的一个非常有效的方案是 `pr` 命令。它存在于许多版本的 UNIX 中，并提供了大量选项来满足你的各种需求。

例如，以下命令：

```
# pr -h "Public Information" -o 20 < pr --help | lpr
```

将给你一个格式美观的页面，顶部包含“Public Information”（以及时间和日期），内容为 `pr` 命令的帮助列表。

这里需要稍作解释。首先执行的命令部分是 `pr --help`，它生成 `pr` 命令的帮助列表。这段文本通过管道传输到行首的 `pr -h "Public Information" -o 20` 命令中的 `pr` 命令。不仅它会生成带有包含“Public Information”以及其他标准页眉信息的格式化输出，还会给你一个 20 个空格宽度的左边距（也许是为了留作注释）。然后，这个 `pr` 命令的输出通过管道传输到 `lpr` spooler。

![](img/df365d352a104b50fea29e59a052de4d_262_0.png)

如果你觉得这更像是一场打字测试而非护林行为，那你可能是对的。但是，如果你只是在 pr 和 -h 之间加上 +356，该命令将变为：

`pr +356 -h "Public Information" -o 20 < longprintout.txt | lpr`

这个命令真正能保护森林，因为你将从 `longprintout.txt` 的第 356 页开始打印。当然，这一页会有正确的页眉和页码。

另一个对格式化文本（并保护森林）非常有用的命令是 `groff`。该命令实际上是整个 `groff` 文档格式化系统的前端，具有广泛的功能，特别是当你想为特定设备格式化文档时。

Caldera 提供的 `groff` 版本支持以下目标设备：

- PostScript 打印机
- TeX dvi 设备
- 多个 X11 查看器（在 75 和 100 dpi 下）
- 打字机类设备
- 使用 ISO Latin-1 字符集的打字机类设备
- PCL5 兼容打印机

另一个格式化命令是 `troff`。当你需要包含小数点尺寸和数学表达式等格式化（如物理或数学论文中可能出现的情况），`troff` 是最有用的。

## 使用其他应用程序配置打印机

Caldera OpenLinux 附带了 WordPerfect 8 for Linux，这将在第 25 章与其他文字处理软件包一起介绍。为了将打印机设置为与 WordPerfect 配合工作，请选中角落的 K-Gear 图标，突出显示应用程序，然后单击 WordPerfect。

在 WordPerfect 标志窗口中，选择 Program（程序）然后选择 Printer Control（打印机控制）。

在图 9.10 所示的 Printer Control（打印机控制）对话框中，你可以管理 WordPerfect 的打印机。

![](img/df365d352a104b50fea29e59a052de4d_264_0.png)

在此对话框中，你可以选择任何 WordPerfect 打印作业的目的地，并锁定该打印机，以便其他应用程序不会干扰 WordPerfect 的打印机设置。

此外，你可以查看当前的 WordPerfect 打印队列，并可选择取消打印作业、将其移动到另一台打印机、重新排序打印作业、停止打印作业或保留打印作业。

你还可以通过单击打印作业，然后单击 Status（状态）按钮来检查打印作业的状态。

Caldera OpenLinux 还附带了 Star Office 5.0。该应用程序的打印机设置通过图 9.11 所示的对话框进行处理。

![](img/df365d352a104b50fea29e59a052de4d_264_1.png)

该应用程序的默认设置对于大多数打印机开箱即用即可正常工作。你可以看到，有许多选项可以提高 Star Office 的性能。希望使用 Caldera OpenLinux 下 Star Office 传真功能的人需要探索这些选项。

首先，如果你突出显示打印机并单击打印机安装对话框上的 Connect（连接）按钮，将在你的监视器上显示图 9.12 所示的 Connect（连接）对话框。

# 图 9.12
Star Office 打印机连接对话框。

![](img/df365d352a104b50fea29e59a052de4d_265_0.png)

此对话框允许你修改或移除打印机队列，并配置 Star Office 的传真输出。

如果你选择 Configure fax（配置传真），将进入一个输入框，允许你选择打印到文件或管道，并输入 Star Office 使用的特定传真命令。Star Office 文档将提供有关传真打印选项具体信息的更多细节。

## 有用的增强打印功能程序（及获取途径）

最有用的打印工具之一使你能够在一页纸上打印文档的多页内容（再次保护森林）。这个工具是 mpag，可以从以下地址获取：

http://www.userfriendly.net/linux/RPM/turbolinux/1.2/RPMS/mpage-2.4-1.i386.html

请注意，归档文件使用 _z 后缀表示 _Z；换句话说，该文件是使用 compress 而非 gzip 进行压缩的。这个命令不仅显著加快了打印速度，还能保护森林。

另一个有用的程序是 nenscript，它可以格式化 ASCII 文件，将其转换为 PostScript，然后允许你选择许多选项，如横向或纵向打印、单列或双列、是否带页眉等。可以在以下地址找到 nenscript：

http://www.im.lcs.mit.edu/magnus/nenscript/

## 大师们的一些秘诀（初级部）

当其他方法都失败时，有时查看 Grant Taylor 的 Linux Printing HOWTO 主页很有用，可以在以下地址找到：

http://www.picante.com/~gtaylor/pht/

如果你试图从 Linux 打印到 Windows 95 网络上的打印机，另一个非常值得访问的网站是：

http://home1.pacific.net.sg/~harish/linuxprint.html

最后一个针对大师们（初级部）的网站，它包含了你通常可能想要的所有软件包（包括打印软件包）：

http://www.shopternet.net/publiclibrary/RPM/Groups.html

该网站按功能对所有软件包进行了分类。

