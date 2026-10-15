
# 如何在 Ubuntu 20.10 上安装 Nagios 监控

> 原文：<https://blog.eldernode.com/install-nagios-monitoring-on-ubuntu-20-10/>

![How To Install Nagios Monitoring on Ubuntu 20.10](img/13c218e5697893099ac33356ae3bea4a.png)

在接下来的[监控工具](https://blog.eldernode.com/website-and-server-monitoring-tools/)教程中，我们将展示 Nagios 安装指南。在任何 Linux 操作系统上，都可以运行这个开源的网络监控系统。因为 Nagios 提供了关键参数的概述，所以您更喜欢在[命令行](https://blog.eldernode.com/linux-server-monitoring-commands/)界面或基于 Web 的图形界面中工作。一旦确定了能够修复检测到的网络或服务器问题的关键级别，管理员就会收到电子邮件和文本消息作为警报通知。准备好你自己的 [Linux VPS](https://eldernode.com/linux-vps/)，继续和我们一起学习如何在 Ubuntu 20.10 服务器上安装 Nagios Monitoring。

为了让本教程更好地发挥作用，请考虑下面的先决条件：

- 一个拥有 `sudo` 权限的非根用户。

## 在 Ubuntu 20.10 上安装 Nagios 监控

为了维护系统和服务的安全性和可用性，您需要监控工具的帮助，以防止对您的业务产生任何负面影响。使用 TCP 端口、SMTP、POP3、HTTP、NNTP、PING 等，Nagios 能够监视网络细节。准备好一个 [Ubuntu VPS](https://eldernode.com/ubuntu-vps/) 之后，你就可以下载并安装 Nagios 了。让我们通过这个指南的步骤来学习和完成它。

### 更新您的系统

出于一些安全考虑，最好更新您的系统：

```bash
sudo apt-get update
```

注意：如果你最近安装了 Ubuntu 系统，你需要 [Apache](https://blog.eldernode.com/apache-web-server-ubuntu-20/) 和 [PHP](https://blog.eldernode.com/install-and-configure-php-on-ubuntu-20-04/)。运行以下命令来安装它们：

```bash
sudo apt-get install wget build-essential unzip openssl libssl-dev
```

```bash
sudo apt-get install apache2 php libapache2-mod-php php-gd libgd-dev
```

### 创建 Nagios 用户

安装前的第一步是在您的系统中为 Nagios 创建一个新的用户帐户。使用下面的命令在您的系统中创建一个：

```bash
sudo adduser nagios
```

要将您创建的用户添加到一个组中，您需要首先为 Nagios 设置“nagcmd”创建一个组。然后，将您的“nagios”用户添加到 Apache 组。

```bash
sudo groupadd nagcmd
```

```bash
sudo usermod -a -G nagcmd nagios
```

```bash
sudo usermod -a -G nagcmd www-data
```

### 安装 Nagios 核心服务

是时候安装 Nagios 核心了。可以从[官方网站](https://www.nagios.org/downloads/)免费领取最新版本的 Nagios core。

```bash
cd /opt/
```

```bash
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.5.tar.gz
```

然后，要将文件移动到您选择的位置，通过运行以下命令提取文件：

```bash
tar xzf nagios-4.4.5.tar.gz
```

解压缩完成后，使用下面的命令导航到“nagios”源目录并安装。这样就可以用 Ubuntu 编译 Nagios 了。

```bash
cd nagios-4.4.5
```

```bash
sudo ./configure --with-command-group=
```

```bash
sudo make all
```

```bash
sudo make install
```

```bash
sudo make install-init
```

```bash
sudo make install-daemoninit
```

```bash
sudo make install-config
```

```bash
sudo make install-commandmode
```

```bash
sudo make install-exfoliation
```

要为 Nagios Web 界面创建多个事件触发器，请在 `libexec` 目录下复制事件处理程序脚本。

### 设置 Apache 认证

要为 Nagios 服务器创建 Apache 配置文件，请运行：

```bash
sudo vi /etc/apache2/conf-available/nagios.conf
```

为了防止对配置进行更多的更改，请为用户 `nagiosadmin` 设置 Apache 身份验证：

```bash
htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```

然后，要使新设置生效，请启用 Apache 配置并重新启动 Apache 服务：

```bash
sudo a2enconf nagios
```

```bash
sudo a2enmod cgi rewrite
```

```bash
sudo service apache2 restart
```

### 更新您的电子邮件地址

您只需要运行下面的命令来编辑位于目录 `/usr/local/nagios/etc/objects` 中的 `contacts.cfg` 文件，以包含我们希望接收通知的电子邮件地址。

```bash
sudo gedit /usr/local/nagios/etc/objects/contacts.cfg
```

### 安装 Nagios 插件

在这一步，您应该下载最新的 `nagios-plugins` 源代码并安装。要执行此运行，请执行以下操作：

```bash
cd /opt
```

```bash
wget http://www.nagios-plugins.org/download/nagios-plugins-2.2.1.tar.gz
```

```bash
tar xzf nagios-plugins-2.2.1.tar.gz
```

```bash
cd nagios-plugins-2.2.1
```

要编译和安装 Nagios 插件，请键入：

```bash
sudo ./configure --with-nagios-user=nagios --with-nagios-group=nagios --with-openssl
```

```bash
sudo make
```

```bash
sudo make install
```

### 验证设置

要验证 Nagios 安装和配置文件，运行以下命令，然后就可以启动 Nagios 核心服务了。

```bash
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

```bash
service nagios start
```

要让 Nagios 在系统引导时自动启动，请通过运行以下命令来配置 Nagios：

```bash
sudo systemctl enable nagios
```

## 在 Ubuntu 上使用 Nagios

您可以通过运行以下命令来确保配置是否正确可见：

```bash
sudo /usr/local/nagios/bin/nagios -v
```

### 访问 Nagios Web 界面

如果您访问 `nagios` 服务器，就可以访问您的 `nagios` 设置。为此，您需要使用主机名或 IP 地址后跟 `/nagios`。

```text
http://eldernode.example.net/nagios/
```

这样，您已经验证了 Apache。用户名可以是 `nagiosadmin`，密码是您在设置 Apache 的身份验证步骤时创建的。

![Login page](img/1a2d8ef63b5dee5be3b41a3926155d57.png)

登录后，您可以查看如下所示的 Nagios 界面。也可以使用侧边栏按钮查看主机、服务和警报。

![The Dashboard of Nagios](img/02b30d9ccc8f207c650cbd1ac3325fa9.png)

## 结论

在本文中，您学习了如何在 Ubuntu 20.10 上安装 Nagios Monitoring。从现在开始，您可以使用这个最流行的工具来监控和解决您的服务器性能问题。如果您有兴趣了解更多信息，可以找到关于[的相关文章，介绍用于 Linux 的 Nagios 监控系统](https://blog.eldernode.com/nagios-monitoring-system-for-linux/)。
