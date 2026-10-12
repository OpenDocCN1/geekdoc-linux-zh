
## 第 15 章：Web 服务器与 Apache 的 LAMP

这些选项通常非常直观；例如，`sudo apachectl start` 命令启动了 Apache 服务。`graceful` 和 `graceful-stop` 选项分别重启和停止 Apache 服务，而不会中断任何活动连接。

> 提示 每当你想检查 Apache 配置文件的语法情况时，请运行 `sudo apache2ctl config` 命令。当你准备好测试结果时，使用 `sudo apache2ctl configtest` 命令重启服务，然后在浏览器中检查结果。它会在不断开当前用户连接的情况下重新加载 Apache 配置文件。

`configtest` 选项最有用；它作为 `/etc/apache2/conf` 配置文件的语法检查器。正如你所看到的，它包含了将编辑以提供实际网站的文件中的指令。它结合了以前可用命令的功能，并与 `apache2` 手册页中的选项一起工作。一个与配置相关的 apache2 命令是 `-S` 开关，它会显示每个普通和安全虚拟主机的 TCP/IP 端口号、URL 和配置文件。在你稍后在本节中配置虚拟主机后，运行 `apache2ctl config` 和 `sudo apache2ctl -S` 命令并观察输出。

> 注意 较版本的 `apache2ctl` 命令包含了用于安全网站的 `startssl` 选项。这种支持现在也是 `start` 和 `stop` 选项的一部分。

`apache2ctl status` 命令提供有关服务器和相关活动的信息。示例输出如图 15-4 所示。`apache2ctl fullname status` 包含了进程标识符 (PIDs)、安全服务器 (SSL/TLS) 连接、主要模块等信息。

### 检查第一个主机

第一个主机配置在 `/etc/apache2/sites-enabled/default.conf` 文件中。

如所述，以下 `ServerSignature` 指令允许在错误消息中使用页脚。

```
ServerSignature On
```

以下指令将对文档的访问限制在本地主机 localhost 系统，如 `Allow from` 指令所示。地址 `127.0.0.0/255.0.0.0` 可以更改为 `192.168.0.0/24` 等设置，以允许访问所需的网络。

```
Alias /doc "/usr/share/doc/"

<Directory "/usr/share/doc/">

  Options Indexes MultiViews FollowSymLinks

  AllowOverride None

  Order deny,allow

  Deny from all

  Allow from 127.0.0.0/255.0.0.0 ::1/128

</Directory>
```

文件中的最后一个指令关闭了虚拟主机语句：

```
</VirtualHost>
```

### 配置虚拟主机

在配置虚拟主机之前，请为 `/etc/apache2/sites-enabled` 目录下的 `000-default` 文件创建一个副本，你可以使用以下命令进行操作：

```
$ cd /etc/apache2/sites-enabled
$ sudo cp 000-default website1
```

然后创建一个专用的 Web 页面和日志目录。我在这里指定了一些任意目录。你使用的目录名称也必须在虚拟主机文件中指定。

```
$ sudo mkdir /var/www/website1
$ sudo mkdir /var/log/apache2/website1
```

现在打开 `website1` 文件。首先，添加至少一个通用指令，该指令反映了网站的名称：

```
ServerName sitel.example.org
```

通常会使用 `ServerAlias` 指令对应可能使用的每个主机或域名，例如如下：

```
ServerAlias www.example.org
```

#### 第 15 章：Web 服务器与 Apache 的 LAMP 架构

然后，为了反映刚刚创建的新目录，请更改以下指令：
- `ServerAdmin`: 设置为网站管理员的电子邮件地址
- `DocumentRoot`: 配置为存放网站文件的目录——在本例中为 `/var/www/website1`
- `<Directory <dir>>`: 将 `/dir` 替换为 `DocumentRoot` 目录目录
- `ErrorLog`: 设置为日志文件的专用目录
- `CustomLog`: 设置为日志文件的专用目录

这些仅基于 Ubuntu Apache 服务器随带的默认配置的细微更改。根据任何自定义配置，可能需要进行类似的更改。

一旦配置了第一个虚拟主机，你就可以向 `DocumentRoot` 目录添加 Web 页面。要测试虚拟主机，只需要一个文本文件。例如，对于此虚拟主机，我在 `/var/www/website1` 目录中创建了一个 `index.html` 文件。我在这个文件中添加了简单的文本，如图 15-5 所示。

为了为远程客户端测试或配置此网站，我可能需要更改每个客户端上的 `/etc/hosts` 配置文件，或者将指定的网站名称添加到 DNS（域名系统）数据库中。

现在我可以根据需要对多个虚拟主机重复此过程。鉴于 Apache 主配置文件（`/etc/apache2/apache2.conf`）中的以下内容：

```
Include /etc/apache2/sites-enabled/
```
该目录中的所有文件都会包含在 Apache 配置中。

![](img/fadb0f527b947cf4d02cbbbb791a6562_421_0.png)

图 15-5. 测试虚拟主机

### 配置安全虚拟主机

在公众视野中，网站被认为使用加密通信。稍微get敏感的用户知道通过协议 HTTPS 识别安全网站。安全性由安全套接层（SSL）协议及其继任者传输层安全（TLS）提供。HTTPS 的文档引用仍使用 SSL，因此此处使用了它。

要配置虚拟主机，你需要采取四个基本步骤。首先，启用 SSL 模块，该模块在 Ubuntu 安装的默认 Apache 包中可用。接下来，创建 SSL 证书——可以通过官方证书机构 (CA) 的帮助，也可以创建一个“自签名”证书。接下来，更改与普通虚拟主机关联的配置文件将其范围限制在普通网站的标准 TCP/IP 端口 (80)。最后，你可以根据用于普通网站的虚拟主机模板创建一个安全虚拟主机。

#### 启用 SSL 模块

SSL 模块包含在默认 Apache 服务器包 `apache2.2-common` 中。要在 Apache 配置中启用 SSL 模块，请运行以下命令：

```
$ sudo a2enmod ssl
```

当下次 Apache 重启时，`ssl.conf` 和 `ssl.load` 文件将包含在 `/etc/apache2/mods-enabled` 目录下的启用模块列表中。如果由于原因你想重启进程，`a2dismod` 命令可以提供帮助。

#### 创建 SSL 证书

如果没有私钥-公钥密钥对，对浏览器中使用 `https://` 访问安全网站的连接将是不安全的。互联网上适当安全的网站使用由 CA 生成的官方公钥对。但此类官方密钥对可能昂贵，且学习如何配置安全虚拟网站并非必须。加密基于基于互联网工程任务组 (IETF) 的 X.509 标准的公钥基础设施。在本节列出的加密密钥文件名（`server.key`、`server.csr` 和 `server.crt`）是任意的。在本节列出的命令会在本地目录创建上述的文件。

创建自签名证书的一种方法是使用 `openssl` 命令。步骤如下：

```bash
$ openssl req -new -newkey rsa:2048 -key server.key -out server.csr
```

该命令将提示输入信息：
- 国家名称（两位字母）：US
- 州或省：California
- 城市：San Francisco
- 组织名称：My Company
- 常用名称：example.com
- 电子邮件地址：admin@example.com

生成 CSR 后，你可以使用以下命令创建自签名证书：

```bash
$ openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

现在你有了一个私钥（`server.key`）和一个证书（`server.crt`）。它们将用于配置你的安全虚拟主机。

## 第 15 章：Web 服务器与 Apache 的 LAMP

为了确保系统安全，在虚拟主机容器内部需要四个特殊的指令。第一个指令直观易懂，因为它激活了 SSL 协议引擎：

```
SSLELEngine on
```
