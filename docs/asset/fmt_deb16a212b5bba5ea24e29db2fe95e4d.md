
此外，Apache 2 安装了 `/usr/local/etc/apache2x/extra_directory`，其中包含几个额外文件：`httpdssl.conf`、`http-vhosts.conf`、`http-userdir.conf` 等。这些文件允许您在较小的外部文件中配置 Apache 的特定功能（如 SSL 安全或用户的主目录），以保持其整洁并易于维护。如果您希望将所有配置选项保留在一个文件中，可以拷贝单个文件的内容。

# 表 26.2 AllowOverride 配置选项

| 指令 (Directive) | 允许 .htaccess 文件覆盖的内容 |
|---|---|
| `AllowOverride Options` | `Options` 指令 |
| `AllowOverride FileInfo` | 文件类型指令，例如 `AddType` 和 `ErrorDocument` |
| `AllowOverride AuthConfig` | 授权指令，如 `Require` 和 `Auth` |
| `AllowOverride Limit` | 主机访问指令，如 `Allow`、`Deny` 和 `Order` |
| `AllowOverride All` | 以上所有内容 |

注意

`Options` 指令是 Apache 中最大且功能最全的项之一；它控制着 Apache 许多重要功能的可用性，例如 `ExecCGI`（执行 CGI 脚本的能力）、`Includes`（服务器包含）和 `MultiViews`（多视图内容协商）。这些功能可以在分级目录结构中的任何层级对配置进行添加或删减。请参阅 `http://httpd.apache.org/docs/1.3/mod_core.html#options` 了解关于 `Options` 指令的完整内容以及如何使用。

配置完成后，请重启服务器，正如我们稍后将讨论的那样。现在你可以在任何 Web 可访问目录中放置 `.htaccess` 文件，并将其放入 Apache 允许 `.htaccess` 文件的任何配置目录中（关于 `.htaccess` 上下文中将使用哪些指令的详情，请参见 `http://httpd.apache.org/docs/`）。

注意

常用访问目录中的 `.htaccess` 文件可能会影响性能，因为服务器必须在每个新的 HTTP 请求时打开并读取它。如果可能，最好将更改配置到全局 `httpd.conf` 文件中，这样它只需读取一次。

`httpd.conf` 文件（或 `extra/user-dir.conf`）包含一个用于控制用户目录 (`/home`) 的注释块；如果你计划运行一个允许不同用户拥有自己站点的服务器，但你又希望让支持各种数据更改 HTTP/1.1 方法（如 `DELETE`、`COPY` 和 `MOVE`）的浏览器无法执行这些操作，并且你想解锁此块：

```
# 控制 UserDir 目录的访问。以下是一个示例
# 适用于这些目录限制为只读的站点。
#<Directory /home/*/public_html>
# AllowOverride FileInfo AuthConfig Limit
# Options MultiViews Indexes SymLinksIfOwner IncludesNoExec
# <Limit GET POST OPTIONS PROPFIND>
# Order allow,deny
# Allow all
#
</Limit>
```

## 第 26 章 配置 Web 服务器

```
</Limit>
#   <LimitExcept GET OPTIONS PROPFIND>
#     Order deny,allow
#     Deny from all
#   </LimitExcept>
#</Directory>
```

请注意，这里的 `AllowOverride` 允许 `.htaccess` 文件覆盖 `File`、`AuthConfig` 和 `Limit` 指令，前提是 `Options` 指令已在全局级别设置且未允许覆盖。

根据历史背景，每个用户的文档目录被称为 `public_html`；因此，对 `/home.some/~user/` 的请求如果存在 `index.html` 文件，则会显示该文档，Apache 将提供该文件而不是目录列表。（微软服务器通常使用 `Default.htm` 实现此功能。）你可以使用 `DirectoryIndex` 指令指定任意数量的此类索引文件名。Apache 将尝试按照你输入它们的顺序尝试你指定的每个文件。

## 启动和停止 HTTP 守护进程

`ports` 集合中的 Apache 安装过程将自动启动服务器。你可以通过使用 `ps` 和 `grep` 查找 `httpd` 进程来验证这一点：

```
# ps -waux | grep httpd
root      220 0.0 2.0 4436 2456 ?? Ss Sat02PM 00:02:79 /usr/local/sbin/httpd
nobody    303 0.0 2.0 4496 2548 ?? I Sat02PM 00:00:00 /usr/local/sbin/httpd
nobody    304 0.0 2.0 4462 2452 ?? I Sat02PM 00:00:00 /usr/local/sbin/httpd
nobody    305 0.0 2.0 4462 2452 ?? I Sat02PM 00:00:00 /usr/local/sbin/httpd
nobody    306 0.0 2.0 4462 2452 ?? I Sat02PM 00:00:00 /usr/local/sbin/httpd
nobody    307 0.0 2.0 4462 2452 ?? I Sat02PM 00:00:00 /usr/local/sbin/httpd
nobody 13963 0.0 2.0 4468 2468 ?? I Sat02PM 00:00:00 /usr/local/sbin/httpd
```

注意 Apache 1.3 使用 `fork` 模型（`forking model`），其中一个“主”进程（此处输出中由 `root` 所有）监听 80 端口以接收的请求，然后派生一个自己的副本（由特权伪用户 `nobody` 所有）作为子进程来处理每个请求。主进程本身不会处理任何请求。

拥有一个以 `root` 身份运行的 Web 服务器是非常危险的，这意味着它也可以以 `root` 身份执行 CGI 程序——一个微小的 CGI 脚本就可能导致漏洞被利用，从而清空你的整个硬盘。

## 启动和停止 HTTP 守护进程

在 `fork` 模型下，如果你想重启服务器，手动杀死进程是不切实际的。Apache 提供了一个名为 `apachectl` 的工具来处理这种情况。`apachectl` 的常用用法是 `restart` 和 `graceful` 命令。这些命令允许你在不中断当前连接的情况下重新加载配置。

如果你想停止服务器，可以使用 Apache 提供的 `stop` 命令：

```
# apachectl stop
/usr/local/sbin/apachectl stop: Apache stopped
```

## 第 26 章 配置 Web 服务器

`apachectl` 的另一个常用用法是 `configtest` 命令。这会让 Apache（无论是否正在运行）读取 `/etc/apache` 中的配置文件并报告任何错误，但它不会实际启动服务器。这是一个极好的诊断工具，也是 `restart` 和 `graceful` 命令的组成部分。如果配置无效，它将保持运行中的进程不变。

```
# apachectl configtest
/usr/local/sbin/apachectl graceful: Syntax OK
```

> 提示
>
> 如果 Apache 没有运行，`apachectl restart` 或 `apachectl graceful` 将启动它。

## 使用 Apache 进行基础访问控制

网站某些部分几乎都需要防止公众查看；访问控制允许你通过主机/IP 地址或密码验证将这些部分限制给授权用户。我们将查看这些。

### 按地址访问控制

假设你想将一个文件、目录或一组文件和目录限制一组短的 IP 地址或主机名。如果你有一个永久安全的站点区域（例如一组管理脚本），可以在全局 (`httpd.conf`) 级别执行；或者对于普通用户或临时资源，更高效的方法是在任何目录（或其受保护项目的上级目录）中使用 `.htaccess` 文件。

首先，确保在你想要保护的站点部分启用了 `.htaccess` 覆盖。正如你之前提到的，你可以在 `/usr/local/www/data` 级别或目录结构中更深处的另一个 `<Directory>` 容器中使用 `AllowOverride Limit`，以启用访问控制指令 `Allow`、`Deny` 和 `Order` 的使用。

要关闭一个目录对指定地址或主机名以外的所有访问，在该目录中放置一个包含以下内容的 `.htaccess` 文件：

# 使用 Apache 进行基础访问控制

`Order deny,allow`

`Deny from all`

`Allow from 64.41.131.102`

`Allow from stripes.example.com`
