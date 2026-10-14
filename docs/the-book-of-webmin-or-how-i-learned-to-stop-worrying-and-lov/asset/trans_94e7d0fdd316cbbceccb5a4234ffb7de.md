

## 完成并缓存传输后

如果在传输完成前但在已接收到对象此百分比之后取消了传输，Apache 将继续获取对象以缓存完整对象。在此处输入 0 将使用默认值，而 100 则表示除非整个传输完成，否则不会存储对象。建议使用 60 到 90 之间的数字。此选项配置 CacheForceCompletion [http://httpd.apache.org/docs/mod/mod_proxy.html#cacheforcecompletion]，默认值为 90。

## 缓存垃圾回收间隔

如果已配置此项，Apache 将执行周期性垃圾回收，即当缓存对象占用的空间大于配置的 Cache 大小时删除文件。此选项接受浮点值，因此例如可以通过在此处输入 0.5 来配置每 30 分钟执行一次垃圾回收。如果未设置此项，缓存将无限增长。此选项配置 CacheGcInterval [http://httpd.apache.org/docs/mod/mod_proxy.html#cachegcinterval]，默认值为 none。

## 缓存文件过期时间因子

如果源 HTTP 服务器未为对象提供过期时间，Apache 可以通过将上次修改时间乘以此因子来估算。此选项配置 CacheLastModifiedFactor [http://httpd.apache.org/docs/mod/mod_proxy.html#cachelastmodifiedfactor] 指令，默认值为 0.1。

## 缓存文件最大过期时间

在对象存储此小时数之后，即使源服务器提供的过期时间尚未到达，Apache 也会向源服务器检查新内容。此选项配置 CacheMaxExpire [http://httpd.apache.org/docs/mod/mod_proxy.html#cachemaxexpire] 指令，默认值为 24 小时。

## 缓存大小

假设已配置垃圾回收，Apache 将限制缓存对象存储目录的大小为此千字节数。此选项对应于 CacheSize [http://httpd.apache.org/docs/mod/mod_proxy.html#cachesize] 指令，默认值为 5 KB。

## 服务器配置

此页面允许您重新配置虚拟服务器的基本配置细节。例如，如果您在创建虚拟服务器时将其放在 8080 端口进行测试，但现在想将其移至 80 端口用于生产，您可以在此处执行该更新。

## 地址和端口

如果您的系统具有多个接口，Apache 默认将在所有接口上监听 80 端口。但是，您可以使用此选项将虚拟服务器配置为仅在一个地址上响应。您也可以在此处配置不同的端口。

## 文档根目录

这是根目录，从此开始访问服务器上对象的路径。此选项配置 DocumentRoot [http://httpd.apache.org/docs/mod/core.html#documentroot] 指令。

## 服务器名称

在使用基于名称的虚拟服务器时，此名称应与服务器应响应的名称相匹配。这也用于创建重定向 URL。如果未指定，Apache 将尝试从 IP 地址推断，这并不总是可靠的。此选项对应于 ServerName [http://httpd.apache.org/docs/mod/core.html#servername] 指令。

## 教程：一个基本的 Apache 配置

Apache 是一个极其庞大且功能丰富的软件。初次接触可能会令人望而生畏。幸运的是，只要谨慎操作并注意与您的安装和环境相关的文档，安装、配置和维护都非常容易。Apache 的安装在此未涵盖，因为它在 Apache 网站上有完善的文档，并且您的操作系统供应商很可能提供合适的软件包以实现自动安装。这里将涵盖的是设置 Apache 以提供 HTML 网页的初始障碍。下一节将把配置更进一步，配置虚拟主机服务。稍后，BIND 模块章节中的一个部分将涵盖为您的 Web 服务器添加 /usr/w 服务。

## 配置 Apache 路径

> **NOTE** *如果您是从操作系统供应商的软件包安装 Apache，或者供应商未提供软件包并且它已安装在程序选择的默认位置，您可以跳过本节并继续到下一节，介绍初始模块选择。对于任何受支持的操作系统，Webmin 都有一个配置文件，其中包含其管理的程序的合理默认路径。这些配置假定安装在您操作系统的默认位置。因此，例如，在 Red Hat Linux 系统上，Webmin 会期望 httpd.conf 文件位于 /etc/httpd/conf 目录中，而在 Solaris 上则期望位于 /usr/local/apache/conf。*

Webmin 直接使用 Apache 配置文件，因此必须知道在哪里找到它们。当您第一次浏览到 Webmin 的 Apache 模块时，您可能会收到一个错误，提示找不到配置文件。您需要找到配置文件，以及 Apache 二进制文件，以及系统上可能的启动和关闭脚本，并配置 Webmin 在适当的位置搜索。最重要的路径可能是 Apache 服务器根目录和 httpd 可执行文件的路径。

## 模块选择

Apache 极其模块化，其绝大多数可用功能都被分解为可在运行时根据运行环境的需求加载的小模块。Webmin 需要了解可用于您的 Apache 的模块，以便为可用的选项提供配置选项并隐藏不可用的选项。因此，您第一次访问 Webmin Apache 模块时，会看到一个 Apache 模块列表，并在其旁边有复选框。如果您使用的是软件包或默认的 Apache 源安装，您只需单击 Configure 即可。如果您从头开始构建 Apache 并进行了自定义，则需要选择您在安装中提供的模块，然后单击 Configure。

## 添加内容

信不信由你，我们现在几乎准备好使用 Apache 提供内容了。一旦您到达 Webmin 中的主 Apache 模块页面，您将看到一组全局服务器选项的图标，以及一个标记为 Default server 的单个虚拟服务器配置部分。默认服务器是当没有其他虚拟服务器响应时将回答请求的服务器。由于我们系统上尚未配置任何虚拟服务器，默认服务器将回答到达我们机器的所有 HTTP 请求。请注意 Document root 字段中的路径，因为我们将把第一个网页放在那里。

在我系统上，默认服务器的 Document root 是 /var/www/html，该目录是在安装过程中自动创建的。因此我将创建一个名为 index.html 的网页并将其放入该目录，确保该页面具有允许 Apache 进程读取它的权限。名称 index.html 很重要，您必须使用正确的默认页面文件名，否则 Apache 不会在 URL 地址后未指定文件的情况下提供它。索引页面的其他常见名称是 index.htm 和 default.htm。

## 启动 Apache

现在剩下要做的就是启动您的 Apache 服务器。假设 Webmin 已为您的安装正确配置，它甚至可以从 Webmin 中通过单击按钮启动。只需浏览到 Apache 模块主页面，然后单击页面右上角的 Start Apache 链接即可。

要测试您的新网站，请使用您喜欢的浏览器浏览到服务器所在的 IP。例如，我的测试服务器位于 IP 192.168.1.1，因此我将在浏览器 URL 字段中输入 http://192.168.1.1。假设一切顺利，您将看到您的新网页。

