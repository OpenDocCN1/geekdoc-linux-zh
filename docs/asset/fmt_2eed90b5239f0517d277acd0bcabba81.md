
`$ su`

Password: password

# `lynx -source http://go-gnome.com/ | sh`

```
```

`Lynx`是一款基于文本的 Web 浏览器。`-source`选项指示`lynx`将 Web 页面的源代码输出到标准输出并退出。`go-gnome.com`上的页面实际上是一个 shell 脚本。因此，它会通过`sh`（bash shell 解释器）来运行。该 shell 脚本将引导你完成剩余的安装过程。

> **提示**
>
> Helix GNOME 也适用于 Solaris，但过程略有不同（尽管几乎同样简单）。从下载页面选择 Solaris，然后按照说明操作。
>
> 另请注意，在撰写本文时，Caldera OpenLinux 上默认的 Helix GNOME 安装存在一些问题。在 OpenLinux 上安装 Helix GNOME 的说明可在 OpenLinux 支持站点 `support.calderasystems.com` 上找到。搜索 “GNOME Helix”。

你将会被问到的第一个问题是从哪里下载 GNOME。除非你恰好靠近加利福尼亚州帕洛阿尔托或马萨诸塞州剑桥的主要镜像之一，否则请选择 Helix Code, Inc. Ubiquitous (Akamaized) 链接。有关 Akamai 的更多信息，请参阅下面的侧边栏“如何无处不在：Akamai”。

## 如何无处不在：Akamai

你会希望看到“Ubiquitous (Akamaized)”这个短语越来越多地出现在镜像列表中。`Akamai`（`www.akamai.com`）是一家实际上按需提供镜像服务的公司，但其功能远不止于此。当你连接到 Akamai 服务器时，网络会将你与能够以最快速度提供所需数据的服务器匹配起来。这意味着该服务器离你最近且负载最小。如果有太多人想要同一份信息，Akamai 会在网络中最需要的地方自动生成新的镜像。所有这一切都以透明的方式完成。

我多年来一直从互联网下载软件。我花了很多个夜晚寻找一个不过载的所需信息镜像（在弗吉尼亚州，有时从德国下载比从马萨诸塞州更快）。我还没有遇到过 Akamai 系统过载的情况。你可以更快地获取数据，麻烦更少，对网络的负担也更小。作为一名用户，我强烈建议在可用时使用这项服务，除非你恰好非常靠近主镜像。

选择镜像后，将下载主图形安装程序。该文件大约 2MB，因此除非你的网络连接速度很快，否则可能需要一些时间。一个小条形图会显示已下载的数量。下载完成后，图 4.1 中显示的图形安装程序将自动启动。

**图 4.1**
Helix GNOME 图形安装程序非常易于使用。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_91_0.png)

接下来，系统会要求你选择从哪里获取 Helix GNOME 的其余部分。通常你会选择 Helix Code 镜像站点，这将从众多 Helix Code 镜像之一进行下载。不过，如果你是从 Helix Code CD 安装，则可以选择本地介质。最后，如果你将软件包放在本地网络的某个位置，则可以选择其他网络站点。

由于 Helix Code 安装程序可以使用 HTTP，如果你的网络需要代理，则可能需要在下一页配置代理。

然后选择一个镜像。这些是通用的 GNOME 镜像，这就是为什么这些镜像比你选择安装程序镜像时要多得多。再次寻找离你较近的城市。如果没有，请选择 Helix Code Inc. Ubiquitous (Akamai-ized)。你应该优先选择 HTTP 代理而不是 FTP 代理，因为 HTTP 通常更容易让站点实现负载均衡。显然，你不应该选择任何测试镜像（这些镜像标记为“请勿使用！”）。

最后，开始选择软件包，如图 4.2 所示。如果这是你第一次安装 GNOME，即使你打算接受默认设置，也至少应该看看有哪些可用选项。这将让你很好地了解 GNOME 附带的内容。如果你有大量磁盘空间（和快速的网络连接），可以选择“安装全部”，这很好，因为你不用担心遗漏任何东西。

当你单击“下一步”时，Helix GNOME 将开始安装。你可以通过条形图查看进度，但你可能只想让它自己运行。在安装完成之前不需要再进行任何交互。然后它会询问你是否要使用 `gdm` 登录管理器；如果你主要使用 GNOME，你可能会选择使用它。最后，它将重新启动 X（确保你已经退出所有其他 X 应用程序！），然后你就可以开始使用 GNOME 了。

**图 4.2**
这里有很多软件包，但即使只是快速浏览一下，也能让你对可用的内容有一个很好的了解。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_92_0.png)

## 选择 GNOME

许多发行版允许你在安装时选择使用 KDE、GNOME 或其他桌面环境。不过，安装后切换桌面通常相当简单。唯一复杂的部分是如何确定你的特定发行版启动桌面的方式。

### 使用显示管理器

如果你使用的是 `gdm`（GNOME 显示管理器）或 `kdm`（KDE 显示管理器），你可以在登录时通过会话（Session）或会话类型（Session type）菜单选择桌面。

一旦你选择过一次桌面，显示管理器会在你再次登录时记住该选择。只需将该设置保留为默认值即可。

### 使用 switchdesk

Red Hat 包含一个名为 `switchdesk` 的实用工具，它允许你在 GNOME、KDE 和 `twm`（一个简单的窗口管理器）之间轻松切换。在命令行中输入以下命令：

```bash
$ switchdesk-gnome
```

然后选择你想使用的桌面（这里以 GNOME 为例），并按下 OK。

“Change Only Applies to Current Display（仅更改当前显示）”选项允许你为不同的显示设置不同的桌面。通常，更改显示意味着你从不同的机器登录。例如，你可以使用 NCD X 终端（一种显示 X 的机器，但它本身不进行任何计算，也没有操作系统）。如果你的 X 终端位于慢速网络链路上，你可能会更愿意使用像 `twm` 这样的轻量级桌面，而不是 GNOME。

> **提示**
>
> `switchdesk-kde` 是另一个实用工具，你可以用它来代替 `switchdesk-gnome`。这两个工具的区别在于用于显示对话框的工具包不同。任一工具都可以用来选择任一桌面。

### 手动选择 GNOME

如果你想手动选择 GNOME，可以直接修改配置文件。如果你有非常自定义的启动序列，这会很有用。

要在 Red Hat 及类似发行版中为所有用户修改默认桌面，只需编辑 `/etc/sysconfig/desktop`，并输入 GNOME 作为一行内容。这将自动为所有尚未选择自己桌面的用户设置桌面。

如果你想在 Red Hat 中为单个用户设置默认桌面，请编辑 `${HOME}/.Xclients`，使其内容为 `exec gnome-session`。

在 Debian 中，至少在 Woody 的当前状态下，没有自动为所有用户选择 GNOME 的方法。对于单个用户，你可以将以下内容添加到 `${HOME}/.xsession`：

```text
# Load default window-manager
/usr/bin/x-window-manager&
# Start GNOME
exec /usr/bin/gnome-session
```

你可能还想让 `sawfish` 成为你的默认窗口管理器：

```text
# update-alternatives --config x-window-manager
```

有 4 个程序提供 `x-window-manager`。

| 选择 | 命令 |
| --- | --- |
| 1 | /usr/bin/sawfish |
| 2 | /usr/bin/X11/twm |
| 3 | /usr/bin/kde2 |
| \* 4 | /usr/X11R6/bin/wmaker |

```text
Enter to keep the default[*], or type selection number: 1
Using '/usr/bin/sawfish' to provide x-window-manager.
```
