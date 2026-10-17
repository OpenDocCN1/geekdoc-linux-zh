
debug2: gss names ok: [gss-ex-gss-group14-sha1]: gss names ok: (curtain-sha256-openssh.org, ecdsa-sha-nist256, ecdsa-sha-nist384, diffie-hellman-group14, diffie-hellman-group16-sha256, diffie-hellman-group18-sha512,diffie-hellman-group-exchange-sha1

RH24-RHEL8.0-en-20190531

## 第 9 章 | 故障排查 Ansible

- 15. 使用 Ansible 最高级别的详细日志时，Ansible 日是检查 `/home/student/troubleshoot-playbook/ansible.log` 中之前输出的更好选项。

```
[user@workstation troubleshoot-playbook]$ tail ansible.log
2018-12-17 19:22:50 pid18227 user | task path: /home/student/troubleshoot-playbook/samba.yml:2
2018-12-17 19:22:54 pid18227 user | fatal: [server.lab.example.com UNREACHABLE] => {
  "changed": false,
  "msg": "Failed to connect to the host via: OpenSSH_7.1p1
OpenSSH_7.1p1-11 Sep 2018: Reading configuration data /home/student/.ssh/config line 1
Applying options for /
debug1: Reading configuration data at /etc/ssh/sh_config
debug2: Including /etc/ssh/sh_config.08-hdk-training.conf depth 0
debug1: Reading configuration data /etc/ssh/sh_config.08-hdk-training.conf
Applying options for /
debug1: Reading configuration data /etc/ssh/sh_config.05-redhat.config line 52:1: Reading configuration data at /etc/ssh/sh_config.05-redhat.config
debug2: Including /etc/ssh/sh_config.05-redhat.config line 2: Including /etc/crypto-policies/back-ends/openssh.config
debug1: Reading configuration data /etc/crypto-policies/back-ends/openssh.config
debug2: gss names ok: [nist25519-sha256@openssh.org, ed25519-nist256, ecd256-nist384, diffie-hellman-group14-sha256, diffie-hellman-group16-sha256, diffie-hellman-group18-sha512,diffie-hellman-group-exchange-sha1]
debug2: gss names ok: [gss-ec-sha256@libssh.org, ecdsa-sha-nist256, ecdsa-sha-nist256, ecd256-nist384, diffie-hellman-group14-sha256, diffie-hellman-group16-sha256, diffie-hellman-group18-sha512,diffie-hellman-group-exchange-sha1]
```

# 第 9 章 | Ansible 故障排除

- 18. 修改 playbook，并将 `deliver samba config` 任务中的 `src` 参数更正为 `samba.conf.j2`。完成后，它应该如下所示：

```
...output已省略...
  name: deliver samba config
  template:
    src: samba.conf.j2
    dest: /etc/samba/smb.conf
    owner: root
  ...output已省略...
```

- 19. 再次运行 playbook。使用 `--step` 选项执行 playbook。它应该无错误地运行。

```
[student@workstation troubleshoot-playbook]$$ ansible-playbook samba.yml --step

PLAY [Install a server server]
**************************************************
Perform task: Gathering Facts N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: install samba N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: install firewall N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: debug install_state variable N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: start samba N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: start firewall N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: configure firewall for samba N(o)/y(es)/(c)continue: y
  ...output omitted...
Perform task: TASK: deliver samba config N(o)/y(es)/(c)continue: y
  ...output omitted...

PLAY RECAP
**************************************************
servera.lab.example.com :**************************** : ok=8  changed=1  unreachable=0  failed=0
```

## 完成

在工作站上，运行 `troubleshoot-playbook finish` 脚本来清理本次练习。

```
[student@workstation ~]$ lab troubleshoot-playbook finish
```

本引导练习结束。

# ANSI 故障排除

托管主机

## 目标

完成本节后，你应该能够排除运行 playbook 的托管主机上的故障。

## 使用检查模式作为测试工具

你可以使用 `ansible-playbook --check` 命令对 playbook 运行冒烟测试。此选项在执行 playbook 时不会对托管主机的配置进行更改。如果 playbook 中使用的模块支持检查模式（check mode），则对托管主机将进行的更改将会显示但不会执行。如果模块不支持检查模式，则不会显示更改，但模块仍然会采取操作。

```
$[demo ~~$ ansible-playbook --check playbook.yml
```

> 注意：

如果你的任务使用了条件判断，`ansible-playbook --check` 命令可能无法正常工作。

你可以通过 `check_mode` 设置来控制单个任务是否在检查模式下运行。如果任务具有 `check_mode: yes`，则它始终在检查模式下运行，无论你是否向 `ansible-playbook` 传递了 `--check` 选项。同样，如果任务具有 `check_mode: no`，则它不会在检查模式下运行。

以下示例展示了如何使用 `check_mode`：
