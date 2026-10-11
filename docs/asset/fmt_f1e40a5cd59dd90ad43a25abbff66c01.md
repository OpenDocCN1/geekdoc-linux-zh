
> 注意：除非您已经创建了该目录，否则您将收到一个关于 `public_html` 不存在的警告。请以拥有该网站的用户身份运行 `mkdir ~/public_html` 来创建它。

可以通过重复 `VirtualHost` 块并重复配置测试 `configtest` 和重载 `graceful` 步骤添加额外的虚拟主机。

# 第 V 部分 运行服务器

> 注意
您可能想为了方便，将各个虚拟主机放在单独的文件中。然而，您应该小心将您的主虚拟主机放在一个其他文件之前读取的文件，因为第一个虚拟主机将接收那些与您的配置中任何项都不匹配的主名的请求。在商业 Web 托管环境中，通常会创建一个特殊的默认虚拟主机，其中包含一条错误消息，指示由于未配置任何网站。

# 用户内容与 UserDir 设置

在您无法为每个想要提供 Web 空间的用户设置虚拟主机的情况下，您可以轻松地使用 Apache 中的 `mod_userdir` 模块。每个用户家目录下的 `public_html` 目录都可以通过 `http://~/servername/~username/` 供 Web 访问。例如，在 `www.example.com` 上的名为 `wtucker` 的用户将 Web 内容存储在 `/home/wtucker/public_html` 中。该内容可以通过 `http://www.example.com/~wtucker` 访问。

# 安装 Web 应用：Coppermine Photo Gallery

一旦您的 LAMP 服务器运行，您就可以开始安装或创建运行其上的应用程序。其中一个应用程序就是 Coppermine Photo Gallery `CPG`，本节将演示其安装过程。`CPG` 是一个用 PHP 编写的 Web 相册管理系统。通过它的界面，您可以将照片上传到自己的相册中，这些将通过您的 LAMP 服务器在 Web 上可用。

您可以在虚拟主机下或主主机上的用户家目录下安装 `CPG`。使用这两种方法中的一种，单个服务器都可以轻松支持多个 `CPG` 安装。

要在在本章描述的 Debian 系统上安装 `CPG`，请遵循以下步骤：

- 1. 安装 `unzip` 和 `imagemagick` 程序。`unzip` 用于在下载后解压包，`imagemagick` 用于调整图像大小和创建缩略图：
```
# apt-get install imagemagick
```
- 2. 为 `CPG` 创建一个 MySQL 数据库。如果您愿意，可以使用 `cpg` 以外的数据库名称。数据库用户名 `GRANT` 语句中 `@localhost'` 之前的部分 和数据库名称不匹配。确保将 `mypassword` 替换为其他内容：
```
# mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or g.
Your MySQL connection id is 8 to server version:
4.0.24_Debian-10-log
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
```

# 运行 Linux, Apache, MySQL, and PHP (LAMP) 服务器

```
mysql> CREATE DATABASE cpg;

Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON cpg.* TO 'cpg'@'localhost' IDENTIFIED BY 'password';

Query OK, 0 rows affected (0.00 sec)
```

```
mysql> \a

Bye
```

- 3. 以将拥有 `CPG` 安装的用户身份登录，并从互联网下载最新版本：
```bash
$ mkdir -p /public/html

$ cd /public/html

$ wget http://dl.sourceforge.net/sourceforge/coppermine/cpg1.4.10.zip

--19:30:46-- http://dl.sourceforge.net/sourceforge/coppermine/cpg1.4.10.zip
=> 'cpg1.4.10.zip'
```

- 4. 解压包：
```bash
$ unzip cpg1.4.10.zip
```

- 5. 重命名解压的目录并设置权限：
```bash
$ mv cpg-1.4.10 cpg

$ chmod -R 777 cpg
```

- 6. 在虚拟主机 或主主机 中配置 Apache 配置：
```bash
# apachectl configtest

Syntax OK

# apachectl graceful
```

- 7. 在浏览器中访问 `http://www.example.com/cpg/install.php` 根据您的设置替换域名 并完成安装向导 此处省略原文中具体的步骤描述翻译，保持逻辑一致：
在浏览器中访问 `http://www.example.com/cpg/install.php` 并按照提示完成 `CPG` 的安装配置。

- 8. 安装完成后，访问 `http://www.example.com/cpg` 即可使用管理员账户登录登录并开始管理您的相册。

# 第五部分 运行服务器

遇到问题时，首先使用 `apachectl` 程序并配合 `configtest` 参数来测试配置。事实上，养成在每次更改配置后运行它的习惯是一个好主意：
```
# apachectl configtest

Syntax OK

# apachectl graceful
/usr/sbin/apachectl: httpd gracefully restarted
```

如果发生语法错误，`apachectl` 会指示错误发生的位置，并尝试对问题的性质提供提示。随后你可以使用平滑重启选项 `apachectl graceful` 来指示 Apache 重新加载配置，而不会断开任何活动的连接。

`apachectl` 中的平滑重启选项在向 apache 发送加载信号之前会自动测试配置，但在进行任何配置更改后，养成手动运行配置测试的习惯仍然是一个主意。

> 注意

某些问题可能通过了 `apachectl` 执行的语法测试，但随后会导致 HTTP 守护进程在重新加载配置后立即退出。如果发生这种情况，请使用 `tail` 命令捕获 Apache 的错误日志以获取有用信息。在 Debian 系统上，错误日志位于 `/var/log/apache/error.log`。在其他系统中，可以通过查找 Apache 配置中的 `ErrorLog` 指令找到它的位置。

你可能会遇到类似这样的错误消息：
```
[crit] (98)Address already in use: make_sock: could not bind to port 80
```

此错误通常表示有其他内容绑定到了端口 80 除非你尝试安装了另一个 Web 服务器，否则并不常见，或者另一个进程已经在运行 `apachectl` 捕到了它，或者你在多个地方告诉了 Apache 绑定相同的 IP 地址和端口组合。

你可以使用 `netstat` 命令查看处于 `LISTEN` 状态的 TCP 端口程序列表 包括 Apache：
```
# netstat -nltp

Active Internet connections (only servers)
Proto Local Remote Address State PID/Program name
tcp 0.0.0.0:80 0.0.0.0:* LISTEN 2105/apache
```
