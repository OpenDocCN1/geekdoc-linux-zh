
`[user01@remotehost ~$] ls -l /etc/ssh/*key.pub`

`/etc/ssh/ssh_host_ecdsa_key.pub /etc/ssh/ssh_host_ed25519_key.pub /etc/ssh/`
`_host_rsa_key.pub`

```
> 注意
将与服务器的 `ssh_host_*.key.pub` 文件匹配的条目添加到你的 `~/.ssh/known_hosts` 文件或系统范围的 `/etc/ssh/ssh_known_hosts` 文件是一个良好的做法。
```

## 参考文献

`ssh(1)`, `w(1)` 和 `hostname(1)` 手页
更多信息请参阅 Red Hat Enterprise Linux 8.0 BETA 配置与管理安全指南中的“Using Secure Communications Between Two Systems With OpenSSH”，
`https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_security/assembly-using-secure-communications-with-openssh-configuring-and-managing-security`

314

RH12-RHEL8.0-en-1-202190507

## 引导练习

## 访问远程命令行

在本次练习中，你将以不同的用户登录远程系统并执行命令。

### 目标
你应该能够：

- 登录到远程系统。

### 准备
- 登录到远程系统。
- 执行命令。

1. 打开到 workstation 的 SSH 会话。

```
[student@workstation ~$
```

2. 打开到 serverb 的 SSH 会话。

```
[student@workstation ~$ serverb

The authenticity of 'serverb (172.25.250.11)' can't be established.

ECDSA fingerprint is SHA256:aQS0PTOLrqCO2XGk0IYCa7apPKimerDoauk720.

Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added serverb,172.25.250.12 (ECDSA) to the list of known
hosts.

student@serverb: password:

...output omitted...

[student@serverb ~$]
```

3. 在 server 上运行 `w` 命令。

```
[student@serverb ~ w

18:49:22 up 2:55,  1 user, load average: 0.00, 0.00, 0.00

USER TTY FROM LOGIN IDLE JCPU PCPU WHAT

student pts/0 172.25.250.10   18:33 0.00s 0.01s 0.00s
```

4. 退出 server 上的 student shell。

```
[student@serverb ~ exit

logout

Connection to server closed.

[student@workstation ~$]
```

5. 以 root 身份打开到 server 的 SSH 会话。

```
[student@workstation ~ ssh root@server

root@server's password: redhat

...output omitted...

[root@server ~]
```

6. 在 server 上运行 `w` 命令。

```
[root@server ~ w

19:10:28 up 3:16,  1 user,  load average: 0.00, 0.00, 0.00

USER TTY FROM LOGIN IDLE JCPU PCPU WHAT

root pts/0 172.25.250.10   19:09 0.00s 0.01s 0.00s
```

7. 退出 server 上的 root 用户的 shell。

```
[root@server ~ exit

logout

Connection to server closed.

[student@workstation ~$]
```

- 从 servera 上删除 `/home/student/.ssh/known_hosts`。这会导致 ssh 丢失对远程系统的记录身份。

```
$student@servera~$ rm /home/student/.ssh/known_hosts
```

主机密钥可能会因为合法原因发生变化：例如，远程机器因为硬件故障被更换，或者远程机器重新安装了系统。通常情况下，建议在 `known_hosts` 文件中删除特定主机的密钥。由于该 `known_hosts` 文件只有一个条目，你可以删除整个文件。

- 以 student 身份打开一个到 server 的 SSH 会话。如果被提示，请接受密钥。在提示输入 server 上 student 的密码时使用密码。

```
$student@server~$ student@server '172.25.250.11' can't be established.

ECDSA key fingerprint is SHA256:ERTdjooI2rwSwZQngD5or+JXfbidugubdXBuHuwZA

Are sure you want to continue connecting (yes/no) yes

Warning: Permanently added '172.25.250.11' (ECDSA) to the list of known hosts

student@servers password: student

...omitted...

[student@server~$]
```

注意，`ssh` 命令要求你进行确认以接受或拒绝主机密钥，因为无法找到远程主机。

- 退出 server 上 student 用户的 shell，并确认 servera 上存在一个新的 `known_hosts` 实例。

```
$student@server~$ exit

logout

Connection to server closed closed.

$student@server~$ ls -l /home/student/.ssh/known_hosts

-rw-r--r-- 1 student 183 Feb 1 20:26 /home/student/.ssh/known_hosts
```

- 确认新的 `known_hosts` 文件实例包含 servera 的主机密钥。

```
$student@server~$ cat /home/student/.ssh/known_hosts

172.25.250.11 ecdsa-sha2-nistp256

AAAAAE2VjZHNLOkYToYTildZhNYTAAAAmIldZhNYTAAABB019LEYEhmU1rqnQBBPukH2Ba0/QBa9Wub5n4b3S3mihwKKFFFA/UNj8NDpEmHke/GmnkcEYMLbCfd9nNA=
```

实际输出。

- 在不访问交互式 shell 的情况下在 serverb 上远程运行 `hostname`。

```
$student@server~$ student@server hostname

student@server's password: student

server.lab.example.com
```

上述命令显示了远程系统 serverb 的主机名。

- 13. 退出 servera 上 student 用户的 shell。

```
[student@servera ~]$ exit

logout

Connection to servera closed.
```

## 完成

在工作站上运行 `lab ssh-access finish` 以完成此练习。

```
[student@workstation ~]$ lab ssh-access finish
```
