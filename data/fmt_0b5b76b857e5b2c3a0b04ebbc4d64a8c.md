
默认文件中只有两条指令，在表 29-11 中进行了解释。

| 指令 | 描述 |
| :--- | :--- |
| `SQUID_OPTS` | 默认为 `-D`。在 Squid 启动时启用 DNS 检查。 |
| `SQUID_SHUTDOWN_TIMEOUT` | 默认为 100。指定延迟开始关闭 Squid 的秒数。 |

# 表 29-11 Squid 启动文件中的指令

Squid 的主配置文件是 `/etc/squid/squid.conf`。该文件中定义的关键指令在表 29-12 中列出并描述。

| 指令 | 描述 |
| :--- | :--- |
| `http_port` | 默认值为 3128。指定要使用的端口号。 |
| `hierarchy_stoplist` | 默认值为 "cgi-bin?"。一组词，如果在 URL 中找到，将导致该对象由此 Squid 服务器直接处理。 |
| `access_log` | 默认值为 `/var/log/squid/access.log`。跟踪页面的下载情况。 |
| `acl` | 访问控制列表。某些选项包括：<br>`SSL_ports` / Safe ports: 指定用于缓存流量的端口。<br>`localhost src 127.0.0.1/255.255.255.255`: 允许访问本地主机。<br>`src_net src 192.168.1.0/24`: 允许访问指定的网络。<br>`dst_net dst 192.168.2.0/24`: 允许访问目标网络。 |

请参考第 22 章“DNS 和 DHCP”获取更多 `acl` 指令用法信息。

Red Hat 认证技术员与工程师

| 指令 | 描述 |
| :--- | :--- |
| `cache_dir` | 默认值为 `/var/spool/squid`，大小为 100MB。定义缓存目录和缓存内容的最大大小。 |
| `cache_mem` | 默认值为 8MB。定义用于持有传输中对象的内存量。 |
| `cache_peer` | 允许你在父/兄弟缓存模型中连接多个 Squid 服务器的缓存。 |
| `http_access` | allow—允许来自指定系统的查询 |

表 29-12 Squid 配置文件中的指令

## Squid 的 SELinux 要求

如果强制执行 SELinux（enforced），你需要禁用对 Squid 服务的保护以确保功能正常运行。使用如如下所示的 `setbool` 命令，或使用第 30 章“系统和网络安全”中解释的 SELinux 配置系统 `system-config-selinux`。仅指定需要禁用的布尔值，保持其他不变。

```bash
# setbool -P squid_connect_any=1 squid_disable_trans=1
```

使用 `getsebool` 命令进行验证：

```bash
# getsebool -a | grep ^squid
squid_connect_any --
squid_disable_trans --
```

## 配置 Squid

为了确保 Squid 服务的顺畅运行，如果 SELinux 处于强制模式，你需要禁用对该服务的保护。使用如下所示的 `setbool` 命令，或使用第 30 章“系统和网络安全”中解释的 SELinux 配置系统 `system-config-selinux`。仅指定需要禁用的布尔值，保持其他不变。

```bash
# setbool -P squid_connect_any=1 squid_disable_trans=1
```

使用 `getsebool` 命令进行验证：

```bash
# getsebool -a | grep ^squid
squid_connect_any --
squid_disable_trans --
```

## 配置 Squid 服务

为了确保 Squid 服务的顺畅运行，如果 SELinux 处于强制模式，你需要禁用对该服务的保护。使用如下所示的 `setbool` 命令，或使用第 30 章“系统和网络安全”中解释的 SELinux 配置系统 `system-config-selinux`。仅指定需要禁用的布尔值，保持其他不变。

要配置本地网络上的系统作为代理服务器，并让 Squid 在 8080 端口上监听：

```bash
# setbool -P squid_connect_any=1 squid_disable_trans=1
```

使用 `getsebool` 命令进行验证：

```bash
# getsebool -a | grep ^squid
squid_connect_any --
squid_disable_trans --
```

要配置本地网络上的系统作为代理服务器，并让 Squid 在 8080 端口上监听：

1. 检查是否安装了 Squid 包：

```bash
# rpm -qa | grep squid
squid-2.6.STABLE
```

2. 使用以下命令使 Squid 开机自启动：

```bash
# chkconfig squid on
```

3. 参考“防火墙安全”章节修改防火墙设置以开启 8080 端口。4. 编辑 `/etc/squid/squid.conf` 文件并设置以下指令：

```http
http_port 8080
visible_hostname rhel4
acl allow_net 192.168.0.0/24
acl deny_net 192.168.5.0/24
acl deny_dom geticify.com
http_access allow_net
http_access deny_net
http_access deny_dom
```

第一行定义了 Squid 监听的端口，第二行指定了服务器名称，接下来的两个是访问列表，最后一对通过 `http_access` 对它们进行配置。

5. 使用以下方法启动 Squid。这将读取 `/etc/squid/squid.conf` 文件并启动守护进程，开始在 8080 端口监听。

```bash
# service squid start
init_dir /var/spool/squid... Starting squid.      [ OK ]
```

6. 验证 Squid 的运行状态：

```bash
# service squid status
squid (pid 3337) is running...
```
