
`/etc/hosts.allow` 和 `/etc/hosts.deny` 文件的格式相同。关键字 `ALL` 表示所有客户端。例如：

```
in.telnetd: .example.com
fingered: ALL
```

这意味着 `telnet` 连接允许来自 `example.com` 域名的客户端，而 `finger` 连接允许所有客户端。

服务守护进程列在左侧，如果要出两个服务守护进程，则进程之间用逗号（`,`)）分隔。分号作为守护进程名称与地址部分之间的分隔符。如果需要提到多个地址，地址之间用逗号分隔。

`ALL` 标志允许用户将文件设置为尽可能严格的限制。这增强了安全性。

## 18.4.安全级别配置

安全级别配置工具用于设置系统的安全级别。要调用安全级别配置工具，请在终端窗口中输入以下命令：

```
[root@localhost~]# system-config-securitylevel
```

![](img/01872e44e0db1c79895b45feb5b484a6_157_0.png)

在“防火墙选项”（Firewall Options）选项卡上，用户可以设置启用或禁用防火墙。受信任的服务允许通过防火墙。在其他端口上，用户可以通过点击“添加”（Add）按钮来添加信任端口，点击“添加”按钮会显示下方面板：

![](img/01872e44e0db1c79895b45feb5b484a6_158_0.png)

在添加端口面板上，用户可以输入端口以及协议（`tcp` 和 `udp`）。输入值后按 确定。

用户可以点击“高级选项”（Advanced options）选项卡来添加一个包含 `iptables` 保存格式的 `iptables` 规则的文件。这允许用户添加更复杂的规则并自定义防火墙。

![](img/01872e44e0db1c79895b45feb5b484a6_158_1.png)

用户可以浏览并上传包含用户定义规则的文件。进行更改后，点击“应用”（apply）然后点击“确定”。

### 18.4.1.配置文件

有两个配置文件 `/etc/sysconfig/iptables` 和 `/etc/sysconfig/iptables-config`。

`/etc/sysconfig/iptables` 文件包含当前施加于系统的安全级别。

该文件由安全级别配置工具写入。

`/etc/sysconfig/iptables-config` 文件用于加载额外的 `iptables` 模块。额外的模块有助于 NAT 过滤和辅助程序。示例 `/etc/sysconfig/iptables-config` 文件如下：

```
IPTABLES_MODULES="ip_conntrack_netbios_ip_conntrack_ftp"
```

`IPTABLES_MODULES` 指令定义了加载的模块。在上面的示例中，加载了 `ip_conntrack_netbios_ip_conntrack_ftp` 模块。

- # 在重启时保存当前防火墙规则。
- # 值：yes|no，默认：no
- # 如果防火墙重启，则将所有防火墙规则保存到 `/etc/sysconfig/iptables`。

```
IPTABLES_SAVE_ON_RESTART="no"
```

如果值为 `yes`，则规则将保存到文件 `/etc/sysconfig/iptables`。

## 18.5.命令参考

| 命令 | 描述 |
|---|---|
| `iptables -A` | 在当前 `iptables` 规则中追加安全规则 |
| `iptables -D` | 删除规则 |
| `iptables -R` | 替换规则 |
| `iptables -I` | 插入规则 |
| `iptables -L` | 列出所有规则 |

## 19.PAM 和 SELINUX

### 19.1.PAM

PAM 代表可插认证模块（Pluggable Authentication module）。PAM 是一个库系统，处理系统上应用程序（服务）的认证任务。

配置文件 `/etc/pam.conf` 或 `/etc/pam.d` 目录下的文件用于配置 PAM。如果 `/etc/pam.d` 目录中存在文件，则忽略 `/etc/pam.conf` 文件的内容。

### 19.2./etc/pam.d

`/etc/pam.d` 目录下的文件对应使用 PAM 进行认证的服务。例如，上述目录下的 `passwd` 文件包含以下行：

```
#%PAM-1.0
auth include system-auth
account include system-auth
password include system-auth
```

第一行是注释。

第二行包含 PAM 规则。后续行的格式为规则行：

`type control module- path module-argument`

上述类型为 `auth`。

PAM 允许四种类型：`account`（账户）、`password`（密码）、`authentication`（认证）和 `session`（会话）。

- Account – 账户类型根据资源可用性、时间和其他参数定义对服务的访问。
- authentication(auth) – 认证类型提示用户输入密码，如果用户提供了密码，他就可以访问该服务。
- Password – 密码类型用于更新用户信息，如更改用户密码。
- Session – 此类型用于在用户访问服务之前或之后执行任务（如日志记录）。

控制（control）的有效值包括 `required`（必须）、`sufficient`（足够）和 `optional`（可选）。

- Required – 意味着如果 PAM 模块返回失败，pam 将返回失败。假设调用了三个模块，如果此模块返回 false，则结果将为 false，但 pam 会调用该进程调用的所有模块。
- Sufficient – 意味着如果此模块返回成功，PAM 将返回成功，且将不再调用该进程调用的其他 PAM 模块。
- Optional – 此模块的成功或失败取决于此模块返回 PAM 模块的结果。假设调用了三个模块，如果此模块返回 false，则结果将为 false，但 pam 会调用该进程调用的所有模块。后续行的格式为规则行：

`type control module- path module-argument`

（注：原文后续部分存在大量重复内容，已根据要求进行翻译并保持格式一致）

## 19.SELinux

SELinux 是一个增强安全的 Linux 内核，提供了强制访问控制（MAC）机制。它允许系统管理员定义限制进程访问文件的安全策略。

SELinux 工具用于设置系统的安全级别。要调用 SELinux 工具，在终端窗口中输入以下命令：

```
[root@localhost~]# system-config-level
```

![](img/01872e44e0db1c79895b45feb5b484a6_157_0.png)

在“防火墙选项”（Firewall Options）选项卡上，用户可以设置启用或禁用防火墙。受信任的服务允许通过防火墙。在其他端口上，用户可以通过点击“添加”（Add）按钮来添加信任端口，点击“添加”按钮会显示下方面板：

![](img/01872e44e0db1c79895b45feb5b484a6_158_0.png)

在添加端口面板上，用户可以输入端口以及协议（`tcp` 和 `udp`）。输入值后按 确定。

用户可以点击“高级选项”（Advanced options）选项卡来添加一个包含 `iptables` 保存格式的 `iptables` 规则的文件。这允许用户添加更复杂的规则并自定义防火墙。

![](img/01872e44e0db1c79895b45feb5b484a6_158_1.png)

用户可以浏览并上传包含用户定义规则的文件。进行更改后，点击“应用”（apply）然后点击“确定”。

### 19.2.1.配置文件

有两个配置文件 `/etc/sysconfig/iptables` 和 `/etc/sysconfig/iptables-config`。

`/etc/sysconfig/iptables` 文件包含当前施加于系统的安全级别。

该文件由安全级别配置工具写入。

`/etc/sysconfig/iptables-config` 文件用于加载额外的 `iptables` 模块。额外的模块有助于 NAT 过滤和辅助程序。示例 `/etc/sysconfig/iptables-config` 文件如下：

```
IPTABLES_MODULES="ip_conntrack_netbios_ip_conntrack_ftp"
```

`IPTABLES_MODULES` 指令定义了加载的模块。在上面的示例中，加载了 `ip_conntrack_netbios_ip_conntrack_ftp` 模块。

- # 在重启时保存当前防火墙规则。
- # 值：yes|no，默认：no
- # 如果防火墙重启，则将所有防火墙规则保存到 `/etc/sysconfig/iptables`。
