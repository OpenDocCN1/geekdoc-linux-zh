
## 在网站中创建仅限成员的区域

使用 mod_auth 指令，您可以在网站上创建需要用户名/密码身份验证的仅限成员区域。例如，假设您想创建一个名为 http://your_server_name/memberonly 的仅限成员区域。方法如下：

- 1. 确定您要限制访问的物理目录。大多数人使用 DocumentRoot 指定的目录内的目录，但只要 Apache 用户（由 User 指令设置）被允许读取目录内容，您可以使用任何目录。在此我假设您的 DocumentRoot 设置为 /www/mysite/htdocs，并且您希望限制对名为 /www/mysite/htdocs/memberonly 的目录的访问。请根据您自己的 DocumentRoot 设置和文件名相应地进行更改。
- 2. 修改 httpd.conf 文件以创建名为 /memberonly/ 的新别名，如下所示：
```
Alias /memberonly/ "/www/mysite/htdocs/memberonly/"
```
- 3. 在 httpd.conf 文件中添加以下指令，将 /memberonly/ 设置为需要用户身份验证的受限区域。
```
<Location /memberonly/>
    AuthName "Member-Only Access"
    AuthType Basic
    AuthUserFile /www/secrets/.members
    Require valid-user
</Location>
```

在上述内容中，AuthName 指令仅创建一个标签，该标签会由 Web 浏览器显示给用户。此标签应具有意义，以便用户知道请求的内容。请确保如上所示使用双引号。AuthType 始终设置为 Basic，因为 HTTP 默认仅支持 Basic 身份验证。AuthUserFile 指向名为 .members 的密码文件。require 指令表示只有有效用户才允许访问。

- 4. 使用 htpasswd 实用程序创建密码文件。假设您已将 Apache 安装在 /usr/local/apache 中，htpasswd 命令仅在首次使用时应按如下方式运行：
```
/usr/local/apache/bin/htpasswd -c path_to_password_file username
```
-c 选项仅在创建文件时需要，并且只需使用一次。例如，要为上述 /memberonly/ 配置创建名为 mrbert 的第一个用户，请运行以下命令：
```
/usr/local/apache/bin/htpasswd -c /www/secrets/.members mrbert
```
- 5. 为确保用户已创建在密码文件中，请使用文本编辑器查看其内容。还请确保只有 Apache 用户（使用 User 指令设置）可以访问此文件。例如，如果您以 httpd 用户运行 Apache，您可以运行
```
chown httpd:httpd /www/secrets/.members && chmod 750 /www/secrets/.members
```
命令以确保只有 httpd 用户（和组）可以读取此文件。
- 6. 使用 /usr/local/apache/bin/apachectl restart 命令重启 Apache 服务器。

现在使用 http://your_server_name/memberonly/ 访问仅限成员的区域，您将被提示输入用户名和密码。您应该在显示的对话框中看到 AuthName（"Member-Only Access"）的值。输入无效的用户名和密码，您应该会看到拒绝消息。最后，输入使用 htpasswd 实用程序创建的有效用户名和密码。您应该可以访问受限区域。

![](img/9eb7e89292d2f85707b4d49102c865b7_349_0.png)

如果您使用默认的通用日志格式记录访问，您将在日志文件中看到已登录的用户名。

## 使用 .htaccess 文件创建仅限成员的区域

在上一节中我讨论了如何使用 httpd.conf 文件中的配置创建仅限成员的区域。这种配置不适合 Internet Service Providers（ISP）或在同一 Web 服务器上运行多个虚拟网站的各个部门的大型公司等组织。在这些情况下，在 httpd.conf 中添加仅限成员的配置可能无法很好地管理，因为您必须在各种用户（在 ISP 设置的情况下）请求此类更改时添加或删除配置。在这种环境中，最佳方法是使用基于 .htaccess 的身份验证。

使用基于 .htaccess 的身份验证时，您可以允许用户或部门在无需您参与的情况下创建任意多个仅限成员的区域——这对繁忙的系统管理员来说是一大福音。如果您希望使用 .htaccess 文件进行仅限成员的身份验证，请按照以下步骤操作：

- 1. 在 httpd.conf 文件中添加以下指令：
```
AccessFileName .htaccess
```
- 2. 将以下默认配置更改：
```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```
为
```
<Directory />
Options FollowSymLinks
AllowOverride AuthConfig
</Directory>
```
这允许在 .htaccess 文件中使用授权指令（AuthDBMGroupFile、AuthDBMUserFile、AuthGroupFile、AuthName、AuthType、AuthUserFile、Require 等）。
- 3. 使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache 服务器。

![](img/9eb7e89292d2f85707b4d49102c865b7_350_0.png)

> 如果您只想为某个虚拟主机启用基于 .htaccess 的身份验证，则将此指令添加到适当的 <VirtualHost> 容器中。

- 4. 现在您可以在任何可通过 Web 访问的目录中创建 .htaccess 文件并控制对其的访问。您需要在 .htaccess 文件中具有以下指令：
```
AuthName "Enter Label Here"
AuthType Basic
AuthUserFile user_password_file
Require valid-user
```
例如，如果您有一个名为 /www/mysite/htdocs/asb 的目录，并且希望将对该目录的访问限制为列在 /www/mysite/secrets/users.pwd 中的用户，则您将使用以下配置：
```
AuthName "ASB Member Only Access"
AuthType Basic
AuthUserFile /www/mysite/secrets/users.pwd
Require valid-user
```
- 5. 确保 .htaccess 文件只能由 Apache 用户（使用 User 指令设置）读取。例如，如果您以 httpd 运行 Apache，则从您保存文件的目录运行 chown httpd:httpd .htaccess && chmod 750 .htaccess 命令。

![](img/9eb7e89292d2f85707b4d49102c865b7_351_0.png)

> 创建或修改 .htaccess 文件不需要重启 Apache 服务器，因此您可以尝试网站的受限区域，查看身份验证过程是否正常工作。

## 对不同 Web 区域进行受限访问的用户分组

如果您需要允许不同用户访问网站的不同部分，您有几种选择。不要使用 require valid-user，这会为所有有效用户打开受限区域，您可以使用特定的用户名。例如，在以下指令中，只有 cgodsave 和 jolson 可以访问 /financial 部分，而 esmith 和 jkirk 可以访问 /sales 部分：

```
<Location /financial>
    AuthName "Members Only"
    AuthType Basic
    AuthUserFile /www/mysite/secrets/.users.pwd
    Require cgodsave jolson
</Location>
```

```
<Location /sales>
    AuthName "Members Only"
    AuthType Basic
    AuthUserFile /www/mysite/secrets/.users.pwd
    Require esmith jkirk
</Location>
```

然而，在配置中命名所有用户是一项繁琐且通常难以管理的任务。另一种方法是创建单独的密码文件，以便上述配置段如下所示：

```
<Location /financial>
    AuthName "Members Only"
    AuthType Basic
    AuthUserFile /www/mysite/secrets/.financial-team.pwd
    Require valid-user
</Location>
```

```
<Location /sales>
    AuthName "Members Only"
    AuthType Basic
    AuthUserFile /www/mysite/secrets/.sales-team.pwd
    Require valid-user
</Location>
```

现在仅将应添加到 /www/mysite/secrets/.financial-team.pwd 的用户（在这种情况下为 cgodsave 和 jolson）添加进去，并对应添加到 /www/mysite/secrets/.sales-team.pwd 的用户（esmith 和 jkirk）执行相同操作。

然而，如果维护多个密码文件对您来说不具吸引力，您可以使用另一种方法。例如，请看以下配置段：
