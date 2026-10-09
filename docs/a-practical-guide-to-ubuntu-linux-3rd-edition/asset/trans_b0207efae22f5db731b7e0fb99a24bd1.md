
如果浏览器未显示目录列表，它会显示两种错误之一：**连接被拒绝**（Connection refused）或一个错误页面。如果您遇到**连接被拒绝**错误，请确保端口 80 未被防火墙阻止（第 901 页），并检查服务器是否正在运行：

```
$ ps -ef | grep apache2
max    3479  12869  0 16:55 pts/1    00:00:00 grep apache2
root     5031     1  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
www-data  5032  5031  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
www-data  5088  5031  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
www-data  5092  5031  0 Mar26 ?       00:00:00 /usr/sbin/apache2 -k start
```

如果服务器正在运行，请确认您在**Listen 指令**中指定的端口不是 80 以外的其他端口。如果是，您在浏览器中指定的**URL** 必须反映此端口号（**http://localhost:port** 指定端口 **port**）。否则，请检查错误日志（*/var/log/httpd/error_log*）以获取有关故障的信息。

为了验证不是浏览器的问题，请使用 **telnet** 尝试连接到服务器的 80 端口：

```
$ telnet www.example.com 80
Trying 192.0.34.166...
Connected to www.example.com.
Escape character is '^A'.
CONTROL-^
telnet> quit
Connection closed.
```

如果 **telnet** 显示**连接被拒绝**，这意味着本地系统无法连接到服务器。

## 模块

Apache 是一个骨架程序，依赖外部模块（称为动态共享对象，**DSO**）来提供其大部分功能。除了 Ubuntu Linux 自带的模块外，还有许多其他可用模块。请参阅 *httpd.apache.org/modules* 获取更多信息。请参阅第 905 页的 *a2enmod* 以了解有关启用模块的信息。

## 配置模块

> *提示* 您可以通过编辑 **mods-available** 目录中对应的 *.conf* 文件来配置某些模块。

存放模块的文件名以 **libapache2-mod-** 前缀开头。以下命令显示模块的完整列表。您可以通过 **grep** 管道列表来查找所需的模块。请参阅第 530 页了解 *apt-cache* 的信息。

```
$ apt-cache search libapache2-mod
libapache2-mod-auth-kerb - apache2 module for Kerberos authentication
libapache2-mod-auth-mysql - Apache 2 module for MySQL authentication
libapache2-mod-auth-pam - Module for Apache2 which authenticate using PAM
libapache2-mod-auth-pgsql - Module for Apache2 which provides pgsql authentication
libapache2-mod-authnz - Module for Apache2 which provides plaintext authentication
libapache2-mod-auth-sys-group - Module for Apache2 which checks user against system group
libapache2-mod-macro - Create macros inside apache2 config files
libapache2-mod-perl2 - Integration of perl with the Apache2 web server
libapache2-mod-perl2-dev - Integration of perl with the Apache2 web server - development files
libapache2-mod-perl2-doc - Integration of perl with the Apache2 web server - documentation
libapache2-mod-php5 - server-side, HTML-embedded scripting language (apache 2 module)
libapache2-mod-php5filter - server-side, HTML-embedded scripting language (apache 2...)
libapache2-mod-python - Apache 2 module that embeds Python within the server
...
```

```
$ apt-cache search libapache2-mod | grep ruby
libapache2-mod-ruby - Embedding Ruby in the Apache2 web server
```

## mod_cgi 和 CGI 脚本

CGI（通用网关接口）允许外部应用程序与 Web 服务器接口。任何程序只要实时运行（在请求时）并将其输出传递给请求客户端，就可以成为 CGI 程序。各种脚本，包括 shell、Perl、Python 和 PHP，是最常见的 CGI 程序，因为脚本可以调用程序并将其输出格式化为 HTML 以便客户端使用。

Apache 可以通过多种不同的方式处理 CGI 程序的请求。最常见的方法是将 CGI 程序放入 cgi-bin 目录，然后仅允许从该目录执行。由 ScriptAlias 指令（第 929 页）指定的 cgi-bin 目录位置是 /usr/lib/cgi-bin。或者，AddHandler 指令（第 923 页）可以识别常规内容中脚本的文件名扩展名，例如 .cgi 或 .pl（例如，AddHandler cgi-script .cgi）。如果使用 AddHandler，还必须在适当的 <Directory> 容器内的 Options 指令中指定 ExecCGI 选项。必须加载 mod_cgi 模块才能访问和执行 CGI 脚本。

以下 Perl CGI 脚本显示 Apache 环境。该脚本仅应用于调试，因为它如果远程客户端可以访问则存在安全风险：

```
#!/usr/bin/perl
##
## printenv -- demo CGI program that prints its environment
##

print "Content-type: text/plain\n\n";
foreach $var (sort(keys(%ENV))) {
    $val = $ENV{$var};
    $val =~ s/\n/\\n/g;
    $val =~ s/"/\"/g;
    print "$var=$val";
}
```

## mod_ssl

SSL（安全套接字层），由 mod_ssl 模块实现，有两个功能：它允许客户端验证服务器的身份，并启用客户端和服务器之间的安全双向通信。SSL 用于 Web 页面上需要密码、信用卡号或其他敏感信息的表单。

Apache 对 SSL 通信使用 HTTPS 协议——而不是 HTTP。当 Apache 使用 SSL 时，它会监听第二个端口（默认 443）以建立连接，并在向客户端发送请求的内容之前执行握手序列。

服务器验证对于金融交易至关重要。毕竟，您不希望将信用卡号交给冒充知名公司的欺诈性 Web 站点。SSL 使用证书来明确识别服务器。在公共网络（如互联网）上，只有当证书包含来自 VeriSign 或 Thawte 等权威来源的数字签名时，身份识别才是可靠的。SSL Web 页面由以 https:// 开头的 URI 标识。

数据加密可防止恶意用户窃听互联网连接并复制个人信息。为了加密通信，SSL 位于网络和应用程序之间，加密服务器和客户端之间的通信。

## 设置 mod_ssl

mod_ssl 包作为 apache2 包的一部分安装——您不需要单独安装它。/etc/apache2/mods-available/ssl.conf 文件配置 mod_ssl；同一目录中的 ssl.load 加载它。您必须使用命令 a2enmod ssl 启用该模块。该文件的前几条指令为 SSL 操作设置各种参数。

您可以在 sites-available 目录中为 SSL 设置虚拟主机，并使用 a2ensite（第 906 页）启用它。与任何虚拟主机一样，SSL 虚拟主机保存了需要配置的指令，如 ServerName 和 ServerAdmin。此外，它还保存了一些与 SSL 相关的指令。请参阅第 940 页的示例。

## 使用自签名证书进行加密

如果您需要用于加密而非验证的 SSL——即客户端已经信任服务器——您可以生成并使用自签名证书，从而绕过获取数字签名证书所涉及的时间和费用。自签名证书在您连接到服务器时会产生警告：大多数浏览器显示一个对话框，允许您检查和接受证书。exim4 守护进程也使用证书（第 736 页）。

以下示例创建了一个自签名证书。（如果系统中缺少 apache2-ssl-certificate，请参阅 www.modssl.org/docs/2.8/ssl_faq.html#To2.82if 上的程序。您不需要为自签名证书发送 CSR。）

```
$ sudo apache2-ssl-certificate
creating selfsigned certificate
replace it with one signed by a certification authority (CA)

enter your ServerName at the Common Name prompt

If you want your certificate to expire after x days call this program
with -days x
Generating a 1024 bit RSA private key ..............++++++++
............++++++++
writing new private key to '/etc/apache2/ssl/apache.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguishing Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value.
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [GB]:US
State or Province Name (full name) [Some-State]:California
Locality Name (eg, city) []:San Francisco
Organization Name (eg, company; recommended) []:Sobel1 Associates Inc.
Organizational Unit Name (eg, section) []:
server name (eg, ssl.domain.tld; required!!) []:www.sobel1.com
Email Address []:msg@sobel1.com
```

前五个问题的答案是任意的：它们可以帮助客户端在检查证书时识别站点。第六个问题（**服务器名称**）的答案至关重要。由于证书与服务器名称绑定，您必须准确输入服务器的 FQDN。如果您错误地输入此信息，服务器名称和证书名称将不匹配。浏览器将在每次建立连接时生成警告消息。

现在，您必须在 /etc/apache2/sites-available 中创建一个启用 SSL 的虚拟主机。基于名称的虚拟主机托管在 SSL 中不起作用，因为 Apache 用于区分基于名称的虚拟主机的 HTTP Host 头是加密的。您只能使用一个 SSL 证书，每个 IP 地址匹配一个域名。您可以拥有该 IP 地址上的多个虚拟主机，但如果它们通过 HTTPS 访问，客户端将收到证书与域名不匹配的错误。在启用新的虚拟主机并重启 Apache 后，新证书将投入使用。

以下是 /etc/apache2/sites-available/ssl 的通配符设置示例。使用 **sudo a2ensite ssl** 启用它。

```
<VirtualHost *:80>
Redirect permanent / https://www.sobel1.com/
</VirtualHost>
```
