
## 基于用户的安全

您可以将 Apache 服务器上配置的网站的访问限制为具有密码的授权用户。如后所述，这些密码可以与常规身份验证数据库不同。

例如，要为练习 14-3 中描述的网站配置基于用户的安全，您需要在 `/var/www/html/help` 目录上设置一个 `<Directory>` 容器。您希望在 `<Directory>` 容器中包含多个命令：

- 要设置基本身份验证，您需要一个 `AuthType Basic` 指令。
- 要向请求用户描述站点，您可以包含 `AuthName "some comment"` 指令。
- 要引用名为 `/etc/httpd/testpass` 的 Web 服务器密码数据库，您需要 `AuthUserFile /etc/httpd/testpass` 指令。
- 要将站点限制为名为 `engineer1` 的单个用户，您可以添加 `Require user engineer1` 指令。
- 或者，要将站点限制为 `/etc/httpd/webgroups` 中定义的组，您将添加 `AuthGroupFile /etc/httpd/webgroups` 指令。您还需要一个类似 `Require group Design` 的指令，其中 `Design` 是 `webgroups` 中指定的组名。

这是我在 `<Virtual Host>` 容器后添加的代码示例：

```
<Directory "/var/www/html/help">

AuthType Basic

AuthName "Password Protected Test"

AuthUserFile /etc/httpd/testpass

Require user engineer1

</Directory>
```

配置正确后，下次您尝试在 Firefox 浏览器中访问 `http://server1.example.com/help` 网站目录时，会提示您输入用户名和密码，如图 14-7 所示。

## 图 14-7 网站的密码保护

![](img/9139201cfcaf4292284a0eed074928e5_785_0.png)

## 认证目标 14.03

### 专用 Apache 目录

在本节中，您将探索专用 Apache 目录的几个选项。对于这些目录中的某些目录，使用 `.htaccess` 文件设置专用安全可能是合适的。如前所述，您可以根据用户和组设置密码保护，这对应于 RHCE 目标中引用的“私有目录”。一个适合私有目录的示例是 `httpd.conf` 文件中包含的主目录示例。借助正确的选项，此类目录也可以由组成员管理。

对 Apache 配置文件进行任何更改后，您可能希望测试结果。为此，您可以运行 `apachectl restart` 命令。或者，

要在不中断任何当前连接用户的情况下让 Apache 重新加载配置文件，请运行 `apachectl graceful` 命令。功能上等效的替代命令是 `/etc/init.d/httpd reload`。

## 通过 .htaccess 文件进行控制

鉴于 `httpd.conf` 文件所涉及的复杂性，你可能会看向 `.htaccess` 文件并想“太好了，又多了一个复杂点”。但如果使用正确，`.htaccess` 文件可以简化应用于某个目录或虚拟主机的指令列表，因为它可用于覆盖继承的权限。为此，你需要在目标 `<Directory>` 容器中包含以下命令：

```
AllowOverride Options
```

然后你可以配置 `.htaccess` 文件以覆盖之前设置的权限。`.htaccess` 文件可以存储在任何 Web 目录中，并标记为 `httpd_config_t` SELinux 上下文。

## 密码保护访问

要为网站配置密码，你需要创建一个单独的用户名和密码数据库。就像 `useradd` 和 `passwd` 命令用于普通用户一样，`htpasswd` 命令用于为 Apache 设置用户名和密码。

例如，要在 `/etc/httpd` 目录中创建一个名为 `webpass` 的数据库文件，请从以下命令开始：

```
# htpasswd -c /etc/httpd/webpass engineer1
```

`-c` 开关创建指定的文件，第一个用户是 `engineer1`。系统会提示你为 `engineer1` 输入密码。`webpass` 数据库中的用户不需要拥有常规的 Linux 账户。请注意 `ServerRoot` 目录 (`/etc/httpd`) 的使用。在配置虚拟主机时也很有帮助。

如果你想向此身份验证数据库添加更多用户，请省略 `-c` 开关。例如，以下命令为用户 `drafter1` 设置第二个账户：

```
# htpasswd /etc/httpd/webpass drafter1
```

要为多个用户设置访问权限，你还需要一个组文件。例如，要将 `engineer1` 和 `drafter1` 用户设置为名为 `design` 的组，你可以在 `/etc/httpd/grouppass` 文件中添加以下行：

```
design: engineer1 drafter1
```

在这种情况下，`AuthUserFile` 指令将与 `/etc/httpd/webpass` 身份验证数据库关联，而 `AuthGroupFile` 指令将与组数据库关联。

## 主目录访问

默认的 `httpd.conf` 文件包含注释建议，可启用对用户主目录的访问。通过 Apache 的一个有用选项是对用户主目录的访问。你可以通过将以下指令从

```
UserDir disabled

#UserDir public_html
```

改为

```
#UserDir disabled

UserDir public_html
```

来开始设置对用户主目录的访问。

然后任何人都可以访问用户将其放置在 `~/public_html` 目录中的网页。例如，名为 `michael` 的用户可以创建 `/home/michael/public_html` 目录并添加他选择的网页。

然而，这需要一定的安全妥协；你需要使 `michael` 的主目录对所有用户可执行。这也称为 701 权限，可以通过以下命令配置：

```
# chmod 701 /home/michael
```

你还需要在以同样方式使用以下命令使 `public_html` 子目录对所有用户可执行：

```
# chmod 701 /home/michael/public_html
```

但这会带来一些安全风险。即使黑客可能无法直接读取所提及目录的内容，如果他通过 resulting 网站看到一个脚本，他将能够以任何已登录用户的身份执行该脚本。

如果挂载 `/home` 目录的文件系统使用了第 4 章中讨论的访问控制列表，则有一种替代方法。你可以为名为 `apache` 的用户在所提及的目录上创建 ACL。对于用户 `michael` 及其主目录，使用以下命令即可：

```
# setfacl -m u:apache:x /home/michael

# setfacl -m u:apache:x /home/michael/public_html
```

无论权限是直接设置还是通过 ACL 设置，作为 Web 服务器的逻辑下一步，是在此目录中添加一个 `index.html` 文件。对于我们的目的，它可以是一个文本文件。以下注释的段落是帮助使共享的主目录更安全的一种极佳方法。

此外，SELinux 必须配置为“允许 HTTPd 读取主目录”，与 `httpd_enable_homedirs` 布尔值相关联。你可以通过 SELinux 管理工具或使用 `setsebool -P httpd_enable_homedirs 1` 命令激活该选项。

在那时，指向用户 `michael` 目录的 Web 服务器可以读取 `public_html` 子目录中的 `index.html` 文件。图 14-8 说明了结果，其中所注明的文本是 `index.html` 的唯一内容。

当然，`httpd.conf` 文件中建议了额外的更改。如果你激活以 `<Directory /home/*/public_html>` 容器开头的段落，它支持对所有用户主目录的 `public_html` 子目录的额外访问级别。

```
#<Directory /home/*/public_html>
```

## FIGURE 14-8

查看用户 michael 的 index.html 文件

![](img/9139201cfcaf4292284a0eed074928e5_788_0.png)

`AllowOverride` 指令支持按文档类型（FileInfo）进行的信息访问、与授权指令相关联的访问（AuthConfig），以及由 Allow、Deny 和 Order 等指令保护的访问。

```
#   AllowOverride FileInfo AuthConfig Limit
```
