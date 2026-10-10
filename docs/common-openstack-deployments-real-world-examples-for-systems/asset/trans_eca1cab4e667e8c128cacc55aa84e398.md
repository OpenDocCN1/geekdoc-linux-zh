

## 场景

正如我们在第 8 章中展示的那样，你现在可以为你的用户提供真正的持久化存储。这次，我们以对象的形式提供存储，而不是文件系统，因此这对于你希望从外部访问的一系列独立文件来说特别有价值。由于我们添加了一个额外的组件，需要再次使用 Puppet 进行一些设置以配置此存储。

**警告**
不要在未重新安装的情况下重用你第 7 章“公共计算云”或第 8 章中的系统，因为此示例将从你的安装中移除 Celiometer 或 Cinder 组件。

如果你希望一起运行所有这些服务，请参阅第 12 章，“完整的云”。

### 控制节点设置

使用你在第 5 章中可用的控制节点和计算节点，你只需要运行一条命令来添加对 Swift 对象存储的支持。此外，在此场景中，你只需要修改控制节点。无需对计算节点进行任何修改。

以下是将处理你的基础对象存储角色的 Puppet apply 命令：

```bash
sudo puppet apply /etc/puppet/modules/deployments/manifests/role/foundations_object_storage.pp
```

根据你的系统和网络速度，这需要一些时间，因为它会下载 Swift 所需的一切并设置配置。如果出现问题且此命令失败，也可以使用 --debug 标志运行 Puppet 以显示更多细节。

在此期间，我们可以探索一下这个 foundations_object_storage.pp 文件包含什么：

```puppet
class deployments::role::foundations_object_storage {
include deployments::role::foundations
include deployments::profile::swift
}
include deployments::role::foundations_object_storage
```

正如你之前所见，这是在调用我们的基础角色，以确保所有基本组件都已安装。这主要是为了安全起见，仍然建议你在遵循第 5 章中的步骤，以确保其无错误运行。然后它包含了 Swift 本身的配置文件，你可以在控制节点的 /etc/puppet/modules/deployments/manifests/profile/swift.pp 处查看，它包含以下内容：

```bash
cat /etc/puppet/modules/deployments/manifests/profile/swift.pp
```

```puppet
class deployments::profile::swift {
include ::memcached
include ::swift
include ::swift::keystone::auth
include ::swift::proxy
include ::swift::proxy::account_quotas
include ::swift::proxy::authcache
include ::swift::proxy::cache
include ::swift::proxy::catch_errors
include ::swift::proxy::container_quotas
include ::swift::proxy::formpost
include ::swift::proxy::healthcheck
include ::swift::proxy::keystone
include ::swift::proxy::proxy_logging
include ::swift::proxy::ratelimit
include ::swift::proxy::staticweb
include ::swift::proxy::tempurl
include ::swift::proxy::tempauth
include ::swift::ringbuilder
include ::swift::storage::all

$swift_components = ['account', 'container', 'object']
$swift::storage::filter::recon( $swift_components )
$swift::storage::filter::healthcheck( $swift_components )

file { '/srv/node':
ensure => directory,
owner => 'swift',
group => 'swift',
require => Package['swift'],
}

$loopback_devices = hiera('swift_ring_loopback_devices', [])
if ! empty($loopback_devices) {
 create_resources('swift::storage::loopback', $loopback_devices)
}

$object_devices = hiera('swift_ring_object_devices', [])
if ! empty($object_devices) {
 create_resources('swift::storage::object', $object_devices)
}

$container_devices = hiera('swift_ring_container_devices', [])
if ! empty($container_devices) {
 create_resources('swift::storage::container', $container_devices)
}

$account_devices = hiera('swift_ring_account_devices', [])
if ! empty($account_devices) {
 create_resources('swift::storage::account', $account_devices)
}
```

如你所见，我们引入了相当多的内容，然后进行了一些 Swift 使用本地存储点存储我们将添加的对象所需的配置。我们引入了 memcached，它用于缓存特定类型的查找，例如身份验证令牌以及你引用的容器或账户是否存在。它不用于缓存对象本身。与其他服务一样，我们将使用 Keystone 进行身份验证，因此我们需要确保包含 Keystone 支持。在我们的部署中，我们还引入了所有存储机制（storage::all），以便你可以使用它们，但请注意，我们在此部署示例中使用了一系列三个 XFS 环回设备。

我们还引入了各种代理清单。逐一查看，你有：

- account_quotas—提供设置账户配额的功能（Swift “账户”对应于 Keystone “项目”，也称为“租户”）。请注意，账户本身是 Keystone 的一部分。
- authcache—身份验证的标准令牌支持。
- cache—使用 memcached 支持特定类型查找的缓存。
- catch_errors—捕获代理管道中发生的错误并将其转换为相应的错误报告。
- container_quotas—提供在特定容器上设置配额的功能。
- formpost—支持使用 HTML 表单 POST 上传对象。
- healthcheck—一个用于监控 Swift 代理服务器是否存活的简单工具，也用于向负载均衡器添加多个代理时。
- keystoneauth—用于管理 Swift 代理的 keystone 中间件。
- proxy_logging—为向代理服务器发出的所有外部 API 请求提供自定义日志记录。
- ratelimit—支持账户和容器的速率限制，以防止单个账户在集群中使用过多的资源。
- staticweb—支持 Swift 静态 Web 中间件以创建静态网站。
- tempurl—支持对象的临时访问。
- tempauth—参考中间件以创建自定义身份验证组件。这绝不应该在生产环境中使用，但对于开发和测试很有用。

Swift 的 Puppet 配置文件的最后一部分设置了将用于存储我们为容器创建的对象 XFS 环回设备（1-3）。

最后，Rings 在章的前面已经讨论过，通过调用 Swift ring-builder 清单，我们可以管理这些 Rings。

> **警告**
> 我们的部署场景只是一个示例，并不具备使其适合生产环境的特征。因此，我们使用该模块配置 Rings 的方式也不适合生产环境，因此在为实际部署配置此内容时要小心谨慎。如果 Puppet Swift 模块未正确使用，每个主机上的 rings 将不同，并且数据持久性存在高风险。

在撰写本文时，Swift 团队的成员正提议对 Puppet 模块进行架构更改。这将使该模块更容易使用且更准确，并有助于保护操作者免受错误配置的影响。Puppet 配置在未来可能会有重大变化。

在许多部署中，而不是使用 Puppet 模块，Rings 通常是手动构建的，然后复制到所有节点。这比我们在本章中能够提供的深入使用 ring-builder 而非 Puppet 模块需要更深入的了解，但这可能是你部署的更好选择。

在准备你自己的部署时，也务必回顾本章前面的“关键概念”部分，并对你需要做出的存储决策进行更深入的调研。

现在让我们回到你运行的 Puppet 命令。一旦此命令完成，你就可以开始向对象存储添加文件并共享它们了。

### 创建容器和对象：仪表板

为了使用 Swift 对象存储，你首先需要创建一个容器来容纳你的对象。这是在 Horizon 仪表板中完成的，通过你的测试用户登录并导航到左侧菜单中的对象存储。

在此屏幕上，点击标有“Container”并带有加号图标的按钮，这将带你进入如图 9.3 所示的“创建容器”屏幕。

![](img/8684900d708748f86bb043faa5589f9e_205_0.png)

图 9.3 Swift 中的“创建容器”屏幕

