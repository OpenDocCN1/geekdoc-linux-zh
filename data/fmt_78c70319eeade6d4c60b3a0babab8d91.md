
重试安装：
```
[localuser@localhost ~]$ sudo dnf install nano
```
Installed: nano-5.6.1-5.el9.x86_64
完成!

## 场景 2：缺失依赖

问题：由于缺少依赖项，安装 `gedit` 失败。
```
[localuser@localhost ~]$ sudo dnf install gedit
```
Error: Problem: package gedit-2:40.0-6.el9.x86_64 requires libpeas-gtk

### 解决方案：

搜索依赖：
```
[localuser@localhost ~]$ dnf search libpeas-gtk
```
libpeas-gtk.x86_64 : GTK+ widgets for libpeas

安装依赖项：
```
[localuser@localhost ~]$ sudo dnf install libpeas-gtk
```

重试安装：
```
[localuser@localhost ~]$ sudo dnf install gedit
```
Installed: gedit-2:40.0-6.el9.x86_64
完成!

## 场景 3：仓库访问错误

问题：由于网络问题或 URL 错误导致无法访问仓库。
```
[localuser@localhost ~]$ sudo dnf update
```

Error: Failed to download metadata for repo 'epel': Cannot prepare internal mirrorlist

### 解决方案：

检查网络连接：
```
[localuser@localhost ~]$ ping google.com
```
PING google.com (142.250.190.78) 56(84) bytes of data.

验证 `/etc/yum.repos.d/` 中的仓库配置：
```
[localuser@localhost ~]$ cat /etc/yum.repos.d/epel.repo
```
epel
baseurl=https://dl.fedoraproject.org/pub/epel/9/Everything/x86_64/

enabled=1
gpgcheck=1

如果 URL 错误，更新它或禁用该仓库：
```
[localuser@localhost ~]$ sudo dnf config-manager --set-disabled epel
```

清除并刷新缓存：

```
[localuser@localhost ~]$ sudo dnf clean all
```

```
[localuser@localhost ~]$ sudo dnf makecache
```

## 第 3 步：通用故障排除

检查日志：
```
[localuser@localhost ~]$ cat /var/log/dnf
```

检查冲突：
```
[localuser@localhost ~]$ dnf check
```

强制刷新元数据：
```
[localuser@localhost ~]$ sudo dnf makecache --refresh
```

安装问题包：
```
[localuser@localhost ~]$ sudo dnf install <package_name>
```

## 第 4 步：验证

确认包已安装：
```
[localuser@localhost ~]$ rpm -q <package_name>
```

## 自动化包管理

自动化在确保整个基础设施的一致性和效率方面起着关键作用。这可以通过使用 CloudFormation 模板来实现。

### 前提条件

- AWS 账户：确保我们有一个 AWS 账户。
- IAM 权限：创建 EC2 实例和 CloudFormation 栈的权限。
- AWS CLI 或 AWS 管理控制台：用于部署模板。
- YAML 语法基础知识：用于编辑模板。

## 实验步骤

### 第 1 步：编写 CloudFormation 模板

- 打开文本编辑器并创建一个名为 `package-management.yaml` 的新文件。
- 添加以下 YAML 内容来定义一个 EC2 实例：

# 用于 EC2 实例的 AWS CloudFormation 模板

AWSTemplateVersion: "2010-09-09"
Description: 自动化 EC2 实例上的包管理

Resources:

  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro # 指定低成本的通用实例类型
      ImageId: ami-0abcd1234efgh5678 # Rocky Linux 9 的 AMI ID（根据区域替换为有效 ID）
      KeyName: my-key-pair # 用于安全访问的 SSH 密钥
      UserData:
        Fn::Base64: |
          #!/bin/bash
          # 更新所有已软件包到最新版本
          sudo dnf update -y
          # 安装 Apache HTTP 服务器
          sudo dnf install -y httpd
          # 启动 Apache 服务
          sudo systemctl start httpd
          # 确保 Apache 开机启动
          sudo systemctl enable httpd
      Tags:
        - Key: Name
          Value: MyEC2Instance # 用于标识的名称标签

每个属性和 `UserData` 脚本中的命令现在包含了注释。`Description` 字段说明了模板的目标。

### 第 2 步：验证 CloudFormation 模板

- 使用 AWS CLI 验证模板：
  ```
  aws cloudformation validate-template --template-body file://package-management.yaml
  ```

- 如果模板有效，我们将收到成功消息。如果验证失败，请修复任何错误。

### 第 3 步：部署 CloudFormation 栈

- 使用 AWS CLI 部署栈：

```
aws cloudformation create-stack \
  --stack-name PackageManagementStack \
  --template-body file://package-management.yaml \
  --parameters ParameterKey=KeyName,ParameterValue=my-key-pair
```

b. 或者，也可以通过 AWS 管理控制台上传模板：

- i. 转到 CloudFormation。
- ii. 点击“创建栈” > “使用新资源（标准（standard）”。
- iii. 上传模板文件并按照提示操作。

## 第 4 步：验证自动化

- a. 栈创建完成后，导航到 EC2 仪表板。
- b. 找到由栈启动的 EC2 实例并使用 SSH 连接到它：

```
ssh -i /path/to/my-key-pair.pem ec2-user@<instance_public_ip>
```
