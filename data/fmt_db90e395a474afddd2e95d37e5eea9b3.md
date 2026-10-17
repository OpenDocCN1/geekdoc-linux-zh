
你可以通过在 Ubuntu 软件中心搜索`firestarter`并安装它来获取 Firestarter。安装完成后，通过选择 **系统 ▸ 管理 ▸ Firestarter** 运行它（你可能会被要求输入密码）。Firestarter 第一次打开时会弹出一个不言自明的设置向导。只需仔细阅读每个屏幕；如果有建议的选择，就按建议选择；然后在每个向导屏幕中点击 **下一步** 按钮，直到到达最后一个屏幕（如图 19-2 所示）。在该屏幕上，确保 *立即启动防火墙* 旁边的框已勾选，然后点击 **保存** 按钮。向导窗口随后会关闭，Firestarter 主窗口将会出现。假设检测并选择了正确的网络设备并且向导选择正确，防火墙就会启动并运行。

![](img/f7cef0df22f9dba5a41777808c98eece_379_0.png)

*图 19-2：Firestarter 设置向导的最后一个屏幕*

如果选择了错误的网络设备，将会出现一个警告窗口告知你。在这种情况下，你可以通过在 Firestarter 主窗口中选择 **编辑 ▸ 首选项**，然后在出现的首选项窗口中点击 **网络设置** 来进行一些试错操作（图 19-3）。在该窗口中，从“已检测到的设备”下拉菜单中选择其他列出的设备之一，然后点击 **接受** 按钮。回到 Firestarter 主窗口后，点击 **启动防火墙** 按钮（看起来像播放按钮），看看会发生什么。如果仍然无法启动防火墙，请重复我刚才描述的过程，这次选择不同的网络设备。

![](img/f7cef0df22f9dba5a41777808c98eece_380_0.png)

图 19-3：在 Firestarter 中选择网络设备

一旦你的防火墙启动并运行，实际上你不需要再做任何事情。你只需查看 Firestarter 窗口（图 19-4）即可了解计算机网络方面的情况——你有哪些活动连接、进出的数据量有多少，以及是否发生了例如防火墙阻止入侵者的事件。如果你点击事件标签页，你就可以看到这些事件的详细信息，例如哪些连接尝试被阻止、它们来自哪里以及何时发生。

![](img/f7cef0df22f9dba5a41777808c98eece_380_1.png)

图 19-4：Firestarter 运行中

## 控制 Firestarter

你可以通过创建自己的策略来控制 Firestarter 如何处理各种网络事件。Firestarter 中默认的策略集允许你通过互联网做任何你通常会做的事情，同时它会阻止来自互联网或网络上任何其他计算机对你的计算机的新连接。

要让设置更严格一些，你可以点击 Policy 选项卡，在 Editing 下拉菜单中选择 Outbound traffic policy，然后选择 Restrictive by default, whitelist traffic。如果你只是想禁止在你的计算机上工作的人访问某个特定网站，例如，只需选择 Permissive by default, blacklist traffic，右键单击 Deny connections to host 字段，并在弹出菜单中选择 Add Rule。在 Add new outbound rule 窗口中，输入目标站点的域名（如 example.com），点击 Add，然后点击主 Firestarter 窗口中的 Apply Policy 按钮（它看起来像一个绿色复选标记）。

## 确认 Firestarter 自动运行

第一次运行 Firestarter 后，它将设置自己在每次启动系统时自动启动。不要担心你看不到第一次启动时看到的图形界面；Firestarter 将在后台运行，静默地保护你的计算机。

如果你是那种怀疑的人，你可以通过打开一个 Terminal 窗口，输入 `sudo /etc/init.d/firestarter status`，然后按 ENTER 来检查 Firestarter 是否确实在后台运行。如果 Firestarter 正在运行，你将在 Terminal 窗口中看到消息 * Firestarter is running... 担忧结束。如果 Firestarter 未运行，响应将显示为 * Firestarter is stopped。

## 了解更多信息

如果你对防火墙的世界还不熟悉，你可以查看 Firestarter 主页以了解更多信息。要查看在线手册，只需转到 Firestarter Help 菜单，并选择 Online Users’ Manual，它将在你的网页浏览器中打开该页面。如果你更喜欢在安装 Firestarter 之前查看手册，请将浏览器指向 http://www.fs-security.com/docs/。你还会在那里找到一个相当不错的快速教程。

## ClamAV：Linux 风格的防病毒软件

尽管缺乏能够对你的 Linux 系统造成破坏的病毒，你的计算机仍可能成为传播 Windows 病毒的媒介。因此，有许多免费的防病毒扫描程序可供有兴趣帮助保护 Windows 用户免受病毒侵害的 Linux 用户使用。其中包括 Panda Desktop Secure (http://www.pandasecurity.com/usa/homeusers/downloads/desktopsecure/)、f-Prot (http://www.f-prot.com/) 以及许多其他软件。然而，对于大多数 Linux 用户来说，首选的病毒扫描程序是开源竞争者：ClamAV。

尽管 ClamAV 可用于多种操作系统，但它被认为是最适合 Linux 的防病毒软件包。它是开源的并且完全免费，你不必担心许可证或续期的麻烦。不幸的是，ClamAV 本身是一个命令行驱动的应用程序，这使得它有点不太友好。幸运的是，所有相关人员都有一个图形界面，尽管很简单；它被称为 ClamTk。ClamAV 和 ClamTk 都可以通过 Ubuntu 软件中心获得——只需搜索`clamtk`，然后安装 Virus Scanner。Ubuntu 软件中心随后将自动安装 ClamAV 以及运行所需的所有其他软件包。

一旦安装了 ClamAV，你可以通过选择 Applications ▸ Accessories ▸ Virus Scanner 来执行病毒扫描。这将打开 ClamTk Virus Scanner 窗口（图 19-5）。

运行后，你可以从 Scan 菜单按需扫描系统。要扫描单个文件夹，请选择 A Directory。要扫描一个目录及其内部的所有内容，请选择 Recursive Scan。在任何一种情况下，都会出现 Select a Directory 窗口。选择你想要扫描的文件夹或磁盘，然后点击 OK。ClamAV 然后将开始扫描你的系统。ClamTk 将在按钮栏正下方的空白处随时告知它正在扫描的内容。如果它发现任何可疑项目，它将在窗口的主窗格中列出该项目。

![](img/f7cef0df22f9dba5a41777808c98eece_382_0.png)

图 19-5：ClamTk——ClamAV 的图形界面

ClamAV 默认设置在启动时检查签名更新。这些签名更新告诉 ClamAV 要注意哪些新病毒。如果你让机器连续开机几天，设置 ClamAV 每天自动检查签名更新而不是仅在启动时检查也是一个好主意。为此，请转到 Advanced 菜单，并选择 Scheduler。在 Schedule 窗口中，在窗口下半部分选择 ClamAV 执行更新检查的时间。完成后点击 Add 按钮。你还可以使用此窗口设置定期扫描系统的时间——只需选择你希望扫描发生的时间，然后点击 Add。完成后，点击 Close。

正如我提到的，在病毒扫描期间你可能遇到的唯一病毒是为 Windows 系统设计的病毒，这些病毒无法影响你的 Linux 系统。虽然扫描整个系统寻找病毒不会有什么坏处，最好将你的病毒扫描活动集中在你的 Windows 分区上（如果你有的话），以及你将作为电子邮件附件发送的任何文件，特别是发送给 Windows 用户的文件。

## Project 19A: 使用 avast! 进行病毒扫描

虽然 ClamAV 可能是 Linux 世界中首选的病毒扫描程序，但我个人最喜欢的仍然是 avast!，它在我的 Windows 年代保护了我。我认为它更容易使用，而且就其价值而言，看起来更漂亮。缺点是它要求你每年注册一次以获取许可证密钥，但这 hardly 是一项艰巨的任务，而且仍然是免费的。

### 19A-1: 下载 avast! DEB 包和许可证密钥

首先你必须获取 avast! 文件和许可证密钥。你可以通过打开网络浏览器并访问 http://www.avast.com/linux-home-edition/ 来完成此操作。到达那里后，点击 Download 选项卡，然后下载 avast! Linux Edition 的 DEB 包。
