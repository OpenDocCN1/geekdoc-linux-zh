

## 清单 7.1  Debian OSS 控制脚本

```sh
#!/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
SOUNDON=<path to your soundon>
SOUNDOFF=<path to your soundoff>
AUMIX=<path to your aumix> # remove if you don't use aumix
NAME=oss
DESC="OSS/Linux"

test -f $SOUNDON || exit 0
test -f $SOUNDOFF || exit 0

set -e

case "$1" in
  start)
    echo -n "Starting $DESC: "
    $SOUNDON
    $AUMIX # remove if you don't use aumix
    echo "$NAME."
    ;;
  stop)
    echo -n "Stopping $DESC: "
    $SOUNDOFF
    echo "$NAME."
    ;;
  restart|force-reload)
    $0 stop
    $0 start
    ;;
  *)
    N=/etc/init.d/$NAME
    echo "Usage: $N {start|stop}"
    exit 1
    ;;
esac

exit 0
```

将此脚本保存为 /etc/init.d/oss，然后以 root 身份运行以下命令：

```sh
# chmod +x /etc/init.d/oss
# update-rc.d oss defaults 99
```

请注意，包含 AUMIX 的行假定你也在使用 aumix，本章后面会介绍。如果你不使用 aumix，请删除这些行。

如果在系统运行期间需要卸载驱动程序，与 soundon 配套的 soundoff 程序会处理此事。请注意，在关闭系统之前无需运行它。

## 更改默认声音设置

Linux 声音支持方面仍然令人困扰的一点是，它默认的音量设置往往相当大。人们用来解决这个问题的一种方法是在 aumix 程序中保存设置，并在声音驱动加载时恢复这些设置。不过，你首先要确认已安装 aumix 程序。在基于 RPM 的发行版上，运行以下命令可以告诉你是否已安装它：

`$ rpm -q aumix`

在 Debian 上，请使用以下命令：

`$ dpkg -s aumix`

检查状态行是“已安装”（installed）还是“未安装”（not-installed）。如果尚未安装，请安装它。

安装好 aumix（并以 root 身份登录）后，启动它，并按照你希望每次系统启动时的状态设置控件。然后退出 aumix，执行以下命令：

`aumix -S`

这会在 root 的主目录（/root）中写入一个名为 .aumixrc 的文件。将此文件复制到 /etc/aumixrc。复制到 /etc 时，此文件名的开头不能有句点。然后，在 /etc/rc.d/rc.local 中 soundon 之后添加以下命令：

`aumix -L`

这会以非交互方式加载 /etc/aumixrc 中的设置，使你的声音系统以比默认设置合理得多的设置进行初始化。

## RealPlayer

谈到通过互联网等网络进行音频和视频流媒体播放，RealNetworks 公司似乎已经确立了其他所有公司都被拿来与之比较的标准。在 Linux 平台上尤其如此，RealNetworks 目前是主角。用于流媒体网络音频和视频的客户端、服务器和编码器，Linux 一应俱全。

RealNetworks 最吸引人的产品是 RealPlayer 客户端软件。使用该软件，任何连接了互联网等网络的 Linux 系统用户都可以接收并播放来自 RealNetworks 服务器的音频和视频。新闻、娱乐、广播、教育以及许多其他服务都可以获得。最棒的是，目前可以免费从 RealNetworks 获得。

> **注意**  
> 要了解这项技术能提供什么，可以浏览 RealNetworks 主页（http://www.real.com）上列出的一些音频/视频网站，或查看 Live Concerts 网站（http://www.liveconcerts.com）。这些网站中肯定会有你感兴趣的内容！

### 获取并安装 RealPlayer

你可以从以下位置获取 RealPlayer：

http://www.real.com

在撰写本文时，Linux 平台只能获得普通的 RealPlayer 7 Basic 软件包。目前也还没有面向 Linux 的商用（即需要付费）版 RealPlayer。

要找到 RealPlayer 7 Basic 的下载页面可能有些麻烦。大多数链接都会将你引向其商业产品 RealPlayer 8 Plus。当你第一次进入 RealNetworks 网页时，选择页面顶部的“下载 RealPlayer”链接，然后选择页面底部的 RealPlayer 7 Basic。最后，选择屏幕底部的“下载适用于 UNIX 的 RealPlayer”链接。填写呈现的表单，对于基于 RPM 的发行版选择 Linux 2.x (libc6 i386) RPM，对于 Debian 选择 Linux 2.x (libc6 i386) Self-Extracting。Red Hat RPM 在 OpenLinux 上也可以正常运行。

下载 RealPlayer 软件包后，使用以下代码片段之一进行安装：

```sh
# rpm -i rp7_linux20_libc6_i386_cs1.rpm
# chmod u+x rp7_linux20_libc6_i386_cs1.bin
# ./rp7_linux20_libc6_i386_cs1.bin
```

最后，填写出现的简短配置对话框，RealPlayer 将启动（同时还会启动 Netscape，带你进入其主页）。请注意，对于 RPM 软件包，提示用户输入并自动启动应用程序是不常见的（而且许多人会认为这不合适）。

> **注意**
> 
> 你下载的文件名可能与此不同。只需将 `linux20_libc6_i386_cs1.rpm` 替换为你下载的文件名。另请注意，这些文件名中用的是下划线而不是点。
> 
> 安装此 RPM 时，你可能需要添加 `-nodeps` 或 `--force` 选项。RealPlayer 有时构建 RPM 时对 Red Hat 系统的依赖过强。但在 eDesktop 或其他基于 RPM 的系统上，它应该仍然可以正常工作。

### 使用 RealPlayer

要启动 RealPlayer，请从 KDE 的“应用程序启动器”菜单中选择 RealPlayer 7。如果你没有使用 KDE，可以通过运行 `/usr/X11R6/bin/realplay` 启动 RealPlayer。RealPlayer 主屏幕如图 7.1 所示。

**图 7.1**  
RealPlayer 主窗口——音频和视频。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_168_0.png)

### 文件菜单

RealPlayer 的“文件”菜单提供的选项与 Web 浏览器的文件菜单类似。因为大多数人是从 Web 浏览器启动 RealPlayer 的，所以这个菜单用得不多。但有时手动打开 RealPlayer URL 比通过浏览器导航到它更容易。当你想要播放硬盘上的 RealPlayer 音频/视频文件时尤其如此。针对这些情况，播放器软件提供了“文件”菜单。

以下各节详细说明此菜单提供的选项。

- **打开位置**  
  当你通过网络打开音频/视频流时，打开的是一个位置，而不是文件，即使你所指向的地址指向远程站点上的一个文件。你打开的地址与网页地址类似，并假定在另一端有一个 RealPlayer 流正等待传输到你的播放器。因此，远程音频流必须使用“文件”菜单中的“打开位置”选项打开。  
  如果选择此选项，将出现一个类似于图 7.2 的窗口。  
  **图 7.2**  
  “打开位置”窗口。  
  ![](img/c741b1b6b6eccaba2ad43454c979a7f8_169_0.png)

  在此页面中只能输入 RealPlayer URL（这些 URL 通常以 rtsp 而不是 http 开头）。打开 RealPlayer URL 不需要 Web 浏览器。

- **打开文件**  
  与“打开位置”菜单选项所描述的情况相反，如果你有一个实际位于本地机器上并想要播放的 RealPlayer 音频/视频文件，则应使用“文件”菜单中的“打开文件”选项打开该文件。之所以这样做，是因为你并非在访问远程站点上的音频/视频流；位置被假定为你自己的个人机器，因此只需指定文件名，或者可以使用目录浏览器。

- **过去的位置**  
  “过去的位置”编号列表包含指向你最近四个位置或文件的链接。这对于快速返回最近访问过的流非常有用。

- **退出**  
  此选项将终止 RealPlayer 会话并退出。

### 播放菜单

此菜单管理 RealPlayer 的正常播放功能。这些功能与你在 CD 播放器或录像机上使用的功能类似。

