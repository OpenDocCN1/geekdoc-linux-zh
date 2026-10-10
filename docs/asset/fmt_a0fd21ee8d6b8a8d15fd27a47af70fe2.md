
Apache 程序包提供的 `apxs` 可用于构建 Apache 扩展模块。通过 `apxs`，你可以用 C 语言编译 Apache 源代码，并创建可以使用 `LoadModule` 指令加载的动态共享对象。Apache 要求必须存在 `mod_so` 模块，它包含了广泛的选项，例如用 `-n` 指定模块名称，`-a` 在 `httpd.conf` 文件中添加条目，以及 `-i` 在你的 Web 服务器上安装模块。

你可以在 Apache 服务器 `http.apache.org` 以及位于你网站 Web 根目录下的 Apache 手书中找到 Apache 配置指令的完整列表。在许多系统中，它位于分发版设置的 Web 站点默认条目的主子目录下（是 `/var/www/manual/`）。

# 第五部分：网络服务器

## 服务器配置

直接指令用于配置您服务器的整体操作。这些指令放置在 `httpd.conf` 配置文件的中间，直接位于标记为 Server Settings（服务器设置）的章节下方。某些指令需要路径名，而另一些指令只需要通过 `on` 和 `off` 关键字开启或关闭。`httpd.conf` 文件已经包含了这些指令。某些指令被开前的 `#` 符号注释掉了。你可以通过删除 `#` 符号来激活某个指令。许多条目的前面都有解释其用途的注释。

以下是 `ServerAdmin` 指令的示例，用于设置用户发送管理性问题的地址。你将 `you@your.address` 替换为你想要接收系统管理邮件的地址。默认情况下，它设置为 `root@localhost`。

```
# ServerAdmin: 您的地址，问题应电子邮件至此处。
ServerAdmin you@your.address
```

Web 服务器通常使用 80 端口，这是 Apache 的默认端口。如果你想使用不同的端口，请用 `Port` 指令指定它。

```
80
```

`ServerName` 指令持有您的 Web 服务器的主机名。指定主机名对于避免不必要的 DNS 查找失败导致服务器挂起非常重要。注意该条目被 `#` 注释了。只需删除 `#` 在 `new.host.name` 处输入你的 Web 服务器主机名。如果你使用的端口不是 80，请务必在附加的主机上指定它，例如 `turtle.mytrek.com:80`。这里是原始条目：

- `ServerName` 允许你设置一个主机名，如果该主机与程序
# 获取的主机不同，则会将该主机名发送回给客户端
# 用于你的服务器（例如，使用
# "www" 而不是主机的真实名称）。

```
ServerName new.host:80
```

一个修改后的 `ServerName` 条目看起来如下：

```
ServerName turtle.mytrek.com
```

当接收到 `UseCanonicalName` 指令请求时（例如对于系统上的本地文件），系统将使用 `ServerName` 和 `Port` 指令来生成 URL 服务器名称。如果它是关闭的，则将使用客户端请求提供的名称。如果服务器通过一个名称引用，而通过其他名称引用（例如曾用 `www.com` 指代 `turtle.mytrek.com`），这可能会引起混淆。将 `UseCanonicalName` 设置为 `on` 可以解决这个问题，生成正确的 URL。

在 Fedora 系统上，已经为使用 `/var/www` 作为你的网站目录的标准 Web 服务器创建了条目。你可以通过更改适当的指令根据自己的需求定制网站。`DocumentRoot` 指令决定你的 Web 用户的根目录。

```
DocumentRoot /var/www/html
```

### MPM 配置

MPM `prefork` 和 `worker` 模块的配置设置使你的 Apache Web 服务器适应工作负载需求。默认条目已经为在轻负载负载下运行的标准 Web 服务器准备就绪。你可以根据不同需求修改这些设置。

Fedora 有条件地配置了 Unix 和 Linux 系统常用的两种 MPM 模块：`prefork` 和 `worker`。`worker` 模块支持每个进程运行多个线程，在保持兼容性的同时降低对服务器资源的负载。它们共享多个指令，例如 `StartServer` 和 `MaxRequestsPerChild`。你可以通过设置 `/etc/sysconfig/httpd` 文件中的选项来决定使用哪个模块。

## 第 23 章：Web 服务器：Apache 497

注意 你也可以配置 Apache 仅作为代理或缓存服务器运行。默认代理缓存服务器指令已包含在 `httpd.conf` 文件中。`ProxyRequests` 指令开启代理活动。可以使用类似 `CacheRoot` 的指令配置缓存目录，使用 `CacheSize` 指定缓存大小（默认 500KB），使用 `CacheExpire` 为未修改的文档设置时间限制。

## 目录级配置：.htaccess 和 <Directory>

Apache 最灵活的方面之一是它配置单个目录的能力。通过 `Directory` 指令，你可以定义一个仅适用于特定目录的指令块。此类指令可以放置在 `httpd.conf` 或访问配置文件中。你也可以在特定目录中使用 `.htaccess` 文件来存放配置指令。这些指令随后仅应用于该目录。"htaccess" 这一名称实际上是通过 `AccessFileName` 指令设置的。如果你愿意，可以更改它。

```
AccessFileName .htaccess
```

`Directory` 块以 `<Directory pathname>` 指令开始，其中 `pathname` 是要配置的目录。结束时使用 `<>` 符号，并在 "Directory" 词前加上斜杠：`</Directory>`。放置在此块内的指令仅适用于指定的目录。接下来的示例演示了仅允许来自 `www.myvids.com` 的 `mypics` 请求访问。

```
<Directory /var/www/html/mypics
Deny, Allow
Deny from www.myvids.com
</Directory>
```

通过 `Options` 指令，你可以启用目录中的某些功能，例如符号链接的使用、自动索引、C CGI 脚本执行和内容协商。默认是 `All` 选项，它会开启内容协商（Multiview）之外的所有功能。接下来的示例启用了自动索引（Indexes）、符号链接（FollowSymLinks）和内容协商（Multiview）。

```
Options FollowSymLinks Multiview
```

配置通过配置文件或上级目录中的指令项完成。存储在 `.htaccess` 文件和 `Directory` 块中的特定目录指令可以被这些配置覆盖。这种能力可以通过 `AllowOverride` 指令进行控制。使用 `all` 参数，`.htaccess` 文件可以覆盖任何之前的配置。使用 `none` 参数不允许覆盖，实际上禁用了 `.htaccess` 文件。你可以进一步控制授权指令、用于类型指令的 `FileInfo`、用于索引指令的 `Indexes`、用于访问控制指令的 `Limit` 以及用于选项指令的 `Options`。

```
AllowOverride all
```

![](img/af27012edddcf42a8b40fad81183c10b_534_0.png)

## 访问控制

通过访问控制指令（如 `allow` 和 `deny`），你可以控制远程用户和主机对你网站的访问。`allow` 指令后跟随主机名列表将访问限制为仅这些主机。带有主机名列表的 `deny` 指令将拒绝这些系统的访问。参数 `all` 将指令应用于所有主机。`order` 指令指定了访问控制指令的执行顺序。

```
order, deny
allow all
```

## URL 路径名

某些指令可以修改或完成用于访问网站的 URL 路径段。URL 的路径段指定网站上的特定目录或 Web 页面。指令允许你别名或重定向路径名，以及选择默认 Web 页面。通过 `Alias` 指令，你可以让用户访问位于系统其他部分或其他系统的资源。别名可以使用 URL 而不是系统上的路径名。通过 `Redirect` 指令，你可以将用户重定向到另一个站点。

```
Alias /mytrain /home/dylan/train
Redirect /mycars http://www.autos.com/mycars
```

如果 Apache 只接收目录而不是特定的 Web 页面，它将查找该目录下的索引页并显示它。通常使用的名称由 `DirectoryIndex` 指令列出。使用的是 index.html，但你可以添加其他的。这里了标准名称。当 Apache 只访问一个 Web 目录时，它会查找并显示其中的 `index.html` Web 页面。

```
DirectoryIndex index.html index.shtml index.cgi
```
