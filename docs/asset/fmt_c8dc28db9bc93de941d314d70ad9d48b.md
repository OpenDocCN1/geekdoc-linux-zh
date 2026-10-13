
# MIME 类型映射

`application/msword` `doc`

`application/pdf` `pdf`

`application/postscript` `ai` `eps` `ps`

`application/x-perl` `tcl`

`audio/mpeg` `mpg` `mp2` `mp3`

`audio/x-pn` `realaudio` `ram` `rm`

`audio/x-wav` `wav`

`image/gif` `gif`

`image/jpeg` `J` `Jpg` `jpe`

`image/png` `png`

`text/html` `html` `htm`

`text/plain` `asc` `txt`

`video/mpeg` `mpeg` `mpeg` `mne`

每一行显示 MIME 类型（例如 `text/html`），随后是该类型的对应扩展名（`html` 或 `htm`）。

## 访问控制指令

访问-控制指令允许你控制谁可以访问系统中的不同目录。这些是全局访问配置指令。在 Apache Web 服务器提供的每个目录中，你都可以有一个由 `AccessFileName` 指令指定名称的访问配置文件。（默认情况下，每个目录的访问配置文件命名为 `.htaccess`。）

去掉了大部分注释行后，访问控制指令的格式如下：

```
# 第一，我们把“默认”配置为
# 一组非常严格的权限。
<Directory />
Options None
AllowOverride None
</Directory>
```

### 第三部分：与 Red Hat Linux 联网

```
# 以下目录名称应
# 与 httpd.conf 中的 DocumentRoot 匹配
<Directory /var/www/html>
Options Indexes Includes FollowSymLinks
AllowOverride None
order allow,deny
allow from all
</Directory>
```

```
# 目录名称应匹配
# cgi-bin 目录的位置
<Directory "/var/www/cgi-bin">
AllowOverride ExecCGI
Options ExecCGI
order allow,deny
allow from all
</Directory>
```

访问控制指令使用的语法与其他 Apache 指令不同。其语法类似于 HTML。各种访问控制指令被封装在成对标签中，例如 `<Directory>` ... `</Directory>`。

以下描述了部分访问控制指令：

- `FancyIndexing` 开启花哨的目录列表，其中包含文件名以及代表文件类型、大小和最后修改日期的图标。
- `IconHeight=N` 指定图标的高度为 N 像素。
- `IconWidth=N` 指定图标的宽度为 N 像素。
- `NameWidth=N` 使文件名的宽度为 N 个字符。
- `IconAreLinks` 使图标像链接一样工作。
- `ScanHTMLTitles` 显示 HTML 文件的描述。
- `SuppressHTMLPre`（原文为`SuppressHTMLPream`）不向头文件（通过 `HeaderName` 指令）中添加标准的 HTML 导言。
- `SuppressLastModified` 停止显示最后的修改日期。
- `SuppressSize` 停止显示文件大小。
- `SuppressDescription` 停止显示任何文件描述。
- `SuppressColumnSorting` 停止列标题作为启用排序的链接。

- `ErrorDocument` 文件名 ...指定当发生特定类型的错误时，服务器应该发送的文件。你也可以为错误提供文本消息。这里是一些示例：
`ErrorDocument 403 "Sorry, you cannot access this directory"`
`ErrorDocument 404 /cgi-bin/bad_link.pl`
`ErrorDocument 401 /new_subscriber.html`

如果你没有此指令，服务器将发送内置的错误消息。`errortype` 可以是 HTTP/1.1 错误之一（更多信息请参阅 RFC 2616：`http://www.ietf.org/rfc/rfc2616.txt` 或 `http://www.cis.ohio-state-edu/dtub/rfc/rfc2616.html`）：

- 400—请求错误（Bad Request）
- 401—未授权（Unauthorized）
- 402—需要付款（Payment Required）
- 403—禁止（Forbidden）
- 404—未找到（Not Found）
- 405—方法不允许（Method Not Allowed）
- 406—不可接受（Not Acceptable）
- 407—需要代理身份认证（Proxy Authentication Required）
- 408—请求超时（Request Timeout）
- 409—冲突（Conflict）
- 410—已删除（Gone）
- 411—需要长度（Length Required）
- 412—前提条件失败（Precondition Failed）

- 413-请求实体过大（Request Entity Too Large）
- 414-请求 URI 过长（Request-URI Too Long）
- 415-不支持的媒体类型（Unsupported Media Type）
- 416-请求范围不可（Requested Range Not Satisfiable）
- 417-期望失败（Expectation Failed）
- 500-内部服务器错误（Internal Server Error）
- 501-未实现（Not Implemented）
- 502-坏网关（Bad Gateway）
- 503-服务不可用（Service Unavailable）
- 504-网关超时（Gateway Timeout）
- 505-不支持 HTTP 版本（HTTP Version Not Supported）

## TypesConfig

`TypesConfig` 文件名—指定包含文件扩展名到 MIME 类型映射的文件。（MIME 代表多用途互联网邮件扩展，它定义了在单条消息文件中封装附件的方法。）服务器会报告 MIME 类型。如果你没有指定 `TypesConfig` 指令，以下是默认 `/etc/mime.types` 文件中的几行选定内容：

| MIME Type | Extensions |
| :--- | :--- |
| `application/msword` | `doc` |
| `application/pdf` | `pdf` |
| `application/postscript` | `ai` `ps` |
| `application/x-perl` | `tcl` |
| `audio/mpeg` | `mpg` `mp2` `mp3` |
| `audio/x-pn` | `realaudio` `ram` `rm` |
| `audio/x-wav` | `wav` |
| `image/gif` | `gif` |
| `image/jpeg` | `J` `Jpg` `jpe` |
| `image/png` | `png` |
| `text/html` | `html` `htm` |
| `text/plain` | `asc` `txt` |
| `video/mpeg` | `mpeg` `mpeg` `mne` |

每一行显示 MIME 类型（例如 `text/html`），随后是该类型的对应扩展名（`html` 或 `htm`）。

访问控制指令允许你控制谁可以访问系统中的不同目录。这些是全局访问配置指令。在 Apache Web 服务器提供的每个目录中，你都可以有一个由 `AccessFileName` 指令指定名称的访问配置文件。（默认情况下，每个目录的访问配置文件命名为 `.htaccess`。）

去掉了大部分注释行后，访问控制指令的格式如下：

```
# 第一，我们把“默认”配置为
# 一组非常严格的权限。
<Directory />
Options None
AllowOverride None
</Directory>
```

```
# 以下目录名称应
# 与 httpd.conf 中的 DocumentRoot 匹配
<Directory /var/www/html>
Options Indexes Includes FollowSymLinks
AllowOverride None
order allow,deny
allow from all
</Directory>
```

```
# 目录名称应匹配
# cgi-bin 目录的位置
<Directory "/var/www/cgi-bin">
AllowOverride ExecCGI
Options ExecCGI
order allow,deny
allow from all
</Directory>
```
