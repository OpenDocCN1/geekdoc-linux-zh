
手动部署实例可能非常耗时，特别是在管理多个环境或确保配置一致性时。AWS CloudFormation 和 Terraform 等自动化工具通过定义基础设施即代码 (IaC) 来简化此过程。这些工具允许我们高效地部署和管理 Rocky Linux 实例，确保可重复性、扩展性并减少配置漂移。

# 使用 CloudFormation 自动化

AWS CloudFormation 允许我们使用代码定义并配置 AWS 基础设施。通过编写 YAML 模板，我们可以使用结构化格式指定 Rocky Linux AMI、实例类型、安全组和其他配置。这种方法确保了部署的一致性、可重复性和可效率。

## 使用 CloudFormation 自动化部署的步骤

1. 创建 YAML 模板

   定义必要的基础设施组件，包括：

   - `ImageId`：指定 Rocky Linux AMI。
   - `InstanceType`：定义分配给实例的计算资源。
   - `SecurityGroups`：控制访问规则（例如，允许 22 端口的 SSH）。

2. 使用 AWS CLI 部署 CloudFormation 栈

   使用以下命令创建新栈：

   ```bash
   aws cloudformation create-stack --stack-name rocky-linux-stack --template-body file://rocky-linux-template.yml
   ```

   此命令指示 AWS CloudFormation 读取 `rocky-linux-template.yml` 文件并自动配置所需的资源。

   一旦部署完成，AWS CloudFormation 确保了部署保持一致性、可重复性和可管理性。

# 使用 Terraform 自动化

手动部署实例可能非常耗时，特别是在管理多个环境或确保配置一致性时。AWS CloudFormation 和 Terraform 等自动化工具通过定义基础设施即代码 (IaC) 来简化此过程。这些工具允许我们高效地部署和管理 Rocky Linux 实例，确保可重复性、扩展性并减少配置漂移。

## 使用 Terraform 自动化的步骤

1. 创建 Terraform 配置

   定义必要的基础设施组件，包括：

   - `ImageId`：指定 Rocky Linux AMI。
   - `InstanceType`：定义分配给实例的计算资源。
   - `SecurityGroups`：控制访问规则（例如，允许 22 端口的 SSH）。

   ```hcl
   terraform {
     required_providers {
       aws = {
         source  = "hashicorp/aws"
         version = "~> 5.0"
       }
     }
   }

   provider "aws" {
     region = "us-east-1"
   }

   resource "aws_instance" "rocky-linux" {
     ami           = "ami-0a2b7ef1b"
     instance_type = "t2.micro"
     key_name      = "your-key"
     tags = {
       Name        = "rocky-linux"
       Environment = "dev"
     }
   }
   ```

2. 使用 AWS CLI 部署栈

   要使用 Terraform 部署基础设施，首先初始化目录并应用配置：

   ```bash
   terraform init
   terraform apply -auto-approve
   ```

   执行后，Terraform 将部署定义的 Rocky Linux 实例。它还会生成并维护一个状态文件，用于跟踪基础设施的当前状态。该文件实现了高效的更新和持续一致的管理。

3. 配置安全组以限制 SSH 访问。

4. 验证未经授权的访问已被拦截。

# 实验 4：配置自动化备份

**目标：** 为 Rocky Linux 实例实现自动化备份。

1. 手动为 EC2 实例创建快照。
2. 配置 AWS Lambda 函数以自动化快照。
3. 使用快照测试恢复。

**在 AWS EC2 上部署 Rocky Linux 既简单又高效——特别是当通过 AWS CloudFormation 和 HashiCorp Terraform 等自动化工具增强时。** 这些工具通过实现基础设施即代码 (IaC)，简化了 EC2 实例的配置和管理。CloudFormation 提供了一种专为 AWS 环境优化的原生声明式方法，而 Terraform 则提供了跨平台兼容性，允许在不同的云提供商之间一致地管理基础设施。通过预定义的配置，可以精确且可重复地部署和自定义 Rocky Linux 实例。

**安全性仍然任何云端部署的关键组件。** 实施 IAM 最佳实践——例如最小权限原则和基于角色的访问控制——有助于确保访问仅限于授权的用户和服务。此外，通过配置安全组和防火墙规则限制不必要的网络流量，可以最大限度地减少受到外部威胁的风险。

本章包含专注于在 AWS 上部署、配置和保护 Rocky Linux 实例的**实践实验**。这些练习提供了在基础设施自动化以及在受控环境中应用云安全标准的实操经验。

# 在 AWS 中配置 Rocky Linux 实例

在 AWS 中配置 Rocky Linux 实例可确保最优性能、安全自动化。本指南涵盖了网络、存储、安全和自动化工具等关键方面，以便在 AWS 云中高效地管理 Rocky Linux 环境。

- 实例初始化与系统更新

    - 登录 AWS 管理控制台并启动 Rocky Linux 实例。

    - 使用 `ssh -i my-key.pem ec2-user@<instance-public-ip>` 通过 SSH 连接。

    - 使用 `sudo dnf update -y` 更新系统。

    - 设置主机并启用所需的服务。

- 配置网络与安全

    - 如必要，分配静态私有 IP 地址。

    - 使用 `firewall` 或 `iptables` 配置防火墙规则。

    - 设置安全组仅允许必要的入站流量。

    - 启用 SSH 密钥认证并禁用密码认证。

- 存储与磁盘管理

    - 附加额外的 EBS 卷并使用 `mkfs.xfs` 进行格式化。

    - 使用 `/etc/fstab` 挂载并配置自动挂载。

    - 使用 `tuned` 配置优化磁盘性能。

- 用户管理与访问控制

    - 使用 `useradd` 和 `passwd` 创建并管理用户。

    - 为管理任务配置 `sudo` 权限。

    - 使用 `/etc/ssh/sshd_config` 设置 SSH 访问限制。

## 使用 Ansible 和 Terraform 进行自动化

- 使用 Ansible 自动化包安装和配置。

- 使用 Terraform 定义安全组和 AMI 并部署实例。

- 使用 `cron` 或 `systemd` 定时器调度自动化维护任务。

## 监控与日志

- 安装并配置 CloudWatch Agent 用于实例监控。

- 使用 `logrotate` 设置日志轮转。

- 使用 `journalctl` 处理 systemd 日志和故障排除。

## 章节：建议

- 在 AWS 上正确配置 Rocky Linux 可提高安全性和性能。

- 使用 Ansible 和 Terraform 进行自动化可简化实例管理。

- 监控和日志有助于维护系统的健康和可靠性。

# 云安全最佳实践：IAM 和安全组

云安全对于保护基础设施、应用程序和数据免受未经授权的访问和网络威胁至关重要。身份访问管理 (IAM) 和安全组是云安全的基础组件，提供了受的资源访问和网络隔离。本指南扩展了 IAM 和安全组的最佳实践，强调了安全策略、监控和自动化以加强云安全。

## 身份和访问管理 (IAM) 最佳实践

IAM 是一种关键的安全机制，确保只有授权的用户和服务才能访问云资源。以下最佳实践增强了 IAM 安全性：

### 最小权限原则 (PoLP)

最小权限原则确保用户、应用程序和服务仅接收执行任务所需的权限。这最大限度地减少了权限提升和意外暴露的风险。

1. 使用具有细粒度权限的 IAM 策略。
2. 将分配给角色或组级别，而不是用户级别。
3. 定期审查 IAM 策略以移除过多的权限。

### 使用 IAM 角色代替长期凭据

IAM 角色提供临时安全凭证，降低了凭据泄露和未经授权访问的风险。

- 为需要访问 AWS 资源的应用程序和服务使用 IAM 角色。
- 避免在代码或配置文件中硬编码访问密钥。
- 频繁轮换 IAM 凭据，并执行严格的生命周期管理。

### 启用多因素认证 (MFA)

MFA 通过要求额外的身份因素增强访问安全。

- 对所有特权用户（包括管理员和服务账户）强制执行 MFA。
- 利用硬件或虚拟 MFA 令牌提高安全性。
- 使用条件访问策略根据用户角色和位置强制 MFA。

### 审计 IAM 策略和访问日志

定期审计有助于检测配置错误和潜在的安全威胁。
