
# 配置并启动 NIS 客户端守护进程

NIS 守护进程 `ypbind` 使用配置文件 `/etc/yp.conf` 来读取客户端所在域内的 NIS 服务器列表。`/etc/yp.conf` 指定了你应该使用的 NIS 服务器客户端，以及如何找到它们。服务器将此过程定义为绑定客户端。可以通过向 `/etc/yp.conf` 文件中添加以下条目来设置：

```
domain developers.com server linuxser
```

上述条目指定了客户端如何使用 `linuxser` 服务器。
要对 NIS 域进行广播查询，你可以在 `/etc/yp.conf` 文件中添加以下条目：

```
domain developers.com broadcast
```

将服务器与 NIS 域关联，以便客户端连接到同一域的多个服务器。`/etc/yp.conf` 文件中的以下条目可以启用此功能：

```
domain developers.com server linuxser
```

你可以根据设置添加任何其他服务器或域。前面的示例识别了用于 `developers.com` 域的服务器。
作为另一种选择，你可以使用 `authconf` 命令并为配置客户端提供 NIS 域名名和 NIS 服务器名称。

## 测试客户端

NIS 客户端需要 RPC 才能正常工作。因此，在启动 `ypbind` 守护进程之前，请确保 `portmapper` 正在运行。你可以在 shell 提示符处执行以下命令来确保：

```
# rpcinfo -p <client name>
```

在上述命令中，将 `<client name>` 参数指定为 NIS 客户端的 IP 地址或主机名。在 NIS 客户端的 shell 提示符处执行以下命令启动主客户端守护进程 `ypbind`：

```
# service ypbind
```

执行以下命令确认 `ypbind` 正在运行：编辑 `/etc/host.conf` 文件并按如下所示修改顺序条目：

```
# rpcinfo -u linuxpc1 ypbind
order hosts, bind
```
上述条目指定使用 NIS 用于主机名查找。

4. 配置客户端启动文件以使用 NIS：使用 `chkconfig` 使 `ypbind` 在启动时启动。要启用此项，请在 shell 提示符处执行以下命令：

```
# chkconfig --levels 345 ypbind on
```

5. 重启客户端：重启服务器以确保客户端守护进程启动。

假设你已经在 `softdevelopers.com` 域的 `linuxuser` 节点上配置了 NIS 服务器。现在你必须将 `linuxpc1` 配置为 NIS 客户端。执行以下步骤将 `linuxpc1` 配置为 NIS 客户端：

# 设置 NIS 域名名

按照上一节中配置 NIS 服务器的方法，设置 NIS 域名名如下：

```
# NISDOMAIN=softdevelopers.com
```

# 配置并启动 NIS 客户端守护进程

NIS 守护进程 `ypbind` 使用配置文件 `/etc/yp.conf` 来读取客户端所在域内的 NIS 服务器列表。`/etc/yp.conf` 指定了你应该使用的 NIS 服务器客户端，以及如何找到它们。服务器将此过程定义为绑定客户端。可以通过向 `/etc/yp.conf` 文件中添加以下条目来设置：

```
domain developers.com server linuxser
```

上述条目指定了客户端如何使用 `linuxser` 服务器。
要对 NIS 域进行广播查询，你可以在 `/etc/yp.conf` 文件中添加以下条目：

```
domain developers.com broadcast
```

将服务器与 NIS 域关联，以便客户端连接到同一域的多个服务器。`/etc/yp.conf` 文件中的以下条目可以启用此功能：

```
domain developers.com server linuxser
```

你可以根据设置添加任何其他服务器或域。前面的示例识别了用于 `developers.com` 域的服务器。另一种此外，你可以使用 `authconf` 命令并为配置客户端提供 NIS 域名名和 NIS 服务器名称。

## 测试客户端

NIS 客户端需要 RPC 才能正常工作。因此，在启动 `ypbind` 守护进程之前，请确保 `portmapper` 正在运行。你可以在 shell 提示符处执行以下命令来确保：

```
# rpcinfo -p <client name>
```

在上述命令中，将 `<client name>` 参数指定为 NIS 客户端的 IP 地址或主机名。在 NIS 客户端的 shell 提示符处执行以下命令启动主客户端守护进程 `ypbind`：

```
# service ypbind
```

执行以下命令确认 `ypbind` 正在运行：编辑 `/etc/host.conf` 文件并按如下所示修改顺序条目：

```
# rpcinfo -u linuxpc1 ypbind
order hosts, bind
```
上述条目指定使用 NIS 用于主机名查找。

4. 配置客户端启动文件以使用 NIS：使用 `chkconfig` 使 `ypbind` 在启动时启动。要启用此项，请在 shell 提示符处执行以下命令：

```
# chkconfig --levels 345 ypbind on
```

5. 重启客户端：重启服务器以确保客户端守护进程启动。

假设你已经在 `softdevelopers.com` 域的 `linuxuser` 节点上配置了 NIS 服务器。现在你必须将 `linuxpc1` 配置为 NIS 客户端。执行以下步骤将 `linuxpc1` 配置为 NIS 客户端：

# 设置 NIS 域名名

按照上一节中配置 NIS 服务器的方法，设置 NIS 域名名如下：

```
# NISDOMAIN=softdevelopers.com
```
