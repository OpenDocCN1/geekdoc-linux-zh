
此示例仅允许由此站点中的主机发起的 POST 请求访问 `cgi-bin` 目录。如果该站点具有一些通过 HTTP POST 方法发送输入数据的 HTML 表单，只有 `yourdomain.com` 中的用户才能有效使用这些表单。通常，CGI 应用程序存储在 `cgi-bin` 目录中，许多网站的 HTML 表单通过 POST 方法将数据传递给 CGI 应用程序。使用上述基于主机的访问控制配置，站点可以允许任何人运行 CGI 脚本，但仅允许特定站点（在此例中为 `yourdomain.com`）实际向 CGI 脚本提交数据。这使得此类网站的 CGI 访问具有某种只读性质。每个人都可以运行生成输出而无需任何用户输入的应用程序，但只有特定域的用户才能提供输入。

# 使用 HTTP 认证方案

基于 `mod_auth` 模块的标准基础 HTTP 认证通过存储在文本文件中的用户名、组和密码来确认身份。如果你处理的用户数量较少，这种方法效果很好。然而，如果你有大量用户（数千或更多），使用 `mod_auth` 可能会产生性能影响——在这种情况下，可以使用更高级的方法，例如 DBM 文件、Berkeley SQL 数据库。下一节将介绍几个基础 HTTP 认证的示例。

## 要求用户名和密码

此示例创建了一个受限目录，访问时需要用户名和密码。我假设以下是针对名为 `apache.nitec.com` 网站的设置：

```
DocumentRoot "/www/htdocs"

AccessFileName .htaccess

AllowOverride All
```

假设你想限制对以下目录的访问，使得名为 `reader` 且密码为 `bought-it` 的用户才能访问该目录：

```
/www/htdocs/readonly
```

以下步骤创建相应的限制访问：

- 1. 使用 `htpasswd` 创建用户文件。

标准的 Apache 分发版包含一个名为 `htpasswd` 的工具，它可以创建 `AuthFile` 指令所需的用户文件。像如下使用该程序：

```
htpasswd -c /www/secrets/.htpassword reader
```

`htpasswd` 工具会询问 `reader` 的密码。输入 `bought-it` 然后再次输入密码以确认。重新输入密码后，该工具会创建一个文件 `.www/secrets/.htpassword`。注意以下几点：

- `-c` 选项告诉 `htpasswd` 你想要一个新的用户文件。如果你已经有了密码文件并想添加新用户，则不需要此选项。
- 将用户文件放置在 `apache.nitec.com` 网站的文档根目录之外，因为你不希望任何人通过 Web 下载它。
- 在文件名开头使用句号 (.)，使其不会出现在 Unix 系统中。这样做并没有实际益处，但可以帮助识别 Unix 文件，因为这是一种传统的 Unix 习惯。Unix 系统中的许多配置文件以句号开头（`.login` 和 `.profile`）。

- 2. 执行以下命令：

```
cat /www/secrets/.htpasswd
```

这将显示类似的一行（密码与此示例不相同）：
`reader:hul6FFh1`

- 3. 创建 `.htaccess` 文件。
使用文本编辑器在 `/www/ht/.htaccess` 中添加以下行：
`AuthName "Readers Only"`
`AuthType Basic`
`UserFile /www/secrets/.htpasswd`
`require user`

# 第四部分：网络服务安全

你可以使用 `ErrorDocument` 指令来更改认证所需的消息：

```
ErrorDocument 401 /nice401message.html
```

## 允许用户组访问目录

与其允许用户 `reader` 访问受限区域（如上一个示例所示），尝试允许 `smart_readers` 组的任何人访问同一个目录。假设该组有两个用户：`pikejb` 和 `bcarloid`。

按照以下步骤赋予 `smart_readers` 组的用户权限：

- 1. 使用 `htpasswd` 创建用户文件。
  使用 `htpasswd` 工具创建用户 `pikejb` 和 `bcarloid`。
- 2. 创建组文件。
  使用文本编辑器（大多数 Unix 系统上的 vi）创建一个名为 `/secrets/.htgroup` 的文件。该文件有一行：
  `smart_readers: pikejb bcarloid`
- 3. 在 `/www/htdocs/readonly` 中创建 `.htaccess` 文件。
  使用文本编辑器在 `/data/web/apache/public/htdocs/readonly/.htaccess` 文件中添加以下行：
  `AuthName "Readers Only"`
  `AuthType Basic`
  `UserFile /secrets/.htpasswd`
  `AuthGroupFile /secrets/.htgroup`
  `require group smart_readers`
- 4. 确保 `.htaccess`、`.htpasswd` 和 `.htgroup` 文件仅对 Apache 可读，并且除所有者外没有对这些文件具有写入权限。

## 第 15 章：Web 服务器安全

### 将基于主机的访问控制与 HTTP 身份验证结合

在本示例中，你将看到如何将基于主机的访问控制方案与 Apache 中提供的基本 HTTP 身份验证方法相结合。假设你想允许 `smart_readers` 组访问与倒数第二个示例（“允许一组用户访问目录”）中相同的目录，并且你希望任何任何来自 `nitec.com` 域名且没有用户名和密码的用户也能访问该目录。

这意味着，如果一个对 URL `http://apache.nitec.com/readonly` 的请求来自名为 `classroom.nitec.com` 的域名，则该请求将在不经过 HTTP 身份验证的情况下被处理，因为你执行了以下步骤：

- 1. 修改 `.htaccess` 文件（参考上一个示例），如下所示：

```
AuthName "Readers Only"

AuthType Basic

AuthUserFile /www/secrets/.htpasswd

AuthGroupFile /www/secrets/.htgroup

require group smart_readers

order deny, allow

deny from all

allow from classroom.nitec.com
```

这添加了三个基于主机的访问控制指令（在前面的章节中讨论过）。

- `order` 指令告诉 Apache 在评估 `allow` 指令之前评估 `deny` 指令。
- `deny` 指令告诉 Apache 拒绝所有主机的访问。
- `allow` 指令实际上告诉 Apache 允许来自 `classroom.nitec.com` 的访问。

第三条指令实际上告诉 Apache `classroom.nitec.com` 域名中的任何主机都可以访问此目录。

- 2. 使用来自 `user1.classroom.nitec.com` 主机的 Web 浏览器，如果尝试访问 `http://apache.nitec.com/readonly`，你的浏览器将显示用户名和密码认证对话框。这意味着你必须进行身份验证。

这并不是你想要的结果。那么到底发生了什么？Apache 假设该目录同时需要基于主机的验证和基本 HTTP 身份验证——因此，在通过这两种方法之前，它会拒绝访问该目录。解决这个问题的方法是 `satisfy` 指令，你可以这样使用它：

```
AuthName "Readers Only"

AuthType Basic

AuthUserFile /www/secrets/.htpasswd

AuthGroupFile /www/secrets/.htgroup

require group smart_readers

order deny, allow

allow from classroom.nitec.com

satisfy any
```

`satisfy` 指令接受 `all` 或 `any` 值。因为你只想在请求来自 `classroom.nitec.com` 域名以外的任何主机时才激活基本 HTTP 身份验证，请为 `satisfy` 指令指定 `any`。这实际上告诉 Apache 执行如下：

```
IF (REMOTE_HOST NOT IN .classroom.nitec.com DOMAIN) THEN

  Basic HTTP authentication Required

ENDIF
```
