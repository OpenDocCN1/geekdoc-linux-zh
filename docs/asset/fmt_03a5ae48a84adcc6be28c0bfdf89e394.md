
```bash
# systemctl --now enable rsyslog
```

### CIS 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 6.2 收集审计日志 收集审计日志。确保企业资产范围内已启用日志以及企业的审计管理流程。 | | | |
| v7 | 6.2 激活审计日志 确保所有系统和网络设备上已启用日志。 | | | |
| v7 | 6.3 启用详细日志 启用系统日志以包含详细信息，如事件源、日期、用户、时间戳、源地址、目的地址和其他有用元素。 | | | |

### MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| T1070, T1070.002, T1562, T1562.001 | TA0005 | |

## 4.2.2.3 确保 journal 配置为将日志发送到 rsyslog（手动）

配置适用性：

- 等级 1 - 服务器
- 等级 1 - 工作站

描述：

来自 `journald` 的数据可能存储在挥发性内存中或本地持久化在服务器上。虽然存在导出远程 `journald` 日志的工具，但使用 `RSyslog` 服务提供了一种一致的日志收集和导出方法。

原理：

如果 `RSyslog` 是捕获日志的首选方法，系统的所有日志都应发送到那里进行进一步处理。

审计：

如果 `RSyslog` 是捕获日志的首选方法，请检查 `/etc/systemd/journald.conf` 并验证日志是否已转发到 `rsyslog`。

```bash
# grep \s*ForwardToSyslog /etc/systemd/journald.conf
```

验证输出是否匹配：

```bash
ForwardToSyslog=yes
```

修复：

编辑 `/etc/systemd/journald.conf` 文件并添加以下行：

```bash
ForwardToSyslog=yes
```

重启服务：

```bash
# systemctl restart rsyslog
```

### 其他信息：

如 `journal` 手册帮助页所述，`journal` 日志可以通过此处提到的过程或通过如 `systemd-journal.service` 这样的设施导出到 `rsyslog`。每种实现方式都涉及权衡，其中 `ForwardToSyslog` 会立即捕获所有事件（如果配置妥当，则转发到外部日志服务器），但不会捕获所有启动事件。另一方面，`systemd-journal.service` 等机制会记录重启事件，但可能会延迟向 `rsyslog` 发送信息，导致在导出之前存在日志篡改的风险。请注意所有用于保护系统的工具的局限性。

主配置文件 `/etc/systemd/journal.conf` 在任何自定义的 `.conf` 文件之前被读取。如果存在自定义配置，它们将覆盖主配置参数。

### CIS 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 8.2 收集审计日志 收集审计日志。确保企业资产范围内已启用日志以及企业的审计管理流程。 | | | |
| v8 | 8.9 集中审计日志 尽可能在企业资产范围内集中审计日志的收集和保留。 | | | |
| v7 | 6.2 激活审计日志 确保所有系统和网络设备上已启用本地日志。 | | | |
| v7 | 6.3 启用详细日志 启用系统日志以包含详细信息，如事件源、日期、用户、时间戳、源地址、目的地址和其他有用元素。 | | | |
| v7 | 6.5 集中日志管理 确保将日志聚合到集中日志系统进行分析和审查。 | | | |

## 4.2.2.4 确保 rsyslog 默认权限已配置（自动化）

配置适用性：

- 等级 1 - 服务器
- 等级 1 - 工作站

描述：

`rsyslog` 将创建系统中不存在的日志文件。此设置控制应用于这些新创建文件的权限。

原理：

确保日志文件具有正确的权限以确保敏感数据得到存档和保护很重要。

影响：

系统的全局 `umask` 可能会覆盖 `RSyslog` 通过 `FileCreateMode` 配置的更严格的文件权限。`rsyslog` 还有自己的 `umask` 指令可以更改文件模式。因此，确保在 `/etc/rsyslog.conf`、`/etc/rsyslog.d/*` 创建任何文件之前已设置了 `FileCreateMode` 至关重要。

审计：

运行以下命令：

```bash
# grep ^FileCreateMode /etc/rsyslog.conf /etc/rsyslog.d/*
```

验证输出是否匹配：

```bash
FileCreateMode 0640
```

如果站点策略规定了较松的权限，请遵循该策略。更严格的权限如 `0600` 即可。

修复：

编辑 `/etc/rsyslog.conf` 或 `/etc/rsyslog.d/` 中的专用 `.conf` 文件，并将 `FileCreateMode` 设置为 `0640` 或更严格：

```bash
FileCreateMode 0640
```

重启服务：

```bash
# systemctl restart rsyslog
```

### 参考：

- 1. 查看 `rsyslog.conf(5)` 页更多信息。

### CIS 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 3.3 配置访问列表 根据用户的需要配置访问列表。将数据访问控制（即权限）应用于本地和远程文件系统、数据库和应用程序。 | | | |
| v8 | 8.2 收集审计日志 收集审计日志。确保企业资产范围内已启用日志以及企业的管理流程。 | | | |
| v7 | 5.1 建立配置 为所有操作系统和软件维护文档化的标准配置。 | | | |
| v7 | 6.2 激活审计日志 确保所有系统和网络设备上已启用本地日志。 | | | |
| v7 | 6.3 启用详细日志 启用系统日志以包含详细信息，如事件源、日期、用户、时间戳、源地址、目的地址和其他有用元素。 | | | |

### MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| T1070, T1070.002, T1083, T1083.000 | TA0007 | |

## 4.2.2.5 确保日志已配置（手动）

配置适用性：

- 等级 1 - 服务器
- 等级 1 - 工作站

描述：

`/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 文件指定了日志规则以及使用哪些文件来记录某类消息。

原理：

大量重要的安全相关信息通过 `rsyslog` 发送（例如，成功和失败的 `su` 尝试、失败的登录尝试、`root` 登录尝试等）。

审计：

检查 `/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 内容以确保设置了适当的日志。此外，运行以下命令并验证日志文件按预期记录信息：

```bash
# ls -l /var/log/
```

修复：

根据你的环境编辑 `/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 文件中的以下行。

注意：下面的配置仅供示例。对于你希望存储日志数据的组织应谨慎。

```
*emerg:*
*auth,authpriv.* /var/log/secure
*mail.* /var/log/mail
*mail.info /var/log/mail.info
*mail.warning /var/log/warn
*mail.err /var/log/mail.err
*cron.* /var/log/cron
*=warning;*=err /var/log/warn
*crit /var/log/warn
*;mail,none;news.news /var/log/messages
*local0,local1.* /var/log/localmessages
*local2,local3.* /var/log/localmessages
*local4,local5.* /var/log/localmessages
*local6,local7.* /var/log/localmessages
```

运行以下命令重载 `rsyslog` 配置：

```bash
# systemctl restart rsyslog
```

### MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| T1070, T1070.002 | TA0005 | |

## 4.2.2.6 确保 rsyslog 配置为将日志发送到远程日志主机（手动）：

配置适用性：

- 等级 1 - 服务器
- 等级 1 - 工作站

描述：

`Rsyslog` 支持将其收集的日志事件发送到远程日志主机，或接收来自远程主机的消息，从而实现集中日志管理。

原理：

将日志数据存储在远程主机上可以保护日志完整性免受本地攻击的影响。如果攻击者获得了本地系统的 `root` 权限，他们可能会篡改或删除存储在本地系统上的日志数据。

审计：

检查 `/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 文件，并验证日志是否已发送到中心主机（其中 `loghost.example.com` 是您的中心日志主机的名称）：

旧格式

```bash
# grep "^\.*[^\I][^\I]*@"" /etc/rsyslog.conf /etc/rsyslog.d/*..conf
```

输出应包含 <远程日志主机的 FQDN 或 IP>，例如：

```
*.* @loghost.example.com
```

新格式

输出应包含 <远程日志主机的 FQDN 或 IP>，例如：

```
* action(type="omfwd" target="loghost.example.com" port="514"
protocol="tcp")
```

### 修复：

编辑 `/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 文件并添加以下行（其中 `loghost.example.com` 是您的中心日志主机的名称）。`target` 指可以是完全限定域名，也可以是 IP 地址。

```
* action(type="omfwd" target="192.168.2.100" port="514" protocol="tcp" action.resumeRetryCount="100" queue.type="LinkedList" queue.size="1000")
```

运行以下命令以重载 `rsyslog` 配置：

```bash
# systemctl restart rsyslog
```

### 参考：

- 1. 请查看 `rsyslog.conf(5)` 手册页获取更多信息。

### 附加信息：

此外，请参阅 `Rsyslog` 文档了解 `TLS` 的实现细节。

### CIS 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 8.2 收集审计日志 收集审计日志。根据企业的审计日志管理流程，确保企业资产范围内已启用日志记录。 | | | | ● |
| v7 | 6.2 激活审计日志 确保所有系统和网络设备上已启用本地日志记录 | | | | |
| v7 | 6.3 启用详细日志 启用系统日志以包含详细信息，例如事件源、日期、用户、时间戳、源地址、目的地址和其他有用元素。 | | ● | | |

### MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
| :--- | :--- | :--- |
| T1070, T1070.002, T1562, T1562.006 | TA0040 | M1029 |

## 4.2.2.7 确保 rsyslog 未配置为接收来自远程客户端的日志（自动）

配置适用性：

- 等级 1 - 服务器
- 等级 1 - 工作站

描述：

`RSyslog` 支持接收来自远程主机的消息，从而当日志服务器。客户端不应从其他主机接收数据。

原理：

如果客户端被配置为接收数据并使其变为服务器，该系统将超出其运行边界。

审计：

检查 `/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 文件，并验证系统未配置接受传入日志。

旧格式

```bash
# grep '$ModLoad imtcp' /etc/rsyslog.conf /etc/rsyslog.d/*.conf
# grep '$InputTCPServer' /etc/rsyslog.conf /etc/rsyslog.d/*.conf
```

新格式

```bash
# grep -P '^\module\(load=imtcp\')' /etc/rsyslog.conf /etc/rsyslog.d/*.conf
# grep -P '^\input\(type=imtcp\) port=\"514\')' /etc/rsyslog.conf /etc/rsyslog.d/*.conf
```

预期无输出。

修复：

如果客户端被配置为接收数据并使其变为服务器，该系统将超出其运行边界。编辑 `/etc/rsyslog.conf` 和 `/etc/rsyslog.d/*.conf` 文件并添加以下行（其中 `loghost.example.com` 是您的中心日志主机的名称）。

```
* action(type="omfwd" target="loghost.example.com" port="514" protocol="tcp")
```

运行以下命令以重载 `rsyslog` 配置：

```bash
# systemctl restart rsyslog
```

### CIS 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| :--- | :--- | :--- | :--- | :--- |
| v8 | 8.2 收集审计日志 收集审计日志。根据企业的审计日志管理流程，确保企业资产范围内已启用日志记录。 | | | | ● |
| v7 | 6.2 激活审计日志 确保所有系统和网络设备上已启用本地日志记录 | | | | |
| v7 | 6.3 启用详细日志 启用系统日志以包含详细信息，例如事件源、日期、用户、时间戳、源地址、目的地址和其他有用元素。 | | ● | | |

```bash
*.journal)
    if stat -Lc "%a" "$fname" | grep -Pq --^\h*[0,2,4,6] [0,4]0\$; then
        output=\$output\n- File: \$fname \$(stat -Lc "%a" "$fname")"
    fi
    fi;
    if stat -Lc "%U %G" "$fname" | grep -Pq --^\h*(root)\h+(systemd-journal-root)\h\$; then
        output=\$output\n- File: \$fname ownership: \$(stat -Lc "%U:%G" "$fname")"
    fi
    fi;
    if stat -Lc "%a" "$fname" | grep -Pq --^\h*[0,2,4,6] [0,4]0\$; then
        output=\$output\n- File: \$(stat -Lc "%a" "$fname")"
    fi
    fi;
    if stat -Lc "%U %G" "$fname" | grep -Pq --^\h*(syslog|root)\h+(adm|root)\h\$; then
        output=\$output\n- File: \$fname ownership: \$(stat -Lc "%U:%G" "$fname")"
    fi
    fi;
esac
done
# 如果所有文件通过，则通过通过
if [ -z "$Output" ]; then
    echo -e "\n- PASS\n- All files in /var/log/ have appropriate permissions and ownership"
else
    # 打印失败的原因
    echo -e "\n- FAIL:$output"
fi
echo -e "\n- End check - logfiles have appropriate permissions and ownership"
}
```

### 修复 (Remediation):

运行以下脚本以更新 `/var/log` 中文件的权限和所有权。虽然该脚本没有破坏性，但审计过程的输出会被记录下来，以防修复操作导致问题。
