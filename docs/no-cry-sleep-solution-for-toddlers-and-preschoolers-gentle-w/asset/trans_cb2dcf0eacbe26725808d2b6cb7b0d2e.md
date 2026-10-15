

你的 Web 页面的主目录。ServerRoot 指令指定了你的 Web 服务器配置、错误和日志文件存放的位置。

```
DocumentRoot /var/www/html
ServerRoot /etc/httpd
```

MaxClients 指令设置同时可以连接到你的服务器的客户端的最大数量。

```
MaxClients 150
```

> 注意 你还可以将 Apache 配置为仅作为代理和/或缓存服务器运行。默认的代理和缓存服务器指令已包含在 httpd.conf 文件中。ProxyRequests 指令打开代理活动。缓存可以通过诸如 CacheRoot 指定缓存目录、CacheSize 指定缓存大小（默认 500KB）以及 CacheMaxExpire 设置未修改文档的时间限制等指令进行配置。

## 目录级配置：.htaccess 和 <Directory>

Apache 最灵活的方面之一是其能够配置单个目录的能力。通过 Directory 指令，你可以定义一组仅适用于特定目录的指令。Directory 指令列在表 22-5 中。此类指令可以放在 httpd.conf 或 access.conf 配置文件中。你还可以在特定目录中使用 .htaccess 文件来保存配置指令。然后这些指令仅应用于该目录。名称 “.htaccess” 实际上是通过 AccessFileName 指令设置的。你可以按需更改它。

```
AccessFileName .htaccess
```

| Directive | Description |
|---|---|
| AccessFileName filename filename ... | 默认的目录配置文件名位于目录内。 |
| <Directory directory> ... </Directory> | <Directory> 和 </Directory> 指令作为标签操作，用来包含一组仅适用于指定目录及其子目录的指令。 |
| <DirectoryMatch regex> ... </DirectoryMatch> | <DirectoryMatch> 和 </DirectoryMatch> 包含一组仅适用于指定目录的指令。其操作与 <Directory> 相同，但接受正则表达式作为参数。 |
| DirectoryIndex local-url local-url ... | 指定当客户端请求目录索引时要查找的资源列表，通常是在目录名称末尾指定 / 时（通常为 index.html）。 |

TABLE 22-5 Directory Directives

| Directive | Description |
|---|---|
| Options [+|-]option [+|-]option ... | 控制特定目录中可用的服务器功能。OPTIONS None 如果设置为 None，则不启用任何额外功能。All 除 MultiViews 外的所有选项。这是默认设置。ExecCGI 允许执行 CGI 脚本。FollowSymLinks 服务器在此目录中跟随符号链接。Includes 允许服务器端包含。IncludesNOEXEC 允许服务器端包含，但禁用 #exec 命令和 CGI 脚本的 #include。Indexes 对于没有 DirectoryIndex 的目录，返回格式化的目录列表。MultiViews 允许内容协商 MultiViews。SymLinksIfOwnerMatch 服务器仅跟随目标文件或目录与链接拥有相同用户 ID 的符号链接。 |
| AllowOverride override override ... | 可以由 .htaccess 文件中的条目覆盖的指令。All 允许覆盖，none 禁止覆盖。默认：AllowOverride All 上下文：directory |

# TABLE 22-5 Directory Directives (continued)

Directory 块以 <Directory pathname> 指令开始，其中 pathname 是要配置的目录。结束指令使用相同的 <> 符号，但在单词 "Directory" 前加上斜杠：</Directory>。放置在此块内的指令仅适用于指定的目录。以下示例拒绝来自 www.myvids.com 的对 mypics 目录的访问请求。

```
<Directory /var/www/html/mypics>
Order Deny,Allow
Deny from www.myvids.com
</Directory>
```

使用 Options 指令，你可以在目录中启用某些功能，例如使用符号链接、自动索引、执行 CGI 脚本和内容协商。默认是 All 选项，它打开除内容协商（MultiViews）外的所有功能。以下示例启用自动索引（Indexes）、符号链接（FollowSymLinks）和内容协商（MultiViews）。

```
Options Indexes FollowSymLinks Multiviews
```

