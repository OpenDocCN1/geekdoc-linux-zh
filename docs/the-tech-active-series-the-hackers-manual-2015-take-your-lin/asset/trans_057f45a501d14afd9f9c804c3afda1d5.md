

## Can I share with you... there?

shares, OpenStack object storage 或第三方存储，如 Google Drive、Dropbox、Amazon S3。这里令人兴奋的新增功能是能够在 OwnCloud 安装之间共享——也就是所谓的服务器到服务器共享。设置起来很简单，你可以为用户启用特定的 OwnCloud 共享，或者如果你信任他们，可以授予他们连接 OwnCloud 资源自由。显然，他们访问每个资源都需要自己的登录凭据。

服务器到服务器共享消除了从一个云下载文件到桌面再上传到另一个云这种 otherwise 尴尬流程的麻烦。更不用说拥有三个不同版本的同一文件在各处飞来飞去所带来的所有同步问题了。但 OwnCloud 承诺在未来版本中会有更多功能，其愿景是所谓的“数据联合”，在其中你可以在云之间无缝共享文件，而无需显式访问它们。这更进一步抽象掉了服务器之间的边界。

Web 界面也得到了一些润色，现在对移动设备更加友好，尽管移动用户可能更愿意使用专用应用。文档是懒加载的，因此文档或庞大的照片库会在你操作不断缩小的滚动条时分块读取。虽然这使事情看起来初始更快，但在某些情况下会有些别扭。

最值得注意的是 Pictures 应用，目前没有按日期排序的选项，因此如果你只想在一个大型文件夹中查看最新的照片，那么请准备好进行长时间的滚动和等待时间。关于此问题已提交了错误报告，并且改进的懒加载计划在 7.0.3 中推出。

存在适用于 Android 或（颤抖）iDevices 的应用，因此你可以在外出时或懒得走到电脑前时获取数据。目前它们在官方商店的价格为 63p 和 69p，但 Android 版是开源的，如果你手头拮据，可以从其他来源（如 F-Droid）免费获取。不幸的是，这些应用并没有像其 Dropbox 和 Google Drive 同行那样性感。特别是上传多个文件必须一个一个进行，而且没有上传整个文件夹的选项。这对某些人来说可能是致命缺陷，但不必如此：OwnCloud 可以通过 WebDAV 协议共享其文件，并且有各种各样的应用可以在你的标签页和移动设备上同步共享。

如果你太酷而不想设置传统安装方法，那么在 https://registry.hub.docker.com 上有几个现成的可供使用

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_79_0.png)

## Appy appy fun bus

OwnCloud 附带了许多可选应用程序，包括日历和联系人列表，以及前面提到的文档和图片应用。随着 OwnCloud 社区的成长，出现了许多令人兴奋的第三方应用程序。事实上，你可以在 http://apps.owncloud.com 上浏览一大堆它们。

例如，你可以下载一个名为 Music 的应用，它会为你索引音乐目录，然后通过精美的 HTML5 界面让你播放。它还可以与 Ampache 媒体服务器协同工作，以便你的文件可以通过任何兼容客户端播放。在 LXP 办公室里最受欢迎的、毫无疑问的是 Chat 应用程序，通过它各种各样无法在法律上重现的对话被传输，全部以测试的名义进行。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_79_1.png)

官方桌面客户端是一个简单但功能齐全的 Qt4 应用程序，它安静地驻留在系统托盘中，并在同步时以与 Dropbox 等效的方式通知你。默认情况下，它会将整个 OwnCloud 账户同步到本地目录 ~/owncloud，但你可以根据自己的云偏好挑选文件夹。

## Syncing on my mind

你也可以设置带宽限制。桌面客户端在你使用 Gnome 时看起来有点别扭，因为其系统托盘会消失，不过理论上，一旦你完成配置，就不再需要与之交互了。显然，如果你想同步到远程机器，桌面客户端就没什么用了：在这种情况下，你需要使用前面提到的 WebDAV。

davfs2 程序通过 FUSE 内核模块工作，使你能够像本地文件系统一样查看 WebDAV 共享。在基于 Debian 的发行版上安装该包只是一个简单的操作：

```
$ sudo apt-get install davfs2
```

并且该包肯定存在于其他发行版的仓库中。你可以可选地在可执行文件上设置 SUID 位，以便非 root 用户可以挂载 WebDAV 共享。Debian 和 Ubuntu 可以通过以下方式为你完成此操作：

```
$ sudo dpkg-reconfigure davfs2
```

如果你接受警告（实际上相当安全，因为程序会放弃其 root 权限），那么 webdav 组中的任何人都可以挂载 WebDAV 共享，因此像这样将你的用户添加到该组：

```
$ sudo gpasswd -a username webdav
```

现在创建一个文件夹 ~/owncloud-dav 作为我们的挂载点。我们还需要指定 OwnCloud 登录凭据，它们存储在文件 ~/davfs2/secrets 中。此文件可能已在之前的重新配置期间为你创建，但如果没有，你也可以轻松手动创建。由于此文件将包含敏感数据，因此锁定权限非常重要：

```
$ chmod 600 ~/davfs2/secrets
```

向你的 secrets 文件添加如下一行

```
https://yourserver.com/owncloud/remote.php/webdav
username password
```

根据需要替换 URL、用户名和密码。你还需要在 /etc/fstab 中添加以下内容（这需要 root 权限，因此 sudo nano /etc/fstab）：

```
https://yourserver.com/owncloud/remote.php/webdav /home/username davfs user,rw,noauto 0 0
```

同样，你需要将用户名替换为你自己的。如果你想允许多个用户访问，则需要为每个用户添加一行。如果一切顺利，用户将能够通过简单的命令挂载他们的 OwnCloud 文件夹：

```
$ mount ~/owncloud-dav
```

如果你使用的是自签名证书，那么你会收到关于可能的中间人攻击的警告，但我们已经讨论过这个问题了。用户可能希望自动挂载他们的 OwnCloud 资源，这通常只需将上述挂载命令添加到 ~/.bashrc 中即可。然而，警告信息会变得烦人，因此你可以通过使用以下棘手的命令来静默它并管道传输同意：

```
echo 'y' | mount ~/owncloud-dav > /dev/null 2>&1
```

也可以在 Gnome 中使用 Nautilus 或 KDE 中使用 Dolphin 在无需任何额外软件的情况下挂载 WebDAV 共享。你需要在 Nautilus 中使用 davs:// URI 前缀，或在 Dolphin 中使用 webdav://。

在过去一年中，约有 300 名开发者为 OwnCloud 贡献了新代码，使其成为今天最活跃的开源项目之一，也是开源能够取得成就的光辉典范。

柏林年度 OwnCloud 大会的反馈表明它取得了巨大的成功，而最近在英国的黑客马拉松将结出丰硕成果并修复许多错误。在一个大玩家及其庞大数据孤岛渴望你的数据，并且非常乐意在隐私等琐碎问题上移动球门柱的世界里，也许现在是时候让数据属于你自己的了。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_80_0.png)

Pictures 应用会尽可能合理地平铺你的照片，但缺乏按日期排序的选项。

Quick tip 如果你的 OwnCloud 服务器更改了 IP 地址或域名，那么你需要在文件 /var/www/owncloud/config/config.php 中的 trusted_domains 数组进行更新。

