
这将安装 Puppet 以及用于运行 Puppet 代理守护进程的 init 脚本（`/etc/init.d/puppet`）。至此，我们完成了安装过程，但 Puppet 尚未启动。让我们现在配置主节点和代理节点，以便它们在需要时能够相互通信。此过程中的第一步是设置主节点的名称和证书。你需要一个能够解析名称到相应 IP 地址的 DNS 服务器，然后在主节点的 `puppet.conf` 文件的主配置部分，将 `dns_alt_names` 设置为主节点可能拥有的每个主机名的逗号分隔值。代理节点尝试连接的默认名称是 `puppet`。因此，如果你使用“puppet”作为主节点的主机名，将为你节省一些精力。这是最重要的一步之一，应谨慎操作，以避免后期出现通信问题。

### 04 激活证书

下一步是在主节点上激活证书。如果这是你部署中唯一的 Puppet 主节点，或者它将作为多主节点站点的 CA 服务器，你现在应该运行以下命令：

```bash
$ sudo puppet master --verbose --no-daemonize
```

这将创建 CA 证书和 Puppet 主节点证书，并包含适当的 DNS 名称。一旦终端输出显示：

> 注意：正在启动 Puppet 主节点版本 3.8.3。

...请通过按下 Ctrl+C 终止该进程，因为我们不希望主节点持续运行。现在，将所有 Puppet 清单和模块放置到位，如果你计划使用 Puppet 管理配置加载，请配置 Web 服务器。

### 05 配置代理

首先，你需要配置每个代理节点中的 `puppet.conf` 设置，以便它们能够连接到你的 Puppet 主节点服务器。此外，某些特定于环境因素应根据你的基础设施需求进行调整。然后，你需要启动 Puppet 代理服务。你可以将其配置为在启动时运行，或者设置一个计划任务（cron job），使其在特定间隔运行。要启动 Puppet 服务，请输入：

```bash
$ sudo puppet resource service <NAME>
ensure=running enable=true
```

然后使用以下命令配置计划任务：

```bash
$ sudo puppet resource cron puppet-agent \
ensure=present user=root minute=30 command=/usr/\
bin/puppet_agent --onetime --no-daemonize --play
```

最后一步是为每个代理节点签署证书。请注意，在代理/主节点部署中，管理员必须在节点获取配置之前批准每个代理节点的证书请求。代理节点在首次尝试运行时将请求证书。要批准请求，请登录到 Puppet 主节点服务器，并使用以下命令查看未处理的请求：

```bash
$ sudo puppet cert list
```

然后输入以下命令来签署请求：

```bash
$ sudo puppet cert sign <NAME>
```

你也可以使用以下命令一次性签署所有请求：

```bash
$ sudo puppet cert sign --all
```

至此，代理节点现在准备就绪，可以与主节点通信。Puppet 还通过允许你分类节点来实现更高水平的配置。通过这种方式，你可以决定哪些代理节点从主节点接收哪些信息。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_22_0.png)

![](img/0fc17bd4c29dc437e3ac28a53f7559db_22_1.png)

### 文件更新时运行

每当文件更改时，你可以自动运行命令。只需使用一个 `exec` 资源并将 `refreshonly` 设置为 `true`，例如：

```ruby
file { "/etc/bind":
  source => "/dist/apps/bind"
}

exec { "/usr/bin/ndc reload":
  subscribe => File["/etc/bind"],
  refreshonly => true
}
```

![](img/0fc17bd4c29dc437e3ac28a53f7559db_22_2.png)

## 功能

## DEVOPS

### 使用 VAGRANT 管理你的虚拟机

Vagrant 让你能够轻松地一次性管理多个虚拟机。在这里，我们将学习如何安装并开始使用 Vagrant。

在深入了解 Vagrant 能为你做什么之前，让我们先理解一下什么是 Vagrant。简单来说，Vagrant 提供了一个易于配置、可重复且便携的工作环境，构建在虚拟化技术之上。Vagrant 构建的工作环境可以由单个一致的工作流控制，以帮助最大化工效和灵活性。

为了实现其魔力，Vagrant 站在 VirtualBox、VMWare、AWS 或其他提供商等巨人的肩膀上。然后，你可以使用预配工具——如 shell 脚本、Chef 或 Puppet——在机器上自动安装和配置软件。因此，一旦你创建了一个 Vagrantfile，你只需要运行 `vagrant up`，一切都为你安装并配置好，供你使用。你团队的其他成员可以从相同的配置创建他们的开发环境，因此，无论你是在 Linux、OS X 还是 Windows 上工作，你团队的所有成员都在相同的环境中运行代码，针对相同的依赖项，所有配置方式都相同。

## 安装 Vagrant

Vagrant 可以轻松地在你的系统上下载和安装。前往 Vagrant 下载页面（`vagrantup.com/downloads.html`）并下载适合你系统的软件包。然后，你可以按照你平台的标准安装程序安装它。此外，安装程序会自动将 `vagrant` 命令添加到你的系统路径中，因此你现在可以开始使用它。如果你看到“命令未找到”错误，只需注销并重新登录，它应该就能正常工作。

## Vagrantfile

`Vagrantfile` 描述了项目所需的机器类型，以及如何配置和预配这些机器。请注意，该文件的实际文件名仅为 `Vagrantfile`。Vagrant 每个项目运行一个 `Vagrantfile`，并且 `Vagrantfile` 应该提交到版本控制。这使参与项目的其他开发人员可以签出代码，运行 `vagrant up` 并继续工作。`Vagrantfile` 在 Vagrant 支持的每个平台之间都是便携的。

## 环境变量

你可以在 `Vagrantfile` 中使用环境变量，方法是调用 `ENV[variable_name]`。例如：

```ruby
config.vm.box =
"#{ENV['boxname']}"
```

## VAGRANTFILE 解释
