
```
user@linux:~ mysql -u eventdb -p eventdb
mys> SELECT * FROM events WHERE datetime < '2007-11-16'
-> AND acknowledged;
```

MySQL 以 `YYYY-MM-dd HH:MM:SS` 格式存储日期，这就是为什么简单的字符串比较是有效的。如果管理员确认了一个条目，`acknowledged` 字段将包含值 `1`。一个简单的清理脚本会删除所有超过两周的确认记录：

```bash
#!/bin/bash
OLDDATE=$(date --date='2 weeks' '+%Y-%m-%d %H:%M:%S')
MYSQL="mysql --user=eventdb --password=password eventdb"

$MYSQL --execute="DELETE FROM events WHERE datetime < '$OLDDATE' AND acknowledged;"
$MYSQL --execute="optimize table events";
```

该脚本通过 `cron` 每日运行，但尚未经过测试。如果你想在删除数据之前归档数据，需要在 `DELETE` 语句之前导出。为了做到这一点，你需要在上述的 `SELECT` 命令中 `SELECT * FROM` 之间添加 SQL 语句 `INTO OUTFILE`。这会将数据保存到以制表符为分隔符的文本文件中所示：

```
SELECT *
INTO OUTFILE '/var/backups/eventdb/$OLDDATE.txt'
FIELDS TERMINATED BY '\t'
FROM events WHERE datetime < '2007-11-16' AND acknowledged;
```

`EventDB` tar 包在清理子目录下包含两个脚本 `eventdb_clean_database.sh` 和 `rotate_eventdb.sh`，它们基本上包含了上述的所有功能。尽管如此，你仍然应该仔细考虑如何清理数据库，并相应地修改和测试脚本。

### 23.6 将 Windows 事件发送到 Syslog

为了将 Windows 系统集成到 syslog 环境，你需要一个服务来读取 Windows 日志并通过 syslog 协议将其发送到中央 syslog 服务器。此任务由免费提供且易于安装的 Eventlog（项目名称 *Eventlog to Syslog* 的缩写）完成，该工具来自普渡大学工程网络的首页。该网页提供了两个下载，分别对应 32 位和 64 位系统（`eventlog_exe_32.zip` 或 `eventlog_exe_64.zip`），均来自源代码。包中包含 `eventlog.exe` 和 `eventlog.dll` 文件被复制到 Windows 服务器的 `system32` 子目录（通常为 `C:\Windows\system32`）。通过以下命令安装并激活服务：

```
C:\Windows\system32> eventlog -h
C:\Windows\system32> start eventlog
```

如果要在已经在运行该服务的系统上安装当前的 `eventlog` 版本，你必须先安装旧版本：

```
C:\Windows\system32> stop eventlog
C:\Windows\system32> eventlog -u
```

`eventlog` 将所有日志条目发送到中央 syslog 服务器。消息进入守护进程设施（facility），可能的优先级有 `notice`、`warning` 和 `err`。在所有情况下，你都应该利用 syslog 服务器上 `syslog-ng` 的大量选项，因为即使在小型环境中，单个域控制器的消息每小时也可以管理 1000 条更多条目！

如果你想先在 Windows 侧过滤条目，你将需要其他服务。一个免费但也很老旧、且可能从 2003 年起无法完美工作的工具是 `syslog`。你还可以在互联网上找到可以购买的各种商业选项。另一个 Windows 过滤器由 Nagios EventAgent 提供，它在 Nagios 上可用，但与 EventDB 不兼容，因为数据是通过方式发送的。

## 23.7 使用 SNMP 使不可理解的内容变得可读

`SNMP` 翻译器（`SNMPTT`）通过随附的 MIB 将难以理解的对象标识转换为可读文本。为了安装此工具，从 Sourceforge 解压 `SNMPTT` 源码到 `/usr/local/src`

```
local:/src # tar xvf snmptt_1.2.gz
local:/src # cd snmptt_1.2
linux:src/snmptt_1.2 # cp nethandler snmpttconvert /usr/bin/
linux:src/snmptt_1.2 # chmod + /usr/bin/snmptt*
linux:src/snmptt_1.2 # cp snmptt.ini /etc/snmp/
```

`SNMP` Trap 由 `snmptrapd` 接收。为了将它们转发到 `snmptt`，在 `snmptrap.conf` 文件中输入以下内容：

```
# /etc/snmp/snmptrap.conf
trap default /usr/bin/snmptt
```

`snmp` 接受数字格式，这就是为什么 `snmptrap` 需要带有 `-O` 参数启动。根据发行版本，`snmptrap` 启动脚本可能需要调整。对于 Debian，`/etc/default/snmpd` 文件已相应修改：

```
# /etc/default/snmpd (Debian)
...
TRAPRUN=yes
TRAPOPTS='-ls -On -p /var/run/snmptrap.pid'
```

`-ls` 选项通过 syslog 记录所有。。你应该关闭它，将 `-ls` 替换为 `-t`。

### 23.7.1 配置文件 snmptt.ini

描述中央配置文件 `/etc/snmp/snmptt.ini` 的所有参数将超出本书的范围。我们只查看可以检查并可能需要调整的部分和选项：

```
[General]
mode = standalone
net_snmp_perl_enable = 1
mibs_environment = ALL
...
[Logging]
```

```ini
log_enable = 1
log_system_enable = 1
unknown_trap_log_enable = 1
syslog_enable = 1
syslog_level = warning

[trafiles]
snmptt_conf_files = <<END
/etc/snmptt/snmptt.conf
/etc/snmptt/messagebox.conf
END
```

`[General]` 节中的 `mode=standalone` 设置表示 `snmppd` 调用 `snmptt`。当使用 `mode=daemon` 时，`SNMPTT` 作为一个独立的守护进程运行。

`net_snmp_perl=1` 启用 Perl 模块 `SNMP`，它可以 OID 转换为有意义的文本。为了实现这一点，默认 0 禁用了此参数，而这显然是必要的。`mibs_environment=ALL` 集成了所有安装的 MIB。然而，这些 MIB 必须没有错误，对于发行版（例如 Debian 的 `mibs-base` 软件包）来说这是正常情况。

`[Trafiles]` 节中的参数 `snmp_conf_files` 包含配置文件列表，这些文件用于翻译传入的 SNMP traps 并在必要时触发操作。这些信息获取自设备的 MIB——具体方法请参见 [23.7.2 转换 MIB]。

`[Logging]` 节中的三个日志参数 `log_enable=1`、`log_system_enable=1` 和 `unknown_trap_log_enable=1` 确保 `SNMPTT` 将其活动记录到 `/var/log/snmptt*`，这在查找错误时非常有用。通过设置 `unknown_trap_log_enable=1` 记录未知陷阱，你可以发现 `SNMPTT` 没有翻译它收到的陷阱（例如，它包含了从 MIB 获取的配置文件中预期的其他 OID）。

两个 `syslog_*` 参数将翻译后的陷阱转发到 syslog 守护进程，并带有 `warning` 的 syslog 优先级，告知数据将出现在 `EventDB` 中。

`snmptt.ini` 以及与设备相关的配置文件中允许的参数在 `SNMPTT` 主页上有详细的文档说明。

### 23.7.2 转换 MIB

随附的程序 `snmpttconvertmib` 可将 MIB 转换为供 `SNMPTT` 使用的配置文件。转换器仅翻译通过 `snmptt_conf_files` 集成的配置文件显式列出的文件。
