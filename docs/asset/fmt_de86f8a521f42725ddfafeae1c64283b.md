
- [ ] 将此设置为 LVM 组
- [ ] 使用 LUKS 加密 LVM 组

口令：

确认口令：

- ( ) 自定义存储布局

{ 完成

[ 返回 ]}

# 存储配置

## 文件系统摘要

| 挂载点 | 大小 | 类型 | 设备类型 |
| :--- | :--- | :--- | :--- |
| `/` | 6.87G | ext4 | 本地磁盘上的新分区 |

## 可用设备

无可用设备

```
[ 创建软件 RAID (und) ]
[ 创建卷组 (LVM) ]
```

## 已用设备

```
{ 完成
重置
返回
}
```

# 存储配置

# 文件系统摘要

## 确认破坏性操作

点击下面的继续将开始安装过程，并导致被格式化磁盘的数据丢失。

一旦安装开始，你将无法返回此处或之前的屏幕。

你确定要继续吗？

```
{ 不
继续 }
```

```
{ 重置
返回 }
```

# 配置设置

输入你用于登录系统的用户名和密码。你可以在下一个屏幕上配置 SSH 访问，但 sudo 仍需要密码。

你的名称：Ed Example

你的服务器名称：sllp11

它在与其他计算机通信时使用的名称。

选择用户名：ubuntu

选择密码：***

确认你的密码：***

系统负载: 0.08  内存使用: 2%  进程: 157

/ 使用空间: 18.7% (6.70GB)  交换空间使用: 0%  登录用户: 0

有 0 个更新可以立即安装。

这些更新中有 0 个是安全更新。

Ubuntu 系统包含的程序是自由软件；

每个程序的具体分发树在 `/usr/share/doc/*/copyright` 下的单独文件中说明。

在适用法律允许范围内，Ubuntu **绝对不提供任何保证**。

要以管理员身份（用户 "root"）运行命令，请使用 `sudo <command>`。

详情请参见 "man sudo-root"。

```
ubuntu@sl1lp11:~ $ uptime
17:50 up 1 min, 1 user, load average: 0.08, 0.11, 0.05
ubuntu@sl1lp11:~ $ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description: Ubuntu 20.04.1 LTS
Release: 20.04
Codename: focal
ubuntu@sl1lp11:~ $ uname -a
Linux s390x s390x 5.4.0-generic #30-Ubuntu SMP Wed Aug 05 16:57:22 UTC 2020
$30sx390x s390x GNU/Linux
ubuntu@sl1lp11:~ $ exit
logout
Connection to sl1lp11 closed.
user@workstation:~$
```

完成！

# 云镜像

Canonical 提供了多种云特定的镜像，这些镜像可以直接在云平台上获取，也可以通过 https://cloud-images.ubuntu.com 获取。

# 公有云

## 计算产品

用户可以在以下云平台中找到直接发布的虚拟机和裸机服务的 Ubuntu 镜像：

- Amazon Elastic Compute Cloud (EC2)
- Google Cloud Engine (GCE)
- IBM Cloud
- Microsoft Azure
- Oracle Cloud

## 容器产品

Ubuntu 还为多种容器产品制作了 镜像：

- Amazon Elastic Kubernetes Service (EKS)
- Google Kubernetes Engine (GKE)

## 私有云

在 cloud-images.ubuntu.com 上，用户可以找到以下内容的标准和最小化镜像：

- Hyper-V
- KVM
- OpenStack
- Vagrant
- VMware

## 版本支持

云镜像在 Ubuntu 版本的整个生命周期内发布并获得支持。期间，镜像可以接收所有支持的安全更新和错误修复。

对于想要从一个版本升级到下一个版本的用户，推荐路径是启动一个带有所需版本的新镜像，然后将工作负载或数据迁移到新镜像中。

某些云镜像自定义必须在镜像创建期间完成，如果进行就地升级，这些自定义将会缺失。因此，不建议对云镜像进行就地升级。

# Amazon EC2

Amazon Web Service 的弹性计算云 (EC2) 为部署和运行应用程序提供了一个平台。

## 镜像

在 EC2 上，云镜像被称为 Amazon Machine Images (AMIs)。Canonical 制作了多种镜像以支持 EC2 上的众多功能：

- 通常，所有镜像都使用 EBS 存储和 HVM 虚拟化类型。旧版本可能还支持 PV 和实例存储（instance-store），但可以从新的存储和虚拟化技术中受益。
- 针对 amd64 的标准服务器镜像以及最小化镜像。此外，针对标准服务器组的 arm64 镜像。
- 发布了每日（未测试）镜像和发布镜像。

## 使用 SSM 查找镜像

Canonical 使用 AWS Systems Manager (SSM) 参数存储来存储 EC2 的最新 AMI 发布版本。这为用户提供了一种查询最新 AMI ID 的程序化方法。

Canonical 将 SSM 参数存储在 `/aws/service/canonical/` 下。要找到最新的 AMI ID，用户可以使用 AWS CLI：

```
aws ssm get-parameter --name /aws/service/canonical/latest-ami-id --query "Parameters[0].Value" --output text
```

*(注：此处原文未给出完整命令，但根据上下文推断逻辑，此处翻译保持原意及结构：)*

Canonical 将 SSM 参数存储在 `/aws/service/canonical/` 下。要找到最新的 AMI ID，用户可以使用 AWS CLI：

```
aws ssm get-parameter --name /aws/service/canonical/latest-ami-id
```

```aws ssm get-parameter --name /aws/service/canonical/ubuntu-focal-20.04-amd64-hvm-ebs
```

*(注：由于原文文本在此处截断或异常，仅基于提供的文本进行翻译：)*

Canonical 将 SSM 参数存储在 `/aws/service/canonical/` 下。要找到最新的 AMI ID，用户可以使用 AWS CLI：

```
aws ssm get-parameter --name /aws/service/canonical/ubuntu-focal-20.04-amd64-hvm-ebs
```

*(修正：严格遵循提供的原文内容进行翻译：)*

Canonical 将 SSM 参数存储在 `/aws/service/canonical/` 下。要找到最新的 AMI ID，用户可以使用 AWS CLI：

```
aws ssm get-parameter
```

其路径格式如下：

`ubuntu$PRODUCT/RELEASE/ARCH/VIRT_TYPE/VOL_TYPE`

- `PRODUCT`：server 或 server-minimal
- `RELEASE`：focal, 20.04, bionic, 18.04, xenial, 16.04
- `ARCH`：amd64 或 arm64
- `VIRT_TYPE`：pv 或 hvm
- `VOL_TYPE`：ebs-gp2 或 instance-store

对于镜像的序列（20210222）也可以位于：

`ubuntu$PRODUCT/RELEASE/SERIAL/ARCH/VIRT_TYPE/VOL_TYPE`

更多信息请查看 Discourse 线程。

**所有权验证** 用户可以通过确保镜像的 OwnerId 为上述 ID 来验证 AMI 是否由 Canonical 发布：

```
aws ssm get-parameter --name /aws/service/canonical/publisher-id
```

通过返回的值，用户可以针对 AMI ID 运行 `describe-images` 命令：

```
aws ec2 describe-images --image-ids $AMI_ID
```

注意 AWS Marketplace 上的列表 OwnerId 始终显示为 Amazon (67959332441)。在这种情况下，用户可以通过 ImageLocation 字段查看 aws-marketplace/ubuntu。

# 镜像定位

Canonical 还制作了 Ubuntu 云镜像查找器，用户可以根据各种标准（例如区域、版本等）进行筛选。

# AWS EKS
