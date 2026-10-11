
在安装 WordPress 之前，根据你的 VPS 或虚拟机的安装情况，你可能需要安装几个包。使用以下操作确保你已具备正确的配置。

我们需要加载的第一项是 `php-gd`。WordPress 和其他平台需要它来正确缩放缩略图。我们可以通过以下命令安装它：

```
sudo yum install php-gd
```

在提示时请务必输入密码并按 `y`。

为了让 Apache 看到新模块，我们需要重启 `httpd`。

```
sudo service httpd restart
```

现在我们还需要另外几个包。第一个是 `wget`。`Wget` 是一个从网络服务器收集内容的程序。它允许我们从网络下载文件到服务器。要安装 `wget`，请使用以下命令：

```
sudo yum install wget
```

同样，在提示时请务必输入密码并按 `y`。

我们下一个用于简化流程的工具叫做 `rsync`。`Rsync` 是一个允许我们在计算机系统上保留文件副本并将文件同步到其他文件夹的实用程序。要安装 `rsync`，请使用以下命令：

```
sudo yum install rsync
```

### 下载 WordPress

我喜欢教程中使用 WordPress 的原因之一是它可以配置新用户，而且 WordPress 团队始终在同一个链接处提供软件的最稳定版本。

在继续之前，确保你处于主目录。记住，你可以随时在 CLI 中输入 `cd` 回到主目录。

现在我们确认位于主目录，可以使用以下命令使用 `wget` 获取最新版本的 WordPress：

```
wget http://wordpress.org/latest.tar.gz
```

这会下载 WordPress 的压缩版本，我们现在需要使用 `tar` 命令对其进行解压。在 Linux 中，`tar` 代表“tape archive”（磁带存档），源于大多数系统管理员会将文件备份到磁带驱动器的时代。对于我们的目的，它允许我们从下载中收集压缩文件并将其提取到主目录。我们可以通过以下命令实现：

```
tar xvzf latest.tar.gz
```

在你的主文件夹中，现在会有一个名为 `wordpress` 的目录。要完成安装，我们需要将文件移动到 Apache 文档根目录 `/var/www/html`。使用方便的 `rsync` 工具，这非常简单。使用以下命令将文件同步到 Apache 目录。

```
sudo rsync -avP ~/wordpress/ /var/www/html/
```

记住，大小写很重要。该命令中的微小错误就可能导致你后续操作出现问题。命令运行后，`rsync` 将执行工作并将所有文件复制到 `/var/www/html` 目录。

我们还有一件事要做，我们需要为 WordPress 创建一个 `uploads` 文件夹来存储文件。使用我们之前使用的 `mkdir` 命令可以让这变得简单。

```
sudo mkdir /var/www/html/wp-content/uploads
```

### 更改所有权、权限和编辑文件的回顾

现在我们有两个步骤来完成正确的配置。我们需要更改 WordPress 文件和文件夹的所有权。这将提高安全性并允许 WordPress 按预期运行。为了做到这一点，我们将使用书中用过的 `chown` 命令。

```
sudo chown -R apache:apache /var/www/html/*
```

| 更改 Apache Web 目录的所有者 |
| :--- |
| 命令 | `sudo chown -R apache:apache /var/www/html/*` |
| 结果 | 系统将更改 `/var/www/html` 及其子目录的所有权 |
| 命令行显示 | `[tidus@centos:~]$ sudo chown -R apache:apache /var/www/html/*`\n`password for tidus:`\n`[tidus@centos:~]$` |

现在我们的最后一步是配置 WordPress 文件，通过它连接到我们创建的数据库。确保你记得我们设置的数据库名称、用户名和密码。

首先，我们需要切换到 `/var/www/html` 目录。

| 切换目录 |
| :--- |
| 命令 | `cd /var/www/html` |
| 结果 | 系统将带我们进入 html 目录 |
| 命令行显示 | `[tidus@centos:~]$ cd /var/www/html [tidus@centos: html]$` |

WordPress 使用名为 `wp-config.php` 的文件连接数据库。在安装过程中，提供了一个示例文件。我们需要复制该文件并用我们的数据库对其进行配置。

| 复制文件 |
| :--- |
| 命令 | `sudo cp wp-config-sample.php wp-config.php` |
| 结果 | 系统将文件复制为所需名称的新文件 |
| 命令行显示 | `[tidus@centos: html]$ sudo cp wp-config-sample.php wp-config.php [tidus@centos: html]$` |

现在我们有了一个可以修改的配置文件，可以使用 `nano` 进行编辑。

```
sudo nano wp-config.php
```

我们在该文件中对数据库连接所需的唯一修改是针对以下字段：`DB_NAME`、`DB_USER`、`DB_PASSWORD`。这将允许网站与数据库通信。请查看下一页获取我的配置示例。

**注意：你不应该将 password 作为密码，它在书中仅作为指南。**

### WP-Config.php 配置

```
/** WordPress 数据库名称 */
define('DB_NAME', 'wordpress');

/** MySQL 数据库用户名 */
define('DB_USER', 'wpuser');

/** MySQL 数据库密码 */
define('DB_PASSWORD', 'password');
```

这些是你应该在该文件中更改唯一值。完成后，在 `nano` 中关闭并保存更改。

### 通过浏览器访问 WordPress

我们最后需要完成的步骤是通过浏览器访问 WordPress。要做到这一点，请在浏览器中输入你的 IP 地址 `http://myipaddress`。你应该会看到一个与页面类似的屏幕。

![](img/373347a8cccfab65b3dc27644fdd6a60_106_0.png)

填写网站所需的信息，然后点击“Install WordPress”（安装 WordPress）按钮。这将确认安装并自动为你在数据库中创建表。

要继续操作，请点击页面底部的“Login”（登录）按钮。

现在，你的 CentOS 服务器上已经运行起了一个正常工作的 WordPress 系统了。

# 第 14 章

## 结语

恭喜你！在不到 85 页的内容里，我们已经掌握了一些 CentOS 7 的基础知识，并利用这些信息构建了一个基础 Web 服务器。

当然，还有许多内容需要学习，但这仅仅是一个开始。随着你不断地进行实验和学习，本指南将让你熟练在 CentOS 7 上进行导航和安装软件包。希望现在使用命令行界面已经不再那么可怕了。

如果你对进一步学习有任何问题，请随时发送邮件至 `info@nathanemail.com` 联系我。

感谢，并祝你在后续的学习道路上顺利！
