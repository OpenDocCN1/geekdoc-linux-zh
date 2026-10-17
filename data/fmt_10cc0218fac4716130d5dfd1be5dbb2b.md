
```
[student@workstation deploy-manage]$ ansible intranetweb --list-hosts
BECOME password: student
hosts (1):
servera.lab.example.com
```

## 完成

在工作站上，运行 `lab deploy-manage finish` 脚本清理本次练习。

```
[student@workstation ~]$ lab deploy-manage finish
```

引导式练习结束。

# 运行即时命令 (AD HOC COMMANDS)

## 目标

完成本节后，你应该能够使用即时命令（ad hoc command）运行单个 Ansible 自动化任务，并解释即时命令的一些用场景。

## 使用 Ansible 运行即时命令

即时命令是一种快速执行单个 Ansible 任务的方法，你不需要将其保存以便以后再次运行。它们是简单的在线操作，可以在不编写剧本（playbook）的情况下运行。

即时命令对于快速测试和更改非常有用。例如，你可以使用即时命令来确保一组服务器上的 `/etc/hosts` 文件中存在某行特定。你可以使用另一个即时命令高效地在多台不同的机器上重启服务，或者确保特定的软件包已更新到最新。

即时命令对于使用 Ansible 快速执行简单任务非常有用。它们也有其局限性，通常你可能希望使用 Ansible Playbooks 来充分发挥 Ansible 的威力。但在许多情况下，即时命令正是你快速执行简单任务所需的工具。

## 运行即时命令

使用主机模式（host-pattern）运行即时命令：

```
ansible host-pattern -m module [-a 'module arguments'] -i inventory
```

`host-pattern` 参数用于指定运行即时命令的托管主机。它可以是清单中的某个特定托管主机或主机组。你已经看到过它与 `--list-hosts` 选项结合使用，该选项会显示哪些主机匹配了模式主机。你还看到可以使用 `-i` 参数来指定与当前 Ansible 配置文件中默认位置不同的清单位置。

`-m` 参数的参数是 Ansible 应该在目标主机上运行的模块名称。模块是执行以实现你的任务的小型程序。某些模块不需要额外信息，但另一些模块需要额外的参数来指定操作的细节。`-a` 参数接收这些参数列表作为引号字符串的形式。

最简单的即时命令之一是使用 `ping` 模块。该模块并不执行 ICMP ping，而是检查你是否可以在托管主机上运行基于 Python 的模块。例如，以下即时命令确定清单中的所有托管主机是否都能运行标准模块：

### 第 2 章 | 部署 Ansible

```
[user@controlnode]$ ansible all -m ping
server.la.example.com | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/libexec/platform-python",
  "changed": false,
  "ping": "pong"
}
```

## 使用即时命令通过模块执行任务

模块是即时命令完成任务的工具。Ansible 提供了数百个模块，你通常可以使用它们完成工作。当你标准安装中发现一个经过测试的、满足你特殊特殊模块时。

`ansible-doc -l` 列出了系统上安装的所有模块。你可以使用 `ansible-doc` 通过名称查看特定模块的文档，并查找有关模块接受哪些参数作为选项的信息。例如，以下命令显示了 `ping` 模块的文档：

```
[user@controlnode]$ ansible-doc ping
> PING (/usr/lib/python3.6/site-packages/ansible/modules/system/ping.py)
```

这是一个测试模块，它在成功连接时始终返回 'pong'。它在剧本中没有意义，但从 '/usr/bin/ansible' 调用时，它对于验证登录能力以及配置了可用的模块很有用。它不是 ping，这只是一个在远程节点需要 Python 的测试模块。对于 Windows 目标，请使用 `win_ping` 模块。对于网络目标，请使用 `net_ping` 模块。

- * 此模块由 Ansible Core 团队维护

选项 (= 是强制性的):

- 为 'ping' 返回值返回的数据。

如果此参数设置为 'crash'，模块将导致异常。

[默认值: pong]

type: str

- 另另：

* `net_ping`

`net_ping` 模块的官方文档。

https://docs.ansible.com/ansible/latest/modules/net_ping_module.html

* `win_ping`

`win_ping` 模块的官方文档。

https://docs.ansible.com/ansible/latest/modules/win_ping_module.html

作者：Ansible Core Team, Michael DeHaan

元数据：

status:

- stableinterface

RH294-RHEL8.0-en-2019531

### 第 2 章 | 部署 Ansible

支持：core

示例：

```
## 测试可以登录 'webservers' 并使用 json 执行 python
## ansible webservers -m ping
```

## 来自 Ansible Playbook 的示例

- ping:

## 诱发异常以查看发生了什么

- ping:

  data: crash

返回值：

ping:

description: 由 data 参数提供

returned: success

type: str

sample: pong

要了解更多关于模块，请访问 http://docs.ansible.com/ansible/latest/modules_by_category。下面的表列出了许多实用模块。

## Ansible 模块

| 类别 | 模块 |
| --- | --- |
| 文件模块 | - `copy`: 将本地文件复制到托管主机<br>- `file`: 设置权限和其他属性<br>- `lineinfile`: 确保文件中存在某行<br>- `synchronize`: 使用 `rsync` 同步内容 |
| 软件包模块 | - `package`: 使用自动检测包管理器管理软件包<br>- `yum`: 使用 YUM 包管理器管理软件包<br>- `apt`: 使用 APT 包管理器管理软件包<br>- `dnf`: 使用 DNF 包管理器管理软件包<br>- `gem`: 管理 Ruby gem<br>- `pip`: 管理来自 PyPI 的 Python 包 |
| 系统模块 | - `firewall`: 管理任意端口和服务服务<br>- `reboot`: 重启机器<br>- `service`: 管理服务<br>- `user`: 添加、删除和管理用户账户 |

### 第 2 章 | 部署 Ansible

| 类别 | 模块 |
|---|---|
| 网络工具模块 | - `get_url`: 通过 HTTP、HTTPS 或 FTP 下载文件<br>- `nmcli`: 管理网络<br>- `uri`: 与 Web 服务交互 |

大多数模块都需要参数。你可以在模块的文档中找到可用的参数列表。即时命令使用 `-a` 参数将参数传递给模块。不需要参数时，省略即时命令中的 `-a` 参数。如果需要多个参数，请以空格分隔的列表提供。

例如，以下命令使用 `user` 模块在 `server.example.com` 上创建 UID 为 4000 的 newbie 用户：

```
$[controlnode]$ ansible -m user -a 'name=newbie uid=4000 state=present' \
server.example.com | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/libexec/platform-python"
  },
  "changed": true,
  "comment": ""
  "createhome": true,
  "group": 4000,
  "home": "/home/newbie",
  "name": "newbie",
  "shell": "/bin/bash",
  "state": "present",
}
```

大多数模块都是幂等的（idempotent），这意味着它们可以多次运行，如果系统处于正确状态，它们将报告没有更改。例如，如果你再次运行即时命令，它应该报告没有更改：
