

## 4. 客户端配置：配置 Web 浏览器以使用您的 Squid 服务器

刷新防火墙规则：[ OK ]
将链设置为接受策略：filter [ OK ]
卸载 iptables 模块：[ OK ]
应用 iptables 防火墙规则：[ OK ]
加载额外的 iptables 模块：ip_conntrack_netbios_n[ OK ]

接下来，让我们学习如何使用 Squid 配置进行客户端设置。

您需要手动配置 PC 浏览器的代理服务器设置才能使用 Squid 服务器。使用的方法取决于您的浏览器。

例如，若要通过 Internet Explorer 进行这些更改：

1. 点击浏览器菜单栏中的“工具”项。
2. 点击“Internet 选项”。
3. 点击“连接”。
4. 点击“局域网设置”。
5. 使用您的 Squid 服务器所使用的地址和 TCP 端口（默认为 3128）进行配置。图 1 展示了 Internet Explorer 中的代理服务器设置。

![](img/f3b9cff79e19317416c12eaf5ded7245_183_0.png)

图 2 展示了代理服务器的地址以及端口号。

![](img/f3b9cff79e19317416c12eaf5ded7245_184_0.png)

▲ 图 2

以下是如何使用 Mozilla 或 Firefox 进行相同更改的方法：

1. 点击浏览器菜单栏中的“编辑”项。
2. 点击“首选项”。
3. 点击“高级”。
4. 点击“代理”。
5. Squid 代理服务器的高级配置：

在 Squid 代理服务器的高级配置中，您还将了解访问控制列表（ACL）。

### 访问控制列表

您可以通过访问控制列表（ACL）限制用户浏览互联网的能力。每个 ACL 行定义一种特定的活动类型，例如访问时间或源网络；随后它们与 http_access 语句关联，该语句告诉 Squid 是否允许或拒绝符合该 ACL 的流量。

Squid 通过从上到下检查 http_access 列表来匹配其收到的每个 Web 访问请求。如果找到匹配项，它将执行允许或拒绝语句，并停止进一步读取。您必须小心不要在列表中将一个 deny（拒绝）语句放置在一个位于其下方的相似 allow（允许）语句之前。由于最终的 http_access 语句会拒绝所有请求，因此最好将新的 http_access 语句放置在其上方。

接下来，让我们学习如何通过时间限制 Web 访问。

### 通过时间限制 Web 访问

您可以创建带有时间参数的访问控制列表。例如，您仅允许家庭网络在工作时间访问：

```
#
# Add this to the bottom of the ACL section of squid.conf
#
acl home_network src 172.16.1.0/24
acl business_hours time M T W H F 9:00-17:00

#  
# Add this at the top of the http_access section of squid.conf
#
http_access allow home_network business_hours
```

或者，您仅允许早晨访问：

```
#
# Add this to the bottom of the ACL section of squid.conf
#
acl mornings time 08:00-12:00

#  
# Add this at the top of the http_access section of squid.conf
#
http_access allow mornings
```

### 通过 IP 地址限制 Web 访问

您可以创建一个访问控制列表，将 Web 访问限制在特定网络上的用户。在这种情况下，它是一个定义 172.16.1.0 家庭网络的 ACL：

```
#  
# Add this to the bottom of the ACL section of squid.conf
#
acl our_network src 172.16.1.0/255.255.255.0
```

您还必须添加相应的 http_access 语句，以允许匹配该 ACL 的流量：

```
#  
# Add this at the top of the http_access section of squid.conf
#
http_access allow our_network
```

### 使用 ncsa_auth 辅助程序进行 Squid 代理认证

为了精细控制，您可能需要使用 Squid 代理服务器认证。这将仅允许授权用户使用代理服务器。

您需要使用 proxy_auth ACL 来配置 ncsa_auth 模块。浏览器在 Authorization 请求头中发送用户的认证信息。如果 Squid 收到请求且 http_access 规则列表到达 proxy_auth ACL，Squid 会查找 Authorization 头。如果该头存在，Squid 会对其进行解码并提取用户名和密码。

然而，Squid 本身不具备密码认证功能。您需要借助*认证辅助程序*。以下辅助程序在大多数 Squid 和大多数 Linux 发行版中默认包含：

- NCSA：使用 NCSA 风格的用户名和密码文件。
- LDAP：使用轻量级目录访问协议
- MSNT：使用 Windows NT 认证域。
- PAM：使用 Linux 可插拔认证模块方案。
- SMB：使用 SMB 服务器，如 Windows NT 或 Samba。
- getpwnam：使用传统 Unix 密码文件。
- SASL：使用 SASL 库。
- NTLM：协商和摘要认证

接下来，让我们学习如何配置 NCSA。

### 配置 NCSA 风格的用户名和密码认证

首先使用 `htpasswd` 命令创建 NCSA 密码文件。`htpasswd` 用于创建和更新用于存储 Squid 用户基本认证的用户名和密码的扁平文件。

```
[root@netmon tmp]#htpasswd /etc/squid/passwd user1

Output:
New password:
Re-type new password:
Adding password for user user1
```

确保 Squid 可以读取 passwd 文件：

```
[root@netmon tmp]#chmod o+r /etc/squid/passwd
```

### 定位 ncsa_auth 认证辅助程序

通常 `ncsa_auth` 位于 `/usr/lib/squid/ncsa_auth`。您可以使用 `rpm`（RedHat 和 Fedora）查找其位置。
如果您使用的是 RHEL/Fedora Core 或基于 RPM 的发行版，请尝试：

```
# rpm -qI squid | grep ncsa_auth

Output:
/usr/lib/squid/ncsa_auth
```

### 为 Squid 代理认证配置 ncsa_auth

现在打开 /etc/squid/squid.conf 文件

```
[root@netmon tmp]#vi /etc/squid/squid.conf
Append (or modify) following configuration directive:
auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Squid proxy-caching web server
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive off

Also find out your ACL section and append/modify
acl ncsa_users proxy_auth REQUIRED
http_access allow ncsa_users
```

保存并关闭该文件。

- auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd ：指定 Squid 密码文件和辅助程序位置
- auth_param basic children 5 ：包含要生成的认证器进程数量。
- auth_param basic realm Squid proxy-caching web server ：包含用户在输入用户名和密码时看到的文本部分
- auth_param basic credentialsttl 2 hours ：指定 Squid 假设外部验证的用户名:密码对有效的时长 - 换句话说，即以什么频率为该用户调用辅助程序进行密码提示。此处设置为 2 小时。
- auth_param basic casesensitive off ：指定用户名是否区分大小写。仅可以是 on 或 off
- acl ncsa_users proxy_auth REQUIRED ：要求任何已认证用户都匹配名为 ncsa_users 的 ACL
- http_access allow ncsa_users ：仅当用户成功认证时才允许代理访问。

输入以下命令以重启 Squid 服务器。

```
[root@netmon tmp]#/etc/init.d/squid restart
```

接下来，让我们学习如何监控 Squid 代理服务器。

## 监控 Squid 代理服务器

### 日志记录

日志文件可在 /var/log/squid 中找到。

查看访问日志文件 /var/log/squid/access.log：

- [root@netmon tmp]#tail -f /var/log/squid/access.log

上述命令将监控所有传入请求并将其记录到 /var/log/squid/access.log 文件中。现在，如果有人通过浏览器访问网站，Squid 将记录相关信息。

- 工具：可以使用各种工具来分析这些日志文件。其中一个工具是 Webalizer。Webalizer 提供带有图形的有用统计数据。以下是一个简单的 Webalizer 示例：

```
[root@netmon tmp]#/usr/bin/webalizer -F squid /var/log/squid./access.log
```

Webalizer 将处理日志文件并将结果放置在 /var/lib/webalizer/。要查看结果，请输入：

```
[root@netmon tmp]#mozilla /var/lib/webalizer/index.html
```

