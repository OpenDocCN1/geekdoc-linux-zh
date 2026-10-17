
**CAUTION** 请注意，Apache 中的日志记录存在特定的安全问题。因为任何日志辅助程序都将作为启动 Apache 的用户（通常是 `root`）启动，所以该程序必须安全。有关进一步安全信息的良好资源是官方 Apache 文档中的 Security Tips [`http://httpd.apache.org/docs/misc/security_tips.html`] 部分。

## 错误日志到

这设置了 Apache 为此虚拟服务器发送错误信息的位置。通常这会发送到 `syslog` 守护进程，后者将其写入主 Web 服务器错误日志。然而，Apache 可以将此发送到备用日志程序或文件。此选项配置 `ErrorLog` [`http://www.apache.org/docs/mod/core.html#errorlog`] 指令，通常默认为记录到 `syslog` 守护进程（如果可用）。

## 浏览器日志文件

在此，您可以定义 Apache 是否将访问 Web 服务器的用户代理（浏览器，最常见，不过机器人和自动下载器也会出现）的日志保留下来。此信息通常只有短暂的兴趣，除非您考虑实施与某些浏览器不兼容的技术（如 Flash、Shockwave 以及大量鲜为人知且甚至不太可访问的数据格式）。查看这些日志通常会提醒您此类技术可能会疏远您客户的百分比。默认情况下不会记录代理信息。此选项配置 `AgentLog` [`http://www.apache.org/docs/mod/mod_log_agent.html#agentlog`] 指令。

## 默认日志格式

此选项允许您配置 Apache 以任意选择的格式写入日志。如果您希望 Apache 以通用日志格式记录，您只需将其保留为默认值。然而，要以不同方式记录，您将选择格式选项并在字段中填写命名日志格式的昵称（下面讨论）或日志格式字符串。此选项配置 `CustomLog` 指令。[`http://www.apache.org/docs/mod/mod_log_config.html#customlog`]

## 命名日志格式

命名日志格式是上面讨论的自定义日志格式，已被定义并被赋予昵称以供其他日志指令使用。自定义日志格式是通过输入一系列变量来创建，以指示应存在的数据字段及其出现的顺序。例如，一个模仿通用日志格式的自定义日志类型如下所示：

```
%h %l %u %t \"%r\" %>s %b
```

此选项配置 `LogFormat` [`http://www.apache.org/docs/mod/mod_log_config.html#logformat`] 指令。

## 访问日志文件

在此，您可以定义 Apache 发送日志到的附加位置、格式或程序。配置方式与上面的默认日志类似，只是您可以拥有任意数量的访问日志文件。这允许您例如将图像访问记录到单独的文件，或将访问记录到另一种格式以供处理和分析。此选项与 `TransferLog` [`http://www.apache.org/docs/mod/mod_log_config.html#transferlog`] 指令相关。请注意，影响所有其他日志指令的相同安全影响也影响此选项。

## 不记录引用的来源

此选项将提供的主机名添加到一个列表中，引荐信息将不会从这些主机记录。例如，如果我想让我的位于 `penguinfeet.org` 的 Web 服务器忽略来自我的另一个网页 `swelltech.com` 的引荐，我会在此处输入 `swelltech.com`。然后，我的统计数据就不会因来自我自己页面的大量引荐而失真。此选项与 `RefererIgnore` [`http://www.apache.org/docs/mod/mod_log_referer.html#refererignore`] 指令相关。

## 引荐日志文件

在此定义引荐信息记录到的位置。这可以是文件或程序。此选项配置 `RefererLog` [`http://www.apache.org/docs/mod/mod_log_referer.html#refererlog`] 指令。

## 文档选项

在此，您可以访问许多会影响权限、位置和行为的虚拟服务器特定选项。

此页面的第一个字段没有标签。它是文档根目录。这通常在虚拟服务器创建时设置，并且由 Webmin 自动创建。此选项与 `DocumentRoot` [`http://www.apache.org/docs/mod/core.html#documentroot`] 指令相关。

## 用户 WWW 目录

在此，您配置用户可通过 Apache 发布 HTML 文档的位置。语法有几种形式，可执行不同类型的扩展以创建实际路径。首先，`htmldocs` 形式的相对链接对于用户 `joe` 翻译为 `joe/htmldocs`。绝对链接，例如 `/usr/htmldocs`，将翻译为 `/usr/htmldocs/joe`。最后，可以使用 `*` 表示用户名进行翻译。例如，`/home/*/htmldocs` 将翻译为 `/home/joe/htmldocs`。此选项配置 `UserDir` [`http://www.apache.org/docs/mod/mod_userdir.html#userdir`] 指令。

以下字段是与上述用户 WWW 目录选项连接的延续选项。它们控制将对哪些用户的目录执行翻译。选择所有用户可访问意味着对于 URL 中输入的任何用户名，翻译将发生并且用户的 Web 目录可浏览。所有用户除外允许您禁止某些用户，而其余用户将被翻译。这可用于例如禁用违反服务条款的用户的网站。最后，只有明确命名的用户才会执行目录翻译。

## 每目录选项文件

在此，您可以指定一个文件名以检查目录访问选项。除非在 Apache 配置的其他地方被禁止，否则在此名称的任何目录中找到的文件中的选项将覆盖该目录的默认权限。例如，如果我选择文件名 `.acl`，并在我的一个目录中创建了这样一个文件，其中包含生成目录索引的指令，那么对于该目录将生成此类索引。即使默认是不生成索引也是如此。如果您正在运行虚拟主机服务器，这可以让您的用户在不干扰或更改同一服务器上其他站点行为的情况下，对其个人站点的 Web 服务器行为拥有一定自由度。这可以被视为 Apache 可配置性洋葱的一层或多层。此选项配置 `AccessFileName` 指令，默认为 `.htaccess`。

## 目录选项

在此，您可以选择为此目录使用默认选项。这会影响虚拟服务器的根目录和所有子目录，除非它们包含如上所述的 Per-directory options file 部分中讨论的 `AccessFileName` 文件。此选项与 `Options` [`http://www.apache.org/docs/mod/core.html#options`] 指令相关，默认为 `all`，除 `Generate Multiviews` 外。

可用的目录选项如下：

- `执行 CGI 程序` 允许执行位于此目录中的 CGI 脚本。
- `跟随符号链接` 服务器将跟随此目录中的符号链接。这与 `ExecCGI` 指令相关。
- `服务器端包含和执行` 允许服务器端包含。这与 `FollowSymLinks` 指令相关。
- `服务器端包含` 允许服务器端包含，但禁止 `#exec` 命令以及对 CGI 脚本使用 `#include`。这与 `IncludesNOEXEC` 指令相关。
- `生成目录索引` 当 URL 映射到目录中且没有索引 HTML 文件时（通常是 `index.html`，但此项为可配置选项），Apache 可以为该目录生成格式化的文件列表。此选项与 `Indexes` 指令相关。
- `生成 Multiviews` 允许内容协商的 `multiviews`。这允许以同一 URL 引用多种语言、字符集和呈现形式。然后客户端浏览器会与服务器协商以选择适合用户的版本。更多信息请参阅内容协商 [`http://httpd.apache.org/docs/content-negotiation.html`]。此选项与 `MultiViews` 指令相关。
- `仅在所有者匹配时跟随符号链接` Apache 仅会跟随目标文件或目录的所有权与链接相匹配的符号链接。此选项与 `SymLinksIfOwnerMatch` 指令相关。

请注意，如果多个项目适用（从父目录继承），则特定于所选目录的项目适用，除非选择了与父目录合并。例如，如果 `/home/httpd/penguinfoet` 具有所有权限，但子目录 `/home/httpd/penguinfoet/users` 只有 `ExecCGI`，则该目录仅具有执行 CGI 选项可用。与父目录合并后，子目录将获得与父目录相同的选项，除非明确关闭。

## 生成 MD5 摘要
