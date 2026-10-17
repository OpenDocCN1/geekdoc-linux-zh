
`-p` 选项指定优先级，包括 "emerg"（紧急）、"alert"（警报）、"crit"（严重）、"err"（错误）、"warning"（警告）、"notice"（通知）、"info"（信息）、"debug"（调试）或代表每个命名级别的 0 到 7 之间的值。这些优先级值与 `syslog(3)` 定义相同。默认为 "info"。`-t` 选项是一个标识符，可以是任意字符串作为程序或脚本名称。此字符串可以使用 `journalctl` 命令进行搜索。

列出日志中最近的五个条目。

```
# journalctl -n 5
```

Jan 06 07:20:58 testv1.both.org systemd[1]: sysstat-collect.service: Deactivated successfully

Jan 06 07:20:58 testv1.both.org systemd[1]: Finished sysstat-collect.service. activity accounting tool.

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42
