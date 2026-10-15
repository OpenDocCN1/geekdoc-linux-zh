
- 创建具有 sudo 权限的非 root 用户：`sudo adduser admin`; `sudo usermod -G wheel admin`

- 重启 SSH 服务：`systemctl restart sshd`

### 3. 验证部署

a. 运行系统更新

b. 查看系统日志：`journalctl -xe`; `cat /var/log/messages`

# 实验 2：AWS 与 Azure 之间的混合云网络

**目标：** 在 AWS 和 Azure 的 Rocky Linux 实例之间建立安全通信通道。

步骤

1. 设置 IPSec VPN 隧道

    a. 在 AWS 和 Azure 上部署 VPN 网关。

    b. 配置两个云之间的点对点 VPN 连接。

2. 安全密钥交换

    a. 生成实例间认证的 SSH 密钥对：

```
ssh-keygen -t rsa -b 4096 -C "admin@rockylinux"
```

    b. 部署 AWS Secrets Manager 以安全存储和检索私钥。

# 实验 3：在 AWS Rocky Linux 上部署容器

**目标：** 在 AWS Rocky Linux 上部署和管理 Docker 容器。

步骤

1. 安装 Docker

    * 安装 Docker：`sudo dnf install -y docker`

    * 启动并启用 Docker：`sudo systemctl start docker`; `sudo systemctl enable docker`

    * 验证安装：`docker --version`

2. 部署 Web 应用容器

    * 拉并运行示例 Nginx 容器：`docker pull nginx`; `docker run -d -p 80:80 nginx`

    * 通过公共 IP 确认访问。

3. 使用 AWS ELB 设置负载均衡

    * 部署负载均衡器（ELB）。

    * 注册运行 Nginx 的 Rocky Linux 实例。

    * 配置自动扩展以管理工作负载。

# 实验 4：实现集中日志与监控

**目标：** 配置 Prometheus 和 Grafana 以监控 AWS 中的 Rocky Linux 实例。

步骤

1. 安装 Prometheus

a. 下载并安装 Prometheus：`sudo dnf install -y prometheus`

b. 配置 Prometheus 以监控系统指标。

2. 部署 Grafana

   a. 安装 Grafana：`sudo dnf install -y grafana`

   b. 配置 Grafana 获取 Prometheus 指标。

   c. 设置仪表板以监控 CPU、内存和网络活动。

3. 启用 AWS CloudWatch 日志

   a. 安装并配置 AWS CloudWatch Agent。

   b. 创建日志组并定义保留策略。

# 实验 5：使用 Ansible 实现部署自动化

**目标：** 使用 Ansible 自动化 Rocky Linux 实例配置和软件包安装。

步骤

1. 安装 Ansible

   a. 安装 Ansible：`sudo dnf install -y ansible`

   b. 验证安装：`ansible --version`

2. 创建 Ansible 文件

   a. 在 `/etc/ansible/hosts` 中定义 Rocky Linux 实例：

```
[servers]
192.168.1.100
```

   b. 确保连接性：`ansible -m ping`

3. 运行 Playbook 安装 Nginx

   a. 创建一个 Ansible playbook (`nginx.yml`)。

```yaml
- hosts: servers
  become: yes
  tasks:
    - name: Install Nginx
      dnf:
        name: nginx
        state: present
```

   b. 执行 playbook：`ansible-playbook nginx.yml`

   c. 通过服务器的公 IP 验证安装。

这些实践实验室演示如何在混合和多云环境中高效地部署、保护和管理 Rocky Linux，并以 AWS 为主。通过利用自动化工具、安全网络配置和监控解决方案，组织可以提高云部署的运营效率和安全性。

## 结论

Rocky Linux 证明是云部署的一种强大且多功能的操作系统，在各种云环境中提供了稳定性、安全性和灵活性。本章探讨了在 AWS 中部署和管理 Rocky Linux 的关键方面，从使用 Amazon Machine Images (AMI) 备实例，到通过 IAM 和安全组实施安全最佳实践。

此外，对混合和多云策略的讨论强调了现代企业基础设施中灵活性的重要。因此，通过利用 Terraform 和 Ansible 等自动化工具，组织可以简化云操作，确保效率和可扩展性。

随着云应用的持续演进，在云环境中精通 Rocky Linux 将对于旨在优化部署性能、安全性和成本效益的 IT 专业人员和组织至关重要。

# 重点回顾

- AWS 上的优化部署

  - 预配置 AMI：Rocky Linux 提供官方 Amazon Machine Images (AMI)，确保精简的 EC2 实例部署。

  - 可扩展性和高可用性：支持 AWS 自动伸缩组 (ASG) 和弹性负载均衡 (ELB)以保持性能和可用性。

  - 代码即基础设施 (IaC)：Terraform 和 AWS CloudFormation 等工具实现了 Rocky Linux 实例的自动化备备。

- 云安全最佳实践

  - 身份和访问管理 (IAM)：通过 IAM 角色和策略实施最小权限访问，防止未经授权的访问。

  - 网络安全：安全组和网络 ACL 定义严格的入站和出站流量规则以增强保护。

  - 数据加密：AWS 密钥管理服务 (KMS) 对静态和传输中的数据进行加密以确保安全。

  - 日志与监控：与 AWS CloudWatch、AWS CloudTrail 以及第三方工具（例如 Splunk）集成提供实时安全洞察。

- 云环境的优化配置

  - 自动化实例设置：Cloud-init 和 Ansible 允许自动化配置和部署后自定义。

  - 存储管理：支持用于持久存储的 Amazon EBS 和用于扩展对象存储的 S3。

  - 性能优化：微调 CPU、内存和 I/O 参数确保实例运行高效且成本效益。

- 混合和多云兼容性

  - 跨云部署：Rocky Linux 可以在 AWS、Azure 和 Google Cloud 上运行，为多云策略提供活性。

  - 混合集成：AWS Direct Connect 和 VPN 等工具实现了本地数据中心与云基础设施之间的无缝连接。

  - 容器化与编排：Kubernetes 和 Docker 允许在云原生应用中高效部署和管理 Rocky Linux 工作负载。

# 选择题

1. 使用哪个命令通过 AWS CLI 在启动上的 Rocky Linux 实例？

   a. `aws ec2 run-instances --image-id ami-xxxxx --count 1 --instance-type t2.micro`

   b. `aws start-rocky-linux-instance`

   c. `aws deploy rocky-linux --instance t2.micro`

   d. `aws create-instance rocky-linux`

2. 哪种 AWS 服务提供虚拟服务器以便在云中运行 Rocky Linux？

   a. Amazon RDS

   b. Amazon Lambda

   c. Amazon EC2

   d. AWS Fargate

3. 哪种工具可以用于自动化 AWS 中 Rocky Linux 实例的配置？

   a. AWS CloudFormation

   b. Kubernetes

   c. Docker Compose

   d. Prometheus

4. 哪种 AWS 安全功能有助于控制指向 Rocky Linux 实例的入站和出站流量？

   a. IAM 策略

   b. AWS WAF

   c. 安全组

   d. AWS Shield

5. 在 AWS 中处理 Rocky Linux 时，IAM 角色的主要功能是什么？

- IAM (身份和访问管理): AWS 服务，用于用于管理与 Rocky Linux 9 实例交互的用户及服务的访问权限和身份验证。

- Ansible Cloud Modules: Ansible 内部的模块，用于自动化云操作，包括在 AWS 中对 Rocky Linux 9 实例进行置备、扩展和配置。
