
256 个虚拟身份与之关联。如果需要更改此限制，请使用 ndd 更改参数 ip_addrs_per_if（有关使用 ndd 的详细信息，请参阅第 498 页）。

要配置虚拟接口，只需在其中一个虚拟名称上运行 ifconfig 即可。（底层物理接口必须已经“plumbed”。）在大多数情况下，您希望设置系统，使虚拟接口的 ifconfig 在启动时自动执行。

下面是一个示例，其中 Solaris 机器在内部虚拟专用网络（VPN）上有一个私有地址空间中的地址，以及用于 Internet 的外部地址，两者都与同一物理接口 hme0 相关联。为了使这些接口在启动时自动配置，管理员设置了两个主机名文件：/etc/hostname.hme0 和 /etc/hostname.hme0:1。

```
$ ls -l /etc/host*
-rw-r--r-- 1 root root 10 Nov 4 10:19 /etc/hostname.hme0
-rw-r--r-- 1 root root 16 Dec 21 19:34 /etc/hostname.hme0:1
```

主机名文件可以包含来自 /etc/hosts 文件的主机名或 IP 地址。在本例中，管理员使用了各一个：

```
$ cat /etc/hostname.hme0
overkill
$ cat /etc/hostname.hme0:1
206.0.1.133
$ grep overkill /etc/hosts
10.1.2.9 overkill overkill.domain
```

在启动时，两个地址都会自动配置（连同我们从下面显示的输出中省略的回环地址）：

```
$ ifconfig -a
hme0: flags=863<UP,BROADCAST,NOTRAILERS,RUNNING,MULTICAST> mtu 1500 inet 10.1.2.9 netmask ffffff00 broadcast 10.1.2.255
hme0:1: flags=863<UP,BROADCAST,NOTRAILERS,RUNNING,MULTICAST> mtu 1500 inet 206.0.1.133 netmask ffffff80 broadcast 206.0.1.255
```

## HP-UX 虚拟接口

在 HP-UX 上，您使用 ifconfig 命令添加虚拟接口。其语法与 Solaris 非常相似。例如，要添加第一个接口，您将执行命令

```
$ sudo ifconfig lan0:1 192.168.69.1 up
```

## AIX 虚拟接口

在 AIX 上，您创建一个“别名”以向接口添加额外的 IP 地址。例如，要将 192.168.1.3 添加为 en0 接口的虚拟 IP 地址，您可以使用 ifconfig：

```
$ sudo ifconfig en0 192.168.1.3 netmask 255.255.255.0 alias
```

但是，此别名只是临时的。要创建永久虚拟 IP，请使用 chdev 命令：

```
$ sudo chdev -l en0 -a alias4=192.168.1.3,255.255.255.0
```

## 告知 Apache 关于虚拟接口

除了创建虚拟接口之外，您还需要告诉 Apache 当客户端尝试连接到每个接口（IP 地址）时应提供哪些文档。您通过 httpd.conf 文件中的 VirtualHost 子句来完成此操作。每个已配置的虚拟接口都有一个 VirtualHost 子句。下面是一个示例：

```
<VirtualHost 128.138.243.150>
ServerName www.company.com
ServerAdmin webmaster@www.company.com
DocumentRoot /var/www/htdocs/company
ErrorLog logs/www.company.com-error_log
CustomLog logs/www.company.com-access_log combined
ScriptAlias /cgi-bin/ /var/www/cgi-bin/company
</VirtualHost>
```

在此示例中，任何连接到虚拟主机 128.138.243.150 的客户端都会从 /var/www/htdocs/company 提供文档。几乎任何 Apache 指令都可以放入 VirtualHost 子句中，以定义特定于该虚拟主机的设置。相对目录路径，包括 DocumentRoot、ErrorLog 和 CustomLog 指令的路径，都是在 ServerRoot 的上下文中解释的。

使用基于名称的虚拟主机时，多个 DNS 名称都指向同一个 IP 地址。Apache 配置类似，但您指定 Apache 应在该地址上监听传入的基于名称的虚拟主机请求的主 IP 地址，并在 VirtualHost 子句中省略 IP 地址：

```
NameVirtualHost 128.138.243.150

<VirtualHost *>
ServerName www.company.com
ServerAdmin webmaster@www.company.com
DocumentRoot /var/www/htdocs/company
ErrorLog logs/www.company.com-error_log
CustomLog logs/www.company.com-access_log combined
ScriptAlias /cgi-bin/ /var/www/cgi-bin/company
</VirtualHost>
```

在此配置中，Apache 会在 HTTP 标头中查找以确定请求的站点。服务器在主 IP 地址 128.138.243.150 上监听对 www.company.com 的请求。

## 23.4 安全套接字层（SSL）

SSL 协议保护网站与客户端浏览器之间的通信。以 https:// 开头的 URL 使用此技术。SSL 使用密码学来防止窃听、篡改和消息伪造。
