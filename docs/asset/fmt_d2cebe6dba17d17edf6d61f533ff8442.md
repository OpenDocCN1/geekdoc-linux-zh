
前面的示例在组 `linux` 中定义的所有主机上执行命令 `uname -r`。第二个命令将文件 `/etc/hosts` 从控制节点复制到远程节点，并将文件存储在 `/tmp/hosts`。由于目标文件不存在或内容不同，任务被标记为 `CHANGED`。当文件的内容和属性相当时，文件不会修改，任务被标记为 `SUCCESS`，如图 12.19 所示：

```bash
agonzalez@ubuntu:~$ ansible rhel -m copy -a "src=/etc/hosts dest=/tmp/hosts"
rhel | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/bin/python3"
  },
  "changed": false,
  "checksum": "3be3cada0d11b51a5ab9474c501cdf420eec49a",
  "dest": "/tmp/hosts",
  "gid": 1000,
  "group": "agonzalez",
  "mode": "0664",
  "owner": "agonzalez",
  "path": "/tmp/hosts",
  "size": 221,
  "state": "file",
  "uid": 1000
}
```

图 12.19：`ansible` 命令的输出示例

临时操作（Ad-hoc）仅应在特定场合使用，例如检查连接性或执行快速任务。建议编写包含已定义任务的 `Playbook`，以便在需要时进行重用或修改。

### YAML

这种数据序列化语言是定义应用程序配置的最流行语言之一。其流行性源于可读性；与其他格式如 `XML` 和 `JSON` 相比，创建和操作更容易。在上一节 *主机清单（Inventory）* 中，我们引入了它来定义主机和变量。`Ansible` 中的剧本、任务和变量将以 YAML 定义。以下代码块展示了一段有效的 YAML 代码：

```yaml
---
name: Alberto
age: 38
married: False
technologies:
- Ansible
- Terraform
- Linux
data:
  name: Alberto
  lastname: Gonzalez
...
```

从前面的示例中，可以观察到以下概念：

- YAML 文件以三个短横线（`---`）开始。
- YAML 文件以三个点（`...`）结束。
- 普通变量可以包含字符串（`name`）或数字（`age`）。字符串可以使用双引号或单引号包裹。
- 可以定义布尔变量（`married`）。
- 可以定义包含元素列表的变量（`technologies`）。
- 可以定义包含键和值的字典（`data`）。要访问值，有以下两种方法：
  - `data['name']`
  - `data.name`

可以有复杂的变量，例如列表的列表、字典的列表，或者字典的值可以包含列表，以及其他复杂的组合。YAML 提供了灵活性，可以定义包含多行值或长行的变量。使用特殊字符竖线 (`|`) 和大于号 (`>`)。参考以下示例：

```yaml
---
separated_lines: |
Lorem ipsum dolor sit amet, consectetur adipiscing elit, 
sed do eiusmod tempor incididunt ut labore et dolore magna 
aliqua.  
Ut enim ad minim veniam, quis nostrud exercitation ullamco 
laboris 
nisi ut aliquip ex ea commodo consequat.
joined_lines: >  
Lorem ipsum dolor sit amet, consectetur adipiscing elit, 
sed do eiusmod tempor incididunt ut labore et dolore magna 
aliqua.
```

`Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`

`表 12.5` 展示了该变量的结果（其中 `\n` 是换行的特殊字符）：

|  |  |
|---|---|
| `separated_lines` | Lorem ipsum dolor sit amet, consectetur adipiscing elit, `<br>\nsed do eiusmod tempor incididunt ut labore et dolore<br>` magna aliqua. `\n`<br>\nut enim ad minim veniam, quis nostrud<br>exercitation ullamco laboris `\n`nisi ut aliquip ex ea<br>commodo consequat`\n` |
| `joined_lines` | Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat`\n` |

*表 12.5：多行 Ansible 变量示例*

### Ansible 配置

`Ansible` 中的某些设置可以通过名为 `ansible.cfg` 的配置文件进行调节。可以使用命令 `ansible-config` 配合参数 `init` 生成该文件。可以使用选项 `--disabled` 来包含所有可用的选项。选项 `-t all` 包含所有与**插件**相关的选项。配置文件包含不同的部分，以下是一些示例：

- `[defaults]`： `Ansible` 工具的默认选项。
- `[privilege_escalation]`： 权限提升选项，例如 `sudo`。
- `[persistent_connection]`： `SSH` 持久连接的选项。
- `[colors]`： 定义用于不同状态（已更改、错误等）的颜色。
- `[galaxy]`： 公共存储库 `Ansible Galaxy` 的选项。
- `[inventory]`： 清单文件和**插件**的选项。
- `[jinja2]`： 名为 `Jinja2` 的模板系统的选项。
- `[ssh_connection]`： `SSH` 的选项。
- `[tags]`： `Ansible 标签`的选项。

`Ansible` 将尝试按以下顺序定位 `ansible.cfg` 文件：

- 指向 `ansible.cfg` 位置的环境变量 `ANSIBLE_CONFIG`
- 当前目录
- 文件 `~/.ansible.cfg`
- `/etc/ansible/ansible.cfg`

配置中一些常见的选项及其默认值定义在*表 12.6* 中：

| 选项 | 默认值 | 描述 |
| :--- | :--- | :--- |
| `[defaults]` | | |
| `inventory` | `/etc/ansible/hosts` | 默认清单源 |
| `forks` | `5` | 用于执行任务的最大进程数。 |
| `host_key_checking` | `True` | 检查目标主机的主机密钥。 |
| `timeout` | `10` | 连接插件使用的默认超时时间 |
| `[privilege_escalation]` | | |
| `become` | `False` | 切换权限提升的使用 |
| `become_method` | `sudo` | 当“`become`”启用时要使用的权限提升方法。 |
| `become_user` | `root` | 你的远程用户*变为*的用户。 |
| `become_ask_pass` | `False` | 切换以提示输入权限提升密码。 |
| `[ssh_connection]` | | |
| `ssh_args` | `-C -o ControlMaster=auto -o ControlPersist=60s` | 传递给所有 SSH CLI 工具的参数。 |
| `control_path_dir` | `~/.ansible/cp` | 用于*`ControlPath`*的目录。 |

### 剧本 (Playbooks)
