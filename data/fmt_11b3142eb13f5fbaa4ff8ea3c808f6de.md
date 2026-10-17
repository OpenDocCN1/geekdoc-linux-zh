
## 使用 SELinux 布尔值

```yaml
- name: enabling SELinux and a boolean
  hosts: ansible
  vars:
    myboolean: httpd_read_user_content
  tasks:
    - name: enabling SELinux
      selinux:
        policy: targeted
        state: enforcing
    - name: checking current {{ myboolean }} Boolean status
      shell: getboolean -a | grep {{ myboolean }}
      register: bool_stat

- name: showing boolean status
  debug:
    msg: "the current {{ myboolean }} status is {{ bool_stat.stdout }}"
- name: enabling boolean
  seboolean:
    name: "{{myboolean}}"
    state: yes
    persistent: yes
```

在列表 8-12 的示例 playbook 中，首先使用 `selinux` 模块确保 `SELinux` 处于 `enforcing` 状态。在使用它时，使用 `seboolean` 模块来启用该布尔值。

### 更改 Web 服务器配置

```
+ - name: 使用 linefile 更改 web 服务器配置
  linefile:
    path: /etc/httpd/conf/httpd.conf
    regex: '^DocumentRoot "/var/www/html'
    line: DocumentRoot "/web"
+
+ - name: 使用 linefile 更改 web 服务器安全设置
  linefile:
    path: /etc/httpd/conf/httpd.conf
    regex: '^<Directory "/var/www">'
    line: '<Directory "/web">'
-
- name: 使用 secontext 在新的 documentroot 上设置上下文
```

# 5. 在最后的步骤中，你负责配置 SELinux 特定的设置：

```
+ - name: 使用 secontext 在新的 documentroot 上设置上下文
  sefcontext:
    target: '/web/(.*)?'
    stype: httpd_sys_content_t
    state: present
-
- name: 运行 restorecon 命令
  command: restorecon -Rv /web
-
- name: 允许 web 服务器运行用户内容
  boolean:
    name: httpd_read_user_content
```

# 6. 此时，完整的 playbook 应该如下所示：

```yaml
---
name: 管理 web 服务器 SELinux 属性
  hosts: ansible
  tasks:
    - name: 确保 SELinux 已启用并强制执行
      selinux:
        policy: targeted
        state: enforcing
    - name: 安装 web 服务器 yum:
      name: httpd
      state: latest
    - name: 启动并启用 web 服务器服务:
      name: httpd
      state: started
      enabled: yes
    - name: 开启防火墙服务 firewalld:
      service: http
      state: enabled
      immediate: yes
    - name: 创建 /web 目录文件
      name: /web
      state: directory
    - name: 在 /web 中创建 index.html 文件
      copy:
        content: 'welcome to the exercise82 web server'
        dest: /web/index.html
    - name: 使用 lineinfile 更改 web 配置
      lineinfile:
        path: /etc/httpd/httpd.conf
        regex: '^DocumentRoot "/var/www/html"
        line: DocumentRoot "/web"
    - name: 使用 lineinfile 更改 web 服务器
      lineinfile:
        path: /etc/httpd/httpd.conf
        regex: '^<Directory "/var/www">'
        line: '<Directory "/web">'
    - name: 使用 secontext 在新的 documentroot 上设置上下文
      secontext:
        target: '/web/(.*)?'
        stype: httpd_sys_content_t
        state: present
    - name: 运行 restorecon 命令
      command: restorecon -Rv /web
    - name: 允许 web 服务器运行用户内容
      seboolean:
        name: httpd_read_user_content
        state: yes
        persistent: yes
```

# 7. 使用 `ansible-playbook exercise82.yaml` 运行 playbook 并验证其输出。

8. 使用 `curl http://ansible` 验证 web 服务是否可访问。在这种情况下，它不应该能够正常工作。尝试分析原因。你可以在本章末尾、章节实验之前找到答案。

## 使用 JINJA2 模板

模板（`template`）是一个包含变量的配置文件，并根据这些变量，根据特定主机的要求在受管主机上生成。使用模板允许以结构化的生成配置文件，这比从特定文件中更改特定行要强大得多。`Ansible` 使用 `Jinja2` 来生成模板。

### 使用简单模板

`Jinja2` 是为 `Python` 开发者提供的通用模板语言。它被用于 `Ansible` 模板，但基于 `Jinja2` 的方法也出现在 `Ansible` 的其他部分。例如，根据 `Jinja2` 引用变量的方式。

在 `Jinja2` 模板中，可以使用三个元素。表 8-4 提供了概述。

![](img/ea4c3f03927a5fe74f47acc2107727ea_353_0.png)

**表 8-4 Jinja2 模板元素**

| 元素 | 示例 |
| --- | --- |
| data | 示例文本 |
| comment | [# 示例文本 #] |
| variable | `{{ ansible_facts['default_ipv4']['address'] }}` |
| expression | `{% for myhost in groups['web'] %}\n{{ myhost }}\n{% endif %}` |

要使用模板，你必须创建一个用 `Jinja2` 编写的模板文件。接下来，该模板文件必须包含在使用模板模块的 `Ansible` playbook 中。列表 8-13 显示了模板文件可能的内容，列表 8-14 显示了调用模板的 playbook 示例。

### 列表 8-13 示例受管

```apache
# {{ ansible_managed }}
<VirtualHost :80>
  ServerAdmin webmaster@{{ ansible_facts['fqdn'] }}
  ServerName {{ ansible_facts['fqdn'] }}
  ErrorLog logs/{{ ansible_facts['hostname'] }}-
  CustomLog logs/{{ ansible_facts['hostname'] } }}-common.log
  DocumentRoot /var/www/vhosts/{{ ansible_facts['hostname'] }}/

  <Directory /var/www/vhosts/{{ ansible_facts['hostname'] }}>>
    Options +Indexes +FollowSymlinks +Includes
    Order allow,deny
    Allow from all
  </Directory>
</VirtualHost>
```

示例模板以 `{{ ansible_managed }}` 开头。该字符串通常用于标识文件是由 `Ansible` 管理的，以防止管理员意外更改文件内容。在处理模板时，该字符串会被替换为 `ansible_managed` 的值。在 `ansible.cfg` 中可以设置该变量。例如，`ansible_fqdn` 和 `ansible_hostname` 变量作为 `facts` 设置。要生成模板，你需要一个使用模板模块的 playbook。列表 8-14 显示了一个示例。

### 列表 8-14 示例受管

```yaml
---
name: 使用模板文件
  hosts: ansible
  tasks:
    - name: 安装 httpd
      yum:
        name: httpd
        state: latest
    - name: 启动并启用 httpd
      service:
        name: httpd
        state: started
        enabled: true
    - name: 模板文件
      template:
        src: listing13.j2
        dest: /etc/httpd/conf.d/vhost.conf
        owner: root
        group: root
        mode: '0644'
    - name: 重启 httpd
      service:
        name: httpd
        state: restarted
```

列表 8-14 中的示例 playbook 使用模板作为源文件，并根据模板在受管主机上生成文件。要进行验证，你可以使用 ad hoc 命令 `ansible2 -a "cat /tmp/hostports.txt"`。

### 在模板中使用 if 条件语句

`for` 语句可以在模板中用于迭代一系列值。`if` 语句可以用于在变量包含特定值或求值为布尔真时才包含文本。列表 8-17 显示了一个示例模板文件，其变量在列表 8-18 的示例 playbook 中设置。

#### 列表 8-17 if 模板示例

```jinja2
{% if apache_package == 'apache' %}
Welcome to Apache
{% else %}
Welcome to httpd
{% endif %}
```

#### 列表 8-18 使用 if 使用模板

```yaml
---
- name: 使用 if 使用模板
  vars:
    apache_package: 'httpd'
  hosts: ansible2
  tasks:
    template:
      src: listing817.j2
      dest: /tmp/hostports.txt
```

## 使用 Jinja2

在 `Jinja2` 模板中，你可以使用过滤器。过滤器是在模板表达式的值（例如变量）上执行某些操作的方法。过滤器包含在变量定义本身，变量及其过滤器的结果将用于生成的生成文件中。表 8-5 概述了某些常用过滤器。练习 8-3 你将练习你的技能，并与使用条件语句的模板进行操作。

**表 8-5 常用过滤器概述**

| 过滤器示例 | 用途 |
| --- | --- |
| `{{ myvar | to_json }}` | 以 `JSON` 格式写入 `myvar` 的内容 |
| `{{ myvar | to_yaml }}` | 以 `YAML` 格式写入 `myvar` 的内容 |
| `{{ myvar | ipaddr }}` | 测试 `myvar` 是否包含 `IP` 地址 |

> **考试提示**
>
> `https://docs.ansible.com` 上的 `Ansible` 文档包含一个名为“常见问题（Frequently Asked Questions）”的章节。在该章节中，你可以找到“如何在模板内部遍历组中的主机列表”的问题。现在就阅读并学习它。这里的回答提供了一个在模板中使用条件语句的极佳示例，这些信息在考试中可能会很有用。

## 练习 8-3 在模板中使用条件语句

1. 使用你的编辑器创建文件 `exercise83.j2`。包含以下行代码以打开 `Jinja2` 条件语句：

```
{% for host in groups['all'] %}
```

2. 该语句定义了一个名为 `host` 的变量。该变量遍历魔术变量 `groups`，该变量持有清单（`inventory`）定义的所有 `Ansible` 主机组。在这些组中，`all` 组（包含所有清单主机名）被处理。

3. 添加以下行（请将其作为单行写入）；它将跨两行显示，但不要按回车键插入换行符：

```
{{ hostvars[host]['ansible_default_ipv4']['address'] }} {{ hostvars[host]['ansible_f_qdn'] }} {{ hostvars[host]['ansible_hostname'] }}
```

此行为每个清单主机写入单行，包含三个项目。为了实现这一点，你使用了魔术变量 `hostvars`，它可以用于识别在清单主机上发现的 `Ansible` 事实（`facts`）。`[host]` 部分被替换为当前主机的名称，之后引用特定的事实。结果是，为每个主机生成一行，包含 `IP` 地址、`FQDN`，紧接着是主机名。

4. 添加以下行来关闭 `for` 循环：

```
{% endfor %}
```

5. 验证完整文件内容如下所示，并保存退出文件：

```
{% for host in groups['all'] %}
{{ hostvars[host]['ansible_default_ipv4']['address'] }} {{ hostvars[host]['ansible_f_qdn'] }} {{ hostvars[host]['ansible_hostname'] }}
{% endfor %}
```

6. 使用你的编辑器创建文件 `exercise83.yaml`。它应该包含以下行：

```
---
- name: generate /etc/hosts file
  hosts: all
  tasks:
  - name:
    template:
      src: exercise83.j2
      dest: /tmp/hosts
```

7. 使用 `ansible-playbook exercise83.yaml` 运行 playbook。

8. 使用 `ansible all -a "cat /tmp/hosts"` 验证是否生成了 `/tmp/hosts` 文件。

## 总结

在本章中，你学习了如何使用 `Ansible` 操作文本文件。在第一部分，你学习了可以使用的最重要的 `Ansible` 模块。接下来，你学习了如何使用 `Ansible` 管理 `SELinux`。在本章的最后一部分，你学习了如何使用 `Jinja2` 模板生成配置文件。

## 考试准备任务

正如引言中“如何使用本书”部分提到的，你有几种准备考试的选择：此处的练习、第 16 章“最终准备”以及伴随性网站上的考试模拟题。

## 复习所有关键主题

复习本章中最重要的主题，这些主题在页面外边角标记有“关键主题（Key Topics）”图标。表 8-6 列出了这些关键主题引用及其对应的页码。

### 表 8-6 第 8 章关键主题

| 关键主题元素 | 描述 | 页码 |
|---|---|--|
| 列表 | `file` 模块任务 | |
| 表 8-4 | `Jinja2` 模板元素 | |

### 记忆表格

打印附录 D “记忆表格”（在伙伴网站上找到）的副本，或者至少打印本章的章节，并完成附录 E “记忆表格答案”（同样在伙伴网站上）中的表格和列表，其中包含了已完成的表格和列表供你检查工作。

### 定义关键术语

定义本章的以下关键术语，并在术表中检查你的答案：

- `Jinja2`
- `template`（模板）

### 复习习题

1. 你应该使用哪个模块来处理文件系统 `ACL`？
2. 你可以使用哪些模块根据正则表达式替换文本文件中的字符串？（列出两个。）
3. 你应该使用哪个模块来获取文件状态？
4. 列出三个使用 `file` 模块经常执行的任务。
5. 你应该使用哪个模块来管理 `SELinux`？
6. 使用 `file` 模块使用 `SELinux` 有什么问题？
7. 你可以使用哪个模块来更改 `SELinux`？
8. 一个 playbook 运行成功，但处理程序（handler）没有被触发。原因是什么？
9. 你如何使用 `Jinja2`？
10. `Jinja2` 的作用是什么？

### 练习答案

在执行练习 8-2 的所有步骤后，`SELinux` 的更改已完成，权限也设置正确。

## 章末实验

### 实验 8-1: 生成 /hosts 文件

编写一个 playbook 在所有主机上生成 `/hosts` 文件。满足以下要求：
