
您刚刚在集群中的一个服务器上创建了 EVMS 卷。正如您预期的，这将导致 EVMS 卷在该服务器每次启动时都处于激活状态。然而，另一台服务器仍然不知道这个 EVMS 卷。为了让它知道共享磁盘设备上有类似于 EVMS 卷的东西，您需要使用 `boot.evms` 命令启动 `boot.evms` 脚本。确保在每次服务器重启时都激活它，使用 `inserv boot.evms` 命令。（或使用 YaST 运行编辑器执行这些操作）。在继续之前，请确保 `smb.conf` 在所有节点中都存在。

# 在所有服务器上挂载共享文件系统的挂载点

除了加载脚本外，您还需要为此集群资源准备一个卸载脚本，以确保服务被正确卸载。以下卸载脚本可以正常工作：

1. 将 `/etc/samba/smb.conf` 文件复制到共享设备上的 `etc` 目录。将其重命名以反映集群资源的名称。例如，使用 `mv smb.conf cluster_smb.conf` 将其重命名。在接后的步骤中，我们将集群资源的 `smb.conf` 文件称为 `cluster_smb.conf`。
2. 使用编辑器打开 `cluster_smb.conf` 文件，并在 `[global]` 部分添加以下行内容：

```
bind interfaces only = yes
interfaces = cluster resource ip address
pid directory = $SAMBA_ROOT/share/locks
```

在这些行中，第一行将确保 Samba 只连接到使用 `interfaces` 参数指定的接口，该参数设置为分配给 Samba 集群资源的唯一 IP 地址。最后，`pid directory` 设置将确保 Samba 服务器创建的 PID 文件写入共享磁盘上的目录。在此参数中使用了 `$SAMBA_ROOT` 变量；您将在稍后配置 Samba 集群资源时设置它。

# 创建 Samba 集群资源

现在已经对 `smb.conf` 文件进行了所有必要的修改，您仍然需要创建 Samba 集群资源。Novell 集群服务 1.8 自带了一个模板对象来

## 在 OES Linux 上对 Samba 服务器进行集群化

使此资源的创建变得更加简单。以下步骤描述了如何创建 Samba 集群资源：

1. 确保你为 Samba 服务器创建的共享磁盘已卸载。
2. 在 `https://yourserver/nps` 上启动 iManager 并以 admin 身份登录。
3. 在 iManager 中，激活“集群”（Clusters）、“集群选项”（Cluster Options）。
4. 指定你想要创建 Samba 资源的所在的集群名称，然后点击“新建”（New）创建一个新资源。
5. 从“新建资源”（New Resource）窗口中，选择资源类型并点击“下一步”（Next）继续。
6. 使用 Samba 作为集群资源名称，并在“从模板继承”（Inherit from Template）字段中，浏览到 `Samba_Template` 对象。确保“定义附加属性”（Define Additional Properties）框已勾选，然后点击“下一步”继续。

> 提示
>
> 如果你没有看到 Samba 资源模板，请确保你正在使用 OES SP1 或更高版本。Samba 资源模板仅从此 OES 版本开始。

7. 现在你将看到 Samba 资源的加载脚本，该脚本是根据 Samba 资源模板上的加载脚本自动生成的。确保你调整了加载脚本以反映你的环境。通常必须修改以下参数：
   * `RESOURCE_IP`: 你想要分配给 Samba 资源的 IP 地址。
   * `MOUNT_FS`: 你在共享磁盘上使用的文件系统类型。
   * `MOUNT_DEV`: EVMS 卷的名称。如果你使用 YaST 创建了 EVMS 卷，名称将类似于 `/dev/evms/lm/system/samba`。
   * `MOUNT_POINT`: 你将挂载共享磁盘设备的目录名称。在本例中，我们使用 `/mnt/samba` 作为该目录名称。
   * `CONFIG_FILE`: 你在共享磁盘上创建的 `cluster_samba.conf` 配置文件的名称。确保你也包含了该文件的完整路径。
8. 点击“下一步”后，你将进入可以配置卸载脚本（unload script）的屏幕。按照本过程第 7 步提到的进行相同的修改，完成后点击“下一步”。

## 第 8 章：支持集群的应用程序

9. 设置你想要为此资源使用的资源策略。有关这些策略的更多信息，请参阅第 6 章，并设置适当的值。然后点击“下一步”继续。
10. 确保分配了正确的节点。如果是这样，点击“完成”（Finish）结束 Samba 集群资源的配置。

你现在已经配置了集群资源。根据你的服务器上当前加载的内容，它可能尚无法加载。如果共享卷已挂载在任何地方，或者 Samba 服务器已加载到集群中的任何节点上，则 Samba 集群资源将无法成功加载。首先，确保通过 `ps -ef | grep smb` 命令没有服务器上没有活跃的 Samba 服务器。如果此命令显示任何活跃的 Samba 服务器，请使用 `rcsm` 停止服务器。然后使用 `inserv -r smb` 防止服务器自动启动。接下来，确保供 Samba 服务器使用的共享设备未被挂载。如果是，请使用 `umount /media/samba` 将其卸载（这仅在设备挂载在 `/media/samba` 时有效）。如果你收到“设备忙” 消息，请使用 `fuser` 显示当前在共享设备上打开所有文件的进程列表。接下来，尝试正常终止这些进程。如果你在执行此操作时遇到问题，可以使用 `fuser -k /media/samba`，这将强制卸载设备。然而，后一种方法应仅作为最后手段。

## 从 Samba 集群资源提供共享

你现在已为 Samba 服务器创建了集群资源。然而，到目前为止 Samba 服务器尚未尚未共享任何内容。在这里我们将讨论如何通过 Samba 服务器在共享资源上共享目录：

1. 在共享磁盘设备上，使用 `mkdir` 创建目录。例如，使用 `mkdir /media/samba/share` 创建名为该名称的目录。在发布此命令之前，使用 `mount` 确保共享磁盘设备当前已挂载。
2. 要访问共享，需要两点：Linux 文件系统层级对共享目录的权限，以及 Samba 服务器授予的访问共享的权限。要在 Linux 文件系统层级访问共享，你需要创建一个 eDirectory，该目录也可以被用作 Linux 文件系统层级的受托人（trustee）。这被称为启用 LUM（Linux 用户管理）的组。你可以从 iManager、Linux 用户管理将 eDirectory 组启用为自己的组。当 eDirectory 组被授予组权限后，在 Linux 文件系统中，你可以从命令行使用 `chmod` 为该组授予权限。例如，在某些场景下，如果某些 Linux 用户需要在 Linux 文件系统层级写入共享目录，你需要一个 LUM 组，将这些用户添加为该组成员，然后使用 `chmod +rw yourgroup` 提供必要的权限。

作为下一步，你必须在共享磁盘设备上的 `/etc/cluster_smb.conf` 上将共享目录配置为共享。创建此共享的条目如下所示：

```
[share]
comment = shared directory
path = /mnt/samba/share
read only = no
inherit acls = yes
```

当然，你应该意识到这是一个关于如何配置共享的非常基础的示例。有关配置 Samba 时可以使用的选项的细节，请参阅 `smb.conf` 的主页。

磁盘设备上的 Samba 共享已准备就绪。你可以启动 Samba 服务器并从任何位置访问。

# 第 9 章：高级集群、维护与故障排除

对于集群，有一些文档是您应该收集并添加到系统文档中的。关于集群节点的布局、资源、资源优先级以及所使用的 IP 地址，不能仅通过检查 iManager 获取。

## 更改主节点 IP 地址

集群主资源是集群中主节点上始终可用的资源。它可以作为您管理集群的主要访问方式，因为无论哪些节点故障，只要集群至少有一个节点处于存状态，该资源及其 IP 地址就始终可用。

如果您必须更改集群的 IP 地址方案，则也必须更改此地址。您无法在主资源本身中更改它。您必须在集群常规属性中更改地址。请注意，更改此地址需要关闭整个集群。

要更改地址，请执行以下步骤：
1. 在 iManager 中选择“集群选项 (Cluster Options)”任务，并选择您想要更改地址的集群。
2. 点击集群选择文本框下的“属性 (Properties)”按钮。
3. 在“常规 (General)”选项卡中输入新的主节点 IP 地址。
