
`mirrorlist-http://fedora.redhat.com/download/mirrors/fedora-core-$releasever`
`mirrorlist-http://fedora.redhat.com/download/mirrors/updates-released-$releasever`

如果你在配置文件中看到以下指令，这些文件（以及`/etc/yum.repos.d`目录中的任何其他文件）就是激活状态：

`enabled=0`

对于`Fedora Core 3`和`Fedora Core 4`，这些命令都将你的计算机连接到两个不同服务器上的`os`和`updates`仓库：`download.fedora.redhat.com`以及在`fedora-core-3`和`updates-released-fc3`（以及`fedora-core-4`和`updates-released-fc4`文件）中指定的随机镜像，地址位于`http://fedora.redhat.com/download/up2date-mirrors/`。

最好将这些命令行指向不同的镜像。你可以从`http://fedora.redhat.com/download/mirrors.html`获取镜像列表。在对URL进行任何更改之前，请检查相关的目录。你可能也需要更改那里。

例如，在本书期间，如果你使用南加利州大学的镜像服务器，该服务器URL为`http://mirrors.usc.edu`。然而，由于`os`和`updates`仓库的子目录不同，生成的命令行将是：

`yum-core-3`
`http://mirrors.usc.edu/pub/linux/distributions/fedora/3/$ARCH/os/`
`yum updates-released-fc3`
`http://mirrors.usc.edu/pub/linux/distributions/fedora/updates/$3/$ARCH/`

在`Fedora Core 3`中，你会在`/etc/sysconfig/rhn/sources`中找到两组命令行。第二组命令行用于选择一个特定的仓库。默认情况下实际上是从可用列表中随机选择一个仓库。

`fedora-core-3`
`http://fedora.redhat.com/download/up2date/`
`updates-released-fc3`
`http://fedora.redhat.com/download/up2date/`

在`Fedora Core 3`中，你会在`/etc/sysconfig/rhn/sources`中找到两组命令行。第二组命令行用于选择一个特定的仓库。默认情况下实际上是从可用列表中随机选择一个仓库。

使用你选择的文本编辑器打开`/etc/yum.reposd`目录下的`fedora-devel.repo`文件。

将`mirrorlist`指令更改为指向最合适的地理位置镜像文件。例如，如果你位于美国东海岸，你可能将`mirrorlist`指令替换为以下：

`mirrorlist=http://fedora.redhat.com/download/mirrors/fedora-core-wrawide.us.east`

确保`enabled`指令处于激活状态，或设置为`1`。默认情况下，它是未激活的或设置为`0`：

`enabled=1`

确保`gpgcheck`指令处于激活状态，或设置为`1`。默认情况下，它是未激活的或设置为`0`：

`gpgcheck=1`

引用相应的GPG文件，在此例中使用以下指令：

`gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-rawhide`

保存文件。下次你运行`update`时，你应该能在通道列表中找到开发库。

## 注意

不要在生产计算机上启用开发库。此库包含了最新软件包的每日构建版本，专为测试设计。根据定义，它们可能仍然存在Bug。

## 注意

请小心。对于截至本文编写发布的所有`Fedora Linux`版本，源文件中有一个命令会尝试将你的`Fedora Linux`计算机连接到红帽网络（`Red Hat Network`）。如果你拥有红帽企业 Linux（`RHEL`）的订阅，启用以下命令会导致`Red Hat Update Agent`提示你在红帽网络上注册此计算机，这可能会消耗该服务的宝贵订阅。切勿启用此命令！

`#up2date default`

在运行`Red Hat Update Agent`之前，你应该确保关键组件本身是最新的。你可以通过以下两个简单的命令来实现这一点：

`up2date`
`u2date yum`

这两个软件包的更新并不频繁。然而，如果你配置了一个脚本来自动更新，你应该将这些命令作为该脚本的一部分。

当配置妥当后，你可以通过两种方式进行。如果你想从命令行界面更新内核包以外的所有包，请运行以下命令，它默认会下载并安装所有可用的更新。

`up2date -u`

天哪，这不简单吗？但请注意，当你第一次在`Fedora Linux`上运行此命令时，可能需要一些时间。在我的情况下，此命令下载了约 2000 个头文件到`/var/spool/up2date`；整个过程花费了近一小时。

但你可能不想更新所有软件包。例如，截至本文编写，`Firefox Web` 浏览器的更新可能会破坏你安装的任何插件。在这种情况下，你可能想将`Firefox`排除在更新列表之外。你可以通过以下命令找到可用更新列表：

`up2date -l`

如果列表很长，你可能想对输出进行管道处理。例如，如果你想查看更新列表中是否有`Firefox`的升级包，可以运行以下命令：

`up2date -l | grep firefox`

如果`Firefox`在列表中，你可以让`Update Agent`排除它。当然，如果你使用`up2date --configure`进行配置是可以可以的，但这只是一个临时措施。我假设你最终还是想要与`Firefox`浏览器新版本相关的安全更新。

在`Fedora Linux`中，`Update Agent`默认配置使用`yum`。这意味着你可以利用与`yum`命令相关的开关和选项。你可以使用`yum`开关，例如`--exclude`。在这种情况下，你可以通过以下命令将`Firefox`排除在更新列表中：

`## up2date -u --exclude=firefox`

你可以使用`--exclude`开关排除任何你想从更新列表中剔除的包。现在，这不简单吗？

即使是`Update Agent`的命令行版本，对于倾向于在`GUI`中运行`Update Agent`时使用交互式模式的管理员，如果你想这样做，请按照以下步骤操作：

1. 从命令行界面运行`up2date`命令。
2. 除非你已以`root`用户登录，否则会提示输入`root`密码。
3. 当看到“Welcome to Red Hat Update Agent”窗口时，点击`Forward`。
4. 按照屏幕提示配置你的存储库。
5. 配置完成后，`Update Agent`将列出可用的更新。
6. 检查列表并选择你要安装的项。
7. 点击`Install`开始下载和安装过程。
8. 过程完成后，`Update Agent`将提供更改的摘要。
9. 点击`Finish`退出。

## 注意事项

在查找第三方之前，请检查所有可用的`RHEL`频道。红帽为其企业级Linux发行版在其他通道中提供了许多额外的软件包。这些包括`Java`、`Macromedia Flash`和`Real Player`等软件包。运行搜索。你可能会大吃一惊。根据我的经验推测，红帽将在未来某个时候将`yum`添加到这些通道之一。

你可以从`Fedora`或`Red Hat`镜像站点，或者从一个使用`yum`仓库的`RHEL`重编译版本中获取`yum`。如果你正在运行`RHEL 3`，可以从`RHEL 3`重编译版本或`Red Hat Linux 9`获取兼容版本的`yum`。如果你正在运行`RHEL 4`，可以从`RHEL 4`重编译版本或`Fedora Core 3`获取兼容的`yum`。如前所述，`Fedora`镜像站点列在`fed.redhat.com/download/mirrors.html`。`Red Hat Linux 9`通常也可以从相同的镜像站点获取；你可能需要向上搜索或查看目录树来找到这些文件。在写本文时，实用的`RHEL`仓库可以从以下来源获取：
