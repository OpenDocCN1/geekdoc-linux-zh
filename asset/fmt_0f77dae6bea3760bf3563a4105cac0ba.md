
# ScoreBoardFile：用于存储内部服务器进程信息的文件。

并非所有架构都需要此文件。但如果需要（当您运行 Apache 时创建此文件您就会知道），
则**必须**确保两个 Apache 调用实例不共享同一个 scoreboard 文件。

`ScoreBoardFile` `/var/run/httpd.scoreboard`

在标准配置中，服务器将按顺序处理此文件、`srm.conf` 和 `access.conf`。
后两个文件现在分发时为空，因为建议将所有指令保留在单个文件中以简化配置。
下面注释掉的值是其内置默认值。您可以使用 `"/dev/null"`（用于 Unix）或
`"nul"`（用于 Win32）作为这些指令的参数，从而让服务器完全忽略这些文件。

`#ResourceConfig conf/srm.conf`
`#AccessConfig conf/access.conf`

### Timeout：接收和发送超时前的秒数。

`Timeout` `300`

### KeepAlive：是否允许持久连接（每个连接超过一个请求）。

设置为 `"Off"` 可禁用。

`KeepAlive` `On`

### MaxKeepAliveRequests：允许在持久连接期间处理的最大请求数。

设置为 `0` 表示允许无限数量。
建议将此数字保持较高，以获得最佳性能。

`MaxKeepAliveRequests` `100`

### KeepAliveTimeout：在同一连接上等待同一客户端下一个请求的秒数。

`KeepAliveTimeout` `15`

### 服务器池大小调节

无需猜测需要多少个服务器进程，Apache 会根据其观察到的负载动态适应……
即，它试图维持足够的服务器进程来处理当前负载，外加一些备用服务器来处理瞬时的
负载峰值（例如，单个 Netscape 浏览器发出的多个同时请求）。

它通过定期检查有多少服务器在等待请求来实现这一点。如果少于 `MinSpareServers`，
它会创建一个新的备用服务器。如果多于 `MaxSpareServers`，部分备用服务器会终止。
默认值对于大多数站点可能已经足够。

`MinSpareServers` `5`
`MaxSpareServers` `20`

初始启动的服务器数量——应为一个合理的近似值。

`StartServers` `8`

正在运行的服务器总数限制，即限制可以同时连接的客户端数量……
如果达到此限制，客户端将被**锁定在外**，因此**不应**设置得太低。
它主要旨在作为刹车，防止失控的服务器在系统崩溃时拖垮系统……

`MaxClients` `150`

### MaxRequestsPerChild

每个子进程允许处理的请求数，之后子进程将终止。
子进程退出是为了避免在长期运行后出现问题，当 Apache（以及它可能使用的库）
泄漏内存或其他资源时。在大多数系统上，这实际上并不需要，但少数系统
（如 Solaris）的库中确实存在明显的泄漏。对于这些平台，设置为类似 `10000`
的值；设置为 `0` 表示无限制。

注意：此值不包括初始请求之后的 keepalive 请求。例如，如果一个子进程处理
一个初始请求和 10 个后续的 "keepalive" 请求，它仅算作此限制下的 1 个请求。

`MaxRequestsPerChild` `100`

### Listen

允许您除了默认端口外，将 Apache 绑定到特定的 IP 地址和/或端口。
另请参阅 `<VirtualHost>` 指令。

`#Listen 3000`
`#Listen 12.34.56.78:80`
`Listen` `80`

### BindAddress

您可以使用此选项支持虚拟主机。此指令用于告诉服务器监听哪些 IP 地址。
它可以包含 `"*"`, 一个 IP 地址或一个完全合格的互联网域名。
另请参阅 `<VirtualHost>` 和 `Listen` 指令。

`#BindAddress *`

### 动态共享对象 (DSO) 支持

若要使用作为 DSO 构建的模块的功能，您必须在此处放置相应的 '`LoadModule`'
行，以便其中包含的指令在实际使用前可用。请阅读 Apache 1.3 发行版中的
`README.DSO` 文件，了解有关 DSO 机制的更多详细信息，并运行 '`httpd -l`'
查看您的 `httpd` 二进制文件中已内置（静态链接且始终可用）的模块列表。

注意：模块加载顺序很重要。未经专家建议，请勿更改以下顺序。

示例：
`# LoadModule foo_module modules/mod_foo.so`

```
#LoadModule mmap_static_module    modules/mod_mmap_static.so
LoadModule vhost_alias_module     modules/mod_alias.so
LoadModule env_module             modules/mod_env.so
LoadModule config_log_module      modules/mod_log_config.so
LoadModule agent_log_module      modules/mod_log_agent.so
LoadModule referer_log_module    modules/mod_log_referer.so
#LoadModule mime_magic_module    modules/mod_mime_magic.so
LoadModule mime_module            modules/mod_mime.so
LoadModule negotiation_module    modules/mod_negotiation.so
LoadModule status_module          modules/mod_status.so
LoadModule info_module            modules/mod_info.so
LoadModule includes_module        modules/mod_include.so
LoadModule autoindex_module       modules/mod_autoindex.so
LoadModule dir_module             modules/mod_dir.so
LoadModule cgi_module             modules/mod_cgi.so
LoadModule asis_module            modules/mod_asis.so
LoadModule imap_module            modules/mod_imap.so
LoadModule action_module          modules/mod_actions.so
#LoadModule speling_module       modules/mod_speling.so
LoadModule userdir_module         modules/mod_userdir.so
LoadModule aliases_module         modules/mod_aliases.so
LoadModule rewrite_module         modules/mod_rewrite.so
LoadModule access_module          modules/mod_access.so
#LoadModule auth_module           modules/mod_auth.so
#LoadModule anon_auth_module      modules/mod_auth_anon.so
#LoadModule db_auth_module        modules/mod_auth_db.so
#LoadModule digest_module         modules/mod_digest.so
#LoadModule proxy_module          modules/libproxy.so
#LoadModule cern_meta_module      modules/mod_cern_meta.so
LoadModule expires_module         modules/mod_expires.so
LoadModule headers_module         modules/mod_headers.so
#LoadModule usertrack_module     modules/mod_usertrack.so
#LoadModule example_module       modules/mod_example.so
```
