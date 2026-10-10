

以下内容可以添加到你的 `/etc/hosts` 文件末尾：

```
192.168.122.2      controller
192.168.122.5      compute
```

你需要牢记这一更改。在生产环境中你未必会这样操作，但为了我们的目的，在设置服务时使用“controller”和“compute”这些名称来指代各个系统，会使解释变得更加容易。

## 软件包

在安装的这个阶段，你只需要两个软件包：

```
$ sudo apt-get install ntp python-openstackclient
```

网络时间协议（ntp）守护程序可确保节点之间的时间保持正确同步，而 `python-openstackclient` 工具则是在命令行中向 OpenStack 服务发出大多数查询时所使用的工具。我们在计算节点上安装客户端，以便日后可能需要用于调试时可以使用它。

## OpenStack 组件

现在核心系统已经准备就绪，我们将继续为 OpenStack 简单配置设置典型的常规标准服务。在控制器节点上，你将拥有以下关键服务及其相应的支持代理、守护程序和插件：

- Keystone（身份）
- Nova（计算）
- Neutron（网络）
- Glance（镜像）

在计算节点上，你只需要运行 Nova 计算服务以运行实例，并运行 Neutron 的 Open vSwitch 代理来处理隧道。我们将从配置控制器节点开始。

### 控制器节点

再次强调，你的控制器节点将运行 OpenStack 的核心服务。它运行大多数服务、数据库和队列服务器，并托管 API 端点。此服务器还有两个网卡，用于处理来自计算服务器的网络流量。

#### Keystone

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
> 包含 OpenStack 配置的目录（例如 `/etc/keystone`）由 root 用户拥有，并且仅允许 root 用户读取访问。其中包含的文件包含重要的机密数据，系统中的其他用户不应能够访问这些数据。请勿更改这些权限。

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

#### Fernet 令牌

Fernet 是对称密钥加密的实现，用于加密明文，并使用相同的加密密钥解密密文。使用该实现后，Fernet 令牌在 OpenStack Kilo 版本中作为受支持的令牌格式发布，并在随后的版本中进行了性能和可靠性方面的改进。Fernet 相对于 UUID 的主要优势是令牌不需要*持久化*；也就是说，它们不需要存储在数据库中。这解决了令牌数据库复制滞后的问题，并且也意味着不需要使用 cron 任务来清理过期的令牌。尽管 UUID 令牌仍然被更广泛地使用，包括本书后续章节中我们的部署场景，但 Keystone 社区正在努力使 Fernet 成为默认的令牌格式。

Fernet 令牌由 Fernet 密钥进行加密签名。Fernet 签名密钥通常位于 `/etc/keystone/fernet-keys`，并通常每周或每月轮换一次，以防止对加密进行暴力破解攻击。虽然你可以拥有更多的密钥，但你需要至少拥有三个可用的 Fernet 密钥：*主要*（primary）、*次要*（secondary）和*预置*（staged）。

密钥轮换可能需要更多的解释才能清楚，但主要需要记住的是，如果你以集群方式运行 Keystone，你不需要同时执行密钥轮换。如果你需要更多信息，OpenStack 社区的各个成员已撰写博客文章并在会议上就其使用和实现进行了演讲。欲了解更多内容，你可以从 OpenStack 管理员指南中位于 `http://docs.openstack.org/admin-guide/keystone_fernet_token_faq.html` 的常见问题解答开始，并在网上搜索更多资料。

下一步是将模式添加到你的 Keystone 数据库中。有一个 `keystone-manage` 命令可以帮助完成此操作，需要以 root 用户身份运行：

```
$ sudo -u root /bin/sh -c "keystone-manage db_sync" keystone
```

现在我们要设置 Fernet。

```
$ sudo keystone-manage fernet_setup --keystone-user keystone \
--keystone-group keystone
2016-05-15 16:52:25.128 10350 INFO keystone.token.providers.fernet.utils [-] [fernet_tokens]
key_repository does not appear to exist; attempting to create it
2016-05-15 16:52:25.129 10350 INFO keystone.token.providers.fernet.utils [-] Created a new
key: /etc/keystone/fernet-keys/0
2016-05-15 16:52:25.129 10350 INFO keystone.token.providers.fernet.utils [-] Starting key
rotation with 1 key files: ['/etc/keystone/fernet-keys/0']
2016-05-15 16:52:25.129 10350 INFO keystone.token.providers.fernet.utils [-] Current primary
key is: 0
2016-05-15 16:52:25.130 10350 INFO keystone.token.providers.fernet.utils [-] Next primary key
will be: 1
2016-05-15 16:52:25.130 10350 INFO keystone.token.providers.fernet.utils [-] Promoted key 0
to be the primary: 1
2016-05-15 16:52:25.130 10350 INFO keystone.token.providers.fernet.utils [-] Created a new
key: /etc/keystone/fernet-keys/1
```

为 Keystone 配置的最后一个组件是 Apache Web 服务器。首先，你需要将 `/etc/apache2/apache2.conf` 中的 ServerName 设置为以下内容：

```
ServerName controller
```

接下来，在 `/etc/apache2/sites-available/wsgi-keystone.conf` 创建一个文件并添加以下内容：

```
Listen 5000
Listen 35357

<VirtualHost *:5000>
    WSGIDaemonProcess keystone-public processes=5 threads=1 user=keystone group=keystone
    WSGIProcessGroup keystone-public
    WSGIScriptAlias / /usr/bin/keystone-wsgi-public
    WSGIApplicationGroup %{GLOBAL}
    WSGIPassAuthorization On
    <IfVersion >= 2.4>
        ErrorLogFormat "%{C}t %M"
    </IfVersion>
    ErrorLog /var/log/apache2/keystone.log
    CustomLog /var/log/apache2/keystone_access.log combined
    <Directory /usr/bin>
        <IfVersion >= 2.4>
            Require all granted
        </IfVersion>
        <IfVersion < 2.4>
            Order allow,deny
            Allow from all
        </IfVersion>
    </Directory>
</VirtualHost>

<VirtualHost *:35357>
    WSGIDaemonProcess keystone-admin processes=5 threads=1 user=keystone group=keystone
    WSGIProcessGroup keystone-admin
    WSGIApplicationGroup %{GLOBAL}
    WSGIPassAuthorization On
    <IfVersion >= 2.4>
        ErrorLogFormat "%{C}t %M"
```

