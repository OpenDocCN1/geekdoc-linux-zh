
```
[user@server1 ~]$ systemctl -t socket --all
UNIT                     SUB STATE      DESCRIPTION
avahi-daemon.socket      active running    AVAH/DNS/mDNS Stack Activation Socket
dbus.socket             active running    CUPS Scheduler
de-event.socket          active running    System Message Box Socket
iscdd.socket            active running    Listening-wrapper event daemon FIFs
isiscid.socket           active running    Listening Open-ISCD Socket
lmv2-ipvold.socket      active running    Listening LMDB daemon socket
multipath.socket        active running    listening multipath socket
richting.socket         active running    Routing Backend Activation
spice-vdns.socket      active running    Activation socket for guest agent S
sssd-kcm.socket          active active    SSSD Kerberos Cache responder S
syslog.socket           inactive dead   Syslog Socket
-.mount                               loaded active  Root Boot
boot.mount                         loaded active  Root Boot
dev-bugpages.mount                 loaded active  Page System
mnt.mount                          loaded active  Message Queue
```

# 列出上次系统启动时启动失败（--failed）的所有单元

```
[user@server1 ~]$ systemctl --failed
UNIT LOAD ACTIVE SUB DESCRIPTION
* vbox-service.service loaded failed failed vbox-service.service
* vbox.service loaded failed failed vbox.service
```

`LOAD` = 反映定义是否已正确加载。

`ACTIVE` = 高层单元激活状态，即 `SUB` 的泛化。

`SUB` = 低层单元激活状态，其值取决于单元类型。

列出了 2 个已加载的单元。使用 `--all` 也可以查看已加载但未激活的单元。

使用 `systemctl list-unit-files` 显示所有已安装的单元。

# 列出当前默认目标的所有依赖项的层级结构

```
[user@server1 ~]$ systemctl list-dependencies
default.target
  * accounts-daemon.service 
    * dbus.service
    * polkit-daemon.service
    * systemd2-update-utamp-runlevel.service
    * udev2.service
    * multi-user.target
      * atd.service
      * auditd.service
```

# 列出特定单元的所有依赖项的层级结构

```
[user@server1 ~]$ systemctl list-dependencies atd.service
atd.service
  * system.slice
    * sysinit.target
    * -dev-hugepages.mount
    * -dev-queue.mount
    * dracut-shutdown.service
    * import-state.service
    * lscsi.service
```

还有其他列出子命令和额外的标志可用于生成各种报告。

# 管理服务单元

`systemctl` 命令提供了多个子命令来管理服务单元，包括启动、停止、重启和检查它们的状态。这些和其他管理操作总结在表 12-3 中。以下示例了它们在名为 `atd` 的服务单元上的用法。

## 检查 atd 服务的运行状态和其他细节

```
[user@server1 (running) -] systemctl status atd
* atd.service - Job spool tools
Loaded: loaded (/usr/lib/systemd/system/atd.service; enabled; vendor preset: enabled)
Active: active (running) since Wed 2019-10-09 07:42:00 EDT; 1 day 4h
Main PID: 942 (atd)
Tasks: 1 (limit: 5064)
Memory: 496.0K
ControlGroup: /system.slice/atd.service
└942 /usr/sbin/atd -f
```

上述输出显示了许多关于 `atd` 服务的信息。第 1 行显示服务的描述（从 `/usr/lib/systemd/system/atd.service` 文件读取）。第 2 行说明了加载状态，显示了内存中单元文件的当前加载状态。`Loaded` 的其他可能包括 `error`（如果加载文件出现问题）、`not-found`（如果未找到与单元关联的文件）、`bad-setting`（如果缺少关键设置）和 `masked`（如果单元文件被掩蔽）。第 2 行还告诉该服务是否设置为系统启动时自动启动（启用或禁用）。

第 3 行显示了当前的激活状态和服务的启动时间。激活状态指定了服务的当前状态。可能的状态包括：

- `Active (running)`: 服务正在运行一个或多个进程运行
- `Active (exited)`: 完成了一次性配置
- `Active (waiting)`: 正在运行但正在等待事件
- `Inactive`: 未运行
- `Activating`: 正在激活过程中
- `Deactivating`: 正在去激活过程中
- `Failed`: 如果服务崩溃或无法启动

输出还描绘了服务进程的 PID 和其他信息。

## 在下次系统重启动时禁用 atd 服务自动启动

```
[user@server1 ~]$ sudo systemctl disable atd
Removed /etc/systemd/system/multi-user.target.wants/atd.service.
```

## 在下次系统重启动时重新启用 atd 自动启动

```
[user@server1 ~]$ sudo systemctl enable atd
Created symlink /etc/systemd/system/multi-user.target.wants/atd.service → /usr/lib/system/atd.service.
```

## 检查 atd 是否设置为下次系统重启动时自动启动

```
[user@server1 ~]$ systemctl is-enabled atd
enabled
```

## 检查 atd 服务是否正在运行

```
[user@server1 ~]$ systemctl is-active atd
active
```

## 停止并重启 atd

```
[user@server1 ~]$ sudo systemctl stop atd ; sudo systemctl start atd
[user@server1 ~]$ sudo systemctl restart atd
```

## 显示 atd 服务的细节

```
[user@server1 ~]$ systemctl show atd
Type=simple
Restart=no
NotifyAccess=none
RestartUSSec=100ms
```

禁止启用或禁用 `atd`：
