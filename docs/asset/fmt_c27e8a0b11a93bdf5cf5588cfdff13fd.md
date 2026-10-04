
在下一步中，我们将禁用 Stonith，它是 Pacemaker 的隔离（fencing）实现方案。在安装 Pacemaker 集群时，默认会配置 Stonith。隔离（Fencing）可以定义为将高可用集群带回已知状态的方法。当集群资源管理器无法确定节点状态或节点上资源的状态时，隔离将集群再次带回到已知状态。

然而，此时，红帽企业级 Linux（Red Hat Enterprise Linux）尚未为任何云环境（包括 Azure）提供隔离代理（fencing agents）。因此，将在练习中禁用它。

## 注意

在支持的环境或出于评估目的，您应该保持启用 Stonith。微软正在针对尚未支持的环境解决方案。

目前，我们可以通过运行以下命令来禁用 Stonith，其中 `property` 命令用于管理 Pacemaker 属性。以下命令将集群的 `stonith-enabled` 属性设置为 `false`：

```bash
sudo pcs property set stonith-enabled=false
```

## 注意

有关关于隔离（fencing）和 Stonith 的更多细节，请参阅 clusterlabs.org/pacemaker/doc/crm_fencing.html。

同样，将 `start-failure-is-fatal` 属性设置为 `false`。该属性始终用于将故障视为致命。我们希望禁用它，让集群根据资源当前的失败计数和迁移阈值，自行决定是否尝试在同一节点上启动。运行以下命令：

```bash
sudo pcs property set start-failure-is-fatal=false
```

请注意，您可以使用以下命令列出 Pacemaker 集群属性，该命令会列出已配置的属性：

```bash
## pcs property list

Cluster Properties:

cluster-infrastructure: corosync

cluster-name: sqlonlinux

dc-version: 1.1.16-12.el7_4.5-94ff4df

have-watchdog: false

master-ag_cluster: 0

start-failure-is-fatal: false

stonith-enabled: false
```

您可以使用 `--all` 选项列出所有属性，包括带有默认值的未设置属性。我的安装返回了 40 个属性：

```bash
$ sudo pcs property list --all
```

以下是当前的集群状态：

```bash
## pcs status

Cluster name: sqllinuxc

Stack: corosync

Current DC: sqllinuxlinux2 (version 1.1.16-12.el7_4.5-94ff4df) - partition with quorum

Last updated: Wed Jan 24 06:35:11 2018

Last change: Wed Jan 24 06:35:07 2018 by root via cibadmin on sqllinuxlinux

3 nodes configured

0 resources configured

Online: [ sqllinux1 sqllinux2 sqllinuxlinux3 ]

No resources

Daemon Status:

corosync: active/disabled

pacemaker: active/disabled

pcsd: active/enabled
```

接下来，在 SQL Server 的三个实例上都创建以下登录：

```sql
USE master

GO

CREATE LOGIN pacemakerLogin WITH PASSWORD = N'Pa$$word!!'
```

为创建的登录授予以下权限：

```sql
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::agl TO pacemakerLogin

GRANT VIEW SERVER STATE TO pacemakerLogin
```

在每个节点上保存登录信息。创建一个包含以下信息的文本文件，SQL Server 登录名称和密码：

```
pacemakerLogin

Pa$$word!!
```

将其保存到 `/var/opt/mssql/secrets/passwd`。将权限更改为仅允许 root 用户可读：

```bash
sudo chown root:root /var/opt/mssql/secrets/passwd

sudo chmod 400 /var/opt/mssql/secrets/passwd
```

最后它看起来像这样：

```bash
$ ls -l /var/opt/mssql/secrets/passwd

-r-------- 1 root root Jan 24 07:25 /var/opt/mssql/secrets/passwd
```

从 `sqllinux1` 创建可用性组资源：

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=agl master=true
```

基本上，使用 `pcs` 命令管理集群资源。`mssql` 是安装了 SQL Server 高可用包的资源提供程序。由于使用了 `master` 选项，创建了主从资源。这是集群的当前状态：

```bash
## pcs status

Cluster name: sqllinuxc

Stack: corosync

Current DC: sqllinuxlinux2 (version 1.1.16-12.el7_4.5-94ff4df) - partition with quorum

Last updated: Wed Jan 24 06:35:11 2018

Last change: Wed Jan 24 06:35:07 2018 by root via cibadmin on sqllinuxlinux

3 nodes configured

3 resources configured

Online: [ sqllinux1 sqllinux2 sqllinuxlinux3 ]

Full list of resources:

Master/Slave Set: ag_cluster [sqllinux1]

Stopped: [sqllinux2 sqllinuxlinux3]

Daemon Status:

corosync: active/disabled

pacemaker: active/disabled

pcsd: active/enabled
```

列出可用的 Open Cluster Framework (OCF) 资源提供程序：

```bash
$ sudo pcs resource providers
```

如果您没有安装过高可用包，您可能会遇到以下错误：

```bash
$ sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=agl master=true

Error: Agent 'ocf:mssql:ag' is not installed or does not provide metadata.

Metadata query for ocf:mssql:ag failed: -5, use --force to override
```

运行命令为集群创建虚拟 IP 资源。您需要指定静态 IP 地址：

```bash
$ sudo pcs resource create virtualip ocf:heartbeat:addr ip=13.91.249.38
```

注意我们再次创建一个集群资源，与之前创建可用性组资源一样，但这次是虚拟 IP 资源。我们可以使用约束（constraints）来强制两个资源是否在同一节点上运行，或者集群中资源的启动顺序。在这种情况下，让我们添加关联约束以确保可用性组主副本和虚拟 IP 资源运行在同一主机上。这需要一个分值为 `INFINITY` 的关联约束。运行以下语句：

```bash
$ sudo pcs constraint col add virtualip ag_cluster-master INFINITY --rsc-role=Master
```

下一个约束将确保首先启动可用性组集群资源，然后是虚拟 IP 资源。这是为了避免 IP 地址可用但指向尚未可用的节点的情况：

```bash
$ sudo pcs constraint order ag_cluster-master then start virtualip
```

最后，可以使用 destroy 命令永久删除当前节点上的集群，杀死所有集群进程并删除所有集群配置文件。这有助于移除测试配置并重新开始：

```bash
## sudo pcs cluster destroy

Shutting down pacemaker/corosync services...

Killing any remaining services...

Removing all cluster configuration files...
```

同样，您可以通过运行以下命令从 SQL Server 中删除可用性组：

```sql
DROP AVAILABILITY GROUP ag
```

## 在 Ubuntu 上配置 Pacemaker

在 Ubuntu 上配置 Pacemaker 与红帽企业级 Linux 的配置非常相似，因此在本节中我将涵盖所有所需的命令。细节可能需要参考之前关于 Red Hat Linux 的部分。当说明与红帽企业级 Linux 的指令相似时，将进行摘要。为了节省页面，将不包含命令输出。

首先创建安装了 Ubuntu 和 SQL Server 的三台虚拟机。如果您使用 Microsoft Azure，请搜索“Ubuntu SQL Server 2017”以找到镜像“Free SQL Server License: SQL Server 2017 Developer on Ubuntu Server 16.04 LTS”。参考第 1 章获取有关创建并按指示配置虚拟机的更详细说明。虚拟机 sqlonux1、sqlonux2 和 sqlonux3 将作为主备副本。

打开所有所需的防火墙端口。与之前一样，除了 TCP 端口 1433 和 5022，我们还需要打开 Pacemaker 防火墙端口。在这种情况下，我们需要打开 TCP 端口 2224、3121 和 21064 以及 UDP 端口 5405。您可以使用以下命令设置所需的端口。`ufw` 是 Ubuntu 自带的防火墙配置工具。

```bash
sudo ufw allow 1433/tcp

sudo ufw allow 5022/tcp

sudo ufw allow 2224/tcp

sudo ufw allow 3121/tcp

sudo ufw allow 21064/tcp

sudo ufw allow 5405/udp

sudo ufw reload
```

## 第 7 章：高可用与灾难恢复 241

运行以下命令在所有节点上安装 Pacemaker、隔离代理（fencing agents）、资源代理（resource agents）以及 Corosync：

```bash
$ sudo apt-get install pacemaker pcs fence-agents resource-agents

Reading package lists... Done

Building dependency tree

Reading state information... Done

resource-agents is already the newest version (1:3.9.7-1).

fence-agents is already the newest version (4.0.22-2).

pacemaker is already the newest version (1.11.4-2ubuntu1.3)

pcs is already the newest version (0.9.149-ubuntu1.1)

 upgraded, 0 newly installed, 0 to remove and 81 upgraded.
```

从我新创建的 Azure 虚拟机可以看出，操作系统已经安装了所需的软件，但在你的情况下可能会有所不同。接下来，运行此命令设置 `hacluster` 用户密码：

```bash
sudo passwd hacluster
```

在所有节点上启用并启动 pcsd 和 Pacemaker：

```bash
$ sudo systemctl enable pcsd

$ sudo systemctl start pcsd

$ sudo systemctl enable pacemaker
```

正在同步 pacemaker.service 状态到 SysV init（使用 /lib/systemd/systemd-sysv-install...）：
执行 /lib/systemd/systemd-sysv-install enable pacemaker

如所述，Pacemaker 集群配置存储在 `/etc/corosync/corosync.conf`。在下面的示例中，你可以看到节点列表和日志配置。该文件在执行 `pcs cluster setup` 时创建。对于红帽企业版 Linux（Red Hat Enterprise Linux），也会创建相同的配置文件。

```yaml
totem {

version: 2

secauth: off

cluster_name: sqlonlinuxc

transport: udpu

}

nodelist {

node {

  ring0_addr: sqlonlinux1

  nodeid: 1

}
```

## 运行在 Linux 上的 Microsoft SQL Server 2017

```yaml
node {

  ring0_addr: sqllinux2

  nodeid: 2

}

node {

  ring0_addr: sqllinux3

  nodeid: 3

}

quorum {

  provider: corosync_votequorum

}

logging {

  logfile: yes

  logfile: /var/log/corosync/corosync.log

  to_syslog: yes

}
```

## 注意

在编写本文时，安装过程中存在关于日志文件位置的 Bug，它错误地指向了 `/var/log/cluster/corosync.log`。解决方法仅是修复位置并将其更改为 `/var/log/corosync/corosync.log`，或者直接在 `/var/log/cluster/corosync.log` 创建该文件。厂商正在修复此问题。

接下来，与红帽企业版 Linux 一样，对三个节点集群运行以下命令：

```bash
$ sudo pcs cluster auth sqllinux1 sqllinux2 sqllinux3 -u hacluster -p Pa$$word!

$ sudo pcs cluster setup --name sqllinuxc sqllinux1 sqllinux2 sqllinux3

$ sudo pcs cluster start --all
```

安装 SQL Server 高可用性包：

```bash
$ sudo apt-get install mssql-server-ha
```

这次我在我的 Azure 虚拟机上尝试时并不顺利，因为遇到了了一个错误。因此，我必须按照所示注册仓库：

```bash
sudo add-apt-repository "$(curl https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update
```

然后我就可以像之前指示的那样运行 `apt-get install` 了。

## 第 7 章：高可用与灾难恢复 243

与红帽企业版 Linux 相同，通过将 `stonith-enabled` 属性设置为 `false` 来禁用 Stonith：

```bash
$ sudo pcs property set stonith-enabled=false
```

同时将 `start-failure-is-fatal` 属性设置为 `false`。该属性始终用于将启动失败视为致命错误，从而让集群决定是否尝试在同一节点上重新启动：

```bash
sudo pcs property set start-failure-is-fatal=false
```

接下来，在三个 SQL Server 实例上创建以下登录登录：

```sql
USE [master]

GO

CREATE LOGIN pacemakerLogin with PASSWORD=N'Pa$$word!'
```

为创建的用户授予权限：

```sql
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP:agl TO pacemakerLogin

GRANT VIEW SERVER STATE TO pacemakerLogin
```

在每个节点上保存登录信息。创建一个包含以下信息的文本文件，即 SQL Server 登录名和密码：

```text
pacemakerLogin

Pa$$word!
```
