
Apache 软件包提供的 `apxs` 应用可用于构建 Apache 扩展模块。通过 `apxs` 应用，你可以用 C 语言编译 Apache 模块源码，并创建可以由 `LoadModule` 指令加载的动态共享对象。`apxs` 应用要求 `mod_so` 是你 Apache 程序的一部分。它包含了广泛的选项，例如用 `-n` 指定模块名称，`-a` 在 `httpd.conf` 文件中添加该条目，以及 `-i` 在你的 Web 服务器上安装该模块。

你可以在 Apache 网站以及位于站点根目录的目录中找到 Apache Web 配置指令的完整列表。在许多系统中，它位于发行版设置的 Web 站点默认目录下的 `manual` 子目录中（在 Mandrake 和 Red Hat 上，路径为 `/var/www/manual/`）。许多常用的指令列在表 21-4 中。

## 服务器配置

某些指令用于配置你服务器的整体操作。这些指令放置在 `httpd.conf` 配置文件中。某些指令需要路径，而另一些只需要通过 `on` 和 `off` 关键字来开启或关闭。Apache 提供了一个默认的 `httpd.conf` 配置文件。`httpd.conf` 已经包含了这些指令。某些指令前面的 `#` 符号被注释掉了。

你可以通过删除 `#` 符号来激活指令。许多条目前面都有解释其用途的注释。以下是 `ServerAdmin` 指令的示例，用于设置用户发送管理问题邮件的地址。你将 `you@address` 条目替换为你想要接收系统管理邮件的条目。默认情况下，它设置为 `root@localhost`。

```
# ServerAdmin: 你的地址，问题应发送至此处

ServerAdmin you@your.address
```

某些指令需要关于你系统的特定信息。例如，`ServerName` 保存你 Web 服务器的主机名。指定主机名对于避免不必要的 DNS 查找失败导致服务器挂起非常重要。注意该条目被 `#` 注释了。只需删除 `#` 并在 `new.host.name` 中输入你 Web 服务器的主机名。

```
# ServerName 允许你设置一个主机名，如果该主机名与程序

# 获取的主机名不同，则将其返回给客户端（例如：

# 使用 "www" 而不是主机的真实名称）。

#ServerName new.host.name
```

在 Mandrake、SuSE 和 Red Hat 中，对于使用 `/var/www` 作为 Web 目录的标准 Web 服务器安装，已经创建了条目。你可以通过更改适当的指令来根据需求定制你的 Web 服务器。`DocumentRoot` 决定了 Web 页面的家目录。`ServerRoot` 指令指定了你 Web 服务器配置、错误和日志文件的存放位置。

```
DocumentRoot /var/www/html

ServerRoot /etc/httpd
```

`MaxClients` 指令设置同时连接到你服务器的最大客户端数量。

```
MaxClients 150
```

## 目录级配置：.htaccess 和 <Directory>

Apache 最灵活的方面之一是其配置单个目录的能力。通过 `Directory` 指令，你可以定义一个仅适用于特定目录的指令块。此类指令可以放置在 `httpd.conf` 或 `access.conf` 配置文件中。你也可以在特定目录中使用 `.htaccess` 文件来存放配置指令。指令随后仅应用于该目录。“htaccess”名称实际上是通过 `AccessFileName` 指令设置的。如果你需要，可以更改它。

```
AccessFileName .htaccess
```

`Directory` 块以 `<Directory pathname>` 指令开始，其中 `pathname` 是要配置的目录。结束指令使用相同的 `<>` 符号，并在“Directory”单词前加斜杠：`</Directory>`。放置在此块内的指令仅适用于指定的目录。以下示例拒绝来自 `www.myvids.com` 的请求对 `mypics` 目录的访问。

```
<Directory /var/www/html/mypics>

Order Deny, Allow

Deny from www.myvids.com

</Directory>
```

通过 `Options` 指令，你可以启用某些功能，如符号链接、自动索引、CGI 执行和内容协商。默认值是 `All`，它会开启所有功能。以下示例启用了自动索引（Indexes）、符号链接（FollowSymLinks）和内容协商（Multiviews）。控制会从上级目录继承到下级目录。如果你想按目录严格控制整个站点的访问，可以使用以下条目拒绝所有用户。然后，在单个目录中，你可以允许某些用户、组或主机访问。

```
<Directory /var/www/html>

Order Deny,Allow

Deny from All

</Directory>
```

## 访问控制

通过 `allow` 和 `deny` 等访问控制指令，你可以根据远程用户和主机控制对 Web 站点的访问。`allow` 指令后跟主机列表将限制仅允许这些主机访问。带有主机列表的 `deny` 指令将拒绝这些系统的访问。`all` 参数适用于所有主机。`order` 指令指定应用访问控制指令的顺序。其他访问控制指令（如 `require`）可以建立身份验证控制，要求用户登录。访问控制指令可以全局用于控制整个站点，也可以在 `Directory` 指令内控制单个目录。在此示例中，允许所有用户访问：

```
order allow,

allow from all
```

你可以通过将其限制在特定的 HTML 访问方法来进一步限定访问控制指令。HTML 访问方法是浏览器与你 Web 站点的接口。例如，浏览器可以从页面获取信息（GET）或通过页面发送信息（POST）。你可以使用 `<Limit>` 指令来控制此类访问方法。该指令随后与 `<Limit>` 配对定义一个 `Limit` 块，你可以在其中放置访问控制指令。这些指令仅适用于指定的访问方法。你可以将此类 `Limit` 块与 `Directory` 块一起使用，为特定目录设置访问方法控制。`/etc/config/httpd.conf` 文件中的以下 Directory 块控制你 Web 站点主目录 `/var/www/html` 的访问。

```
# 这应该根据设置的 DocumentRoot 进行更改

<Directory /var/www/html>

Options Indexes FollowSymLinks

AllowOverride All

<Limit GET>

order allow,

allow from all

</Limit>

</Directory>
```

## URL 路径名

某些指令可以修改或完成用于访问你网站的 URL 路径段。URL 的路径段指定了你网站上的特定目录或 Web 页面。指令允许你访问或重定向路径名，并选择默认 Web 页面。通过 `Alias` 指令，你可以让用户访问系统其他部分、其他文件系统或其他网站上的资源。别名使用互联网上网站的 URL，而不是你系统上目录的路径名。通过 `Redirect` 指令，你可以将用户重定向到另一个站点。

```
Alias /mytrain /home/dylan/trainproj

Redirect /mycars http://www.myautos.com/mycars
```

如果只给 Apache 提供一个目录而不是特定的 Web 页面，它会在该目录中查找索引 Web 页面并显示它。默认 Web 页面的可能名称由 `DirectoryIndex` 指令列出。通常使用的名称是 `index.html`，但你可以添加其他的。标准名称在此显示。当给 Apache 访问一个 Web 目录时，它会查找并显示位于其中的 `index.html` Web 页面。

```
DirectoryIndex index.html index.shtml index.cgi
```

Apache 还允许用户在用户主目录下的特殊子目录中维护 Web 页面，而不是主网站目录。使用 `~` 加上用户名可以访问此目录。该目录的名称通过 `UserDir` 指令指定。默认名称是 `public_html`，如下。站点 `turtle.mytrek.com/~dylan` 访问主机 `turtle.mytrek.com` 目录 `turtle.mytrek.com/home/dylan/public_html`。

```
UserDir public_html
```
