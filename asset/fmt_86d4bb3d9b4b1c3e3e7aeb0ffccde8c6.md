
如果你为你的 Web 服务器有一个管理网站，你可能希望使用 `ServerName` 指令来设置它。如果你在 DNS 服务器中没有完全限定域名，或者你的 DNS 服务器不完全可靠，请使用 IP 地址。

```
#ServerName new.host:80
```

## 规范名称

技术上，每个 URL（如 `http://example.com/`）都应该有一个斜杠。`httpd.conf` 文件包含了 `CanonicalName`。

```
UseCanonicalName Off
```

## 文档根目录

Web 服务器的根目录由 `DocumentRoot` 指令指定。这是你编写网页的地方。

```
DocumentRoot "/var/www/html"
```

## 目录权限

接下来，我们查看通过服务器访问的目录权限。它们由 `<Directory />` 容器定义，与 `DocumentRoot` 相关。

```
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>
```

`Options` 指令决定了你可以从该目录执行的操作。它可以设置为多个不同的值，如表 25.5 所示。`AllowOverride` 指令可以指向 `.htaccess` 文件；`AllowOverride None` 设置甚至不会查看 `.htaccess` 文件。

## 特定目录权限

接下来，我们查看 `httpd.conf` 中 `/var/www/html` 目录的默认权限，由以下容器指定：

```
<Directory /var/www/html>
```

`Options` 指令支持通过符号链接进行递归，并在没有 `index.html` 类型文件时列出目录中的文件（参见图 25.2 示例）：

```
Options Indexes FollowSymLinks
```

### 表 25.5：OPTIONS 指令值

| 值 | 描述 |
|---|---|
| All | 支持除 MultiViews 外的所有项 |
| ExecCGI | 允许运行 CGI 脚本。 |
| FollowSymLinks | 允许符号链接的文件或目录。 |
| Includes | 允许使用服务器端包含 (SSI)。 |
| IncludesNOEXEC | 允许 SSI 但不允许 CGI。 |
| Indexes | 如果没有 index.html 类型文件，设置 Apache 返回该目录的文件列表。该文件的选项由 `DirectoryIndex` 指令指定。 |
| MultiViews | 支持内容协商，例如不同语言的网页之间的协商。 |
| SymLinksIfOwner | 如果目标文件或目录由同一用户所有，则跟随符号链接。 |

正如上一节所示，`AllowOverride` 指明了 `.htaccess` 文件中的指令类型。对于其他 `AllowOverride` 选项，请参见表 25.6。以下选项不会查看 `.htaccess` 文件：

```
AllowOverride None
```

## .htaccess 文件

`.htaccess` 文件是一种分布式配置文件，你可以用它来对网站上的单个目录进行配置。它是实现特定目录访问限制的常用方法。

在大多数情况下，`.htaccess` 文件并不是必须的；你可以在主 Apache 配置文件 `httpd.conf` 中按目录配置访问权限。在主 Apache 文件的默认版本中，查找 `<Directory>` 容器。观察不同目录的限制设置。

然而，如果你的服务器上有大量的网站（例如与许多 ISP 关联的个人主页），你可能希望使用 `.htaccess` 文件让用户自行管理其主目录下 Web 页的访问权限。你可以使用标准方案来读取 `.htaccess` 文件，这在后文的“用户目录权限”部分会有描述。

如果你想实现分布式配置文件，可以采取一些措施来增强其安全性。在 `httpd.conf` 中查找 `AccessFileName` 指令。分配一个除 `.htaccess` 以外的文件名。另见本章的“访问控制”部分。

最后，还有访问控制指令；以下内容按顺序查找 `Allow` 后的 `Deny` 指令：

- Order allow,deny
- Allow from all

## 用户目录权限

你可以在用户的家目录下设置 Web 页。默认情况下，它们通过以下命令被禁用的：

```
UserDir disable
```

你可以将该命令替换为：

```
UserDir public_html
```

假设你有一个名为 `ez` 的用户，她在 `/home/ez/public_html` 目录下有一组 Web 页。同时假设你的网站是 `www.example.abc`。你需要设置相应的权限。

```
# chmod 711 /home/ez
# chmod 755 /home/ez/public_html
# chmod 744 /home/ez/public_html/*
```

当你将浏览器指向 `www.example.abc/~ez` 时，你将看到存储在 `/home/ez/public_html` 目录中的任何 `index.html` 页面。
你可以进一步限制用户家目录下 Web 页和文件的访问。查看以下来自 `httpd.conf` 的示例：
