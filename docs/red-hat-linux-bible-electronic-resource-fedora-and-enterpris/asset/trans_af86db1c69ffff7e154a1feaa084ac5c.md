
```
-----BEGIN CERTIFICATE-----
MIIEFjCCAwgAwIBAgIOMI26ZZd6njZgn97tJAVFODANBgqkhgiG9w0BAQQFADCB
ujEIMB0GA1UECWMhWmVyAaNpZ24gVHlc3QgTmdVddiEludcglBnybFm0aW9wYWxwgDUzVy
dmNP2Z24siE1uL4y4xAxMzxBgNVBASTkTLZ1iCmlTawDuEIudzglcymFoaW9wYXwgUDFVv
dmVjIENBC0gZ2xxc3MgMzFJMEc1orYZG0d3d3LnZlLnlZdWd3dWMlaB0W9uXwgUFJmg
SW5jb3JwLWm5JfJLZ1igTE1B0klMSVRZilZEUXC4gYyk5NyBWZZXJPuZ1njbAeFw0w
MzXZKBuWdAWDMDaEFvm0wNDMwMTYu5UNTETAMVQMQswcqDVQ2N1E2VUZtUETmBEG
A1UECBMKV2F2aGlud33RvHiTxErE371UEBXQLRmVcZXZxJbCbcXYKxGzAZBgNVBAOU
Ek1ETS7TZXj2aWmLcwngSW51LJjEMMAG0AIUECQxd3d3MTMwMwQYDVQQFCpUZXJtcI
cyBviZB1c2UyYXQgd3d3LnZlcm1zLnB5cGEcgEGKGMPMDAXFDASBgNVBAMUC2lkb
M1uMIGEMAOGCSQGS1b3DQBEQAQUAA4GNADCBiOQKBgQDaHsk+uZO/
7jjDPFEnqT80BaIL3yPILxFjhj3xPMXLGwZLmkDmdQjXsa4x7AhEpr1ubuVnhVJiO
FnLDopsx4p7r4n+P8FyS4M5ggrbcQOzyYNk2jjqyVF/7yOW2pd13ot4eacyYaza4Og
g9PTxhU2jEG4twvKCAFWhuEogUICMV2gQIDAQABo41BJTCCASEwQCDVRO7bTA1w
A DEBgbNVHSAePTA7mDMGGCGCSAGAG+EBBxbcDMCoKAYIkwYBBOUHAgEWGHOdHBz
Oia8vd3d3LnZ1cm1laWdDuLmnNvB5yc6EwCWyDVRPBAqADAgWgMCGAJLUdJQJHM8G
CwcGSA G+EIEMO0CoW1YQBuAwGGCCcGAQuFBNXwmCQMDOCGCCAGQFbWBEBbCGwJ/Ak
BpgBrEBPGCoaYYA/XROcDovL29jczAudlOclb1FAj5xP17B68wxLKTeRu4Novu13
06As5OdeGNW0dAHA6LY9jcMwuDMVyaxNpZ24uY2R0LON5XXNzm01udGVybFbmFoW9w
YXkXZKXZZXXIuYj3UsMBkgCcSMCgSAG+E+eF4Cec3zYJODASzNmwMTeYMa0GSCsq
GSB13 DQEBBAUAAG4BAJ/Psvtcm1dSkQi5nuEudLc0b1FAj5xP17B68wxLKTeRu4Novu13
8lLLZnAr+acHCCwK0l3rQpJgV2y1mwj/kPnC1WjoYefXdh7+Mbg/6f6mmlK9auW
TRIPW/+aBO8RyOJLMA2VQQvhX42njJGpcWNY9AGSHm1UEBjSyvtb1lX
```

将此证书复制并粘贴到名为 `server.crt` 的空文件中，该文件必须位于 `/etc/httpd/conf/ssl.crt` 目录中，然后重新启动您的 Web 服务器：

```
# service httpd restart
```

假设您的网站之前工作正常，现在您可以通过在 Web 地址中的 `http` 后面加上一个 "s" 来以安全的方式查看它。因此，如果您之前在 `http://www.acmerarina.com` 查看网站，现在可以通过访问 `https://www.acmerarina.com` 以安全的方式查看它。

## 创建自签名证书

生成并运行自签名 SSL 证书比拥有签名证书要容易得多。要生成自签名 SSL 证书，请执行以下操作：

- 1. 删除当前存在的密钥和证书：

```
# cd /etc/httpd/conf
# rm ssl.key/server.key ssl.crt/server.crt
```

- 2. 创建您自己的服务器密钥：

```
# /usr/bin/openssl genrsa 1024 > ssl.key/server.key
```

- 3. 使 `server.key` 文件仅对 root 可读和可写：

```
# chmod 600 ssl.key/server.key
```

- 通过输入以下内容创建自签名证书：

```
# make testcert
umask 77 ;
/usr/bin/openssl req -new-key /etc/httpd/conf/ssl.key/server.key 
    -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
...
...
```

此时，是时候开始向证书添加一些识别信息，以便第三方来源稍后进行验证。在此之前，您必须解锁刚刚创建的私钥。输入上面输入的密码来执行此操作。然后按照以下示例过程操作：

```
You are about to be asked to enter information that will be
incorporated into your certificate request.
What you are about to enter is what is called
a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value, If you enter '.', the field will be left blank.
---
Country Name (2 letter code) [GB]:**US**
State or Province Name (full name) [Berkshire]: **Ohio**
Locality Name (eg, city) [Newbury]: **Cincinnati**
Organization Name (eg, company) [My Company Ltd]:**Industrial Press, Inc.**
Organizational Unit Name (eg, section) []:**IT**
Common Name (eg, your name or your server's hostname)
[]:**www.industrialpressinc.com**
Email Address []: **webmaster@industrialpressinc.com**
```

上述生成过程会将所有文件放置在正确的位置。您需要做的就是重新启动 Web 服务器，并在 URL 前加上 https 而不是 http。不要忘记，您会从 Web 浏览器收到证书验证消息，您可以安全地忽略它。

## 重新启动您的 Web 服务器

到目前为止，您可能已经注意到每次启动 Web 服务器时都需要输入证书密码。这是为了防止有人入侵您的服务器并窃取您的私钥。如果发生这种情况，您可以放心，私钥是一堆乱码。破解者无法利用它。如果没有这种保护，破解者可能会获取您的私钥并轻松冒充您，在所有情况下都显得合法。

如果您实在无法忍受每次 Web 服务器启动时都要输入密码，并且愿意接受增加的风险，您可以删除私钥上的密码加密。只需执行以下操作：

```
# cd /etc/httpd/conf/ssl.key
# /usr/bin/openssl rsa -in server.key -out server.key
```

## 故障排除您的证书

以下提示如果您在使用 SSL 证书时遇到问题可能会有所帮助。

- 每个 IP 地址只允许一个 SSL 证书。如果您想向服务器添加多个启用 SSL 的网站，您必须将另一个 IP 地址绑定到网络接口。
- 请确保 `/etc/httpd/conf/ssl.*` 目录及其内容上的权限掩码为 700 (`rwx------`)。
- 请确保您没有在 Web 服务器上阻止端口 443。所有 `https` 请求都通过端口 443 进入。如果您阻止了它，您将无法获取安全页面。
- 证书仅有效一年。一年期满后，您必须使用证书颁发机构续订证书。每个证书颁发机构对此有不同的流程；请查看颁发机构的网站以获取更多详细信息。
- 请确保已安装 `mod_ssl` 软件包。如果未安装，您将无法提供任何启用 SSL 的流量。

## 导出加密技术

在描述如何使用各种加密工具之前，我需要警告您美国政府的一项不寻常政策。多年以来，美国政府将加密技术视为军火。因此，任何希望出口加密技术的人都必须从商务部获得出口许可证。这不仅适用于美国开发的加密软件，还适用于从其他国家获得然后再出口到另一个国家（甚至是您获得它的同一国家）的软件。因此，如果您在 Linux 系统上安装了加密技术然后将其运出境外，您就违反了联邦法律！此外，如果您通过电子邮件将加密软件发送给另一个国家的朋友或让他们从您的服务器下载，您就违反了法律。

2000 年 1 月，美国有关加密软件的出口法律大大放宽。然而，通常美国商务部的出口管理局在加密产品出口前需要对其进行审查。美国公司也不允许向被归类为支持恐怖主义的国家出口加密技术。

## 使用 Secure Shell 软件包

Secure Shell 软件包 (SSH) 是一个提供与 rsh、rcp 和 rlogin 命令类似的 shell 服务的软件包，但会加密网络流量。它使用私钥加密，因此非常适合用于连接互联网的计算机。Red Hat Linux 发行版包含以下用于 SSH 的客户端和服务器软件包：openssh、openssh-client 和 openssh-server 软件包。

## 启动 SSH 服务

如果您已安装 openssh-server 软件包，则 SSH 服务器会自动配置为启动。SSH 守护进程从 /etc/init.d/sshd 启动脚本启动。为了确保服务设置为自动启动，请以 root 用户身份输入以下内容：

```
# chkconfig --list sshd
sshd        0:off   1:off   2:on    3:on    4:on    5:on    6:off
```

这表明 sshd 服务设置为在系统状态 2、3、4 和 5（正常启动状态）下运行，并在所有其他状态下关闭。如果 SSH 服务处于关闭状态，您可以以 root 用户身份输入以下内容将其打开以用于默认运行状态：

```
# chkconfig sshd on
```

此行在您进入运行级别 2、3、4 或 5 时打开 SSH 服务。要立即启动服务，请输入以下内容：

```
# /etc/init.d/sshd start
```

## 使用 ssh、sftp 和 scp 命令

您可以使用 SSH 服务的三个命令是 ssh、sftp 和 scp。远程用户使用 ssh 命令安全地登录到您的系统。scp 命令允许远程用户复制文件到系统和从系统复制。sftp 命令提供了一种安全访问 FTP 站点的方式。

与正常的远程 shell 服务一样，安全 shell 会查看 /etc/hosts.equiv 文件和用户 .rhost 文件以确定是否应允许连接。它还会在 ssh 特定的文件 /etc/shosts.equiv 和 .shosts 中查找。使用 shosts.equiv 和 .shosts 文件是首选，因为它避免授予对未加密远程 shell 服务的访问权限。/etc/shosts.equiv 和 .shosts 文件在功能上等同于传统的 hosts.equiv 和 .rhosts，因此相同的说明和规则适用。

现在您可以准备好测试 SSH 服务了。从安装了 SSH 的另一台计算机（如果没有其他计算机，甚至可以从同一台计算机）上，输入 ssh 命令，后跟一个空格和您要连接的系统名称。例如，要连接到系统 ratbert.glaci.com，请输入：

```
# ssh ratbert.glaci.com
```
