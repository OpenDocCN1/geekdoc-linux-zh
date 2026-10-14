

默认情况下，Ubuntu 并未激活 Apache SSL 模块，该模块允许你在传输网页时使用加密。SSL 模块要求你拥有一个有效的证书用于加密。

你可以从授权的证书颁发机构（CA）购买证书，或者如果在 Ubuntu 服务器安装过程中选择了安装 SSL，也可以使用 OpenSSL 包创建自己的自签名证书。

要创建自签名证书，请按照以下步骤操作：

- 1. **使用以下命令为证书生成密钥：**
  ```
  openssl genrsa -des3 -out server.key 1024
  ```
  输入一个密码短语来保护密钥免受未经授权的修改。
- 2. **生成证书签名请求（CSR），用于在证书中标识你和你的服务器。使用以下命令执行此操作：**
  ```
  openssl req -new -key server.key -out server.csr
  ```
  你在步骤 1 中创建的 server.key 文件必须位于你运行此命令的文件夹中。此命令会询问你的姓名、组织和服务器信息。这些信息将用于在证书中标识你给你的客户。
- 3. **使用以下命令创建自签名证书：**
  ```
  openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
  ```
  你之前生成的 server.key 和 server.csr 文件必须位于你运行此命令的同一文件夹中。
- 4. **将密钥和证书复制到服务器 /etc/ssl 文件夹位置：**
  ```
  sudo cp server.key /etc/ssl/private
  sudo cp server.crt /etc/ssl/certs
  ```
- 5. **在 Web 主机的 default-ssl 虚拟主机配置行中指定文件位置：**
  ```
  SSLCertificateFile /etc/ssl/certs/server.crt
  SSLCertificateKeyFile /etc/ssl/private/server.key
  ```
- 6. **在 Apache 中启用 SSL 模块：**
  ```
  sudo a2enmod ssl
  ```
- 7. **使用以下命令将 default-ssl 虚拟主机添加到已启用的站点中：**
  ```
  sudo a2ensite default-ssl
  ```

现在你应该能够使用 HTTPS 协议连接到你的网站。当你使用自签名证书时，大多数 Web 浏览器会产生警告消息，指出接受来自 Web 服务器的自签名证书存在安全风险。自签名证书不应在生产环境中使用，因为它迫使用户接受你作为签名机构。

## MySQL 软件

一个成功的动态网页环境的主要组件是用于存储和访问数据的数据库。开源世界中使用最广泛的数据库平台是 MySQL 数据库服务器。

MySQL 的流行很大程度上源于它曾是 PHP 编程语言的原始默认数据库（然而，PHP 现在可以与许多不同的数据库包接口），以及 MySQL 数据库服务器的速度。

原始的 MySQL 数据库服务器以速度快但不够健壮而闻名。它缺乏商业数据库中常见的许多高级功能，例如事务、外键和行级记录锁定。

为了解决这个问题，MySQL 的开发人员重新设计了 MySQL，使其能够使用多个存储引擎。存储引擎是数据库服务器的核心。它处理数据库接口——为服务器存储、管理和删除数据。

MySQL 现在支持几种不同类型的存储引擎，每种都有不同的专长。表 21-3 列出了 MySQL 中可用的不同存储引擎。

| Table 21-3: The MySQL Storage Engines |
| Engine | Description |
| MyISAM | The original storage engine; speedy, but lacking many advanced database features |
| InnoDB | The newest, full-featured storage engine; although it supports many commercial-quality features, it's significantly slower than the MyISAM storage engine |
| Memory | Provides tables in memory |
| Merge | Combines multiple MyISAM tables into a single table |
| CSV | Stores data as comma-separated values in text files |

许多高流量的 Web 应用站点仍然使用原始的 MyISAM 存储引擎以获得其速度特性，牺牲高级功能换取性能。

以下各节描述了如何在 Ubuntu 服务器上使用已安装的 MySQL 数据库服务器。

## 访问服务器

在 Ubuntu 服务器上，你通过命令行界面工具访问 MySQL 服务器。mysql 程序允许你连接到 MySQL 服务器、执行 SQL 命令并查看结果。

要使用 root 用户账户连接到默认的 MySQL 数据库，输入

```
mysql -u root -p
```

输入密码后，你应该处于 MySQL 提示符处：

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with : or \g.
```

