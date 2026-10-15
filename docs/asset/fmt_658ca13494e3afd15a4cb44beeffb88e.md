
连接从 `gateA` 发起，命令在 `gateB` 上执行。

### `gateB` 在 Linux 上

```
gateA# ssh -w5:5 root@gateB
gateB# ifconfig tun5 10.0.0.1 netmask 255.255.255.252  # Executed on the gateB shell
gateB# route add -net 192.168.51.0 netmask 255.255.255.0 dev tun5
gateB# echo 1 > /proc/sys/net/ipv4/ip_forward      # Only needed if not default gw
gateB# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

### `gateB` 在 FreeBSD 上

```
gateA# ssh -w5:5 root@gateB      # Creates the tun5 devices
gateB# ifconfig tun5 10.0.0.1 10.0.0.2   # Executed on the gateB shell
gateB# route add 192.168.51.0/24 10.0.0.1,2
gateB# sysctl net.inet.ip.forwarding=1   # Only needed if not default gw
gateB# natd -s -m -u -dynamic -n fxp0    # see NAT (page 17)
gateB# sysctl net.inet.ip.fw.enable=1
```

### 配置 `gateA`

在 `gateA` 上执行的命令：

#### `gateA` 在 Linux 上

```
gateA# ifconfig tun5 10.0.0.2 netmask 255.255.255.252
gateA# route add -net 192.168.16.0 netmask 255.255.255.0 dev tun5
gateA# echo 1 > /proc/sys/net/ipv4/ip_forward
gateA# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

#### `gateA` 在 FreeBSD 上

```
gateA# ifconfig tun5 10.0.0.2 10.0.0.1
gateA# route add 192.168.16.0/24 10.0.0.1,2
gateA# sysctl net.inet.ip.forwarding=1
gateA# natd -s -m -u -dynamic -n fxp0      # see NAT (page 17)
gateA# sysctl net.inet.ip.fw.enable=1
```

两个私有网络现在已通过 SSH VPN 透明连接。IP 转发和 NAT 设置只有在网关不是默认网关时才有必要。在这种情况下客户端将不知道如何转发响应，并且必须激活 `nat`。

## 7 RSYNC

`Rsync` 几乎可以完全取代 `cp` 和 `scp`，而且中断的传输可以高效地重新开始。尾部斜杠的存在与否具有不同的含义，`man` 手册很不错……这里有一些示例：

复制目录及其完整内容：

```
# rsync -a /home/colin/ /backup/colin/      # "archive" mode. e.g keep the same
# rsync -a /var/ /var_bak
# rsync -aR --delete --during /home/user/ /backup/   # use relative (see below)
```

与之前相同但通过网络并使用压缩。`Rsync` 默认使用 `SSH` 进行传输，如果已设置则会使用 `ssh` 密钥。使用与 `SCP` 相同的方式 "..."。典型的远程复制：

```
# rsync -axSzrv /home/user/ user@server:/backup/user/   # Copy to remote
# rsync -a 'user@server:My\ Documents' 'My\ Documents'   # Quote AND escape spaces for the remote sh
```

排除 `/home/user/` 内的任何 `tmp` 目录并保持相对文件夹层次结构，即远程目录将具有结构 `/backup/home/user/`。这通常用于备份。

```
# rsync -aZR --exclude=tmp/ /home/user/ user@server:/backup/
```

### 使用端口 20022 进行 ssh 连接：

```
# rsync -az -e 'ssh -p 20022' /home/colin/ user@server:/backup/colin/
```

使用 `rsync` 守护进程（使用“:”）速度要快得多，但不会通过 `ssh` 加密。`/backup` 的位置由 `/etc/rsyncd.conf` 中的配置定义。变量 `RSYNC_PASSWORD` 可以设置以避免手动输入密码的需要。

### — RSYNC —

```
# rsync -axSRz /home/ ruser@hostname::rmodule/backup/
# rsync -axSRz ruser@hostname::rmodule/backup/ /home/    # To copy back
```

一些重要选项：

+   `-a`, `--archive`      archive mode; same as `-rlptgoD` (no `-H`)
+   `-r`, `--recursive`    recurse into directories
+   `-R`, `--relative`     use relative path names
+   `-H`, `--hard-links`   preserve hard links
+   `-S`, `--sparse`       handle sparse files efficiently
+   `-x`, `--one-file-system`  don't cross file system boundaries
+   `--exclude=PATTERN`  exclude files matching PATTERN
+   `--delete-during`    receiver deletes during xfer, not before
+   `--delete-after`     receiver deletes after rtransfer, not before

## 7.1 Windows 上的 Rsync

`Rsync` 可通过 `cygwin` 在 Windows 上使用，或作为独立软件包打包在 `cwrsync`¹³ 中。这对于自动备份非常方便。安装其中之一（不要同时安装两个）并将路径添加到 Windows 系统变量中：# 控制面板 -> 系统 -> 高级选项卡，按钮 环境变量。编辑“Path”系统变量并添加已安装 `rsync` 的完整路径，例如 `C:\Program Files\cwRsync\bin` 或 `C:\cygwin\bin`。这样 `rsync` 和 `ssh` 命令就可以在 Windows 命令 shell 中使用。

### 公钥认证

`Rsync` 自动通过 `SSH` 隧道传输，因此使用服务器上的 `SSH` 认证。自动备份必须避免用户交互，为此可以使用 `SSH` 公钥认证，`rsync` 命令将无需密码运行。

以下所有命令都在 Windows 控制台中执行。在控制台中（开始 -> 运行 -> `cmd`）按 `SSH` 中所述创建并上传密钥，并根据需要更改“user”和“server”。如果文件 `authorized_keys2` 尚不存在，只需将 `id_dsa.pub` 复制到 `authorized_keys2` 并上传即可。

```
# ssh-keygen -t dsa -N ''          # Creates a public and a private key
# rsync user@server:.ssh/authorized_keys2 .  # Copy the file locally from the server
# cat id_dsa.pub >> authorized_keys2  # Or use an editor to add the key
# rsync authorized_keys2 user@server:.ssh/  # Copy the file back to the server
# del authorized_keys2               # Remove the local copy
```

现在用以下命令测试（在一行中）：
