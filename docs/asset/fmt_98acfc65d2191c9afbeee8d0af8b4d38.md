
# 在 AWS 中配置 Rocky Linux

## 1. 优化网络

- a. 启用防火墙规则：配置 `firewalld` 管理端口：

```bash
sudo firewall-cmd --add-service=ssh --permanent
```

```bash
sudo firewall-cmd --reload
```

- b. 使用弹性 IP `Elastic IPs`：为实例分配弹性 IP 以确保具有静态 IP。
- c. 启用高可用：使用多个可用区和负载均衡器来实现冗余。

## 2. 磁盘管理

- a. 使用 `/etc/fstab` 配置自动挂载
  - i. 打开 `/etc/fstab` 文件：`sudo nano /etc/fstab`
  - ii. 添加以下行进行自动挂载（确保使用正确的设备名称 `/dev/xvda127`）：

```text
/dev/xvda127 /data ext4 defaults,nofail 0 2
```

  - iii. 保存并退出文件。
- b. 验证已连接卷
  - i. SSH 连接到 EC2 实例并运行：`lsblk`
  - ii. 验证磁盘和分区：

```text
[ec2-user@ip-172-31-20-219 ~]$ lsblk
NAME      MAJ MIN RM SIZE TYPE MOUNTPOINT
xvda      202:0  0   8G 0 disk /
xvda1     202:1  0   8G 0 part /
xvda127   259:0  0   1M 0 part /
```

故障排除与维护涉及识别和解决系统或应用程序中的问题，并进行常规维护以确保最佳性能。关键活动包括监控系统健康、应用更新和补丁、诊断错误以及优化资源，以防止中断并维持长期可靠性。

## 常见问题

- 实例无法访问：
  - 验证安全组规则。
  - 检查 `firewalld` 和 SSH 配置。
- 磁盘满：
  - 识别大文件：`sudo du -sh /* | sort -hn`
  - 清理或调整卷大小。

## 自动化维护

- 使用 `cron` 执行定期任务：
  - `sudo yum install cronie`
  - `sudo crontab -e`

示例：每周日清理临时文件

`0 3 * * 0 /usr/bin/find /tmp -type f -mtime +7 -exec rm -f {} \;`

最后，我们使用键盘上的 ESC 键 `:wq` 保存更改。在 AWS 环境中管理 Rocky Linux 需要 Linux 知识和对 AWS 工具的熟悉。通过优化系统配置、与 AWS 服务集成并遵循最佳实践，我们可以实现安全、可扩展且高效的云基础设施。

## 使用 AWS CLI 和 SDK 进行云自动化

自动化是在 Amazon Web Services `AWS` 中高效管理云基础设施的关键。AWS 命令行界面 `CLI` 和软件开发包 `SDK` 提供了强大的工具，用于自动化任务、扩展操作以及将 AWS 服务集成到应用程序中。

### AWS CLI

AWS CLI 是一个命令行工具，允许用户以编程方式与 AWS 服务进行交互。它支持所有 AWS 服务，提供了一种脚本化和自动化任务的高效方法。

- **更新系统**：`sudo dnf update -y`
- **安装 AWS CLI v2**：下载并安装 AWS CLI v2：
  - `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`
  - `unzip awscliv2.zip`
  - `sudo ./install`
- **验证安装**：运行以下命令确认 AWS CLI 是否安装正确：`aws-cli --version`
- **常用命令**

我们应该看到类似的内容：`aws-cli/2.x.x Python/3.x.x Linux/5.x.x`

### 列出 S3 桶

列出 S3 桶是指检索并显示与 AWS 账户关联的所有 Amazon S3 存储桶的过程。可以使用 AWS CLI 通过命令 `aws s3 ls` 实现，提供可用存储资源的概览。

- `aws s3 mb s://kasparov-server`
- `aws s3 mb s://cesarsmserver`
- `aws s3 ls`

示例输出：

```
$[ec2-user@ip-172-31-31-92 ~]$ aws s3 ls
2024-12-23 22:08:54 cesarsmserver
2024-12-23 22:08:36 kasparov-server
```

> 图 6.20：通过 AWS CLI 列出 S3 桶

所示命令用于使用 AWS CLI 创建和列出 Amazon S3 桶。`aws s3 mb s://<bucket-name>` 命令创建一个指定名称的新 S3 桶，例如 kasparov-server 或 cesarsmserver。之后，`aws s3 ls` 命令列出与 AWS 账户关联的所有可用桶。输出（图 6.9）显示了新创建的桶，提供了 S3 存储资源的快速概述。这些命令对于管理和组织 Amazon S3 中的数据至关重要。

### AWS CLI 验证示例

自动化实例启动和验证。

- 1. 从 AMI 启动实例：此信息可以在实例的仪表板中找到。

```bash
ec2 run-instances --image-id ami-0abcd1234efgh5678 --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-12345 --subnet-id subnet-67890
```

示例输出：

```json
{
  "Groups": [],
  "Instances": [
    {
      "AmiLaunchIndex": 0,
      "ImageId": "ami-01016d07b1128cd2d2",
      "InstanceId": "i-0d72a8e976ee017e6",
      "InstanceType": "t2.micro",
      "KeyName": "RockyLinux_9",
      "LaunchTime": "2024-12-29T06:23:08:00",
      "Monitoring": {
        "State": "disabled"
      },
      "Placement": {
        "AvailabilityZone": "us-east-1d",
        "GroupName": "",
        "Tenancy": "default"
      },
      "PrivateDnsName": "ip-172-31-22-111.ec2.internal",
      "PrivateIpAddress": "172.31.22.111",
      "ProductCodes": []
    }
  ]
}
```

图 6.21：显示如何使用 AWS CLI 从指定的 Amazon 映像 `AMI` 自动启动 EC2 实例。通过运行 `ec2 run-instances`，我们可以为实例指定 AMI ID、实例类型、密钥对、安全组和子网。在这种情况下，`--image-id` 指向特定的 AMI。输出（图 6.10）通常会显示关于新启动实例的信息，包括其 ID 和其他元数据。

- 2. **连接并验证**：使用 SSH 或运行 Systems Manager 命令。
- 3. **终止实例**：我们将省略此命令。

`aws ec2 terminate-instances --instance-ids i-0abcd1234efgh5678`

- 4. **配置 AWS CLI**：使用凭据与 AWS CLI 交互。

## 连接到实例

- a. 获取公 IP：
  - 在 AWS 控制台中找到实例的公 IP 地址。
- b. 通过 SSH 连接：`ssh -i /path/to/<the given key>.pem rocky@public-ip`
- c. 初始设置：
  - 更新系统：`sudo dnf update -y`
  - 安装基础工具：`sudo dnf install wget -y curl vim --allowerasing`

### g. 配置安全组

定义入站规则，例如允许 SSH（端口 `22`）。

### h. 启动实例

- i. 为 SSH 访问选择或创建密钥对。
- ii. 检查并启动实例。
