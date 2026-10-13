
# 综合回顾

`/usr/bin/ssh-copy-id`: INFO: Source of key(s) to be installed: `/home/`

`production5/.ssh/rsa.pub`

无法建立 `server (172.25.20.11)` 的真实性。
ECDSA 指纹为 `SHA256:cickRA4f6E9rsWdpQ7LbcpZv1Al6BousKS4KTY`
确定你要继续连接吗？(yes/no) yes
`/usr/bin/ssh-copy-id`: INFO: attempting to log in with the new key(s), to filter out that are already installed
`/usr/bin/ssh-copy-id`: INFO: 1 key(s) remains to be installed - if you prompted now it is to install the new keys
`production5@server's password`: `redhat**`

添加的密钥数量： 1

现在尝试使用 `"ssh production5@server"` 登录机器，
并检查是否只添加了你需要的密钥。

## 5.5. 使用 SSH 密钥认证代替密码认证来以 production5 用户身份登录服务器。此命令应该失败。

```
[production ~] ssh -o authentication=yes \
-o password=no production5@server
```

`production5@server`: Permission denied (`publickey,gssapi-keyex,gssapi-mic,password`).

## 5.6. 在连接到服务器的 root 用户终端机上，将 use_home_dirs SELinux 布尔值设置为 true。

```
[root@server ~] setsebool -P nfs_home_dirs true
```

## 5.7. 返回到以 production5 用户连接到服务器的终端，使用 SSH 密钥认证代替密码认证来以 production5 用户身份登录服务器。此命令应该成功。

RHI34-RHEL9.0-en-2-20220609

## 第 12 章 | 综合回顾

```
[production5@server ~$ ssh -o pubkeyauthentication=yes \
--o passwordauthentication=no production5@server \
--output omitted.
[production5@server ~$]
```

- 5.8. 退出并关闭以 production5 用户连接到服务器的终端。保持以 root 用户连接到服务器的终端。

- 6. 在服务器上，调整防火墙设置以拒绝所有源自服务器机器的连接请求。调整服务器 IPv4 地址 (`172.25.250.100`) 以配置防火墙规则。

### 6.1. 将服务器的 IPv4 地址添加到块区域（block zone）。

```
[root@server #] firewall-cmd --add-source=172.25.250.10/32 \
--zone=block permanent
success
```

### 6.2. 重新加载防火墙设置的更改。

```
[root@server #] firewall-cmd --reload
success
```

- 7. 在服务器上，调查并修复失败的 Apache Web 服务问题，该服务监听 `30800/TCP` 端口连接。适当调整防火墙设置，使 `30800/TCP` 对传入连接开放。

### 7.1. 重启 httpd 服务。此命令重启服务失败。

```
[root@server #] systemctl restart httpd.service
Job for httpd.service failed because the control process exited with error code.
请通过 "systemctl status httpd.service" 和 "journalctl -xeu httpd.service" 查看详情。
```

### 7.2. 调查 httpd 服务失败的原因。权限错误表明 httpd 守护进程在启动时未能绑定到 `30800/TCP` 端口。SELinux 策略阻止应用程序绑定到非标准端口。按 q 退出命令。

```
[root@server #] systemctl status httpd.service
× httpd.service - The HTTP Server
Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
Active: Failed (Result: exit-code) since 2022-05-02 13:20:46 EDT; 29s ago
ocs: man httpd.service(8)
Process: 2322 ExecStart=/usr/sbin/httpd -DFOREGROUND OPTIONS (code=exited, status=1/FAILURE)
Main PID: 2322 (code=exited)
Status: 1/FAILURE
Starting: Reading configuration...
```

第 12 章 | 综合回顾

```
[production5@server ~$ ssh -o pubkeyauthentication=yes \
--o passwordauthentication=no production5@server \
--output omitted.
[production5@server ~$]
```

- 5.8. 退出并关闭以 production5 用户连接到服务器的终端。保持以 root 用户连接到服务器的终端。

- 6. 在服务器上，调整防火墙设置以拒绝所有源自服务器机器的连接请求。调整服务器 IPv4 地址 (`172.25.250.100`) 以配置防火墙规则。

### 6.1. 将服务器的 IPv4 地址添加到块区域。

```
[root@server #] firewall-cmd --add-source=172.25.250.10/32 \
--zone=block permanent
success
```

### 6.2. 重新加载防火墙设置的更改。

```
[root@server #] firewall-cmd --reload
success
```

- 7. 在服务器上，调查并修复失败的 Apache Web 服务问题，该服务监听 `30800/TCP` 端口连接。适当调整防火墙设置，使 `30800/TCP` 对传入连接开放。

### 7.1. 重启 httpd 服务。此命令重启服务失败。

```
[root@server #] systemctl restart httpd.service
Job for httpd.service failed because the control process exited with error code.
请通过 "systemctl status httpd.service" 和 "journalctl -xeu httpd.service" 查看详情。
```

### 7.2. 调查 httpd 服务失败的原因。权限错误表明 httpd 守护进程在启动时未能绑定到 `30800/TCP` 端口。SELinux 策略阻止应用程序绑定到非标准端口。按 q 退出命令。

```
[root@server #] systemctl status httpd.service
× httpd.service - The HTTP Server
Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
Active: Failed (Result: exit-code) since 2022-05-02 13:20:46 EDT; 29s ago
ocs: man httpd.service(8)
Process: 2322 ExecStart=/usr/sbin/httpd -DFOREGROUND OPTIONS (code=exited, status=1/FAILURE)
Main PID: 2322 (code=exited)
Status: 1/FAILURE
Starting: Reading configuration...
```
