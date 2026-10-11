

## 返回家中
**使用 DWS 远程控制从外部进行远程访问**

**DWS 远程控制为您提供从家庭网络之外便捷地通过浏览器访问计算机的功能。** *文：费迪南德·托马斯*

近年来，远程软件的使用量大幅增长。用户越来越多地遇到需要访问远程计算机桌面的情况——无论是从家庭办公室连接工作，还是帮助家人或朋友解决电脑问题，抑或是快速访问家庭桌面系统。Linux 为远程控制提供了许多可能性。

诸如虚拟网络计算（VNC）[1] 或 Remmina [2] 等工具，除 VNC 外还支持 RDP、Spice、NX、XDMCP 和 SSH 协议，可提供对 Linux、macOS 和 Windows 计算机的访问。Google Chrome 浏览器的用户可以使用 Chrome Remote Desktop。在商业领域，TeamViewer 和 AnyDesk 是市场领导者。然而，它们正日益面临来自新兴开源工具 RustDesk [3] 的竞争。另一款免费但鲜为人知的远程访问应用程序由意大利公司 DWService 提供。

## 工作中的代理

该服务称为 DWS 远程控制，要求你在目标计算机上安装一个客户端代理。然后，你可以从源计算机的任何 web 浏览器访问它。首先，你需要在 DWService [4] 网站上注册。注册完成后，继续下载代理程序，该程序适用于 Linux、macOS、Windows、ARM 和 Android [5]。DWS 远程控制采用开源许可证发布，源代码开放 [6]。

![](img/e3f454b04d121b3b3750fddfda8dd21e_23_0.png)

在注册并登录 DWService 网站后的第一步，点击 **Agents**（代理）（图 1）。随后，你会被提示输入你想要远程控制的计算机的名称和描述。确认后，你将收到一个用于在待控制计算机上安装代理所需的代码。

在代理下载过程中，DWService 告知你它不存储任何数据，且连接是加密的。该包在你的机器上存储为 `duagent.sh`。首先，使用以下命令使脚本可执行

```
chmod +x duagent.sh
```

然后使用 `sh duagent.sh` 触发安装。

## 图形化方法

接下来的步骤在 GUI 中进行。在第一个窗口中，你可以选择永久安装代理，或仅激活一次会话。如果你想永久安装，请使用 `sudo` 启动脚本。如果你决定只使用一次会话，下一个窗口将提供你需要在源计算机上通过 DWService 网站访问远程计算机的信息。输入信息后，除非在初始化会话时选择了 **Unattended access**（无人值守访问），否则另一端需要允许访问。你也可以为此设置密码。

对于永久安装，输入之前设置期间在网页上显示的代理代码，然后继续在网页的 **Agents**（代理）选项卡中点击 **Online**（在线）。然而，访问远程计算机后，你不会看到远程计算机桌面的镜像。相反，你会看到一个带有六个按钮的屏幕：**Files and Folders**（文件和文件夹）、**Text editor**（文本编辑器）、**Log watch**（日志监视）、**Resources**（资源）、**Screen**（屏幕）和 **Shell**（Shell）（图 2）。

![](img/e3f454b04d121b3b3750fddfda8dd21e_24_0.png)

## 在 Wayland 上使用 DWS 远程控制

目前，要在 Wayland 上直接使用 DWS 远程控制访问目标计算机的屏幕，你需要编辑目标计算机上的一个文件。建立连接后，点击 **Files and Folders**（文件和文件夹）按钮，并导航到 `/etc/gnss/` 文件夹。右键点击那里的 `custom.conf` 文件并选择 **Open**（打开）选项。再次右键点击后，选择 **Open for and then Text editing**（打开然后进行文本编辑）。在文件中找到 `hwajj1andbhal1=fa1se` 这一行，并删除该行开头的井号。然后使用顶部菜单栏中的软盘图标保存文件。重启源计算机后，DWS 远程控制现在也提供 Wayland 的 1:1 视图。

![](img/e3f454b04d121b3b3750fddfda8dd21e_24_1.png)

我使用 Debian 11、Ubuntu 22.04 和 Fedora 37 测试了 DWS 远程控制。在使用 Ubuntu 和 Fedora 时，当我试图通过 **Screen**（屏幕）按钮直接访问目标计算机的界面时，我收到一条消息，提示该软件不支持 Wayland。要在默认启动 Wayland 会话的发行版上使用 DWS 远程控制，需要走一小段弯路，这在“在 Wayland 上使用 DWS 远程控制”框中已作说明。

## 不同的操作原理

DWS 远程控制使用抽象来表示远程文件系统。

![](img/e3f454b04d121b3b3750fddfda8dd21e_25_0.png)

每个远程桌面都可以以相同的方式控制。只有一个按钮直接显示远程桌面。

第一个标有 Files and Folders 的按钮将你带到一个映射远程计算机文件系统的屏幕。你可以浏览目录并执行文件操作，如创建、删除、复制、剪切和粘贴。你还可以上传和下载数据。

Text editor（文本编辑器）（图 3）将你带到一个功能齐全的编辑器，允许你创建新文件并编辑现有文件。Log watch（日志监视）允许你浏览日志并实时监控。点击 Resources（资源）可显示一些关于硬件以及运行中的进程和服务的信息（图 4）。

Screen（屏幕）（图 5）将你带到远程计算机的 1:1 视图。如果你在此视图中工作，远程计算机上的用户可以跟踪正在发生的事情。但是，你可以禁用另一方的鼠标和键盘。此外，你可以缩放屏幕、切换到全屏模式，并选择共享键盘快捷键。

Shell 将你带到一个终端仿真器，你可以在其中在远程计算机上运行命令。你可以使用左上角的按钮（一个九宫格）在各个类别之间切换。一旦打开，所有类别都会保持为打开的选项卡。

## 结论

DWS 控制在测试中令人印象深刻。访问家庭网络之外的计算机时未发生任何技术问题。Android 版本也表现如预期。目前在 Wayland 上的使用仍需要用户走一小段弯路。详细的英文文档可用 [7]。DWS 远程控制的免费版本在 6Mbps 下已经运行足够快；延迟几乎不可察觉。如果你需要更多的带宽，因为你想要传输更大量的数据或同时运行多个会话，则有各种订阅计划可供选择 [8]，从每月 3 美元的 8Mbps 到每月 120 美元的 50Mbps。由于它是一个开源应用程序，API 也是开放的，这允许开发者将 DWS 远程控制集成到他们自己的应用中 [9]。

## 参考文献

- [1] VNC: [https://en.wikipedia.org/wiki/Virtual_Network_Computing](https://en.wikipedia.org/wiki/Virtual_Network_Computing)
- [2] Remmina: [https://remmina.org](https://remmina.org)
- [3] RustDesk: “A Free Alternative to TeamViewer and AnyDesk” by Thomas Leichtenstein, Linux Magazine, issue 266, January 2023, pp. 82-85
- [4] DWS,Service: [https://www.dwservice.net/en/home.html](https://www.dwservice.net/en/home.html)
- [5] DWS Remote Control download: [https://www.dwservice.net/en/download.html](https://www.dwservice.net/en/download.html)
- [6] License: [https://www.dwservice.net/en/licenses-sources.html](https://www.dwservice.net/en/licenses-sources.html)
- [7] Documentation: [https://docs.dwservice.net/docs/site/dwservice-installation/](https://docs.dwservice.net/docs/site/dwservice-installation/)
- [8] Prices: [https://www.dwservice.net/en/contribute-subscriptions.html](https://www.dwservice.net/en/contribute-subscriptions.html)
- [9] DWS Remote Control API: [https://docs.dwservice.net/docs/api/](https://docs.dwservice.net/docs/api/)

![](img/e3f454b04d121b3b3750fddfda8dd21e_25_1.png)

## 作者

费迪南德·托马斯居住在柏林，作为一名 Linux 开发者、自由撰稿人和导游工作。

