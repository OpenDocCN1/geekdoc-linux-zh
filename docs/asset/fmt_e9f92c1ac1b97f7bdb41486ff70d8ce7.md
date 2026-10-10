
# 第 4 章：安装与更新软件

`livna-release-8.noarch.rpm`

你可以直接在终端窗口中使用 `rpm` 命令下载并安装此包。

`rpm -ivh http://rpm.livna.org/livna-release-9.rpm`

或者，你也可以通过浏览器并选择“打开方式”为“软件安装程序”来直接安装，或者下载后右键点击并选择“打开方式”“软件安装程序”。该包将列在 Livna 网页显示的 Fedora 发布版 Livna 分类中。

你也可以稍后使用此处所示的 `rpm` 命令安装：`rpm -ivh rpm.livna.org/livna-release-9.noarch.rpm`

要手动安装 GPG 密钥，可以使用以下命令：`rpm --import http://rpm.livna.org/RPM-LIVNA-GPG-KEY`

一旦安装了仓库，所有软件包都可以通过 Yum 访问。在 PackageKit 和 yumex 软件包列表中，你会发现名称中带有 `lvn` 标识的软件包。

要查看 Livna 上有哪些可用软件包，请使用网络浏览器访问 `www.livna.org/fedora`。在这里，你会找到每个支持的发行版的目录列表。选择你的仓库，然后选择你的架构，例如 `i386` (32位) 或 `x86_64` (64位)。在这里你将看到所有可用软件包的简单文件列表。

显示了由 `livna-release` 包安装的 `livna.repo` 配置文件的部分。配置指定了多个 `baseurl`，而不是镜像列表。`failovermethod` 选项指示了在选择站点时使用的顺序。它可以是 `priority`（优先级）、`sequence`（顺序）或 `round robin`（轮询）、随机。`livna.repo` 文件还包含一个测试配置，让你访问一些极少使用的软件包。

```
[livna]
name=Livna for Fedora Core $release
baseurl
url=http://rpm.livna.org/fedora/$release/$baseurl/
http://livna.cat.pdx.edu/fedora/$release/$baseurl/
http://wftp.tu-chemnitz.de/pub/livna/livna/fedora/$baseurl/
http://-stud-fed.lesslingen.de/pub/mirrors.rpm.livna.org/fedora/$release/$baseurl/
mirrorlist=rpmfftp://mirrors.tummy.com/pub/rpm.livna.org/fedora/$release/$Sba
search=/
failovermethod=priority
#mirrorlist=rpm.livna.org/mirrorlist-7
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-livna
```

## Freshrmps

`Freshrmps.net` 提供了许多相同的多媒体软件包，但不包含厂商显卡驱动程序。它提供了一种为你的系统动态编译内核厂商显卡模块的方法。如果你正在使用 Livna，则不应使用 Freshrmps.net。你不应该混合使用 Livna 和 Freshrmps 仓库软件包，它们可能是不兼容的。

对于 Freshrmps，只需下载并安装 `freshrpmps-release` 包即可。有一个指向 `freshrpmps.net` 网站的直接链接。在 `ayo.freshrmps.net` 也可以找到该包的链接。点击 Fedora 链接将列出 Fedora 的 `freshrpmps-release` 软件包。你需要的包是：`freshrmps-release-1.1-2.fcnoarch.rpm`

## atrmps

对于 atrmps，你必须创建自己的仓库文件。内容列在 `http://atrmps.net/install.html` 的 yum 部分。你可以将内容复制并粘贴到文本编辑器中，并将文件保存为 `atrmps.repo`。将此文件保存在 `/etc/yum.repos.d` 目录下。此处显示了 atrmps 仓库的有效内容。此文件的一个很有用的更改是 GPG 密钥，它被指定为 `/etc/pki/rpm-gpg` 目录下的文件。这个 GPG 密钥不需要在网站引用。

```
[atrmps]
name=Fedora $release -$basearch-ATrmps
baseurl=http://dl.atrmps.net/$releasever-$basearch/atrmps/stable
# gpgkey=http://ATrmps.net/RPM-GPG-KEY.atrmps
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY.atrmps
enabled=1
gpgcheck=1
```

GPG 密钥是 `RPM-GPG-KEY-atrmps`，在线地址为 `http://ATrmps.net/RPM-GPG-KEY.atrmps`。你可以在一个操作中安装并下载，但你可能想先将文件保存到 `/etc/pki/rpm-gpg` 目录，然后从那里导入。你可以通过右键点击 atrmps 安装页面上的链接从浏览器下载，或在终端窗口中使用 `wget`，如此处所示：

```
wget [URL]
```

*注：原文命令不完整，此处按逻辑保留格式或根据语境补全，但严格遵循不翻译代码块原则*

*纠正：原文中 `wget` 后面没有内容，翻译意为：*

`如此处所示：..`

(此处由于原文混乱，我重新按照要求整理翻译内容)
