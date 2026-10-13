
通过这种方式，`http`进程首先读取 `deny` 行（拒绝所有访问），然后按照 `allow` 行中的说明处理所有异常。

# Apache 日志文件

为了帮助你排查 Apache 问题，默认使用两个日志文件。你可以在 `/var/log/httpd` 目录下找到这些文件。`access_log` 文件包含访问你服务器的用户信息。注意，在繁忙的 Web 服务器上，它的增长速度非常快！`error_log` 文件包含错误消息，对于排查你的 Apache 服务器非常有用。

# Apache 和 SELinux

作为管理员，SELinux 往往会令人困扰。这是因为它以非常严格的方式定义了什么是允许的，什么是不允许的。此外，如果发生了任何策略中未明确允许的操作，SELinux 都会拒绝它。你已经在练习 8.6 中学习了这一点。

为了确保在 SELinux 环境下运行顺畅，有几点需要处理。首先，你需要确保已应用适当的上下文类型（context types）。通常，在 Apache 可以访问文档的目录上使用 `httpd_sys_content_t`，在 Apache 需要脚本的目录上使用 `httpd_sys_script_exec_t`。但也提供其他上下文类型。以下是为 `httpd` 定义的上下文类型：

- `httpd_sys_content_t`：设置在 `httpd` 进程可以访问的目录上。
- `httpd_sys_script_exec_t`：设置在允许 `httpd` 进程运行脚本的目录下。
- `httpd_sys_rw_content_t`：如果你想从 `httpd` 进程运行脚本并允许将结果数据写入目录，则此上下文有用。
- `httpd_sys_ra_content_t`：使用此允许脚本附加到现有文件。
- `httpd_unconfined_exec_t`：使用此允许脚本在没有 SELinux 保护的情况下运行。仅在其他方法都无效时才将其作为最后手段！
- `public_content_t`：使用此允许 `httpd` 进程以及其他服务（如 Samba 和 NFS）访问目录。
- `public_rw_t`：使用此允许对目录进行共享读写访问。

要更改策略中的上下文类型，可以使用 `semanage fcontext` 命令。例如，使用 `semanage fcontext -a -t httpd_sys_content_t "/www/(.*)"` 为指定的上下文类型标记 `/www` 目录。接下来使用 `restore -r` 将新上下文应用到文件系统。

除了可用于 Apache 的上下文类型外，Apache 还有许多布尔值（Booleans），以及特定功能的开关控制。使用 `getseboolean -a | grep httpd` 获取 `httpd` 所有可用的布尔值列表。或者，你可以阅读 `httpd_selinux` 页面获取关于 Apache SELinux 的特定信息。`semanage Boolean -l` 命令将产生所有布尔值简洁简短的描述。在练习 16.2 中，你将为 Apache 配置 SELinux。

## 练习 16.2

### 为 Apache 配置 SELinux

在此练习中，你将在不同的端口上运行 Apache。SELinux 会拒绝此操作，但你将应用适当的修复以确保 Apache 监听该端口。

- 1. 打开一个 `root` shell。将文件 `/etc/httpd/conf/httpd.conf` 复制到 `httpd.conf.bak`，这允许你以后恢复到原始状态。
- 2. 用编辑器打开 `/etc/httpd/conf/httpd.conf` 文件。
- 3. 使用参数 `Listen 80` 并将其更改为 `Listen 888`。保存更改并使用 `service httpd` 重启 `httpd` 进程。它会给你一个错误消息。
- 4. 使用 `tail -f /var/log/messages` 读取 Apache 尝试在端口 888 上启动时写入的日志消息。如果你没有看到

# 使用虚拟主机

```
DocumentRoot /www/docs/dummy-host.example.com

ServerName dummy-host.example.com

ErrorLog logs/dummy-host.example.com-error_log

CustomLog logs/dummy-host.example.com-access_log common

</VirtualHost>
```

列表 16.2 中的示例定义了虚拟主机应该监听的端口。该端口设置为 `*:80`，这意味着它可以在此机器上 80 端口的任何 IP 地址可用。接下来，使用 `ServerAdmin` 指令来告诉用户，如果他们需要联系此 Web 服务器的管理员，应该联系谁。

在定义虚拟主机时，你使用的最重要的参数是针对该虚拟主机的特定。在这个示例中，使用了 `/www` 下的 `DocumentRoot`，这意味着你还需要设置适当的 SELinux 类型。接下来指定了 `ServerName`，配置的最后一部分是为该虚拟主机定义的专用日志文件。

![](img/3a7e027360b64bc83d5cf9a2db902251_426_0.png)

在设置虚拟主机时，你应该意识到一点：要么将所有内容都配置为虚拟主机，要么不配置。这意味着如果你在一个同样有普通主机定义的 Apache 服务器上设置了虚拟主机，那么在安装虚拟主机后，普通主机定义将会失效。

在配置虚拟主机时，你应该考虑在 `/etc/httpd/conf.d` 为虚拟主机创建独立的 `.conf` 文件。使用独立的 `.conf` 文件会让虚拟主机管理更容易，特别是如果你计划创建许多虚拟主机。在练习 16.4 中，你将学习如何设置两个虚拟主机。

# 练习 16.4

## 配置虚拟主机

在此练习中，你将创建两个虚拟主机。在设置虚拟主机之前，你将首先设置名称解析。之后，你将创建虚拟主机配置。你还需要更改 SELinux 配置以使之正常工作。在此练习中，你将同时使用计算机和虚拟机。

- 1. 在你的主机计算机上，用编辑器打开 `/etc/httpd/conf.d` 文件，并添加两行，以便将你要创建的虚拟主机名称解析到虚拟机的 IP 地址。
- 2. 在虚拟机上，打开 `root` shell，并在 `/etc/httpd/conf.d` 目录下创建一个名为 `server1.example.com.conf` 的配置文件。赋予其以下内容：

```
<VirtualHost *:80>

  ServerAdmin webmaster@server1.example.com
```

# 练习 16.4（继续）

```
DocumentRoot /www/docs/server1.example.com

ServerName server1.example.com

ErrorLog logs/server1/example-error_log

CustomLog logs/server1.example.com-access_log

</VirtualHost>
```
