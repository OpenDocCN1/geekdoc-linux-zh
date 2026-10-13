
```
output omitted...
tasks:
  name: install samba
  yum:
    name: samba
    state: "{{ install_state }}"
  output omitted...
```

10. 使用 `--syntax-check` 选项运行 playbook。它不应该显示任何额外的语法错误。

```
[student@workstation troubleshoot-playbook]$ ansible-playbook --syntax-check \
  > samba.yml
```

`playbook: samba.yml`

11. 运行 playbook。将抛出一个与 SSH 相关的错误。

```
[student@workstation troubleshoot-playbook]$ ansible-playbook samba.yml
PLAY [Install a samba server]
****************************************************************
```

```
TASK [Gathering Facts]
****************************************************************
fatal: [servera.lab.example.com]: UNREACHABLE! => {"changed": false,
"msg": "Failed to connect to the host via ssh: Could not resolve hostname servera.lab.example.com: Name or service not found\r\n", "unreachable": true}
```

```
PLAY RECAP
****************************************************************
```

```
servera.lab.example.com      : ok=0    changed=0    unreachable=1
failed=0
```

12. 使用 `ping` 命令确保受托管主机 `servera.lab.example.com` 正在运行。

```
[student@workstation troubleshoot-playbook]$ ping -c3
servera.lab.example.com
PING servera.lab.example.com (172.250.250.10): 64 bytes of data.
64 bytes from servera.lab.example.com (172.250.250.10): icmp_seq=64  time=0.247 ms
64 bytes from servera.lab.example.com (172.250.250.10): icmp_seq=2  time=64
time=0.329 ms
64 bytes from servera.lab.example.com (172.250.250.10): icmp_seq=10  time=0.320 ms
```

![](img/c66fec31e9528c7da22e5fa5113dfa6e_377_0.png)

## 第 9 章 | 故障排查 Ansible ping 统计

--- server.lab.example.com ---

3 packets transmitted, 3 received, 0% packet loss, time 1999ms

rtt min/avg/max/dev 0.247/0.298/0.041 ms

- 13. 确保你可以作为用户通过 SSH 连接到受托管主机 `server.lab.example.com`，并且正确的 SSH 密钥已就绪。完成后退出。

```
[student]@workstation troubleshoot-playbook]$ ssh
devops@server.lab.example.com
Warning: Permanently added server.lab.example.com,172.25.250.10 (ECDSA)
to the list of known hosts.
... output omitted...
[devops@server~~]$ exit
Connection to server.lab.example.com closed.
```

- 14. 使用 `-vvvv` 运行 playbook 以获取更多运行信息。由于受托管主机 `server.lab.example.com` 无法访问，产生了错误。

```
[student]@workstation troubleshoot-playbook]$ ansible-playbook -vvvv
samba.yml
... output omitted.
```

PLAYBOOK: samba.yml ***

1 plays in a samba server

[Install a samba server] *************************************************

[Gathering Facts] *********************************

task path: /home/troubleshoot-playbook/samba.yml:2

server.lab.example.com: ESTABLISH CONNECTION FOR USER: devs

... output omitted.

fatal: server.lab.example.com: UNREACHABLE! => {

  "changed": false,

  "msg": "Failed to connect to the host via: OpenSSH.7.8,

OpenSSH_7.8p1-11 Sep 2018ndebug1: Reading configuration data /home/troubleshoot/ssh_config/ndebug1 line 1: options for /ndebug1: Reading configuration data /etc/ssh/

sh_config/ndebug1 line 52: Including /etc/ssh/

sh_config/ndebug1/01-transmit.config line 0: Reading configuration

data /etc/ssh/sh_config/ndebug1: line 1: options for /ndebug3

sh_config/ndebug1: Reading configuration data /etc/ssh/

sh_config/ndebug1 line 52: Including /etc/ssh/

sh_config/ndebug1/01-transmit.config line 0: Reading configuration /etc/ssh/

sh_config/ndebug1: line 1: options for /ndebug3

sh_config/ndebug1: Reading configuration data /etc/ssh/

sh_config/ndebug1 line 52: Including /etc/ssh/

sh_config/ndebug1/01-transmit.config line 0: Reading configuration /etc/ssh/

sh_config/ndebug1: line 1: options for /ndebug3

sh_config/ndebug1: Reading configuration data /etc/ssh/

sh_config/ndebug1 line 52: Including /etc/ssh/

sh_config/ndebug1/01-transmit.config line 0: Reading configuration /etc/ssh/

sh_config/ndebug1: line 1: options for /ndebug3

sh_config/ndebug1: Reading configuration data /etc/ssh/

sh_config/ndebug1 line 0 /etc/crypto-policies/back-ends/openssh.config

debug1: Reading configuration data /etc/crypto-policies/back-ends/openssh.config
