
- 1. 在 Squid 服务器上重新启动 `squid` 守护进程。方法是重新启动计算机或输入 `/etc/rc.d/init.d/squid restart`。（如果 `squid` 未运行，则使用 `restart`。）

- 2. 在 Squid 服务器上重新启动 Internet 连接（如果尚未启用）。

- 3. 在您网络中的客户机上，设置 Netscape（或其他 Web 浏览器）使用 Squid 服务器作为代理服务器（本章后文有说明）。（在 Netscape 中，进入 `Preferences` `高级` ⇨ `代理设置`，选择手动代理，并添加 Squid 服务器的主机名，默认端口 `3128`。）

- 4. 在客户机上，使用您刚才配置的浏览器打开 Internet 上的任何网页。

如果网页未显示，请参阅调试 `Squid` 的章节，获取解决问题的建议。

### 修改 Squid 配置文件

如果您想为 `Squid` 创建更复杂的访问权限设置，应从默认的 `squid.conf` 配置文件开始（以替换前面展示的 `quickstart` 示例）。如果您已经修改了 `squid.conf` 文件，请先将其复制一份，然后将 `/etc/squid.d/squid.conf.default` 复制到 `/etc/squid/squid.conf`。

**注意**

首先，以 `root` 用户打开 `/etc/squid.d/squid.conf` 文件。您将看到大量关于可以在该文件中设置的值的说明。总体而言，大多数需要配置 `Squid` 的标签都是用于设置缓存和代理主机对您代理服务器的访问。

**注意**

不要修改 `squid.conf.default` 文件！如果您真的弄乱了 `squid.conf` 文件，可以通过再次将此文件复制为 `squid.conf` 来重新开始。如果您想确切回顾已做出的更改，请在 `/etc/squid.d` 目录中输入以下命令：

```
diff squid.conf squid.conf.default | more
```

### 在 squid.conf 中配置访问控制

为了防止任何人使用您的计算资源，`Squid` 要求您定义哪些主机可以访问您的 HTTP（Web 浏览）服务。默认情况下，除本地主机外，所有主机都被拒绝访问 `Squid` HTTP 服务。使用 `acl` 标签，您可以创建访问列表。然后，使用 `http_access` 标签，可以为您创建的访问列表授权访问 HTTP（Web）服务。

访问控制列表标签（`acl`）的形式为：

```
acl name type string
acl name type file
```

名称是您想为列表分配的任何名称。`string` 是一段文本，`file` 是适用于特定 `acl` 类型的信息文件。有效的 `acl` 类型包括 `dst`、`src`、`dstdomain`、`sdomain`、`url_path_pattern`、`url_pattern`、`time`、`port`、`proto`、`method`、`browser` 和 `user`。
