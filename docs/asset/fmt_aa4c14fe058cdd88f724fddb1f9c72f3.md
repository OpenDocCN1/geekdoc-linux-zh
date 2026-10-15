
# S3 桶创建与 AWS CLI 安装

点击创建桶并按照向导创建一个新的 S3 桶。选择合适的名称和区域。

## 2. 在 Rocky Linux 9 上安装 AWS CLI

在 Rocky Linux 9 机器上安装 AWS CLI。

```bash
sudo dnf install aws-cli
```

`aws configure` # 设置访问密钥、区域和输出格式

## 3. 与 S3 存储桶同步数据

### a. 从 KVM 虚拟机上传文件到 AWS S3

使用 `aws s3 cp` 命令：

```
aws s3 ls
touch myfile.txt
aws s3 cp /path/to/local/file s3://<bucket-name>/<object-key>
```

### b. 从 S3 下载文件到 KVM 虚拟机

```
aws s3 cp s3://<bucket-name>/<object-key> /path/to/local/destination
```

## 4. 为混合云访问设置权限

配置 IAM 角色和 S3 存储桶策略，以确保 EC2 实例和本地服务器都能安全地访问 S3。创建一个具有适当权限的 IAM 角色并将其分配给 EC2 实例。

## 5. 数据同步自动化

可以使用 AWS CLI 脚本和 `cron` 任务实现本地 KVM 虚拟机与 AWS EC2 实例之间的数据同步。例如：

```bash
crontab -e # 编辑 cron 任务
0 * * * * aws s3 sync /local-folder s3://<bucket-name>/backup/
```

# 实验 4：使用 AWS IAM 管理混合云安全

在混合云环境中，安全性是一个至关重要的问题。IAM（身份和访问管理）在控制云资源访问以及跨本地和云系统管理身份方面起着关键作用。

## 场景

我们将配置 AWS IAM 来管理对 AWS 服务的访问，确保本地系统和云服务的安全性。

## 步骤

### 1. 创建 IAM 角色和策略

#### a. 为 EC2 实例创建 IAM 角色

允许访问 S3 存储桶和其他服务。使用 IAM 策略为该角色分配适当权限。

#### b. 允许完全访问 S3 的 IAM 策略示例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::<bucket-name>/*"
    }
  ]
}
```

### 2. 将 IAM 角色分配给 EC2 实例

将 IAM 角色附加到需要访问 S3 存储或其他 AWS 资源的 EC2 实例。

### 3. 在本地系统中使用 IAM

#### a. 在 Rocky Linux 9 上

我们可以使用带有 IAM 凭证的 AWS CLI 安全地与 AWS 资源交互。

#### b. 凭证存储

确保我们的 AWS 凭证存储在 `~/.aws/credentials` 文件或通过环境变量设置。

### 4. 混合环境的安全最佳实践

#### a. 加密

始终对敏感数据进行传输中加密（使用 VPN）和静态地加密（使用 S3 加密）。

#### b. 多因素身份验证 (MFA)

对访问关键云资源的 IAM 用户和角色启用 MFA。

在本章中，我们探索了混合云环境的概念，重点关注了本地基础设施（在 Rocky Linux 9 上使用 KVM）与云资源（AWS EC2 和 S3）的集成。混合云模型提供了灵活性和扩展性，使其能够优化工作负载、管理成本，并将本地系统与云资源安全地集成。

核心要点包括：

- 混合云架构集成了私有（本地）和公共（云）云，以实现最佳性能和成本效益。
- VPN 连接实现了本地系统与云系统之间的无缝通信。
- AWS S3 提供了可扩展的存储解决方案，本地和云系统均可访问。
- IAM 角色和策略有助于保护混合环境并管理对云服务的访问。

通过理解和实施这些实践，组织可以在混合模型中利用本地和云资源的力量，确保它们为未来的扩展性和效率做好了充分准备。

到此，混合云环境简介章节已圆满结束。

# 结论

使用 KVM 进行虚拟化为优化 IT 基础设施提供了一个强大且灵活的框架，使其成为现代数据中心和云解决方案的基石。通过将 Rocky Linux 转换为虚拟机管理程序（hypervisor），KVM 实现了高效的资源分配、成本节省和操作扩展性（注：此处 scalability 通常指规模业务的可扩展性）。在整个章节中，我们探索了安装和配置 KVM 的基本步骤，演示了如何有效地设置和管理虚拟机。虚拟网络的集成进一步增强了虚拟机与物理或云网络之间的连通性和无缝通信，这是部署稳健虚拟化解决方案的关键方面。

此外，本章对本地 KVM 虚拟化和 AWS EC2 进行了对比分析，阐明了它们独特的优势和用例。这种比较为组织如何根据需求选择最佳方法提供了见解。最后，对混合云环境的介绍强调了结合本地和云解决方案的潜力，提供了利用两者优势的灵活性。掌握 Rocky Linux 上的 KVM 使读者具备部署多功能和可扩展虚拟化解决方案的知识，为高效的 IT 管理和创新的云策略铺平了道路。

在下一章中，我们将重点转向使用 Docker 进行容器化，这是传统虚拟化的一种轻量且高效的替代方案。我们将探索如何在 Rocky Linux 上部署和管理容器，将它们与 AWS 服务集成，并利用 Docker Compose 进行多容器应用程序，为可扩展和可移植的云原生解决方案奠定基础。

# 记忆点

- 安装和配置 KVM
- 基于内核的虚拟机 (KVM) 是 Linux 内核的内置功能，允许 Rocky Linux 当虚拟机管理程序来托管虚拟机 (VMs)。安装 KVM 涉及使用 `dnf` 等包管理器安装必要的包，如 `qemu-kvm`、`libvirt` 和 `virt-manager`。
- 创建和管理虚拟机：KVM 允许管理员使用 `virt-manager` 图形界面或 `virsh` 命令行来创建和管理虚拟机。虚拟机可以运行不同的操作系统，并对 CPU、内存和存储进行自定义。快照和备份为状态管理提供了灵活性，允许管理员还原更改。
- 虚拟机网络：KVM 虚拟网络使用桥接或 NAT。桥接网络将虚拟机直接连接到主机物理网络，而 NAT 允许虚拟机内部通信或访问外部网络。使用 `virsh` 工具或编辑 `/etc/libvirt/q/` 文件来管理虚拟网络。
- 对比本地虚拟化与 AWS EC2：本地 KVM 虚拟化提供了对基础设施的完全控制，对于可预测的工作负载可能更具成本效益，而 AWS EC2 通过处理硬件准备、扩展和更新简化了基础设施管理。KVM 则允许根据组织需求定制环境。

# 混合云简介

- 混合云环境结合了本地基础设施和云资源的优点，提供了灵活性和冗余。
- 将 KVM 与云平台结合使用允许组织创建混合设置，以增强扩展性和韧性。

# 选择题

1. 在 Rocky Linux 上安装 KVM 使用什么命令？

  a. `dnf install kvm-qemu`
  b. `dnf install qemu-kvm`
  c. `yum install kvm-tools`
  d. `apt-get install qemu-qemu`

2. `/etc/libvirt/libvirtd.conf` 文件的目的是？

  a. 存储虚拟机日志
  b. 配置 libvirt 守护进程
  c. 管理虚拟机快照
  d. 定义虚拟网络接口

[PAGE 589]

3. 在 KVM 中，通常用于通过命令行界面创建和管理虚拟机的工具是？

  a. `virt-manager`
  b. `virsh`
  c. `kvm-cli`
  d. `qemu-tools`

4. KVM 中的桥接网络（bridged network）允许什么？

  a. 仅限虚拟机内部通信
  b. 虚拟机直接连接到主机的物理网络
  c. 虚拟机通过宿主机访问互联网
  d. 虚拟机内部的隔离通信

5. 快照（snapshots）在 KVM 中的作用是什么？

  a. 加密虚拟机磁盘镜像
  b. 创建宿主机系统的备份
  c. 虚拟虚拟机的当前状态以备日后恢复
  d. 实时监控虚拟机的性能

6. 哪个命令在 Rocky Linux 上启动 libvirt 服务？

  a. `service libvirt start`
  b. `systemctl enable libvirt`
  c. `systemctl start libvirtd`
  d. `libvirt --start`

7. AWS EC2 相比本地（on-premises）KVM 虚拟化，其核心优势是什么？

  a. 对硬件基础设施的完全控制
  b. 简化的硬件配置和扩展性
  c. 对于可预测负载具有较低的初始成本
  d. 对虚拟网络的高级支持

8. KVM 虚拟网络配置中的哪个参数定义网络类型为 NAT 或桥接？

  a. `<forward mode>`

[PAGE 590]
