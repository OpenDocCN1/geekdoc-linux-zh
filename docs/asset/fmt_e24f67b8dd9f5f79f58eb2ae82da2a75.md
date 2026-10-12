
```text
TASK [Install required packages] ***************************************************
changed: [ubuntu] => (item=apache2)
changed: [ubuntu] => (item=php)
changed: [ubuntu] => (item=php-mysql)
```

*图 12.29：使用循环的输出示例*

以下示例展示了如何循环一个包含要创建的用户名和组的字典列表。为此，使用了模块`user`（用户）。

```yaml
- name: Create users
  ansible.builtin.user:
    name: "{{ item.name }}"
    groups: "{{ item.groups }}"
  loop:
    - {name: "user1", groups: "users"}
    - {name: "user2", groups: "users,sudo"}
```

#### 注册

Ansible 的任务会生成有关执行的信息。可以使用表达式`register`将该信息保存在变量中。在使用模块`command`（命令）或`shell`（shell）时，这特别有用。以下代码显示了一个示例：

```yaml
- name: Run a command
  ansible.builtin.command: hostname -I
  register: hostname_output
- name: Show content of registered variable
  ansible.builtin.debug:
    var: hostname_output
```

图 12.30 显示了`debug`（调试）任务的输出：

任务`[显示已注册变量的内容] ***********************`

```json
ok: [ubuntu] => {
  "hostname_output": {
    "changed": true,
    "cmd": [
      "hostname",
      "-I"
    ],
    "delta": "0:00:00.007307",
    "end": "2022-10-22 17:53:53.924471",
    "failed": false,
    "msg": "",
    "rc": 0,
    "start": "2022-10-22 17:53:53.917164",
    "stderr": "",
    "stderr_lines": [],
    "stdout": "192.168.122.43 192.168.100.1 ",
    "stdout_lines": [
      "192.168.122.43 192.168.100.1 "
    ]
  }
}
```

![](img/863afa537de4eed7deb11978bfbfa90e_421_0.png)

已注册的变量是一个字典，包含以下常用键：

- `changed`: 指示任务是否更改了系统。
- `cmd`: 执行的命令（如果我们使用了`command`或`shell`）。
- `failed`: 指示任务是否失败。
- `rc`: 退出代码（如果我们使用了`command`或`shell`）。
- `stderr / stderr_lines`: 标准错误输出消息。
- `stdout / stdout_lines`: 标准输出消息。

要访问注册值中的一个`键`，有以下两种选择：

```yaml
- name: 显示变量的 stdout（选项 1）
  ansible.builtin.debug:
    msg: "运行时间: {{ hostname_output.stdout }}"

- name: 显示变量的 stdout（选项 2）
  ansible.builtin.debug:
    msg: "运行时间: {{ hostname_output['stdout'] }}"
```

#### 模板

模板是一个包含变量和不同语句（条件、循环等）的动态文件。这些模板使用 Jinja2 语言，它简化了模板的定义，且 YAML 易于阅读。表 12.11 展示了可在 Jinja2 模板文件中使用的常用语法：

| **类型** | **语法** | **示例** |
| :--- | :--- | :--- |
| 变量 | `{{ variable }}` | `{{ ansible_fqdn }}` |
| 条件 | `{% if expression %}`<br>`statements`<br>`{% elif %}`<br>`statements`<br>`{% else %}`<br>`statements`<br>`{% endif %}` | `{% if purpose == "production" %}`<br>`警报：这是一个生产系统。`<br>`{% else %}`<br>`这不是一个生产系统。`<br>`{% endif %}` |
| 循环 | `{% for variable in list %}`<br>`statements`<br>`{% endfor %}` | `allowed_users:`<br>`{% for user in userlist %}`<br>`- {{ user }}`<br>`{% endfor %}` |
| 注释 | `{# text #}` | `{# 这是一条注释 #}` |

*表 12.11: Jinja2 模板语法*

模块`template`处理 Ansible 工具（如`ansible-playbook`）执行所在地的模板，并将处理后的文件传输到受管主机。以下模板展示了如何填充库存中主机信息的`/etc/hosts`文件。

```
127.0.0.1 localhost localhost.localdomain localhost4
::1           localhost localhost.localdomain localhost6
{% for host in play_hosts %}
{{ hostvars[host]['ansible_default_ipv4']['address'] }} {{ host }}
{% endfor %}
```

处理该模板的示例任务如下：

```yaml
- name: 填充 /etc/hosts
  ansible.builtin.template:
  src: hosts.j2
  dest: /etc/hosts
```

#### 块（Blocks）

Ansible 允许将多个任务分组在一个块（Block）中。这允许指定不同的参数，例如`become`、`become_user`或`user`。用于定义块的表达式是`block`，它包含一个任务列表。以下代码展示了一个使用块的角色示例：

```yaml
- name: 块示例
  hosts: linux
  become: True
  tasks:
    - name: 安装和配置 Ubuntu 系统
      when: ansible_distribution == "Ubuntu"
      block:
        - name: 安装所需的包
          ansible.builtin.apt:
            name: "{{ item }}"
          loop:
            - apache2
            - php
            - php-mysql
        - name: 生成 index.html 文件
          ansible.builtin.copy:
            content: "Hello to {{ ansible_hostname }}"
            dest: /var/www/html/index.html
```

#### 常用模块列表

Ansible 提供了大量的核心模块，以在受管主机上执行各种各样的任务。以下列表显示了`ansible.builtin`集合中的一些模块：

- `add_host`: 向`ansible-playbook`的内存库存添加主机（以及可选的组）。
- `apt`: 管理`apt`包。
- `apt_key`: 添加或移除`apt-key`。
- `apt_repository`: 添加和移除 APT 软件仓库。
- `assemble`: 从片段组装配置文件。
- `assert`: 断言给定的表达式为真。
- `async_status`: 获取异步任务的状态。
- `blockinfile`: 插入/更新/移除由标记行包围的文本块。
- `command`: 在目标上执行命令。
- `copy`: 将文件复制到远程位置。
