
![](img/d84604054810a13cacfdac212ebee2f7_256_1.png)

图 12-12：身份验证程序

Squid 2.5 及以上支持三种不同类型的客户端身份验证：Basic、Digest 和 NTLM。旧版 Squid 仅支持 Basic 身份验证，这是一种最初记录的简单、未加密的身份验证方法。两种新方法 Digest 和 NTLM 支持明文和加密身份验证机制。使用哪种方法取决于你的客户端群体。Basic 身份验证适用于完全支持代理的所有浏览器客户端。Digest 身份验证是安全身份验证 Web 客户端的标准方法，受所有完全符合 HTTP/1.1 的浏览器支持（包括现代版本的 IE、Netscape 和 Mozilla）。NTLM 是微软开发的专有机制，目前仅受微软客户端软件支持。

## Basic 和 Digest 身份验证选项

Basic 身份验证最简单易用，因为它最易访问且实现最简单。Digest 身份验证是 RFC 2617 中记录的安全身份验证方法，提供代理和 Web 服务器用户的加密身份验证。唯一真正需要的配置细节是身份验证程序的位置以及要传递给程序的任何命令行参数，尽管还有几个额外的参数可用。

## Basic 身份验证程序、Digest 身份验证程序

如果你希望使用 Squid 进行 Basic 或 Digest 身份验证，这是唯一必需的选项。你可以指定 Squid 提供的几个身份验证程序之一，例如 `ncsa_auth` 用于针对独立的 htpasswd 风格密码文件进行身份验证，`pam_auth` 用于针对本地 PAM 系统进行身份验证，或 `smb_auth` 用于针对远程或本地 SMB 服务器进行身份验证。另一个更简单的选择是使用内置的 Webmin 身份验证模块。它是一种简单的 NCSA 风格身份验证器，可在无需任何额外配置的情况下集成到 Webmin Squid 用户和密码管理工具中。此选项与 `auth_param basic program` 指令或 `auth_param digest program` 相对应，默认情况下为禁用。

## 身份验证程序数量

此选项与 `auth_param basic children` 或 `auth_param digest children` 指令相对应，默认值为 5。如果你的 Squid 支持非常多的用户，你可能需要将其提高到 10 或 20。

## 身份验证缓存时间

这是 Squid 将缓存身份验证凭据的时间长度。Squid 通常会定期查询身份验证程序并将其测试结果存储在其自己的内存中，以便不必频繁查询外部身份验证器。这提高了性能，但如果需要快速更改凭据，你可能希望降低此值。此选项与 `auth_param basic credentials_ttl` 相对应。

## 身份验证域

当客户端浏览器收到基本身份验证请求时，它会包含一个标识请求者数据的短字符串。此信息通常会显示给用户在输入凭据的弹出框中。此选项与 `auth_param basic realm` 或 `auth_param digest realm` 指令相对应，没有默认值。

## NTLM 身份验证选项

与 Digest 身份验证类似，NTLM 身份验证为网络服务器提供加密连接。但请注意，它并不是一种 HTTP 身份验证方案。它是一种连接身份验证方案，无法被代理（尽管代理可以使用它来验证自己的客户端）。NTLM 的安全性也低于 Digest 身份验证，并且有漏洞的历史。话虽如此，它非常流行，因为 Windows 支持一种网络“单点登录”，用户只需在本地网络上登录一次，就可以使用相同的凭据自动通过代理服务器进行身份验证。

## NTLM 身份验证程序

与上面 Basic 和 Digest 身份验证一样，这里将包含指向身份验证程序的路径以及任何命令行参数。通常参数会指定域或工作组以及要进行身份验证的服务器。此选项对应于 `auth_param ntlm program` 指令，默认情况下处于禁用状态。

## NTLM 挑战可以重用的次数

此选项配置特定 NTLM 挑战可以重用的次数。增加此数字可能会略微降低延迟并减轻服务器负载，但也可能增加重放攻击的风险（其中挑战响应被记录并回放以模仿合法用户的连接）。此选项对应于 `auth_param ntlm max_challenge_reuses` 指令，默认值为 0。

## NTLM 挑战的生命周期

此选项对应于 `auth_param ntlm max_challenge_lifetime` 指令，默认值为 2 分钟。它用于指定挑战可以被重用的时间长度。如果挑战比此值更新并且挑战的重用次数少于前一个值，则会重用挑战。

## 访问控制

Squid 的访问控制功能可能是其最复杂的一组功能，但也是最强大的功能之一。事实上，许多人主要就是为了这些功能而使用 Squid。由于其复杂性，您将逐步学习它，

## NTLM authentication options

Like Digest authentication, NTLM authentication provides an encrypted connection to a network server. Beware that it is not an HTTP authentication scheme, however. It is a connection authentication scheme that cannot be proxied (though a proxy can use it to authenticate its own clients). NTLM is also less secure than Digest authentication and has a history of vulnerabilities. That said, it is quite popular, because Windows supports a sort of network "single sign-on", in which users only need to log on once to the local network, and they can be automatically authenticated to the proxy server using the same credentials.

## NTLM authentication program

As in Basic and Digest authentication above, this will contain a path to the authentication program and any command-line arguments. Often the arguments will specify the domain or workgroup and the server to authenticate against. This option correlates to the `auth_param ntlm program` directive and is disabled by default.

## Number of times an NTLM challenge can be re-used

This option configures the number of times that a particular NTLM challenge can be reused. Increasing this number may reduce latency and load on the server slightly, but can also increase the risk of replay attacks (where a challenge response is recorded and played back to imitate the connection of a legitimate user). This option correlates to the `auth_param ntlm max_challenge_reuses` directive and defaults to 0.

## Lifetime of NTLM challenges

This option corresponds to the `auth_param ntlm max_challenge_lifetime` directive and defaults to 2 minutes. It is used to specify the length of time that a challenge can be reused. If a challenge is newer than this value and the challenge has been reused fewer than the previous value, a challenge will be reused.

## Access Control
