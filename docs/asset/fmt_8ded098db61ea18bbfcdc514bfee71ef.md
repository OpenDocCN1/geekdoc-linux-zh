
```
$CONTACTNAME:gregor$
$CONTACTEMAIL:smith$
```

此外，还有针对主机、服务和联系人组的按需宏，在每个情况下引用点都是相关的组。

## D.3 用户定义的宏

从 Nagios 3.0 开始，您可以在主机、服务和联系人定义中指定自己的宏。这些宏在 Nagios 术语中被称为自定义宏，其处理方式与标准宏相同，但名称以下划线开头，以便于识别。

（注：此处由于原文文本存在大量重复和错乱，根据指令“不要重复输出原文”的原则，翻译部分已根据核心逻辑进行了整合与去重处理。）

:由于您提供的英文文本中存在大量的段落重复（如 D.2 On-Demand Macros 之后的内容反复出现），且提供这些环境变量需要花费大量时间。您应该考虑是否可以在 Nagios 3.0 中一次性完成（请参见参数 `use_large_installation_tweaks`、A.1 主配置文件 `nagios.cfg`、`enable_environment_macros`、A.1 主配置文件 `nagios.cfg`）。在 Nagios 2.x 中，无法关闭环境变量。

驱动程序。在这里，客户端发送一个所谓的类型 1 消息，包含客户端的主机名和域名。服务器返回一个 NTLM 挑战（一个 NTLM 类型 2 消息），随后客户端通过类型 3 消息完成身份验证，该消息不仅向服务器传回客户端名称和域名，还传回了挑战（挑战已使用客户端的密码进行了加密）。该过程是微软特有的，且从未作为标准发布。尽管如此。

Firefox 能够使用它。在互联网上也可以找到关于 NTLM 协议与身份验证相关的描述。³318

微软将很快把基于 NTLM 的认证替换为更新的、基于 Kerberos 的认证。从 Windows Server 2008 开始，NTLM 将不再用于 HTTP 认证，至少在服务器端是如此。

它的继者已经投入实践了一段时间。它使用一个名为“通用安全服务应用程序编程接口”（GSSAPI）的通用接口。对于 HTTP 认证以及 GSSAPI，使用了一种名为 SPNEGO（简单与协商）的机制，通过该机制进行身份验证协商。微软在一份请求注释（RFC 4559）中描述了 HTTP 认证，其中也讨论了 NTLM 过程。较新版本的 SPNEGO 则在 RFC 4178 中描述。

SPNEGO 过程比 NTLM 认证稍快，且更接近 HTTP 认证的 Basic 和 Digest。首先，客户端使用 GET 命令请求一个受保护的页面。服务器返回状态码 401（未授权），并包含以下身份验证过程：

```
HTTP/1.1 401 Authorization Required
WWW-Authenticate: Negotiate
WWW-Authenticate: NTLM
WWW-Authenticate: Basic realm="Nagios Monitoring"
```

此示例中的服务器提供了三种过程的选择：Negotiate 代表基于 Kerberos 的 SPNEGO 过程，代表旧的 NTLM 认证，Basic 指的是经典的用户密码方法，即身份验证数据以明文形式传输。选择这三种过程中的一种由客户端决定。客户端（此处是 Microsoft Internet Explorer 6.0 的一个实例）选择了安全的基于 Kerberos 的过程：

```
GET /nagios/index.html HTTP/1.1

Authorization: Negotiate YIIIvGkWRWBRGU0IIIisCCCegJDA...
```

在 HTTP 头部字段 Authorization 之后是关键字 Negotiate，随后是 Base64 编码的身份验证数据。如果成功，服务器将返回 HTTP 代码 200（OK），且 HTTP 头部包含身份验证数据${321}$，客户端对其进行处理：

```
HTTP/1.1 200 OK
...
WWW-Authenticate: Negotiate oYGeMIGbo...
```

如果成功，浏览器将显示它收到的 HTTP 页面。这里的 negotiate 过程以较为简化的形式显示，服务器在收到客户端的 Authorization 包后，可能会返回一个带有 WWW-Authenticate 字段的 **401 代码**（未授权），因为还需要进一步的身份验证数据。随后客户端根据要求发送另一个 Authorization 头部。重复此过程，直到服务器回答 200 OK 为止。

- $^{316}$ http://en.wikipedia.org/wiki/Single_sign_on

- $^{317}$ 所述场景也可能适用于 Windows 2000，但作者未能对其进行测试。尽管如此，Windows 2000 和 Windows 2003 之间的 Kerberos 实现确实存在差异，这可能需要对此处描述的过程进行调整。

- $^{318}$ http://www.innovation.ch/personal/erald/ntlm.html，更多细节请见 http://davenport.sourceforge.net/ntlm

- $^{319}$ http://rfc.sunsite.dk/rfc/rfc4559.html

- $^{320}$ http://rfc.sunsite.dk/rfc/rfc4178

- $^{321}$ 身份验证数据

```
kdc = dc01.example.net:88
kdc = dc02.example.net:88
admin_server = dc01.example.net
}
```

[libdefaults] 节基本上定义了默认值。在这里，重要的是领域域（domain realm）必须大写写。在 [realms] 部分，定义了各自对应服务器的各个域。`kdc` 参数描述了充当密钥服务的 Kerberos 服务器（Active Directory 中的所有域控制器），而 `admin_server` 是 Kerberos 主服务器（通常是 Active Directory 中的第一个域控制器）。必须能够将此处指定的名称解析为 IP 地址，这可以通过对所给定的完全限定域名（FQDN）进行 `ping` 测试来验证。

要查看 Kerberos 是否正常工作，最好使用 `kinit` 程序，如果执行成功，它将从 Kerberos 服务器获取一个有效的票据（ticket）：

```bash
linux:~ # kinit administrator@EXAMPLE.NET
Password for administrator@EXAMPLE.NET: ******
```

`kinit` 需要一个有效的账户，并且用户名后的域名必须大写写。如果密码正确且一切正常，`kinit` 将没有输出。现在可以使用 `klist` 显示票据：

```bash
linux:~ # klist
Ticket cache: FILE=/tmp/krb5c_0
Default principal: administrator@EXAMPLE.NET
```

| 有效开始时间 | 到期时间 | 服务主体 |

| :--- | :--- | :--- |

| 08/26/07 14:31:47 | 08/27/07 00:31:49 | krbtgt.EXAMPLE.NET@EXAMPLE.NET |

| 续期直到 | | |

Kerberos 4 票据缓存：/tmp/tkt0

klist: 你没有缓存票据

## E.2.4 Apache 配置

你必须确保 Apache 在启动时加载了 `mod_auth_kerb` 模块。通过发行版安装时，该模块已经经过预配置。在 Debian "Etch" 中，配套的 `LoadModule` 可以在文件 `/etc/apache2/mods-available/mod_auth_kerb` 中找到。

```apache
LoadModule auth_kerb_module /usr/lib/apache2/modules/mod_auth_kerb.so
```

要激活它，使用 `a2enmod` 命令，它的作用仅仅是在 `/etc/apache2/mods-enabled/` 目录下放置一个软链接，指向配置文件：

```bash
linux:~ # a2enmod auth_kerb
Module auth_kerb installed; run /etc/init.d/apache2 force-reload to enable.
```

为了能够使用 Kerberos 进行认证，你可能需要修改 Apache 配置文件 `/etc/apache2/conf.d/nagios.conf`，该文件在 1.5.3 用户认证 (1.5.2 SELinux) 中描述：
