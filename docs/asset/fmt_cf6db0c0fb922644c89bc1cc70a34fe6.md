
# 第1章 压缩、系统备份与软件安装

```
是否继续 [y/n]
正在下载软件包：
正在设置并读取 Presto delta 元数据
http://www.muug.mb.ca/pub/fedora/linux/updates/i386/repodata/2699347f72edbb28dc74f46f715d383f6f7bbd95e89d50277ecc6c130af5-prestodelta.xml: [Errno 14] HTTP Error 404
http://www.muug.mb.ca/pub/fedora/linux/updates/i386/repodata/2699347f72edbb28dc74f46f715d383f6f7bbd95e89d50277ecc6c130af5-prestodelta.xml. [Errno 14] HTTP Error 550
正在尝试其他。
http://www.muug.mb.ca/pub/fedora/linux/updates/i386/repodata/2699347f72edbb28dc74f46f715d383f6f7bbd95e89d50277ecc6c130af5-prestodelta.xml.
正在尝试其他。
正在处理 delta 元数据
待下载软件包大小: 27 M
(1/3): firefox-3.6.7-1-fc13.i686.rpm
(2/3): xrunner-1.9.2-7-fc13.i686.rpm
(3/3): xrunner-devel-1.9.2-7-fc13.i686.rpm

| 总计 | 速度 | 大小 | 时间 |
| :--- | :--- | :--- | :--- |
| 382 kb/s | 27 Mb | 01:11 |
```

运行 `rpm_check_debug`

正在测试事务

事务测试成功

正在执行事务

正在更新 : `xrunner-1.9.2-7-fc13.i686` 1/6

正在更新 : `xrunner-devel-1.9.2-7-fc13.i686` 2/6

正在更新 : `firefox-3.6.3-4-fc13.i686` 3/6

正在清理 : `firefox-3.6.3-4-fc13.i686` 4/6

正在清理 : `xrunner-devel-1.9.2.3-1-fc13.i686` 5/6

正在清理 : `xrunner-1.9.2-3-1-fc13.i686` 6/6

```
已更新：

firefox.i686 0.3:6.7-1-fc13

依赖更新：

xrunner.i686 0.1.9.2-7-fc13

xrunner-devel.i686 0.1.9.2-7-fc13
```

完成！
`[root@server1]#`

从之前的输出可以看出，你的命令在安装 `Firefox` 之前找到了并安装了两个依赖包：`xrunner` 和 `xrunner-devel`。

## 软件安装

`yum` 命令在找到接受连接的仓库之前，尝试了两个包含必要软件的不同软件仓库（称为软件镜像）。这是很常见的，因为软件仓库会限制并发连接数以允许快速下载。当软件仓库达到其并发连接限制时，它会向 `yum` 命令返回负面响应，然后 `yum` 会搜索 `yum` 配置中列出的下一个软件镜像。

`GNOME` 和 `KDE` 桌面环境包含一个“软件更新”工具，该工具会定期检查系统中安装软件的更新 `RPM` 软件包。如果你在通知窗口中选择“更新”选项，它将通知你任何新版本的软件包，并使用 `yum` 命令自动下载并安装它们。你也可以在 `GNOME` 桌面环境中手动运行“软件更新”工具，打开系统菜单并导航到“管理”，“软件更新”。

![](img/bafa5678973f896b93838a140b8f7840_538_0.png)

未在 `Fedora` 默认仓库托管的软件包仍然可以使用 `yum` 命令下载和安装。许多软件作者将其软件包托管在私有仓库中，并在其网站上提供说明，引导你完成将私有软件仓库添加到 `yum` 配置文件的过程（通过安装特殊的 `RPM` 并使用 `yum` 命令安装软件包）。例如，如果你想安装 `VLC` 媒体播放器，可以访问这些针对 `Fedora` 13 的说明：`http://www.videolan.org/afric/download-load-vlc.html`。`VLC` 媒体播放器托管在私有的 `RPM Fusion` 仓库中，`VLC` 媒体网站引导你运行带有 `RPM Fusion` 仓库位置的 `yum` 配置文件：

```
[root@server1]# # rpm -ivh

http://download.rpmfusion.org/free/fedora/rpmfusion-release.noarch

正在检索 http://download.rpmfusion.org/free/fedora/rpmfusion-release.noarch

正在安装 http://download.rpmfusion.org/free/fedora/rpmfusion-release.noarch

################ [100%]

正在更新 : xrunner-1.9.2-7-fc13.i686

正在更新 : xrunner-devel-1.9.2-7-fc13.i686

正在更新 : firefox-3.6.3-4-fc13.i686

正在清理 : firefox-3.6.3-4-fc13.i686

正在清理 : xrunner-devel-1.9.2.3-1-fc13.i686

正在清理 : xrunner-1.9.2-3-1-fc13.i686
```
