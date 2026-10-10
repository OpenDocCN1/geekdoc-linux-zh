
> “Linux：拥有**CLUE**的操作系统……**C**ommand Line **U**ser **E**nvironment（命令行用户环境）。”
> – 匿名（发布于 comp.software.testing）

## 使用终端

Linux 命令行，即终端（Terminal），是一个功能极其强大的环境。通过它，你可以让操作系统跪地求饶（指掌控其核心），也可以将其更新至惊艳的状态。你可以入侵远程计算机，观看动态 ASCII 篝火，安装新的应用程序和程序，观看从荷兰服务器上播放的《星球大战》，并编写复杂的自动化脚本。

在本节中，您将探索终端的复杂性及其在 Linux 中的工作方式。您将学习如何从终端操作 Linux 文件系统，并发现终端中一些奇特但有趣的功能。

在 Linux 世界中，终端至高无上。了解其工作原理，你就能获得所有的力量。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_44_0.png)

## 终端基础

大多数操作系统使用两种类型的界面：GUI（图形用户界面，即 Windows、macOS 和 Linux Mint 启动后的桌面）以及命令行。虽然现代操作系统对命令行有所回避，但 Mint 使用终端来赋予用户更大的系统控制权。

### 接管命令

命令行，或称为终端，是一个极其强大的界面。你在桌面上能做的所有事情，都可以在终端中完成。让我们从了解它是如何工作的开始。

- **步骤 1**：你可以通过点击面板上的终端图标来访问终端，该图标位于 Firefox 和文件图标之间；或者通过打开菜单，从左侧快速启动条中选择终端来启动它。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_45_0.png)

- **步骤 2**：终端允许你访问 Linux Mint Shell，称为 Bash，它让你能够访问底层操作系统。Mint 中的所有元素，包括桌面和 GUI，都是从命令行运行的模块。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_45_2.png)

- **步骤 3**：你目前在终端中看到的内容是你的登录名，后面跟着计算机名称；即你首次安装 Mint 时设置时的名称。该行以当前文件夹名称结尾；起初这只是一个波浪号 ~，意味着你的主目录（Home 文件夹）。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_45_1.png)

- **步骤 4**：行末闪烁的光标是你输入基于文本的命令的位置。你可以开始尝试一个简单的命令：打印当前工作目录（Print Working Directory，pwd），它会将你当前所在的文件夹输出到屏幕上。输入 pwd 并按下 Enter 键。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_45_3.png)

- **步骤 5**：你输入的所有命令工作方式相同：你输入命令，包含任何扩展命令用途的参数，并按下 Enter 键执行你输入的命令行。在终端中输入：uname -a 并按下 Enter。这会显示一些关于 Mint 的系统信息。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_46_0.png)

- **步骤 6**：在我们开始输入命令之前，让我们花点时间看看终端提供哪些菜单选项。File（文件）菜单选项允许你打开一个新的终端，创建一个新配置档（profile），在其中你可以更改终端的大小、颜色和行为规范，添加一个新标签页，以及关闭所有当前活动的终端会话。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_46_1.png)

- **步骤 7**：Edit（编辑）选项允许你将命令复制和粘贴到终端以及其他来源；当你想要从网页复制一个非常长且复杂的命令时，这很有用。它还允许你编辑当前配置首选项。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_46_2.png)

- **步骤 8**：View（查看）和 Search（搜索）选项允许你更改终端窗口的大小，当然也可以搜索终端内的任何特定关键词。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_46_3.png)

- **步骤 9**：Terminal（终端）条目扩展了配置编辑和大小调整，并允许你更改字符编码。有趣的是，你甚至可以将其设置为**只读**模式，这禁止你在终端中输入任何命令；当你需要永久显示终端内容时，这很有用。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_46_4.png)

- **步骤 10**：最后，Help（帮助）选项显示终端的帮助内容和版本号，或者更准确地说，是 GNOME Terminal；我们今后将简单地称之为终端。内容值得一读，以帮助熟悉终端的工作方式。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_46_5.png)

## 通过终端更新 Mint

到目前为止，你一直在使用盾牌图标启动 Mint 更新管理器来更新系统并升级当前安装的应用程序、工具和其他元素。然而，你也可以从终端完成完整的系统更新和升级。

### 使用 apt-get

要通过终端更新和升级，你使用 APT（Advanced Packaging Tool，高级打包工具）命令。这是一个强大的命令，它根据用途结合不同的元素。

- **步骤 1**：首先，打开一个新的终端，或者如果你已经打开了一个，使用 `clear` 命令清除其内容。这为你提供了一个干净的开始。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_47_0.png)

- **步骤 2**：在终端中输入：**apt-get**。这会显示最常用的 apt-get 命令列表，以及每个命令功能的简要描述。即使此时你无法完全理解，也值得一看。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_47_2.png)

- **步骤 3**：APT-get 用于更新和升级 Mint，以及 Ubuntu 和其他基于 Debian 的发行版中的软件。使用 Update 元素获取新的软件包列表并更新源列表。Upgrade 下载并将这些文件升级到最新版本。要开始整个升级和更新过程，输入：**sudo apt-get update**，然后输入你的密码。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_47_1.png)

- **步骤 4**：现在请注意 sudo 命令的添加。sudo 命令曾经意味着“超级用户执行”（Super User Do）；如今，更常见的说法是“替代用户执行”（Substitute User Do）。这意味着管理用户（超级用户）使用 APT（高级打包工具）获取任何更新。现在尝试这个：**sudo apt-get upgrade**。

![](img/7801ba6bee6a3a08f7f02897cdbcd867_47_3.png)

- **步骤 5**：根据你的更新状态，如果有任何等待安装的内容，系统可能会询问你是否要应用 `sudo apt-get upgrade` 命令的结果。你可以按 **Y** 接受并继续。这里发生的是 apt-get 有一些要应用于 Mint 的更新软件，而你正在确认此操作。

```
Reading state information... Done
The following NEW packages will be installed:
  libyaml-perl
E: Unable to locate package libyaml-perl
david@david-mint:~$ sudo apt-get update && sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
```

- **步骤 6**：终端窗口可能会显示一长串看起来像乱码的内容，但不要担心。升级所需的文件已被下载、准备、解包、处理、安装并正确设置。执行升级时，即使是最小的软件包，背后也有大量操作在进行。

```
Preparing to unpack .../linux-headers-4.9.0-55-generic_4.9.79-55.88_amd64.deb ...
Unpacking linux-headers-4.9.0-55-generic (4.9.79-55.88) over (4.9.4-6.67.88) ...
Preparing to unpack .../linux-headers-4.9.0-generic_4.9.79-55.88_all.deb ...
Unpacking linux-headers-4.9.0-generic (4.9.79-55.88) over (1.5.212.4) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for docutils (0.14+dfsg-1) ...
Processing triggers for libdrm2 (1.0.0-1) ...
Processing triggers for systemd (2.9.9-0ubuntu6) ...
Processing triggers for shared-mime-info (1.4-1) ...
Processing triggers for libgdk-pixbuf-2.0-0 (2.32.4) ...
Setting up grub-common (2.02+dfsg-25.6.8ubuntu2.5) ...
Setting up linux-image-4.9.0-55-generic (4.9.79-55.88) ...
Setting up linux-headers-4.9.0-55-generic (4.9.79-55.88) ...
Processing triggers for initramfs-tools (0.118) ...
Updating initramfs in /boot/initrd.img-4.9.0-55-generic ...
Processing triggers for shared-mime-info (1.4-1) ...
Processing triggers for desktop-file-utils (0.22) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for libc-bin (2.23-0ubuntu6) ...
Processing triggers for man-db (2.7.5-1) ...

Setting up libyaml-perl (4.4-1) ...
Setting up linux-headers-4.9.0-generic (4.9.79-55.88) ...
Processing triggers for linux-headers-4.9.0-55-generic (4.9.79-55.88) ...
  /etc/kernel/postinst.d/dkms
  /etc/kernel/postinst.d/dkms
dkms: autoinstall for kernel: 4.9.0-55-generic
dkms: autoinstall for kernel: 4.9.0-55-generic
dkms: autoinstall for kernel: 4.9.0-55-generic

Preparing to unpack .../libyaml-perl_4.4-1_amd64.deb ...
Unpacking libyaml-perl (4.4-1) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for libc-bin (2.23-0ubuntu6) ...
Processing triggers for shared-mime-info (1.4-1) ...
Processing triggers for desktop-file-utils (0.22) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for shared-mime-info (1.4-1) ...
Processing triggers for desktop-file-utils (0.22) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for shared-mime-info (1.4-1) ...
Processing triggers for desktop-file-utils (0.22) ...
Processing triggers for mime-support (3.60ubuntu1) ...
```

- **步骤 7**：基本上，就是这样了，你的系统现在根据 apt-get update 命令可用的软件包列表已经更新到最新。你可以再运行一遍这个过程，以检查一切是否顺利。总结一下，输入：`sudo apt-get update`，按下 **Enter**，然后输入：`sudo apt-get upgrade` 并按下 **Enter**。

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages will be automatically installed and are no longer required:
  libcopylxml-3.8 libcrypto-1.0.0-ssl libgcc-4.8-dev
  libmysqlclient18 libncurses5 libncurses5-dev libperl5.22 libpthread-stubs0-dev libssl1.0.0 libstdc++-4.8-dev libtcl8.6-0 libyaml-0.2-2
E: Unable to locate package libyaml-perl
david@david-mint:~$ sudo apt-get update && sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
```

- **步骤 8**：有趣的是，Linux Mint 以及其他一些发行版允许你将多个命令链接在一起。因此，在这个例子中，我们可以使用 `sudo apt-get update && sudo apt-get upgrade`。双与符号（&&）用于组合命令，只要前一个命令顺利执行，它就完美运作。建议在任何会话开始时使用更新和升级组合。

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages will be automatically installed and are no longer required:
  libcopylxml-3.8 libcrypto-1.0.0-ssl libgcc-4.8-dev
  libmysqlclient18 libncurses5 libncurses5-dev libperl5.22 libpthread-stubs0-dev libssl1.0.0 libstdc++-4.8-dev libtcl8.6-0 libyaml-0.2-2
E: Unable to locate package libyaml-perl
david@david-mint:~$ sudo apt-get update && sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
```

### 终端 vs 更新管理器？

无论使用哪种发行版，为什么使用终端而不是更新管理器来进行更新和升级？一些用户强烈倾向于使用终端来更新他们的 Linux 系统及附带的应用程序，认为这样更好。然而，事实往往并非如此。

使用终端的 `apt-get` update 并不处理软件包版本之间依赖关系的变更，因此，如果一个软件包从一个版本到另一个版本的依赖字段发生了变更，那么更新可能会被搁置。

更新管理器，或软件管理器（取决于发行版），通常会分阶段进行更新，并标记那些依赖关系发生变化的软件包以进行更新。然而，这就是 Linux 常常令人困惑的地方，有时它并不这样做。

归根结底，这取决于正在更新的软件包的开发人员，以及该发行版仓库中软件包的存放方式，还有该更新是否被分类为稳定版。从本质上说，从用户的角度来看，如果你定期使用终端和更新管理器两者进行更新和升级，那么你将保持尽可能最新的状态，并获得软件包和核心软件的基本且必要的稳定版本。如果你在寻找前沿的软件包更新，最好选择滚动发布（rolling release）发行版。

