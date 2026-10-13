
### 7. 创建一个新的 play 来查询 Web 服务以确保所有配置配置正确
它应该在 `localhost` 上运行。由于 Ansible 事实（fact），Ansible 不需要更改身份，因此将 `become` 模块设为 `false`。你可以使用 `uri` 模块来检查 URL。对于此任务，检查状态码 200 以确认 `servera.lab.com` 上的服务器正在运行且配置正确。

```yaml
name: Verify the Apache service
hosts: localhost
become: false
tasks:
  - name: Ensure the webserver is reachable
    uri:
      url: http://servera.lab.example.com
      status_code: 200
```

### 8. 完成后，playbook 应该如下所示
检查 playbook 并确认两个计划都是正确的。

```yaml
- name: Deploy and start Apache HTTP service
  hosts: webserver
  vars:
    web_pkg: httpd
    firewall_pkg: firewalld
    web_service: httpd
    firewall_service: firewalld
    python_pkg: python3-MySQL
    rule: http

  tasks:
    - name: Required packages are installed and up to date
      yum:
        - "{{ web_pkg }}"
        - "{{ firewall_pkg }}"
        - "{{ python_pkg }}"
        state: latest

    - name: The {{ firewall_service }} service is started and enabled
      service:
        name: "{{ firewall_service }}"
        enabled: true
        state: started

    - name: The {{ web_service }} service is started and enabled
      service:
        name: "{{ web_service }}"
        enabled: true
        state: started

    - name: Web content is in place
      copy:
        content: "Example web content"
        dest: /var/www/html/index.html

    - name: The firewall port for {{ rule }} is open
      firewall:
        service: "{{ rule }}"
        permanent: true
        immediate: true
        state: enabled

    - name: Verify the Apache service
      hosts: localhost
      become: false
      tasks:
        - name: Ensure the webserver is reachable
          uri: http://servera.lab.example.com
          status_code: 200
```

### 9. 在运行 playbook 之前，使用 `ansible-playbook --syntax-check` 命令验证其语法
如果报告了任何错误，在在移动下一步之前修正它们。你应该看到类似下面的输出：

```bash
$student@workstation data-variables]$ ansible-playbook --syntax-check
playbook.yml
```

playbook: playbook.yml

### 10. 使用 `ansible-playbook` 命令运行 playbook
观察 Ansible 安装包、启动并启用服务以及确保 Web 服务器可访问的输出。

```bash
$student@workstation data-variables]$ ansible-playbook playbook.yml

PLAY [Deploy and start Apache HTTP service]
************************************************

TASK [Gathering Facts]
************************************************
ok: servera.lab.com

TASK [Required packages are installed and up to date]
************************************************
ok: servera.lab.com

TASK [The firewalld service is started and enabled]
************************************************
changed: servera.lab.com

TASK [The httpd service is started and enabled]
************************************************
changed: servera.lab.com

TASK [Web content is in place]
************************************************
changed: servera.lab.com

TASK [The firewall port for http is open]
************************************************
changed: servera.lab.com

TASK [Verify the Apache service]
************************************************
Gathering Facts: localhost

TASK [Ensure the webserver is reachable]
************************************************
ok: localhost

PLAY RECAP
************************************************
localhost : ok=2 changed=0
servera.lab.com : ok=6 changed=4
```

### 9. 在工作站上运行 `data-variables finish` 脚本来清理此练习

```bash
[student@workstation ~]$ finish
```

## 管理秘密

### 目标
完成本节后，你应该能够使用 Ansible Vault 加密变量，并运行引用加密文件的 playbook。

# 引入 Ansible Vault
Ansible 可能需要加密敏感数据（如密码或 API 密钥）以配置托管主机。通常，这些信息可能以明文存储在清单变量或其他 Ansible 文件中。然而，任何访问 Ansible 文件或存储这些文件的版本控制系统的人都可以访问这些数据。这构成了一个明显的安全风险。

包含在 Ansible 中的 Ansible Vault 可用于加密任何结构数据文件。要使用 Ansible Vault，可以使用命令行工具 `ansible-vault` 创建、编辑、加密、解密和查看文件。Ansible Vault 可以加密 Ansible 使用的结构化数据。这可能包括清单变量、包含的变量、执行 playbook 时传递的变量以及角色中定义的变量。

> 重要
Ansible Vault 没有实现自己的加密函数，而是使用外部 Python 工具包。文件使用密码作为密钥进行对称加密。注意，这种方法没有经过第三方正式审计。

## 创建加密文件
要创建一个新的加密文件，使用 `ansible-vault create filename`。命令会提示新的卷密码，然后使用默认编辑器 `vi` 打开文件。你可以通过设置和导出 `EDITOR` 环境变量来指定不同的默认编辑器。例如，要将默认编辑器设置为 `nano`，执行 `export EDITOR=nano`。
