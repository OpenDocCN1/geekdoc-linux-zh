

如果要使用 libcurl 的默认密码列表并忽略任何显式的 `http.sslCipherList` 选项，请将 *GIT_SSL_CIPHER_LIST* 设置为空字符串。

## http.sslVerify

在通过 HTTPS 获取或推送时，是否验证 SSL 证书。可被 *GIT_SSL_NO_VERIFY* 环境变量覆盖。

## http.sslCert

在通过 HTTPS 获取或推送时，包含 SSL 证书的文件。可被 *GIT_SSL_CERT* 环境变量覆盖。

## http.sslKey

在通过 HTTPS 获取或推送时，包含 SSL 私钥的文件。可被 *GIT_SSL_KEY* 环境变量覆盖。

## http.sslCertPasswordProtected

启用 Git 的 SSL 证书密码提示。否则，如果证书或私钥是加密的，OpenSSL 可能会提示用户多次输入。可被 *GIT_SSL_CERT_PASSWORD_PROTECTED* 环境变量覆盖。

## http.sslCAInfo

在通过 HTTPS 获取或推送时，包含用于验证对端的证书的文件。可被 *GIT_SSL_CAINFO* 环境变量覆盖。

## http.sslCAPath

在通过 HTTPS 获取或推送时，包含用于验证对端的 CA 证书文件的路径。可被 *GIT_SSL_CAPATH* 环境变量覆盖。

## http.sslTry

在通过常规 FTP 协议连接时，尝试使用 AUTH SSL/TLS 和加密数据传输。如果 FTP 服务器出于安全原因需要它，或者你希望在远程 FTP 服务器支持时始终安全连接，可能需要此功能。默认值为 *false*，因为这可能会在配置错误的服务器上触发证书验证错误。

## http.maxRequests

并行启动多少个 HTTP 请求。可被 *GIT_HTTP_MAX_REQUESTS* 环境变量覆盖。默认值为 5。

## http.minSessions

在请求之间保留的 curl 会话数量（跨插槽计数）。在调用 http_cleanup() 之前，它们不会通过 curl_easy_cleanup() 结束。如果未定义 USE_CURL_MULTI，该值将被限制为 1。默认值为 1。

## http.postBuffer

智能 HTTP 传输机制在向远程系统 POST 数据时使用的缓冲区最大字节数。对于大于此缓冲区大小的请求，使用 HTTP/1.1 和 Transfer-Encoding: chunked 以避免在本地创建巨大的打包文件。默认值为 1 MiB，这对大多数请求来说已经足够。

## http.lowSpeedLimit, http.lowSpeedTime

如果 HTTP 传输速度低于 `http.lowSpeedLimit` 且持续时间超过 `http.lowSpeedTime` 秒，传输将被中止。可被 `GIT_HTTP_LOW_SPEED_LIMIT` 和 `GIT_HTTP_LOW_SPEED_TIME` 环境变量覆盖。

## http.noEPSV

一个布尔值，禁用 curl 使用 EPSV ftp 命令。这对于某些不支持 EPSV 模式的“糟糕”ftp 服务器可能有用。可被 `GIT_CURL_FTP_NO_EPSV` 环境变量覆盖。默认值为 false（curl 将使用 EPSV）。

## http.userAgent

呈现给 HTTP 服务器的 HTTP USER_AGENT 字符串。默认值表示客户端 Git 的版本，例如 git/1.7.1。此选项允许你将此值覆盖为更常见的值，例如 Mozilla/4.0。在某些情况下，例如通过限制常见 USER_AGENT 字符串集合（但不包括 git/1.7.1 这样的字符串）的防火墙连接时，这可能是必需的。可被 `GIT_HTTP_USER_AGENT` 环境变量覆盖。

## http.<url>.*

上述任何 http.* 选项都可以选择性地应用于某些 URL。要使配置键匹配 URL，配置键的每个元素将按照以下顺序与 URL 的元素进行比较：

- 1. 协议（例如 https 中的）此字段必须在配置键和 URL 之间完全匹配。
- 2. 主机/域名（例如 example.com 中的）此字段必须在配置键和 URL 之间完全匹配。
- 3. 端口号（例如 8080 中的）此字段必须在配置键和 URL 之间完全匹配。省略的端口号会自动转换为协议对应的默认值后再进行匹配。
- 4. 路径（例如 repo.git 中的）配置键的路径字段必须与 URL 的路径字段完全匹配，或者作为斜杠分隔路径元素的前缀匹配。这意味着路径为 foo/ 的配置键匹配 URL 路径 foo/bar。前缀只能在斜杠 (/) 边界处匹配。更长的匹配优先（因此路径为 foo/bar/ 的配置键比仅路径为 foo/ 的配置键更好地匹配 URL 路径 foo/bar）。
- 5. 用户名（例如 `user` 在 `If the config key has a user name it must match the user name in the URL exactly. If the config key does not have a user name, that config key will match a URL with any user name (including none), but at a lower precedence than a config key with a user name.` 中）如果配置键包含用户名，它必须与 URL 中的用户名完全匹配。如果配置键不包含用户名，该配置键将匹配具有任何用户名（包括无用户名）的 URL，但其优先级低于包含用户名的配置键。

上述列表按优先级降序排列；与配置键路径匹配的 URL 优先于与其用户名匹配的 URL。例如，如果 URL 是 a，则配置键 match of 优先于配置键 match of。

在进行任何匹配尝试之前，所有 URL 都会进行规范化（如果嵌入在 URL 中，密码部分始终被忽略用于匹配目的），以便拼写不同但等效的 URL 能够正确匹配。环境变量设置始终优先于任何匹配。用于匹配的 URL 是直接提供给 Git 命令的 URL。这意味着因重定向而访问的任何 URL 都不参与匹配。

## i18n.commitEncoding

提交消息存储所使用的字符编码；Git 本身并不关心特定编码，但当从电子邮件导入提交或在 `gitk` 图形历史浏览器中（以及可能在未来或其他 porcelain 工具中的其他位置）时，此信息是必要的。参见例如 (1)。默认为 *utf-8*。

## i18n.logOutputEncoding

运行 `git log` 及其相关命令时，提交消息转换所使用的字符编码。

## imap

*imap* 部分中的配置变量在 (1) 中描述。

## index.version

指定新索引文件初始化时应使用的版本。这不会影响现有仓库。

## init.templateDir

指定复制模板的目录。（参见 (1) 中的“TEMPLATE DIRECTORY”部分。）

## instaweb.browser

指定将在 gitweb 中浏览工作仓库的程序。参见 (1)。

## instaweb.httpd

在 (1) 中启动 gitweb 的 HTTP 守护进程命令行。参见 (1)。

## instaweb.local

如果为 true，由 (1) 启动的 Web 服务器将绑定到本地 IP (127.0.0.1)。

## instaweb.modulePath

(1) 使用的默认模块路径，替代 /usr/lib/apache2/modules。仅当 httpd 是 Apache 时使用。

## instaweb.port

绑定 gitweb httpd 的端口号。参见 (1)。

## interactive.singleKey

在交互式命令中，允许用户使用单个键提供单字母输入（即无需按回车）。目前，这在 (1)、(1)、(1) 和 (1) 的 —patch 模式中使用。请注意，如果便携式按键输入不可用，此设置将被静默忽略；需要 Perl 模块 Term::ReadKey。

## log.abbrevCommit

如果为 true，使 (1)、(1) 和 (1) 假设使用了 —abbrev-commit。你可以使用 —no-abbrev-commit 覆盖此选项。

## log.date

设置 `log` 命令的默认日期时间模式。设置 `log.date` 的值类似于使用 `git log` 的 `—date` 选项。可能的值包括 `relative`、`local`、`default`、`iso`、`rfc` 和 `short`；详情参见 (1)。

## log.decorate

打印出由 `log` 命令显示的任何提交的 ref 名称。如果指定了 `short`，ref 名称前缀 `refs/heads/`、`refs/tags/` 和 `refs/remotes/` 将不会被打印。如果指定了 `full`，完整的 ref 名称（包括前缀）将被打印。这与 `log` 命令的 `—decorate` 选项相同。

## log.showRoot

如果为 true，初始提交将作为一个大型创建事件显示。这相当于与空树的差异。通常隐藏根提交的工具，如 (1) 或 (1)，现在将显示它。默认为 True。

## log.mailmap

如果为 true，使 (1)、(1) 和 (1) 假设使用了 `—use-mailmap`。

## mailinfo.scissors

如果为 true，使 (1)（因此也包括 (1)）默认行为就像在命令行中提供了 `—scissors` 选项一样。当激活时，此功能会移除消息体中剪刀线（即主要由 `">8"`、`"8<"` 和 `"-"` 组成的行）之前的所有内容。

## mailmap.file

扩展 mailmap 文件的位置。首先加载位于仓库根目录的默认 mailmap，然后加载此变量指向的 mailmap 文件。mailmap 文件的位置可能在仓库子目录中，或在某处
