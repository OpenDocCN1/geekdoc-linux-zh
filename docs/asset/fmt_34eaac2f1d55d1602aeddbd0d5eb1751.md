
`path` 属性指定了 URL 中用于名为 `myapp` 的 `servlet` 的路径。`docBase` 属性指定了查找此 `servlet` 的路径。这可以是绝对路径，也可以是相对于 Tomcat 上下文管理器（默认为 `$TOMCAT_HOME/webapps`）的路径。`debug` 属性指定了调试日志消息的级别，而 `reloadable` 属性指定了当 `servlet` 发生变化时，Tomcat 是否会自动重新加载它。

## 2. 重启 Tomcat

使用 `/usr/bin/tomcat stop ; /usr/bin/tomcat start` 命令停止并重启 Tomcat。这将生成一个新的 `/var/tomcat/conf/mod_jk.conf.auto` 文件，其中应包含以下配置段：

```apache
Alias /myapp "/var/tomcat/webapps/myapp"

<Directory "/var/tomcat/webapps/myapp">
    Options Indexes FollowSymLinks
</Directory>

JkMount /myapp/servlet/* ajp12
JkMount /myapp/*.jsp ajp12

<Location "/myapp/WEB-INF/">
    AllowOverride None
    deny from all
</Location>

<Location "/myapp/META-INF/">
    AllowOverride None
    deny from all
</Location>
```
