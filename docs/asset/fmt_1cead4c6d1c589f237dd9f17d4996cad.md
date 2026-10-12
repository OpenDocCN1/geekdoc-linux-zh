
# `*`、一个 IP 地址或完全限定的 Internet 域名。另见 `<VirtualHost>` 和 `Listen` 指令。

# 716 第 42 章 • 万维网服务

# `BindAddress *`

### 动态共享对象 (DSO) 支持

为了能够使用作为 DSO 构建的模块的功能，你必须在此位置放置相应的 `LoadModule` 行，以便其中包含的指令在我们使用之前实际上可用。请阅读 Apache 1.3 分发版中的 `README.DSO` 文件，以获取有关 DSO 机制的更多信息，并运行 `httpd -t` 获取你的 httpd 二进制文件中已内置的（静态链接，因此始终可用）模块列表。

注意：模块加载的顺序是重要的。在没有专家建议的情况下，不要更改顺序。

示例：

```
#LoadModule foo_module modules/mod_foo.so
#LoadModule mmap_static_module modules/mod_mmap_static.so
#LoadModule host_alias_module modules/mod_host_alias.so
#LoadModule env_module modules/mod_env.so
#LoadModule config_log_module modules/mod_log_config.so
#LoadModule agent_log_module modules/mod_agent_log.so
#LoadModule referer_log_module modules/mod_log_referer.so
#LoadModule mime_magic_module modules/mod_mime_magic.so
#LoadModule mime_module modules/mod_mime.so
#LoadModule negotiation_module modules/mod_negotiation.so
#LoadModule status_module modules/mod_status.so
#LoadModule info_module modules/mod_info.so
#LoadModule include_module modules/mod_include.so
#LoadModule autoindex_module modules/mod_autoindex.so
#LoadModule dir_module modules/mod_dir.so
#LoadModule cgi_module modules/mod_cgi.so
#LoadModule alias_module modules/mod_alias.so
#LoadModule imap_module modules/mod_imap.so
#LoadModule action_module modules/mod_action.so
#LoadModule speling_module modules/mod_speling.so
#LoadModule userdir_module modules/mod_userdir.so
#LoadModule alias_module modules/mod_alias.so
#LoadModule rewrite_module modules/mod_rewrite.so
```

# 配置 Apache 717
