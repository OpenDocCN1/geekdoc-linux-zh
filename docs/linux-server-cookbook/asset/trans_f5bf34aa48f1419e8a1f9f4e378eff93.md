
## 包含与导入

处理单个 *Playbook*（剧本）可能涉及许多行，包括变量定义、任务和处理程序（handlers）。*Ansible* 允许使用 *tasks*（任务）或 *Play*（剧本）选项将文件拆分并在主文件中包含它们。可执行的语句在 *表 12.8* 中描述：

| 语句 | 描述 |
| :--- | :--- |
| `include_vars` | 任务部分内的一个任务。包含带有变量的 YAML 文件。示例：<br>`tasks:`<br>`#include_vars: variables_httpd.yaml` |
| `vars_files` | 在 *Playbook* 级别可以定义包含 *Playbook* 所需变量的文件。示例：<br>`- name: My playbook`<br>`#hosts: webservers`<br>`#vars_files:`<br>`#variables_httpd.yaml` |
| `import_playbook` | 在 *Playbook* 级别可以包含外部 *Playbooks*（剧本）。示例：<br>`#import_playbook: configure_httpd.yaml`<br>`#import_playbook: configure_mariadb.yaml` |
| `include_tasks` `import_tasks` | 任务部分内的一个任务。它包含（或导入）文件中定义的任务列表。可以向任务传递变量。示例：<br>`tasks:`<br>`#include_tasks: install_httpd.yaml`<br>`#import_tasks: configure_httpd.yaml`<br>`#vars:`<br>`#httpd_port: 443`<br><br>可以在处理程序部分中包含任务。 |
| `include_role` `import_role` | 它在 *tasks*（任务）部分内包含一个 *role*（角色）（如下所述）。示例：<br>`#import_role:`<br>`#name: httpd`<br>`#include_role:`<br>`#name: httpd` |

*表 12.8*：用于变量、任务和角色的文件包含语法及示例。

*Import*（导入）语句在剧本解析时预先处理；而 **include**（包含）语句则在剧本执行期间处理。

## 事实与魔术变量

当 *Ansible* 连接到 **host**（主机）时，默认会收集有关该主机的信息。这些信息称为 **facts**（事实）。一个名为 **ansible_facts** 的特殊变量会被填充有关远程系统的信息，例如操作系统、发行版、IP 地址、系统资源信息等。可以使用模块 **debug**（调试）来打印关于 **ansible_facts** 变量的信息。以下代码显示了 *Ubuntu* 系统的输出示例（已截断，仅显示部分值）：

```text
TASK [debug]
*********************************************************************
****
ok: [ubuntu] => {
  "ansible_facts": {
    "all_ipv4_addresses": [
      "192.168.122.43",
      "192.168.100.1"
    ],
    "all_ipv6_addresses": [
      "fe80::5054:ff:fe1a:9cc4",
      "fe80::5054:ff:fe8f:d41a"
    ],
    "architecture": "x86_64",
    "discovered_interpreter_python": "/usr/bin/python3",
    "distribution": "Ubuntu",
    "distribution_major_version": "22",
    "distribution_release": "jammy",
    "distribution_version": "22.04",
    "dns": {
      "nameservers": [
        "8.8.8.8"
      ]
    },
    "kernel": "5.15.0-50-generic",
"kernel_version": "#56-Ubuntu SMP Tue Sep 20 13:23:26 UTC
2022",
"memfree_mb": 1806,
"memtotal_mb": 3923,
"nodename": "ubuntu",
"os_family": "Debian",
"processor_count": 2,
}
}
```

上述示例仅显示了 **ansible_facts** 变量中可用的部分选项。该变量包含有关系统的更多信息，例如关于以太网网卡、磁盘和挂载点的详细信息。

Ansible 具有一些魔术变量，用户无法直接设置它们，并且 **Ansible** 会根据配置或获取的事实覆盖其值。对于在 **ansible_facts** 中定义的变量，将以前缀 **ansible_** 开头。例如，**ansible_facts** 中的 **os_family** 键可以通过魔术变量 **ansible_os_family** 访问。

## 条件语句

可以使用表达式 **when** 有条件地执行基于任务的操作。指示的条件可以是变量具有特定值或所需的任何比较。在以下任务示例中，仅当 **ansible_distribution** 变量等于 Ubuntu 时，该任务才会被执行。

```yaml
- name: Conditionals example
  hosts: linux
  become: True
  tasks:
    - name: Install apache2 package
      ansible.builtin.apt:
        name: apache2
      when: ansible_distribution == "Ubuntu"
```

如果条件被评估为 false，则该任务将在特定 *host*（主机）上被跳过。图 12.28 显示了输出示例：

```text
agonzalez@ansible:~/playbooks$ ansible-playbook playbook5.yaml
PLAY [Conditionals example] *****************************************************

TASK [Gathering Facts] ******************************************************
ok: [rhel]
ok: [ubuntu]

TASK [Install apache2 package] **********************************************
skipping: [rhel]
changed: [ubuntu]

PLAY RECAP *******************************************************************
rhel   : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
ubuntu : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

![](img/863afa537de4eed7deb11978bfbfa90e_418_0.png)

简单的值比较在 *表 12.9* 中描述：

| 表达式 | 描述 | 示例 |
| :--- | :--- | :--- |
| `item1 == item2` | 检查两个元素是否具有相同的值。 | `ansible_distribution == "Ubuntu"` |
| `item1 != item2` | 检查两个元素是否具有不同的值。 | `ansible_distribution != "Ubuntu"` |
| `item1 > item2` | 检查 *item1* 是否大于 *item2* | `ansible_distribution_major_version > 15` |
| `item1 >= item2` | 检查 *item1* 是否大于或等于 *item2* | `ansible_processor_count >= 2` |
| `item1 < item2` | 检查 *item1* 是否小于 *item2* | `ansible_distribution_major_version < 15` |
| `item1 <= item2` | 检查 *item1* 是否小于或等于 *item2* | `ansible_processor_count <= 2` |

![](img/863afa537de4eed7deb11978bfbfa90e_418_1.png)

Ansible 允许更多的逻辑条件，如 *表 12.10* 中所述：

| 表达式 | 描述 | 示例 |
| :--- | :--- | :--- |
| `item1 ~ item2` | 检查 *item1* 是否在 *item2* 的值内部 | `"x86" ~ ansible_architecture` |
| `item1 in item2` | 检查 *item1* 是否在元素列表 item2 内部 | `ansible_distribution in ["Ubuntu", "Debian"]` |
| `item1 not in item2` | 检查 item1 是否在元素列表 item2 外部 | `ansible_distribution not in ["Ubuntu", "Debian"]` |
| `item1 is defined` | 检查变量 item1 是否已定义 | `username is defined` |
| `item1 is not defined` | 检查变量 item1 是否未定义 | `username is not defined` |

*表 12.10：逻辑条件表达式*

可以使用单词 **and**（与）以及单词 **or**（或）来组合条件表达式。以下示例展示了用法，其中 *task* 是由用户定义的变量：

```yaml
    - name: Install apache2 package
        ansible.builtin.apt:
            name: apache2
        when: ansible_distribution == "Ubuntu" and (
            task is defined and task == "install")
```

## 循环

使用 Ansible，可以循环元素并为每个元素执行任务。可以遍历简单列表或复杂变量，例如字典。使用表达式 **loop**，可以遍历简单和复杂元素。以下示例显示了一个简单示例：

```yaml
        - name: Install required packages
            ansible.builtin.apt:
                name: "{{ item }}"
            loop:
                - apache2
                - php
                - php-mysql
```

如前一个示例所示，特殊变量 **item** 包含循环中每个元素的值。图 12.29 显示了前一个任务执行的示例输出：

```text
TASK [Install required packages] ***************************************************
changed: [ubuntu] => (item=apache2)
changed: [ubuntu] => (item=php)
changed: [ubuntu] => (item=php-mysql)
```

*图 12.29：使用循环的输出示例*

以下示例展示了如何循环一个包含要创建的用户名和组的字典列表。为此，使用了模块 **user**（用户）。

```yaml
- name: Create users
  ansible.builtin.user:
    name: "{{ item.name }}"
    groups: "{{ item.groups }}"
  loop:
    - {name: "user1", groups: "users"}
    - {name: "user2", groups: "users,sudo"}
```

## 注册

Ansible 的任务会生成有关执行的信息。可以使用表达式 **register** 将该信息保存在变量中。在使用模块 **command**（命令）或 **shell**（shell）时，这特别有用。以下代码显示了一个示例：

```yaml
- name: Run a command
  ansible.builtin.command: hostname -I
  register: hostname_output
- name: Show content of registered variable
  ansible.builtin.debug:
    var: hostname_output
```

图 12.30 显示了 **debug**（调试）任务的输出：

