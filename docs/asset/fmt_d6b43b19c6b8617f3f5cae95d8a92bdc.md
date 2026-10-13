
## 5. 配置 `serverb`，当 `production5` 用户登录时，使用网络文件系统 `/home-directories/production5` 自动挂载其主目录。该网络文件系统从 `servera.lab.example.com` 导出。调整适当的 SELinux 布尔值，使得 `production5` 在通过 SSH 密钥身份验证后可以使用通过 NFS 挂载的主目录。`production5` 用户的密码为 `redhat`。

### 5.1. 在服务器上，使用 `sudo -i` 命令切换到 root 用户账号。

```
[student@serverb ~]$ sudo -i
[sudo] password for student: student
[root@serverb ~]#
```

### 5.2. 安装 `autofs` 包。

```
[root@serverb ~]# yum install autofs
...output omitted.
Is this ok [y/N]: y
...output omitted...
Installed:
autofs-1:5.1.4-29.el8.x64
Complete!
```

### 5.3. 创建包含以下内容的 `autofs` 主映射表文件 `/etc/auto.master.d/production5.autofs`。

```
/etc/auto.master
```

### 5.4. 创建包含以下内容的 `/etc/auto/production5` 文件。

```
/production5 -rw servera.example.com:/home-directories/production5
```

### 5.5. 重启 `autofs` 服务。

```
[root@serverb ~]# systemctl restart autofs
```

## 6. 在 `servera` 上，验证 `production5` 用户无法通过 SSH 登录 `serverb`。SELinux 布尔值导致了此问题，你将通过以下步骤修复：

### 6.1. 从工作站以 `student` 身份登录 `servera`。

```
[student@workstation -]$ ssh student@servera
...output omitted...
```

### 6.2. 使用密码 `redhat` 切换到 `production5` 用户。

```
[student@servera -$] su production5
Password: redhat
```

### 6.3. 以 `production5` 身份使用 `ssh-keygen` 命令生成 SSH 密钥。

```
[production5@servera -$] ssh-keygen
Generating public/private rsa key pair.
Enter file where to save the key (/home/student/.ssh/id_rsa): Enter
Created directory '/home/student/.ssh'.
Enter passphrase (empty for no passphrase): Enter
Enter passphrase again: Enter
Your identification has been saved in /home/student/.ssh/id_rsa.
Your public key has been saved in /home/student/.ssh/id_rsa.pub.
Your key fingerprint is:
SHA256:i1TP2ZTYXwiLGfXuGTHfqQBF9hVuLa+Vmm4kGFKYKY
student@serverb.example.com
The key's fingerprint image is:
```

```
+-[RSA 2048]-+
|  +B0*|
|      =#B|
|    X.*o=|
|    E,++|
|  S o   +
|    + 0 = |
|  0 0 ++|
|      |
+-[SHA256]------+
```

### 6.4. 使用 `ssh-copy-id` 命令将 `production5` 的 SSH 密钥对的公钥传输到服务器上的 `production5`。如果提示，使用 `production5` 用户的密码。

```
[production5@server]$ ssh-copy-id production5@server
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/production5/.ssh/id_rsa.pub"
The authenticity of host 'server (172.25.250.10)' can't be
established.
ECDSA fingerprint is SHA256:cickaRnWF4eR9sdPxQ7Lkcpival6B
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copyid INFO: attempting to log in with the new key,
to filter out any that are already installed
/usr/bin/ssh-copyid INFO: 1 key(s) remains to be installed - if you
are prompted it to install the new keys
production5@server's password: redhat
```

Number of key(s) added: 1

现在使用 "`ssh production5@server`" 登录机器，并检查所需的密钥已添加。

### 6.5. 使用 SSH 公钥身份验证而非密码身份验证登录 `server production5`。此命令应该失败。

```
[production5@server]$ ssh -o pubkeyauthentication=yes
-o passwordauthentication=no production5@server
production5@server: Permission denied (publickey,gssapi-key,gssapi,password).
```

## 7. 在服务器上设置适当的 SELinux 布尔值，使得 `production5` 可以使用 SSH 公钥身份验证登录服务器并使用主目录。

### 7.1. 在服务器上，以 root 身份将 `use_nfs_home_dirs` SELinux 布尔值设置为 `true`。

```
[root@server]$ setsebool -P use_nfs_home_dirs true
```

### 7.2. 使用 SSH 公钥身份验证而非密码身份验证登录 `server production5`。此命令应该成功。

```
[production5@server]$ ssh -o pubkeyauthentication=yes
-o passwordauthentication=no production5@server
...output omitted...
[production5@server]$
```

## 8. 在服务器上调整防火墙设置，拒绝来自 `servera` 的 SSH 连接。服务器使用 IPv4 地址 `172.25.250.10`。

### 8.1. 使用 `firewall-cmd` 将 `servera` 的 IPv4 地址添加到防火墙的 `block` 区域。

```
root@server # firewall-cmd --add-source=172.25.250.10/32 \
--zone=block --permanent
```

### 8.2. 使用 `firewall-cmd --reload` 重新加载更改。

```
root@server # firewall-cmd --reload
```

## 9. 在服务器上，调查并修复 Apache HTTPD 守护进程的问题。该进程被配置为监听端口 `30080/TCP`，但无法启动。适当调整防火墙设置，使端口 `30080/TCP` 允许入站连接。

### 9.1. 使用 `systemctl` 命令重启 `httpd` 服务。此命令重启失败。

```
root@server # systemctl restart httpd
Job for httpd.service failed the control process exited with error code.
```
