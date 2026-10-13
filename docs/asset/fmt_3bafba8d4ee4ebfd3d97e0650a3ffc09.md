
在这种情况下，优势是 `demo.com` 的大多数变量可以放置在 `vars` 文件中，但敏感变量可以通过将它们在 `vault` 文件中分离来保持保密。然后管理员可以使用 `ansible-vault` 加密 `vault` 文件，同时将 `vars` 保留为明文。

示例中使用的文件名 `host_vars/demo.com` 没有什么特殊。该目录包含更多文件，其中一些被 Ansible Vault 加密，另一些则。

Playbook 变量（与清单 变量相比）也可以被 Ansible Vault 保护。敏感的 playbook 变量可以放在一个用 Ansible Vault 加密的单独文件中，并通过 `vars_files` 指令包含在 playbook 中。这非常有用，因为 playbook 变量的优先级高于清单变量。

## 参考文献

- `ansible-playbook(i)` 和 `vault(i)` man pages
- Vault – Ansible Documentation
  https://docs.ansible.com/ansible/latest/user_guide/playbooks_vault.html
- Variables and Vars – Ansible Documentation
  https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html#best-practices-for-variables-and-vars

# 第 4 章 | 管理变量和事实

## 引导性练习

## 管理秘密

在本练习中，你将使用 Ansible Vault 对敏感变量进行加密以保护它们，然后运行一个使用这些变量的 playbook。

## 学习目标

你应当能够：

- 使用在加密文件中定义的变量执行 playbook。

## 准备工作

使用密码以 `student` 身份登录到工作站。
在工作站上，运行 `lab data-secret start` 命令。该脚本会确保工作站上安装了 Ansible，并为本次练习创建一个工作目录。该目录包含一个清单文件（inventory），它将 `servera.lab.example.com` 指定为托管主机，它是 `devserver` 组的一部分。

```
[student@workstation]-$ lab data-secret start
```

1. 在工作站上，以 `student` 身份切换到 `/home/student/data-secret` 工作目录。

```
[student@workstation]-$ cd /data-secret
```

2. 编辑提供的加密文件 `secret.yml` 的内容。可以使用 `redhat` 作为密码对其进行解密。取消 `username` 和 `pwhash` 变量条目的注释。

2.1 编辑加密文件 `/home/student/data-secret/secret.yml`。在提示 vault 时提供密码 `redhat`。加密文件将在 `vim` 编辑器中打开。

```
[student@workstation-secret]$ ansible-vault edit secret.yml
password: redhat
```

2.2 取消两个变量条目的注释，保存文件并退出编辑器。它们应该显示如下所示：

```
username: ansibleuser1
pwhash: ${6}$jf...uxhp1
```

3. 创建名为 `/home/student/data-secret/create_users.yml` 的 playbook，该 playbook 使用 `/home/student/data-secret/secret.yml` 加密文件中定义的变量。

配置 playbook 使用 `devservers` 主机组。在远程托管主机上以 `devops` 用户身份运行此 playbook。配置 playbook 创建由 `username` 变量定义的 `ansible1` 用户。使用存储在 `pwhash` 变量中的 `password` 单词设置该用户的密码。

```
- name: create user accounts for all our servers
  hosts: devservers
  become: True
  remote_user: devops
  vars_files:
    - secret.yml
tasks:
  - name: Creating user from secret.yml
    user:
      name: "{{ username }}"
      password: "{{ pwash }}"
```

4. 使用 `ansible-playbook --syntax-check` 命令验证 `create_users.yml` playbook 的语法。使用 `--ask-vault-pass` 选项提示输入 vault 密码以解密 `secret.yml`。在继续之前解决任何语法错误。

```
[workstation-data-secret]$ ansible-playbook --syntax-check \
> --ask-vault-pass create_users.yml
Vault password (default): redhat
playbook: create_users.yml
```

> 注意
> 与其使用 `--ask-vault-pass`，你可以使用较新的 `--vault-id @prompt` 选项来实现相同功能。

5. 创建一个名为 `vault-pass` 的密码文件用于 playbook 执行，而不是提示输入密码。该文件必须包含明文 `redhat` 作为 vault 密码。将该文件的权限更改为 `0600`。

```
[workstation-data-secret]$ echo 'redhat' > vault-pass
[workstation-data-secret]$ chmod 0600 vault-pass
```

6. 使用 `vault-pass` 文件执行 Ansible playbook，使用存储在 `secret.yml` Ansible Vault 文件变量中的密码在远程系统上创建 `ansible1` 用户。

```
[workstation-data-secret]$ ansible-playbook \
> --vault-password-file=vault-pass create_users.yml
PLAY [create user accounts for all our servers]
************************************
```

# 第 4 章 | 管理变量和事实

```
TASK [Gathering Facts]
********************************************************************
ok: [servera.lab.example.com]

TASK [Creating users from secret.yml]
********************************************************************
changed: [servera.lab.example.com]

PLAY RECAP
servera.lab.example.com : ok=2 changed=1 unreachable=0 failed=0
```

7. 验证 playbook 是否运行正确。`ansibleuser` 应该存在于 `servera.lab.example.com` 上并具有正确的密码。通过 ssh 登录到 `servera.lab.example.com` 进行测试。`ansibleuser` 的用户名是 `redhat`。为了确保 SSH 仅通过密码验证而非 SSH 密钥，在登录时使用 `-o PreferredAuthentications=password` 选项。
成功登录后从 `servera` 退出。

```
[student@workstation-data-secret~$] ssh -o PreferredAuthentications=password \
ansibleuser1@servera.lab.example.com
ansibleuser1@servera.lab.example.com's password: redhat
Activate the web console with: systemctl enable --now cockpit.socket
```

```
[ansibleuser1@servera~$] exit
logout
```
