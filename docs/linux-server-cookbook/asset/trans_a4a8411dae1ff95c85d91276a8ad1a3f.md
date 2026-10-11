
- 提供商虚拟网络
- 租户物理网络
- 自助虚拟网络
- 提供商物理网络

图 16.10：使用 VXLAN 的 OpenStack 网络架构。来源：OpenStack

采用 OVN 简化了基础设施，但需要更多关于**软件定义网络（SDN）** 如何工作的知识，以将逻辑部分与数据路径分离。图 16.11 展示了涉及的组件：

![](img/863afa537de4eed7deb11978bfbfa90e_570_0.png)

## 集成 OVN 的网络服务

![](img/863afa537de4eed7deb11978bfbfa90e_571_0.png)

图 16.11：使用 VXLAN 的 OpenStack 网络架构。来源：OpenStack

## 虚拟机的网络

要在 OpenStack 上运行虚拟机，它必须连接到网络。该网络至少应关联一个子网。可以配置子网以向连接到它的虚拟机提供 DHCP 地址。参数 `network create` 用于创建网络，该网络可以是叠加网络或提供商网络。参数 `subnet create` 用于在内部创建子网。图 16.12 创建了一个提供商网络，用作浮动 IP 的外部网络。

```bash
[stack@client ~]$ openstack network create external --share --external \
>   --provider-physical-network datacentre \
>   --provider-network-type flat
```

图 16.12：创建外部网络的示例命令

以下命令的输出包括 `id`、`status` 以及与创建的网络相关的信息。请参阅表 16.4：

| 字段 | 值 |
| :--- | :--- |
| admin_state_up | UP |
| availability_zone_hints | |
| availability_zones | |
| created_at | 2022-12-04T19:44:24Z |
| description | |
| dns_domain | |
| id | 8229579d-1427-4b74-bb89-1d7a16cfac5f |
| location | cloud='development', project.domain_id=, project.domain_name='Default', project.id='7690147846bb4f24b724a940673d6ce8', project.name='admin', region_name='regionOne', zone= |
| mtu | 1500 |
| name | external |
| port_security_enabled | True |
| project_id | 7690147846bb4f24b724a940673d6ce8 |
| provider:network_type | flat |
| provider:physical_network | datacentre |
| provider:segmentation_id | None |
| qos_policy_id | None |
| revision_number | 1 |
| router:external | External |
| segments | None |
| shared | True |
| status | ACTIVE |
| subnets | |
| tags | |
| updated_at | 2022-12-04T19:44:24Z |

表 16.4：创建网络的输出示例。

物理网络通过地址为 10.0.0.0/24 的子网进行连接。图 16.13 显示了附加到之前创建的网络的子网创建示例。

```bash
[stack@client ~]$ openstack subnet create subexternal --no-dhcp \
> --network external --subnet-range 10.0.0.0/24 \
> --allocation-pool start=10.0.0.220,end=10.0.0.230 \
> --gateway 10.0.0.1 --dns-nameserver 8.8.8.8
```

![](img/863afa537de4eed7deb11978bfbfa90e_573_0.png)

子网默认启用 DHCP 进行创建；选项 `--no-dhcp` 用于禁用它。前一条命令的输出如表 16.5 所示：

| 字段 | 值 |
| --- | --- |
| allocation_pools | 10.0.0.220-10.0.0.230 |
| cidr | 10.0.0.0/24 |
| created_at | 2022-12-04T20:10:50Z |
| description | |
| dns_nameservers | 8.8.8.8 |
| enable_dhcp | False |
| gateway_ip | 10.0.0.1 |
| host_routes | |
| id | 229b4e9e-35aa-47db-8f30-8ad1dcd50608 |
| ip_version | 4 |
| location | cloud='development', project.domain_id=, project.domain_name='Default', project.id='7690147846bb4f24b724a940673d6ce8', project.name='admin', region_name='regionOne', zone= |
| name | subexternal |
| network_id | 8229579d-1427-4b74-bb89-1d7a16cfac5f |
| prefix_length | None |
| project_id | 7690147846bb4f24b724a940673d6ce8 |
| tags | |
| updated_at | 2022-12-04T20:10:50Z |

表 16.5：创建子网的输出示例

图 16.14 展示了创建供虚拟机使用的叠加网络。

```bash
[stack@client ~]$ openstack network create overlay_network
[stack@client ~]$ openstack subnet create sub_overlay_network \
> --network overlay_network --subnet-range 172.16.0.0/24
```

图 16.14：创建网络和子网的示例命令

从网络创建来看，需要注意的是，当创建叠加网络时，MTU 小于 1500，因为一些字节被保留用于封装，并且前例中的封装类型为 GENEVE。请参阅表 16.6：

| 字段 | 值 |
|---|---|
| mtu | 1442 |
| provider:network_type | geneve |

表 16.6：与叠加网络相关的子网字段。

表 16.7 显示了与网络和子网相关的典型任务。

| 参数 | 描述 |
|---|---|
| network list | 列出已创建的现有网络，包括为其配置的子网。 |
| network delete | 删除未使用的网络。 |
| network show | 显示指定网络的所有信息。 |
| network set | 设置子网的不同参数，例如名称或描述。 |
| subnet list | 列出已创建的现有子网。 |
| subnet delete | 删除未使用的子网。 |
| subnet show | 显示指定子网的所有信息。 |
| subnet set | 设置子网的不同参数 |

表 16.7：与网络和子网相关的典型任务

## 路由

创建网络后，可以将虚拟机连接到叠加网络，但它将与集群外部隔离。为了将外部网络与私有网络连接，需要创建一个虚拟路由器。参数 `router create` 用于创建虚拟路由器。请参阅图 16.15：

```bash
[stack@client ~]$ openstack router create router_private -c id -c status
+-------+----------------------------------+
| Field | Value                            |
+-------+----------------------------------+
| id    | 51ac2c9c-54d6-4eab-9572-c1dcfd3e1d84 |
| status | ACTIVE                            |
+-------+----------------------------------+
```

![](img/863afa537de4eed7deb11978bfbfa90e_575_0.png)

为了指定连接到虚拟路由器的外部网络，使用参数 `set` 和选项 `--external-gateway`。使用参数 `router add subnet`，可以将子网添加到路由器。图 16.16 显示使用之前创建的路由器的操作：

```bash
[stack@client ~]$ openstack router set --external-gateway external router_private
[stack@client ~]$ openstack router add subnet router_private sub_overlay_network
```

![](img/863afa537de4eed7deb11978bfbfa90e_575_1.png)

表 16.8 显示了与路由器相关的典型任务

| 参数 | 描述 |
| :--- | :--- |
| router remove subnet | 从路由器中删除现有的子网。 |
| router list | 列出已创建的现有路由器。 |
| router delete | 如果现有路由器未在使用，则将其删除。 |
| router show | 显示指定路由器的所有信息。 |
| router set | 设置路由器的不同参数，例如名称或描述。 |
| router unset | 取消配置一些参数，例如外部网关。 |

![](img/863afa537de4eed7deb11978bfbfa90e_575_2.png)

## 安全组

安全组是一组应用于虚拟机的防火墙规则。默认情况下，OpenStack 仅允许出站流量。当创建项目时，会创建一个安全组并作为默认值关联。管理员和用户可以向安全组添加规则，或者创建一个新的安全组并将规则添加到其中。图 16.17 显示了允许连接到端口 22（SSH）的示例：

```bash
[stack@client ~]$ openstack security group create allowssh -c id
+----+-----------------------------------------+
| Field | Value                                 |
+----+-----------------------------------------+
| id  | 7af16f2c-b257-4c78-8d56-cd7397843976  |
+----+-----------------------------------------+

[stack@client ~]$ openstack security group rule create  --ingress \
>  --ethertype IPv4 --protocol tcp --dst-port 22 allowssh -c id
+----+-----------------------------------------+
| Field | Value                                 |
+----+-----------------------------------------+
| id  | 97a95b9d-1946-4c21-9d96-961088d521994  |
+----+-----------------------------------------+
```

图 16.17：创建安全组并允许 SSH 的示例

表 16.9 显示了与安全组相关的典型任务。

| **参数** | **描述** |
|---|---|
| security group list | 列出已创建的现有安全组。 |
| security group delete | 删除现有的安全组。 |
| security group show | 显示指定安全组的所有信息，包括分配的规则。 |
| security group set | 设置安全组的不同参数，例如名称或描述。 |
| security group rule delete | 从安全组中删除现有的安全组规则。 |

表 16.9：与安全组相关的典型任务

## 公钥

为了访问虚拟机，必须使用 SSH 密钥认证方法。为 Linux 发行版提供的云映像没有默认密码。OpenStack 允许上传公钥以注入虚拟机，从而允许远程访问。请参阅图 16.18：

```bash
[stack@client ~]$ openstack keypair create --public-key ~/.ssh/id_rsa.pub mykey
+------------+------------------------------------------------------+
| Field | Value                                      |
+------------+------------------------------------------------------+
| fingerprint | f1:1a:36:55:5c:7f:38:5f:ef:2b:5d:85:61:1b:d8:e6 |
| name | mykey                                      |
| user_id | 6c1f154be7c14eb3b137e73910fad113           |
+------------+------------------------------------------------------+
```

