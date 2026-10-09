

6. Squid 需要知道您希望允许 `local_net` ACL 中的机器访问代理缓存，这通过在 `squid.conf` 中紧接在 `http_access deny all` 行之前的位置添加以下一行来完成：
   ```
   http_access allow local_net
   ```
7. 您需要告诉 Squid 缓存管理用户的用户名。如果您希望使用 `webmaster@yourdomain.com` 作为缓存管理用户，请在 `squid.conf` 中定义以下一行：
   ```
   cache_mgr webmaster
   ```
8. 要告知 Squid 应该以哪个用户和组运行，请在 `squid.conf` 中添加以下行：
   ```
   cache_effective_user nobody
   cache_effective_group nogroup
   ```
   这里，Squid 被指示以 `nobody` 用户身份运行，并使用名为 `nogroup` 的组的权限。
9. 保存 `squid.conf` 文件并运行以下命令以创建缓存目录：
   ```
   /usr/local/squid/squid -z
   ```

## 先生们，启动你们的 Squid

在配置好 Squid 后，您可以运行 `/usr/local/squid/bin/squid` 命令来首次启动 Squid。您可以通过多种方式验证其是否正在工作：

-   Squid 会出现在 `ps -x` 列表中。
-   运行 `client www.nitec.com` 会将网页文本转储到您的终端。
-   `/usr/local/squid/logs` 目录中的 `cache.log` 和 `store.log` 文件显示 Squid 正在运行。
-   运行 `squid -k check && echo "Squid is running"` 会告诉您 Squid 处于活动状态。

现在来进行真正的测试：如果您将客户端机器上的 Web 浏览器配置为使用 Squid 代理，您应该能看到结果。在 Netscape Navigator 中，选择“编辑偏好设置”，然后在“高级”类别中选择“代理”。通过选择“手动代理配置”并点击“查看”，您可以指定 Squid 服务器的 IP 地址作为 http、FTP 和 Gopher 代理服务器。默认代理端口是 3128，因此除非您在 `squid.conf` 文件中更改了它，否则将该数字填入端口字段。

> 注意
> 如果您使用 Microsoft Internet Explorer，可以通过选择“工具 -> Internet 选项 -> 连接 -> 局域网设置”将 Squid 服务器设置为您的 http、FTP 和 Gopher 代理。然后勾选“使用代理服务器”选项，这将启用“高级”按钮。点击“高级”按钮，并在 HTTP、FTP 和 Gopher 相应的输入框中输入 Squid 服务器地址和端口号。多次点击“确定”以关闭所有对话框。

此时，您应该能够像没有代理一样浏览任何网站。您可以通过检查代理服务器上的日志文件 `/usr/local/squid/logs/access.log` 并确认您正在查看的网站出现在其中，来再次确认 Squid 是否正常工作。

## 调整 Squid 以符合您的需求

现在 Squid 已经启动并运行，您可以自定义它以满足您的需求。最终，像 Squid 这样的工具对于您的用户来说应该是完全透明的。这种“不可见性”将用户从管理的复杂性中解放出来，使他们能够像没有 Web 代理服务器一样浏览网络。虽然我在这里没有详细说明如何实现这一点，但您可以参阅 `http://squid.nlanr.net/Squid/FAQ/FAQ.html` 上的 Squid 常见问题解答。该网站的第 17 节详细说明了如何使用 Squid 作为透明代理。

> 本节向您展示了使用 Squid 作为 Web 代理的基础知识。Squid 具有许多超出此处讨论范围的功能。如果您对使 Squid 具备基础功能之外的功能感兴趣，请访问 `http://squid.nlanr.net` 上的 Squid 网页。

## 为 Squid 设置规则

默认情况下，Squid 不限制您的用户访问任何站点。您可以在 `squid.conf` 文件中定义规则，以设置访问控制列表（ACL），并根据这些列表允许或拒绝访客；例如：

```
acl BadWords url_regex foo bar
```

通过添加上面这一行，您定义了一个名为 `BadWords` 的 ACL 规则，它匹配包含单词 `foo` 或 `bar` 的任何 URL。

> 这适用于 `http://foo.deepwell.com/pictures` 和 `http://www.thekenneddycompound.com/ourbar.jpg`，因为它们都包含属于 `BadWords` 成员的单词。

通过添加以下内容：

```
http_access deny BadWords
```

到 `squid.conf` 中，您阻止用户访问匹配此规则的任何 URL。

> 几乎每个使用基于单词的 ACL 的管理员都有一个故事，讲述他们是如何没有考虑到单词可以使用的多种方式。您应该意识到，如果您禁止用户访问包含单词“sex”的网站，您同时也禁止他们访问 `www.buildersexchange.com` 以及可能落入该类别的其他网站。

## 更改 Squid 的缓存内存设置

您可以控制 Squid 在缓存内存中保留的网页数量。

## 使用重定向器而不是规则

如果您发现自己正在 squid.conf 文件中管理一个大型的“黑名单”站点列表，您应该考虑使用一种称为重定向器的程序。大量的 ACL 规则列表可能会开始减慢高负载 Squid 代理的速度。通过使用重定向器完成同样的工作，您可以提高 Squid 根据过滤规则允许或拒绝 URL 的效率。您可以从 www.senet.com.au/squirm 获取有关 Squirm（一个功能齐全且可与 Squid 配合使用的重定向器）的更多信息。

cachemgr.cgi 文件包含在 Squid 发行版中。它是一个 CGI 程序，允许您查看代理的统计信息，并关闭和重启 Squid。安装只需要花您几分钟时间，但它提供了关于代理性能的具体细节。如果您想要调整您的 Web 缓存，这个工具会很有帮助。

例如，通过添加这一行

```
cache_mem 16 MB
```

您允许 Squid 使用 16MB 的内存来在内存中保存网页。通过反复试验，您可能会发现您需要不同的数量。

> **注意** cache_mem 不是 Squid 消耗的内存量；它只是设置 Squid 用于保存网页、图片等内容的最大内存量。Squid 文档指出，您可以预期 Squid 消耗的量可达此值的三倍。

## 以 Apache 日志格式写入 Squid 日志

Apache 以通用日志格式（CLF）写入日志。如果您有 Apache 日志分析工具，能够使用相同的工具解析 Squid 日志岂不是很棒？您可以让 Squid 以 CLF 格式写入日志来实现这一点。

通过使用这一行

```
emulate_httpd_log on
```

/var/log/squid 中的文件将以类似于 Web 服务器日志文件的格式写入。这种安排使您可以使用 Analog 或 Webtrends 等 Web 统计程序来分析您的日志，并检查用户正在查看的网站。

## 避免负面缓存

如果您输入一个 URL 并发现页面不存在，该页面临时在不久的将来可能都不会存在。通过设置 negative_ttl 为所需的分钟数，如下一个示例所示，您可以控制 Squid 记住之前尝试中未找到页面的时长。这被称为负面缓存。

```
negative_ttl 2 minutes
```

负面缓存并不总是好事。默认值是五分钟，但我建议将其缩短为两分钟，甚至一分钟，或者干脆禁用它。为什么要这样做？您希望您的代理尽可能透明。如果用户正在寻找一个已知存在的页面，您不希望 URL 出现与您用户能够访问它之间存在短暂的滞后时间。

## 使用 mod_backhand 构建 Web 服务器集群

如果您有一个 Web 服务器集群（即 Web 服务器农场），并希望使用原生 Apache 模块在服务器之间重定向请求，请考虑使用 `mod_backhand`。例如，如果您有一个由三个类似配置的 Apache 服务器组成的 Web 服务器集群，并希望将高负载的 CGI 或 `mod_perl` 请求分发到请求时不忙的服务器，您可以充分利用此模块。该模块使用集群中所有服务器的资源状态信息，并将请求重定向到比其他人更准备处理特定请求的服务器。

以下是如何使用 Apache 下载、编译、安装和配置此模块的方法。

1.  从 `http://www.backhand.org/mod_backhand` 下载模块源代码。
2.  以 root 身份提取源发行版到一个目录中，在新创建的 `mod_backhand` 子目录中运行 `./precompile path_to_apache_source` 命令。请记住将 `path_to_apache_source` 更改为实际的 Apache 源发行版路径。
3.  使用 `--enable-backhand` 或 `--enable-modules=backhand` 选项以及所有您通常使用的选项，从 Apache 源发行版目录中的 `configure` 脚本配置 Apache 源。
4.  像往常一样运行 `make && make install`。
5.  将以下配置段添加到您的 `httpd.conf` 中：
   ```apache
   <IfModule mod_backhand.c>
     UnixSocketDir /var/backhand/backhand
     MulticastStats 192.168.1.254:4445
     AcceptStats 192.168.1.0/24
   </IfModule>
   ```
   上述示例配置假设您的 IP 广播地址是 `192.168.1.254`，并且您有一个 C 类网络 `192.168.1.0/24`，它承载了您所有的 Web 服务器。请确保根据您的网络更改这些 IP 地址。`UnixSocketDir` 必须仅对 Apache 用户可访问。

> `mod_backhand` 模块使用以太网广播地址或 IP 多播地址来通告每个服务器的资源状态。上述例子使用的是以太网广播地址；您也可以使用多播地址。

