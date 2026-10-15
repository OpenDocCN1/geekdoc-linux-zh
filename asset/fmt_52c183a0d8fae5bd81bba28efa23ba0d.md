
`/etc/rc`

`/etc/rc.local`

`/etc/rc.serial`

（以及可能的其他文件）

最近，某些 BSD 系统初始化方案使用 `/etc/rc.d...`目录来存放启动文件，而不是将所有内容都放在 `/etc` 中。

System V 初始化将其初始化文件放在 `/etc/...` 或 `/etc/rc.d/` 目录以及以下的一若干子目录下：

```
rwxr-xr-x 2 root root 1024 Jul 6 15:12 init.d

rwxr-xr-x 1 root root 1776 Feb 2 05:01 rc

rwxr-xr-x 1 root root 820 Jan 2 1996 rc.local

rwxr-xr-x 1 root root 2567 Jul 5 20:30 rc.sysinit

rwxr-xr-x 2 root root 1024 Jul 6 15:12 rc0.d
```
