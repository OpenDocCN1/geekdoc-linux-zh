
在安装 Samba 软件包并对可以实现的功能进行快速了解后，尝试设置 Samba 服务器，并查看默认配置下的效果。

# 启动和停止 Samba

安装 `samba` 和 `samba-common` 后，你可以启动并调查其在默认配置下的运行情况。Samba 服务器有两个主要的服务，每个服务都有自己的守护进程：

- `smb`：该服务控制 `smbd` 守护进程，它提供 Windows 客户端可以访问的文件共享服务。
- `nmb`：该服务控制 `nmb` 守护进程。通过提供 NetBIOS 服务名到地址的映射，`nmb` 可以映射来自 Windows 客户端对 NetBIOS 名称的请求，以便通过 IP 地址进行解析。

使用 Samba 共享文件和打印机，只需要 `smb` 服务。下一节介绍了如何启动和启用 Samba 服务。

## 启动 Samba (`smb`) 服务

`smb` 服务负责启动 `smbd` 服务，并将本地系统中的文件和打印机提供给网络上的其他计算机。按照习惯，Linux 系统上的服务启用和启动方式不同。对于不同的 Linux 系统，你需要找到服务的名称以及启动 `smbd` 守护进程的正确工具。

在 Fedora 和 RHEL 中，要让 Samba 在系统启动时立即启动，请在命令行输入：

```
# systemctl enable smb.service
# systemctl start smb.service
# systemctl status smb.service
smb.service - Samba Daemon
Loaded: loaded (/usr/lib/systemd/system/smb.service; enabled)
Active: active (running) since Fri 2020-01-31 07:23:37 UTC; 6s ago
Docs: man:smbd(8)
man:samba(7)
man:smb.conf(5)
Status: "smbd: ready to serve connections"
Tasks: 4 (limit: 12216)
Memory: 20.7M
Main PID: 4838 (smbd)
CGroup: /system.slice/smb.service
```

- 4838 /usr/sbin/smbd --foreground --no-process-group
- 4840 /usr/sbin/smbd --foreground --no-process-group

第一个 `systemctl` 命令启用服务，第二个启动它，第三个显示状态。若要进一步调查，请注意服务文件位于 `/usr/lib/systemd/system/smb.service`。查看其内容：

```
# cat /usr/lib/systemd/system/smb.service

[Unit]

Description=Samba SMB Daemon

Documentation=man:smbd(8) man:samba(7) man:smb.conf(5)

WantedBy=network-online.target

After=network-online.target network-online.target.service

[Service]

Type=notify

NotifyAccess=all

PIDFile=/run/smbd.pid

LimitNOFILE=16384

Environment=/etc/sysconfig/samba

ExecStart=/usr/sbin/smbd --foreground --no-process-group $SMBDOPTIONS

ExecReload=/bin/kill -HUP $MAINPID

LimitCORE=infinity

Environment=KRB5CC_NAME=file:/run/krb5cc_samba

[Install]

WantedBy=multi-user.target
```

Samba 守护进程 `smbd` 在网络、network-online、nmb 和 windbind target之后启动。`/etc/sysconfig/samba` 文件包含了在这些守护进程启动时作为参数传递的变量。默认没有设置任何选项。`WantedBy` 行表示任何 `smbd.service` 都应该在系统启动到多用户模式（`multi-user.target`）时启动，默认情况下确实如此。

在 RHEL 6 及更早版本中，你可以如下方式启动 Samba 服务：

```
# service smbd start
Starting SMB services: [ OK ]
# chconfig smbd on
# service smbd status
smbd (pid 28056) is running...
# chconfig -list smbd
smb 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

无论你是在 RHEL、Fedora 还是其他 Linux 系统上运行 Samba 服务器，可以使用 `smclient`（`samba-client` 软件包）检查对服务器的访问。你可以使用以下命令从服务器获取基本信息：

```
# smclient -L localhost
Enter Samba\root's password: <ENTER>
```

`smclient` 输出允许你查看服务器提供的服务。默认情况下，查询服务器时允许匿名登录（因此在提示密码时我按了回车）。

| Sharename | Type | Comment |
| --- | --- | --- |
| print$ | Disk | Printer Drivers |
| IPC$ | IPC | IPC Service |
| (Samba Version 4.10.10) | | |
| deskjet | Printer | workgroup |

你可以从此输出推断出关于默认 Samba 设置的一些信息：

- 通过 Linux 系统上的 CUPS 服务器共享的所有打印机默认也可以从同一系统的 Samba 服务器可用。
- 服务器尚未共享任何目录。
- 服务器尚未运行 NetBIOS 名称服务。

接下来，你可以决定是否要在 Samba 服务器上运行 NetBIOS 名称服务。

## 启动 NetBIOS (`nbmd`) 名称服务器

如果网络上没有运行 Windows 域（此处所示），你可以在 Samba 主机上启动 `nbmb` 服务来提供该服务。在 Fedora 或 RHEL 7 中启动 `nbmb` 服务（`nbmd` 守护进程），请输入：

```
# systemctl enable nbmb.service
# systemctl start nbmb.service
# systemctl status nbmb.service
```

在 RHEL 6 及更早版本中，你会输入以下内容启动名称服务：

```
# service nmb start
# service nmb status
# chkconfig nmb on
# chkconfig --list nmb
```

无论如何启动 NetBIOS 服务，`nbmd` 守护进程现在都应该运行并准备好提供 NetBIOS 名称到地址的映射。运行 `smclient -L` 命令，后跟服务器的 IP 地址。这次，输出的最后几行

## 第 19 章：配置 Windows 文件共享 (Samba) 服务器

输出应该显示从在 Samba 服务器上运行的 NetBIOS 服务器获取的信息。在这种情况下，最后几行看起来如下：

```
# smbclient -L localhost
...
Workgroup    Master
------------    ------
SAMBA        FEDORA30
```

你可以看到新生成的 NetBIOS 服务器的名称是 FEDORA30，并且它是该工作组（workgroup）的主服务器（master）。你可以查询 nmb 服务器以获取 FEDORA30 的 IP 地址，输入以下命令：

```
# nmblookup -U localhost FEDORA30
querying FEDORA30 on 127.0.0.1
192.168.122.81 FEDORA30<>
```
