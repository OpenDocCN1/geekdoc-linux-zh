
像其他所有 SSH 客户端一样，你通过 `exit` 关闭连接。这会让浏览器窗口保持打开并在中心列出一个按钮。这将刷新屏幕并重新打开到远程主机的连接。

## 23 保存连接

遗憾的是，没有真实的方法可以在浏览器内“存储”一组到不同机器的连接。最好的是在不同的端口上配置系列请求，然后你可以将 URL 作为浏览器的书签。

## 18 启动客户端

要启动客户端，你只需要打开浏览器并输入 `http://yourmachine.com:4200`，其中你更改了使用的端口。这将打开一个终端窗口，你可以在其中输入用户名和密码。

## 19 连接到不同的机器

登录后，你可以直接 `SSH` 到另一台机器。但如果这是你想做的事，可以使用 `ssh -S myshost@host`。这意味着你可以连接到不同的机器，每个机器都有自己的端口。

## 20 连接选项

由于这是最新可用的基于 Web 的 SSH 客户端，你根本没有相同级别的配置选项。

## 24 现在去哪里？

希望本教程能向你展示当你遇到不幸的锁定的域名时可用的选项。如果它不符合你的具体情况，不要害怕在野外寻找一些选项。

## 17 启动服务器

一旦安装了 `shellinbox`，只需在远程主机上启动 `shellinbox` 即可完成。大量的

## 16 安装

一旦下载了源码，你需要使用通常 `./configure; make install` 脚本进行安装，这在大多数 Linux 发行版中都有效。在你想要连接的远程主机上，

# 在你的系统上安装 Cinnamon

- 拥有更传统的应用程序菜单，同时具备较新桌面的搜索功能
- 自定义应用布局，让你轻松访问喜爱的程序
- 查找并安装扩展（如小组件和桌面扩展）来增强你的用户体验
- 使用 `Linux Mint MDM` 显示管理器来获得完整的 `Linux Mint` 体验

![](img/4c82285250803e975d41cda3a51d081f_43_0.png)

# 在你的系统上安装 Cinnamon

学习如何在一些流行的桌面发行版安装 Cinnamon 桌面环境，以及如何根据你的需求对其进行配置

> 顾问 Rob Zetsloot 负责复杂系统建模，是一名 Python Web 开发者。他热于计算实验。

Cinnamon 2.0 是 Linux Mint 桌面环境的下一次也是最重要的迭代。虽然它最初是 GNOME 的分支，但 Cinnamon 2.0 现在已完全从 GNOME 后端移除。它不仅适用于 Mint；它是一个完全开源的项目，并且可以从你选择的任何 Linux 发行版中获取。

# 资源

- `cinnamon.linuxmint.com/7?page_id=61`
- 使用 ONE 一键安装包：`software.opens.org/package/cinnamon`

虽然某些发行版在仓库中已经包含了它

我们将介绍如何在 Fedora、openSUSE、Debian 和 Ubuntu 上安装它。然而，这些方法适用于更多发行版，而且这些自定义方法对 Linux Mint 用户同样有用。

# 在你的系统上安装 Cinnamon

如何在流行的桌面发行版上安装 Cinnamon

# 教程

在我们所有要安装 Cinnamon 的发行版中，你都需要注销，以便它以用户身份加入你当前的环境供选择。要开始使用 Cinnamon，你需要注销，在屏幕上找到会话管理器并切换到 Cinnamon

完成后，注销并选择 Cinnamon 会话。

## 03 openSUSE

对于 openSUSE，你需要确保已安装了 Cinnamon——可以通过使用 GNOME 界面或直接安装来实现。然后，你可以使用 openSUSE 软件包网站的一键方法获取 Cinnamon。

## 04 Debian

Cinnamon 不是 Debian 的默认软件包，因此你需要为它添加 APT 仓库。首先，在此处查找仓库列表：

## 06 Ubuntu

Linux Mint 团队为 Ubuntu 维护了一个包含最新版本 Cinnamon 的 PPA。要将此添加到 Ubuntu，请打开终端并输入：

Cinnamon 在大约一年前被添加到 Fedora 仓库，如果你不喜欢 GNOME Shell，将其作为替代方案安装非常简单。安装命令为：

```
$ sudo yum install cinnamon
```

```
echo 'deb http://packages.linuxmint.com/rolling release main' | sudo tee /etc/apt/sources.list.d/cinnamon
```

## 05 Debian

添加后，你需要使用以下命令更新 Apt：

```
$ sudo apt-get update
```

...并使用以下命令安装密钥和桌面环境：

```
$ sudo apt-get install linux-cinnamon
```

```
$ sudo apt-get install cinnamon-cinnamon-settings
```

当系统提示确认时，按回车键。

# Ubuntu

一旦添加了 PPA，你需要更新 Debian 中的软件列表。执行以下操作：

```
$ sudo apt-get update
```

完成完成后，你只需运行一个命令即可安装它：

```
$ sudo apt-get install cinnamon
```

## 08 Ubuntu

如果你使用的是 Ubuntu，会话选择不是首要步骤。在 Cinnamon 安装后注销，然后点击你的用户名。旁边是 Ubuntu 图标——点击该图标将打开会话管理器，Cinnamon 将列在其中。

## 09 Cinnamon

Cinnamon 的工作方式与 GNOME 或 Unity 不同——顶部有一个传统的面板，所有选项都清晰可见。Mint 菜单的工作原理类似，尽管它不是占据整个屏幕，而是在侧边打开，允许你搜索应用程序和文档。

![](img/4c82285250803e975d41cda3a51d081f_44_0.png)

基于 GNOME-shell 技术的 Linux 桌面环境

Cinnamon 桌面提供了新功能和传统的用户体验。底层技术源自 GNOME，但桌面布局更接近 GNOME。重点在于让用户感到如家，并为他们提供易用的体验。

- openSUSE Factory
- openSUSE 12.3
- openSUSE 12.2
- openSUSE Tumbleweed

显示不支持的发行版的更多包

| 名称 | 版本 | 构建 | 大小 | 来源 | 仓库 |
|---|---|---|---|---|---|
| meta-data | ... | ... | ... | ... | ... |

![](img/4c82285250803e975d41cda3a51d081f_44_1.png)

# 教程 在你的系统上安装 Cinnamon

![](img/4c82285250803e975d41cda3a51d081f_45_0.png)

## 快速启动

现在我们可以开始自定义使用 Cinnamon 的方式。首先，我们可以开始在屏幕底部面板的快速启动栏中添加应用程序。打开 Mint 菜单，将你想添加的任何程序拖放到工具栏上。通过右键点击，

![](img/4c82285250803e975d41cda3a51d081f_45_1.png)

我们可以让顶部和底部都有面板，并经典模式。

## 桌面组件 (Desklets)

Cinnamon 的功能之一是可以添加桌面组件，这些类似于 Android 或其他操作系统的桌面小部件。你可以在系统设置的“桌面组件”中找到它们，你可以从网上下载一些额外的。

## 收藏 (Favorites)

Mint 菜单侧边列了一些应用，我们可以在添加收藏。可以通过右键点击应用并选择“添加到收藏”来添加或删除它们。你还可以向上向下移动它们。

![](img/4c82285250803e975d41cda3a51d081f_45_2.png)

## 装饰你的桌面

使用 Cinnamon 网站获取桌面组件和小组件非常简单，也可以通过 `cinnamon-mint.com` 访问。有些已经在小组件菜单中了，但你可以搜索更好的桌面组件主题。将文件解压到 `~/.local/share/cinnamon/applets` 然后激活面板。

![](img/4c82285250803e975d41cda3a51d081f_45_3.png)

## 面板 (Panel)

在系统设置中，你会找到面板选项。这允许你将面板移动到屏幕顶部，更像 GNOME 2。

## 小组件 (Applets)

小组件在桌面组件之前，允许你向面板添加功能。右键点击面板将进入小组件菜单，你可以添加一些实用的工具，如显示如果你使用不同的显示器，这样你就不用把鼠标移动到角落了。

![](img/4c82285250803e975d41cda3a51d081f_45_4.png)

## 管理显示
