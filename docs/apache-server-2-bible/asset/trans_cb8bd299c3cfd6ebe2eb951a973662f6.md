

您即将输入的是所谓的**区别名称**（Distinguished Name，简称 DN）。
字段有很多，但您可以留空其中一些。
某些字段会有默认值。
如果您输入“.”，该字段将被留空。
-----
国家名称（2 位代码）[GB]:US
州或省名称（全称）[Some-State]:California
所在地名称（例如，城市）[]:Sacramento
组织名称（例如，公司）[]:MyORG
组织单位名称（例如，部门）[]:CS
服务器名称（例如 ssl.domain.tld；必填!!!）
[]:Shea_evoknow.com
电子邮件地址 []:kabi@evoknow.com

名为 `httpd.pem` 的证书创建在您的 Apache 源分布目录的 `SSLConf/conf` 子目录中。

现在您已准备好配置 Apache。

## 配置使用 Apache-SSL 的 Apache

当您在“编译和安装 Apache-SSL 补丁以适配 Apache”部分运行 `make install` 时，它在您的 Apache 安装目录的 `conf` 子目录中创建了一个 `httpd.conf` 文件。例如，如果您使用 `--prefix=/usr/local/apache` 来配置 Apache，您将在 `/usr/local/apache/conf` 目录中找到 `httpd.conf` 文件。您需要使用 `mv` 命令将其重命名为 `httpd.conf`。如果您将在其他目录中安装 Apache，请确保将 `/usr/local/apache/conf/` 替换为适当的路径名。

在使用 Apache 中的 SSL 时，您有两种选择。您可以为主服务器启用 SSL，或者为一个或多个虚拟 Web 站点启用它。在这里，我将向您展示如何为主 Apache 服务器启用 SSL，并讨论您需要执行哪些操作才能为虚拟 Web 站点启用 SSL。请按照以下步骤修改 `httpd.conf` 文件：

- 默认情况下，Web 浏览器会将 SSL 请求发送到您的 Web 服务器的 443 端口，因此，如果您希望将主 Apache 服务器转换为支持 SSL 的服务器，请将 `Port` 指令行更改为：
  ```
  Port 443
  ```
- 添加以下行，以告知 Apache 如何生成加密 SSL 连接所需的随机数据：
  ```
  SSLRandomFile file /dev/urandom 1024
  SSLRandomFilePerConnection file /dev/urandom 1024
  ```
- 如果您希望拒绝除 https（即 SSL 请求）以外的所有请求，请插入以下指令：
  ```
  SSLRequireSSL
  ```
- 要启用 SSL 服务，请添加以下指令：
  ```
  SSLEnable
  ```
- 默认情况下，支持 SSL 的 Apache 所使用的缓存服务器创建在 Apache 源分布的 `src/modules/ssl` 目录中。请设置此目录，如下所示：
  ```
  SSLCacheServerPath \
  `/path/to/apache_version`/src/modules/ssl/gcache
  ```
- 添加以下指令以启用缓存服务器端口和缓存超时值：
  ```
  SSLCacheServerPort logs/gcache_port
  SSLSessionCacheTimeout 15
  ```
- 现在您需要告知 Apache 保存服务器证书文件的位置。如果您按照之前的 OpenSSL 安装说明创建了服务器证书，您的服务器证书应该位于 `/usr/local/ssl/certs` 目录中。但是，如果您决定暂时使用测试证书（通过之前讨论的 make_certificate 命令创建），那么您的测试证书位于 `/path/to/apache_version/SSLconf/conf` 目录中，名为 `httpd.pem`。请设置以下指令为您的服务器证书的完全限定路径，如下所示：
  ```
  SSLCertificateFile \
  `/path/to/apache_version`/SSLconf/conf/httpd.pem
  ```
- 设置以下指令并保存 `httpd.conf` 文件：
  ```
  SSLVerifyClient 3
  SSLVerifyDepth 10
  SSLFakeBasicAuth
  SSLBanCipher NULL-MD5:NULL-SHA
  ```
- 要在 443 端口上为名为 `myvhost.Evoknow.com` 的虚拟主机启用 SSL，我需要以下配置：
  ```
  Listen 443
  <VirtualHost myvhost.evoknow.com:443>
    SSLEnable
    SSLCertificateFile `/path/to/myvhost.certificate.cert`
  </VirtualHost>
  ```

您的支持 SSL 的 Apache 服务器已准备就绪，可以进行测试。

## 测试您的 SSL 连接

在使用 `/usr/local/apache/bin/apache -k startssl` 命令启动 Apache 服务器后，您应该能够使用 `http://localhost` 或 `https://your_server_hostname/` 从本地（在 Web 服务器本身）或远程 Web 客户端访问您的 SSL 站点。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_592_0.png)

> 大多数人在测试他们的 SSL 服务器时忘记使用 `https` 而使用了 `http`，当他们看不到 SSL 连接时就会惊慌失措（通常由大多数流行 Web 浏览器状态栏中的一个小锁图标显示）。

## 获取证书

在您使用 SSL（通过 mod\_ssl 或 Apache-SSL）使用 Apache 之前，您必须创建适当的服务器证书。您可以从商业证书颁发机构（CA）获取服务器证书，或者您可以创建自己的证书颁发机构，然后为您的服务器和客户端创建证书。后一种方法通常用于希望在校区之间内部管理证书的大型组织。

### 从商业 CA 获取服务器证书

要从商业 CA 获取签名证书，您必须满足其要求。有两种类型的要求：

- 您（请求者）必须证明您就是您声称的实体。
- 您必须提交电子形式的证书签名请求（CSR）。

第一个要求通常是通过遵循 CA 验证个人或组织指南来满足的，因此您必须咨询您选择的 CA 以了解如何继续。通常，如果您计划为 Web 服务器认证，请准备好提交法律文件副本，如商业登记或注册文件。或者，您可以使用 OpenSSL 创建 CSR。

创建 CSR 的第一步是为服务器创建私钥。然后您需要创建一个证书签名请求，该请求需要发送到商业证书颁发机构。在您获得商业证书颁发机构的批准后，您可以将证书安装到您的服务器上，并在 Apache 中使用 SSL。我将在以下部分中详细讨论这些步骤。

### 生成私钥

要为名为 `www.domain.com` 的 Web 服务器主机生成加密的私钥，请运行：

```
openssl genrsa -des3 -out www.domain.com.key 1024 -rand /dev/random
```

当您运行此命令时，您会被要求输入一个密码短语（即密码）来加密私钥。由于私钥是使用 `des3` 密码加密的，每次启动服务器时您都被要求输入密码短语。如果这是不理想的，您可以通过从上述命令行中移除 `-des3` 选项来创建非加密版本的私钥。我强烈建议您使用加密的私钥以确保高水平的安全性。毕竟，您不希望其他有权访问您服务器的人能够看到您的私钥。清单 19-1 显示了 www.domain.com.key 文件的内容。

**清单 19-1：www.domain.com.key 文件的内容**

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: DES-EDE3-CBC, C4B89F2F597AF68

47f4qGkrffT7NEyqEs/uYaPoeAqksOnALTkUVvADHKL7BbA+BB+rT/aaM7hhwEzU

jjaRd1XfkIej3qH6d/2I0AwFfyIAY0H13w082pI15uxui2sm7ZRyUDpRMjxzI
/srhn/DU+dlq1lpH3vJRw2hhNVJHUBOcuCsz8Z8GOhICa5MF6s2xDR+ckPOT2Uvf5
jLGiyrRoBzNQOFDv8wqZeOSOSuKHU9ZKda/PCb+wfyDWZfr8H9PNT1mlajMGt
19LWZkzBw2mmw79Pq6X5ycq+7dKMxiQL6d/dY1HOZUYHJm3jtqUlPI7NXjd4TG
k8xXbvxjPioVyFKoqhmVPq7Wd9enYU72RuVo+a105oTG2Gp15y37GkUnTy
1W8JFH5BuscSrP+95SKTKvOwOLnOjRtgxK/YEZTQEza4qPCsz6eiyAw4fFTaw
6q/G3ZJCpJBJ2YLmwvua3dpv9bucSCxmB0oX9vjEBB/yvj9pLbu5pSBKxA4th
fZcZB94wxrr/EM6GDs2xgnNh+SwF5F3c/bpURMCq/0t6FF/H47jVnUf1t7d0tTT7
UbdQvAAsr9tKSfzsRKMOGB4OvneuD5C2UI/3O/NaXS5/Efu9HGlctcRKwZEVI/+
MSJBe3JYDmB6mGDGNJUEXp64hv4jKo0NdkAjKE6K2E2w2o2al1F8u12PNotW6YD
T5hgoISm5mqQQLCfs5JH5TAbKxLejsygO5RzvPJS0KznWaHcLoFic14pDSor4ghM
6YEdaSBu1vSf3tn2vKsHueZHqFov51GcjBvEyAE0Y4QL0k9EznMBw=
-----END RSA PRIVATE KEY-----
```

### 生成证书签名请求

现在您需要使用您的私钥如下所示生成 CSR：

```
openssl req -new -key www.domain.com.key -out www.domain.com.csr
```

如果您之前加密了私钥，您会被要求输入私钥的密码短语。输入适当的密码短语。然后，您会被要求输入国家名称、州、城市、组织名称、组织单位（部门名称、通用名称（即，如果证书请求是为您自己，则是您的名字，或者是您的服务器的主机名）、电子邮件地址以及一些可选信息，如挑战密码和可选的公司名称。

在此阶段，您需要将您的 CSR 提交给像 Thawte 这样的 CA。因为认证过程涉及验证您的个人或业务身份文件，所以在您收到证书之前可能需要几天到几周甚至几个月的时间。以下部分使用 Thawte 作为选定的 CA。

