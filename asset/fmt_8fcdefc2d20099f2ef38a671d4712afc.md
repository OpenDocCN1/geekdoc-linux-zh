
`rpm -q httpd`


如果没有结果，说明你没有安装 Apache 软件包，你可以跳过其余步骤。在我们的系统上，Apache 已经安装，输出如下：
`httpd-2.0.48-1.2`

### 2. 如果你得到了结果，请找到该包的依赖项，以便你可以先删除它们：
`rpm -q --whatrequires httpd`

在我们的系统中，返回的结果如下：
`redhat-config-httpd-1.1.0-5`

### 3. 开始从你的系统中删除软件包，从依赖项开始：
`rpm -e redhat-config-httpd`

### 4. 确保没有 Apache Apache 服务器在运行，如果它们仍在运行，请杀死它们：
`ps aux | grep httpd`
`killall httpd`

系统似乎已经清空了 Apache，现在我们继续获取源文件并进行解压。

## 下载并解压 Apache

为了给安装做准备，你需要下载 Apache 1.3。我们建议你从官方源获取文件，因此请访问 `httpd.apache.org/download.cgi` 并在 Apache 1.3 章节下选择 Unix Source（Unix 源码）。文件名应类似于 `apache_1.3.XX.tar.gz`。

> 在你下载时，我们留下了具体的版本号，它可能比我们编写本文时使用的版本更高。

- 使用以下步骤解压 Apache：
1. 创建新目录：
`mkdir -p /usr/local/src/webserver`
在我们的 Fedora 系统上，我们创建了一个位于 `/usr/local/src/webserver` 的新目录。
2. 使用 `wget` 下载源码：
`wget 'http://apache.archive.com/httpd/apache_1.3.29.tar.gz'`

> 我们应该检查 `http://httpd.apache.org` 以获取更新的下载 URL。此步骤中的示例 URL 可能会随时间推移失效。

- 3. 解压源码文件：
`tar zpxf apache_1.3.29.tar.gz`
你现在应该可以看到一个名为 `apache_1.3.29` 的目录。

## 通过防火墙允许 HTTP 服务器访问

在第 6 章“Linux 安全”中，你已经为服务器配置了防火墙。现在你需要扩展防火墙设置，并为你的 Web 服务器允许适当的 HTTP 访问。让我们为你的防火墙添加 HTTP 和 HTTPS 访问。

- 如果你没有为普通 HTTP 访问启用 80 端口或为 HTTPS 访问启用 443 端口，现在需要这样做。

我们在你的端口访问部分添加了以下行：
```bash
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

这被认为是安装并运行 Apache Web 服务器的最快方法。请按照以下步骤操作：

- 1. 我们从运行配置脚本开始：
   `cd /usr/local1/src/webserver/apache_1.3.29`
   `./configure`

- 2. 关注错误输出，然后运行 `make`：
   `make`

- 3. 运行 `make install` 命令将文件复制到 `/usr/local/apache` 目录：
   `make install`
   关注错误输出。
   默认情况下，您的 Apache 文件将安装到 `/usr/local/apache`。

- 4. 将您的 `apachectl` 链接到系统路径中：
   `ln -s /usr/local/apache/bin/apachectl /usr/bin/apachectl`
   `ln -s /usr/local/apache/bin/apachectl /usr/sbin/apachectl`

- 5. 启动 Apache！
   `apachectl start`

- 6. 在浏览器浏览器通过主机名或 IP 地址访问您的机器：`http://yourdomain.com`。您应该看到之前图 8.1 所示的精美 Apache Web 服务器临时页面。

## 使用 SSL 动态共享对象安装方法

该安装方法包含安全套层（SSL）并使用动态共享对象。在开始此安装方法之前，您必须进行一些准备工作。

## 下载并编译 OpenSSL

当您准备安装带有 `mod_ssl` 的 SSL 版本 Apache 时，必须先下载并编译 OpenSSL。您不需要安装 OpenSSL，因为我们需要为 `mod_ssl` 安装构建所需的头文件，而且您的服务器上已经存在一个用于证书管理的默认安装。现在让我们开始编译 OpenSSL 吧。

- 1. 下载 OpenSSL 和 `mod_ssl` 以便能够编译带 SSL 的 Apache：
   `cd /usr/local1/src/webserver`

在下载文件之前，请始终检查 `www.openssl.org/source` 上标记为 `[Latest]` 的版本。

```
wget http://www.openssl.org/source/openssl-0.9.7c.tar.gz
```

在下载文件之前，请始终检查 `www.modssl.org` 的最新版本。

```
wget http://www.modssl.org/source/mod_ssl-2.8.16-1.3.29.tar.gz
```

- 2. 解压源码

```
tar zpf openssl*
tar zpf mod_ssl\*
```

- 3. 对于此安装，您不需要安装 OpenSSL；您只需要为 `mod_ssl` 构建所需的源码头文件：

```
cd /usr/local/src/webserver/openssl-0.9.7c
./config
make
```

## 创建安装脚本

正如我们之前提到的，我们总是创建一个脚本来运行那些冗长的配置选项，而不是尝试记忆我们编译系统时使用的参数。以下是创建安装脚本的步骤：

- 1. 在 `/usr/local/src/webserver` 中创建一个名为 `_ssl_install` 的文件，并其中添加以下内容：

```
cd /usr/local/src/webserver/mod_ssl-2.8.16-1.3.29
./configure \
  --apache=/usr/local/src/webserver/apache_1.3.29 \
  --ssl=/usr/local/src/webserver/openssl-0.9.7c \
  --prefix=/www/ \
  --enable-module=so \
  --enable-module=rewrite \
  --enable-shared=rewrite \
  --enable-module=setenvif \
  --enable-shared=setenvif \
  --enable-module=mime \
  --enable-shared=mime \
  --enable-module=mime_magic \
  --enable-shared=mime_magic \
  --enable-module=dir \
  --enable-shared=dir \
  --enable-module=auth \
  --enable-shared=auth \
  --enable-module=access \
  --enable-shared=access \
  --enable-module=alias \
  --enable-shared=alias \
  --enable-module=status \
  --enable-shared=status
```

```
--enable-module=userdir \
--enable-shared=userdir \
--enable-module=vhost_alias \
--enable-shared=vhost_alias \
--enable-module=env \
--enable-shared=env \
--enable-module=log_referer \
--enable-shared=log_referer \
--enable-module=log_config \
--enable-shared=log_config \
--enable-module=log_agent \
--enable-shared=log_agent \
--enable-module=headers \
--enable-shared=headers
```

您应该会注意到此脚本与我们之前的非 SSL 安装有几处不同。最明显的区别是您需要进入 `mod_ssl` 目录进行初始配置。此外，您必须定义 Apache Web 服务器文件和 OpenSSL 源码的位置。脚本的其余部分与“使用非 SSL 动态共享安装方法”部分显示的脚本非常相似。

- 2. 为您的脚本添加执行权限并运行它：
```bash
```
