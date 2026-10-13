
```bash
[student@workstation file-manage]$ ansible-playbook add_block.yml
PLAY [Add block of text to a file]
************************************

TASK [Gathering Facts]
************************************
ok: [servera.lab.example.com]
ok: [servera.lab.example.com]

TASK [Add a block of text to an existing file]
************************************

changed: [servera.lab.example.com]
changed: [servera.lab.example.com]
************************************

PLAY RECAP
servera.lab.example.com             : ok=2    changed=1 unreachable=0
failed=0
servera.lab.example.com             : ok=2    changed=1 unreachable=0
failed=0
```

### 5.4. 使用带有 `cat` 命令的命令来验证托管主机上 `/home/devops/users.txt` 文件的正确内容。

```bash
[student@workstation file-manage]$ ansible all -m command \
-a 'cat users.txt' -u devops
servera.lab.example.com | CHANGED | rc=0 >>
This line was added by the lineinfile module.
# BEGIN ANSIBLE MANAGED BLOCK
This block of text consists of two lines.
They have been added by the blockinfile module.
# END ANSIBLE MANAGED BLOCK

servera.lab.example.com | CHANGED | rc=0 >>
This line was added by the lineinfile module.
# BEGIN ANSIBLE MANAGED BLOCK
This block of text consists of two lines.
They have been added by the blockinfile module.
# END ANSIBLE MANAGED BLOCK
```

- 6. 在当前工作目录下创建一个名为 `remove_file.yml` 的 playbook：配置该 playbook 使用 `file` 模块从所有托管主机上删除 `/home/devops/users.txt` 文件。

### 6.1. 创建 `remove_file.yml` playbook：

```yaml
---
name: Use the file module to remove a file
hosts: all
remote_user: devops
tasks:
  - name: Remove a file from managed hosts
    file:
      path: /home/devops/users.txt
      state: absent
```

## 6.2. 使用 `ansible-playbook --syntax-check remove_file.yml` 命令验证 `remove_file.yml` playbook。

```bash
[student@workstation file-manage]$ ansible-playbook --syntax-check remove_file.yml
```

## 6.3. 运行 playbook：

```bash
[student@workstation file-manage]$ ansible-playbook remove_file.yml
PLAY [Use the file module to remove a file]
****************************************

TASK [Gathering Facts]
****************************************
ok: [servera.lab.example.com]
ok: [servera.lab.example.com]

TASK [Remove a file from managed hosts]
****************************************
changed: [servera.lab.example.com]
changed: [servera.lab.example.com]
```

### 6.4. 使用带有 `cat` 命令的命令来验证托管主机上 `users.txt` 文件的内容。

```bash
[student@workstation file-manage]$ ansible all -m command \
-a 'cat users.txt' -u devops
serverb.lab.example.com | CHANGED | rc=0
This line was added by the lineinfile module.

servera.lab.example.com | CHANGED | rc=0
This line was added by the lineinfile module.
```

PLAY RECAP

************************************************

servera.lab.example.com : ok=2 changed=1 unreachable=0

failed=0

serverb.lab.example.com : ok=2 changed=1 unreachable=0

failed=0

## 结束

在工作站运行 `lab-manage` 脚本以清理本次练习。

本练习结束。

## 使用 JJA2 模板部署自定义文件

## 目标

完成本节后，你将能够使用 Jinja2 模板部署文件。

## 文件模板化

Red Hat Ansible 有许多模块可以修改现有文件，包括 `lineinfile` 和 `blockinfile` 等。然而，它们并不总是易用的。

管理文件的更强大方法是使用模板。通过这种方法，你可以使用 变量和因子自动定制配置。

## JJA2 简介

Ansible 在模板文件中使用 Jinja2 模板系统。Ansible 在 playbook 中也使用 Jinja2 语法来引用变量，因此你已经了解如何使用它。

## 使用分隔符

变量和逻辑表达式位于分隔符之间。例如，Jinja2 模板使用 `{% ... %}` 处理表达式或逻辑（例如循环），而 `{{ ... }}` 用于将表达式或变量的结果输出给用户。后者标签在渲染时会被替换为值，并对用户可见。使用 `{# ... #}` 语法来包含不出现在最终文件中的注释。

在示例中，第一行包含一个不会出现在最终文件的注释。第二行的变量引用将被替换为相应的系统因子值。

```jinja2
## /etc/hosts line
{{ ansible_facts['default_ipv4'] }} {{ ansible_facts['hostname'] }}
```

# 第 6 章 | 将文件部署到托管主机

以下示例展示了如何为 `/etc/ssh/sshd_config` 创建一个模板，其中包含 Ansible 从托管主机获取的变量和事实（facts）。当执行关联的 playbook 时，任何文件都将被其正在配置的托管主机中的对应值替换。

> 注意

> 包含 Jinja 模板的文件不需要任何特定的文件扩展名（例如，`j2`）。但是，提供此类文件扩展名可能会让你更容易记住它是一个模板文件。

```ssh
# {{ ansible_managed }}
# 不要对此文件进行任何本地修改，否则更改将会丢失

Port {{ ssh_port }}
ListenAddress {{ ansible_facts['default_ipv4']['address'] }}

HostKey = /etc/ssh/ssh_host_rsa_key
HostKey = /etc/ssh/ssh_host_ecdsa_key
HostKey = /etc/ssh/ssh_host_ed25519_key

SyslogFacility AUTHPRIV
```
