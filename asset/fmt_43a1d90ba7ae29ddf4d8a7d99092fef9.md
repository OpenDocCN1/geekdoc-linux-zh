
```
[student@workstation file-manage]$ ansible-playbook
secure_log_backups.yml
PLAY Use the fetch module to retrieve secure log files
**************************************************
TASK (Gathering Facts)
**************************************************
ok: [servera.lab.example.com]
ok: [serverb.lab.example.com]

TASK (Fetch the /var/log/secure file from managed hosts)
************************************
changed: [serverb.lab.example.com]
changed: [servera.lab.example.com]
```

PLAY RECAP

*********************************\*\*\*\*\*\*\*\*\*\*\*\*

servera.lab.example.com : ok=2  changed=1 unreachable=0 failed=0

serverb.lab.example.com : ok=2  changed=1 unreachable=0 failed=0

```

## 1.6. 验证 playbook 的执行结果：

```
[student@workstation file-manage]$ tree -F secure-backups

secure-backups

+- servera.lab.example.com/

| +- var/

| |   +- log/

| |     └── secure

+- serverb.lab.example.com/

| +- var/

|     └── log/
```

## 2. 在当前工作目录下创建 `copy_file.yml` playbook。配置该 playbook 以 `root` 用户身份将 `/home/student/file-manage/files/users.txt` 文件复制到所有托管主机。

### 2.1. 为 `copy_file.yml` playbook 添加以下初始内容：

```yaml
- name: Using the copy module
hosts: all
remote_user: root
```

### 2.2. 添加一个任务，使用 `copy` 模块将 `/home/student/file-manage/files/users.txt` 文件复制到所有托管主机。使用 `copy` 模块为 `users.txt` 文件设置以下参数：

| PARAMETER | VALUES |
| \--- | --- |
| src | files/users.txt |
| dest | /home/devops/users.txt |
| owner | devops |
| group | devops |
| mode | u+rw, g-wx, o-rwx |
| setype | samba_share_t |

```yaml
tasks:
  - name: Copy a file to managed hosts and set attributes
    copy:
      src: files/users.txt
      dest: /home/devops/users.txt
      owner: devops
      group: devops
      mode: u+rw, g-wx, o-rwx
      setype: samba_share_t
```

### 2.3. 使用 `ansible-playbook --syntax-check copy_file.yml` 命令验证其语法。纠正任何错误后进入下一步。

```
[student@workstation file-manage]$ ansible-playbook --syntax-check \
> copy_file.yml

playbook: copy_file.yml
```

### 2.4. 运行 `ansible-playbook copy_file.yml` 执行 playbook：

```
[student@workstation file-manage]$ ansible-playbook
copy_file.yml

PLAY Using the copy module
**************************************************

TASK (Gathering Facts)
**************************************************

ok: [servera.lab.example.com]
ok: [serverb.lab.example.com]

TASK (Copy a file to managed hosts and set attributes)
**************************************************

changed: [serverb.lab.example.com]
changed: [servera.lab.example.com]
```

PLAY RECAP
*********************************\*\*\*\*\*\*\*\*\*\*\*\*
servera.lab.example.com : ok=2  changed=1 unreachable=0 failed=0
serverb.lab.example.com : ok=2  changed=1 unreachable=0 failed=0

```

### 2.5. 使用 `root` 用户身份执行 `ls -Z` 命令来验证托管主机上 `users.txt` 文件的 SELinux 上下文。

```
[student@workstation file-manage]$ ansible all -m command -a 'ls -Z'
servera.lab.example.com | CHANGED | rc=0
unconfined_u:object_r:samba_share_t:s

serverb.lab.example.com | CHANGED | rc=0
unconfined_u:object_r:samba_share_t:s
```

## 3. 在上一步中，`users.txt` 文件被设置了 `samba_share_t` 类型。现在确定应该设置为默认的 SELinux 上下文。在当前工作目录下创建一个该 playbook。配置该 playbook 使用 `file` 模块来确保默认的 SELinux 用户、角色和类型。注意：在现实世界中，你可能还会从 `copy_file.yml` 中删除 `setype` 关键字。

### 3.1. 创建 `sellinux_defaults.yml` playbook：

```yaml
- name: Using the file module to ensure SELinux context
hosts: all
remote_user: root
tasks:
  - name: SELlinux context is set to defaults
    file:
      path: /home/devops/users.txt
      user: default
      role: default
      type: default
      level: default
```

### 3.2. 使用 `ansible-playbook --syntax-check selinux_defaults.yml` 命令验证 `sellinux_defaults.yml` playbook 的语法。

```
[student@workstation file-manage]$ ansible-playbook --syntax-check
> selinux_defaults.yml

playbook: selinux_defaults.yml
```

### 3.3. 运行 playbook：
