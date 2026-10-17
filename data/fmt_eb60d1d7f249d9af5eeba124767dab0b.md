
## 安装步骤

5. 运行 `cd ..` 命令将当前目录变回 `src`。
6. 运行 `./configure` 命令，并附上你通常使用的任何命令行参数。例如，如果你想将 Apache 安装到 `/usr/local/apache`，请使用 `--prefix=/usr/local/apache` 选项运行此脚本。
7. 运行 `make && make install` 命令来编译和安装 Apache。

这将编译并安装标准（`httpd`）和启用 SSL（`httpsd`）的 Apache。现在你需要为 Apache 创建一个服务器证书。

### 为 Apache-SSL 服务器创建证书

若要创建一个临时证书以便快速开始，请遵循以下步骤：

1. 进入 Apache 源代码分发目录下的 `src`（例如 `/usr/local/src/httpd_version/src`）子目录。
2. 进入 `src` 目录后，运行 `make certificate` 命令以创建一个仅用于测试目的的临时证书。`make certificate` 命令使用 `/usr/local/ssl/bin/openssl` 程序为你创建一个服务器证书。你会被问到几个不言自明的问题。以下是此命令的一个会话示例：

```
ps > /tmp/ssl-rand; date >> /tmp/ssl-rand ;\
RANFILE=/tmp/ssl-rand /usr/local/ssl/bin/openssl req -config
../SSLconf/conf/ssl.cnf \\
-new -x509 -nodes -out ../SSLconf/conf/httpsd.pem \\
-keyout ../SSLconf/conf/httpsd.pem ; \\
In -sf httpsd.pem ../SSLconf/conf/ \usr/local/ssl/bin/openssl
\
x509 -noout -hash < ../SSLconf/conf/httpsd.pem ; .0; \\
rm /tmp/ssl-rand

Using configuration from ../SSLconf/conf/ssl.cnf
Generating a 1024 bit RSA private key
..........................................+++++
.................................................+++++
writing new private key to '../SSLconf/conf/httpsd.pem'
-----
You are about to be asked to enter information that will be
incorporated
into your certificate request.
```

您即将输入的是所谓的 `区别名称`（`Distinguished Name`，简称 `DN`）。
字段有很多，但您可以留空其中一些。
某些字段会有默认值。
如果您输入“.”，该字段将被留空。

```
-----
国家名称（2 位代码）[GB]:US
州或省名称（全称）[Some-State]:California
所在地名称（例如，城市）[]:Sacramento
组织名称（例如，公司）[]:MyORG
组织单位名称（例如，部门）[]:CS
服务器名称（例如 ssl.domain.tld；必填!!!）
[]:Shea_evoknow.com
电子邮件地址 []:kabi@evoknow.com
```

名为 `httpd.pem` 的证书创建在您的 Apache 源分布目录的 `SSLconf/conf` 子目录中。

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

- 现在您需要告知 Apache 保存服务器证书文件的位置。如果您按照之前的 OpenSSL 安装说明创建了服务器证书，您的服务器证书应该位于 `/usr/local/ssl/certs` 目录中。但是，如果您决定暂时使用测试证书（通过之前讨论的 `make_certificate` 命令创建），那么您的测试证书位于 `/path/to/apache_version/SSLconf/conf` 目录中，名为 `httpd.pem`。请设置以下指令为您的服务器证书的完全限定路径，如下所示：

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
