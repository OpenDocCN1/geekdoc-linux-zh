
系统启动后，您需要启用 Ubuntu 云归档（Ubuntu Cloud Archive）以获取最新版本的 OpenStack，并更新软件包列表以及云归档中比 Ubuntu 14.04 默认提供的更新版本。请执行以下命令：

```
$ sudo add-apt-repository cloud-archive:mistaka
$ sudo apt-get update
$ sudo apt-get dist-upgrade
```

请注意第一条命令中的 `mistaka`。如前所述，在本书撰写时，Mistaka 是 OpenStack 最新稳定版的代号。更新命令也非常重要。如果不执行该命令，您将无法获取所有必需的软件包，并且会安装一个较旧、与本书中部分选项不兼容的 OpenStack 版本。

接下来，您将配置网络并安装运行 OpenStack 各组件所需的软件包。

> **提示**
>
> 名为 `scripts-and-configs` 的 Git 仓库是 GitHub 上 `DeploymentsBook` 项目的一部分，位于 <https://github.com/DeploymentsBook>。该仓库包含了许多配置文件的内容以及本章中更详细的说明。您可以使用此仓库将示例直接复制粘贴到系统中，而无需从书中逐字复制。

我们将首先从控制器节点开始。

## 控制器节点

控制器节点是您 OpenStack 部署的核心。它运行所有 OpenStack 服务、数据库、消息队列服务器以及其他组件。另一个节点（计算节点）则专门用于运行计算实例。

## 网络

我们的部署网络规范已在第 3 章中详细讨论过。您需要做的第一个配置修改是 `/etc/network/interfaces` 文件，该文件用于配置您的网络。在下面的示例中，假设您已定义本地回环接口 `lo`，以及两个网卡 `eth0` 和 `eth1`。

> **请牢记**
>
> - `eth0` 接口是连接到 `virbr0` 或连接至计算服务器的交换机的接口。
> - `eth1` 接口要么连接到 `virbr1`，要么是将系统连接到其他交换机（即本例提供商网络中“公网”地址）的接口。

使用 `sudo` 和您喜欢的文本编辑器打开 `/etc/network/interfaces`，并进行修改，使其类似于以下内容：

```
## 回环网络接口
auto lo
iface lo inet loopback

## 主要/维护网络接口
auto eth0
iface eth0 inet static
    address 192.168.122.2
    netmask 255.255.255.0
    network 192.168.122.0
    broadcast 192.168.122.255
    gateway 192.168.122.1
    dns-nameservers 8.8.8.8 8.8.4.4

## 租户网络（未直接分配地址）
auto eth1
iface eth1 inet manual
```

在此示例中，控制器服务器的 IP 地址为 `192.168.122.2`。请根据您的实际网络环境和控制器服务器从 `DHCP` 获取的地址调整此设置。

现在，您需要启用 `eth1` 网络。该接口不会被直接分配地址，但需要处于 `UP` 状态，以便后续网络服务使用：

```
$ sudo ifup eth1
```

下次重启时，该接口将自动启用。如果您愿意，现在就可以进行测试，并确认 `eth1` 处于 `UP` 状态。

```
$ ip link show eth1
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT
    group default qlen 1000
    link/ether 54:24:00:7b:95:83 brd ff:ff:ff:ff:ff:ff
```

最后，将控制器主机和计算主机添加到您的 `/etc/hosts` 文件中。这并非生产环境中必需的更改，但有助于简化本章后续步骤，因为在仅需名称的地方，它将解析相应的 IP 地址。在此示例中，计算服务器的地址为 `192.168.122.5`。以下内容可添加至文件末尾：

```
192.168.122.2 controller
192.168.122.5 compute
```

在进行本章后续操作时，请留意此更改。在配置中，我们将使用名称“`controller`”和“`compute`”来代替各服务器的 IP 地址。

## 软件包

OpenStack 控制器需要多个软件包来准备环境。这些软件包通常来自标准的 Ubuntu 软件库，因此有时 Ubuntu 云归档团队会在库中包含软件组件的更新版本，以配合较新版本的 OpenStack 使用。请使用以下命令在控制器服务器上安装这些先决软件包：

```
$ sudo apt-get install ntp rabbitmq-server mysql-server \
python-pymysql python-openstackclient openvswitch-switch
```

这将安装网络时间协议（`ntp`）守护进程，以确保节点间的时间正确同步。`ntp` 无需额外配置。OpenStack 后端运行所需的服务也将通过该命令安装，包括消息队列服务 RabbitMQ、MySQL 服务器以及用于连接 MySQL 的 Python 相关模块。安装过程中系统会提示您设置 MySQL 的 `root` 密码。请确保这是一个独特且安全的密码，并牢记它。`python-openstackclient` 工具将用于向 OpenStack 服务发起大多数查询。Open vSwitch 软件包用于网络配置，将在本章后续部分进行配置。

## 初始配置

> **提示**
>
> 是否收到“`E: Unable to locate package python-pymysql`”消息？该软件包仅包含在 Ubuntu 云归档（UCA）中。请确保您已执行之前的步骤以启用 UCA，并运行 `apt-get update` 以确保您的软件源是最新的。

RabbitMQ 安装时不会提示创建用户和设置权限，因此现在我们需要完成这些操作。在以下命令及后续交互中，我们将创建一个名为 "openstack" 的用户，并将 `RABBIT_PASSWORD` 替换为您希望使用的密码。

```
$ sudo rabbitmqctl add_user openstack RABBIT_PASSWORD
Creating user "openstack" ...
$ sudo rabbitmqctl set_permissions openstack "\.\.\." "\.\.\." "\.\.\."
Setting permissions for user "openstack" in vhost "/" ...
```

请记住所设置的密码。在后续配置 Nova 和 Neutron 时将需要用到它。

> **提示**
>
> 我们为所有服务使用相同的 RabbitMQ 密码。在生产环境中，建议为每个服务使用不同的 RabbitMQ 凭据。

最后，需要对 MySQL 配置进行两项更改。创建名为 `/etc/mysql/conf.d/openstack.cnf` 的新文件，内容如下，并将示例中的 `192.168.122.2` 替换为您自己的控制器地址：

```
[mysql]
bind-address = 192.168.122.2
default-storage-engine = innodb
innodb_file_per_table
collation-server = utf8_general_ci
character-set-server = utf8
```

创建该文件后，重启 MySQL 服务以应用更改：

```
$ sudo service mysql restart
```

此时，您的控制器已完成基本配置。在完成计算节点的基本配置后，我们就可以开始安装用于在节点上运行服务的 OpenStack 软件包了。

## 计算节点

由于计算节点仅用于运行 OpenStack 实例，因此此处的要求相对简单。

## 网络

在计算节点上，您唯一需要修改的网络配置是 `/etc/hosts` 文件，正如您在控制器节点上所操作的那样。同样，在此示例中，我们假设控制器的地址为 `192.168.122.2`，计算服务器的地址为 `192.168.122.5`。再次强调，请更新所有示例以反映您系统的实际地址。

以下内容可以添加到你的 `/etc/hosts` 文件末尾：

```
192.168.122.2      controller
192.168.122.5      compute
```

你需要牢记这一更改。在生产环境中你未必会这样操作，但为了我们的目的，在设置服务时使用“`controller`”和“`compute`”这些名称来指代各个系统，会使解释变得更加容易。

## 软件包

在安装的这个阶段，你只需要两个软件包：

```
$ sudo apt-get install ntp python-openstackclient
```

网络时间协议（`ntp`）守护程序可确保节点之间的时间保持正确同步，而 `python-openstackclient` 工具则是在命令行中向 OpenStack 服务发出大多数查询时所使用的工具。我们在计算节点上安装客户端，以便日后可能需要用于调试时可以使用它。

## OpenStack 组件

现在核心系统已经准备就绪，我们将继续为 OpenStack 简单配置设置典型的常规标准服务。在控制器节点上，你将拥有以下关键服务及其相应的支持代理、守护程序和插件：

- Keystone（身份）
- Nova（计算）
- Neutron（网络）
- Glance（镜像）

在计算节点上，你只需要运行 Nova 计算服务以运行实例，并运行 Neutron 的 Open vSwitch 代理来处理隧道。我们将从配置控制器节点开始。

## 控制器节点

再次强调，你的控制器节点将运行 OpenStack 的核心服务。它运行大多数服务、数据库和队列服务器，并托管 API 端点。此服务器还有两个网卡，用于处理来自计算服务器的网络流量。

## Keystone

如第 1 章“什么是 OpenStack？”中所描述的，Keystone 是 OpenStack 的身份服务，为 OpenStack 提供身份、令牌、目录和策略（如角色）等服务。对于用户和服务，Keystone 可用于提供基于密码的用户认证，或通过 API 使用令牌进行 OpenStack 服务之间更偏向服务的交互。Keystone 还跟踪用户策略，并存储每个 OpenStack 服务的 API 端点。你为 OpenStack 部署的每个服务都必须向 Keystone 或提供相同功能的替代身份服务注册，因此我们希望首先安装它。

我们此前在章节中配置了 Mitaka 版本的 Ubuntu 云存档（Ubuntu Cloud Archive），这意味着我们现在可以使用 `apt-get` 安装最新的 OpenStack 稳定版软件包。但是，我们将首先创建一个 MySQL 数据库和用户，该用户拥有访问该数据库的权限，以便供 Keystone 使用。你可以使用已经熟悉的 MySQL 工具来完成此操作，或者通过命令行使用以下命令，其中 `KEYSTONE_DBPASSWORD` 替换为 Keystone 用户的数据库密码：

```
$ mysql -u root -P
mysql> CREATE DATABASE keystone;
mysql> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' IDENTIFIED BY
'KEYSTONE_DBPASSWORD';
mysql> quit
```

在安装 Keystone 本身之前，我们要确保它在启动时不会启动任何遗留的守护程序。运行以下命令（此命令没有输出）：

```
$ sudo sh -c 'echo "manual" > /etc/init/keystone.override'
```

现在你可以安装 Keystone 以及带有 WSGI（Web Server Gateway Interface）的 Apache Web 服务器，这将替代 Keystone 守护程序使用：

```
$ sudo apt-get install keystone apache2 libapache2-mod-wsgi
```

安装这些软件包后，你将拥有一个位于 `/etc/keystone/keystone.conf` 的 Keystone 配置文件。你需要使用 `sudo` 来编辑此文件。

> **警告**
>
> 包含 OpenStack 配置的目录（例如 `/etc/keystone`）由 `root` 用户拥有，并且仅允许 `root` 用户读取访问。其中包含的文件包含重要的机密数据，系统中的其他用户不应能够访问这些数据。请勿更改这些权限。

此 Keystone 配置文件需要进行几处编辑。我们将首先添加 `admin_token`。`admin_token` 是一个重要的数据片段，它赋予你对 Keystone——以及你的整个 OpenStack 部署——的大量访问权限。它暂时用于我们的初始配置，且不应设置为简单的密码。官方 OpenStack 文档建议你使用以下命令生成管理令牌：

```
$ openssl rand -hex 10
```

获取该命令的结果，并将其添加到配置文件中。这也位于 `[DEFAULT]` 部分下。示例如下：

```
admin_token=975c8ac7c7718d33ba57
```

接下来，你需要更新 `[database]` 部分，使用新的 MySQL 数据库而不是 Ubuntu 软件包创建的 SQLite 数据库。如果存在 `sqlite` 连接配置段，你需要将其注释掉，因为不能定义两种连接类型。然后添加以下内容：

```
connection = mysql+pymysql://keystone:KEYSTONE_DBPASSWORD@controller/keystone
```

最后，我们希望在我们的 Keystone 安装中使用 Fernet 令牌，因此请将以下内容添加到 `[token]` 部分：

```
provider = fernet
```

包含这些更改的 `keystone.conf` 文件示例可以在前文提到的本书的 `scripts-and-configs` 代码库中找到。

## Fernet 令牌

Fernet 是对称密钥加密的实现，用于加密明文，并使用相同的加密密钥解密密文。使用该实现后，Fernet 令牌在 OpenStack Kilo 版本中作为受支持的令牌格式发布，并在随后的版本中进行了性能和可靠性方面的改进。Fernet 相对于 UUID 的主要优势是令牌不需要持久化；也就是说，它们不需要存储在数据库中。这解决了令牌数据库复制滞后的问题，并且也意味着不需要使用 `cron` 任务来清理过期的令牌。尽管 UUID 令牌仍然被更广泛地使用，包括本书后续章节中我们的部署场景，但 Keystone 社区正在努力使 Fernet 成为默认的令牌格式。

Fernet 令牌由 Fernet 密钥进行加密签名。Fernet 签名密钥通常位于 `/etc/keystone/fernet-keys`，并通常每周或每月轮换一次，以防止对加密进行暴力破解攻击。虽然你可以拥有更多的密钥，但你需要至少拥有三个可用的 Fernet 密钥：主要（primary）、次要（secondary）和预置（staged）。

密钥轮换可能需要更多的解释才能清楚，但主要需要记住的是，如果你以集群方式运行 Keystone，你不需要同时执行密钥轮换。如果你需要更多信息，OpenStack 社区的各个成员已撰写博客文章并在会议上就其使用和实现进行了演讲。欲了解更多内容，你可以从 OpenStack 管理员指南中位于 <http://docs.openstack.org/admin-guide/keystone_fernet_token_faq.html> 的常见问题解答开始，并在网上搜索更多资料。

下一步是将模式添加到你的 Keystone 数据库中。有一个 `keystone-manage` 命令可以帮助完成此操作，需要以 `root` 用户身份运行：

```
$ sudo -u root /bin/sh -c "keystone-manage db_sync" keystone
```

现在我们要设置 Fernet。
