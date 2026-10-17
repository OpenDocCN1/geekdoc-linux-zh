
; `path` = `/home/samba` `public` = `yes`

; `writable` = `yes`

; `printable` = `no`

; `write list` = `@staff`

## 其他示例。

### 一个私有打印机，仅供 `fred` 使用。打印数据将存放在 `fred` 的目录中。注意 `fred` 必须对所在的 位置具有写入权限。

```
; [fredsprn]
; comment = Fred 的打印机
; valid users = fred
; path = /homes/fred
; printer = freds_printer
; public = no
; printable = yes
```

### 一个私有目录，仅供 `fred` 使用。注意 `fred` 需要对该 目录具有写入权限。

```
;[freddir]
; comment = Fred 的服务
; path = /usr/somewhere/private
; valid users = fred
; public = no
; writable = yes
; printable = no
```

### 一种为每个连接的机器提供不同目录的服务，这允许你为接入的机器定制配置。你还可以 使用 `%u` 选项根据用户名进行定制。 `%m` 将被替换为正在连接的机器名称。

`482` 第 8 章：网络客户端服务

图 8-30 Red Hat 7.1 的主 Samba 配置文件 `/etc/samba/smb.conf` （更有趣的特性已加粗）（续续）

```
[pchome]
; comment = PC 目录
; path = /usr/pc/%m
; public = no
; writable = yes
```

### 一个公共可访问的目录，所有用户均可读/写。注意 用户在目录中创建的所有文件将归默认用户 所有，任何具有访问权限的用户都可以删除其他用户的文件。显然， 此目录必须允许默认用户写入。当然，也可以指定 其他用户，在这种情况下，所有文件将由该用户所有。

```
[public]
; path = /usr/somewhere/else/public
; public = yes
; only guest = yes
; writable = yes
; printable = no
```

### 以下两个项目演示了如何共享目录，以便两个 用户可以放置文件，且这些文件将属于特定的用户。 在此设置中，目录应该允许两个用户写入，并 应该对其设置粘滞位（sticky bit）以防止滥用。显然，这可以 扩展到所需的任何数量的用户。

```
[mshare]
; comment = Mary 和 Fred 的东西
; path = /usr/somewhere/shared
; valid users = mary fred
; public = no
; writable = yes
; printable = no
; create mask = 0765
```
