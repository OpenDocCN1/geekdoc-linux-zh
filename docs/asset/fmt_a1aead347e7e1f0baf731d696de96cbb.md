
| Automount | `.automount` | 文件系统自动挂载点。 |
| Device | `.device` | 内核识别的设备文件。 |
| Mount | `.mount` | 文件系统挂载点。 |
| Path | `.path` | 文件系统中的文件或目录。 |
| Scope | `.scope` | 外部创建的进程。 |
| Slice | `.slice` | 管理系统进程的层级组织单元组。 |
| Snapshot | `.snapshot` | `systemd` 管理器的保存状态。 |
| Socket | `.socket` | 进程间通信套接字。 |
| Swap | `.swap` | 交换设备或交换文件。 |
| Timer | `.timer` | `systemd` 定时器。 |

表 11-1

请注意，目标单位类型与其他类型不同，因为它包含一组 `systemd` 单位
such as services or other targets.

## 11.6 Dynamically Changing the Current Target

The `systemctl set-default` command outlined previously specifies the target that will be used the next time the system starts but does not change the current system's state. To change to a different target dynamically, use the `systemctl` command again, using the `isolate` option followed by the destination target. To switch the current system to the graphical target without rebooting, for example, the following command would be used:

```
# systemctl isolate graphical.target
```

Once executed, the system will start the graphical desktop environment.

## 11.7 Enabling, Disabling, and Masking systemd Units

A newly installed RHEL 9 system will include the base `systemd` service units but is unlikely to include all the services the system will eventually need once it goes into a production environment. A basic RHEL 9 installation, for example, will typically not include the packages necessary to run an Apache web server, a key element of which is the `httpd.service` unit.

The system administrator will resolve this problem by installing the necessary `httpd` packages using the following command:

```
# dnf install httpd
```

Having configured the web server, the next task will be to check the status of the `httpd` service unit to identify whether it was activated as part of the installation process:

```
# systemctl status httpd.service
httpd.service - The Apache HTTP Server
  Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
  Active: inactive (dead)
  Docs: man:httpd.service(8)
```

Note that the service has loaded but is inactive because it is preset by the vendor to be disabled when first installed. To start the service, the following command can be used:

```
# systemctl start httpd.service
```

A status check will now indicate that the service is active:

```
# systemctl status httpd.service
httpd.service - The Apache HTTP Server
  Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
  Active: active (running) since Fri 2019-02-15 11:13:26 EST; 8s ago
  Docs: man:httpd.service(8)
Main PID: 10721 (httpd)
  Status: "Started, listening on: port 80"
  Tasks: 213 (limit: 13923)
Memory: 24.1M
```

### Managing RHEL 9 systemd Units

Note, however, that the status indicates that the service is still disabled. This means that the next time the system reboots, the `httpd` service will not start automatically and will need to be started manually by the system administrator.

To configure the `httpd` service to start automatically each time the system starts, it must be enabled as follows:

```bash
# systemctl enable httpd.service
```

Once the service has been enabled, the Loaded section of the status output will read as follows:

```
Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
```

```bash
# systemctl status httpd.service
● httpd.service - The Apache HTTP Server
    Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
    Active: active (running) since Thu 2023-03-30 09:04:21 EDT; 2min 17s ago
    Docs: man:httpd.service(8)
  Main PID: 4500 (httpd)
    Status: "Total requests: 0; Idle/Busy workers 100/0;Requests/sec: 0; Bytes served/sec: 0 B/sec"
    Tasks: 213 (limit: 22087)
    Memory: 35.4M
```

A currently running service may be stopped at any time as follows:

```bash
# systemctl stop httpd.service
```
