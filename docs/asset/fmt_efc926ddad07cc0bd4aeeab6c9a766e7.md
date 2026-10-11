
`update-rc.d`: We have no instructions for the apt-cacher-ng init script.

`update-rc.d`: It looks like a network service, we disable it.

...

`root@kali:~#`

注意看 `update-rc.d` 脚本如何默认禁用 `apt-cacher-ng` 守护进程的持久化。

## 服务启动

在某些情况下，我们确实希望某些服务在重启后持续存在。为了实现这一点，可以使用 `update-rc.d` 脚本按如下启用服务的重启持久化：

```
root@kali:~# update-rc.d apt-cacher-ng enable

update-rc.d: using dependency based boot sequencing
```

### 服务白名单和黑名单

服务白名单和黑名单可以在 `/usr/sbin/update-rc.d` 文件中找到。通过该文件，你可以显式允许或拒绝服务以其默认状态自动启动。

```
root@kali:~# tail -95 /usr/sbin/update-rc.d |more

}

__DATA___

## List of blacklisted init scripts

#
apache2 disabled
avahi-daemon disabled
bluetooth disabled
cups disabled
dictd disabled
ssh disabled
...

## List of whitelisted init scripts

#
acpid enabled
acpi-fakeakeey enabled
acpi-support enabled
alsa-utils enabled
anacron enabled
...
```

# KALI LINUX

官方 Kali Linux 文档
此 PDF 已在 `docs.kali.org` 上自动生成 - 2013 年 8 月 19 日

# Kali Linux 安全更新策略

Kali Linux 与 Debian 仓库紧密结合，因此对于 Kali 保持未更改的所有软件包（即绝大多数），其接收安全更新的频率与 Debian 主发行版完全一致。其他软件包由 Kali 团队尽力而为（best-effort basis）提供支持。

```
