
### 虚拟主机配置示例

```
ErrorLog /pfr/logs/error_log      # 你的选择

TransferLog /pfr/logs/access_log      # 事务日志

ScriptAlias /cgi/ /pfr/cgi-bin      # 将虚拟目录与真实目录关联

<Directory /pfr/html>               # 文档根

    Options ExecCGI Indexes Includes      # 上述描述

</Directory>

</VirtualHost>
```

要测试你新的虚拟主机设置，你可以使用以下脚本请求重启 Apache Web 服务器：

```bash
[root@notebook /root]# /etc/rc.d/init.d/httpd restart
```

现在，你应该能够使用任何浏览器检查所有虚拟站的 Web 内容页面了。你应该为每个虚拟主机创建一个特定性合适的 `index.html` 页面。

一旦你创建了一个虚拟主机，即使是本地主机也必须变为虚拟的，否则它就会消失。在所有其他虚拟主机条目之前，但在 `NameVirtualHost` 行之后，为 `localhost` 或你的本地 Web 名称创建另一个条目，如图 8-14 所示。

Apache 管理是任何 Linux 系统管理员的必备技能。你应该培养快速安装、配置和排除 Apache 故障的能力。你还应该能够设置和自定义虚拟网站，这将让你成为一个更高效的 Webmaster。你可以通过后续练习来测试你的技能。

![](img/af9747d0cc5d061c585d6aea0a227a74_494_0.png)

===================================================

```
NameVirtualHost 127.0.0.1

<VirtualHost 127.0.0.1>

ServerName localhost

ServerAdmin root@localhost

DocumentRoot /home/httpd/html/

ErrorLog /error_log

TransferLog /access_log

<Directory /home/httpd/html>

    Options ExecCGI Indexes Includes

</Directory>

</VirtualHost>
```
====================================================
