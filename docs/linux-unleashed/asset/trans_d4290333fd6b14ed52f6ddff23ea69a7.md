
## Port
httpd 应监听客户端的端口号。默认端口为 80。如果您不希望 Web 服务器普遍可用，请选择其他数字。

## ResourceConfig
srv.conf 文件的路径，通常为 conf/srv.conf。

## ServerAdmin
管理员的电子邮件地址。

## ServerName
服务器的完全限定主机名。

## ServerRoot
用户不能移动的路径之上（通常是 Web 服务器顶层目录或 /usr/local/etc/httpd）。

## ServerType
独立（守护进程）或 inetd。

## StartServers
守护进程执行时启动的服务器进程数量。

## TimeOut
等待客户端请求的秒数，超过该时间后将断开连接（默认为 1,800，建议减少）。

## TransferLog
访问日志位置的路径。默认为 logs/access_log。

## TypesConfig
MIME 配置文件位置的路径。默认为 conf/mime.conf。

## User
定义服务器应以哪个用户身份运行（仅在作为守护进程运行时有效）。可以是名称或数字，如果是数字，前面必须加 #。默认为 #-1。

接下来需要检查的配置文件是 srv.conf，它用于处理服务器资源。srv.conf 文件中需要检查或设置的变量如下：

## AccessFileName
提供访问权限的文件（默认为 .htaccess）。

## AddDescription
提供一种文件类型的描述。例如，条目可以是 AddDescription PostScript file *.ps。允许多个条目。

## AddEncoding
指示具有特定扩展名的文件以某种方式编码，例如 AddEncoding compress z。允许多个条目。

## AddIcon
指定为每种类型文件显示的图标名称。

## AddIconType
使用 MIME 类型来确定使用的图标。

## AddType
覆盖扩展名的 MIME 定义。

## Alias
将一个路径名替换为另一个路径名，例如 `Alias data /usr/www/data`。

## DefaultType
默认 MIME 类型，通常为 `text/plain`。

## DefaultIcon
当 FancyIndexing 开启时使用的默认图标（默认为 `/icons/unknown.xbm`）。

## DirectoryIndex
当 URL 仅针对您的服务时返回的文件名。默认值为 `index.html`。

## DocumentRoot
HTML 文档目录的绝对路径。默认为 `/usr/local/etc/httpd/htdocs`。

## FancyIndexing
为索引的文件列表添加图标和文件名信息。默认开启。（此选项用于与 HTTP 首次发行版的向后兼容性。）

## HeaderName
在正在索引的文件列表顶部使用的文件名。默认为 `Header`。

## IndexOptions
索引参数（包括 FancyIndexing、IconsAreLinks、ScanHTMLTitles、SuppressLastModified、SuppressSize 和 SuppressDescription）。

## ReadmeName
脚注文件显示在目录索引中。默认为 `README`。

## Redirect
将一个路径映射到另一个 URL。

## ScriptAlias
类似于 Alias，但用于脚本。

## UserDir
用户可用于 httpd 访问的目录。默认为 `public_html`。通常设置为用户的主页目录。可以设置为 DISABLED。

第三个需要检查和修改的文件是 `access.conf-dist`，它定义了可供 WWW 浏览器使用的服务。通常，浏览器可以访问所有内容，但您可能希望修改该文件以加强安全性或禁用您的 Web 网站不支持的一些服务。`conf-dist` 文件的格式与前两个配置文件不同。它使用由尖括号界定的一组“分节指令”。条目的通用格式为：

```
<Directory Dir_Name> ...
</Directory>
```

开头和结尾定界符（分别为 `<Directory>` 和 `</Directory>`）之间的内容是指令。实际上，由于文件中可能存在多种变体，事情并没有那么简单。定制 access.conf-dist 文件的最佳方法是遵循典型 Web 服务器安装步骤：

1.  定位 Options 指令并移除 Indexes 选项。这可以防止用户浏览 httpd 目录。稍后讨论有效的 Options 条目。
2.  定位第一个 Directory 指令并检查 cgi-bin 目录的路径。默认路径是 `/usr/local/etc/httpd/cgi-bin`。
3.  找到 AllowOverride 变量并将其设置为 None（这可以防止其他人更改设置）。默认为 All。稍后讨论 AllowOverride 变量的有效值。
4.  找到 Limit 指令并设置为您想要的值。

Limit 指令控制对服务器的访问。Limit 指令的有效值如下：

-   **allow**：允许在 allow 关键字后指定的特定主机名访问该服务。
-   **deny**：拒绝在 deny 关键字后指定的特定主机名访问该服务。
-   **order**：指定评估 allow 和 deny 指令的顺序（通常设置为 deny, allow，但也可以是 allow, deny）。
-   **require**：要求通过 AuthUserFile 条目中指定的用户文件进行身份验证。

Options 指令可以有多个条目，每个条目都有不同的用途。Options 的默认条目是：
`Options Indexes FollowSymlinks`
您在上述自定义过程的第一步中从 Options 指令中移除了 Indexes 条目。这些条目均应用于 Options 字段所在的目录。Options 指令的有效条目如下：

-   **All**：启用所有功能。
-   **ExecCGI**：可以从此目录执行 cgi 脚本。
-   **FollowSymlinks**：允许 httpd 跟随符号链接。
-   **Includes**：启用服务器的包含文件。
-   **IncludesNoExec**：启用服务器的包含文件，但禁用 exec 选项。
-   **Indexes**：允许用户获取服务器生成的索引（不影响预编译索引）。
-   **None**：不启用任何功能。
-   **SymLinksIfOwnerMatch**：仅当符号链接的用户 ID 与文件的用户 ID 匹配时才跟随符号链接。

AllowOverride 变量默认设置为 All，这应该更改。AllowOverride 有多个有效值，但对于大多数 Linux 系统，推荐的设置是 None。AllowOverride 的有效值如下：

-   **All**：由每个目录中的配置文件控制访问。
-   **AuthConfig**：启用某些身份例程。有效值：AuthName（设置目录的授权名称）；AuthType（设置目录的授权类型，尽管只有一个合法值：Basic）；AuthUserFile（指定包含用户名和密码的文件）；以及 AuthGroupFile（指定包含组名的文件）。
-   **FileInfo**：启用 AddType 和 AddEncoding 指令。
-   **Limit**：启用 Limit 指令。
-   **None**：不允许访问文件。
-   **Options**：启用 Options 指令。

完成上述操作后，配置文件应已正确设置。虽然语法有点令人困惑，但阅读默认值可以告诉您在更改条目时应使用的正确格式。接下来，您可以启动 Web 服务器软件。

## 启动 Web 软件

配置完成后，是时候尝试 Web 服务器软件了。在配置文件中，您决定了 Web 软件是作为守护进程（独立）运行还是从 inetd 启动。每种方法的启动程序略有不同（这是意料之中的），但两种启动程序都可以在命令行中使用以下三个选项之一：

-   **-d**：服务器文件根目录的绝对路径（仅当默认位置无效时使用）。
-   **-f**：如果不是 httpd.conf 的默认值，则读取的配置文件。
-   **-v**：显示版本号。

如果您使用 inetd 启动 Web 服务器软件，需要对 /etc/services 文件进行修改以允许 Web 软件。向 /etc/services 文件添加类似以下的一行：

```
http port/tcp
```

其中 *port* 是您的 Web 服务器软件使用的端口号（通常为 80）。

接下来，修改 /etc/inetd.conf 文件以包含 Web 服务器的启动命令，其中最后一项是 httpd 二进制文件的路径：

```
httpd stream tcp nowait nobody /usr/web/httpd
```

完成后，通过杀死并重启 inetd 进程或重启系统来重启 inetd，服务应可通过您在 /etc/services 中指定的任何端口访问。

如果您将 Web 服务器软件作为守护进程运行，可以随时通过以下命令从命令行启动它：

```
httpd &
```

更好的做法是将启动命令添加到正确的 rc 启动文件中。条目通常看起来像这样：

```
# start httpd
if [ -x /usr/web/httpd ]
then
    /usr/web/httpd
fi
```

当然，要替换 httpd 二进制文件的正确路径。重启您的机器应在默认端口号上启动 Web 服务器软件。

要测试 Web 服务器软件，请使用任何 Web 浏览器并在 URL 字段中输入以下内容：

```
http://machinename
```

其中 *machinename* 是您的 Web 服务器的名称。您可以通过连接 Internet 或从网络上的另一台机器（如果您有的话）执行此操作。如果您看到根 Web 目录的内容或 `index.html` 文件，则一切正常。否则，请检查日志文件和配置文件以寻找问题的线索。

如果您尚未安装 Web 浏览器，可以使用 telnet 检查 Web 服务器是否正在运行。发出类似以下的命令，替换您的服务器名称（如果 Web 端口号不同于 80，也替换端口号）：

```
telnet www.wizard.tpci.com 80
```

