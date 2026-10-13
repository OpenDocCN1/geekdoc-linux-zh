
## 图 14-6

浏览默认的 Apache 测试页面

![](img/9139201cfcaf4292284a0eed074928e5_780_0.png)

最后，Listen 指令定义此服务器的 IP 地址和 TCP/IP 端口。例如，下图所示的默认值意味着此服务器将与任何从计算机的任何 IP 地址在标准 TCP/IP 端口 80 请求网页的计算机一起工作：

```
Listen 80
```

如果本地系统上有多个 IP 地址可用，Listen 指令可用于将访问限制到一个特定的 IP 地址。例如，如果系统有两个网卡，其 IP 地址分别为 192.168.0.200 和 192.168.122.1，则以下指令可帮助将访问限制到 192.168.122.0 网络上的系统：

```
Listen 192.168.122.1:80
```

> 考试提示
> RHCE 目标建议您需要准备好配置常规 HTTP 和安全的 HTTPS 网站。

对于安全网站，/etc/httpd/conf.d 目录中的 ssl.conf 文件中有一个第二个 Listen 指令。此文件中的数据会自动并入整体 Apache 配置中，这得益于练习 14-2 中描述的指令。它包含以下指令，该指令指向 TCP/IP 的默认安全 HTTP（HTTPS）端口 443：

```
Listen 443
```

## 练习 14-2

### Apache 欢迎页面与 noindex.html 故事

在本练习中，您将追踪与 Apache Web 服务器关联的标准测试页面的故事，如图 14-6 所示。本练习假设 httpd 包已安装并且 Apache 服务正在运行。您还将看到当该网页的路径损坏时，会在 /var/www/html 目录中出现一堆测试文件的索引的情况。

- 1. 在 /etc/httpd/conf 目录中打开 httpd.conf 文件。找到以下行：`Include conf.d/*.conf`
- 2. 在同一文件中找到 ServerRoot 指令。它应如下所示：`ServerRoot /etc/httpd` 此外，请记下 `Alias /error/ "/var/www/error/"` 行。您很快需要这些信息。
- 3. 将这两个指令的效果结合起来。换句话说，`Include conf.d/*.conf` 指令将 /etc/httpd/conf.d 目录中 *.conf 文件的内容包含在 Apache 配置中。退出 httpd.conf 文件。
- 4. 导航到 /etc/httpd/conf.d 目录。打开 welcome.conf 文件。
- 5. 注意 ErrorDocument 页面。虽然它指向 /error/noindex.html 文件，但这是基于上述 Alias 指令。换句话说，您应该能在 /var/www/error 目录中找到 noindex.html 文件。
- 6. 查看 /var/www/error/noindex.html 文件。要在 ELinks 浏览器中打开它，请运行 `elinks /var/www/error/noindex.html` 命令。出现的网页现在应该很熟悉。
- 7. 退出浏览器。将 welcome.conf 文件从 /etc/httpd/conf.d 目录移动到备份位置。
- 8. 使用 `apachectl restart` 命令重启 Apache 服务。
- 9. 使用 elinks http://127.0.0.1 命令导航到 localhost 系统。你看到了什么？
- 10. 打开第二个终端，导航到 /var/www/html 目录，并运行 touch test1 test2 test3 test4 命令。
- 11. 在原始终端中重新加载浏览器。你看到了什么？
- 12. 退出浏览器。将 welcome.conf 文件恢复到 /etc/httpd/conf.d 目录。

## 练习 14-3

### 创建文件列表

在本练习中，您将设置一个文件列表以供访问您的 Web 服务器的其他人共享。过程相当简单；您将配置适当的防火墙，创建 DocumentRoot 的子目录，用多个文件填充它，设置适当的安全上下文，并激活 Apache。

- 1. 确保防火墙不会阻止对端口 80 的访问。一种方法是使用 Red Hat 防火墙配置工具，您可以使用 system-config-firewall 命令启动它。在“受信任服务”部分，确保允许传入的 WWW（HTTP）连接。或者，您也可以使用前面为自定义防火墙指定的说明。
- 2. 创建 DocumentRoot 的子目录。在默认的 /etc/httpd/conf/httpd.conf 文件中，它是 /var/www/html。对于本练习，我已创建 /var/www/html/help 目录。
- 3. 复制 /var/www/manual 目录中的文件：
  # cp -ar /var/www/manual/* /var/www/html/help/
- 4. 使用以下命令重启 Apache 服务：
  # apachectl restart
- 5. 确保下次启动时 Apache 会启动：
  # chkconfig httpd on
- 6. 使用 ls -Z /var/www/html 和 ls -Z /var/www/html/help 命令查看 /var/www/html/sharing 目录和复制文件的安全上下文。如果它与此处显示的上下文不对应，请使用以下命令设置它们：

```
# chcon -R -u system_u /var/www/html/sharing/
# chcon -R -t httpd_sys_content_t /var/www/html/sharing/
```

- 7. 在本地服务器上启动 ELinks 浏览器，指向 help/ 子目录：

```
# elinks http://127.0.0.1/help
```

- 8. 转到远程系统并尝试访问相同的 Web 目录。例如，如果本地系统的 IP 地址是 192.168.122.50，请导航到 http://192.168.122.50/help。如果可能，请从常规 GUI 浏览器再次尝试一次。

## 基于主机的安全

您可以添加 Order、allow 和 deny 指令来根据主机名或 IP 地址调节访问。以下标准命令序列默认允许访问。它首先读取 deny 指令：

```
Order deny,allow
```

> 考试提示
> 如果您设置 Order allow,deny，访问默认被拒绝。只有与 allow 指令关联的主机名或 IP 地址才允许访问。

您可以从各种形式的主机名或 IP 地址拒绝或允许访问。例如，以下指令拒绝 osborne.com 域中所有计算机的访问：

```
Deny from osborne.com
```

如果 DNS 服务不可靠，您可能更喜欢使用 IP 地址。以下示例指令使用单个 IP 地址；或者，您可以使用部分、网络掩码或 CIDR（无类别域间路由）表示法设置 192.168.122.0 子网，如下所示：

```
Deny from 192.168.122.66
Allow from 192.168.122
Deny from 192.168.122.0/255.255.255.0
Allow from 192.168.122.0/24
```

## 基于用户的安全

您可以将 Apache 服务器上配置的网站的访问限制为具有密码的授权用户。如后所述，这些密码可以与常规身份验证数据库不同。

例如，要为练习 14-3 中描述的网站配置基于用户的安全，您需要在 /var/www/html/help 目录上设置一个 <Directory> 容器。您希望在 <Directory> 容器中包含多个命令：

- - 要设置基本身份验证，您需要一个 AuthType Basic 指令。
- - 要向请求用户描述站点，您可以包含 AuthName "some comment" 指令。
- - 要引用名为 /etc/httpd/testpass 的 Web 服务器密码数据库，您需要 AuthUserFile /etc/httpd/testpass 指令。
- - 要将站点限制为名为 engineer1 的单个用户，您可以添加 Require user engineer1 指令。
- - 或者，要将站点限制为 /etc/httpd/webgroups 中定义的组，您将添加 AuthGroupFile /etc/httpd/webgroups 指令。您还需要一个类似 Require group Design 的指令，其中 Design 是 webgroups 中指定的组名。

这是我在 <Virtual Host> 容器后添加的代码示例：

```
<Directory "/var/www/html/help">
AuthType Basic
AuthName "Password Protected Test"
AuthUserFile /etc/httpd/testpass
Require user engineer1
</Directory>
```

配置正确后，下次您尝试在 Firefox 浏览器中访问 http://server1.example.com/help 网站目录时，会提示您输入用户名和密码，如图 14-7 所示。

## 图 14-7 网站的密码保护

![](img/9139201cfcaf4292284a0eed074928e5_785_0.png)

## 认证目标 14.03

### 专用 Apache 目录

在本节中，您将探索专用 Apache 目录的几个选项。对于这些目录中的某些目录，使用 .htaccess 文件设置专用安全可能是合适的。如前所述，您可以根据用户和组设置密码保护，这对应于 RHCE 目标中引用的“私有目录”。一个适合私有目录的示例是 httpd.conf 文件中包含的主目录示例。借助正确的选项，此类目录也可以由组成员管理。

对 Apache 配置文件进行任何更改后，您可能希望测试结果。为此，您可以运行 apachectl restart 命令。或者，

