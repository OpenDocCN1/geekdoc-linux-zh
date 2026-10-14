
```bash
matthew@semour:-$ openssl x509 -req -days 365 -in server.csr -signkey server.key --out server.crt
```

这将创建一个有效期为`365`天的证书。即使是供应商提供的证书，也有过期日期。应该定期更新证书，以让你的网站访问者对他们所面对的对象感到放心。

要将证书拷贝到它的正确位置，使用此命令：

```bash
matthew@semour:-$ cp server.crt /etc/ssl/certs/
```

要将密钥拷贝到它的正确位置，使用此命令：

```bash
matthew@semour:-$ cp server.key /etc/ssl/private/
```

接下来我们将编辑`default-ssl`文件，即`/etc/apache2/sites-available/default-ssl`，将这些值更改为我在这里显示的。这告诉`Apache2`使用`SSL`以及在哪里找到正确的证书和密钥文件：

```apache
SSLEngine on
SSLCertificateFile /etc/ssl/certs/server.crt
SSLCertificateKeyFile /etc/ssl/private/server.key
```

要使用带有自签名证书和密钥文件的编辑后的默认配置来为`Apache2`配置`HTTPS`，请使用此命令：

```bash
matthew@semour:-$ sudo a2ensite default-ssl
```

并重启`Apache2`：

```bash
matthew@semour:-$ service apache2 restart
```

## 参考文献

在重启期间，你会被要求输入证书密钥的密码。在要求时输入它。你现在有了一个安全的、适用于内部使用的服务器，但并不适用于面向客户的生产环境。

如果你打算托管一个专业网站，最好的做法是使用经过认证的`CA`（证书颁发机构）。每个`CA`都有他们偏好的方法，因此你应该在开始之前阅读他们的要求。基本流程通常如下：

- 1. 创建一对私钥和公钥加密密钥对。
- 2. 基于公钥创建证书。
- 3. 创建一个包含你的服务器和托管该服务器的公司信息的证书请求。
- 4. 将你的证书请求和公钥连同公司身份证明和付款证明发送给`CA`。
- 5. 他们验证请求和你的身份，并返回一个类似于我们创建的自签名证书的证书，但由`CA`签名。
- 6. 你将该证书安装到服务器上并配置`Apache2`使用它。

`CA`签名的证书具有优势。首先，浏览器内置了大多数`CA`机构的数据，大多数情况下，它们会自动识别来自其中一个机构的签名。自签名证书会导致浏览器显示一个（对非技术人员来说）看起来相当可怕的警告，并要求用户绕过它才能查看你的网站。此外，如果`CA`签发了签名证书，他们就保证了提供网页的组织的身份。

要了解更多关于证书和密钥的知识，包括密钥和证书的安装...

# 安装 Nginx 服务器

当请求到达时，并不是启动一个新进程，而是“监听器”向服务器的另一个部分（称为“事件处理程序”）发送消息，然后由其执行任务。通过这种方式提供网页服务的简化结果是需要更少的处理器时间和内存。使用这种方法存在固有的巨大困难，其中最显著的可能是代码复杂性增加，这可能会使得修复漏洞、添加功能以及让新手（甚至是对于熟悉同一代码库但离开了一段时间的老手兵）对代码的理解都变得更加困难。

`Nginx`的设计使其能够良好地扩展，从一台小型、低功耗的服务器到包含许多服务器的大型网络。

配置方面，`Nginx`使用了一套虚拟主机系统，类似于`Apache`，但使用的是一组类似的配置文件。它们之间的区别是语义上的，并不非常困难。你可以在`Nginx`中使用完全不同的语法来创建`URL`重写。此外，它没有与`Apache`类似的重写条件（`rewrite conditions`）的功能。虽然偶尔会有博客文章和网络教程提供一些可以处理某些常见形式的变通方案，但如果你经常需要此类操作，你可能不会选择`Nginx`。

许多人在`Apache`中使用的一个缺失文件是`.htaccess`。`Nginx`中没有类似的东西，因此如果你需要在不重启服务器的情况下更改重写或配置的权限，那么你就无从为力了。这可能是导致你不使用提供`Nginx`的共享托管的主要原因。

最后，另一个文档详尽的选项是同时使用`Apache`和`Nginx`，其中`Apache`处理所有的静态和动态请求，而`Nginx`处理所有的静态请求。这比单独使用`Apache`更快、更轻量，但也带来了复杂性的负担以及随之增加的潜在问题。

## 安装方式

你可以通过`APT`安装`Nginx`，也可以从源码自行编译。`Nginx`源码可以在任何类`Unix`操作系统和`Win32`上编译。

如果你正准备安装新版本的`Nginx`，请先关闭旧服务器。即使旧服务器不太可能干扰安装过程，但关闭它可以确保不会出现问题。

### 从 Ubuntu 存储库安装

你可以从`Ubuntu`存储库安装`nginx`软件包。更新后的包通常包含重要的漏洞修复和安全修复。当发布了更新版本时，请尽快安装它以保持你的系统安全。

有关如何从`Ubuntu`存储库安装软件的更多信息，请参阅第`9`章“管理软件”。

### 自行编译源码

你可以直接从`http://wiki.nginx.org/Install`下载源码。

获取`tar`包后，你必须在临时目录（如`/tmp`）中打开它。打开此`tar`包会创建一个名为`nginx_version_number`的目录，其中`version_number`是你下载的版本（例如`nginx_1.4.4`）。

#### 提示

由于许多`Linux`及其他操作系统的软件包以源码形式分发，提取源码后生成的目录会包含一个`README`和一个`INSTALL`文件。在尝试编译和安装软件之前，请务必仔细`INSTALL`文件。

#### 使用 ./configure 编译 Nginx

要编译`Nginx`，请在刚刚创建的目录下运行`./configure`脚本。使用此命令：

```
matthew@semour:-$ ./configure
```

该文件会生成所谓的`Makefile`，用于编译源代码。

接下来，运行`make`来编译服务器代码。

```
matthew@semour:-$ make
```

编译完成后，安装服务器。这可能需要使用管理员权限完成。

```
matthew@semour:-$ sudo make
```

#### 提示

强烈建议你使用`Ubuntu`版本的`Nginx`，直到你真正了解系统启动时发生了什么。从源码安装`Nginx`时没有“卸载”选项！在本章的剩余部分，我们假设你通过这种方式安装了`Nginx`。如果你是从源码安装，应该检查`Nginx`文档，因为可能与我们在此描述的内容有所不同。

# 配置 Nginx 服务器

你现在可以配置服务器了。`Nginx`最常用的运行方式是使用虚拟主机，就像现在大多数人使用`Apache`的方式一样。过程类似，主要是语法上的差异。

如果你使用包管理器安装，`Nginx`的所有配置文件都位于`/etc/nginx`。主配置文件是`/etc/nginx/nginx.conf`。以下是该文件的示例：

```
user www-data;
worker_processes 1;
```

```
# error_log /var/log/nginx/error.log;
```

```
events {
    worker_connections 1024;
}
```

```
http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    access_log /var/log/nginx/access.log;

    sendfile on;

    tcp_nopush on;
    #tcp_nodelay on;

    keepalive_timeout 0;
    keepalive_timeout 65;

    gzip on;

    include /etc/nginx/sites-enabled/*
}
```

`nginx.conf`文件包含以下部分：

- `user`——设置运行`Nginx`的系统用户。默认配置为：`www-data;`
- `worker_processes`——允许`Nginx`产生多少进程。默认值`1`对于大多数用户来说足够了，但你可以谨慎尝试：`4`。
- `error_log`——在我们的示例中被注释掉了。你可以通过取消注释来设置错误日志的位置。

# 第24 章 Nginx 服务器管理

`events`和`worker_connections`——此设置调整了每个进程允许的连接数。`worker_connections`的值将给出允许连接到服务器的最大并发数。内存决定了服务器是否能处理更多连接，因此保持默认设置即可。

`http`——此部分包含`http`的基础设置：
