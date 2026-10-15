
# 图 5.29：确认 SSH 软件包安装

此图展示了在 Rocky Linux 上确认 SSH 软件包安装的过程。确保安装了必要的 SSH 软件包（如 `openssh-server` 和 `openssh-clients`）是启用 SSH 远程管理的关键步骤。通过使用命令 `rpm -q openssh-server`，管理员可以验证 SSH 服务器的状态。如果软件包未安装，可以使用包管理器（`dnf`）轻松添加。确认这些软件包已正确安装，可以确保系统已准备好进行远程访问。

- `openssh-server`：用于启用系统上的 SSH 服务功能所必需。
- `openssh-clients`：为 SSH 客户端操作提供工具，例如连接到远程服务器。

## 步骤 2：启动并启用 SSH 服务

为了确保 SSH 服务持续运行并在开机时启动，请使用以下命令：

```bash
sudo systemctl start sshd
sudo systemctl enable sshd
```

```
[casermerver@localhost ~]$ sudo systemctl start sshd
[casermerver@localhost ~]$ sudo systemctl enable sshd
```

# 图 5.30：启动并启用 SSH 服务

此图说明了在 Rocky Linux 上启动和启用 SSH 服务的过程。安装必要的 SSH 软件包后，必须启动 SSH 服务以启用远程访问。使用 `systemctl start sshd` 命令，管理员可以启动 SSH 服务，并通过 `systemctl enable` 使其在开机时自动启动。启用 SSH 开机启动可确保系统在每次重启时都可以进行远程访问，从而对服务器提供一致且安全的管理。

验证服务状态：`sudo systemctl status sshd`。

```
[cesarserver@localhost ~1] sudo systemctl status sshd
● sshd.service - OpenSSH server daemon
   ├ Active: active (running) since Sun 2024-12-15 28:21:02 CST; 2h 25min ago
   ├ Main PID: 963 (running)
   ├ Tasks: /etc/ssh/sshd_config
   ├ Memory: 7.1M
   └ CPU: 0ms
   └ ControlGroup: /system.slice/sshd.service [listener 0 of 10-100 stars]
```

```
Dec 15 20:01:02 localhost. sshd[963]: Server listening on 0.0.0.0:port 22
Dec 15 20:01:02 localhost. sshd[963]: Server listening on *:port 22
Dec 15 20:01:02 localhost. sshd[963]: Started OpenSSH server daemon.
Dec 15 20:21:05 localhost. sshd[1986]: Accepted password for cesarserver from 192.168.204.1 port 51835
Dec 15 20:21:05 localhost. sshd[1986]: Session opened for user cesarserver by tcp 192.168.204.1:51835
Dec 15 20:21:05 localhost. sshd[1986]: Session opened for user cesarserver (uid=0)
```

# 图 5.31：验证 SSH 服务状态

此图演示了如何在 Rocky Linux 上确认 SSH 服务的状态。验证对于确保远程访问可用至关重要。通过使用 `systemctl status sshd` 命令，管理员可以检查 SSH 服务是活动状态、非活动状态还是遇到了任何问题。定期确认 SSH 状态有助于确保可靠的远程管理，并在出现连接问题时协助诊断。

## 步骤 3：测试 SSH 访问

在客户端系统中，使用 `ssh` 命令连接到服务器：

`ssh username@server_ip_address`

- a. 将 `username` 替换为服务器用户名。
- b. 将 `server_ip_address` 替换为服务器的 IP 地址或主机名。

在提示时输入密码以确保连接。身份验证成功后将获得服务器的 shell 访问。

# 安全 SSH Access

在修改 Rocky Linux 的 SSH 配置文件之前，最佳实践是创建当前配置的备份。以下是实现此操作的步骤：

1. **创建 SSH 配置备份**：运行以下命令将 `sshd_config` 文件复制到备份文件：
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```

2. **编辑 SSH 配置**：使用编辑器打开文件并修改必要的设置。

- **更改 SSH 端口**：找到 `Port` 指令并将值更改为非标准端口（例如 2222）。
- **禁用 Root 登录**：找到 `PermitRootLogin` 指令并将其设置为 `no`。

3. **重启 SSH 服务**：做出更改后，重启服务以应用更改：
```bash
sudo systemctl restart sshd
```

这是一个多功能且可靠的环境，用于练习和管理 SSH 配置。专注于基于密钥的身份验证并实施高级安全实践，可以增强远程访问设置的安全性和效率，确保对未经授权的访问提供强力保护。

# AWS 中的网络

在本节中，我们将详细介绍亚马逊云服务（AWS）网络的基础知识，并展示如何在 Rocky Linux 实例上配置和管理网络。网络是构建云基础设施中最重要的部分之一，因为它允许我们的应用程序进行安全且高效的通信。

无论我们是托管一个简单的 Web 服务器，还是在多个环境中构建复杂的应用程序，理解 AWS 网络以及它如何与 Rocky Linux 集成，都将帮助我们部署可扩展、安全且高性能的云系统。

## AWS 网络基础知识

让我们从 AWS 网络的关键组件开始：

- 虚拟私有云 (VPC)：云中的私有网络，允许 Linux 管理员安全地部署和管理资源。
- 子网 (Subnets)：VPC 内部划分，用于组织和隔离资源。
- 路由表 (Route Tables)：定义流量在子网之间以及到互联网的移动方式。
- 互联网网关 (IGW)：允许公共子网中的资源访问互联网。
- 安全组 (SGs)：EC2 实例的虚拟防火墙。
  - 根据特定规则控制入站和出站流量。
  - 默认配置允许所有出站流量并阻止所有入站流量。
- 弹性网络接口 (ENIs)：挂载在 EC2 实例上的虚拟网络适配器。
  - 支持多个 IP 地址和安全组。
  - 用于高可用设置和故障备转移。
- 弹性 IP 地址 (Elastic IP Addresses)：静态公共 IP 地址，即使实例重启，地址也会保持不变。
  - 对于需要一致公共 IP 地址的资源有用。

## AWS 网络概念

亚马逊云服务（AWS）网络对于在云中部署 Rocky Linux 至关重要。关键组件包括：

- 虚拟私有云 (VPC)：逻辑上隔离的网络。例如，一个 CIDR 为 10.0.0.0/16 的 VPC 托管了 Web 服务器。
- 子网：VPC 的细分，例如用于负载均衡器的公共子网 (10.0.1.0/24) 和用于数据库的私有子网 (10.0.2.0/24)。
- 弹性 IP：分配给实例的静态公共 IP，确保访问的一性。
- 安全组：控制实例流量的虚拟防火墙。例如，允许 HTTP (端口 80) 和 SSH (端口 22)。
- VPC 对等 (VPC Peering)：允许两个 VPC 之间的无缝通信，例如将生产 VPC 与开发 VPC 链接。

```bash
# 查看安全组规则
aws ec2 describe-security-groups --group-ids sg-1234567890
```

```bash
# 添加 SSH 规则
aws ec2 authorize-security-group-ingress --group-id sg-1234567890
--protocol tcp --port 22 --cidr 0.0.0.0/0
```
