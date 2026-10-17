
Order Ordering Allow|from hostname|IP address or the IP address range

Deny from hostname|IP address or the IP address range

```

其中 `ordering` 值设置为 `"Allow, deny"` 或 `"Deny, allow"`。

### `apachectl` 命令

Apache HTTP 服务器控制接口（`apachectl`）是一个允许管理员使用 `apachectl` 命令控制 HTTP 服务功能的接口。`apachectl` 命令支持各种选项。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_629_1.png)

| 选项 | 用途 |
|---|---|
| `start` 或 `apachectl -k start` | 启动 `apache` 守护进程。如果守护进程已在运行，它会显示错误消息。 |
| `stop` 或 `apachectl -k stop` | 停止 `apache` 守护进程。 |
| `restart` 或 `apachectl -k restart` | 重启 `apache` 守护进程。如果守护进程未运行，它会启动该守护进程。 |
| `fullstatus` | 显示由客户端请求的正在运行的服务的完整状态报告。它需要在系统上启用 `mod_status` 模块。 |
| `status` | 显示由客户端请求的服务的状态报告。该报告不包括正在运行的服务列表。 |
| `configtest` 或 `apachectl -t` | 运行配置文件测试，报告成功状态为“`Syntax OK`”或显示错误消息。它还用于测试 `ssl.conf` 文件的语法。 |
| `graceful` 或 `apachectl -k graceful` | 重启 `Apache httpd` 守护进程。如果未运行，它会启动 `httpd` 守护进程。 |
| `graceful-stop` 或 `apachectl -k graceful-stop` | 停止 `Apache httpd` 守护进程。 |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_630_0.png)

图 13-5：运行 `apachectl` 的配置文件测试。

## 语法

`apachectl` 命令的语法是 `apachectl` `start`/`stop`/`restart`/`status`/`configtest`。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_631_0.png)

## `httpd` 守护进程

`httpd` 守护进程是一个运行 `Apache` 服务的独立守护进程。有许多命令行选项可以与该守护进程一起使用。下表列出了部分选项。

| 选项 | 说明 |
| :--- | :--- |
| `-h` | 显示所使用的命令行选项列表。 |
| `-l` | 显示模块列表。 |
| `-L` | 显示指令及其参数列表。 |
| `-S` | 显示从配置文件解析的设置。 |
| `-t` | 为 `httpd.conf` 文件运行语法配置测试。它也用于检查 `ssl.conf` 文件的语法。 |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_631_1.png)

图 13-6：在系统上运行的 `httpd` 守护进程的 `PID`。

## 基于文本的 Web 浏览器

**定义：**

基于文本的 Web 浏览器 是一种用于在 `CLI` 模式下访问网页的应用程序。它不支持图形或图像，并且可以在彩色或单色模式下运行。该浏览器需要在系统屏幕上显示网站的 `URL`。Web 浏览器具有菜单和选项，您可以使用它们来浏览网页。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_0.png)

基于文本的 Web 浏览器

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_2.png)

网站内容

图 13-7：使用基于文本的 Web 浏览器访问网站。

## `ELinks`

`ELinks` 是一个非 `GUI`、基于文本的 Web 浏览器。它支持彩色文本显示、表格渲染、后台下载、菜单驱动的配置接口、标签页浏览和精简代码。它处理本地文件，并与 `HTTP`、`HTTPS` 和 `FTP` 等远程 `URL` 协议配合使用。`links` 命令允许您打开基于文本的 Web 浏览器。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_632_3.png)

`ELinks`

![](img/477ccb2f05b6ba1b2d563ea74f18c197_633_0.png)

## 语法

`links` 命令的语法是 `links [选项] {URL}`。

## `wget` 命令

`wget` 命令有助于从网站获取内容。它支持通过基于 `HTTP`、`HTTPS`、`FTP` 和 `TCP/IP` 的协议提取内容、递归下载、离线查看 `html` 页面以及代理。该命令是非交互式的，在缓慢和不稳定的网络连接上有效。如果由于网络问题导致下载未完成，`wget` 会自动从停止处继续下载，直到获取整个文件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_634_0.png)

图 13-9：使用 `wget` 命令检索网页。

## 语法

`wget` 命令的语法是 `wget [命令选项] http://(目的地主机名或 IP)`。

## `curl` 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_634_1.png)

`curl` 命令

`Curl` 是一个使用 `URL` 语法将数据传输到服务器或从服务器传输数据的命令行工具。它是一个在多种操作系统上运行的开源软件。它支持 `FTP`、`HTTP`、`FTPS`、`HTTPS`、`SCP`、`SFTP`、`TELNET`、`TFTP`、`LDAP`、`LDAPS`、`TFTP`、`DICT` 和 `FILE` 等协议。`Curl` 通过尝试重用以传输到同一服务器或从中传输多个文件的连接来提高文件传输速度。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_635_0.png)

图 13-10：使用 `curl` 命令下载文件。

## 语法

`curl` 命令的语法为 `curl [options] {URL...}`。

## 应用服务器

应用服务器是在连接到分布式网络的计算机上运行的服务器程序。它充分利用可跨网络访问的应用程序。应用服务器使自定义应用程序可供多个并发用户使用。它也可用于开发、运行和管理应用程序。它由三层组成：第一层图形用户界面（`GUI`），中间层业务逻辑，以及第三层数据库和事务服务器。

## `Tomcat`

`Tomcat` 是一个开源的应用服务器，实现了 `Java` 序列化（`servlet`）并渲染 `JavaServer` 页面。它为 `Java` 代码在 `Linux` 系统上运行提供了 `Java HTTP` web 服务器环境。`Tomcat` 可以响应用户请求运行程序，并将动态结果发送给用户。`Tomcat` 拥有内部 web 服务器，在运行多个应用程序时非常有用。它可以与 `Apache`、`Sun Java System Web Server` 和 `Microsoft Internet Information Server` 等其他 web 服务器配合使用。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_636_0.png)

图 13-11：`Linux` 系统上的 `Tomcat` 应用程序主页。

## `Java` 序列化

`Java` 序列化（`Java Servlet`）是开发为组件并可在服务器上运行的 `Java` 对象文件。由于序列化是 `Java` 程序，它允许你在 web 应用程序中充分利用 `Java` 的强大功能。它允许你访问 `Java` 类库函数，例如网络连接和数据库访问。序列化是一个组件，可以从 `HTML`、`Java Server Page` 或另一个序列化中调用。由于 `Java` 序列化可以从 `HTML` 文档中调用，它为 `HTML` 页面提供了强大的服务器端处理能力。

## 容器

容器，也称为 web 引擎或 web 容器，是一种支持序列化执行的特殊 web 服务器。它将 web 服务器的基本功能与 `Java` 特定的优化和扩展相结合。它将特定的 `URL` 转换为序列化请求。容器包含已注册序列化的功能和 `URL` 等信息。这些信息用于唯一标识序列化并将服务请求分发给适当的序列化。可以向容器添加或移除序列化，而不影响正在运行的序列化。`Tomcat` 是序列化容器的一个示例。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_636_1.png)

## 如何配置 Web 服务器

### 操作参考：安装 `Apache`

要安装 `Apache`：

1. 以 `root` 身份登录。
2. 挂载包含 `Apache` 的 `Linux` 安装介质。
3. 导航到 `/media/name of the media/Server` 目录。
4. 安装 `Apache` 的依赖包。
   - a. 输入 `rpm -ivh apr-(version).(release).rpm`。
   - b. 输入 `rpm -ivh postgresql-libs-(version).(release).rpm`。
   - c. 输入 `rpm -ivh apr-util-(version).(release).rpm`。
5. 输入 `rpm -ivh httpd-(version).(release).rpm` 以安装 `Apache`。
6. 输入 `rpm -qi httpd` 以验证 `Apache` 是否已安装。
7. 如有必要，输入 `umount /media/cdrom` 以卸载安装 `CD`。

### 操作参考：配置 `Apache` Web 服务器

要配置 `Apache` web 服务器：

1. 以 `root` 身份登录。
2. 使用 `vi` 编辑器打开 `httpd.conf` 文件。
   - 当通过 `RPM` 安装 `Apache` 时，从 `/etc/httpd/conf` 目录打开 `httpd.conf` 文件。
   - 当从用户源安装 `Apache` 时，从 `[/Installation Directory]/conf` 目录打开 `httpd.conf` 文件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_637_0.png)

3. 找到 `ServerAdmin` 语句并输入网站管理员的电子邮件地址。
   ```
   ServerAdmin (email address)
   ```
4. 找到 `ServerName` 选项，然后输入 web 服务器的 `IP` 地址。
   ```
   ServerName (IP address: Port)
   ```
5. 找到 `DocumentRoot` 选项并输入用于提供 web 内容目录的路径。
   ```
   DocumentRoot (Absolute path of the web content directory)
   ```
6. 找到 `DirectoryIndex` 选项并输入目录的索引文件列表。
   ```
   DirectoryIndex (List of index files)
   ```
7. 保存并关闭文件。
8. 输入 `service httpd start` 以启动 `httpd` 服务使配置更改生效。
9. 输入 `chkconfig httpd on` 以在系统启动时启用 `httpd` 服务。

如果你想为主机名使用 web 服务器，请更新 `DNS` 区域文件。

### 操作参考：调整 `Apache` 服务器

要调整 `Apache` 服务器：

1. 以 `root` 身份登录。
2. 使用 `vi` 编辑器打开 `/etc/httpd/httpd.conf` 文件。
3. 设置 `Apache` 配置以调整服务器。
   - 找到 `MaxKeepAliveRequests` 指令并指定允许的最大请求数。
   - 找到 `StartServers` 指令并设置初始服务器进程数。
   - 找到 `MinSpareServers` 指令并指定备用服务器的最小数量。
   - 找到 `MaxSpareServers` 指令并指定备用服务器的最大数量。
   - 找到 `MaxClients` 指令并指定并行运行的最大客户端连接数。
   - 找到 `KeepAlive` 指令并将其设置为 `On` 或 `Off` 以允许或阻止每个连接超过一个请求。
   - 找到 `KeepAliveTimeout` 指令并指定请求相对于连接的时间限制。
4. 保存并关闭文件。
5. 输入 `service httpd configtest` 以测试配置文件。
6. 输入 `service httpd restart` 以重启 `httpd` 服务使配置更改生效。

### 操作参考：配置 `Apache` 命名空间

要配置 `Apache` 命名空间：

1. 以 `root` 身份登录。
2. 使用 `vi` 编辑器打开 `/etc/httpd/conf/httpd.conf` 文件。
3. 找到 `UserDir` 选项并取消注释该行，以允许用户为他们的 web 内容分配单独的空间。
4. 取消注释为主目录定义的目录部分，以控制对 `UserDir` 目录的访问。

```apache
<Directory /home/user_name/public_html>

  AllowOverride FileInfo AuthConfig Limit

  Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec

  <Limit GET POST OPTIONS>

    Order allow,deny

    Allow from all

  </Limit>

  <LimitExcept GET POST OPTIONS>

    Order deny,allow

    Deny from all

  </LimitExcept>

</Directory>
```
