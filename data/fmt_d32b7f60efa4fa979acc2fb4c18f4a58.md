
$ sudo firewall-cmd --reload

## 验证配置

列出 `public` 区域的规则以验证配置：

```
$ sudo firewall-cmd --zone=public --list-all
```

以下是示例输出：
`public (active)`
`target: default`
`icmp-block-inversion: no`
`interfaces: eth0`
`sources:`
`services: dhcpv6-client http https ssh`
`ports:`
`protocols:`
`masquerade: no`
`forward-ports:`
`source-ports:`
`icmp-blocks:`
`rich rules:`

## 示例程序：AlphaProject 的防火墙配置

我们将为 `AlphaProject` 实现一个更好、更全面的防火墙配置，涵盖了 `iptables` 和。

## 为 AlphaProject 配置

- 允许入站的 SSH、HTTP 和 HTTPS 流量
```
$ sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
$ sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
$ sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

- 允许已建立和相关的连接
```
$ sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

- 允许回环流量
```
$ sudo iptables -A INPUT -i lo -j ACCEPT
```

- 记录并丢弃其他入站流量
```
$ sudo iptables -A INPUT -j LOG --log-prefix "iptables-dropped: "
$ sudo iptables -A INPUT -j DROP
```

默认情况下，`iptables` 允许所有出站流量。通过以下命令确保这一点：
```
$ sudo iptables -P OUTPUT ACCEPT
```

## 保存配置
```
$ sudo iptables-save > /etc/iptables/rules.v4
```

## 启动并启用 firewalld

```
$ sudo systemctl start firewalld
```

```
$ sudo systemctl enable firewalld
```

将默认区域设置为：

```
$ sudo firewall-cmd --set-default-zone=public
```

## 将接口分配到公共区域

```
$ sudo firewall-cmd --zone=public --change-interface=eth0 --permanent
```

## 允许 SSH、HTTP 和 HTTPS 服务

```
$ sudo firewall-cmd --zone=public --add-service=ssh --permanent
```

```
$ sudo firewall-cmd --zone=public --add-service=http --permanent
```

```
$ sudo firewall-cmd --zone=public --add-service=https --permanent
```

添加一条规则允许已建立和相关的连接：

```
$ sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" service name="ssh" accept --permanent
```

```
$ sudo firewall-cmd --zone=public --add-rich-rule=rule family="ipv4" service name="http" accept --permanent
```

```
$ sudo firewall-cmd --zone=public --add-rich-rule=rule family="ipv4" service name="https" accept --permanent
```

添加一条规则允许丢弃其他入站流量：

```
$ sudo firewall-cmd --zone=public --add-rich-rule=rule family="ipv4" log prefix="firewalld-dropped: " level="info" drop --permanent
```

默认情况下，`firewalld` 允许所有出站流量。验证此配置：

```
$ sudo firewall-cmd --zone=public --list-all
```

重载防火墙规则以应用更改：

```
$ sudo firewall-cmd --reload
```

列出 `public` 区域的规则以验证配置：

```
$ sudo firewall-cmd --zone=public --list-all
```

以下是示例输出：

`public (active)`

```
target: default
icmp-block-inversion: no
interfaces: eth0
sources:
services: ssh http
ports:
protocols:
```

`masquerade: no`
`forward-ports:`
`source-ports:`
`icmp-blocks:`
`rich rules:`
`rule family="ipv4" service name="ssh" accept`
`rule family="ipv4" service name="http" accept`
`rule family="ipv4" service name="https" accept`
`rule family="ipv4" log prefix="firewall-dropped: " level="info" drop`

如果你按照上述步骤操作，你就可以设置防火墙。

## AppArmor 简介

`AppArmor` 是一种 Linux 安全模块 (`LSM`)，它通过使用配置文件（`profiles`）来限制对文件、目录、网络套接字的访问，从而提供一种限制程序的机制。

## AppArmor 的主要用途

- 定义角色并为用户分配权限。
- 限制虚拟机可以的资源。
- 使用可插认证模块 (`PAM`) 增强安全性。

## 安装和启用 AppArmor

在使用 `AppArmor` 之前，确保它已安装并启用。

### 安装 AppArmor

在 Ubuntu 上，你可以使用以下命令安装 `AppArmor`：

```
$ sudo apt update
$ sudo apt install apparmor apparmor-utils
```

### 启用 AppArmor

确保 `AppArmor` 已启用并运行：

```
$ sudo systemctl enable apparmor
$ sudo systemctl start apparmor
```

验证 `AppArmor` 状态：

```
$ sudo apparmor_status
```

`apparmor module is loaded.`
`40 profiles are loaded.`
`40 profiles are in enforce mode.`
`0 profiles are in complain mode.`
`2 processes have profiles defined.`
`2 processes are in enforce mode.`
`0 processes are in complain mode.`
`0 processes are unconfined.`

## 定义策略

策略 定义了应用程序的安全策略。这些策略可以手动创建，也可以使用提供的工具生成。

## 为特定应用程序创建配置文件

我们将为一个示例程序创建一个配置文件。首先，找到应用程序二进制文件：

```
$ which example-app
```

假设应用程序位于，为它创建一个配置文件：

```
$ sudo aa-genprof /usr/bin/example-app
```

此命令将启动 `AppArmor` 配置模式，你可以在其中定义策略。

### 定义配置文件

运行应用程序以生成日志项：

```
$ sudo /usr/bin/example-app
```

`AppArmor` 将监控应用程序的行为并生成配置条目。运行程序后，完成配置生成：

```
$ sudo aa-logprof
```

按照提示定义应用程序的权限。完成后，配置将被强制执行。

## 强制执行配置

确保配置已强制执行：

```
$ sudo aa-enforce /etc/apparmor.d/usr.bin.example-app
```

验证配置状态：
