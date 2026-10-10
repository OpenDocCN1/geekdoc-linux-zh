
## Nova 配置（续）

将以下内容添加到您的配置中：

```
auth_type = password
project_domain_name = default
user_domain_name = default
project_name = service
username = nova
password = NOVA_PASSWORD
```

创建一个 `[vnc]` 部分，其中包含以下内容：

```
[vnc]
vncserver_listen = $my_ip
vncserver_proxyclient_address = $my_ip
```

在新的 `[glance]` 部分中，您需要告诉它在哪里找到镜像服务，在我们的案例中，该服务位于本系统上：

```
[glance]
api_servers = http://controller:9292
```

最后，添加一个 `[oslo_concurrency]` 部分，其中包含以下内容：

```
[oslo_concurrency]
lock_path = /var/run/nova
```

现在，您需要为 MySQL 数据库应用默认架构，正如我们之前对 OpenStack 其他组件所做的那样：

```
$ sudo -u root /bin/sh -c "nova-manage db sync" nova
$ sudo -u root /bin/sh -c "nova-manage api_db sync" nova-api
```

完成这些更改后，重启所有 nova 服务以使更改生效：

```
$ sudo service nova-api restart
$ sudo service nova-consoleauth restart
$ sudo service nova-scheduler restart
$ sudo service nova-conductor restart
$ sudo service nova-novncproxy restart
```

为了测试 Nova 是否正常工作，请运行以下命令：

```
$ openstack compute service list
```

| Binary            | Host      | Zone     | Status  | State |
|-------------------|-----------|----------|---------|-------|
| nova-consoleauth  | controller| internal | enabled | up    |
| nova-scheduler    | controller| internal | enabled | up    |
| nova-conductor    | controller| internal | enabled | up    |

您可能还需要运行 `openstack endpoint list --service nova` 来查看您创建的端点。

如果这一切都正常，您的 Nova 控制节点现在已配置完毕！稍后，您将在另一台服务器上设置 Nova 的计算节点部分。

## Neutron

在 OpenStack 部署中，网络服务 Neutron 可能是配置最复杂的部分之一。在本章早些时候，我们配置了几个 Open vSwitch 网桥和虚拟连接器，它们在这里将很重要。首先，我们需要像之前为其他所有服务所做的那样，创建一个 MySQL 数据库和用户：

```
$ mysql -u root -p
> CREATE DATABASE neutron;
> GRANT ALL PRIVILEGES ON neutron.* TO 'neutron'@'%' IDENTIFIED BY 'NEUTRON_DBPASSWORD';
> quit
```

配置 Neutron 以使用 Keystone 身份服务器。请记住您在提示时输入的密码；稍后配置文件中需要用到它。

```
$ source /etc/openrc.admin
$ openstack user create --domain default --password-prompt neutron
User Password:
Repeat User Password:
```

| Field   | Value                                             |
|---------|---------------------------------------------------|
| domain_id | 2262f2b8aB093a43cbbf4373486bc03ae               |
| enabled | True                                              |
| id      | f0e6a17a78f34132acdfd6755c8b4f54                |
| name    | neutron                                           |

```
$ openstack role add --project service --user neutron admin
$ openstack service create --name neutron --description \
'OpenStack Networking' network
```

| Field     | Value                 |
|-----------|-----------------------|
| description | OpenStack Networking |
| enabled   | True                  |
| id        | 213ed845959864a1872ddbc56040a0ad |
| name      | neutron               |
| type      | network               |

```
$ openstack endpoint create --region RegionOne network \
public http://controller:9696
```

| Field        | Value                                             |
|--------------|---------------------------------------------------|
| enabled      | True                                              |
| id           | 01a5628811c84583acf8010115a0210e                |
| interface    | public                                            |
| region       | RegionOne                                         |
| region_id    | RegionOne                                         |
| service_id   | 213ed845959864a1872ddbc56040a0ad                |
| service_name | neutron                                           |
| service_type | network                                           |
| url          | http://controller:9696                            |

```
$ openstack endpoint create --region RegionOne network \
internal http://controller:9696
```

| Field        | Value                                             |
|--------------|---------------------------------------------------|
| enabled      | True                                              |
| id           | fa7d9be4e9394756b33fa05429874312                |
| interface    | internal                                          |
| region       | RegionOne                                         |
| region_id    | RegionOne                                         |
| service_id   | 213ed845959864a1872ddbc56040a0ad                |
| service_name | neutron                                           |
| service_type | network                                           |
| url          | http://controller:9696                            |

```
$ openstack endpoint create --region RegionOne network \
admin http://controller:9696
```

| Field        | Value                                             |
|--------------|---------------------------------------------------|
| enabled      | True                                              |
| id           | 9fb5225b96a943189215a7dcf8fbf992f                |
| interface    | admin                                             |
| region       | RegionOne                                         |
| region_id    | RegionOne                                         |
| service_id   | 213ed845959864a1872ddbc56040a0ad                |
| service_name | neutron                                           |
| service_type | network                                           |
| url          | http://controller:9696                            |

然后，您将安装 Neutron 软件包。与 Nova 一样，您需要安装几样东西：

```
$ sudo apt-get install neutron-server neutron-dhcp-agent \
neutron-l3-agent neutron-metadata-agent neutron-plugin-ml2 \
neutron-plugin-openvswitch-agent
```

### Neutron 的基本组成部分

就像 Nova 一样，Neutron 在标准安装中有多个服务。以下是您所安装的服务的快速概述：

- **Agents** — 通常运行在您的控制节点上，并与 Neutron 服务器直接通信以提供特定功能，如 DHCP、IP 转发和 NAT。它们还可以作为插件的代理。
- **Plug-INS** — 通常与代理接口，并为特定组件提供支持，例如 Open vSwitch 等虚拟网络解决方案，或针对特定网络硬件（可能是开源或专有的）的支持。
- **Server** — 实际监听队列中 API 请求并完成任务，或者将它们路由到适当的代理或插件以进行分发，然后完成任务的服务器。

再次，您需要编辑配置文件。这次主配置文件位于 `/etc/neutron/neutron.conf`，并且您需要在 `[DEFAULT]` 部分进行以下更改或添加：

```
service_plugins = router
allow_overlapping_ips = true
api_workers = 2
rpc_workers = 2
router_scheduler_driver = neutron.scheduler.l3_agent_scheduler.ChanceScheduler
log_dir = /var/log/neutron
```

与其他配置一样，您还需要禁用引用 sqlite 的连接行，并在 `[database]` 下用 MySQL 的详细信息替换它：

```
connection = mysql://neutron:NEUTRON_DB_PASSWORD@controller/neutron
```

现在，在 `[keystone_authtoken]` 部分，您需要进行一些编辑，使其看起来像以下内容（将 `NEUTRON_PASSWORD` 替换为您之前运行 openstack 客户端命令时设置的值）：

```
auth_uri = http://controller:5000
auth_url = http://controller:35357
project_domain_name = default
user_domain_name = default
project_name = service
username = neutron
password = NEUTRON_PASSWORD
auth_type = password
```

在 `[nova]` 部分，您需要设置 auth_type，以及以下内容，其中 `NOVA_PASSWORD` 是您之前设置 nova 用户时被提示输入的密码：

```
auth_url = http://controller:35357
auth_type = password
project_domain_name = default
user_domain_name = default
region_name = RegionOne
project_name = service
username = nova
password = NOVA_PASSWORD
```

在 `[oslo_messaging_rabbit]` 部分，您需要将其更新为指向您的控制器地址，并告知 Rabbit 用户和密码：

```
rabbit_host = controller
rabbit_userid = openstack
rabbit_password = RABBIT_PASSWORD
```

接下来，您需要编辑 `/etc/neutron/l3_agent.ini` 以将 `interface_driver` 设置为 OVS：

```
interface_driver = neutron.agent.linux.interface.OVSInterfaceDriver
```

现在编辑 `/etc/neutron/plugins/ml2/openvswitch_agent.ini` 并将以下内容添加到 `[agent]` 部分：

```
tunnel_types = vxlan
```

在 `[ovs]` 部分，将 `local_ip` 更新为其自身的 IP，设置网桥映射并启用隧道：

```
local_ip = 192.168.122.2
bridge_mappings = external:br-ex
enable_tunneling = true
```

对此文件的最后更改是指定用于安全组的防火墙驱动：

```
firewall_driver = neutron.agent.linux.iptables_firewall.OVSBridgeIptablesFirewallDriver
```

现在您需要对 `/etc/neutron/dhcp_agent.ini` 进行几处编辑：

```
interface_driver = neutron.agent.linux.interface.OVSInterfaceDriver
dnsmasq_config_file = /etc/neutron/dnsmasq.conf
```

使用以下命令通过设置几个选项来创建 `/etc/neutron/dnsmasq.conf` 文件：

```
$ echo "dhcp-option-force=26,1450" | sudo tee /etc/neutron/dnsmasq.conf
```

接下来，编辑 `/etc/neutron/metadata_agent.ini` 以添加 `metadata_proxy_shared_secret`。此密钥也将由 Nova 使用。将 `something_secret` 替换为您希望使用的任意字符串：

```
metadata_proxy_shared_secret = something_secret
```

最后，您想要编辑的最后一个 Neutron 文件是位于 `/etc/neutron/plugins/ml2/ml2_conf.ini` 的 ml2 插件。此文件需要在 `[ml2]` 部分进行以下自定义：

```
type_drivers = vxlan,flat
tenant_network_types = vxlan
mechanism_drivers = openvswitch
```

在 `[ml2_type_vxlan]` 下，设置 `vni_ranges` 和 `vxlan_group`：

```
vni_ranges = 10:100
vxlan_group = 224.0.0.1
```

在重启服务之前，您需要设置 Neutron 数据库架构：

```
$ sudo -u root /bin/sh -c 'neutron-db-manage --config-file \
/etc/neutron/neutron.conf --config-file \
/etc/neutron/plugins/ml2/ml2_conf.ini upgrade mitaka'  neutron
```

现在，通过运行以下命令重启所有 Neutron 服务：

```
$ sudo service neutron-l3-agent restart
$ sudo service neutron-metadata-agent restart
$ sudo service neutron-openvswitch-agent restart
$ sudo service neutron-dhcp-agent restart
$ sudo service neutron-server restart
```

