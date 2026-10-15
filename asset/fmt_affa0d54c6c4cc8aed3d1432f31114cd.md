
当安装 Oracle Cluster 时，会自动创建两个服务器池：`Generic`（通用）和 `Free`（空）。在新的安装中，所有服务器最初都被分配到 `Free` 服务器池。服务器会自动从 `Free` 移动到新定义的服务器池中。当您升级 Oracle Cluster 时，所有节点都被分配到 `Generic` 服务器池，以确保与 Oracle Database 11g Release 2 (11.2) 之前的数据库版本的兼容性。

## D.3.3 Free 服务器池

`Free` 服务器池包含未分配到任何其他服务器池的服务器。`Free` 服务器池的属性限制如下：

- `SERVER_NAMES`、`MIN_SIZE`、`MAX_SIZE` 不能由用户编辑
- `IMPORTANCE` 和 `ACL` 可以由用户编辑

**另参：** Oracle Clusterera Administration and Deployment Guide

## D.3.4 Generic 服务器池

`Generic` 服务器池存储 11g Release 2 (11.2) 之前的数据库以及具有固定配置的管理员管理的数据库。此外，`Generic` 服务器池包含符合以下任一条件的服务器：

- 您在应用程序资源类型所有资源的 `HOSTING_MEMBERS` 属性中指定的服务器
- 在列出 `Generic` 服务器池为服务器池的服务器池的 `SERVER_NAMES` 属性中指定的名称的服务器
- `Generic` 服务器池的属性限制如下：
- 任何人无法修改 `Generic` 服务器池的属性（所有属性均为只读）
- 当您在 `HOSTING_MEMBERS` 属性中指定服务器名称时，Oracle Clusterware 仅在服务器满足以下条件时允许：
    - 在线且存在于 `Generic` 服务器池中
    - 在线且存在于 `Free` 服务器池中，在这种情况下 Oracle Clusterware 将服务器移动到 `Generic` 服务器池
    - 在线且存在于任何其他服务器池中，且客户端是 `CRS` 管理员（控制服务器池资源管理的用户角色）或被允许使用该服务器池的服务器，在这种情况下服务器将被移动到 `Generic` 服务器池
    - 离线且客户端是 `CRS` 管理员
- 当您向 `Generic` 服务器池注册服务器池时，Oracle Clusterware 仅当服务器名称通过之前为资源指定的相同要求时才允许。

服务器在集群启动时或向集群添加服务器时最初被考虑分配到 `Generic` 服务器池，在此之后才分配到其他服务器池。

## D.4 理解离地升级

在离地升级中，安装程序在单独的 Oracle Cluster home 中安装新版本。Oracle Clusterware 的两个版本都位于每个集群成员节点上，但只有一个版本是激活的。

滚动升级在软件升级到新版本时避免了停机并确保连续可用性。

如果您在每个节点上都有 Oracle Cluster homes，则你可以在所有节点上执行离地升级，或者执行部分滚动升级，使得某些节点运行来自早期版本 Oracle Cluster home 的 Oracle Clusterware，而其他节点运行来自新 Oracle Cluster home 的 Oracle Clusterware。

不支持 Oracle Clusterware 11g release 2 的就地升级。

另参：附录 F，“如何升级到 Oracle Grid Infrastructure”，有关完成滚动升级的说明

## E 手动完成安装前提任务

本附录提供了手动完成集群验证工具 (`CVU`) 和安装程序 (`OUI`) 通常在安装期间完成的配置任务的说明。如果您无法使用修复脚本，请参考此附录。

本附录包含：

- 在节点上配置 SSH
- 配置内核
- 在节点上启用 SSH

### E.1 手动配置 SSH

强制要求无密码 SSH。在后续示例中，使用了 `grid` 用户。您必须为打算使用的每个 Oracle 软件所有者单独配置 SSH。

#### E.1.1 检查系统的现有 SSH 配置

要确定 `ssh` 是否正在运行，请输入命令：

```
$ pgrep
```

#### E.1.2 在节点上配置 SSH

要配置 SSH，首先需要在每个节点上创建 RSA 或 DSA 密钥，然后将所有节点生成的密钥复制到每个节点上都相同的文件中。SSH 文件必须允许 `root` 和软件用户读取。

##### E.1.2.1 在每个节点创建 SSH 目录并创建

在每个节点上完成以下步骤：

1. 以软件所有者身份登录（在本示例中为 `grid` 用户）。
2. 为了确保您是以 `grid` 用户身份登录，并验证用户 ID 与分配给 `grid` 用户的预期 ID 匹配，请输入 `id` 和 `grid` user。例如：

```
$ id
uid=502(grid) gid=501(install) groups=501(install), 502(grid, asmdmin, asmdba)
gid=grid
uid=502(grid) gid=501(install) groups=501(install), 502(grid, asmdmin, asmdba)
```

3. 如必要，在 `grid` 用户的目录下创建 `.ssh` 目录，并对其设置权限以确保只有 `oracle` 用户具有读写权限：

```
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
```

> 注意：如果权限未设置为 700，SSH 配置将失败。

4. 输入以下命令：

```
$ /usr/bin/ssh-keygen -t dsa
```

# 在所有集群节点上手动配置 SSH

在出现提示时，接受密钥文件的默认位置（按 **Enter**）。

> **注意：** Oracle Clusterware 11g release 2 及更高版本不支持带有密码短码的 SSH。

此命令将 DSA 公钥写入 `~/.ssh/id_dsa.pub` 文件，将私钥写入 `~/.ssh/id_dsa` 文件。

切勿将 DSA 密钥分发给任何未授权执行安装 Oracle 软件的人员。

- 5. 对您打算成为集群成员的每个节点，使用 DSA 密钥重复步骤 1 到 4。

## E.1.2.2 将所有密钥添加到公用的 authorized_keys 文件

完成以下步骤：

- 1. 在本地节点上，切换目录到 Oracle Infrastructure 所有者家目录下的 `.ssh` 目录（通常，是 `grid` 或 `oracle`）。

然后，使用以下命令将 DSA 密钥添加到 `authorized_keys` 文件：

```bash
$ id_dsa.pub >> authorized_keys
$ ls
```

在目录中，您应该看到您创建的 `id_dsa.pub` 文件和 `authorized_keys` 文件。

2. 在本地节点上，使用 `SCP`（安全复制）或 `SFTP`（FTP）将 `authorized_keys` 文件复制到远程节点上的 `oracle` 用户 `.ssh` 目录。以下示例使用 `SCP`，针对名为 `node2` 的节点，使用 Oracle Infrastructure 所有者 `grid`，其中 `grid` 用户路径为 `/home/grid`：

```bash
[grid@node2] $ scp authorized_keys /home/grid/.
```

系统会提示接受一个 DSA 密钥。输入 `Yes`，您将看到您正在复制到 `known_hosts` 文件的节点。

在出现提示时，提供 `grid` 用户的密码，该密码在集群的所有节点上应是相同的。`authorized_keys` 文件被复制到远程节点。

您的输出应该如下所示，其中 `xxx` 代表有效 IP 地址的部分：

```bash
[grid@.ssh] $ scp authorized_keys node2:/home/grid/.
The authenticity of host 'node2' (xxx.173.152) can't be established.
DSA key fingerprint is 7e:60:60:a4:40:d4:ae:f6:74:ae:78:fe:7e
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'node2,xxx.173.152' to the list of known hosts
grid@node2's password:
authorized_keys   100   828   7.5KB/s   00
```

3. 使用 `SSH` 登录到您复制 `authorized_keys` 文件的节点。然后切换到 `.ssh` 目录，并将第二个节点的 DSA 密钥添加到 `authorized_keys` 文件中，在提示输入密码时点击 **Enter**，以便设置免密 SSH：

如何完成安装先决任务 手册 E-3
