
这三个 SSL 关键字——`SSLEngine`、`CertificateFile` 和 `SSLCertificateKey` 是启用工作良好的 SSL 服务器的基础 Apache 指令。如果我们安装了 `mod_ssl` 和 `openssl` 软件包，`IfDefine HAVE_SSL` 将始终评估为真。假设你已经安装了这两个软件包，启动 Web 服务器并尝试让 Mozilla Web 浏览器指向 `https://localhost/` 的 Web 服务器。你应该会看到关于证书的警告，“此证书由 Mozilla 无法识别的证书颁发机构颁发。”在每个 SSL 浏览器内部都有一个受信任的证书颁发机构列表。显然，我们自己的本地机器不在信任的 CA 列表中。点击“继续”按钮允许 Web 浏览器临时接受证书并显示默认 Web 页面。

## 创建 CA 签名证书

虽然测试 SSL 服务器规避了对免费自签名证书的需求，但一旦我们将 Web 服务器推向外部世界，我们可能不希望 Web 客户端看到“标识 localhost.localdomain 的证书存在问题。你要继续吗？”在这种情况下，我们需要创建一个证书签名请求文件（CSR），证书颁发机构在为你的组织颁发证书时需要该文件（以及身份证明和费用）。幸运的是，创建 CSR 并不复杂：

```bash
[root@thunderbird ~]# cd /usr/share/ssl/certs

[root@thunderbird ~]# make server.crt

umask 77 \

/usr/bin/openssl genrsa -des3 1024 > server.key

Generating RSA private key, 1024 bit long modulus

++++++++++++++

+++++++++++++

e is 65537 (0x10001)

Enter PEM pass phrase: hello9

Verifying password - Enter PEM pass phrase: hello9

umask 77 \

/usr/bin/openssl req -new -key server.key -x509 -days 365 -out server.crt

Using configuration from /usr/share/ssl/openssl.cnf

Enter PEM pass phrase: hello9

你将被要求输入一些信息，这些信息将合并到你的证书请求中。你将要输入的内容被称为区分名称（Distinguished Name，简称 DN）。

有相当多的字段可以留空。

对于某些字段，将有一个默认值。
```

如果你输入 `""`，该字段将留空。

- 国家名称（2 位代码） [GB]:US
- 州或省名称（全称） [Berkshire]:North Carolina
- 地区性名称（例如，城市） [Newbury]:Raleigh
- 组织名称（例如，公司） [My Company Ltd]:Not quite Red
- 组织单位名称（例如，部门） [: IS/IT Dept.
- 通用名称（例如，你的名称或服务器主机名）[]:www.example.com
- 邮箱地址 []: webmaster@example.com

此过程创建了我们的 `server.crt` 文件和所需的 `server.key` 文件。它们看起来应该是这样的：

```bash
root@thunderbird sert# cat server.crt

----BEGIN CERTIFICATE-----

MIID2TCACOgAAEwQBgkqhkiG9w0BAQEAAQCBJELMAQIUEBMCVMVMX

FZAVGBnVAGtD5cnRoInEcm9saW5HRAmYDYDQHEWYSXYwa10mROWGAYD

QQEXFBQ0D3fyxQVpUGmVdkIncHVMEDBUMIAEUCLCMSVMSQRGvGWc4X6GAW

BGNVBAM30d3y5eGffcLmNBVTCKGC5GS1B30JEQAREY2JD2VibBf2ZGyY

06V4Y1wbBguY29X2MBH41ATYMDN2JAZMTEMW0XTADM69WnjJa2MTVmwowag

C2ZAJGBNVBAT1VMRKTCVFYQ0WDIYF0BS30A3CJY6bLU1YTEQ4MAA1UEBHMX

MIFmvzEBAEAGM0111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

11111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

1111111111111111111111111111111111111111111111111111111111111111

----END CERTIFICATE

root@thunderbird sert# cat server.key

----BEGIN RSA PRIVATE
```

将 `server.key` 文件复制到 `/etc/httpd/ssl.key` 并妥善保管。它包含了你的服务器身份！接下来将 `server.crt` 文件发送给 CA。每个 CA 都有特定的要求，它们都需要 CSR。在它们为你创建并签名证书后，将由你将其放入 `/etc/httpd/conf/ssl.crt/` 目录。如果你使用多个 SSL 虚拟主机，请注意命名证书以免相互覆盖。

## 故障排除

你可以系统地排查 Apache 服务器。Apache 是一个经典的客户端-服务器系统，因此需要三个条件才能正常运行：由于运行 Mozilla 等浏览器非常简单易事，且我们在其他章节中讨论了通用网络故障排除，我们在这里专注于确保服务器运行正常。

如果你的 Web 服务器没有正常工作，以下章节建议调查以下领域：

- 检查 Linux 系统日志
- 本地连接
- 检查 Apache 配置
- 尽可能使用简化 `httpd.conf`
- 增量式添加新指令

### 检查 Linux 系统日志

由 `syslog` 控制的 Linux 系统日志可以显示问题。例如，如果你没有正确配置 VirtualHost 容器，`syslog` 会发出警告。以下 `/var/log/message` 摘：

> Jan 20 12:15:54 atlas [Sun Jan 20 12:15:54 2002] warn NameVirtualHost 192.168.1.133:80 has no VirtualHosts

此日志表明在检查 `httpd.conf` 文件时存在配置问题。在这种情况下，虚拟主机容器尚未与虚拟主机关联，如下：

```
<VirtualHost *
  ServerName virtual_1
  ServerAdmin webmaster@paunchy.net
  DocumentRoot /var/www/virtual_1
</VirtualHost>
```

## 第 6 章：配置基础 Apache 服务器

### 检查 Apache 日志

Apache 可以记录其系统内部发生的任何错误。以下 `httpd.conf` 指令控制错误日志记录：

```
LoadModule config_log_module modules/mod_log_config.so

LoadModule agent_log_module modules/mod_log_agent.so
```
