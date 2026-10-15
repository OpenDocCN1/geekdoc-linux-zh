
- 开发工具
- 图形管理工具
- 遗留 UNIX 兼容
- 科学支持
- 安全工具
- 卡支持
- 系统管理

注意，某些软件包组默认不显示。要显示这些组，请输入 `yum list hidden`。你看到的组列表要长得多。区别在于 `yum groups list` 显示的是环境组，它们包含基础功能。在环境组中，可以使用不同的子组；这些只有在使用 `yum list hidden` 时才会显示。

要获取组内可用软件包的信息，请使用 `yum groups info`。因为组名通常包含空格，请不要忘记将整个组名放在引号中。因此，输入 `yum groups info "Basic Web Server"` 来查看 `Basic Web Server` 组包含的内容。如列表 11.11 所示，此命令显示了组中的强制项和可选项。

# 270 红帽 RHCSA/RHCE 7 认证指南

`directory-client`

`+guest-agents`

`+hardware-monitoring`

`+java-platform`

`+large-systems`

`+load-balancer`

`+mariadb-client`

`+network-file-system-client`

`+performance`

`+perl-web`

`+php`

`+postgresql-client`

`+python-web`

`+remote-system-management`

`+web-servlet`

# 使用 yum 历史

在使用 `yum` 期间，所有操作都会记录在 `/var/log/yum.log` 文件中。你可以使用 `yum history` 命令来获取已执行操作的概览。从历史文件中，可以撤销特定的操作；使用 `yum undo` 后跟你想要撤销的特定操作编号。

在列表 11.12 中，你看到了 `yum history` 命令的输出，每个操作都有自己的 ID。

# 列表 11.12 使用 yum history 显示过去的 yum 操作

```
root@localhost ~]# yum fastmirror
Loaded plugins: fasttestmirror
```

| ID | 登录用户 | 日期和时间 | 操作 | 更改 |
|---|---|---|---|---|
| 14 | root <root> | 2015-02-10 04:07 | I, U | 80 |
| 13 | root <root> | 2015-02-10 03:48 | Install | 2 |
| 12 | root <root> | 2015-01-23 12:29 | Install | 1 |
| 11 | root <root> | 2015-01-23 12:17 | I, U | 4 |
| 10 | root <root> | 2015-01-19 05:35 | Install | 2 |
| 9 | root <root> | 2015-01-19 02:53 | Install | 1 |
| 8 | root <root> | 2015-01-18 05:14 | Install | 3 |
| 7 | root <root> | 2015-01-17 13:47 | Install | 30 |
| 6 | root <root> | 2015-01-17 11:40 | Install | 5 |

# 第 11 章：管理软件 271

| 5 | root <root> | 2015-01-11 10:19 | Install | 1 |
| 4 | root <root> | 2015-01-09 17:36 | I, U | 8 |
| 3 | root <root> | 2015-01-09 17:30 | Install | 1 |
| 2 | root <root> | 2015-01-09 17:22 | Install | 1 |
| 1 | System <unset> | 2014-10-03 02:17 | Install | 297 |

```
history list
```
