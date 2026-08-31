
# 在 Ubuntu 20.04 中使用 Nginx 安装 WordPress 教程 - Eldernode

> 原文：<https://blog.eldernode.com/wordpress-installation-nginx-ubuntu20/>

![Tutorial WordPress installation with Nginx in Ubuntu 20.04](img/109785d6af9469aa0bb511fbf81c3bca.png)

最近你在 Ubuntu 20.04 上了解了 [Nginx](https://eldernode.com/install-nginx-on-ubuntu-20-04-lts/)。关注我们的教程，在 Ubuntu 20.04 中用 Nginx 安装 WordPress。由于 WordPress 平台是一个开源的内容管理系统，在本文中我们将让你更加熟悉这个广泛使用的软件，使用它强大的功能、漂亮的设计，最重要的是，它可以自由地创建你想要的任何东西。

## 教程：Ubuntu 20.04 中用 Nginx 安装 WordPress

要安装 WordPress，你必须在你的 Ubuntu 20.04 服务器上安装 LEMP 堆栈。

### 在 Ubuntu 20.04 中安装 WordPress

**1-** 当您的服务器上有一个 LEMP 堆栈时，您需要使用 [wget command](https://linuxize.com/post/wget-command-examples/) 从 WordPress 的官方网站下载并设置它。

```
http://wordpress.org/latest.tar.gz
```

**同样，参见**

**2-** 当您完成上一步后，使用 [tar command](https://eldernode.com/using-tar-command-on-linux/) 解压归档文件。

**3-** 此时，将 WordPress 文件夹中的内容复制到你网站的文件夹中(如 `mysite.com`)，该文件夹应存储在 web 服务器的 web 文档根目录下 ( `/var/www/html/` )。

**请注意**: 使用 `cp` 命令时，`mysite.com` 目录不一定要存在，会自动创建。

```
ls -l
sudo cp -R wordpress/ /var/www/html/mysite.com
ls -l /var/www/html/mysite.com/
```

**4-** 作为 webserver 用户和组 `www-data` 应该拥有它的读、写、执行权限，在网站目录 `/var/www/html/mysite.com` 上设置正确的权限。

```
sudo chown -R www-data:www-data /var/www/html/mysite.com
sudo chmod -R 775 /var/www/html/mysite.com
```

#### 为网站创建 WordPress 数据库

**5-** 现在，WordPress 需要一个数据库来进行网站数据存储。要提供它，为您的站点创建一个，使用 MySQL 命令登录到 **MariaDB** shell，使用 `-u` 选项提供用户名和 `-p` 作为密码，如果您作为根数据库用户访问，也可以使用 `sudo`。

```
sudo mysql -u root -p
OR
sudo mysql -u root		#this also works for root database user
```

**6-** 要创建你网站的数据库，在你访问数据库 shell 时使用以下命令。使用您想要的数据库用户和密码。

```
MariaDB [(none)]> CREATE DATABASE mysite;
MariaDB [(none)]> GRANT ALL PRIVILEGES ON mysite.* TO 'mysiteadmin'@'localhost' IDENTIFIED BY '[[email protected]]!';
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> EXIT;
```

**7-** 为你的新 WordPress 安装创建一个 `wp-config.php` 文件。在这里，您将定义数据库连接和一些其他参数。然后，进入网站的文档根目录 `/var/www/html/mysite.com` 并从默认提供的示例文件创建一个 `wp-config.php` 文件。

```
cd /var/www/html/mysite.com
sudo mv wp-config-sample.php wp-config.php
```

**同样，参见**

**8-** 创建后打开 `wp-config.php` 文件。

现在，你需要你的 WordPress 站点连接到你为它创建的数据库。因此，请修改数据库连接设置。

#### 为 WordPress 网站创建一个 NGINX 虚拟服务器块 (VirtualHost)

**9-** 此时，要在 **NGINX** 配置中为你的站点配置一个虚拟服务器块，让 **NGINX** 使用你的域名为客户提供你的网站服务。所以，在 `/etc/nginx/conf.d/` 目录下创建一个名为 `mysite.com.conf` 的文件。

```
sudo vim /etc/nginx/conf.d/mysite.com.conf
```

因此，将以下配置复制并粘贴到文件中。不要忘记用你的域名替换 `mysite.com` 和 `www.mysite.com`。

```
server {
        listen 80;
        listen [::]:80;
        root /var/www/html/mysite.com;
        index  index.php index.html index.htm;
        server_name mysite.com www.mysite.com;

        error_log /var/log/nginx/mysite.com_error.log;
        access_log /var/log/nginx/mysite.com_access.log;

        client_max_body_size 100M;
        location / {
                try_files $uri $uri/ /index.php?$args;
        }
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.4-fpm.sock;
                fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
}
```

**除了上述配置的**:

### 根据 `/etc/php/7.4/fpm/pool.d/www.conf` 池配置文件中 `listen` 参数的值的定义， `fastcgi_pass` 参数的值应该指向 **PHP-FPM** 正在监听的套接字。默认是一个 UNIX 套接字 `/run/php/php7.4-fpm.sock`。

**10-** 你应该考虑到 NGINX 通常会将所有请求路由到默认服务器，所以为了使你的新站点和你打算在同一服务器上建立的其他站点能够很好地加载，请删除**默认**服务器块文件。

```
sudo rm /etc/nginx/sites-enabled/default
sudo rm /etc/nginx/sites-available/default
```

**11-** 在重启 Nginx 服务以应用上述更改之前，请检查 **NGINX** 配置语法是否有任何错误。

```
sudo nginx -t
sudo systemctl restart nginx
```

### 通过网络安装程序完成 WordPress 的安装

**12-** 打开网页浏览器，用你的域名导航。使用 web 安装程序完成 WordPress 的安装。

```
http://mysite.com/
OR
http://SERVER_IP/
```

为安装过程选择您喜欢的**语言**，并在 web 安装程序加载后点击**继续**。

**13-** 如下图所示，是时候填写你的新网站所需的信息了。然后点击安装 WordPress。请注意，您随时可以在以后编辑这些信息。

**14-** 成功安装 WordPress 后，点击**登录**按钮进入网站管理员的仪表板。

**15-** 要访问您网站的管理仪表板，请在网站管理员的登录页面提供您在上面创建的用户名和密码，然后单击**登录**。

就是这样！您已经在 **Ubuntu 20.04** 中成功安装了最新版本的 **WordPress** 和 **NGINX**，开始构建您的新网站或博客。

亲爱的用户，我们希望这篇教程能对你有所帮助，如果你有任何问题或想查看我们的用户关于这篇文章的对话，请访问[提问页面](https://eldernode.com/ask)。也为了提高你的知识，有这么多有用的教程为[老年节点培训](https://eldernode.com/blog/)准备。
