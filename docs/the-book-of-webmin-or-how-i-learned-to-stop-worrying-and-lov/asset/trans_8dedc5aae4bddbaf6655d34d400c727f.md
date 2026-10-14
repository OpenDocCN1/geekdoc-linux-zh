

可用的目录选项如下：

- **执行 CGI 程序** 允许执行位于此目录中的 CGI 脚本。
- **跟随符号链接** 服务器将跟随此目录中的符号链接。这与 ExecCGI 指令相关。
- **服务器端包含和执行** 允许服务器端包含。这与 FollowSymLinks 指令相关。
- **服务器端包含** 允许服务器端包含，但禁止 #exec 命令以及对 CGI 脚本使用 #include。这与 IncludesNOEXEC 指令相关。
- **生成目录索引** 当 URL 映射到目录中且没有索引 HTML 文件时（通常是 index.html，但此项为可配置选项），Apache 可以为该目录生成格式化的文件列表。此选项与 Indexes 指令相关。
- **生成 Multiviews** 允许内容协商的 multiviews。这允许以同一 URL 引用多种语言、字符集和呈现形式。然后客户端浏览器会与服务器协商以选择适合用户的版本。更多信息请参阅内容协商 [http://httpd.apache.org/docs/content-negotiation.html]。此选项与 MultiViews 指令相关。
- **仅在所有者匹配时跟随符号链接** Apache 仅会跟随目标文件或目录的所有权与链接相匹配的符号链接。此选项与 SymLinksIfOwnerMatch 指令相关。

请注意，如果多个项目适用（从父目录继承），则特定于所选目录的项目适用，除非选择了与父目录合并。例如，如果 /home/httpd/penguinfoet 具有所有权限，但子目录 /home/httpd/penguinfoet/users 只有 ExecCGI，则该目录仅具有执行 CGI 选项可用。与父目录合并后，子目录将获得与父目录相同的选项，除非明确关闭。

## 生成 MD5 摘要

此选项打开生成 Content-MD5 摘要头的功能。启用后，Apache 将为每个提供的静态页面生成消息摘要或指纹。使用 MD5 摘要时，客户端可以非常确信地保证，如果内容在从源服务器传输过程中被更改，这些更改将反映在消息摘要的更改中。Content-MD5 标准在 RFC 1864 [http://www.ietf.org/rfc/rfc1864.txt?number=1864] 和 RFC 2616 [http://www.ietf.org/rfc/rfc2616.txt?number=2616] 中有描述。此选项配置 ContentDigest [http://httpd.apache.org/docs/mod/core.html#contentdigest] 指令。请注意，此选项可能存在性能影响，因为摘要是为每个请求生成的，并且由模块提供的请求不会创建摘要。

## 从以下生成 ETag 头

ETag 是 HTTP 响应头，用于提供区分具有相同 URL 的两个或多个对象的方式。该头对执行缓存的中间设备以及缓存结果的客户端浏览器很有用。使用 ETag，可以将对象唯一标识给客户端。通常，Apache 根据文件的 i-node 编号、文件的最后修改时间和文件的大小生成 ETag。如果选择选择属性，则可以从中选择任意或全部这些标准。此选项与 FileETag [http://httpd.apache.org/docs/mod/core.html#fileetag] 指令相关。

## 虚拟服务器路径

非常旧的浏览器和代理无法寻址基于名称的虚拟服务器，只能通过其 IP 请求站点。这导致了不幸的效果，即这些浏览器只能访问给定 IP 上的默认网站。解决此问题的变通方法是为默认服务器提供通往每个虚拟服务器的路径。使用此指令，您可以定义此特定虚拟服务器在默认服务器路径中的位置。因此，如果我的虚拟服务器 www.penguinfeet.org 位于 IP 123.45.67.89 的服务器上，并且旧浏览器访问该名称，它将最终浏览到主机上的默认服务器 — 该服务器可以为用户提供指向托管在此服务器上的虚拟服务器的链接列表。如果将其设置为 /penguinfeet，则链接将把用户带到 http://www.penguinfeet.org/penguinfeet/，这就是正确的页面！不算漂亮，但网络并不总是像今天这样经过深思熟虑。谁能责怪网络的原始设计者没有意识到有一天每个人都会拥有自己的域名！好消息是，那些旧的网络客户端在统计上已不再使用（它们根本不会出现在我的 Web 服务器日志中；因人而异）。此选项配置 ServerPath [http://httpd.apache.org/docs/mod/core.html#serverpath] 指令。有关虚拟主机和潜在问题的更多信息，请参阅 Apache 虚拟主机文档 [http://httpd.apache.org/docs/vhosts/]。

## 错误消息页脚

此选项允许您为所有服务器生成的文档（例如错误页面、mod_proxy ftp 目录列表、mod_info 输出等）添加页脚。这通常仅在 Apache 充当代理时才需要，因为它在发现多重代理链中错误消息的来源时最有用。此选项配置 ServerSignature [http://httpd.apache.org/docs/mod/core.html#serversignature] 指令，默认值为 Off。

## 自动纠正拼写错误的 URL？

此选项配置 Apache 是否尝试纠正用户在 URL 中的拼写错误。如果启用，并且 URL 与服务器上的文档不匹配，将会检查所有可能匹配用户请求的对象。如果找到一个与用户请求非常接近的对象 — 例如，大写不正确但对象拼写正确或仅缺少一个字母 — Apache 将静默将用户重定向到更正后的 URL。如果找到多个可能的匹配项，用户将被重定向到包含可能页面的列表的页面，以便他们可以选择正确的页面。如果未找到可能的匹配项，请求将遍历正常的错误路径并导致 404 未找到错误。此选项与 CheckSpelling [http://httpd.apache.org/docs/mod/mod_speling.html#checkspelling] 指令相关，默认值为 Off。

## 错误处理

在服务器错误的情况下，Apache 可以配置为提供自定义错误消息，或重定向到本地或外部 URL，或默认输出简单的硬编码错误消息。在此，您可以配置希望提供自定义消息的任何错误类型。例如，如果您想要一个自定义的 404 消息，将用户引导至本地站点搜索页面（这是一种方便且礼貌的做法），您可以在此页面上完成。要配置 Apache 的自定义错误响应功能，只需输入错误代码，然后输入要显示的 URL 或消息。有关此功能的更多信息，请参阅自定义错误响应文档 [http://httpd.apache.org/docs/custom-error.html]。

## 用户和组

此页面配置 Apache 服务器将运行的用户和组。这设置了 Apache 和子进程在操作时的权限。强烈建议您将其设置为权限尽可能小的用户和组（同时仍允许服务器完成其工作）。在许多 UNIX 操作系统中，这通常配置为 nobody 和 nogroup，在大多数情况下这是一个不错的选择。除非您确切知道自己在做什么以及这样做的<|message|> 安全影响，否则不要将其设置为 root。请注意，如果 Apache 父进程以 root 启动，它将保持为 root，而实际提供请求的[content]

可用的目录选项如下：

- **执行 CGI 程序** 允许执行位于此目录中的 CGI 脚本。
- **跟随符号链接** 服务器将跟随此目录中的符号链接。这与 ExecCGI 指令相关。
- **服务器端包含和执行** 允许服务器端包含。这与 FollowSymLinks 指令相关。
- **服务器端包含** 允许服务器端包含，但禁止 #exec 命令以及对 CGI 脚本使用 #include。这与 IncludesNOEXEC 指令相关。
- **生成目录索引** 当 URL 映射到目录中且没有索引 HTML 文件时（通常是 index.html，但此项为可配置选项），Apache 可以为该目录生成格式化的文件列表。此选项与 Indexes 指令相关。
- **生成 Multiviews** 允许内容协商的 multiviews。这允许以同一 URL 引用多种语言、字符集和呈现形式。然后客户端浏览器会与服务器协商以选择适合用户的版本。更多信息请参阅内容协商 [http://httpd.apache.org/docs/content-negotiation.html]。此选项与 MultiViews 指令相关。
- **仅在所有者匹配时跟随符号链接** Apache 仅会跟随目标文件或目录的所有权与链接相匹配的符号链接。此选项与 SymLinksIfOwnerMatch 指令相关。

请注意，如果多个项目适用（从父目录继承），则特定于所选目录的项目适用，除非选择了与父目录合并。例如，如果 /home/httpd/penguinfoet 具有所有权限，但子目录 /home/httpd/penguinfoet/users 只有 ExecCGI，则该目录仅具有执行 CGI 选项可用。与父目录合并后，子目录将获得与父目录相同的选项，除非明确关闭。

## 生成 MD5 摘要

此选项打开生成 Content-MD5 摘要头的功能。启用后，Apache 将为每个提供的静态页面生成消息摘要或指纹。使用 MD5 摘要时，客户端可以非常确信地保证，如果内容在从源服务器传输过程中被更改，这些更改将反映在消息摘要的更改中。Content-MD5 标准在 RFC 1864 [http://www.ietf.org/rfc/rfc1864.txt?number=1864] 和 RFC 2616 [http://www.ietf.org/rfc/rfc2616.txt?number=2616] 中有描述。此选项配置 ContentDigest [http://httpd.apache.org/docs/mod/core.html#contentdigest] 指令。请注意，此选项可能存在性能影响，因为摘要是为每个请求生成的，并且由模块提供的请求不会创建摘要。

## 从以下生成 ETag 头

ETag 是 HTTP 响应头，用于提供区分具有相同 URL 的两个或多个对象的方式。该头对执行缓存的中间设备以及缓存结果的客户端浏览器很有用。使用 ETag，可以将对象唯一标识给客户端。通常，Apache 根据文件的 i-node 编号、文件的最后修改时间和文件的大小生成 ETag。如果选择选择属性，则可以从中选择任意或全部这些标准。此选项与 FileETag [http://httpd.apache.org/docs/mod/core.html#fileetag] 指令相关。

## 虚拟服务器路径

非常旧的浏览器和代理无法寻址基于名称的虚拟服务器，只能通过其 IP 请求站点。这导致了不幸的效果，即这些浏览器只能访问给定 IP 上的默认网站。解决此问题的变通方法是为默认服务器提供通往每个虚拟服务器的路径。使用此指令，您可以定义此特定虚拟服务器在默认服务器路径中的位置。因此，如果我的虚拟服务器 www.penguinfeet.org 位于 IP 123.45.67.89 的服务器上，并且旧浏览器访问该名称，它将最终浏览到主机上的默认服务器 — 该服务器可以为用户提供指向托管在此服务器上的虚拟服务器的链接列表。如果将其设置为 /penguinfeet，则链接将把用户带到 http://www.penguinfeet.org/penguinfeet/，这就是正确的页面！不算漂亮，但网络并不总是像今天这样经过深思熟虑。谁能责怪网络的原始设计者没有意识到有一天每个人都会拥有自己的域名！好消息是，那些旧的网络客户端在统计上已不再使用（它们根本不会出现在我的 Web 服务器日志中；因人而异）。此选项配置 ServerPath [http://httpd.apache.org/docs/mod/core.html#serverpath] 指令。有关虚拟主机和潜在问题的更多信息，请参阅 Apache 虚拟主机文档 [http://httpd.apache.org/docs/vhosts/]。

## 错误消息页脚

此选项允许您为所有服务器生成的文档（例如错误页面、mod_proxy ftp 目录列表、mod_info 输出等）添加页脚。这通常仅在 Apache 充当代理时才需要，因为它在发现多重代理链中错误消息的来源时最有用。此选项配置 ServerSignature [http://httpd.apache.org/docs/mod/core.html#serversignature] 指令，默认值为 Off。

## 自动纠正拼写错误的 URL？

此选项配置 Apache 是否尝试纠正用户在 URL 中的拼写错误。如果启用，并且 URL 与服务器上的文档不匹配，将会检查所有可能匹配用户请求的对象。如果找到一个与用户请求非常接近的对象 — 例如，大写不正确但对象拼写正确或仅缺少一个字母 — Apache 将静默将用户重定向到更正后的 URL。如果找到多个可能的匹配项，用户将被重定向到包含可能页面的列表的页面，以便他们可以选择正确的页面。如果未找到可能的匹配项，请求将遍历正常的错误路径并导致 404 未找到错误。此选项与 CheckSpelling [http://httpd.apache.org/docs/mod/mod_speling.html#checkspelling] 指令相关，默认值为 Off。

## 错误处理

在服务器错误的情况下，Apache 可以配置为提供自定义错误消息，或重定向到本地或外部 URL，或默认输出简单的硬编码错误消息。在此，您可以配置希望提供自定义消息的任何错误类型。例如，如果您想要一个自定义的 404 消息，将用户引导至本地站点搜索页面（这是一种方便且礼貌的做法），您可以在此页面上完成。要配置 Apache 的自定义错误响应功能，只需输入错误代码，然后输入要显示的 URL 或消息。有关此功能的更多信息，请参阅自定义错误响应文档 [http://httpd.apache.org/docs/custom-error.html]。

## 用户和组

此页面配置 Apache 服务器将运行的用户和组。这设置了 Apache 和子进程在操作时的权限。强烈建议您将其设置为权限尽可能小的用户和组（同时仍允许服务器完成其工作）。在许多 UNIX 操作系统中，这通常配置为 nobody 和 nogroup，在大多数情况下这是一个不错的选择。除非您确切知道自己在做什么以及这样做的安全影响，否则不要将其设置为 root。请注意，如果 Apache 父进程以 root 启动，它将保持为 root，而实际提供请求的子进程将以此处设置的用户和组运行。如果父进程由非 root 用户启动，Apache 将无法 su 到另一个用户，因此将以启动进程的用户运行。此选项配置 User [http://httpd.apache.org/docs/mod/core.html#user] 和 Group [http://httpd.apache.org/docs/mod/core.html#group] 指令。

## 别名和重定向

Apache 提供多种别名和重定向形式。这允许您在 URL 中为用户提供更统一或更简单的路径，以及从服务器根目录之外提供对象。它还允许您在过渡期间将用户重定向到新网站，或在目录结构更改时将浏览器定向到正确的链接。

### 文档目录别名

这允许对象存储在根目录以外的目录中。请注意，以 / 结尾的别名要求请求的 URL 中包含斜杠才能被翻译。此选项与 Alias [http://httpd.apache.org/docs/mod/mod_alias.html#alias] 指令相关。

