
- “Debian 每日软件包”天气文章提供了关于使用 `weatherutility` 的更多细节。

## Puppet

Puppet 是一个跨平台框架，允许系统管理员使用代码执行常见任务。代码可以完成各种任务，从安装新软件到检查文件权限，或更新用户账户。Puppet 不仅在系统初始安装期间非常出色，在系统的整个生命周期内也同样适用。在大多数情况下，puppet 将以客户端/服务器配置使用。

本节将介绍如何在客户端/服务器配置中安装和配置 Puppet。这个简单的示例将演示如何使用 Puppet 安装 Apache。

### 配置

在配置 puppet 之前，你可能想为 `puppet.example.com` 添加 DNS CNAME 记录，其中 `example.com` 是你的域名。默认情况下，Puppet 客户端会检查 DNS `puppet.example.com` 作为 Puppet 服务器名称或 Puppet Master。更多信息请参阅域名服务器。

如果你不想使用 DNS，可以向服务器的 `/etc/hosts` 文件添加条目。例如，如果 Puppet 服务器的 `/etc/hosts` 文件添加：

```
127.0.0.1 localhost.localdomain localhost puppet
192.168.1.17 puppetclient .example.com puppetclient
```

在每个 Puppet 客户端上，为服务器添加条目：

```
192.168.1.16 puppetmaster .example.com puppetmaster puppet
```

### 注意事项

将上述 IP 地址和域名替换为你实际的服务器和客户端地址以及域名。

### 安装

要安装 Puppet，在服务器的终端中输入：

```bash
sudo apt install puppetmaster
```

在客户端机器或机器上，输入：

```bash
sudo apt install puppet
```

### 配置

为 `apache2` 类创建一个文件夹路径：

```bash
sudo mkdir -p /etc/puppet/modules/apache2/manifests/init.pp
```

现在为 `apache2` 设置一些资源。创建文件 `/etc/puppet/modules/apache2/manifests/init.pp` 并包含以下内容：

```bash
class apache2 {
  package `apache2` {
    ensure => installed
  }
  service `apache2` {
    ensure => true,
    enable => true,
    require => Package['apache2'],
  }
}
```

接下来，创建一个节点文件 `/etc/puppet/code/environments/production/manifests/site.pp` 内容如下：

```bash
node `puppetclient.example.com` {
  include apache2
}
```

### 注意事项

将 `puppetclient.example.com` 替换为你实际 Puppet 客户端的主机名。

简单 Puppet 服务器的最后一步是重启守护进程：

```bash
sudo systemctl restart puppetmaster.service
```

现在 Puppet 服务器上的所有配置已完成，是时候配置客户端了。

首先，配置 Puppet agent 守护进程启动。编辑 `/etc/default/puppet`，将 START 修改为 yes：`START=yes` 

然后启动服务：

```bash
sudo systemctl start puppet.service
```

查看客户端状态

`sudo puppet agent --test`

回到 Puppet 服务器，查看证书签名请求：

`sudo cert list`

在 Puppet 服务器上，验证客户端状态并签名客户端证书：

`sudo cert sign puppetclient.example.com`

Puppet 客户端手动在前台运行 agent。此步骤并非严格必要，但仍是测试和调试服务的最佳方法

`sudo puppet agent --test`

检查所有主机上的 `/var/log/syslog` 是否有配置的任何错误。如果一切顺利，`apache2` 包及其依赖项将安装在客户端上。

### 注意事项

此示例非常简单，没有突出 Puppet 的许多功能和优势。更多信息请参阅资源。

### 资源

- 查看官方文档网站。
- 查看 Puppet forge 模块在线仓库。
- 另请参见 Puppet。

## 监控

### 概述

对基本服务器和服务的监控是为了性能、可用性或两者。本节将介绍用于可用性监控的 Nagios 和用于性能监控的 Munin 的安装和配置。

本节中的示例将使用两个主机名为 `server01` 和 `server02` 的服务器。`server01` 将配置 Nagios 来监控自己，`server02` 也将配置 Munin 来监控自己。

### Nagios

#### 安装

首先，在 `server01` 上安装插件：

```bash
sudo apt install nagios
```

在 `server02` 上安装对应的ios：

```bash
sudo apt install nagios-utils
```

在 `server01` 上安装 `nagios-common` 软件包：

```bash
sudo apt install nagios-common
```

在 `server02` 上安装 `nagios-common` 软件包：

```bash
sudo apt install nagios-common
```

在 `server01` 上安装 `nagios-plugins`：

```bash
sudo apt install nagios-plugins
```

在 `server02` 上安装 `nagios-plugins`：

```bash
sudo apt install nagios-plugins
```

#### 配置

Nagios 目录 `/etc/nagios3` 包含以下目录：

- `/etc/nagios3/`: 配置文件。
- `/var/lib/nagios3/`: 存储 Nagios 状态的文件。
- `/var/log/nagios3/`: 日志文件。
- `/usr/lib/nagios3/plugins/`: 插件文件。

编辑 `/etc/nagios3/objects.cfg` 以定义主机：

```
define host localhost {
    use generic-host
    host_name localhost
    alias Localhost
    address 127.0.0.1
}
```

通常情况下，我们需要在 `/etc/nagios3/objects.cfg` 中定义 `server01` 和 `server02`。

在 `/etc/nagios3/objects.cfg` 中添加：

```
define host server01 {
    use generic-host
    host_name server01
    alias Server 01
    address 192.168.1.16
}
```

在 `/etc/nagios3/objects.cfg` 中添加：

```
define host server02 {
    use generic-host
    host_name server02
    alias Server 02
    address 192.168.1.17
}
```

编辑 `/etc/nagios3/objects.cfg` 以定义服务：

```bash
define service http {
    use generic-service
    host_name localhost
    service_description HTTP
    check_command check_http!127.0.0.1
}
```

在 `/etc/nagios3/objects.cfg` 中添加：

```bash
define service http {
    use generic-service
    host_name server01
    service_description HTTP
    check_command check_http!192.168.1.16
}
```
