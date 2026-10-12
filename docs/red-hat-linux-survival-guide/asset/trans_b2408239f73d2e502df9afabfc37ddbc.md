
```
<VirtualHost 192.168.1.3>
    ServerName vhost3.server.com
    # Other directives go here
</VirtualHost>
```

这些 IP 地址中的每一个都必须绑定到服务器上的相应以太网接口。例如，上述配置要求托管上述站点的系统在其 DNS 服务器配置文件中具有以下 DNS 记录：

```
; Address Records
vhost1.server.com.  IN  A 192.168.1.1
vhost2.server.com.  IN  A 192.168.1.2
vhost3.server.com.  IN  A 192.168.1.3

; Reverse DNS records
1                   IN  PTR vhost1.server.com.
2                   IN  PTR vhost2.server.com.
3                   IN  PTR vhost3.server.com.
```

这些地址中的每一个都必须绑定到服务器上的一个或多个以太网接口。通常，在 Linux 系统上，可以使用 IP 别名技术绑定多个 IP 地址。例如：

```
/sbin/ifconfig eth0   192.168.1.1 up
/sbin/ifconfig eth0:0 192.168.1.2 up
/sbin/ifconfig eth0:1 192.168.1.3 up
```

这里，全部三个 IP 地址都绑定到以太网接口 eth0 及其两个别名 eth0:0 和 eth0:1。现在系统将响应这些 IP 地址中的每一个。

## 如何将多个主服务器用作虚拟主机

仅在需要（通常由于非技术原因）维护不同的 httpd.conf 文件时，才建议使用多个主服务器作为虚拟主机。

![](img/9eb7e89292d2f85707b4d49102c865b7_343_0.png)

在实际采用此方法之前，请仔细考虑是否可以避免创建多个主服务器实例，而只需使用 <VirtualHost> 容器即可。

例如，假设你有 16 个 IP 地址，并且希望为 16 个不同的客户端（或部门）提供各自的 httpd.conf 文件，以便每个实体可以自行管理所有内容；他们甚至可以通过在其自己的 httpd.conf 文件中使用 <VirtualHost> 容器来创建自己的虚拟主机。

清单 12-2 显示了 httpd.conf 的一个简化版本（称为 httpd-100.conf），它使用 Listen 指令告诉 Apache 仅为运行它的系统关联的 192.168.1.100 IP 地址提供服务。

### 清单 12-2 httpd-100.conf 文件

```
ServerType standalone
ServerRoot "/usr/local/apache"
PidFile /usr/local/apache/logs/httpd-192.168.1.100.pid
ScoreBoardFile /usr/local/apache/logs/httpd-192.168.1.100.scoreboard
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 60
MaxSpareServers 100
StartServers 50
MaxClients 200
MaxRequestsPerChild 0
Port 80
Listen 192.168.1.100:80
User prod
Group prod
ServerName prod.domain.com
ServerAdmin kabir@prod.domain.com
DocumentRoot "/www/prod/htdocs"
```

请注意，Listen 指令还接受端口号作为参数。在上面的示例中，Apache 被告知在端口 80 上监听给定的 IP 地址。Port 指令仍然是必要的，因为其值用于 Apache 生成的自引用 URL 中。

清单 12-3 显示了另一个名为 httpd-101.conf 的简化 httpd.conf 文件，它告诉 Apache 仅监听 192.168.1.101 地址。

### 清单 12-3 httpd-101.conf 文件

```
ServerType standalone
ServerRoot "/usr/local/apache"
PidFile /usr/local/apache/logs/httpd-192.168.1.101.pid
ScoreBoardFile /usr/local/apache/logs/httpd-192.168.1.101.scoreboard
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 5
MaxSpareServers 10
StartServers 5
MaxClients 10
MaxRequestsPerChild 0
Port 80
Listen 192.168.1.101:80
User stage
Group stage
ServerAdmin lance@stage.domain.com
DocumentRoot "/www/stage/htdocs"
```

使用上述配置文件运行两个主 Apache 服务器的系统必须具备以下条件：

- 一个或多个响应命名 IP 地址的以太网接口。例如，在 Linux 系统上，你可以使用以下 IP 别名命令将以太网接口 eth0 同时绑定到 192.168.1.100 和 192.168.1.101：

```
/sbin/ifconfig eth0 192.168.1.100 up
/sbin/ifconfig eth0:0 192.168.1.101 up
```

当然，如果系统具有多个以太网接口，并且你希望为每个接口使用一个主服务器，则无需使用 IP 别名。

- IP 地址必须与其关联主机名。对于上述配置文件，`192.168.1.100` 与 `prod.domain.com` 关联，而 `192.168.1.101` 与 `stage.domain.com` 关联。

具有此类 IP 地址绑定到其接口的系统现在可以通过使用以下命令运行两个主 Apache 守护进程：

```
/usr/local/apache/bin/httpd -f conf/httpd-100.conf
/usr/local/apache/bin/httpd -f conf/httpd-101.conf
```

如果你运行 `ps auxww | grep httpd | grep root | grep conf` 命令，你将看到两个作为 root 用户运行的主 Apache 服务器。

## 对用户进行身份验证和授权

mod_auth 模块是 Apache 的默认身份验证模块。该模块允许你对凭据存储在文本文件中的用户进行身份验证，通常文本字段包含用户名和加密密码。你还可以使用文本文件创建用户组，可用于创建授权规则。

![](img/9eb7e89292d2f85707b4d49102c865b7_345_0.png)

> 我建议你仅对少量用户使用基于 mod_auth 的身份验证，比如几百个用户左右。我的个人经验表明，当文本文件达到即使是低至几千个（1K-3K）用户名时，查找性能会急剧下降。因此，如果你有非常大的用户群，我不建议使用此模块。

该模块默认已编译到 Apache 中。你可以使用 `/usr/local/apache/bin/httpd -l` 来验证此模块是否已编译到你的 Apache 二进制文件中。如果没有，你必须使用 configure 脚本中的 `--enable-module=auth` 选项重新编译并安装你的 Apache 发行版。我假设你默认已编译 mod_auth。

## 了解 mod_auth 指令

mod_auth 模块提供了 Apache 指令 AuthUserFile、AuthGroupFile 和 AuthAuthoritative。以下各节将更详细地介绍这些指令以及使用该模块的一些示例。

### AuthUserFile

此指令设置包含用于基本 HTTP 身份验证的用户名和密码的文本文件的名称。你必须提供要使用文件的完全限定路径。

语法：AuthUserFile filename

上下文：Directory，per-directory access control file

覆盖：AuthConfig

例如，以下文件通常使用名为 htpasswd 的实用程序创建，该实用程序作为标准 Apache 发行版中的支持程序提供：

```
AuthUserFile /www/mobidac/secrets/.htpasswd
```

此文件的格式非常简单。每一行包含一个用户名和一个加密密码。密码使用标准的 crypt() 函数进行加密。

![](img/9eb7e89292d2f85707b4d49102c865b7_346_0.png)

很重要的一点是，AuthUserFile 指定的文件必须位于网站文档树之外。将它放在可通过 Web 访问的目录中可能会允许某人下载它。

### AuthGroupFile

此指令指定用于基本 HTTP 身份验证的用户组列表的文本文件。文件名是组文件的绝对路径。

语法：AuthGroupFile filename

上下文：Directory，per-directory access control file

覆盖：AuthConfig

你可以使用任何文本编辑器创建此文件。此文件的格式如下：

```
groupname: username username username ...
```

例如，以下命令创建一个名为 startrek 的组，其中包含四个用户：kirk、spock、picard 和 data：

```
startrek: kirk spock picard data
```

AuthUserFile 部分中的 Caution 图标也适用于此指令。

### AuthAuthoritative

如果你对同一目录使用多个身份验证方案，可以将此指令设置为 Off，以便当用户名/密码对在第一个方案中失败时，它会被传递到下一个（较低）级别。

语法：AuthAuthoritative On | Off

默认设置：AuthAuthoritative On

上下文：Directory，per-directory access control file

覆盖：AuthConfig

例如，如果你使用 mod_auth_mysql 和标准的 mod_auth 模块提供身份验证服务，并且用户名/密码对在其中一个模块中失败，则下一个模块将被用来尽可能地对用户进行身份验证。当用户名/密码对在所有模块中均失败时，服务器会重新发出 401 状态头并发送 WWW-Authenticate 响应头以进行重新身份验证。但是，如果某个模块成功验证了用户名/密码对，则较低级别的模块永远不会收到该用户名/密码对。

我建议你保留默认值，因为你不应设计一种逐级递减的身份验证方案，在该方案中用户可能在一个方案中失败而在另一个方案中通过。
