
$ ps -ef | grep apache2

max 5479 12069 0 16:55 pts/1 00:00:02 grep apache2 -k start

root 5031 1 0 Mar 26 00:00:02 /usr/sbin/apache2 -k start

www-data 5032 0 0 Mar 26 00:00:02 /usr/sbin/apache2 -k start

www-data 5033 0 0 Mar 26 00:00:02 /usr/sbin/apache2 -k start

如果服务器正在运行，请确认你没有在 `Listen` 指令中指定除 80 以外的端口。如果你指定了，则在浏览器中指定的 URI 必须反映该端口号（查看 `/var/log/http/error_log` 可指定端口）。否则，请检查错误日志获取有关无法运行的信息。

要验证不是浏览器的问题，请使用 `telnet` 尝试连接服务器的 80 端口：

```
$ telnet www.example.com 80

Trying to 192.0.34.166...

Connected to www.example.com.

Escape character is '^'.

CONTROL> Connection closed.

telnet> quit
```

如果 `telnet` 显示 `Connection refused`，意味着本地系统无法连接到服务器。

# 模块

Apache 是一个骨架程序，它依赖外部模块（称为动态共享对象，DSOs）来提供大部分功能。除了 Ubuntu Linux 自带的模块外，还有许多其他模块可用。更多信息请参阅 http://apache.org/modules。有关启用模块的信息，请参阅 `a2enmod` 页（第 905 页）。

## 配置模块

tip 你可以通过编辑 `modules-available` 目录下对应的 `.conf` 文件来配置某些模块。

存放模块的文件名以 `libapache2-mod-` 前缀开头。以下命令显示模块完整列表。你可以通过 `grep` 过滤列表来查找你需要的模块。有关 `apt-cache` 的信息请参阅第 530 页。

### 第 26 章 APACHE：设置 Web 服务器

```
$ apt-cache search libapache2-mod

libapache2-mod-auth-kerber - 用于 Kerberos 认证的 Apache 2 模块

libapache2-mod-auth-mysql - 用于 MySQL 认证的 Apache 2 模块

libapache2-mod-auth-pam - 用于 Apache 认证 PAM 的 Apache 模块

libapache2-mod-auth-pgsql - 提供 pgsql 认证的 Apache 模块

libapache2-mod-auth-plain - 提供明文认证的 Apache 模块

libapache2-mod-auth-sys-group - 检查用户系统组的 Apache 模块

libapache2-mod-macro - 在 apache 内部创建宏

libapache2-mod-perl2 - perl 与 Apache 服务器的集成

libapache2-mod-perl2-dev - perl 与 Apache 服务器的集成 - 开发文件

libapache2-mod-perl2-doc - perl 与 Apache 服务器的集成 - 文档

libapache2-mod-php5 - 服务器端、嵌入 HTML 的脚本语言（apache 2 模块）

libapache2-mod-php-filter - 服务器端、嵌入 HTML 的脚本语言（apache 2...）

libapache2-mod-python - 在服务器中嵌入 Python 的 Apache
```

```
$ apt-cache search libapache2-mod-ruby | grep ruby

libapache2-mod-ruby - 在 Apache Web 服务器中嵌入 Ruby
```

## mod_cgi 与 CGI 脚本

CGI（通用网关接口）允许外部应用程序与 Web 服务器交互。只要程序是实时运行（在请求发生时运行）并将其输出中继给请求客户端，任何程序都可以作为 CGI 程序。各种类型的脚本（包括 Perl、Python 和 PHP）是遇到常见的 CGI 程序，脚本可以调用它们并将其输出重新格式化为 HTML 供给客户端。

Apache 可以通过几种不同的方式处理 CGI 程序。最常见的方法是将 CGI 程序放在 `cgi-bin` 目录中，然后启用从该目录的执行。`cgi-bin` 目录的位置由 `ScriptAlias` 指令（第 929 页）指定，为 `/usr/lib/cgi-bin`。或者，可以使用 `AddHandler` 指令（第 923 页）识别普通内容中的脚本扩展名，例如 `.cgi` 或 `.pl`（例如 `AddHandler cgi-script .cgi`）。如果你使用 `AddHandler`，则必须加载 `mod_cgi` 模块才能访问并执行 CGI 脚本。

Perl CGI 脚本显示 Apache 环境。此脚本应仅用于调试，因为如果客户端可以访问它将存在安全风险：

```
#!/usr/bin/perl

##

## perl printenv 打印其环境

##

print "Content-type: text/plain\n\n";

foreach $var (sort(keys%ENV)) {

	$val = $ENV{$var};

	$val = s/\n/\\n/g;

	$val = s/\"/\\\"/g;

	print "$var=\\\$val\n";

}
```

# 模块 943

### mod_ssl

SSL（安全套接层）由 `mod_ssl` 模块实现，具有两个功能：它允许客户端验证服务器的身份并确保加密通信。Apache 使用 HTTPS 来防止敏感数据被窃听。

### 设置 Web 服务器

你现在必须在 `/etc/apache2/sites-available` 中创建一个启用了 SSL 的虚拟主机。没有 SSL，基于主机名的托管（Host-by-name hosting）将无法工作；因为客户端发送的 HTTP Host 头意味着 Apache 虚拟主机之间的区别是加密。你可以在该 IP 地址上拥有多个虚拟主机，但如果通过 HTTPS 访问，客户端将收到证书与域名不匹配的错误。在启用新的虚拟主机并重启 Apache 后，新证书将生效。

### 使用自签名证书进行加密

如果你需要没有证书机构的 SSL，可以生成自签名证书。当连接到服务器时，浏览器将显示警告信息，因为它不是签名的证书。

你将被要求输入将包含在证书请求中的信息。你将被要求输入所谓的“区别名称”（Distinguished Name 或 DN）。有几个字段可以留空。某些字段会有默认值。如果你输入 `.`，该字段将留空。

前五个问题的答案是任意的：第六个问题的答案（服务器名称）是强制性的。你必须准确输入服务器的 FQDN（完全域名）。如果此信息不匹配，服务器名称和证书名称将不匹配。

```
Country Name (2 letter code) [GB]:US

State or Province Name (full name) [Some-State]:California

Location Name (eg, city) [:San Francisco

Organization Name (eg, company, recommended) [:Sobell Associates Inc.

Organizational Unit (eg, section) [:server name (eg, ssl.domain.tld; required!!):www.sobell.com

Email Address [:]:example@example.com
```

生成 1024 位 RSA 私钥 .................+
+++++
写入新私钥到 '/etc/apache2/ssl/apache.pem'

以下是 `/etc/apache2/sites-available/` 的通配符设置示例。通过 `VirtualHost *:80` 启用它：

```
<VirtualHost *:443>

<Redirect permanent / https://www.sobell.com/

</VirtualHost>
```

# 模块 945

```
<VirtualHost :443>

ServerName www.sobell.com

SSLEngine On

SSLCertificateFile /etc/apache2/ssl/apache.pem

DocumentRoot /var/www

</VirtualHost>
```
