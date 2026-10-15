
# 设置告警和通知

为了确保系统管理员能够及时收到任何问题或异常情况的通知，设置告警和通知至关重要。通过这种方式，可以快速处理问题，保持系统性能并将停机时间降至最低。我们将使用 Zabbix 和 Nagios 为 AlphaProject 设置通知和告警，并配置触发器。

## 在 Nagios 中配置触发器

Nagios 中的触发器通过返回 `critical`、`warning` 或 `OK` 状态的服务检查定义。这些检查被配置用于监控磁盘空间、CPU 负载、内存使用率等各种参数。

### 定义服务检查

编辑 Nagios 配置文件以定义服务检查。例如，检查磁盘空间：

```bash
$ sudo nano /usr/local/nagios/etc/objects/alphaproject.cfg
```

添加以下服务定义：

```
define service {
    use generic-service
    host_name alphaproject_server
    service_description Disk Space
    check_command check_disk!20%!10%
}
```

`check_command`：指定要运行的命令，在这种情况下，告警和严重阈值分别为 20% 和 10%。

### 定义通知选项

定义谁接收通知以及如何接收。这可以在 `contacts` 文件中设置：

```bash
$ sudo nano /usr/local/nagios/etc/objects/contacts.cfg
```

添加联系人定义：

```
define contact {
    contact_name admin
    alias Admin
    admin@gitforge.com
    service_notification_period 24x7
    service_notification_options w,u,c,r
    service_notification_commands notify-by-email
}
```

### 配置通知命令

编辑命令配置文件定义如何发送通知：

```bash
$ sudo nano /usr/local/nagios/etc/objects/commands.cfg
```

添加通知命令：

```
define command {
    command_name notify-by-email
    command_line /usr/bin/printf "%b" "***** Nagios *****\nNotification Type: $NOTIFICATIONTYPE$\nService: $SERVICEDESC$\nHost: $HOSTNAME$\nAddress: $HOSTADDRESS$\nState: $SERVICESTATE$\nDate: $LONGDATETIME$\nAdditional Info:\n\n$SERVICEOUTPUT$\n" | /usr/bin/mail -s "Nagios Service Alert: $HOSTNAME/$SERVICEDESC is $SERVICESTATE" $CONTACTEMAIL$
}
```

### 重启 Nagios

通过重启 Nagios 应用配置更改：

```bash
$ sudo systemctl restart nagios
```

## 在 Zabbix 中配置触发器

Zabbix 提供了更高级的触发器配置选项，允许复杂的表达式和条件。

### 创建触发器

登录 Zabbix 前端并导航 `Configuration > Hosts > [Your Host] > Triggers > Create Trigger`。

定义触发器详情：

- **名称**：High CPU Usage
- **表达式**：`{Template OS}`
- **严重**：High

### 配置通知动作

导航至 `Configuration > Actions > Create Action`。定义动作详情：

- **名称**：High CPU Usage Notification
- **事件源**：Triggers
- **条件**：Trigger severity = High
- **操作**：向 User Group Admin 发消息

### 定义媒体类型

前往 `Administration > Media Types`。定义通知的电子邮件服务器设置。

- **名称**：Email
- **类型**：Email
- **SMTP 服务器**：`smtp.gitforgits.com`
- **SMTP helo**：`gitforgits.com`
- **SMTP 邮箱**：`zabbix@gitforgits.com`

---

# 使用 Nagios 进行日志监控

Nagios 可以配置为监控日志文件中的特定模式，并在检测到匹配项时触发告警。这涉及定义一个检查日志文件的服务。

### 定义日志监控服务

编辑 Nagios 配置文件：

```bash
$ sudo nano /usr/local/nagios/etc/objects/alphaproject.cfg
```

添加以下服务定义：

```
define service {
    use generic-service
    host_name alphaproject_server
    service_description Log File Monitoring
    check_command check_log!/var/log/syslog!/error/
}
```

通过重启 Nagios 来应用配置更改：

```bash
$ sudo systemctl restart nagios
```

Nagios 现在将监控指定的日志文件以定义的模式（例如 "error"），如果发现该模式将向管理员告警。

# 使用 Zabbix 进行日志分析

Zabbix 提供了高级的日志监控功能，可以根据日志文件内容触发器和告警。从编辑 Zabbix agent 配置文件开始包含日志监控。

```bash
$ sudo nano /etc/zabbix/zabbix_agentd.conf
```

添加以下日志监控参数：

```
LogFile=/var/log/syslog
FontSize=10
Timeout=30
# Log file monitoring item
UserParameter=log.error[*],grep -i "$1" /var/log/syslog
```

重启 Zabbix agent 以应用更改：

```bash
$ sudo systemctl restart zabbix-agent
```

登录 Zabbix 前端并导航到 `Configuration > Hosts > [Your Host] > Items > Create Item`。

定义项详情：

```
Name: Error Log Monitoring
Key: log.error[error]
Type: Zabbix agent
Type of Information: Log
Update Interval: 1m
```
