
d. 设置 `root` 密码并按照提示完成安全设置。

## 步骤 4. 验证 MySQL 安装

a. 登录 MySQL：`sudo mysql -u root -p`

b. 验证服务器正在运行：

```
SHOW DATABASES;
```

Exit MySQL:

```
EXIT;
```

数据库管理的主题将在本书的第 9 章《数据库管理》中深入探讨。本章提供了关于安装和配置 MySQL 和 MariaDB 的全面指南、实施有效的数据库备份和恢复策略、优化数据库性能，以及引入用于托管数据库服务的 AWS RDS。此外，它还将涵盖在云环境中扩展数据库的方法。每个主题都为初学者设计，章节中有清晰的解释，并提供补充的可下载指南以供实践学习。

## 步骤 5：将 PHP 连接到 MySQL

a. 安装 PHP-MySQL 模块：`sudo dnf install php-mysqlqld -y`。

b. 重启 Apache 应用更改：`sudo systemctl restart httpd`。

## 步骤 6：创建一个示例 PHP-MySQL 脚本

a. 创建一个 PHP 文件来测试连接：`sudo nano /var/www/html/dbtest.php`

b. 添加以下代码：

```php
<?php
$servername = "localhost";
$username = "root";
$password = "your_root_password";
// 创建连接
$conn = new mysqli($servername, $username, $password);
// 检查连接
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully to MySQL!";
?>
```

c. 保存并关闭文件。

d. 在浏览器中访问脚本：`http://<server-ip>/dbtest.php`

在这种，服务器 IP 地址是本地 ipv4 地址。如果成功，将显示以下消息：“Connected successfully to MySQL!”

## 步骤 7：调整防火墙和 SELinux（如有必要）

a. 打开 HTTP 和 HTTPS 端口：

- `sudo firewall-cmd --permanent --add-service=http`
- `sudo firewall-cmd --permanent --add-service=https`
- `sudo firewall-cmd --reload`

b. 针对 Apache 和 PHP 调整 SELinux：

- `setsebool -P httpd_can_network_connect on`

在 Rocky Linux 上 PHP 和 MySQL 环境的设置已有效完成。此设置为托管动态网站或应用程序提供了基础。从现在起，可以构建更复杂的应用程序、安装如 WordPress 等 CMS 平台，或对自定义 PHP 代码进行实验。

## 在 AWS 上使用 ELB 和自动扩展部署可扩展 Web 服务器

在现代云基础设施中，可扩展性和高可用性对于提供可靠的 Web 服务至关重要。AWS 提供了强大的工具如弹性负载均衡（ELB）和自动扩展（Auto Scaling），帮助分发流量并自动适应变化的工作负载。当与托管在 EC2 实例上的 Apache Web 服务器结合时，该架构能够实现无缝扩展并提高容错能力。

![](img/b8b015d9ebe4ee947c12a4edae6c2170_425_0.png)

**图 8.7：** 使用 ELB 和自动扩展的 EC2 部署

此图说明了 AWS 上水平可扩展架构中的 Web 流量。来自互联网用户的传入请求首先引导到弹性负载均衡器（ELB），它智能地将流量分发到运行 Apache Web 服务器的多个 EC2 实例上。这些实例属于自动扩展组的一部分，该组根据实时需求和资源利用率动态调整 EC2 实例的数量。这种设置确保了高可用性、容错性和高效的负载分发，非常适用于流量模式多变的 Web 应用程序。

## 在 AWS 中部署 Web 服务器

在 AWS 中部署 Web 服务器具有云可扩展性、高可用性和简化管理的优势。在本节中，我们将逐步介绍在 AWS EC2 实例上部署 Apache Web 服务器的过程，设置自动扩展以处理不同的流量负载，并配置 ELB 以高效地分发入站流量。

### 步骤 1：启动 EC2 实例

在 AWS 中部署 Web 服务器的的第一是是启动一个 EC2 实例。AWS EC2（弹性计算云）提供了扩展的计算能力，我们可以根据需求从多种实例类型中选择。

a. **登录 AWS 管理控制台**：访问 AWS 管理控制台并登录。

b. **启动 EC2 实例**：访问 AWS 管理控制台并登录。

   i. **选择 Amazon 映像 (AMI)**：选择 Amazon Linux。

   ii. **选择实例类型**：根据需求选择合适的实例类型，如 `t2.micro` 或 `t2.medium`。

   iii. **配置实例详情**：默认设置。

   iv. **添加存储**：弹性块存储 (EBS) 存储。

   v. **配置安全组**：创建一个安全组。开放必要的端口：
      - HTTP（80端口）用于网络流量。
      - SSH（22端口）用于远程访问。

   vi. **启动实例**：选择密钥对并点击“启动”。

c. **访问 EC2 实例**：使用 SSH 连接：`ssh -i /path/to/key.pem ec2-user@your-ip`

### 步骤 2：在 EC2 上安装 Apache

访问实例后安装 Apache。Amazon Linux 自带 HTTP 服务器，如果没有安装，可以通过以下命令进行：

- `yum update -y`
- `sudo yum install httpd -y`

安装完成后，启动 Apache 服务并启用它：

- `sudo systemctl start httpd`
- `sudo systemctl enable httpd`

测试安装，在浏览器中打开实例的公 IP 地址。你应该看到 Apache 的测试页面。

### 步骤 3：为网站配置 Apache

现在我们可以配置 Apache 服务内容。默认情况下，Apache 从 `/var/www/html` 提供内容。我们可以在这里上传 HTML 文件或应用程序代码。

**创建一个简单的网页**：

在 `/var/www/html` 创建 `index.html` 文件：

`sudo nano /var/www/html/index.html`

添加一些内容来测试我们的服务器：

```html
<html>
<head>
<title>欢迎来到我的网站</title>
</head>
<body>
<h1>AWS EC2  Apache Web 服务器</h1>
<p>此 Web 服务器已成功部署！</p>
</body>
</html>
```

**重启 Apache**：添加内容后重启 Apache 以确保更改生效：`systemctl restart httpd`

### 确保安全组允许 HTTP 流量

a. 进入 AWS 管理控制台。

b. 导航到 EC2 > 实例并选择该实例。

c. 在安全组下，编辑入站规则以包含：
   i. **类型**：HTTP
   ii. **协议**：TCP
   iii. **端口范围**：80
   iv. **源**：任意 (0.0.0.0/0) 或特定范围。

- `curl http://localhost`
- `links http://公 IP 地址`

### 步骤 4：设置自动扩展 (Auto Scaling)

为了确保 Web 服务器能够处理不同水平的流量，我们可以在 AWS 中配置自动扩展。Auto Scaling 会自动调整应用程序扩展组中 EC2 实例的数量，以处理流量。

a. 创建自动扩展组：
  i. 导航到 EC2 控制板：在 AWS 管理控制台中，进入 EC2 控制板，并在“Auto Scaling 组”下找到“Auto Scaling 组”部分。
  ii. 创建启动配置：此配置指定了如何在扩展组中启动新的 EC2 实例。选择现有的 AMI（Amazon 映像），配置实例类型（例如，针对更高流量选择 `t2.micro` 或更大规格），并选择之前创建的安全组。
  iii. 创建自动扩展组：定义自动扩展组，选择我们刚刚创建的启动配置。根据预期的流量设置所需的实例数（例如为了冗余设置 2 个）、最小实例数（1）和最大实例数（例如 5 个）。
  iv. 设置扩展策略：定义扩容和缩容的策略。例如，可以设置当 CPU 使用率超过 70% 时启动新实例，当 CPU 使用率低于 30% 时缩容。
