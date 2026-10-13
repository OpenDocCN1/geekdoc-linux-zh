
通常，指令被放置在主要的配置文件之一中。这些文件中的 `Directory` 指令可用于配置特定目录。然而，Apache 同样利用基于目录的配置文件。任何目录都可以有自己的 `.htaccess` 文件，其中存储了配置该目录的指令。如果你的站点有许多目录，你可以在每个目录中放置配置指令。使用 `.htaccess` 而不是向主配置文件中填充特定的 `Directory` 指令。你可以控制 `.htaccess` 文件中的哪些指令优于主配置文件中的指令。如果你的站点允许用户或客户端控制的目录，你可能希望仔细监控或禁用这些目录中对 `.htaccess` 文件的使用。（除非使用 `AllowOverride` 指令禁用，否则 `.htaccess` 文件中的指令可能会覆盖标准配置文件。）

Apache Web 服务器的强大功能和灵活性源于其使用模块来扩展其功能。Apache 使用一组核心指令实现。可以创建包含其他指令定义的模块。这些模块可以被加载到 Apache 中，允许你为你的服务器使用这些指令。Apache 分发版包含了一组标准模块，尽管你可以下载其他模块并创建自己的。例如，`mod_autodeindex` 包含了自动索引目录的指令（如下节所述）。`mod_mime` 包含了 MIME 类型和处理程序指令。模块通过 `LoadModule` 指令加载。在 Red Hat Linux 上，你可以在 `httpd.conf` 文件中找到大多数标准模块的 `LoadModule` 指令。

```
LoadModule mime_module modules/mod_mime.so
```

随 Apache 包一起提供的 `apx` 应用可用于构建 Apache 扩展模块。通过 `apx` 应用，你可以用 C 语言编译 Apache 模块共享对象，并使用 `LoadModule` 指令动态加载。Apache `apx` 应用要求 `mod_so` 模块是你 Apache 应用程序的一部分。它包含了丰富的选项，例如用 `-n` 指定模块名称，`-a` 为其添加条目，`-t` 安装模块到你的 Web 服务器。Apache `apx` 应用要求 `mod_so` 模块是你 Apache 应用程序的一部分。它包含了丰富的选项，例如用 `-n` 指定模块名称，`-a` 为其添加条目，`-t` 安装模块到你的 Web 服务器。在 Apache Hat 系统上，Apache `.` 根根。更常用的 Apache 指令列在表 24-3 中。

### 表 24-3：Apache 格式符

| 格式符 | 描述 |
| :--- | :--- |
| `%a` | 远程 IP 地址 |
| `%A` | 地 IP 地址 |
| `%b` | | HTTP HTTP（字节字节字节 |
| `%` `%` | | 变量 |
| `%f` | 文件名 |
| `%h` | 远程主机 |
| `%l` | 远程主机（来自标识） |
| `%m` | 请求方法 |
| `%P` | 服务请求的子进程 ID |
| `%r` | 请求的第一行 |
| `%s` | 状态码 |
| `%t` | 时间，以常用日志格式表示 |
| `%u` | 远程用户（来自认证）；如果 %s 是401 |
| `%U` | 请求 URL 路径 |
| `%v` | 服务请求的规范服务器名称 |

## 服务器配置

某些指令用于配置服务器的整体操作。这些指令放置在 `httpd.conf` 文件中。某些需要路径，而另一些只需要开启。Apache 提供了一个默认的 `httpd.conf` 文件。该文件已经包含了这些指令。有些被 `#` 号注释掉了。你可以移除 `#` 号来激活指令。许多指令前面都有说明用途的注释。如下：

```
# ServerAdmin: 出现问题时的邮件地址

ServerAdmin your@address
```

某些指令需要关于服务器的特定信息。例如，`ServerName` 存储你服务器的主机名。指定主机名对于避免 DNS 查找失败导致服务器挂起很重要。注意该条目被 `#` 注释，并将你的 Web 服务器主机名替换为新的。

```
# ServerName 允许你设置一个返回给客户端的主机名，

# 如果它与程序获取的不同（例如，使用 "www" 代替主机真实名称）

ServerName localhost
```

在 Red Hat 系统上，已经为标准的 Web 服务器安装使用了 `/var/www` 作为站点。你可以通过更改相应的指令来对你的站点进行定制。`DocumentRoot` 指令决定了 Web 页面的根目录。`ServerRoot` 指令指定了 Web 服务器配置、错误和日志文件的位置。

```
DocumentRoot /var/www/html

ServerRoot /etc/httpd
```

`MaxClients` 指令设置同时连接到服务器的最大客户端数量。

```
MaxClients 150
```

## 目录级配置：.htaccess 和 <Directory>

Apache 最灵活的特性之一是配置单个目录的能力。通过 `Directory` 指令，你可以定义一个仅适用于特定目录的指令块。此类指令可以放置在 `httpd.conf` 或 `access.conf` 配置文件中。你还可以在特定目录内使用 `.htaccess` 文件来存放配置指令。这些指令将仅应用于该目录。`.htaccess` 这个名称实际上是由 `AccessFileName` 指令设置的。如果你需要，可以更改它。

### .htaccess 访问

`<Directory>` 块以 `<Directory pathname>` 指令开始，其中 `pathname` 是要配置的目录。结束指令使用 `~` 符号，并在 "Directory" 词前有一个斜杠：`</Directory>`。放置在此块内部的指令仅适用于指定的目录。以下示例仅拒绝来自 www.myvideos.com 的请求对 mypics 目录的访问。

```
<Directory /var/www/html/mypics>

Order Deny,Allow

Deny from www.myvideos.com

</Directory>
```

通过 `Options` 指令，你可以在目录中启用某些功能，例如符号链接的使用、自动索引、CGI脚本的执行以及内容协商。默认是 `All` 选项，它会开启除内容协商（Multiviews）之外的所有功能。以下示例启用了自动索引（Indexes）、符号链接（FollowSymLinks）：

```
Options Indexes FollowSymLinks Multiviews
```

在主配置文件或上级目录中指令中的配置会被下级目录继承。在 `.htaccess` 文件和 `<Directory>` 块中，可以允许特定目录覆盖这些配置。这种能力可以通过 `AllowOverride` 指令来控制。使用 "all" 参数，`.htaccess` 文件可以覆盖之前的任何配置。"none" 参数则允许覆盖，实际上是禁用了 `.htaccess` 文件。你可以进一步控制特定指令组的覆盖。`AuthConfig` 启用授权指令的使用，`FileInfo` 用于类型指令，`Indexes` 用于索引指令，`Limit` 用于访问控制指令，而 `Options` 用于选项指令。

### 访问控制

通过访问控制指令（如 `allow` 和 `deny`），你可以控制远程用户和主机对你 Web 站的访问。`Allow` 指令通过主机名列表过滤访问，将其限制为仅允许这些主机。带有 "all" 参数的 `deny` 指令拒绝所有主机的访问。`order` 指令指定了访问控制指令应用的顺序。其他访问控制指令（如 `require`）可以建立身份验证，要求用户登录。所有访问控制指令都可以全局使用以控制整个站点，也可以放置在 `<Directory>` 块中以控制单个目录的访问。在以下示例中，允许用户访问：

```
order allow,deny

allow from all
```

你可以通过将访问限制为某些 HTML 访问方法来细化访问。HTML 访问方法是浏览器与你的 Web 站交互的方式。例如，浏览器可以从页面获取信息（GET）或通过该页面发送信息（POST）。你可以使用 `<Limit>` 指令控制访问方法。`Limit` 接受要控制的访问方法列表作为参数。该指令随后与 `</Limit>` 指令配对，定义一个 `Limit` 块，你可以在其中放置访问控制指令。这些指令仅适用于指定的访问方法。你可以将 `Limit` 块与 `<Directory>` 块一起使用，设置特定目录的访问方法控制。在 Red Hat 发行版上，`/etc/config/httpd.conf` 文件中的后续 `<Directory>` 块设置了你 Web 站目录 `/var/www/html` 的访问方法。

```
# 这应该更改为任何 documentRoot。

<Directory /var/www/html>

Options Indexes FollowSymLinks

AllowOverride All

<Limit GET>
