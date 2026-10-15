
```
motd file = /etc/rsync.modt # 指定要显示的文件，法律
免责声明，等
max connections = 5      # 最大连接数，防止你被流量淹没
[pub-ftp]
    comment = public ftp area # 简单注释
    path = /home/ftp/pub     # 目录路径
    read only = yes          # 设置为只读，非常适合导出
    chroot = yes             # chroot 到 /home/ftp/pub
    uid = nobody             # 显式设置 UID
    gid = nobody             # 显式设置 GID
[secret]
    comment = my stuff # 我的东西的路径
    path = /home/user/secret
    list = no               # 在请求时隐藏此模块
    secrets file = /etc/rsync.users # 密码文件
    auth = bob   # 查看我内容的的用户列表
    hosts = 1.1.1.1, 2.2.2  # 允许的主机列表
```

如你所见，`rsync` 是可配置的且通常是，异常是实际传输没有以任何方式加密。如果你需要免费方案，建议使用 `SSH` 建立隧道连接，或者某些 VPN 解决方案如 WAN。还要确保你运行的是 `rsync 2.3.x`，或者在 2.2.x 中发现了潜在漏洞。`Rsync` 可以在此处获取：http://rsync.org/。`Rsync` 运行在端口 873`tcp`。

```
ipfwadm -I a accept -P tcp -S 10.0.0.0/8 -D 0.0.0.0/0 873
ipfwadm -I a accept -P tcp -S some.trusted.host -D 0.0.0.0/0 873
ipfwadm -I a deny -P tcp -S 0.0.0.0/0 -D 0.0.0.0/0 873
```

或者

```
ipchains -A input -p tcp -j ACCEPT -s 10.0.0.0/8 -d 0.0.0.0/0 873

ipchains -A input -p tcp -j ACCEPT -s some.trusted.host -d 0.0.0.0/0 873

ipchains -A input -p tcp -j DENY -s 0.0.0.0/0 -d 0.0.0.0/0 873
```

`lpd` 是 UNIX 的打印设施（打印守护进程）。它允许你提交打印作业、通过过滤器运行、管理打印队列等。`lpd` 可以在本地或通过网络接受打印作业，并访问系统的各个部分（守护进程等），这使其成为一个潜在的安全漏洞。`lpd` 曾是许多问题的根源，但现在大多已修复，由于其功能仍然存在潜在的拒绝服务攻击（例如提交打印作业和出纸）。随着网络打印机的出现，`lpd` 正在被逐渐淘汰，但 `lpd` 访问仍通过 `/hosts` 控制。你应该从外部对墙 `lpd`，如果你需要跨网络发送打印作业，请记住任何人都可以读取，因此 VPN 解决方案是一个好主意。`Lpd` 运行在端口 515`tcp`。`hosts` 文件应该包含一个主机列表（workstation1,yourdomain.com 等），每行一个允许使用服务器上 Lpd 服务的主机，你同样可以使用 `ipfwadm/ipchains`：

```
ipfwadm -I a accept -P tcp -S 10.0.0.0/8 -D 0.0.0.0/0 515

ipfwadm -A accept -P tcp -S some.trusted.host -D 0.0.0.0/0 515

ipfwadm -A deny -P tcp -S 0.0.0.0/0 -D 0.0.0.0/0 515
```

或者
```
ipchains -A input -p tcp -j ACCEPT -s 10.0.0.0/8 -d 0.0.0.0/0 515
ipchains -A input -p tcp -j ACCEPT -s some.trusted.host -d 0.0.0.0/0 515
ipchains -A input -p tcp -j DENY -s 0.0.0.0/0 -d 0.0.0.0/0 515
```

## LPRng

原生 `lpd` 的替代品是 “LPRng”（LPR 下一代），它提供了新的增强，并支持更高级别的安全。LPRng 支持 Kerberos 和 PGP 的身份验证，以及一个限制文件 `/etc/lpd.perms`，它允许你根据用户、组、IP 等控制访问，实现了极其灵活且安全的配置。LPRng 拥有完善的文档，可以在此处获取：http://www.astart.com/lpr/LPRng.html。

## pdq

`pdq` 是另一个 LPD 替代品，对增强安全没有真正的强调，但在管理和性能方面比原生 LPD 有一些改进。你可以从此处获取 `pdq`：http://feynman.tam.uiuc.edu/pdq/

## X Window System

X Window System 提供了一种共享数据的网络透明方法，具体说是将程序的导出到远程（本地）主机。使用它可以运行 3D 渲染。这是一个强大的工具，但也非常危险。X Window System 是许多漏洞的根源，但现在大多已修复，由于其功能仍然存在许多潜在的拒绝服务攻击。你应该从外部对 X 使用防火墙，如果你需要跨网络发送数据，请记住任何人都可以读取，因此 VPN 解决方案是一个好主意。X 运行在端口 6000`tcp`。`hosts.access` 文件应该包含一个主机列表（workstation1,yourdomain.com 等），每行一个允许使用服务器上 Lpd 服务的主机，你同样可以使用 `ipfwadm/ipchains`：

```
ipfwadm -I a accept -P tcp -S 10.0.0.0/8 -D 0.0.0.0/0 6000

ipfwadm -A accept -P tcp -S some.trusted.host -D 0.0.0.0/0 6000

ipfwadm -A deny -P tcp -S 0.0.0.0/0 -D 0.0.0.0/0 6000
```
