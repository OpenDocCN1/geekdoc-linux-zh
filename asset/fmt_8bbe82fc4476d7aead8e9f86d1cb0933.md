
`serverb.lab.example.com` `systemd[1]`: `httpd.service`: Failed with result 'exited'.

Failed to start Apache HTTP server

```
- 2. 使用 `sealert` 命令检查 SELinux 是否阻止了 `httpd` 服务绑定到 `1001/TCP` 端口。
```

```
[student@server ~]$ sudo sealert -a /var/log/audit.log
```

100% done

found 1 alerts in `/var/log/audit.log`

SELinux is preventing `/usr/sbin/httpd` from name_bind on the tcp_socket port `1001`.

*****

Plugin bind_ports (99% confidence) suggests

*****

Plugin catchall (49% confidence) suggests

*****

...output omitted...

```
# 第一章 | 管理网络安全

## 3. 配置 SELinux 以允许 `httpd` 服务监听 `1001/TCP` 端口。

### 3.1. 使用 `semanage` 命令找到正确的端口类型。

```
[student@server ~]$ sudo semanage port -l | grep 'http'
http_port_t      udp 80,8081,443,1001
http_port_t      tcp 80,8081,443,1001
```

### 3.2. 使用 `semanage` 命令将 `1001/TCP` 绑定到 `http_port_t` 类型。

```
[student@server ~]$ sudo semanage port -a -t http_port_t -p tcp 1001
[student@server ~]$
```

### 3.3. 确认 `1001/TCP` 已绑定到 `http_port_t`。

```
[student@server ~]$ sudo semanage port -l | grep 'http'
http_port_t      udp 80,8081,443,1001
http_port_t      tcp 80,8081,443,1001
```

### 3.4. 启用并启动 `httpd` 服务。

```
[student@server ~]$ sudo systemctl enable --now httpd
```

### 3.5. 验证 `httpd` 服务的运行状态。

```
[student@server ~]$ systemctl is-active httpd; systemctl is-enabled
active
enabled
```

### 3.6. 退出 `serverb`。

```
[student@server ~]$ exit
Connection to serverb closed.
[student@workstation ~]$
```

# 第二章 管理网络安全

## 4. 从工作站，测试对 `http://server.lab.example.com` 默认服务器以及 `http://server.lab.example.com:1001` 虚拟主机的访问。

### 4.1. 测试对 `http://server.lab.example.com` 服务器的访问。服务器应该返回 SERVER B。

```
[student@workstation ~]$ curl http://server.lab.example.com
SERVER B
```

### 4.2. 测试对 `http://server.lab.example.com:1001` 虚拟主机的访问。测试仍然失败。

```
[student@workstation ~]$ curl http://server.lab.example.com:1001
curl: (7) Failed to connect to server.lab.example.com port 1001: No route to host
```

## 5. 登录到服务器以确定防火墙是否分配了正确的端口。

### 5.1. 从工作站，以 `student` 用户身份登录服务器。

```
[student@workstation ~]$ ssh student@server
...output omitted...
[student@server ~]$
```

### 5.2. 验证默认防火墙区域设置为 `public`。

```
[student@server ~]$ firewall-cmd --get-default-zone
public
```

### 5.3. 如果上一步没有返回 `public` 作为默认区域，使用以下命令进行修正：

```
[student@server ~]$ sudo firewall-cmd --set-default-zone public
```

### 5.4. 确定 `public` 网络区域中列出的开放端口。

```
[student@server ~]$ sudo firewall-cmd --permanent --zone=public --nlist-all
public
target: default
icmp-block-inversion: no
interfaces:
sources:
services: cockpit dhcp6-client http ssh
ports:
protocols:
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

# 第二章 | 管理网络安全

## 6. 将端口 `1001/TCP` 添加到公共网络区域的永久配置中。确认你的配置。

### 6.1. 添加端口

```
[student@server ~]$ sudo firewall-cmd --permanent --zone=public \
--add-port=1001/tcp
success
```

### 6.2. 重载防火墙配置。

```
[student@server ~]$ sudo firewall-cmd --reload
success
```

### 6.3. 确认你的配置。

```
[student@server ~]$ sudo firewall-cmd --permanent --zone=public --list-all
public
target: default
icmp-block-inversion: no
interfaces:
sources:
services: cockpit dhcpv6-client http ssh
ports: 1001/tcp
protocols:
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

### 6.4. 退出 `serverb`。

```
[student@server ~]$ exit
logout
Connection to server closed.
[student@workstation ~]$
```

## 7. 从工作站，确认 `serverb.lab.example.com` 的默认 Web 服务器返回 SERVER B，且 `serverb.lab.example.com:1001` 的虚拟主机返回 VHOST 1。

### 7.1. 测试访问 `http://serverb.lab.example.com` Web 服务器。

```
[student@workstation ~]$ curl http://serverb.lab.example.com
SERVER B
```

### 7.2. 测试访问 `http://serverb.lab.example.com:1001` 虚拟主机。

```
[student@workstation ~]$ curl http://serverb.lab.example.com:1001
VHOST 1
```

# 评估

在工作站上，运行 `lab netsecurity-review grade` 命令以确认此实验实验练习是否成功。

```
[student@workstation ~]$ lab netsecurity-review grade
```

# 完成

在工作站上，运行 `lab netsecurity-review finish` 脚本以完成本次练习。

```
[student@workstation ~]$ lab netsecurity-review finish
```
