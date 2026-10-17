
# 服务定义

```
# 服务定义
define service{
use                     generic-service  ;
    host name               name_of_host
service_description     service_to_be_monitored
is_volatile               0
check_period             24x7
max_check_attempts      3
normal_check_interval   3
retry_check_interval     1
contact_groups          name_of_contactgroup
notification_interval   120
notification_period      24x7
notification_options     w,u,c,r
check_command           plugin_to_be_used
}
```

正如你之前看到的，第一个服务定义仅仅是一个模板，后续的服务定义可以使用 `use` 指令来引用它。这配置了默认设置，文件中的后续服务定义可以使用这些设置。对于 `host_name` 指令，请使用你在定义主机时指定的主机名。

对于 `service_description` 指令，为将被监控的服务创建一个直观的名称。对于 `contactgroups` 指令，输入你之前定义的联系人组名称。

对于 `check_command` 指令，输入你想针对指定主机运行的 Nagios 插件名称。Nagios 插件是一个在指定主机上执行特定功能的可执行文件或脚本。它们通过 `nagios-plugins` 和 `nagios-plugins-extra` 软件包安装。它们存储在你服务器的 `/usr/lib/nagios/plugins` 目录下，如图 8.25 所示：

图 8.25

Nagios 插件。

```
$ /usr/lib/nagios/plugins # ls

$ /usr/lib/nagios/plugins # 
```

例如，如果你想对远程主机的 FTP 服务器运行检查，你将在 `check_command` 指令中指定 `check_ftp` 插件。

正如你可能注意到的，配置 Nagios 需要你进行大量的预计划和自定义配置。然而，我认为你也会同意，在完成后 Nagios 是值得有所付出的，特别是当你负责管理非常大的网络时。

你现在准备好检查你的配置并启动 nagios 守护进程了。

# 检查你的配置并启动 Nagios

由于配置复杂，nagios 守护进程提供了一个验证选项，用于检查你的配置并确保一切运行正常。你通过在 shell 提示符下输入以下命令来实现此：

```
nagios -v nagios.cfg | more
```

请放心，在完全设置正确之前，你可能需要修复许多项目，特别是在你第一次设置 Nagios 的时候。

在你修正了检测到的错误后，你可以在 shell 提示符下输入 `rcnagios start` 来启动守护进程。

让我们在实验 8.2 中尝试一下。

# 实验 8.2: 配置 Nagios

在本次实验练习中，你将在你的 SLES 9 系统上配置 Nagios，并使用它来监控本地运行的 DNS 和 Postfix SMTP 服务。

注意

我们之所以这样做是因为实验的限制。如果你有可用的远程系统，可以自定义这里介绍的步骤来监控该系统。

要完成此练习，你需要一台运行着 DHCP、Samba、Postfix 和 CUPS 的 SLES 9 服务器。要在你的服务器上配置 Nagios，请完成以下操作：

+ 1. 启动你的 SLES 9 服务器并使用密码 `SuSE789` 以 `tux` 身份验证。

2. 通过完成以下步骤将 Nagios 与你的 Apache Web 服务器集成。

   a. 在你的服务器上，打开终端会话。

   b. 在 shell 提示符下，输入 `su -` 并使用密码 `tuX123`。

   c. 在 shell 提示符下，输入 `vi /etc/sysconfig/apache2`。

   d. 滚动到 `APACHE_SERVERADMIN` 的值到 `root@cle9.com`。

   e. 滚动到 `APACHE_SERVERNAME` 指令。

   f. 将 `APACHE_SERVERNAME` 的设置为 `"fs1.cle9.com"`。

   g. 滚动到 `APACHE_CONF_INCLUDE_DIRS` 指令。

   h. 将 `APACHE_CONF_INCLUDE_DIRS` 的设置为 `"/etc/apache2/conf.d/*.conf"`。

   j. 按 Esc；然后输入：`exit`

   k. 在 shell 提示符下，输入 `systemctl restart apache2`。

3. 打开浏览器并导航到 `http://localhost/nagios/` 测试配置。Nagios 主页应该会显示。

# 第 8 章：使用 SLES 9 管理网络

3. 通过以下操作配置 `nagios.cfg` 文件：

a. 在 shell 提示符下，输入 `vi /etc/nagios/nagios.cfg`

b. 验证是否存在以下每个文件的 `config_file=` 指令：

   - `commands.cfg`
   - `contactgroups.cfg`
   - `contacts.cfg`
   - `dependencies.cfg`
   - `escalations.cfg`
   - `hostgroups.cfg`
   - `hosts.cfg`
   - `services.cfg`
   - `timeperiods.cfg`

c. 滚动到 `check_external_commands` 指令并设置为 `1`。

d. 滚动到 `admin_email` 指令并设置为 `root@cle9.com`。

e. 按 Esc；然后输入：`exit`

4. 通过以下操作配置 `cgi.cfg` 文件：

   a. 在 shell 提示符下，输入 `vi /etc/nagios/cgi.cfg`

   b. 滚动到 `use_authentication` 行。

   c. 将 `use_authentication` 的设置为 `0`。

   d. 按 Esc；然后输入：`exit`。

注意

本质上，我们在这里是在允许任何人使用浏览器查看结果。

如果你想使用认证，你需要在 `/etc/apache2/conf.d` 中创建一个包含针对 `/usr/lib/nagios/cgi` 目录的 `AuthOverride` 语句的文件。

然后你需要在目录下创建一个 .htaccess 文件并创建一个用于认证的 htpasswd 文件。有关如何操作的更多信息，请查看 Nagios 浏览器窗口中的文档。

5. 通过以下操作配置 `hosts.cfg` 文件：

   a. 在 shell 提示符下，输入 `kate`。

   b. 选择 `File, Open`；然后打开 `/etc/nagios/hosts.cfg` 文件。

注意

由于涉及大量编辑，我们将在实验中使用 kate 完成这些文件。如果你愿意，也可以使用 vi。

   c. 滚动到 `novel11` 主机定义。

   d. 删除 `novel11` 主机定义及其后的每个主机定义。

   e. 在通用主机定义之后添加以下行：

```
# 'fs1' host definition
define host{
    use                generic-host
    host_name           fs1
    alias               Our CLE9 Server
    address             IP_address_of_fs1
    check_command       check-host-alive
    max_check_attempts  120
    notification_interval 24x7
    notification_options  d,u,r
}
```

   f. 保存对文件的更改。

6. 通过以下操作配置 `hostgroups`：

   a. 在 kate 中，打开 `/etc/nagios/hostgroups.cfg`。

   b. 滚动到 `novell-servers` 组定义。

   c. 删除 `novell-servers` 组定义及其之后所有组定义。

   d. 在文件末尾添加以下行：

   # 'CLE9-Servers' host group definition

```
hostgroup_name CLE9-Servers
alias CLE9 Lab Servers
contact_groups CLE9-admins
members fs1
}
```

- 6. 将你的更改保存到文件中。

- 7. 完成以下步骤以配置你的联系组（contactgroup）：

    - a. 在 kate 中，打开 `/etc/nagios/contactgroups.cfg`。

    - b. 滚动到 `novell-admins` 组定义。

    - c. 删除 `novell-admins` 组定义及其之后的所有组定义。

    - d. 在文件末尾添加以下行：

```
# CLE9-admins' contact group definition
contactgroup{
contactgroup_name CLE9-admins
alias CLE9 Administrators
members tux
}
```

    - e. 将你的更改保存到文件中。

- 9. 完成以下步骤配置你的联系人（contacts）：

    - a. 在 kate 中，打开 `/etc/nagios/contacts.cfg`。

    - b. 滚动到 `daemon` 联系人定义。

    - c. 删除 `daemon` 定义及其之后的所有联系人定义。

    - d. 在文件末尾添加以下行：

```
# 'tuk' contact definition
contact{
contact_name tux
alias Nagios Admin
service_notification_period 24x7
host_notification_period 24x7
service_notification_options w,u,c,r
service_notification_commands notify-by-email
host_notification_commands host-notify-by-email
email tux@cle9.com
}
```

    - e. 将你的更改保存到文件中。

- 10. 完成以下步骤配置 nagios 以监控运行 ns1 上的 DNS 和 SMTP 服务：

    - a. 在 kate 中，打开 `/etc/nagios/services.cfg`。

    - b. 滚动到 `novell1` SMTP 服务定义（在模板定义之后）。

    - c. 删除 `novell1` SMTP 服务定义及其之后的所有服务定义。

    - d. 在文件末尾添加以下行：

```
# Service definition
def service{
  generic-service{
    host_name ns1
    service_description DNS
    is_volatile 0
    check_period 24x7
    max_check_attempts 3
    normal_check_interval 3
    retry_check_interval 1
    contact_groups CLE9-admins
    notification_interval 120
    notification_period 24x7
    notification_options w,u,c,r
    check_command check_dns
  }
}
```

```
# Service definition
def service{
  generic-service{
    host_name ns1
    service_description SMTP
    is_volatile 0
    check_period 24x7
    max_check_attempts 3
    normal_check_interval 3
    retry_check_interval 1
    contact_groups CLE9-admins
    notification_interval 120
    notification_period 24x7
    notification_options w,u,c,r
    check_command check_smtp
  }
}
```

    - e. 将你的更改保存到文件中。

- 11. 在 kate 中打开 `/etc/nagios/dependencies.cfg`

- 12. 删除文件中的所有文本并保存。

- 13. 在 kate 中打开 `/etc/nagios/escalations.cfg`。

- 14. 删除文件中的所有文本并保存。

- 15. 在 kate 中，选择文件（File），全部关闭（Close All）

- 16. 通过完成 `/etc/nagios` 目录来测试你的配置

    - a. 在 shell 提示符下，切换到 `/etc/nagios` 目录

    - b. 在 shell 提示符下，输入 `nagios -v nagios.cfg`。

    - c. 你应该收到一条消息，指示未发现严重问题，如图 8.26 所示。

图 8.26

预检通过！

```
Checked 0 service escalations.
Checking host group escal.
Checked 0 host group escalations.
Checking service dependencies.
Checked 0 service dependencies.
Checking escalations.
Checked 0 host escalations.
Checking host dependencies.
Checked 0 host dependencies.
Checking commands.
Checked 2 commands.
Checking time periods.
Checked 4 time periods.
Checking for circular patterns between hosts...
Checking for circular service execution dependencies...
Checking global event handlers...
Checking absolute_inclusive service processor command...
Checking miss settings.

Total Warnings: 0
Total Errors: 0

This looks okay - No serious problems were detected during the pre-flight check
root:/etc/nagios #
```

- 17. 在 shell 提示符下输入 `rnagios start` 以启动 nagios 守护进程。

- 18. 关闭你的 nagios 浏览器窗口，然后重启浏览器。

- 19. 访问 `http://localhost/nagios/`

- 20. 探索监控（Monitoring）下提供的链接。你应该能看到与图 8.27 显示类似的内容。

## 实验练习 8.2：配置 Nagios

图 8.27

使用 Nagios 进行监控。

![](img/9a8db5c8d556a70e5a1096951368.png)

恭喜！你现在可以随心所欲使用 Nagios 了。

正如我在练习开始时提到的，你已经学习了如何配置 Nagios。

现在让我们来看看 SNMP。

## 第 8 章：使用 SLES 9 管理网络流量

### 使用 SNMP 管理流量

目标：

- 3. 使用 SNMP 监控。

SNMP 代表简单网络管理协议。如果你熟悉 DNS 或 Novell's eDirectory，你已经熟悉数据是如何分级的。

在 DNS 中，我们有根（.）和顶级域名（TLD），如 com、edu、org 和 net。每个顶级域名下都有特定的组，如 novell.com、use.com 和 tld.org。在这些组中，可以有特定的主机。

MIB 使用了类似的结构。它的顶层是 iso。在 iso 内部是 org。这种顶层结构如图 8.28 所示：

图 8.28

SNMP 组件。

![](img/9a8db5c8d556a70e5a1096951370.png)

它们的作用如下：

- 管理器（Manager）——SNMP 管理器负责收集数据。

- 代理（Agents）——SNMP 代理运行在硬件上，包括服务器。

- 管理信息库（MIB）——MIB 定义了使用的参数。

MIB 相当复杂。在继续之前，让我们花几分钟回顾一下 MIB 的结构。

### MIB 是如何组织的

MIB 并不是一个真正的数据库。它仅仅定义了结构。

### SNMP 如何工作

SNMP 是一种用于网络设备的协议。如果你熟悉 DNS（到目前你应该已经熟悉）或 Novell's eDirectory，你已经熟悉数据是如何分级的。

MIB 使用了类似的结构。它的顶层是 iso。在 iso 内部是 org。这种顶层结构如图 8.29 所示：

图 8.29

SNMP MIB 结构。
