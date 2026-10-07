
- 在集群中的单台机器（NFS 服务器）上，创建一个作为实例家目录的文件系统（如果尚未创建）。
- 在本地挂载该文件系统。
- 设置该文件系统在系统重启动时自动挂载。
- 使用 NFS 导出 DB2 家目录系统。
- 在集群中剩余的每台机器上挂载导出的文件系统。

### 启动 NFS 服务

要验证参与分区数据库系统的每台计算机是否都在运行 NFS，请输入以下命令：

```
showmount -e
```

如果你输入 `showmount` 而不指定主机名，它将检查本地系统。如果 NFS 未运行，你会收到类似下面的消息：

```
mount: RPC Program not registered
```

### 启动 NFS

- 确保每台机器上都安装了 `nfs-utils` 和 `nfs-server` 软件包。
- NFS 操作（启动、停止和检查状态）在不同的 Linux 发行版中不同：

#### SUSE

SLES 10 使用基于内核的 NFS 服务器。配置 NFS 服务器的命令是 `serviceconfig`：

- 启动 NFS：`serviceconfig start`
- 停止 NFS：`serviceconfig stop`
- 检查 NFS 状态：`serviceconfig status`

确保 NFS 在启动时已。。可以使用命令 `chkconfig nfs` 进行检查。如果 NFS 未开启，请通过以下命令启用它：

```bash
chkconfig nfs on
```

#### Red Hat

- 启动 NFS：`/sbin/service nfs start`
- 停止 NFS：`/sbin/service nfs stop`

有关在 Red Hat 上配置配置 NFS 的更多详细信息，请参阅：

http://www.redhat.com/docs/manuals/enterprise/RHEL-5/manual/Deployment_Guide-en/nfs.html

在你确认 NFS 在每个系统上运行后，使用命令 `ps -ef | grep rpc.statd` 检查 `rpc.statd` 进程。DB2 需要 `rpc.statd`。请注意，在使用基于内核 NFS 的 SLES 中不需要 `rpc.statd`。

### 创建并配置用于 NFS 的 DB2 家目录文件系统

你需要创建一个跨越分区数据库系统中所有机器共享的 DB2 实例家目录。在我们的示例中，我们在 `mensa` 上分配了一个文件系统 `/export/db2home`。使用 NFS 共享此文件系统。要为 NFS 创建并配置 DB2 家目录文件系统：

1. 如果你尚未执行，请在 NFS 服务器上使用 `fdisk`（创建磁盘分区）和 `mkfs`（在磁盘分区上创建文件系统）等工具，或通过 SUSE YaST 工具创建 DB2 家文件系统（例如 `/export/db2home`）。
2. 使用以下命令本地挂载 DB2 家文件系统：

```bash
mount /export/db2home
```

3. 确保你的新文件系统已添加到 `/etc/fstab` 文件中，这将在每次系统重启时挂载该文件系统。Linux 文件系统创建工具（例如 Disk Raid 或 YaST）在你创建新文件系统时会自动向 `/etc/fstab` 文件添加条目。如果在 `/etc/fstab` 文件未找到你的 DB2 家文件系统，可以手动添加。在 `/etc/fstab` 中，你会看到 `/export/db2home` 的条目。在我们的设置中，该条目为：

```
/dev/sdb5 /export/db2home ext3 data=journal,user_xattr
```

4. 接下来，向 `/etc/exports` 文件添加条目，以便在启动时自动导出 NFS 文件系统。你只需要设置此项。在 `/etc/exports` 中，你会看到如下条目：

`/export/db2home *(rw,sync,no_root_squash)`

在我们的设置中，条目是：

```
/export/db2home *(rw,sync,no_root_squash)
```

5. 运行 `exportfs -a` 导出所有目录。
6. 在集群中的每台机器（包括 NFS 服务器）上，首先使用 `mkdir` 创建 `/db2home` 目录，然后向 `/etc/fstab` 添加条目以自动挂载。我们建议将文件系统配置为启动时挂载、为读写、并包含 `bg` 选项，这样 `setuid` 程序可以正常运行。参考以下示例：

```
mensa:/export/db2home *(rw,sync,no_root_squash)
```

7. 在集群的每台机器上向 `/etc/fstab` 添加条目后，通过以下命令在集群中剩余的每台机器上挂载导出的文件系统：

```bash
mount /db2home
```

如果挂载命令失败，请确保 NFS 服务器已启动。要重启 NFS 服务器，在 NFS 工作站上以 root 身份运行以下命令：

你也可以使用 `showmount` 命令检查 NFS 服务器的状态。例如：

```
showmount -e mensa
```

**提示：**

- 一种良好的习惯是将所有想要导出的目录都放在 `/export` 层次结构中。如果你在目录树的其他地方需要该目录，请使用符号链接或作为 NFS 客户端挂载。例如，如果你的服务器导入其 `/db2home` 层次，请将其放在 `/export`，从而创建 `/export/db2home`。挂载到 `/db2home`。
- 如果 `/etc/exports` 文件中有错误，NFS 在启动时会在 `syslog` 中报告错误。你可能会发现这个调试工具有用。

## 2.2.6 用户和组设置

在本节中，我们将讨论 DB2 需要的用户 ID 和组以及创建它们的过程。

DB2 需要三个用户和组：实例所有者、DB2 隔离用户（fenced user）和数据库管理服务器（DAS）用户。你可以使用 DB2 Setup 提供的默认名称或指定自己的所有者和组名称。在我们的设置中，我们使用了 DB2 Setup 向导提供的默认用户 ID 和组名称，如第 51 页表 2-10 所示。

| 表 2-10 DB2 所需用户示例 |
| --- |
| 所需用户 | 用户名 | 组名 | 描述 |
| 实例所有者 | db2inst1 | db2iadm1 | 管理实例 |
| 围栏用户 (Fenced user) | db2fenc1 | db2fadm1 | 执行围栏用户定义函数，如 UDF 和存储过程 |
| DAS 用户 | dasusr1 | dasadm1 | 管理 DB2 管理服务器 |

### 创建用户

创建用户和组需要 root 权限。

对于 root 安装，有三种方法可以创建 DB2 用户和组：

- 使用 DB2 安装向导
- 使用响应文件（response file）进行安装
- 在操作系统命令行或在操作系统管理工具中创建用户和组

对于非 root 安装，用户和组必须在安装之前已经存在。

#### DB2 安装向导

DB2 Setup 会在安装期间为您创建所有必需的用户和组。创建的默认用户和组列在表 2-10 所示。DB2 Setup 允许您指定自己的用户和组名称。

#### 响应文件

如果在响应文件中指定了用户和组信息，也可以在响应文件安装期间创建用户。示例 2-5 显示了我们响应文件中用于创建 DB2 三个必需用户和组的条目。

示例 2-5 使用响应文件创建用户和组

```
** 实例创建设置
db2inst1.NAME = db2inst1
db2inst1.UID = 1001
db2inst1.GROUP_NAME = db2iadm1
db2inst1.GID = 999
db2inst1.HOME_DIRECTORY = /home/db2inst1
db2inst1.PASSWORD = xxxxxxxxxx
......
```

** 围栏用户创建设置

```
db2inst1.FENCED_USERNAME = db2fenc1
dbinst1.FENCED_UID = 1002
db2inst1.FENCED_GROUP_NAME = db2fadml
db2inst1.FENCED_HOME_DIRECTORY = /dbhome/db2fenc1
db2inst1.FENCED_PASSWORD = xxxxxxxxxx
```

```
** 管理服务器创建设置
DAS_USERNAME = dasusur1
DAS_UID = 1003
DAS_GROUP_NAME = dasadml1
DAS_GID = 997
DAS_HOME_DIRECTORY = /home/dasur1
DAS_PASSWORD = xxxxxxxxxx
```

#### 在操作系统命令行中创建用户和组

要使用此方法，请遵循以下步骤：

1. 以 root 身份登录。
2. 使用以下命令为实例所有者、围栏用户和 DAS 用户创建组：

```
groupadd -g 999 db2iadml
groupadd -g 998 db2fadml
groupadd -g 997 dasadml
```

在我们的设置中，我们使用了数字 997、998 和 999。请通过检查 `/etc/group` 文件，确保您选择的数字在机器上已不存在。
3. 创建属于每个组的用户并指定主目录：

```
useradd -u 1001 -g db2iadml -m -d /dbhome/db2inst1 -s /bin/ksh db2inst1
useradd -u 1002 -g db2fadml -m -d /dbhome/db2fenc1 -s /bin/ksh db2fenc1
useradd -u 1003 -g dasadml -m -d /home/dasusur1 -s /bin/ksh dasusur1
```

在我们的设置中，我们选择了数字 1001、1002 和 1003。请通过检查 `/etc/passwd` 文件，确保您选择的数字在机器上已不存在。
4. 以 root 身份，通过输入以下命令为创建的每个用户设置密码：

```
passwd db2inst1
passwd db2fenc1
passwd dasusur1
```

### 创建用户：多分区的考虑因素

在分区数据库环境中，您只需要为实例所有者和围栏用户创建一个共享目录（但请记住在每台机器上创建用户）。在分区环境中创建用户时，请确保每台机器上的用户 ID 和组 ID 是相同的。在我们的设置中，我们使用了：

- 拥有实例所有权的机器上的一个共享主目录 `/db2home`，该目录在其余机器上通过 NFS 挂载。在此目录中，我们拥有实例所有者和围栏用户的主目录：`db2inst1` 和 `db2fenc1`。
- 每台机器上 DAS 的本地主目录 `dasur1`，存储在 `/home` 目录下。

### 分区数据库的 DAS 考虑因素

我们无法将 DAS 主目录放在共享文件夹中，因为每台机器上具有相同的 DAS 用户 ID。您需要注意 DAS 的考虑因素：

- 分区数据库中的每台物理机器上必须运行 DAS，图形化工具（例如 Control Center）才能工作。
- 每台机器只能有一个 DAS。如果您有旧版 DB2 现有的 DAS，我们建议将其删除并创建一个新的 DAS。
- 与实例一样，每个 DAS 必须在用户 ID 下创建。在环境中为 DAS 使用不同的用户 ID，或者使用相同用户 ID 且不共享用户主目录，都没有区别。
- 如果使用现有用户，请确保该用户在安装前已存在。
- 对于响应文件安装：如果响应文件中指定了用户，请确保该用户在安装前已存在。

### 分区数据库的启用 ssh

在分区数据库环境中，为了让图形化工具（例如 Control Center）工作，分区数据库中的每台物理机器上必须运行 DAS。

- 每台机器只能有一个 DAS。如果您有旧版 DB2 现有的 DAS，我们建议将其删除并创建一个新的 DAS。
- 与实例一样，每个 DAS 必须在用户 ID 下创建。在环境中为 DAS 使用不同的用户 ID，或者使用相同用户 ID 且不共享用户主目录，都没有区别。
- 如果使用现有用户，请确保该用户在安装前已存在。
- 对于响应文件安装：如果响应文件中指定了用户，请确保该用户在安装前已存在。

## 2.2 分区数据库的启用 ssh

在分区数据库环境中，为了让图形化工具（例如 Control Center）工作，分区数据库中的每台物理机器上必须运行 DAS。

- 每台机器只能有一个 DAS。如果您有旧版 DB2 现有的 DAS，我们建议将其删除并创建一个新的 DAS。
- 与实例一样，每个 DAS 必须在用户 ID 下创建。在环境中为 DAS 使用不同的用户 ID，或者使用相同用户 ID 且不共享用户主目录，都没有区别。
- 如果使用现有用户，请确保该用户在安装前已存在。
- 对于响应文件安装：如果响应文件中指定了用户，请确保该用户在安装前已存在。

### 设置基于主机的身份验证

基于主机的身份验证允许机器 A 使用机器 B 上的 ssh。对于基于主机的身份验证，信任机制在 `ssh_known_hosts` 文件中查找公密钥。

将客户端机器的未限定主机名、完全限定的主机名和 IP 地址添加到 `ssh_known_hosts` 文件中，如示例 2-10 和示例 2-11 所示。你可以使用 `ssh-keyscan` 工具来填充此文件。

示例 2-10 更新 ssh_known_hosts 文件以 RSA 加密

```
$ cd /etc/ssh
$ ssh-keyscan -t rsa mensa,mensa.itsosj.sanjose.ibm.com,9.43.86.90
>>ssh_known_hosts
$ ssh-keyscan -t rsa gemini,gemini.itsosj.sanjose.ibm.com,9.43.86.90
>>ssh_known_hosts
```

示例 2-11 为 DSA 加密更新 ssh_known_hosts 文件

```
$ cd /etc/ssh
$ ssh-keyscan -t dsa mensa,mensa.itsosj.sanjose.ibm.com,9.43.86.90
>>ssh_known_hosts
$ ssh-keyscan -t dsa gemini,gemini.itsosj.ibm.com,9.43.86.94
>>ssh_known_hosts
```

5. 重启 ssh 守护进程：

```
/etc/init.d/sshd restart
```

### SSH 客户端配置

按照以下步骤配置 SSH 客户端：

- 1. 编辑 `/etc/ssh/ssh_config` 文件。

如示例 2-12 所示，将 `HostBasedAuthentication` 行从 `no` 更改为 `yes`。

> 示例 2-12 编辑 ssh_config 文件

```
HostBasedAuthentication no
HostBasedAuthentication yes
```

注意，ssh 服务器配置文件为 `sshd_config`。

在 `ssh_config` 文件中添加一行，告诉 ssh 客户端使用 `ssh-keyscan` 读取主机的私钥，如示例 2-13 所示。

> 示例 2-13 在 ssh_config 文件中添加一行

```
EnableSSHKeys yes
```

- 2. 确保 `ssh-keyscan` 是一个 suid-root 可执行文件。

检查 `ssh-keyscan` 设置：

在 SUSE 上：

在 Red Hat 上：

```
ls -l /usr/lib64/ssh/ssh-keyscan
-rwr-xr-x 1 root 173952 2007-05-18 03:55 /usr/lib64/ssh/ssh-keyscan
ls -l /usr/libexec/openssl/ssh-keyscan
-rwr-xr-x 1 root 175424 Jul 13 2007 /usr/libexec/openssl/ssh-keyscan
```

如果权限和所有者与此示例输出不符，请按照第 57 页的示例 2-14 和第 57 页的示例 2-15 修复权限。

示例 2-14 在 SUSE 上修复 ssh-keyscan 的权限

```
$ cd /usr/lib64/ssh/
$ chown root:root ssh-keyscan
$ chmod 4755 /usr/lib64/openssl/ssh-keyscan
```
