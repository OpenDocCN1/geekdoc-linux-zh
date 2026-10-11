
```
# service httpd reload
Reloading httpd: [ OK ]
```

另一个需要考虑的选项是 `graceful` 参数。它会重启 Web 服务器，允许它读取新的配置更改而不会断开任何当前连接的客户端。这里唯一的缺点是，活动连接在终止连接并重新连接之前将使用旧的配置文件。你可以这样使用：

```
# service httpd graceful
```

## 防火墙和 SELinux 配置

为了让你的 Web 服务器完全正常工作，你需要进行一些安全更改。首先，需要在 80 端口上打开防火墙。

- **步骤 1**。使用 `iptables` 创建额外的防火墙规则：

`# iptables -I INPUT 5 -p tcp -m tcp --dport 80 -j ACCEPT`

- **步骤 2**。保存你创建的防火墙规则：

`# iptables save`

`Saving firewall rules to /etc/sysconfig/iptables: [ OK ]`

- **步骤 3**。然后重启 `iptables`：

`# service iptables restart`

`iptables: flushing firewall rules: [ OK ]`

`iptables: Setting chains to policy ACCEPT: filter [ OK ]`

`iptables: Unloading modules: [ OK ]`

`iptables: Applying firewall rules: [ OK ]`

此外，你需要查看 Web 服务器的 SELinux 保护。表 14-1 展示了可用选项。

### 表 14-1 SELinux 选项

| 选项 | 描述 |
| :--- | :--- |
| `httpd_can_network_relay` | 允许 `httpd` 作为中继。 |
| `httpd_can_network_connect_db` | 允许 `httpd` 脚本和模块通过网络连接到数据库。 |
| `httpd_use_gpg` | 允许 `httpd` 在 gpg-web 域运行 gpg。 |
| `httpd_enable_cgi` | 允许 `httpd` 支持 CGI。 |
| `httpd_use_cifs` | 允许 `httpd` 访问 CIFS 文件系统。 |
| `allow_httpd_mod_auth_pam` | 允许 Apache 使用 mod_auth_pam。 |
| `allow_httpd_anon_write` | 允许 Apache 修改公共文件。目录/文件必须标记为 public_content_t。 |
| `httpd_enable_homedirs` | 允许 `httpd` 读取家目录。 |
| `allow_httpd_sys_script` | 允许 Apache 写入公共内容。目录/文件必须标记为 public_content_t。 |
| `httpd_dbus_avahi` | 允许 Apache 通过 dbus 与 avahi 通信。 |
| `httpd_unified` | 统一 `httpd` 处理所有内容。 |
| `httpd_can_network_connect` | 允许 `httpd` 脚本通过 TCP 连接网络。 |
| `allow_httpd_mod_auth_ntlm` | 允许 Apache 使用 mod_auth_ntlm。 |
| `httpd_tty_com` | 允许 `httpd` 与终端通信。在终端输入密码需要。 |
| `httpd_read_user_content` | 允许 `httpd` 读取内容。 |
| `httpd_use_nfs` | 允许 `httpd` 访问 NFS 文件系统。 |
| `httpd_tmp_exec` | 允许 Apache 执行 tmp 内容。 |
| `httpd_execcmem` | 允许 `httpd` 脚本和模块 execcmem/stack。 |
| `httpd_can_sendmail` | 允许 `httpd` 守护进程发送邮件。 |
| `httpd_builtin_scripting` | 允许 `httpd` 使用脚本（通常为 PHP）。 |
| `httpd_can_check_spam` | 允许 `httpd` 守护进程检查垃圾邮件。 |
| `httpd_can_network_connect_cobbler` | 允许 `httpd` 脚本通过网络连接 cobbler。 |
| `httpd_ssi_exec` | 允许在 CGI 脚本域运行可执行文件。 |
| `httpd_enable_ftp_server` | 允许 `httpd` 通过监听端口作为 FTP 服务。 |
| `httpd_setlimit` | 允许 `httpd` 守护进程更改系统限制。 |

**迁移提示**：RHEL6，Web 服务的可用选项已完全改变。确保你熟悉新选项。任何扩展都需要修改 SELinux 保护。

**迁移提示**：RHEL5你需要禁用 SELinux 以使用基础 Web 服务。

**步骤 1**。查询需要更改的布尔值：

`# getsebool -a | grep httpd_dis`

`httpd_disable_trans -> off`

**步骤 2**。禁用 SELinux：

`# setsebool -P httpd_disable_trans=1`

**步骤 3**。验证布尔值已更改：

`# getsebool -a | grep httpd_dis`

`httpd_disable_trans -> on`

当你处理 Web 服务时，SELinux 方面还有一个额外要求：新创建目录的上下文需要设置以便 Web 用户正确访问。例如，假设你创建了以下目录来存放你的网站。

**步骤 1**。创建客户目录：

`# mkdir /var/www/site1`

`# mkdir /var/www/site2`

**步骤 2**。检查文件的当前上下文：

`# ls -Z /var/www`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_exec_t:s0 cgi-bin`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 error`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 html`

`drwxr-xr-x. root root system_u:object_r:httpd_content_t:s0 icons`

`drwxr-xr-x. root root unconfined:object_r:httpd_sys_content_t:s0 site1`

`drwxr-xr-x. root root unconfined:object_r:httpd_sys_content_t:s0 site2`

你可以更改客户站的上下文以匹配默认站点（`html` 目录）。

**步骤 3**。使用 `chcon` 更改用户和域的上下文：

`# chcon -Rvu system_u site1`

`changing security context of 'site1'`

`# chcon -Rvu system_u site1`

`changing security context of 'site1'`

**步骤 4**。你也可以为单个命令引用默认目录：

`# chcon --reference=html site2`

这将更改 `site2` 目录以匹配 `html` 目录的 SELinux 上文。

**步骤 5**。现在检查并验证两个客户目录的所有上下文字段是否已正确更改：

`# ls -Z`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_exec_t:s0 cgi-bin`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 error`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 html`

`drwxr-xr-x. root root system_u:object_r:httpd_content_t:s0 icons`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 site1`

`drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 site2`

### 真实世界技巧

默认的日志级别（`LogLevel`）设置为 `warn`，但你可以将其改为 `info` 或 `debug` 以查看运行情况的详细信息。不过，更改此设置时要非常小心，因为它可能会产生大量数据，并对你的系统产生负面影响或完全锁定。
