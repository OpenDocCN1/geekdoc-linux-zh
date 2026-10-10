
> 请注意更新密码。请记住，这些默认身份验证凭据存在于一个完全公开的 `git` 存储库中。

完成这些更改后，我们终于可以运行命令来应用 `Puppet` 清单，为您安装基础组件。

```
sudo puppet apply /etc/puppet/modules/deployments/manifests/role/foundations.pp
```

此命令可能需要一些时间才能运行。在它运行期间，您将看到大量描述 `Puppet` 正在做什么的输出。

## 再次运行 `puppet apply`

`puppet apply` 命令可以运行多次。如果您需要为某个设置修改 `Hiera common.yaml`，或者在运行过程中遇到了互联网连接中断或其他错误等问题，您可能需要再次运行它。

虽然这种情况不应发生，但如果您确实遇到导致部署场景失败错误，可以使用 `--debug` 标志以调试模式运行 `Puppet` 命令。这将提供更详细的输出，有助于您确定出了什么问题。

使用该标志后，您的命令将变为：

```
sudo puppet apply --debug /etc/puppet/modules/deployments/manifests/role/foundations.pp
```

这将产生大量输出。您可以使用管道和 `tee` 将输出重定向到文件，同时也将其显示在标准输出（`STDOUT`）中：

```
sudo puppet apply --debug \
  /etc/puppet/modules/deployments/manifests/role/foundations.pp | \
  tee ~/puppet_apply_foundations.log
```

这将在您的主目录中创建一个 `puppet_apply_foundations.log` 文件，供您稍后查阅。

在运行期间，请查看 `foundations.pp` `Puppet` 角色中包含的内容：

```
$ cat /etc/puppet/modules/deployments/manifests/role/foundations.pp
class deployments::role::foundations {
 include deployments::profile::base
 include deployments::profile::glance
 include deployments::profile::horizon
 include deployments::profile::keystone
 include deployments::profile::nova
 include deployments::profile::neutron
 include deployments::profile::rabbitmq
 include ::mysql::server
}

include deployments::role::foundations
```

表面上看这非常简单，但我们将深入探讨一下以解释它是如何工作的。

## `Puppet` 角色、配置文件和模块

`OpenStack Puppet` 社区维护了一系列用于部署 `OpenStack` 的开源 `Puppet` 模块，本书也使用了这些模块。模块是共享的配置工具，其通用程度足以供各类组织和企业共享。它们作为一系列构建模块被加载到我们的部署中，以创建您想要的部署场景。我们还使用了一个托管在 `GitHub` 上的高层“`deployments`”模块，其中包含我们的角色和配置文件。

我们使用 `Puppet` 角色和配置文件来组织 `OpenStack Puppet` 模块的 `Puppet` 配置。通过使用角色和配置文件，我们可以创建一系列文件，这些文件定义了包含类似配置文件所定义内容的特定服务器（角色），本质上是将模块粘合在一起。正如您在 `foundations.pp` 中看到的，它包含了像“`base`”这样的配置文件，我们将把所有场景都用到。

您可以通过查看它们在配置中如何被包含来区分我们 `deployments` 模块内部的角色和配置文件与其他模块中的角色和配置文件。然而，角色和配置文件之间的区别不仅仅是名称上的不同。角色是封装配置文件的“业务逻辑”定义。配置文件是封装模块的实现定义。

我们 `deployments` 模块中的角色声明看起来像这样：

```
include deployments::role::foundations
```

您会在 `foundations.pp` 中看到包含此角色。角色的 `puppet` 文件包含自身以使其更易于使用。

配置文件声明类似，但使用 `deployments::profile` 前缀：

```
include deployments::profile::uca
```

最后，当调用我们 `deployments` 模块之外的模块（或模块的组件）时，您会看到类似以下内容：

```
include ::openstacklib::openstackclient
```

要了解有关角色、配置文件和模块的更多信息，请访问官方 `Puppet` 文档 `https://docs.puppet.com/`。关于它们还撰写了许多有价值的文章和博客帖子。由于它们很快就会过时，请使用您喜欢的搜索引擎查找最新信息。

## 配置文件

每个配置文件配置您 `OpenStack` 部署的不同组件，您可以深入研究每一个以了解其配置内容。

## 基础配置文件

基础配置文件在所有我们的部署中共享。

```
$ cat /etc/puppet/modules/deployments/manifests/profile/base.pp
class deployments::profile::base {
include deployments::profile::openrc
include deployments::profile::ucc
include ::ntp
include ::openstacklib::openstackclient
# add an alias to /etc/hosts to ensure sudo works
host { ${::hostbase}:
ip => $::ipaddress,
}
}
```

它设置了我们稍后将在本章中使用来运行 `OpenStack` 客户端命令的 `openrc` 文件。我们添加了网络时间协议（`NTP`）配置，以确保系统中的时间保持同步，并且还包括安装 `OpenStack` 客户端。`UCA` 配置文件配置了 `Ubuntu Cloud Archive`（`UCA`）。如第 1 章所述，我们使用 `UCA` 是为了获取最新的 `OpenStack` 发行版本 `Mitaka`，对应于我们正在运行的 `Ubuntu` 长期支持版本 `14.04`。深入挖掘此配置文件，您会发现有一个部分定义了 `$release`。这是从 `Hiera common.yaml` 文件中获取的，并将该值设置为 `mitaka`。

```
$ cat /etc/puppet/modules/deployments/manifests/profile/uca.pp
## Ubuntu Cloud Archive
class deployments::profile::uca {
$release,
$repo,
{
include ::apt
class { '::openstack_extras'::repo::debian:ubuntu':
release => $release,
repo    => $repo,
package_require => true,
}
Apt::Source{ | -> Package <|}
}
```

最后包含的部分是 `OpenStack` 客户端（`OSC`），我们将其安装在所有系统上，这样您可以在任何所在的系统上运行 `OSC` 命令，以及的 `OpenRC` 凭据。这是一个名为 `openstacklib` 的外部模块，它不属于我们的 `deployments`（部署）模块。

## `Glance` 配置

`Glance`（镜像服务）的配置是你可以开始看到非常有趣的配置选项的地方：

```
$ cat /etc/puppet/modules/deployments/manifests/profile/glance.pp

class deployments::profile::glance {
  $cirros_version = '0.3.4',
}
{
  include ::glance
  include ::glance::api
  include ::glance::registry
  include ::glance::keystone::auth
  include ::glance::backend::file
  include ::glance::db::mysql
  include ::glance::notify::rabbitmq

  glance_image { 'cirros':
    location  => "https://download.cirros-cloud.net/5/${cirros_version}/${cirros_version}-x86_64-disk.img",
    name      => "CirrOS ${cirros_version}",
    is_public => 'Yes',
    container_format => 'bare',
    disk_format => 'qcow2',
  }
}
```

这会调用 `OpenStack Glance` 模块以拉入各种组件。在我们的配置中，我们做出了关于如何让此基本配置工作的几项决定。我们正在拉入 `Glance` 的 `API` 和 `Registry`。然后，我们确保为 `Glance` 设置好 `Keystone` 和 `MySQL`，以便与我们现有的 `Keystone` 和 `MySQL` 服务进行交互。`Puppet` 让这变得非常容易，但如果你想复习一下，可以在第 4 章中看到它是如何手动完成的。最后，我们还在使用存储后端“`file`”，这是 `Glance` 的默认后端类型，意味着它将在文件系统中存储镜像。默认情况下，它们存储在 `/var/lib/glance/images/`，这就是你将在其中找到你上传到 `Glance` 的镜像的地方。`Glance` 可以使用不同的后端选项，如 `OpenStack` 对象存储服务（`Swift`）或亚马逊的 `S3`。在安装中，我们配置了单个镜像，一个非常小且简单的基于 `Linux` 的操作系统，称为 `CirrOS`。如你所见，此配置定义了将使用哪个版本的 `CirrOS` 作为我们 `Glance` 中的初始镜像，以及关于它的各种详细信息。

如果你对在 `Mitaka` 版本中 `OpenStack Glance` 模块的更多细节感兴趣，你可以在节点文件系统或在线浏览它：

- **文件系统**——`/etc/puppet/modules/glance/`

- **在线**——`https://git.openstack.org/cgit/openstack/puppet-glance/tree/?h=stable%2Fmitaka`

## `Horizon` 配置

`Horizon` 仪表板配置非常简单，因为不需要上游 `Puppet` 模块之外的特殊代码即可让仪表板运行。

```
$ cat /etc/puppet/modules/deployments/manifests/profile/horizon.pp

class deployments::profile::horizon
{
    include ::apache
    include ::horizon
}
```

它运行 `Apache`，因此我们正在拉入一个通用的 `Apache` 模块，并且它还需要 `OpenStack Horizon` 模块。

如果你对在 `Mitaka` 版本中 `OpenStack Horizon` 模块的更多细节感兴趣，你可以在节点文件系统或在线浏览它：

- **文件系统**——`/etc/puppet/modules/horizon/`

- **在线**——`https://git.openstack.org/cgit/openstack/puppet-horizon/tree/?h=stable%2Fmitaka`

## `Keystone` 配置

随着 `Keystone` 身份配置，我们又变得复杂起来。

```
$ cat /etc/puppet/modules/deployments/manifests/profile/keystone.pp

class deployments::profile::keystone
{
    include ::apache
    include deployments::profile::users
    include ::keystone
    include ::keystone::cron::token_flush
    include ::keystone::roles::admin
    include ::keystone::endpoint
    include ::keystone::db::mysql
    include ::keystone::apache
}
```

由于 `Keystone` 使用 `WSGI` 来运行服务，它也需要 `Apache` 模块以及特定的 `keystone::wsgi::apache` 类。此外，它拉入了 `Keystone Puppet` 模块的多个其他组件，包括 `cron` 作业、管理角色信息以及端点的配置。最后，你编辑了 `hiera/common.yaml` 来更改 `admin` 和 `test` 用户的密码，这定义了“`deployments::profile::users`”所带来的内容。

> **注意**

> 在第 4 章中，你可能记得我们使用 `Fernet` 令牌配置了 `Keystone`。这是社区推荐正在发展的趋势，并且在我们手动部署中很容易实现。然而，对 `Fernet` 令牌的支持是相对较新出现的，在 `Kilo` 版本中。在 `OpenStack` 中它还不是默认选项。对于我们的 `Puppet` 驱动的部署场景，我们仍然使用当前默认的 `UUID` 令牌。

如果你对在 `Mitaka` 版本中 `OpenStack Keystone` 模块的更多细节感兴趣，你可以在节点文件系统或在线浏览它：

- **文件系统**——`/etc/puppet/modules/keystone/`

- **在线**——`https://git.openstack.org/cgit/openstack/puppet-keystone/tree/?h=stable%2Fmitaka`

## `Nova` 配置

`Nova` 计算控制器配置较长，但相当直接明了。

```
$ cat: /etc/puppet/modules/deployments/manifests/profile/nova.pp
class deployments::profile::nova
{
  include ::nova
  include ::nova::api
  include ::nova::db::mysql
  include ::nova::db::mysql_api
  include ::nova::conductor
  include ::nova::consoleauth
  include ::nova::keystone::auth
  include ::nova::network::neutron
  include ::nova::rabbitmq
  include ::nova::scheduler
  include ::nova::scheduler::filter
  include ::nova::vncproxy

  $nova_deps = ['websockify']
  package { $nova_deps:
    ensure  => 'latest',
    before  => Service['nova-novncproxy']
  }
}
```

它拉入了运行控制器节点上管理计算的服务的后端工作所需的各种控制器特定组件。你稍后会看到，这与我们在计算节点上安装的内容不同。它还处理了 `websockify` 的依赖问题，该问题在出版时未解决。

如果你对在 `Mitaka` 版本中 `OpenStack Nova` 模块的更多细节感兴趣，你可以在节点文件系统或在线浏览它：

- **文件系统**——`/etc/puppet/modules/nova/`

- **在线**——`https://git.openstack.org/cgit/openstack/puppet-nova/tree/?h=stable%2Fmitaka`

## `Neutron` 配置

`Neutron` 网络配置有几个基本组件，但也有几个部分需要仔细检查。
