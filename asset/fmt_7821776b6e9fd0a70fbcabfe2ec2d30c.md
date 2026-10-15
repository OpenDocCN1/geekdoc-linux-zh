
```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

通过 `printf` 宏，生成的消息看起来如下：

```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

通过 `printf` 宏，生成的消息看起来如下：

```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

通过 `printf` 宏，生成的消息看起来如下：

```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

通过 `printf` 宏，生成的消息看起来如下：

```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

通过 `printf` 宏，生成的消息看起来如下：

```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

通过 `printf` 宏，生成的消息看起来如下：

```
define service{
  notification_interval 120
  notification_period 24x7
  notification_options w,u,c,r,f
}
```

| 宏 | 描述 |
| :--- | :--- |
| `$CONTACTEMAILS` | 联系人邮箱 |
| `$DATETIME` | 时间 |
| `$HOSTALIAS` | 主机别名 |
| `$HOSTADDRESS` | 主机地址 |
| `$HOSTNAME` | 主机名称 |
| `$HOSTSTATE` | 主机状态：UP, DOWN, CRITICAL 或 UNKNOWN |
| `$NOTIFICATIONTYPE` | 通知类型：PROBLEM, WARNING, CRITICAL, RECOVERY, ACKNOWLEDGEMENT |
| `$SERVICEDESC` | 服务描述 |
| `$SERVICESTSTATE` | 服务状态：OK, WARNING, CRITICAL 或 UNKNOWN |
| `$NOTIFICATIONOUTPUT` | 通知输出 |

### 12.4.2 通过短信通知

对于 `host_notification_commands`，命令格式类似，只是现在是主机：

```
define contact(
  service_notification_commands notify-by-email,notify-by-sms
  host_notification_commands host-notify-by-email,host-notify-by-sms
  email               nagios-admin@localhost
  pager               459-1234-56789
  address1            root@example.com
  address2            123-456789
)
```

它生成的邮件如下：

```
To: wob@swspace.de
Subject: UP Alert for wob-proxy
Date: Fri 14 Jan 2005 17:50:21 +0100 (CET)
From: Nagios Admin <nagios@swspace.de>

***** Nagios *****
Notification Type: RECOVERY
Host: wob-proxy
State: UP
Address: 172.168.19
Info: PING OK Packet loss = 0%, RTA = 69.10 ms
Date/Time: Fri 14 Jan 2005 17:50:21 CET
```

虽然发送电子邮件所的基础设施通常已经可用，但发送短信通常需要额外安装 `yaps`、`ssmsend` 或 `smsclient`。`yaps` 和 `smsclient` 需要本地调制解调器或 ISDN 卡，或者直接连接手机运营商的“电话”；`ssmsend` 则连接到手机运营商的互联网服务器并通过此路由发送短信。使用 `yaps` 和 `smsclient`，你也可以使用生成并发送短信的邮件网关。

无论你选择哪种方法，都应该注意到发送消息可能会受到干扰：Nagios 服务器与互联网之间的连接通过了许多主机、路由器和防火墙。特别是当 Nagios 监控其中某台机器时，情况会变得变得：如果这台机器宕机，通过 `ssmsend` 发送的消息也将无法工作。同样的情况也适用于邮件-短信网关。无论是涉及自制结构（使用 `yaps` 和 `smsclient`，每个程序都代表自己的短信网关），还是带有复杂的统一消息解决方案的电话系统，如果实际短信发送者与 Nagios 服务器之间存在多个节点（因为你有一个网络化电话系统

在多个位置（例如），由于连接中断导致消息无法到达目的地的概率会增加。

出于这个原因，最佳解决方案是在 Nagios 服务器本身上安装 `smsclient` 或 `yaps`，并具有直接电话访问权限。在较大的网络化电话系统中，你还可以考虑为电话提供一条来自电话系统的专用直连线路。这取决于是使用 ISDN 还是取决于所使用的技术问题。

## 设置 smsclient

虽然 Debian 提供了预编译的 `smsclient` 包，但对于 SuSE 和其他发行版，你必须手动编译该软件。由于历史原因，该程序名为 `sms_client`：通过 `man sms_client` 可以查看简短子集。

源代码的安装遵循常规程序：

```bash
linux: # cd /usr/local/src # tar xvf /path/to/sms_client-2.x.y
linux:local/src # #sms_client-2.x.y
linux:src/sms_client-2.x.y # ./configure
linux:src/sms_client-2.x.y # make && make install
```

这里唯一值得提到的是，“自制”的配置 过程不需要 `autoconf` 和 `automake`。

表 12-2 列出的配置文件现在位于 `/etc/sms` 目录；Debian 包将其安装到 `/etc/smsclient`。

### 表 12-2. smsclient 配置文件

| 文件 | 说明 |
|---|---|
| `sms_addressbook` | 别名和组的定义 |
| `sms_config` | 主配置文件 |
| `sms_daemons` | `smsclient` 守护进程模式的配置文件，在该模式下可以通过专用协议访问。这不是必须的。 |
| `sms_modem` | 调制调器配置 |
| `sms_services` | 支持的服务商 |

`sms_services` 文件列出了支持的服务商，同时将它们分配给所使用的协议。拨打的精确电话号码由 `services` 目录下的对应服务文件（如果你自己编译了它）或 `/usr/lib/smsclient/services`（针对 Debian）指定。如果不确定，你应该向你自己的移动运营商请求电话号码。邮件列表在这里也可以提供帮助。

在 `sms_config` 文件中，你设置了一个默认服务商，程序在未明确指定服务商时会使用它进行通话：

```ini
SMS_default_service = "di"
```

现在 `sms_modem` 文件中仅缺少调制调器的配置。但原则上，任何在 Linux 下运行的调制调器都可以。在下面的示例中，使用带有 Isdn4Linux-HiSax 驱动的 ISDN 卡：
