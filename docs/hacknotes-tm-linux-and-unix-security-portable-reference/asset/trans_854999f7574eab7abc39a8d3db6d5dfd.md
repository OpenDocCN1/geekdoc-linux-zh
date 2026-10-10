

## 在日志文件中查找敏感信息

许多已知程序会向特定的日志文件写入数据。有时，这些日志文件会被意外放置在 Web 服务器的网站根目录下。例如，像在 http://www.google.com/ 上执行类似 “Index of/ dead.letter” 的查询，会为您提供提供 dead.letter 文件的那些 Web 服务器的链接（参见图 1-1）。请注意，dead.letter 文件是由某些电子邮件客户端在用户取消发送电子邮件时创建的，它可能包含正在编辑的电子邮件的一部分内容。此文件以及其他类似的日志文件可能会向潜在的入侵者提供关键且机密的信息。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_59_0.png)

图 1-1. Web 服务器提供的用户 dead.letter 文件内容

还有许多其他众所周知的日志文件可以被搜索。其他示例包括 syslog、maillog、spooler、messages、access_log 和 error_log。

## 搜索 Web 服务器统计信息

各种 Web 应用程序被用于向管理员提供 Web 流量的统计信息。这些统计数据通常受密码保护，并且可能包含机密信息和 URL。可以使用搜索引擎来查找配置错误的托管服务器，这些服务器会提供此类数据。例如，在 http://www.google.com/ 上执行 “Index of" stats 的搜索可能会暴露那些被错误配置为向未经身份验证的外部实体提供服务器统计数据的 Web 服务器的位置（参见图 1-2）。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_60_0.png)

**图 1-2.** somecompanyasanexample.com 向全世界提供 Web 服务器统计数据

## 定位受保护的数据资源

敏感信息通常放置在网站中标有 “protected”、“secret”、“passwords” 等名称的目录内。很多时候，这些目录没有密码保护，可以轻松被搜索到。

作为一个例子，考虑 Apache Web 服务器，它通常被配置为在某些配置和密码文件存在于目录中时提供身份验证。密码文件通常称为 .htpasswd，不应该由 Web 服务器提供。要在 http://www.google.com 上搜索互联网上的此类文件，请执行以下查询：“Index of” .htpasswd。以下是 .htpasswd 文件的一个示例：

```text
joe:1wjdcj1jc0wGFA
admin:XrouH05qTMlU.
```

此文件中包含的密码哈希值可以使用 “John the Ripper” 等密码破解工具轻松破解。

```text
[bash]$ john .htpasswd
Loaded 2 passwords with 2 different salts (Traditional DES [24/32 4K])
mpasswd (joe) (admin)
guesses: 2 time: 0:00:00:21 (3) c/s: 83610 trying: bly045 - $1st20
```

John the Ripper 可在 http://www.openwall.com/john/ 获取。

## 在配置文件中查找敏感信息

各种包含密码、密钥、用户名、内部 IP 地址和其他敏感数据等信息的配置文件，当它们被放置在 Web 根目录内时，可能会被某些 Web 服务器错误地提供出来。搜索这些文件的关键在于知道它们的名称。一个潜在存在漏洞的文件是 sshd_config，它包含 SSH 服务器的配置信息。潜在入侵者可以使用查询 “Index of” sshd_config 进行搜索，以找到提供 sshd_config 文件的 Web 服务器。由于此类配置文件包含敏感信息，它们可能会暴露本不应被外部实体访问的关键信息。

## 搜索 Usenet 归档以发现管理疏忽

新闻组帖子通常包含可辅助攻击者的信息。例如，管理员有时会在技术 Usenet 组中发帖寻求关于某些主题的帮助。这些帖子可能会泄露大量信息，并提醒入侵者管理员在配置某些服务时遇到了困难。网站 **http://groups.google.com/** 可用于搜索此类泄露信息的帖子。

### 防范搜索引擎暴露漏洞

强烈建议实施以下防御策略，以最大限度地降低因搜索引擎和 Web 服务器配置错误导致敏感信息暴露的风险：

- 不要以可能暴露与安全相关管理弱点的方式宣传职位空缺。
- 定期审计您的 Web 服务器配置及其允许提供的数据是个好主意。如果您可以访问 Web 服务器本身，您可以从网站根目录内搜索特定信息。例如，以下命令将列出所有文件名中包含 “log” 单词的文件：
    ```bash
    ls -alR /var/web-root/html | grep log
    ```
- 静态数据中的内容也可以进行搜索。要搜索网站根目录中文件内容里的特定单词，例如 “password”，请使用：
    ```bash
    grep -R password /var/web-root
    ```
- 如果无法访问 Web 服务器文件系统的本地权限，wget 是一个很好的命令行工具，可用于镜像网站。一旦网站内容在本地可用，就可以像建议的那样对数据进行 grep 操作。wget 的使用示例：
    ```bash
    wget -m -np http://www.somecompanyasanexample.com/
    ```
- wget 工具可从 **http://wget.lsd.ic.ac.uk/** 获取。
- 必须指示管理员不要使用他们的真实姓名和电子邮件地址在技术新闻组和消息板上发布职位空缺信息。

## 域名注册商

一个单一组织可能在不同的位置拥有许多网络。通过执行 “whois” 查询可以发现与特定组织关联的域名。大多数域名注册商都有一个相关的公共 whois 服务器（监听端口 69），whois 客户端可以连接该服务器以查询域名所有者的信息。域名 whois 查询返回的信息包括相关的 POC（Point of Contact，联系点）和 DNS IP 地址，这对于确定目标的网络存在非常有用。

由于域名可以通过众多注册商注册，因此您必须首先查询域名注册的注册商，然后从相关的注册商查询域名记录。为了查询正确的注册商，必须对公共 whois 服务器 whois.crsnic.net 执行 whois 查询。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_63_0.png)

> 许多注册商限制了以下各节中提到的查询类型。如果以下任何查询都没有得到特定 whois 服务器的正面响应，它们也许会在另一个注册商的 whois 服务器上起作用。

### 按域名查询域名注册商记录

要查询 somecompanyasanexample.com，您必须使用命令行 whois 工具（大多数 Unix 和 Linux 发行版都包含此工具）在 whois.crsnic.net 上运行 whois 查询，如下所示：

```bash
[bash]$ whois -h whois.crsnic.net somecompanyasanexample.com
[whois.crsnic.net]
Whois Server Version 1.3
Domain names in the .com, .net, and .org domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.
Domain Name: SOMECOMPANYASANEXAMPLE.COM
Registrar: SOME REGISTRAR, INC.
Whois Server: whois.somewhoisserver.com
Referral URL: http://www.someregistrarasanexample.com
Name Server: NS1.SOMEEXAMPLESERVER.NET
Name Server: NS2.SOMEEXAMPLESERVER.NET
Updated Date: 05-nov-2001
>>> Last update of whois database: Sat, 11 Jan 2003 17:11:52 EST <<<
```

上述查询将返回域名的实际注册商及其 whois 服务器。在我们前面的示例中，somecompanyasanexample.com 的注册商的 whois 服务器是 whois.somewhoiserver.com。现在，我们必须查询 whois.somewhoiserver.com：

```text
NOTICE AND WARNING BANNER HERE

Registrant:
Lname,_fname (SOMEHANDLE)   username@somecompanyasanexample.com
1234 Some St.
Somecity, SOMESTATE 99999
SOME COUNTRY

Domain Name: somecompanyasanexample.com

Administrative Contact, Technical Contact:
Lname2,_fname2 (SOMEHANDLE2)  user2@somecompanyasanexample.com
5678 Something St.
Somewhercity, SOMESTATE 99999
SOME COUNTRY
(123)456-7890

Record expires on 31-12-2004
Record created on 31-12-2002
Database last updated on 12-Jan-2003 03:44:29 EST.

Domain servers in listed order:
NS1.SOMEEXAMPLESERVER.NET
NS2.SOMEEXAMPLESERVER.NET
```

### 按域名前缀查询域名注册商记录

为了搜索以 “somecompany” 开头的域名，可以使用以下查询：

```bash
[bash]$ whois -h whois.crsnic.net "somecompany."
[whois.somewhoiserver.com]
Whois server version 1.x

NOTICE AND WARNING BANNER HERE

SOMECOMPANY.COM
SOMECOMPANY.ORG
SOMECOMPANYASANEXAMPLE.COM
SOMECOMPANYTHATDOESNOTEXIST.COM
```

