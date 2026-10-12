

### 4. 将第一个 CD ISO 文件中的 `isolinux` 目录和 `.discinfo` 文件复制到 `/tmp` 目录（该目录恰好是当前目录）。

输入以下命令以复制文件：

```
cp -af ISO1/isolinux ISO1/.discinfo .
```

不要遗漏命令末尾的那个单点号！

### 5. 使用文本编辑器打开 `.discinfo` 文件，并按如下方式编辑第四行：

```
1,2,3,4
```

该行列出了包含在 DVD ISO 映像中的 CD ISO 映像的编号。编辑完该行后，保存 `.discinfo` 文件。

### 6. 使用四个 CD ISO 文件创建 DVD ISO 文件。

输入以下较长的 `mkisofs` 命令以创建一个名为 `fedora-core-dvd.iso` 的新 ISO 文件：

```
mkisofs -o fedora-core-dvd.iso \
       -V 'Fedora Core DVD' \
       -b isolinux/isolinux.bin -c isolinux/boot.cat \
       -no-emul-boot -boot-load-size 4 -boot-info-table \
       -R -m TRANS.TBL \
       -x ISO1/.discinfo \
       -x ISO1/isolinux \
       -graft-points ISO1 \
       .discinfo=.discinfo isolinux==isolinux \
       Fedora/=IS02/Fedora \
       Fedora/=IS03/Fedora \
       Fedora/=IS04/Fedora
```

现在你可以将 DVD ISO 文件刻录到 DVD 介质上。

## 将 DVD ISO 文件刻录到 DVD 介质上

假设 DVD ISO 文件名为 `fedora-core-dvd.iso`，请按照以下步骤将 DVD ISO 文件刻录到 DVD 上：

1.  使用 `cd` 命令将当前目录更改为 DVD ISO 文件所在的位置。
2.  将一张空白 DVD 介质放入 DVD 光驱中。
3.  输入以下 `growisofs` 命令以开始刻录 DVD：

```
growisofs -Z /dev/scd0=fedora-core-dvd.iso
```

请记住，将 DVD 光驱设备名从 `/dev/scd0` 更改为你的 PC DVD 光驱适用的名称。对于外部 DVD 光驱，使用 `/dev/scd0` 作为设备名。对于内部 DVD 光驱，使用 `/dev/cdrom` 作为设备名。

## 执行 FTP 安装

如果你想在拥有 CD 光驱的笔记本电脑或台式 PC 上安装 Fedora Core，你可以从另一个拥有 Fedora Core 发行文件的系统通过 FTP 进行安装。即使你有 CD 光驱，如果你是在网络中的多台 PC 上安装 Fedora Core 且不想逐个插入 CD，那么 FTP 安装也很有意义。本节将引导你完成 FTP 安装。

### 你需要准备的内容

以下是你需要用来刻录 Fedora Core CD 的内容：

-   一张 Fedora 启动 CD，用于引导 PC。当前的 Fedora Core 安装内核太大，无法存储在软盘中，因此你只能从 CD 启动。
-   一个局域网，其中包含另一台拥有 Fedora Core CD ISO 文件的 Fedora Core 或 Red Hat Linux 系统。
-   一台通过网络连接且你希望通过 FTP 安装 Fedora Core 的 PC。

### 操作步骤

请按照以下步骤，通过网络从 Fedora Core ISO 文件执行 FTP 安装：

1.  **在拥有 Fedora Core ISO 文件的 Linux 系统上，将四个 ISO 文件挂载到四个挂载点上。**

    我假设这四个 ISO 文件位于 `/usr/local` 目录中，文件名分别为 `disc1.iso`、`disc2.iso`、`disc3.iso` 和 `disc4.iso`。以 root 身份登录，并在终端窗口中输入以下命令：

    ```
    mkdir /var/ftp/pub/fedora
    cd /var/ftp/pub/fedora
    mkdir disc1
    mkdir disc2
    mkdir disc3
    mkdir disc4
    mount -o loop,ro /usr/local/disc1.iso disc1
    mount -o loop,ro /usr/local/disc2.iso disc2
    mount -o loop,ro /usr/local/disc3.iso disc3
    mount -o loop,ro /usr/local/disc4.iso disc4
    ```

    请记住，将 Fedora Core ISO 文件的路径名替换为正确的目录和文件名。

2.  **确保挂载了 Fedora Core ISO 文件的 Linux 系统上正在运行 FTP 服务器。**
    在终端窗口中输入以下命令：
    ```
    service vsftpd restart
    ```

3.  **创建一张 Fedora Core 启动 CD。**
    使用 CD 刻录机刻录名为 `boot.iso` 的 ISO 映像——该文件位于 `/usr/local/disc1.iso/images` 目录中。有关如何从 ISO 映像刻录 CD 的说明，请参阅“刻录 Fedora Core CD”部分。

4.  **前往你希望执行 FTP 安装的 PC，插入启动 CD，并重启 PC。**
    PC 重启后，片刻之后，文本屏幕将显示欢迎消息和 `boot:` 提示符。

5.  **输入 linux askmethod 并按 Enter 键。**
    文本菜单将显示各种安装方法。

6.  **选择 FTP 作为安装方法并按 Enter 键。**
    系统将提示你为该 PC 配置 TCP/IP 网络。

7.  **选择“动态 IP 配置”并选择“确定”。**
    如果你的网络不支持动态 IP 地址，请输入该 PC 的有效 IP 地址。配置好 TCP/IP 网络后，将显示 FTP 设置屏幕。

8.  **输入挂载了 Fedora Core ISO 文件的 FTP 服务器的 IP 地址或名称。**
    对于联网 PC，你甚至可以指定互联网上任何拥有 Fedora Core 发行版的服务器。有关此类服务器的列表，请查阅 `fedora.redhat.com/download/mirrors.html`。

9.  **指定 Fedora Core ISO 文件所在的目录并按“确定”。**
    对于步骤 1 中的示例，请输入 `/pub/fedora` 作为目录。在此步骤之后，正常的图形化安装将开始。

10. **响应图形化安装步骤中的提示，并照常继续安装。**

# 第二卷

# 工作站与应用

# 第五浪
作者：Rich Tennant

![](img/9f89727199836b0f871f1745838aa8b2_135_0.png)

“那个很难保持网络连接的人就是你吧？”

# 内容概览

-   第 1 章：探索图形用户界面桌面 ................................................ 111
-   第 2 章：学习 Shell ....................................................... 135
-   第 3 章：导航 Linux 文件系统 ...................................... 153
-   第 4 章：探索 Fedora Core 应用程序 .................................... 169
-   第 5 章：使用文本编辑器 ...................................................... 199

# 第 1 章：探索图形用户界面桌面

## 本章内容

-   学习 GUI 的常见功能
-   在 GNOME 中使用 Nautilus shell
-   配置 GNOME
-   在 KDE 中使用 Konqueror
-   配置 KDE

Fedora Core 附带了两个图形用户界面（GUI）——GNOME 和 KDE。GNOME 和 KDE 类似于 Microsoft Windows，但在一点上很独特。与 Microsoft Windows 不同，你可以在 Fedora Core 中自由选择你的 GUI。如果你不喜欢 GNOME，只需注销并以另一个 GUI——KDE 重新登录即可。试试看用 Microsoft Windows 做同样的事！

![](img/9f89727199836b0f871f1745838aa8b2_137_0.png)

GNOME 和 KDE 是独立于 Linux 开发的。事实上，GNOME 和 KDE 也运行在除 Linux 以外的其他 UNIX 操作系统上。你还有选择可以在 Fedora Core 上安装其他 GUI。例如，你可以下载并安装 Ximian Desktop 2 (XD2)——这是来自 Ximian 的一个 GUI 桌面，可从 www.ximian.com/products/desktop/download.html 获取。

本章探讨 GNOME 和 KDE 的主要功能。你只需开始使用这些 GUI 就能最好地掌握它们。顺便说一下，只要你在安装 Fedora Core 时安装了这两个 GUI，你就可以同时尝试 GNOME 和 KDE。否则，GNOME 是 Fedora Core 的默认 GUI。

# 学习 GUI 的常见功能

从用户角度来看，GNOME 和 KDE 可能看起来相似，因为许多功能的工作方式相似。熟悉这些常见功能很有帮助，这样无论你选择哪种 GUI 用于日常工作，都可以依赖它们。

首先，GNOME 和 KDE 的初始桌面看起来与其他流行的 GUI 一样，例如 Microsoft Windows 或 Mac 上的 Apple 桌面。例如，图 1-1 显示了初始的 GNOME 桌面。

![](img/9f89727199836b0f871f1745838aa8b2_138_0.png)

**图 1-1：** GNOME 桌面看起来与其他流行的 GUI 桌面相似。

桌面最初显示你的计算机、你的主文件夹以及用于删除文件的回收站的图标。GNOME 和 KDE 桌面的另一个主要功能是沿底部的栏，称为 *panel*（面板）。面板类似于 Windows 任务栏。左侧有按钮（到各种程序的 *快捷方式*），右侧有 *音量* 控制、*可用更新* 图标和时间显示。面板的中间部分显示你启动的任何应用程序的按钮（或自动启动的）。

![](img/9f89727199836b0f871f1745838aa8b2_138_1.png)

将鼠标悬停在面板上的任何图标上，一个小弹出窗口将显示该图标的名称。弹出窗口还提供关于你可以使用该图标做什么的 *提示*。

# 桌面弹出菜单

当你右键点击桌面空白区域时，GNOME 和 KDE 桌面都会显示弹出菜单。该菜单的具体内容取决于桌面，但它通常提供菜单选项，使你能够执行以下类型的任务：

-   打开一个 *终端* 窗口，你可以在其中输入 Linux 命令。
-   创建一个新的 *文件夹*。

