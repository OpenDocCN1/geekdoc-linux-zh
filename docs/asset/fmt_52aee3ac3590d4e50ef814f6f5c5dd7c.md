
随后你会被要求输入密码来保护你的私钥。该密码至少要有八个字符，且不应该是字典单词，或包含数字或标点符号。你输入的字符不会显示在屏幕上，以防止他人通过窥视获取你的密码。

输入短语：

再次输入密码进行验证。

验证中 - 输入短语：

证书生成过程现在开始。

此时，是时候开始为证书标识某些信息，这些信息稍后将由第三方源验证。在此之前，你必须解锁你创建的私钥。通过输入你作为短语输入的密码来执行。然后按照提示输入信息。这里显示了一个为证书添加信息的会话示例：

为 `/etc/httpd/conf/ssl.key/server.key` 输入短语：
你将被要求输入将要合并到你的证书请求中的信息。
你正要输入的内容被称为区分名称（Distinguished Name，简称 DN）。
有很多字段，但对于某些会有默认值的字段，你可以留空。
如果你输入 '.'，则该字段将留空。

国家名称（两个字母代码） [GB]:US
州或省份（全名） [Berkshire]: Connecticut
地名名称（例如，城市） [Newbury]: Mystic
组织名称（例如，公司） [My Company Ltd]:Acme Marina, Inc.
组织单元名称（例如，部门） [:InfoTech
通用名称（例如，你的名称或服务器的主机名）
[: www.accmarina.com
电子邮件地址 [:]: webmaster@acemarina.com

要完成过程，你将被要求为你的证书添加任何额外属性。除非你有理由提供更多信息，否则你只需在任何一个提示处按回车键将其留空。

请输入以下“额外”属性：
要完成过程，你将被要求为你的证书添加任何额外属性。除非你有理由提供更多信息，否则你只需在任何一个提示处按回车键将其留空。

## 获取证书

一旦创建了 CSR，你需要将其发送给第三方机构进行验证。第一步是选择一个机构。以下是你需要关注的：

- 信誉
- 稳定性
- 支持
- 产品
- 价格

在你选择了机构并发送 CSR 后，他们将验证你的信息，然后你将收到证书文件。下一步是将证书文件的内容复制到你的 Web 服务器配置中。

# 600 第三部分：管理 Fedora 和 RHEL

```
WF0IFW+/a8OWRYQJLMA2QOVHx4znjpGcVNY9AQShm1UIESJy7vtdlIX

----- END CERTIFICATE-----
```

将此证书复制并粘贴到空的 `server.crt` 文件中，该文件必须存放在 `/etc/http/conf/ssl.crt` 目录下，然后重启您的 Web 服务器：

```
# service httpd restart
```

假设您的网站之前运行良好，现在您可以通过在 Web way的 http 之后添加一个 "s" 来以安全的方式查看它。如果您之前通过 `http://www.acmemarina.com` 访问您的网站，现在可以通过访问 `https://www.acmemarina.com` 来安全地查看它。

# 创建自签名证书

生成和运行自签名 SSL 证书比拥有签名证书要简单得多，请执行以下操作：

- 1. 移除当前存在的密钥和证书：

```
# cd /etc/httpd/conf
# rm ssl.key/server.key ssl.crt/server.crt
```

- 2. 创建您自己的服务器密钥：

```
# make genkey
```

- 3. 输入以下内容创建自签名证书：

```
# make testcert
umask 0777 \
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key
x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
```

此时，该开始为证书输入一些识别信息了。在此之前，您必须解锁刚刚创建的私钥。输入您之前输入的密码即可。然后按照此示例程序：

您将被要求输入包含在证书请求中的信息。
您将输入的内容称为 Distinguished名称或 DN。
有很多字段，但您可以留一些空白
某些字段会有默认值，
如果您输入 '.\'，该字段将留空。

```
国家（两位字母代码）[GB]:US

州或省份（全名）[Berkshire]: Ohio
```

# 第 14 章：计算机安全问题

地区名称（例如，城市）[Newbury]: Cincinnati
组织名称（例如，公司）[My Company Ltd]:Industrial Press, Inc.
组织单位名称（例如，部门）[:LT
通用名称（例如，您的名称或您的服务器的主机名）
[] :www.industrialpressinc.com
电子邮件地址 [:webmaster@industrialpressinc.com

上述生成过程将所有文件置于项目文件夹中。您需要做的只是重启 Web 服务器，并在您的 URL 前用 https 替换 http。不要忘记：您将收到来自 Web 浏览器的证书验证消息，您可以安全地忽略它。

# 重启您的 Web 服务器

到目前，您已经注意到您的 Web 服务器每次启动时都会要求您输入证书密码。这是为了防止他人入侵您的服务器并窃取您的私钥。这种情况本该发生，您可以放心地知道私钥只是一团乱码。破解者将无法利用它。如果没有保护，破解者可能会获取您的私钥并轻松地伪装成您，在所有情况下都显得合法的。

如果您无法忍受每次 Web 服务器启动时都要输入密码，并且愿意承担增加的风险，可以移除私钥上的密码加密。只需执行以下操作：

```
# cd /etc/httpd/conf/ssl.key

# /usr/bin/openssl rsa -in server.key -out server.key
```
