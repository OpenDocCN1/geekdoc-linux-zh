
# 教程：在 AlmaLinux 8.4 上安装 WordPress

> 原文：<https://blog.eldernode.com/install-wordpress-on-almalinux/>

![Tutorial Install WordPress on AlmaLinux 8.4](img/b468a08539328635dd88889ab1af7929.png)

进入网站设计领域的用户都熟悉内容管理系统（CMS）。WordPress 是一个网站内容管理系统，你可以用它来创建各种网站和博客。由于 WordPress 内容管理系统的高度灵活性，你将能够使用它来启动任何类型的网站。在这篇文章中，我们将教你如何在 AlmaLinux 8.4 上安装 WordPress。如果你想买一个 [Linux VPS](https://eldernode.com/linux-vps/) 服务器，你可以在 [Eldernode](https://eldernode.com/) 看到可用的软件包。

## 如何在 AlmaLinux 8.4 上安装 WordPress

### WordPress 和其功能介绍

有许多内容管理系统可用于建立一个网站，其中一些比其他人有优势。WordPress 是一个内容管理系统，由各种各样的模板和皮肤组成，免费提供给用户。你可以使用这个系统来启动你的网站，不需要任何编程技能。

使用内容管理系统创建的网站实际上是动态网站。如果你是网站设计新手，想要建立一个网站，我们建议你使用像 WordPress 这样的内容管理系统，因为网站设计和编程非常费时费钱。

WordPress 最重要的优点和特性是：

1. 简单易用
2. 可持续性和创造性
3. 有吸引力的设计选项
4. 灵活性
5. 搜索引擎优化
6. 结构
7. 轻松的内容管理
8. 无孔不入
9. 订阅能力
10. 开源
11. 反应
12. 表演
13. 编程接口应用程序（API）
14. 可量测性
15. WordPress 支持
16. 速度和效率

跟随我们这篇文章，向你展示如何在 AlmaLinux 8.4 上安装 WordPress。

### 在 AlmaLinux 8.4 上安装 WordPress 的先决条件

在这一节，我们想教你在 AlmaLinux 8.4 上安装 WordPress 的先决条件。应该注意的是，第一步是访问 root 用户帐户（或使用 root 权限访问管理员帐户）。

首先，您需要使用下面的命令作为主用户通过 SSH 登录到您的 AlmaLinux 8.4 服务器。注意，在下面的命令中，您必须用相应的 IP 地址和您的 SSH 端口号替换“IP 地址”和“端口号”：

```bash
ssh [[email protected]](/cdn-cgi/l/email-protection)_Address -p Port_number
```

然后，您需要使用以下命令来更新系统：

```bash
dnf update -y
```

现在，您应该通过运行以下命令来验证操作系统的当前版本：

```bash
cat /etc/os-release
```

完成上述步骤后，我们现在到达 LAMP 安装阶段。首先，您需要使用以下命令安装 Apache Web 服务器、MariaDB 服务器、PHP 和其他包：

```bash
dnf install httpd httpd-tools mariadb-server php php-json php-mysqlnd php-json php-curl unzip -y
```

现在，您应该能够使用以下命令启动 Apache 和 MariaDB 服务，并启用它们来重启系统：

```bash
systemctl start httpd
```

```bash
systemctl enable httpd
```

```bash
systemctl start mariadb
```

```bash
systemctl enable mariadb
```

### 如何创建 WordPress 数据库

要在第一步为 WordPress 创建一个数据库，你必须使用下面的命令登录 MariaDB：

```bash
mysql
```

接下来，您需要使用以下命令创建数据库和用户：

```sql
MariaDB [(none)]> CREATE DATABASE wpdb;
```

```sql
MariaDB [(none)]> CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'password';
```

通过执行下面的命令，您可以授予 WordPress 数据库所有的特权：

```sql
MariaDB [(none)]> GRANT ALL ON wpdb.* TO 'wpuser'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

最后，您需要使用以下命令清除特权并退出 MariaDB：

```sql
MariaDB [(none)]> FLUSH PRIVILEGES;
```

```sql
MariaDB [(none)]> EXIT;
```

## 在 AlmaLinux 8.4 上安装 WordPress

在这一节，我们将讨论如何在 AlmaLinux 上安装 WordPress。为此，您必须遵循以下步骤。首先，将目录更改为 Apache Web 根目录，并使用以下命令下载 WordPress 的最新版本：

```bash
cd /var/www/html
```

```bash
wget https://wordpress.org/latest.tar.gz
```

现在，您需要通过运行以下命令来提取下载的文件：

```bash
tar -xvzf latest.tar.gz
```

接下来，您需要将目录更改为 WordPress，并使用以下命令重命名示例配置文件：

```bash
cd wordpress
```

```bash
mv wp-config-sample.php wp-config.php
```

现在，您需要通过运行以下命令来编辑示例配置文件，然后定义您的数据库设置：

```bash
nano wp-config.php
```

打开配置文件后，您需要更改以下值：

```php
define( 'DB_NAME', 'wpdb' );
```

```php
/** MySQL database username */
define( 'DB_USER', 'wpuser' );
```

```php
/** MySQL database password */
define( 'DB_PASSWORD', 'password' );
```

```php
/** MySQL hostname */
define( 'DB_HOST', 'localhost' );
```

最后，您需要使用以下命令保存文件，然后在 WordPress 目录上设置适当的所有权：

```bash
chown -R apache:apache /var/www/html/wordpress
```

### 如何在 AlmaLinux 8.4 上配置 WordPress

在这一节，我们想讨论如何在 AlmaLinux 上配置 WordPress。第一步是配置 Apache。为此，您需要使用以下命令为 WordPress 创建一个 Apache 虚拟主机配置文件：

```bash
nano /etc/httpd/conf.d/wp.conf
```

在用您想要的文本编辑器之一打开配置文件之后，您现在需要向它添加以下行：

```apache
<VirtualHost *:80>
    ServerAdmin [[email protected]](/cdn-cgi/l/email-protection)
    DocumentRoot "/var/www/html/wordpress"
    ServerName wp.example.com
    ErrorLog "/var/log/httpd/example.com-error_log"
    CustomLog "/var/log/httpd/example.com-access_log" combined

    <Directory "/var/www/html/wordpress">
        DirectoryIndex index.html index.php
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

配置完 Apache 后，您必须使用下面的命令保存文件，然后重启 Apache 以应用更改：

```bash
systemctl restart httpd
```

下一步是配置防火墙。为此，您必须使用以下命令通过防火墙启用端口 80 和 443：

```bash
firewall-cmd --permanent --zone=public --add-service=http
```

```bash
firewall-cmd --permanent --zone=public --add-service=https
```

在最后一步中，您可以通过运行以下命令应用更改来重新加载防火墙：

```bash
firewall-cmd --reload
```

### 如何在 AlmaLinux 8.4 上访问 WordPress

在前面的章节中，我们向您展示了如何在 AlmaLinux 上安装和配置 WordPress。现在我们想教你如何访问 WordPress 管理面板。为此，您必须遵循以下步骤。

您可以通过在浏览器中输入以下 URL 来访问 WordPress 安装向导：

```text
http://wp.example.com
```

运行上述命令将带您进入下一页。下一步，你需要选择你想要的语言，然后点击继续按钮：

![language-selection](img/954ab44e1a3f6cebd72b853595d70d97.png)

在前面的部分中选择了您想要的语言后，现在您需要输入网站名称、管理员用户名和密码。然后点击安装按钮：

![website-installation-form](img/ff184c42e07c21a7ba254a0a189a5573.png)

如下图所示，您必须点击登录按钮：

![succesfull-installation-screen](img/7567b052c05540c1df6ba5e8989b4358.png)

点击登录按钮后，你将被重定向到 WordPress 管理登录页面：

![login-screen](img/eb253105596241009b432d476083d591.png)

最后一步，你必须输入你的用户名和密码，点击登录按钮。通过这样做，你会看到管理面板：

![wordpress-Admin-Panel](img/ae214cb1cca60bb7c5b6a841ed024851.png)

## 结论

WordPress 从一个活跃的、真诚的开源社区开始，可以帮助你建立一个伟大的网站并运行。在这篇文章中，我们试图一步一步地教你如何在 AlmaLinux 8.4 上安装 WordPress。
