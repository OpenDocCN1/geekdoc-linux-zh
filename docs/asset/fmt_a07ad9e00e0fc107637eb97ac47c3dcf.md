
## `chconfig` 使用说明

- `` `chconfig -list <service<name>>` `` 可能有助于列出多个匹配项（例如，“avahi-services”）
- `` `chconfig -level 35 <service<name>> on | off | reset` `` 优先级 - 影响级别 3 和 4
- `` `chconfig -level <service<name>> on` `` - 开启级别 2-5 中的服务，影响 0-6
- `` `chconfig -add OR -del` `` 从 `/etc/rc.d/init` 添加或删除
- `` `chconfig -override <service<name>>` `` - `/etc/sysconfig.d/<service<name>>` 文件可以覆盖 init 脚本

`sysv` 只是当前活动运行级别上的一个 Hat TUI 界面。守护进程有 `sysv-runlevel` (或 `-level 35`) 管理级别 3 和 5 的服务。`redhat-services` 或 `system-configs` - 图形服务配置工具

`/sbin/init` 指向 `/bin/init` - 用于切换服务的单字符参数 (0-6)，`s/all` 适用于单用户，`U/` 在不检查 initab 的情况下重启当前运行级别；`Q/q` 在检查 init 时这样做。二进制文件通过查看进程来检查自己是否为 init；真实进程的 id 总是 1。

- `/etc/init` 还会列出所有可用服务
- 用于启动和处理进程的脚本可以作为运行内核的替代方案。
- `sysv` 既启动也不停止服务 - 它规定运行级别。`service` 命令负责这一点。
- 服务立即受到 `sysv` 和其他单元的影响

| SysVRunlevel | 系统目标描述 |
| :--- | :--- | :--- |
| 0 | poweroff.target | 停止系统 |
| 1 | rescue.target | 单用户模式（所有内容已挂载，最小服务） |
| 2 | multi-user.target | 无网络的多用户模式 |
| 3 | multi-user.target | 带有网络的多用户模式 |
| 4 | multi-user.target | 用户可配置 |
| 5 | graphical.target | 用于 GUI (X11 多用户模式) |
| 6 | reboot.target | 重启系统 |

## `systemd` 的 `emergency.target`

- 类似于内核命令行上的 `init=/bin/sh`
- 没有对应的 `sysv-runlevel` - 它会在几乎不需要任何的情况下启动你的机器。
你将获得一个 shell，几乎没有其他东西（后台系统除外）。
- 没有启动服务，没有挂载点，没有建立套接字。
- 适用于独立启动特定脚本。
- 允许逐位启动，手动分步启动各种服务和其他单元。

在 `SysInit` 中，服务可以定义数组命令。例如 `service httpd graceful`。原生 `systemd` 没有这种能力。任何在此处中定义了额外命令的服务，在编写原生系统服务定义时，需要定义其他特定于服务的方法来实现此功能。检查特定包发布以查找可能执行过此操作的服务。

## systemd 单元脚本内容示例

不建议编辑 `/usr/lib/systemd/system/` 下的单元脚本，以便保持软件包的默认/安装状态。对于自定义更改，请将其复制到 `/etc/systemd/system/` 中编辑——此目录将为你覆盖默认设置。

示例单元脚本 - `/usr/lib/systemd/system/httpd.service` 内容：

```
[Unit]

Description=The Apache HTTP Server

After=network.target remote-fs.target nss-lookup.target

[Service]

Type=notify

EnvironmentFile=/etc/sysconfig/httpd

ExecStart=/usr/bin/httpd OPTIONS -D FOREGROUND

ExecReload=/usr/sbin/httpd OPTIONS -k graceful

ExecStop=/bin/kill -WINCH ${MAINPID}

KillSignal=SIGCNT

PrivateTmp=true

[Install]

WantedBy=multi-user.target
```

示例目标单元脚本 - `/usr/lib/systemd/system/multi-user.target` 内容：

```
[Unit]

Description=Multi-User System

Documentation=man:systemd.special(7)

Requires=basic.target

Conflicts=rescue.service rescue.target

After=basic.target rescue.service.target

AllIsolate=yes

[Install]

Alias=default.target
```

> "`After`" 是在此项激活完成后加载的内容
> "`Requires`" 应该是加载逻辑磁盘自动 `lvdisk.automount` 之前需要加载的内容

示例自定义挂载脚本 - `/etc/systemd/system/lvdisk.mount` 和 `lvdisk.automount`
需要一个同名的挂载文件和自动挂载文件（`mydisk5.automount mydisk5.mount`）
这可能是 RHEL 未来版本将通过这种方法进行自动挂载，而不是使用 `/etc/fstab` 方法

```
## vim /etc/systemd/lvdisk.mount

[Unit]

Description=Example test mount

[Mount]

what = /dev/vgdisk/lvdisk

where = /lvdisk

type = xfs

[Install]

WantedBy=multi-user.target
```

```
## vim /etc/systemd/lvdisk.automount

[Unit]

Description=Example test automount

[Automount]

where = /lvdisk

[Install]

WantedBy=multi-user.target
```
