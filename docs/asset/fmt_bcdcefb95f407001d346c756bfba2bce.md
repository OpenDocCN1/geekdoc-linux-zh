
## 4. 现在使用 `cd /repo` 进入该目录。从该目录，使用 `rpm -ivh createrepo`。这不起作用，并会返回“Failed dependencies”（依赖失败）错误。要安装 `createrepo`，你首先需要安装 `deltarpm` 和 `python-deltarpm` 包。使用 `rpm -ivh deltarpm python-deltarpm` 安装这两个包。接着，再次使用 `rpm -ivh createrepo` 安装 `createrepo` 包。

## 5. 一旦安装了 `createrepo` 包，使用 `createrepo /repo`，这将创建允许将 `/repo` 目录作为存储库使用的元数据。这需要几分钟。当此过程完成后，你的存储库就可以使用了。

# 管理存储库

在前面的小节中，你学习了如何将包含 RPM 包的目录转换为存储库。然而，仅仅将目录标记为存储库是不够的。要使用你新创建的存储库，你必须告诉服务器在何处可以找到它。

# 练习 4.2 (继续)

```
repolist: 3,596
[root@hn]# yum refresh-packagekit security nmap
Loaded plugins: product-id, security, subscription-manager
Updating certificate-based repositories.
========================== N/S Matched: nmap ==============
nmap.x86_64 : Network exploration tool and security scanner
Name and summary matches not only, use "search all" for everything.
[root@hn]# ~
```

此时，你的软件库已经启用，你可以使用 `yum` 来管理服务器上的软件包了。

# RHN 和 Satellite

在前面的章节中，你学习了如何创建和管理自己的软件库。在企业环境中，你的服务器将直接连接到 RHN，或者连接到 Red Hat Satellite 或 Red Hat Proxy 服务器，这两者都可以用于从自己的站点内部提供 RHN 软件包。

# 利用 RHN 的优势

在只有几台 Red Hat 服务器的小型环境中，你的服务器可能直接连接到 RHN 网络。这只需要两个条件：

- 你需要为要连接的服务器准备密钥。
- 你需要从服务器直接访问互联网。

通过 RHN，你可以看到通过你的 RHN 账户管理的所有服务器（见图 4.1）。要查看这些服务器，访问 `http://rhn.redhat.com`，使用你的 RHN 用户凭据登录，并进入 `systems`（系统）链接。

通过 RHN，你可以直接访问服务器的补丁并执行其他管理任务。

RHN 适用于小型环境。然而，如果你的环境中有数百台需要管理的 Red Hat 服务器，RHN 并不是最佳方案。在这种情况下，使用 Satellite 会更好。Red Hat Satellite 提供了 RHN 的代理，它还允许基本的部署和版本控制。你用你的 RHN 凭据配置 Satellite，由 Satellite 为你获取补丁和更新。在设置过程中，接下来你将把服务器注册到 Satellite。

# 理解元包处理器

图 4.1 如果你的服务器通过 RHN 注册，你可以在你的 RHN 账户中看到它。

![](img/3a7e027360b64bc83d5cf9a2db902251_136_0.png)

# 在 RHN 中注册服务器

要向 RHN 注册服务器，你可以使用 `rhn_register` 工具。该工具可以在图形界面或文本界面运行。启动 `rhn_register` 工具后，它会显示一个介绍界面，你只需点击 Forward（下一步）即可。接着，工具会显示一个让你选择操作的屏幕。你可以指示想要从 Red Hat Network 下载更新，或者如果你的网络中有 Satellite 服务器，你可以指示你有权访问 Red Hat Network Satellite（见图 4.2）。

要将服务器连接到 RHN，请在屏幕上输入你的登录凭据。

> 如果你无预算购买 Red Hat Enterprise Linux，可以在 `www.redhat.com` 获取免费的 30 天访问码。在 30 天结束后，你的服务器仍将继续工作；但你将无法再次安装更新了。

在成功注册 RHN 后，`rhn_register` 工具会询问你是想要有限的更新（limited updates）还是所有可用更新。这是一个重要的选择。默认情况下，你将获得所有可用更新，这将让你获得 Red Hat Enterprise Linux 所有软件的最新版本。然而，某些软件仅支持 Red Hat Enterprise Linux 的特定子版本。如果你的环境是如此情况，那么最好选择有限更新（见图 4.3）。

# 图 4.2 指定你想要连接到 RHN 还是 Satellite 服务器。

![](img/3a7e027360b64bc83d5cf9a2db902251_137_0.png)

# 图 4.3 如果你的软件仅在 RHEL 的特定子版本上，请选择有限更新。

![](img/3a7e027360b64bc83d5cf9a2db902251_137_1.png)

# 使用 Yum 安装软件

在下一步，程序会要求输入系统名称和个人配置数据（见图 4.4）。这些信息将发送到 RHN，并使你的系统能够注册到 RHN。通常，不需要更改此窗口中的任何选项。

图 4.4 指定要发送到 RHN 的信息

![](img/3a7e027360b64bc83d5cf9a2db902251_138_0.png)

点击 Forward 后，你的系统信息将发送到 RHN。这需要一些时间。注册成功后，你就可以从 RHN 安装更新和补丁了。要验证你确实连接了 RHN，你可以使用 `yum repolist` 命令，该命令提供了你系统当前配置使用的所有软件库的概览。

# 使用 Yum 安装软件

配置软件库后，你可以通过元包处理器 `yum` 安装、查询、更新和删除软件。该工具易于理解且直观。

# 使用 Yum 搜索软件包

要用 `yum` 管理软件，第一步通常是搜索你寻找的软件。`yum search` 命令可以实现此操作。

# 第 4 章 · 管理软件

安装：

```
You have new mail in /var/spool/mail/root
[root@hostname]#
```

在某些情况下，你可能需要安装一个不在你已下载的 RPM 存储库中的单个软件包。要安装此类包，你可以使用命令 `-ivh packagename.rpm`。然而，此命令不会更新你的 yum 数据库，因此使用 `rpm` 命令安装包并不是一个好主意。请使用 `yum install`。这将更新你的 yum 数据库并检查存储库以自动解决任何潜在的依赖问题，就像你习惯使用 `yum install` 一样。

如果某个包已经安装，可以使用 `yum update` 来更新它。使用此命令时指定要更新的特定包名，或者直接使用 `yum update` 检查所有存储库并查找正在更新的包是否有更高版本。

通常情况下，更新包会删除旧版本的包并将其完全替换为最新版本。当你想要更新内核时会发生例外情况。`yum update kernel` 将安装新版本的内核，同时在你的服务器上保留旧版本。这很有用，因为如果新内核出现问题，它允许你启动旧内核。

# 移除包

与安装包一样，使用 `yum` 移除包也很简单。只需使用 `yum remove` 后跟你想要卸载的包名即可。例如，要移除 `nmap` 包，请使用 `yum remove nmap`。`yum remove` 命令将提供其意图执行的操作概述。在概述中，它将显示打算移除的包名以及所有依赖于该包的包。

仔细阅读 `yum` 意图执行的操作是非常重要的。如果你想要移除的包有许多依赖项，`yum` 默认将移除这些依赖项。在某些情况下，按照默认设置继续并不是一个好主意。例如列表 4.7 所示，使用了 `yum remove bash` 的情况。幸运的是，该命令在 `yum` 尝试移除 `bash` 的刻失败了，因为有许多包依赖于它才能运行。移除 `bash` 真的是一个糟糕的主意！

# 列表 4.7：使用 yum remove 时要小心
