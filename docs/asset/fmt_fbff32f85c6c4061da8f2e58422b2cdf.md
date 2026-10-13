
虽然使用公共组件是件好事——即使是为了外观统一——但在实践中这样做可能会导致问题。想象一个想要从互联网安装给定包的管理员。可能为了安装此包，管理员必须先安装其他几个包。这将由著名的“Failed dependencies”（依赖失败）消息指示。

### 列表 4.1：在与 RPM 工作时，你会看到依赖消息

```
[root@Packages]# rpm -ivh createrepo-0.9.8.e16.noarch.rpm
warning: createrepo-0.9.8.e16.noarch.rpm: Header V3 RSA/SHA256
signature, key Id fd43d531: NOKEY
error: Failed dependencies:
  deltarpm is needed by createrepo-0.9.8.e16.noarch
  python-deltarpm is needed by createrepo-0.9.8.e16
[root@Packages]#
```

依赖地狱的解决方案是元处理器。元处理器在 Red Hat 中被称为 `yum`（Yellowdog Update Manager），它与仓库配合，仓库是用户想要安装软件包时咨询的安装源。在仓库中，你发行版的所有软件包通常都是可用的。

在使用 `yum install somepackage` 安装软件包时，`yum` 首先检查是否有依赖项。如果有，`yum` 将检查仓库以查看所需的软件是否在仓库可用，如果是，管理员将看到 `yum` 想要作为依赖安装的软件列表。因此，使用 `yum` 是依赖地狱的解决方案。在列表 4.2 中，你可以看到 `yum` 为它安装的所有内容检查依赖项。

![](img/17f0db741e978e043c6f38c58e661452_29_0.png)

### 列表 4.2：使用 yum 为依赖地狱提供了解决方案

```
[root@hn]# yum install nmap
Loaded plugins: product-id, refresh-packagekit, security, subscription-manager
Updating certificate-based repositories.
Setting up Install Process
Resolving Dependencies
--> Running transaction check
--> Package nmap.x86_64 2:5.21-4.el16 will be installed
--> Finished Dependency Resolution
```

依赖已解析

| 包名 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
|  |  |  |  |  |

安装中: nmap | x86_64 | 2:5.21-4.el16 | repo | 2.2 M |

#### 事务摘要

安装 1 个软件包

```
Total download size: 2.2 M
Installed size: 7.3 M
Is this ok [Y/n]
Exiting on user
[root@hn1]# yum install libvirt
Loaded plugins: product-id, refresh-packagekit, security, subscription-manager
Updating certificate-based repositories.
Setting up Install Process
Resolving Dependencies
--> Running transaction check
--> Package libvirt.x86_64 0:9.4-23.el16 will be installed
--> Processing Dependency: libvirt-client = 0.9.4-23.el16 for package:
libvirt-0.9.4-23.el16.x86_64
--> Processing Dependency: radvd for package: libvirt-0.9.4-23.el16.x86_64-0.9.4-23.el16.x86_64
--> Processing Dependency: lsort for package: libvirt-0.9.4-23.el16.x86_64
--> Processing Dependency: libvirt.so.0(LIBVIRT_PRIVATE_0.9.4)(64bit)
for package: libvirt-0.9.4-23.el16.x86_64
--> Processing Dependency: libvirt.so.0(LIBVIRT_0.9.4)(64bit) for package:
libvirt-0.9.4-23.el16.x86_64
```

# 理解元包处理程序

如果你使用有效的注册密钥安装了 Red Hat Enterprise Linux，安装过程将自动为你在 Red Hat Network (`RHN`) 服务器上设置存储库。通过这些存储库，你将始终确保自己正在使用可用的最新 `RPM` 版本。如果你安装了一个无法连接到 `RHN` 的测试系统，你将需要创建自己的存储库。在接下来的章节中，你将首先学习如何设置自己的存储库。然后你将学习如何将存储库包含在配置中。

# 创建你自己的存储库

如果你安装了无法访问官方 `RHN` 存储库的 Red Hat 服务器，你将需要设置自己的存储库。如果你想将所有的 `RPM` 复制到一个目录并使用该目录作为存储库，此过程也很有用。练习 4.1 描述了如何操作。

## 练习 4.1

### 设置你自己的存储库

在本次练习中，你将学习如何设置自己的存储库并将其标记为存储库。首先，你将从 Red Hat 安装 `DVD` 复制所有的 `RPM` 文件到你在磁盘上创建的目录中。接下来，你将安装并运行 `createrepo` 包，它用于创建 `yum` 在安装软件包包时使用的元数据。在安装 `createrepo` 包时，你会发现也必须处理依赖问题。

1. 使用 `mkdir /repo` 在服务器文件系统的根目录下创建一个可以作为存储库的目录。
2. 将 Red Hat 安装 `DVD` 插入服务器的光驱驱动器。假设你在图形模式下运行服务器，`DVD` 将自动挂载。
3. 使用 `cd /media/RHEL[Tab]` 命令进入挂载的 `DVD`。接下来使用 `cd Packages`，这是所有 `RPM` 默认所在的目录。现在使用 `cp * /repo` 将它们全部复制到你创建的 `/repo` 目录中。完成后，你就不再需要 `DVD` 了。
4. 现在使用 `cd /repo` 进入 `/repo` 目录。在此目录中，输入 `rpm -ivh createrepo[Tab]`。这不起作用，并给你出一个“Failed dependencies”（依赖失败）错误。要安装它，首先安装 `deltarp` 和 `python-deltarp` 包。使用 `rpm -ivh deltarp[Tab] python-deltarp[Tab]` 安装这两个包。接下来，再次使用 `rpm -ivh createrepo[Tab]` 安装 `createrepo` 包。
5. 一旦安装了 `createrepo` 包，使用 `createrepo /repo`，这将创建一个允许你将 `/repo` 目录作为存储库的元数据。这将需要几分钟。当此过程完成后，你的存储库就可以使用了。

### 管理存储库

在前面的章节中，你学习了如何将包含 `RPM` 的目录转换为存储库。然而，仅仅标记目录是不够的。要使用你新创建的存储库，你必须告诉服务器在哪里找到它。要做到这一点，你需要在 `/etc/yum.repos.d/` 目录下创建一个存储库文件。该目录下已经有一些存储库文件了。在列表 4.3 中，你可以看到默认创建的 `rhel-source.repo` 文件的内容。

#### 列表 4.3：示例存储库文件
