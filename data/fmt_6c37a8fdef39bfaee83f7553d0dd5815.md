
```
[root@hn1]# cat /etc/yum.repos.d/rhel-source.repo
[rhel-source]
name=Hat Enterprise Linux $releasever
baseurl= Source
baseurl==http://ftp.redhat.com/pub/redhat/linux/$releasever/en/os/
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-release
[rhel-source-beta]
name=Hat Enterprise Linux $releasever
basearch= Source
baseurl==http://ftp.redhat.com/pub/redhat/linux/beta/$releasever/en/os/
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-beta
root@hn1]#
```

在列表 4.3 的示例文件中，你将找到存储库文件应该包含的所有元素。在这里使用什么并不重要：标识符（如 `[rhel-source]`）允许你尽早识别存储库，并被用在你的计算机上。`name` 参数也是如此；它为存储库命名。

非常重要的参数是 `baseurl`。它告诉如何以 URL 格式找到存储库。如在本例所示，Red Hat 服务器上的存储库。或者，你可以使用 URL 指向服务器上的目录。在后一种情况下，存储库格式看起来像 `file:///yourrepository`。有些人对双斜杠 `//` 感到困惑，但它必须在那里。`//` 部分是路径，告诉你要查看的文件或目录，在本例中是 `/repository`。接下来 `enabled` 参数指定该存储库是否启用。0 表示禁用，如果你想使用此存储库，该参数的值应该是 1。

# 理解元包处理程序

如果你使用有效的注册密钥安装了 Red Hat Enterprise Linux，安装过程将自动为你在 Red Hat Network (RHN) 服务器上设置存储库。通过这些存储库，你将始终确保自己正在使用可用的最新 RPM 版本。如果你安装了一个无法连接到 RHN 的测试系统，你将需要创建自己的存储库。在接下来的章节中，你将首先学习如何设置自己的存储库。然后你将学习如何将存储库包含在配置中。

# 创建你自己的存储库

如果你安装了无法访问官方 RHN 存储库的 Red Hat 服务器，你将需要设置自己的存储库。如果你想将所有的 RPM 复制到一个目录并使用该目录作为存储库，此过程也很有用。练习 4.1 描述了如何操作。

### 练习 4.1

# 设置你自己的存储库

在本次练习中，你将学习如何设置自己的存储库并将其标记为存储库。首先，你将从 Red Hat 安装 DVD 复制所有的 RPM 文件到你在磁盘上创建的目录中。接下来，你将安装并运行 `createrepo` 包，它用于创建 yum 在安装软件包包时使用的元数据。在安装 `createrepo` 包时，你会发现也必须处理依赖问题。

1. 使用 `mkdir /repo` 在服务器文件系统的根目录下创建一个可以作为存储库的目录。
2. 将 Red Hat 安装 DVD 插入服务器的光驱驱动器。假设你在图形模式下运行服务器，DVD 将自动挂载。
3. 使用 `cd /media/RHEL[Tab]` 命令进入挂载的 DVD。接下来使用 `cd Packages`，这是所有 RPM 默认所在的目录。现在使用 `cp * /repo` 将它们全部复制到你创建的 `/repo` 目录中。完成后，你就不再需要 DVD 了。
4. 现在使用 `cd /repo` 进入 `/repo` 目录。在此目录中，输入 `rpm -ivh createrepo[Tab]`。这不起作用，并给你出一个“Failed dependencies”错误。要安装它，首先安装 `deltarp` 和 `python-deltarp` 包。使用 `rpm -ivh deltarp[Tab] python-deltarp[Tab]` 安装这两个包。接下来，再次使用 `rpm -ivh createrepo[Tab]` 安装 `createrepo` 包。
5. 一旦安装了 `createrepo` 包，使用 `createrepo /repo`，这将创建一个允许你将 `/repo` 目录作为存储库的元数据。这将需要几分钟。当此过程完成后，你的存储库就可以使用了。

### 管理存储库

在前面的章节中，你学习了如何将包含 RPM 的目录转换为存储库。然而，仅仅标记目录是不够的。要使用你新创建的存储库，你必须告诉服务器在哪里找到它。要做到这一点，你需要在 `/etc/yum.repos.d/` 目录下创建一个存储库文件。该目录下已经有一些存储库文件了。在列表 4.3 中，你可以看到默认创建的 `rhel-source.repo` 文件的内容。

列表 4.3：示例存储库文件

```
[root@hn1]# cat /etc/yum.repos.d/rhel-source.repo
[rhel-source]
name=Hat Enterprise Linux $releasever
baseurl= Source
baseurl==http://ftp.redhat.com/pub/redhat/linux/$releasever/en/os/
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-release
[rhel-source-beta]
name=Hat Enterprise Linux $releasever
basearch= Source
baseurl==http://ftp.redhat.com/pub/redhat/linux/beta/$releasever/en/os/
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-beta
root@hn1]#
```

在列表 4.3 的示例文件中，你将找到存储库文件应该包含的所有元素。在这里使用什么并不重要：标识符（如 `[rhel-source]`）允许你尽早识别存储库，并被用在你的计算机上。`name` 参数也是如此；它为存储库命名。

非常重要的参数是 `baseurl`。它告诉如何以 URL 格式找到存储库。如在本例所示，Red Hat 服务器上的存储库。或者，你可以使用 URL 指向服务器上的目录。在后一种情况下，存储库格式看起来像 `file:///yourrepository`。有些人对双斜杠 `//` 感到困惑，但它必须在那里。`//` 部分是路径，告诉你要查看的文件或目录，在本例中是 `/repository`。接下来 `enabled` 参数指定该存储库是否启用。0 表示禁用，如果你想使用此存储库，该参数的值应该是 1。

# 理解元包处理程序

如果你使用有效的注册密钥安装了 Red Hat Enterprise Linux，安装过程将自动为你在 Red Hat Network (RHN) 服务器上设置存储库。通过这些存储库，你将始终确保自己正在使用可用的最新 RPM 版本。如果你安装了一个无法连接到 RHN 的测试系统，你将需要创建自己的存储库。在接下来的章节中，你将首先学习如何设置自己的存储库。然后你将学习如何将存储库包含在配置中。

# 创建你自己的存储库

如果你安装了无法访问官方 RHN 存储库的 Red Hat 服务器，你将需要设置自己的存储库。如果你想将所有的 RPM 复制到一个目录并使用该目录作为存储库，此过程也很有用。练习 4.1 描述了如何操作。

### 练习 4.1

# 设置你自己的存储库

在本次练习中，你将学习如何设置自己的存储库并将其标记为存储库。首先，你将从 Red Hat 安装 DVD 复制所有的 RPM 文件到你在磁盘上创建的目录中。接下来，你将安装并运行 `createrepo` 包，它用于创建 yum 在安装软件包包时使用的元数据。在安装 `createrepo` 包时，你会发现也必须处理依赖问题。

1. 使用 `mkdir /repo` 在服务器文件系统的根目录下创建一个可以作为存储库的目录。
2. 将 Red Hat 安装 DVD 插入服务器的光驱驱动器。假设你在图形模式下运行服务器，DVD 将自动挂载。
3. 使用 `cd /media/RHEL[Tab]` 命令进入挂载的 DVD。接下来使用 `cd Packages`，这是所有 RPM 默认所在的目录。现在使用 `cp * /repo` 将它们全部复制到你创建的 `/repo` 目录中。完成后，你就不再需要 DVD 了。
