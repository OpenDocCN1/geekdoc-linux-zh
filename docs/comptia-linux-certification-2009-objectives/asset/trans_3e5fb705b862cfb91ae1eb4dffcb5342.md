

## 活动 13-1
### 配置 Web 服务器

**开始前准备：**

- 在 srvA 上，您已以 root 身份登录到 GUI。
- 终端窗口已显示。
- 输入 `cd /root` 导航到根目录。
- 在终端窗口中，将 `english.html` 文件和 `Our Global Company_files` 目录从 `/085039Data/Web_Services` 目录复制到 `/var/www/html` 目录。
- 清空终端窗口。

**场景：**

您的公司运营着一家连锁零售商店，并希望建立一个在线网络商店，该商店将提供商店信息并促进在线购物。现在，您想要配置 web 服务器以促进 web 托管。此外，您希望以这样一种方式配置 web 服务器，即网站中包含 PHP 页面。

### 操作步骤

| 步骤 | 操作 |
| :--- | :--- |
| 1. | 检查系统上是否已安装 httpd。 |
| a. | 验证系统上是否已安装 apr 软件包。 |
| b. | 验证系统上是否已安装 postgresql-libs 软件包。 |
| c. | 验证系统上是否已安装 apr-util 软件包。 |
| d. | 验证系统上是否已安装 httpd 软件包。 |
| e. | 清空终端窗口。 |
| 2. | 在系统上启用 PHP 支持。 |
| a. | 输入 `yum localinstall /rhelsource/Server/=> php-common-5.1.6-23.el5.i386.rpm` 安装 php-common 软件包。 <br> **注意：** 该步骤中使用的 `=>` 符号仅用于将步骤移至下一行。它不是代码的一部分，因此学生无需输入该符号。 |
| b. | 输入 `yum localinstall \ /rhelsource/Server/=> \ php-cli-5.1.6-23.el5.i386.rpm` 安装 php-cli 软件包。 <br> **注意：** 该步骤中使用的 `⇒` 符号仅用于将步骤移至下一行。它不是代码的一部分，因此学生无需输入该符号。 |
| c. | 输入 `yum localinstall \ /rhelsource/Server/=> \ php-5.1.6-23.el5.i386.rpm` 安装 php 软件包。 <br> **注意：** 该步骤中使用的 `⇒` 符号仅用于将步骤移至下一行。它不是代码的一部分，因此学生无需输入该符号。 |
| d. | 清空终端窗口。 |
| 3. | 为 web 服务器指定别名。 |
| a. | 导航到 /var/named 目录。 |
| b. | 使用 vi 编辑器打开 ogc.forward 文件。 |
| c. | 在文件末尾输入 `www IN CNAME srvA` 以添加 CNAME 记录。 |
| d. | 按 Esc 键切换到命令模式。 |
| e. | 保存并关闭该文件。 |
| f. | 重启 named 服务。 |
| g. | 清空终端窗口。 |
| 4. | 配置 web 服务器以允许 web 托管。 |
| a. | 导航到 /etc/httpd/conf 目录。 |
| b. | 使用 vi 编辑器打开 httpd.conf 文件。 |
| c. | 定位行“#ServerName www.example.com:80”，并将其更改为 **ServerName www.ourglobalcompany.com:80** |
| d. | 按 **Esc** 键切换到命令模式。 |
| e. | 定位 “<Directory “/var/www/html”>” 语句。 |
| f. | 在 <Directory “/var/www/html”> 语句中定位行 **AllowOverride None**。 |
| g. | 将 **AllowOverride None** 参数更改为 **AllowOverride AuthConfig** |
| h. | 按 **Esc** 键切换到命令模式。 |
| i. | 定位行 “DirectoryIndex index.html index.html.var”，并将其更改为 **DirectoryIndex english.html english.html.var** |
| j. | 按 **Esc** 键切换到命令模式。 |
| k. | 保存并关闭该文件。 |
| l. | 清空终端窗口。 |
| 5. | 启动 httpd 服务以应用配置更改。 |
| a. | 输入 **service httpd start** 以启动 httpd 服务。 |
| b. | 输入 **chkconfig httpd on** 以便在系统启动时启动 httpd 服务。 |
| c. | 清空终端窗口。 |
| 6. | 访问您设置的网站。 |
| a. | 输入 `firefox http://ourglobalcompany.com` 在 Firefox 浏览器中打开网站。 |
| b. | 观察 Mozilla Firefox 网页浏览器中显示 Our Global Company 的主页。 |
| c. | 关闭网页浏览器窗口。 |
| d. | 清空终端窗口。 |

## 主题 B
### 实施 Apache 访问控制

您已配置了一个 web 服务器。您可能需要在单个 web 服务器上托管多个网站，并对其进行保护以限制未经授权的访问。在本主题中，您将实施 Apache 访问控制。

您的组织可能有供员工使用的内部网站。由于访问内部网站的用户数量与互联网网站相比会少得多，因此您决定将这两个网站托管在同一台服务器上。为此，您需要使用安全方法来隔离这两个网站的数据。作为系统管理员，确保存储在服务器上的数据的一般安全性也是必不可少的。因此，您需要具备适当设置访问控制的技能。

### 虚拟主机

![](img/477ccb2f05b6ba1b2d563ea74f18c197_645_0.png)

**定义：**
*虚拟主机* 是一种允许管理多个域名的系统。它可以拥有多个域名或 IP 地址。虚拟主机可以基于名称或基于 IP。使用 `VirtualHost` 指令来定义虚拟机。诸如 IP 地址、网页信息、日志格式和域名等详细信息在 httpd.conf 文件中指定。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_645_1.png)

*图 13-12：由 virtualhost 系统管理的域名列表。*

### 基于 IP 的虚拟托管

基于 IP 的虚拟托管使系统能够托管基于 IP 地址的多个网站。服务器将被分配多个 IP 地址，每个 IP 地址将指向一个网站。要定义基于 IP 的虚拟主机，需要在 `VirtualHost` 指令中指定 web 服务器的 IP 地址。

### 基于名称的虚拟托管

基于名称的虚拟托管是一种系统可以基于主机名托管多个网站的方法。在这种方法中，许多主机可以拥有相同的 IP 地址。这种方法更适合同时在同一个 web 服务器上托管多个网站。服务器将被分配多个主机名，每个主机名将指向一个网站。可以使用 `NameVirtualHost` 指令配置基于名称的虚拟托管。需要提供服务的主机的 IP 地址在 `NameVirtualHost` 指令中指定，前提是这些 IP 地址与服务器上的网络接口相关联。此外，可以使用 `Listen` 或 `BindAddress` 指令使服务器监听或限制 `NameVirtualHost` 指令中指定的 IP 地址。`NameVirtualHost` 指令之后是 `VirtualHost` 指令，该指令为每个需要提供服务的主机定义。

### 传输层安全协议

**定义：**

*传输层安全协议 (TLS) 是安全套接字层 (SSL) 的第三个版本，它提供了服务器和客户端之间的安全通信协议。TLS 在服务器和客户端之间建立安全通信通道，然后加密所有需要通信的数据。TLS 使用密码学提供身份验证并安全传输数据。`mod_ssl` 是用于在 Apache 服务器上启用 TLS 和 SSL 的 Apache 模块。`ssl.conf` 配置文件存储在 `/etc/httpd/conf.d` 目录中。它用于为 Apache 服务器提供 TLS 支持。*

![](img/477ccb2f05b6ba1b2d563ea74f18c197_646_0.png)

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_646_1.png)

*图 13-13：服务器和客户端之间的安全通信。*

### 数字证书

*数字证书是用于验证属于个人或公司的特定公钥的数字文档。它包含个人或公司的名称、序列号、过期日期、证书持有者公钥的副本以及证书颁发机构的数字签名。数字证书可以是自签名的，也可以由证书颁发机构 (CA) 签名。设置安全 web 服务器时需要使用它们。数字证书存储在 `/etc/pki/tls/certs` 目录中。*

![](img/477ccb2f05b6ba1b2d563ea74f18c197_646_2.png)

