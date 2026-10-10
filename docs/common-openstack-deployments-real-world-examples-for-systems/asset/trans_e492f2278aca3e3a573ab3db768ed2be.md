
当然可以。大多数文档遵循与我们相同的模式，先分配一个私有地址，然后根据需要分配一个连接到提供商网络的浮动 IP。然而，如果运营者知道其服务需要在特定网络上或互联网上，他们通常会直接从提供商网络分配这些地址。

请回顾第 3 章“网络”，其中对网络及其在本书中所做的决定进行了深入讨论。

现在，我们将讲解如何为您的实例添加一个浮动 IP，以便我们可以 SSH 登录到该实例，并在其上运行 Web 服务器。在实例的“操作”菜单中，您应选择“关联浮动 IP”以弹出操作 IP 的界面。在“IP 地址”下，您可以点击加号添加一个新 IP，这将弹出“分配浮动 IP”界面。它将询问您从哪个池获取地址，而您唯一的选项应该是 `ext-net`。当您点击“分配 IP”时，它会从池中选择一个地址并使其可用于分配给您的虚拟机。默认情况下，它会带您回到“管理浮动 IP 关联”界面，并将新的 IP 地址填入“IP 地址”字段中，如图 6.9 所示。

现在您点击“关联”将其添加到您的实例中。这是实时操作的，通常无需重启实例即可迅速生效。您应该会看到一个绿色的“成功”对话框，并且在实例的“IP 地址”列中，您应该看到类似以下内容：

10.190.0.11
浮动 IP：
203.0.113.9

![](img/8684900d708748f86bb043faa5589f9e_158_0.png)

图 6.9 分配 IP

这个 `203.0.113.9/24` 地址将用于 SSH 以及访问此机器上的任何服务。无论是使用 OpenStack 仪表板（Horizon）还是使用 OpenStack 客户端命令行登录实例并安装和使用公开服务，其操作方式都是相同的。由于这些操作是相同的，我们将在本章末尾解释如何做。现在，您可以学习如何在命令行上执行上述所有操作，或者直接跳到本章末尾的“运行服务”部分。

### 启动实例：OpenStack 客户端

使用 OpenStack 仪表板是一个便捷的方式来与 OpenStack 交互，如果您正在寻找一个简单的界面或不熟悉命令行。然而，许多运营者更喜欢使用命令行与 OpenStack 交互，因为它可能更方便、更快，并且提供更多的选项以及编写脚本来完成任务的能力。现在，我们将带您完成与仪表板相同的工作，但使用 OpenStack 客户端。

在生产环境中，您通常会在一个位于 OpenStack 部署外部的系统上运行客户端，该系统能够访问客户端通信的 OpenStack API。为了简化这些示例，我们将改为从您在第 5 章创建的 Controller 节点上运行所有这些命令。使用仪表板时，您是以特定用户身份登录以完成每个任务的。在使用 OpenStack 客户端时，您将改为使用在第 5 章运行 Puppet 时创建的 `openrc` 凭证文件。您可以直接查看这些文件以了解其内容，或者您也可以向 shell 环境发出一系列导出命令，这些将作为您运行后续命令时的凭证。

### 添加风味

首先，您需要添加一个新风味以供使用。这将类似于您通过仪表板创建的风味，但我们将给它另一个名字。您将使用管理员账户为此风味创建以供所有用户使用。

> **提示**
> OpenStack 命令倾向于提供大量细节，这些细节并不总是适合显示在这些页面上。许多这些命令的输出包含在一个按章节分类的脚本和配置的 GitHub 仓库中，位于 https://github.com/DeploymentsBook/scripts-and-configs。

```bash
$ source /etc/openstack.admin
$ openstack flavor list
```

| ID | 名称 | RAM | 磁盘 | 临时存储 | VCPUs | 是否公开 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | m1.tiny | 512 | 1 | 0 | 1 | True |
| 2 | m1.small | 2048 | 20 | 0 | 2 | True |
| 3 | m1.medium | 4096 | 40 | 0 | 2 | True |
| 4 | m1.large | 8192 | 80 | 0 | 4 | True |
| 5 | m1.xlarge | 16384 | 160 | 0 | 8 | True |
| 74fa1799-055f-4411-a8d7-55026d9a7894 | m1.smaller | 768 | 5 | 0 | 1 | True |

$ openstack flavor create --ram 768 --disk 5 --ephemeral 0 --vcpus 1 --public m1.smaller2

| 字段 | 值 |
| :--- | :--- |
| OS-FLV-DISABLED:disabled | False |
| OS-FLV-EXT-DATA:ephemeral | 0 |
| disk | 5 |
| id | 874857cf-ca29-4dea-b121-aaf36517ac3e |
| name | m1.smaller2 |
| os-flavor-access:is_public | True |
| ram | 768 |
| rxtx_factor | 1.0 |
| swap | |
| vcpus | 1 |

您可以再次运行 `openstack flavor list` 以查看您的 `m1.smaller2` 风味已创建，并且与之前通过仪表板创建的 `m1.smaller` 风味几乎完全相同。

### 添加镜像

从这一步开始，您将使用 test 用户来运行命令。在此步骤中，您将向部署中添加一个镜像以供使用。我们将再次使用 Ubuntu 服务器镜像，但我们将给它一个不同的名称。

```bash
$ source /etc/openrc.test
$ openstack image list
```

| ID | 名称 |
| :--- | :--- |
| 8b6b345c-1e08-426e-b24b-37df6e16a6b0 | Ubuntu 14.04 Server |
| b592fbd2-cbb9-4159-bc22-f2a591b4c348 | Cirros 0.3.4 |

```bash
$ wget https://cloud-images.ubuntu.com/releases/14.04/4/release/ubuntu-14.04-server-cloudimg-amd64-disk1.img
$ openstack image create --container-format bare \
--disk-format qcow2 --min-disk 5 --min-ram 768 \
--file ubuntu-14.04-server-cloudimg-amd64-disk1.img "Ubuntu 14.04 Server 2"
```

| 字段 | 值 |
| :--- | :--- |
| checksum | 2a0b721cb690591b839c7a192dcc2d99be77 |
| container_format | bare |
| created_at | 2016-05-02T20:12:45Z |
| disk_format | qcow2 |
| file | /v2/images/46b946773b47ba03b03bc46aa0682d c0d5b61d04-9064-cd65-363a-afa9a58c0f7c/file |
| id | 5 |
| min_disk | 768 |
| min_ram | |
| name | Ubuntu 14.04 Server 2 |
| owner | d69446773b47ba03b03bc46aa0682d |
| protected | False |
| schema | /v2/schemas/image |
| size | 259392000 |
| status | active |
| tags | |
| updated_at | 2016-05-02T20:12:47Z |
| virtual_size | None |
| visibility | private |

由于这是一个本地镜像文件，命令可能需要一点时间才能返回，然后通常会迅速显示为活动状态。如果没有，您可以使用 `show` 命令检查该镜像加载时的状态。一旦状态变为 `"active"`，您就可以使用该镜像启动实例。

```bash
$ openstack image show 'Ubuntu 14.04 Server 2'
```

| 字段 | 值 |
|:----------|:----------|
| checksum | 2a0bf21fbe9d510c97a419dbc2d99eb7 |
| container_format | bare |
| created_at | 2016-05-02T20:12:45Z |
| disk_format | qcow2 |
| file | /v2/images/cd6b510d-9064-4dc5-b63a-afa9a5f0c7c7/file |
| id | cd6b510d-9064-4dc5-b63a-afa9a5f0c7c7 |
| min_disk | 5 |
| min_ram | 768 |
| name | Ubuntu 14.04 Server 2 |
| owner | d4944a473fdb47ba930b3c4bca06d82d |
| protected | False |
| schema | /v2/schemas/image |
| size | 259392000 |
| status | active |
| tags | |
| updated_at | 2016-05-02T20:12:47Z |
| virtual_size | None |
| visibility | private |

### 启动前访问和安全

使用仪表板时，在此阶段您调整了设置，添加了 SSH 密钥，并修改了默认安全组规则，以便为实例添加 ping、SSH 和 HTTP 访问。我们将首先通过 OpenStack 客户端查看这些设置目前的样子。

```bash
$ source /etc/openrc.test
$ openstack keypair list
```

| 名称 | 指纹 |
|:----------|:----------|
| elizabeth-Desktop | 73:08:27:ee:8f:6d:07:0f:d3:cd:cb:2f:73:4e:38:ab |

```bash
$ openstack security group rule list default
```

| ID | IP 协议 | IP 范围 | 端口范围 |
|:----------|:----------|:----------|:----------|
| 0743e044-5707-47fa-87a7-e5a5036e9d3e | tcp | 0.0.0.0/0 | 80:80 |
| 3977d290-35cb-43a6-8408-c8e6d665c987 | icmp | 0.0.0.0/0 | |
| 52d61ae0-6518-41de-873c-eb8ef91b8cc0 | | | |
| 742da30f-515a-47cc-b8c0-5776b1c78ec8 | tcp | 0.0.0.0/0 | 22:22 |
| 7700b0fe-26a1-4a7b-bca4-57e8b181e0c3 | | | |
