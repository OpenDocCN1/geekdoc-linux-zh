
你可以在 PDA 上使用 Evolution 日历、待办事项管理器和联系人管理器。在本节中，我们将重点介绍如何使用 Evolution 备份你的 PDA，因为这是你可以做出的有趣且有的事情之一。你可以通过阅读在线的 Evolution 文档（选择“帮助”或访问 `www.gnome.org/gnome-office/evolution.shtml`）或通过简单的尝试来了解更多关于使用日历的知识。

你可以使用 `Evolution pilot-link` 工具将 PDA 数据库备份到电脑中。请按照以下步骤操作：

- 1. 根据 PDA 的类型，将基底座插入电脑的串口或 USB 端口。
连接在基底座上的电缆有一个 9 针母头（DB9）。大多数（如果不是全部的话）现代电脑都带有一个 9 针公头，可以连接到由 `/dev/ttyS0` Linux 设备控制的串口插座。（在 Windows 世界中，`/dev/ttyS0` 等于 COM1，`/dev/ttyS1` 等于 COM2，以此此类推。）
如果你使用的是基于 USB 的基底座，端口为 `/dev/ttyUSB0` 或 `/dev/ttyUSB1`。
- 2. 点击 GNOME 面板上的 Evolution 图标。
Evolution 应用程序打开。
- 3. 点击“联系人”按钮，并从“工具”菜单中选择“Pilot 设置”。
“欢迎使用 GNOME Pilot 向导”窗口打开。
- 4. 点击“向前”按钮，打开“Gnome Pilot 设置”窗口，如图 10-5 所示。
![](img/85ec3de0d5219d6ca14d5778e16a3338_158_0.png)
你需要告诉 Evolution 在哪里寻找你的 PDA。打开“端口”菜单并选择串口设备。
设备可能是 `/dev/ttyS0` 或 `/dev/ttyS1`。尝试并不并耻，请顺序选择每个端口，直到找到正确的那个。
不要担心选择速度。除非你有一台非常老的电脑，否则默认值就足够。
- 5. 点击“向前”按钮。
“Pilot 识别”窗口打开。
- 6. 点击“否，我以前从未与此 Pilot 使用过同步软件”按钮。
你的用户名被插入到“用户名”文本框中。（例如，如果你以 paul 的身份登录，那么 paul 就是你的默认 Pilot ID。）
- 7. 点击“向前”按钮接受该用户名；否则，输入你想要作为 Pilot ID 的名称。
- 8. 按下 PDA 基底座上的同步按钮（例如 Palm Pilot 的 HotSync）。
日历数据库被复制到你的 Fedora Core 电脑上。
Evolution 还可以同步你的联系人列表和地址录。很酷，对吧？
![](img/85ec3de0d5219d6ca14d5778e16a3338_159_0.png)
![](img/85ec3de0d5219d6ca14d5778e16a3338_159_1.png)

# 第 11 章：上网与享受音乐

## 本章内容

- Web 的简短历史
- 使用 Mozilla 浏览网页
- 通过插件获取额外帮助
- 保护你的密码安全
- 播放你的 CD
- 构建你的音响系统
- 刻录 CD

在本章中，我们介绍了开源的 Mozilla 浏览器。Mozilla 提供了其他流行浏览器的所有功能。我们将展示如何为你的 Fedora Core 电脑设置 Mozilla，以便你可以上网。你可以将电脑作为多媒体设备。在开始使用 Mozilla 之后，我们将描述如何配置你的 Linux 设备来听音乐和制作 CD。
我们在本章的目标是描述如何使用 Mozilla 的基本功能。然而，我们希望你知道，Mozilla 的功能远比我们在本章中描述的要。关于 Mozilla 的更多信息，请查看“帮助”菜单中的可用功能，例如“参考库”或“帮助内容”。

## 让万维网成为可能

从前，一家名为 Netscape 的公司创建了一个用于浏览的浏览器。该浏览器最初名为 Navigator，后来改为 Communicator。数百万人从网上免费下载了它。Netscape 让数百万人（包括我们，这些作者）拥有了访问爆炸式增长的 Web 服务器的力量。Netscape 创造了历史并改变了世界，因为它将互联网从一个为科学家提供服务的媒介变成了任何人都可以使用的工具。
尽管 Netscape Communicator 免费分发给任何想要它的人，但它并不是像 Linux 那样的开源软件。简单来说，Netscape Communicator 是一项商业性活动，Netscape 认为该软件的工作方式是专有的。
另一方面，Netscape 认识到开源动态的重要性，这就是为什么它发布了 Netscape 的开源版本，命名为 Mozilla。现在，无数的人正在开发和增强 Mozilla，它是 Fedora Core 电脑的默认浏览器。
随书附带的 DVD 包含了 Mozilla，它是 Netscape Communicator 的开源兄弟版本。Netscape 和 Mozilla 非常相似，尽管它们有一些不同的功能。

## 上网

如果你浏览过互联网，你想要做的第一件事就是自定义你的主页。当你启动 Mozilla 时，会出现哪个页面？你也可以设置你想要的页面作为主页。要实现这一点，请遵循以下步骤：
- 1. 点击地球图标启动 Mozilla。
- 2. 从“偏好设置”窗口选择“编辑：偏好设置”。
- 3. 点击“类别”旁边的加号展开。
- 4. 在“偏好设置”窗口的“主页”区域，填写你想要作为主页的 URL。
- 5. 如果你想使用当前页面，点击“使用当前页面”按钮。
![](img/85ec3de0d5219d6ca14d5778e16a3338_161_0.png)
Mozilla 会记住你去过哪里并让你选择之前的页面。Mozilla 记住多长时间取决于你选择的天数。“历史”选项决定了保存位置的天数。如果你磁盘空间有限，选择较小的历史数字。否则，保持默认设置。
如果你的 Linux 连接到带有代理的网络，你需要配置 Mozilla 与其工作。要这样做，从“偏好设置”窗口选择“高级”选项。点击“手动代理配置”按钮并输入你的防火墙名称。例如，在“HTTP 代理”文本框中输入 `proxy.mynetwork.com`（如果你的防火墙名称），并在“端口”文本框中输入 80。如果你使用的是 Fedora 默认防火墙或我们在书中描述的数据包防火墙，则不需要执行此配置过程。

## 安装插件

安装插件的过程非常简单
- 1. 获取插件并放入 Mozilla 插件目录。
- 2. 可选配置 Mozilla 偏好设置以使用该插件。

## 142 第三部分：Linux，哈？它有什么用？无事无所不能！

你可以通过搜索 Mozilla 插件链接来查找、下载并安装几个流行的插件。以下步骤展示了如何安装流行的 Macromedia Shockwave 插件；有了 Shockwave 插件，Mozilla 就可以显示动画和其他酷炫的内容：
+ 1. 启动 Mozilla 和你的互联网连接（如有必要），然后从“帮助”（Help）菜单中选择“关于插件”（About Plug-ins）来检查 Mozilla 已经拥有哪些插件。
Mozilla 显示只安装了默认插件 `libplugin.so`。你需要下载并安装一些实用的插件。
+ 2. 点击“已安装插件”页面顶部的 `plugindoc.mozdev.org` 链接。你会看到 Mozilla 插件页面，它显示了在哪里可以找到最流行和实用的插件。
+ 3. 点击 Linux (x86) 链接。
Macromedia 下载页面打开。
+ 4. 点击 Macromedia Flash Player 链接。
+ 5. 点击 Macromedia Flash Player 6 for x86 Linux 链接。
+ 6. 点击离你最近的镜像站点（例如，美国西部）。
下载 `flash-player-6.0.81.i386.rpm` 的对话框打开。
+ 7. 点击 OK 按钮。
打开第二个窗口，标记为“输入要保存的文件名”。默认情况下，Mozilla 将文件保存到你当前所在的目录——如果你在登录后没有更改目录，那么这应该是你的主目录。
+ 8. 点击“保存”（Save）按钮，软件将保存到你的电脑。
下载管理器（Download Manager）窗口显示下载进度。
+ 9. 要安装 Flash 插件，从 GNOME 菜单中选择“系统工具：终端”（System Tools: Terminal）打开一个 GNOME 终端窗口。
+ 10. 输入以下命令成为 root（超级用户）：
```
su
```
+ 11. 在提示时输入 root 密码。
+ 12. 输入此命令安装 Flash Media 软件：
`rpm -ivh all_flash_plugin*`
Macromedia Flash 6 Plugin—最终用户许可协议（End User License）对话框打开。

# 第 11 章：冲浪网络与享受音乐

+ 13. 在 20 秒限制内点击“接受”（Accept）按钮。
