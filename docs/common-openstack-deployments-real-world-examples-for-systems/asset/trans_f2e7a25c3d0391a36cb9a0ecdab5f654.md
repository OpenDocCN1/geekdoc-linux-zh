

```apache
WSGIApplicationGroup %{GLOBAL}
WSGIPassAuthorization On
IfVersion >= 2.4
  ErrorLogFormat "%{cu}t %M"
  IfVersion
  ErrorLog /var/log/apache2/keystone.log
  CustomLog /var/log/apache2/keystone_access.log combined
  IfVersion
Directory /var/bin
  IfVersion >= 2.4
    Require all granted
  IfVersion
  IfVersion < 2.4
    Order allow,deny
    Allow from all
  IfVersion
  IfVersion
VirtualHost
```

# 提示

这个 Apache 配置文件是本书的 [scripts-and-configs 仓库](https://github.com/DeploymentsBook/scripts-and-configs) 中包含的众多文件之一。你可以轻松地复制它，或者使用 git 从该仓库克隆它。

然后在 Apache 中启用该站点并重载：

```bash
$ sudo a2ensite wsgi-keystone
$ sudo service apache2 reload
```

现在，配置文件选项、数据库和 Web 服务器都已配置完毕，接下来你需要与该服务交互，以配置命令行层面的具体细节。首先，通过一系列导出的变量来准备你的环境。`OS_TOKEN` 是你之前在 `keystone.conf` 中设置的 `admin_token`，由提供的 openssl 命令生成。以下是一个示例。请记住，正如前面所讨论的，“controller” 已被添加到你的 `/etc/hosts` 文件中，并与你的控制器主机 IP 地址相关联。

```bash
export OS_TOKEN=975ec8ac7c771d3ba57
export OS_URL=http://controller:35357/v3
export OS_IDENTITY_API_VERSION=3
```

# 技巧

> 请记住，导出的变量不会跨 shell 或会话保留。每次打开新的 shell 或通过 SSH 登录你的服务器时，你都需要重新运行导出命令。稍后，我们将把你长期使用的导出命令放入一个文本文件中，然后运行 `source /etc/openrc.admin` 以简化操作。

设置好这些环境变量后，你就可以创建 Keystone 期望的基本服务集和端点了：

```bash
$ openstack service create --name keystone --description \
> 'OpenStack Identity' identity
```

| 字段 | 值 |
| :----- | :------ |
| description | OpenStack Identity |
| enabled | True |
| id | 238b7169d4c541568021936c7cde9636 |
| name | keystone |
| type | identity |

```bash
$ openstack endpoint create --region RegionOne identity public \
> http://controller:5000/v3
```

| 字段 | 值 |
| :----- | :------ |
| enabled | True |
| id | c4cf8d93f5e94b9cb49d764f6cb359a3 |
| interface | public |
| region | RegionOne |
| region_id | RegionOne |
| service_id | d2027a47cf854ad9f951fa55aeeffee8d6 |
| service_name | keystone |
| service_type | identity |
| url | http://controller:5000/v3 |

```bash
$ openstack endpoint create --region RegionOne identity internal \
> http://controller:5000/v3
```

| 字段 | 值 |
| :----- | :------ |
| enabled | True |
| id | 36ac8356c7464135910beaa37c64a291 |
| interface | internal |
| region | RegionOne |
| region_id | RegionOne |
| service_id | d2027a47cf854ad9f951fa55aeeffee8d6 |
| service_name | keystone |
| service_type | identity |
| url | http://controller:5000/v3 |

```bash
$ openstack endpoint create --region RegionOne identity \
> admin http://controller:35357/v3
```

| 字段 | 值 |
| :----- | :------ |
| enabled | True |
| id | e753685c582b4918a0aea53d3c8eaf49 |
| interface | admin |
| region | RegionOne |
| region_id | RegionOne |
| service_id | d2027a47cf854ad9f951fa55aeeffee8d6 |
| service_name | keystone |
| service_type | identity |
| url | http://controller:35357/v3 |

接下来，我们将添加默认域，以及预期的项目、用户、角色和服务。当被要求输入密码时，请确保记住你输入的密码。

```bash
$ openstack domain create --description 'Default Domain' default
```

| 字段 | 值 |
| :--- | :--- |
| description | Default Domain |
| enabled | True |
| id | f26f2b8ab069a3cbfbf4373486bcc3ae |
| name | default |

```bash
$ openstack project create --domain default --description \
  "Admin Project" admin
```

| 字段 | 值 |
| :--- | :--- |
| description | Admin Project |
| domain_id | f26f2b8ab069a3cbfbf4373486bcc3ae |
| enabled | True |
| id | 715e61286e1b4f6e50238508349e944fcd |
| is_domain | False |
| name | admin |
| parent_id | f26f2b8ab069a3cbfbf4373486bcc3ae |

```bash
$ openstack user create --domain default --password-prompt admin
User Password:
Repeat User Password:
```

| 字段 | 值 |
| :--- | :--- |
| domain_id | f26f2b8ab069a3cbfbf4373486bcc3ae |
| enabled | True |
| id | 6316c5c1e27e7a679a6555d0a8e1b951 |
| name | admin |

```bash
$ openstack role create admin
```

| 字段 | 值 |
| :--- | :--- |
| domain_id | None |
| id | bdce39a3d3a3410a8abdc0dc0b9191c9 |
| name | admin |

```bash
$ openstack role add --project admin --user admin admin
$ openstack project create --domain default --description \
  'Service Project' service
```

| 字段 | 值 |
| :--- | :--- |
| description | Service Project |
| domain_id | f26f2b8ab069a3cbfbf4373486bcc3ae |
| enabled | True |
| id | 91e8d3828c2a4d77b48415611a20b2c77 |
| is_domain | False |
| name | service |
| parent_id | f26f2b8ab069a3cbfbf4373486bcc3ae |

```bash
$ openstack project create --domain default --description \
    'Test Project' test
```

| 字段 | 值 |
| :--- | :--- |
| description | Test Project |
| domain_id | f26f2b8ab0694a3cbf4373466bcc3ae |
| enabled | True |
| id | 225b2e6c9de4a93b8963e57cb42cec |
| is_domain | False |
| name | test |
| parent_id | f26f2b8ab0694a3cbf4373466bcc3ae |

```bash
$ openstack user create --domain default --password-prompt test
User Password:
Repeat User Password:
```

| 字段 | 值 |
| :--- | :--- |
| domain_id | f26f2b8ab0694a3cbf4373466bcc3ae |
| enabled | True |
| id | 4d2950b731ba45a290a485ecf3affcftb |
| name | test |

```bash
$ openstack role create user
```

| 字段 | 值 |
| :--- | :--- |
| domain_id | None |
| id | ccd4d428cfe461cbc954ae70483c38d |
| name | user |

```bash
$ openstack role add --project test --user test user
```

现在，你拥有了相互关联的管理员（admin）账户项目、用户和角色，一个稍后创建属于此系统的其他 OpenStack 服务时将用到的服务项目，以及作为测试项目一部分的测试用户。你还创建了一个测试用户，它是你用于执行非管理任务（例如创建计算实例）的用户。如果你回想一下使用 DevStack 的经历，该配置中创建了类似的 admin 和 demo 用户。

## 项目、域、角色、用户和用户组

OpenStack 旨在为各种不同类型的云消费者构建灵活的基础架构。然而，OpenStack 安装中项目、域、角色、用户和用户组的存在起初可能会令人困惑。考虑到这一点，欢迎参加关于它们到底是什么的快速课程。

- **项目** — 以前称为“租户（tenant）”，项目是拥有一组相同配额并共享资源（如核心、内存和存储）的用户组。管理员租户被配置为将管理员用户与系统中的其他用户隔离开来。通常每个组织部分共享资源时会创建一个项目。
- **域** — 项目、用户和组的高层账户容器，不同的域可以使用不同的身份验证后端。
- **角色** — 定义用户在特定项目中可以执行的操作形式，即权限和特权。
- **用户** — 用于与 Keystone 交互以访问 OpenStack 服务的单个账户。
- **用户组** — 用户的集合。

用户是一个或多个项目的成员，并被分配角色。角色存在于项目内部。除了 admin 角色外，无法拥有项目外的角色。虽然角色是在项目内授予的，但一旦授予，它就是全局的。

最后，你需要取消设置基于令牌的认证环境变量，并设置刚刚配置的新基于密码的认证凭据，以测试 Keystone 是否按预期工作。`OS_PASSWORD` 将是你在创建 admin 用户时被提示输入的自定义密码。

```bash
$ unset OS_TOKEN OS_URL
$ export OS_PROJECT_DOMAIN_NAME=default
$ export OS_USER_DOMAIN_NAME=default
$ export OS_PROJECT_NAME=admin
$ export OS_USERNAME=admin
$ export OS_PASSWORD=ADMIN_PASSWORD
$ export OS_AUTH_URL=http://controller:5000/v3
$ export OS_IDENTITY_API_VERSION=3
```

为了便于将来使用这些导出变量，我们稍后会讨论将它们添加到 `/etc/openrc.admin` 文件中，你稍后将 source 该文件以执行管理功能。

现在你想运行 `token issue` 命令以确认它返回四行令牌数据，并运行 `user list` 命令，该命令将向你显示一个包含 admin 和 test 用户的表格（部分输出被截断）：

```bash
$ openstack token issue
+-------+---------------------------------------------+
| Field | Value                                       |
+-------+---------------------------------------------+
| expires | 2016-05-16T01:54:40.942971Z               |
| id | gAAAAAABXORpRX0OAPYr:fm5qIOwQ-b..   |
| project_id | 71e4a1286e1b466682238508349e94a4d |
| user_id | a335ce2e2e7e4e9a66595dda8aa61b351  |
+-------+---------------------------------------------+
```

```bash
$ openstack user list
+--------------------------------+-------+
| ID | Name                              |
+--------------------------------+-------+
| 8bf5e7aae64d9add7cfc450045df | test  |
| bc2d151a86394372a5fa4c50055f7a58 | admin |
+--------------------------------+-------+
```

如果这一切都成功运行，恭喜你！Keystone 已配置完毕。

