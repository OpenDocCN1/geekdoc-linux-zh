
“我已经掌握这些了吗？”测试可以让你评估自己是应该仔细阅读本章，还是跳到“考试准备任务”部分。如果你对自己对主题知识的评估有疑问，请阅读整个章节。表 4-1 列出了本章的主要标题以及对应的“我已经掌握这些了吗？”测试测题。你可以在附录 A“‘我已经掌握这些了吗？’测试与复习题”中找到答案。

### 表 4-1 “我已经掌握这些了吗？”章节与题目的映射

| 基础主题章节 | 题目 |
| --- | --- |
| 理解即时命令 | 1-3 |
| 模块操作 | 4-7 |
| 查阅模块文档 | 8,9 |
| 从 Shell 脚本运行即时命令 | 10 |

1. 使用即时命令在多种情况下都很有用。以下哪项不是其中之一？

- a. 方便以一致的方式重复任务
- b. 使用 `setup` 任务快速地将管理节点带到目标状态
- c. 执行快速测试以验证剧本是否执行成功
- d. 运行发现任务以验证节点是否符合某些标准

2. 下面的示例即时命令中有什么错误？

```
ansible all -a "rpm -qa | grep http"
```

- a. 无错误。
- b. 缺少 `-m` 选项来指定应该使用哪个模块。
- c. 它使用了 `command` 模块，但在参数中使用了管道 (`|`)。
- d. 它在参数规范中缺少了 `key=value` 格式。

3. 用户在已经存在用户 `lisa` 的主机上运行即时命令 `ansible all -m user -a "name=lisa"`。发生了什么？

- a. 创建了一个名为 `lisa_o` 的第二个用户。
- b. 移除当前用户 `lisa`，并创建一个新用户 `lisa`。
- c. 命令给出错误信息，没有发生变化。
- d. 命令显示 `SUCCESS` 结果，没有发生变化。

4. 如果你想运行一个将命令输出重定向到文件 `output.txt` 的 `shell` 命令，必须使用哪个模块？

- a. `command`
- b. `shell`
- c. `raw`
- d. `bash`

5. 你想在 `Ansible` 管理的 `Cisco` 路由器上运行一个命令。你应该使用哪个模块？

- a. `command`
- b. `shell`
- c. `raw`
- d. `bash`

6. 你想在一个有多个 `Linux` 发行版的网络中安装软件。在 `Ubuntu` 节点上你会使用哪个模块来实现此？

- a. `apt`
- b. `package`
- c. `software`
- d. `install`

7. 关于 `ping` 模块，以下哪项陈述最准确？

- a. 它测试与 `Ansible` 管理机器的连通性。
- b. 它测试主机当前是否运行。
- c. 它测试清单文件的内容。
- d. 它测试主机是否处于可管理状态。

8. 你应该使用哪个命令来获取控制节点上安装的所有模块的列表？

- a. `ansible-modules`
- b. `ansible -l`
- c. `ansible-doc --list`
- d. `ansible-modules --list`

9. 哪个命令向你显示可以与模块一起使用的参数列表，且格式可以直接用于剧本中？

- a. `ansible-doc`
- b. `ansible-doc -l`
- c. `ansible-doc -s`
- d. `ansible-doc -e`

10. 获取用于系统管理的模块列表的最佳方法是什么？

- a. 对 `ansible-doc -l` 的输出使用 `Grep`。
- b. 使用 `ansible-doc system`。
- c. 在 `docs.ansible.com` 中查找模块索引并导航到系统模块部分。
- d. 使用 `ansible-doc --system`。

## 基础主题

此时，你应该已经有一个可用的 `Ansible` 基础架构了，让我们开始使用它吧！在 `Ansible` 中，你通常处理剧本 (`Playbooks`)。剧本是用 `YAML` 编写的脚本，提供了让管理节点进入所需状态的所有指令。配置剧本将在第 5 章“开始使用剧本”中介绍。在本章中，我们将学习在开始使用剧本之前需要的一些基础知识。你将学习即时命令和模块，它们允许你在无需创建任何剧本的情况下在 `Ansible` 上执行快速任务。

### 理解即时命令

即时命令 (`Ad hoc command`) 是一种针对管理主机运行的 `Ansible` 任务，而不需要使用任何剧本文件或其他脚本类的解决方案。即时命令易于使用且速度快，因此它们被频繁使用。

![](img/ea4c3f03927a5fe74f47acc2107727ea_130_1)

即时命令通常用于以下情况：

- 将节点带到目标状态的 `setup` 任务
- 验证剧本是否执行成功的快速测试
- 验证节点是否符合某些标准的发现任务

让我们来看一个示例命令，并根据该示例理解即时命令需要什么：

`ansible all -m user -a "name=lisa"`

该命令包含了几个元素。首先是 `ansible` 命令，用于运行即时命令。接下来，`all` 部分指定了在哪些主机上运行该命令。第三个元素是模块，即 `user`。在示例中，通过 `-m` 选项调用模块。最后，你通过使用 `-a` 选项为模块提供参数。在即时命令中，参数位于引号内。如果有多个参数，所有都需要包含在引号内。

#### 表 4-2 即时命令的组件

| 命令 | 用途 |
| --- | --- |
| `ansible` | 运行即时命令的命令 |
| `all` | 执行命令的主机 |
| `-m user` | 要使用的模块 |
| `-a "name=lisa"` | 传递给模块的参数 |

运行即时命令时，你必须使用 `Ansible` 用户账户（而不是 `root`），并且必须位于包含清单文件和 `ansible.cfg` 文件的目录下。接下来，你运行命令 `ansible all -m user -a "name=lisa"`，连接清单中的所有主机以确保 `lisa` 存在。

在此过程中，`Ansible` 将所需状态（你刚刚在即时命令中指定的状态）与管理机的当前状态进行比较，如果需要，它将对主机进行更改。在列表 4-1 中你可以看到命令的输出。注意运行在 `ungrouped` 上，这指的是不属于任何组的主机。

### 列表 4-1 即时命令输出

```
[ansible@control ~]$ ansible ungrouped -m user -a "name=lisa"
ansible2 | SUCCESS => (
"ansible_facts": {
  "discovered_interpreter_python": "/usr/libexec/platform-python",
  "append": false,
  "changed": false,
  "comment": "",
  "group": 1002,
  "home": "/home/lisa",
  "move_home": false,
  "name": "Lisa",
  "shell": "/bin/bash",
  "state": "present",
  "uid": 1002
}

ansible1 | CHANGED -> {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/libexec/platform-python",
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1001,
    "home": "/home/lisa",
    "name": "Lisa",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1001
  }
}
```

这就是每个 `Ansible` 命令的工作原理。`Ansible` 命令是幂等的（`idempotent`），这意味着无论当前状态如何，`Ansible` 都会将受管主机带到期望状态。无论你运行该命令多少次，结果始终是相同的期望状态。这就是所谓的 `Ansible` 命令的幂等行为：即使你多次运行同一个命令，结果也始终保持一致。在练习 4-1 中，你可以尝试自己运行一个即时命令（`ad hoc command`）。

> **注意**
>
> 在接下来的练习中，你需要以非 `root` 用户身份执行任务。为此，根据第 2 章“安装 `Ansible`”中的设置说明，你已经创建了一个名称为 `ansible` 的用户。如果你创建了不同名称的用户，请确保使用该特定用户的名称代替 "user ansible"。

### 练习 4-1 运行即时命令

1. 在控制主机上以用户 `ansible` 身份打开 `shell`。
   确保你正处于包含练习 3-3 中创建的 `ansible.cfg` 配置文件的目录中。

2. 创建一个名为 `inventory` 的清单文件，并确保它包含以下内容：

3. 输入 `ansible all -m user -a "name=lisa"` 来指示 `user` 模块创建一个名为 `Lisa` 的用户。这会在所有受管主机上创建用户 `lisa`。

4. 观察命令输出，并确保所有主机都返回 `SUCCESS`（成功）状态或 `CHANGED`（已更改）状态。

5. 再次运行该命令。所有主机现在都返回 `SUCCESS` 状态，因为这次不需要进行任何更改：主机的当前状态已经符合期望状态。

6. 输入命令 `ansible all -m command -a "id lisa"`。在该命令中，你运行了 `command` 模块（一个允许你在受管机器上运行任意命令的模块），参数为 `id lisa`，实际上是在受管节点上执行的命令。

7. 观察命令输出，输出应显示用户 `lisa` 存在，并显示该用户所属的组。

8. 使用 `ansible all -m user -a "name=lisa state=absent"` 清理受管机器。
   > 此命令会连接到受管主机并再次删除用户 `lisa`。

### 使用模块

`Ansible` 的功能由模块提供。可用超过 3000 个模块来处理广泛的任务，允许管理员管理 `Linux` 服务器、`Windows` 服务器、云基础设施、云实例、容器、网络设备等。了解 `Ansible` 等于了解模块。为正确的任务找到正确的模块是一项关键技能，你了解的模块越多，使用 `Ansible` 就会越容易。

模块可以被最好地看作是在 `Ansible Playbook` 或使用即时命令时使用的插件程序。模块本身是用 `Python` 脚本编写的。不过，这并不意味着你必须掌握 `Python`。只有当你是一个想要开发自己模块的开发者时，才需要 `Python` 知识。

#### 探索核心模块

由于使用模块至关重要，让我们探索一些关键模块。表 4-3 提供了概览。

#### 表 4-3 `Ansible` 关键模块

| 名称 | 用途 |
| --- | --- |
| `command` | 运行任意命令，但不使用 `shell` |
| `shell` | 使用 `shell` 运行任意命令 |
| `raw` | 直接在 `SSH` 之上运行命令，不使用 `Python` |
| `copy` | 将文件或文本行复制到文件中 |
| `yum` | 管理 `RHEL` 系受管主机上的软件包 |
| `service` | 管理 `systemd` 和 `system-V` 服务的当前状态 |
| `ping` | 检查受管主机是否处于可管理状态 |

让我们仔细查看这些核心模块。

##### `command`

`command` 模块允许用户使用 `Ansible` 运行任意命令。由 `command` 模块运行的命令不会被 `shell` 解释。这意味着在使用 `command` 模块时，常见的 `shell` 功能（如管道和重定向）将无法工作。`ansible all -m command -a "rpm -qa | grep nmap"` 是不起的。

`command` 模块是默认模块。这意味着如果省略 `-m command` 选项，`Ansible` 默认将提供的参数解释为 `command` 模块的参数。如果需要另一个默认模块，可以在 `ansible.cfg` 中设置选项

```
module_name = module can be set in ansible.cfg.
```

> **考试提示**
>
> 你需要在 `RHCE` 考试中完成相当多的任务。无疑，最优雅的方法是使用相应的模块。然而，使用 `command` 模块或 `shell` 模块并不是错，只是不够优雅。如果是如此，在考试中，你无法使用为执行该任务而设计的模块来完成任务，直接使用命令即可。结果才重要，在考试中，你如何达到结果并不真正重要。

##### `shell`

`shell` 模块与 `command` 模块类似，允许你运行任意命令，但有一个重要区别：`shell` 模块会通过 `shell` 运行命令。这意味着在使用此模块时，常用的 `shell` 功能（如管道和重定向）可以生效。例如，比较命令 `ansible all -m shell -a "rpm -qa | grep nmap"` 与之前使用的命令。这一次它可以正常工作。

##### `raw`

第三个允许在受管节点上运行任意命令的模块是 `raw` 模块。使用 `shell` 和 `command` 模块时，会生成一个 `Python` 脚本，并通过 `SSH` 发送到受管主机上执行。然而，`raw` 模块不需要受管主机具备 `Python`；它直接通过 `SSH` 连接发送命令。这使得 `raw` 模块成为设置机器或在没有 `Python` 的受管机器上工作的极佳选择。

使用相应的选项，可以使用 `raw` 模块在受管主机上执行初始化任务。一个示例是命令 `ansible -u root -i inventory --ask-pass -m raw -a "yum install python"`，可以在尚未接收任何 `Ansible` 配置的主机上安装 `python`。注意，`raw` 模块可以作为 `command` 或 `shell` 模块的替代方案，但这种方法并不推荐。作为一条通用原则，你应该始终尝试使用与要完成的任务最相关的模块。

> **注意**
>
> `command`、`shell` 和 `raw` 模块都用于在受管主机上运行任意命令。在大多数情况下，建议避免使用它们。大多数其他模块都是幂等的并且易于跟踪更改。`command`、`shell` 和 `raw` 模块只是运行任意命令，很难跟踪具体更改了什么，并且难以保证幂等性。由于由于原因，你应该尽可能避免使用它们。

##### `copy`

正如其名，`copy` 模块用于复制内容。你可以用它复制文件，也可以用它将简单的文本行复制到文件中。一个示例是 `ansible -m copy -a 'content="hello world" dest=/etc/motd'`，这会将“hello world”复制到 `/etc/motd` 文件。

##### `yum`

`yum` 模块用于管理 `Red Hat` 及其发行版的软件包。例如，使用 `ansible all -m yum -a "name=nmap state=latest"` 在所有管理节点上安装最新版本的 `nmap` 软件包。注意 `yum` 并不是管理软件包的唯一模块。更通用的模块是 `package`，它的优点是适用于任何 `Linux` 发行版。在两者之间，如果你需要处理特定的 `yum` 命令功能，请使用 `yum` 模块；如果首要任务是管理不同发行版上的软件，请使用 `package` 模块。

##### `service`

`service` 模块用于通过旧的 `system V (init)` 过程或 `systemd` 管理服务的状态。在使用它时，请确保不仅使用参数 `state=started` 启动服务，还使用 `enabled=yes` 启用服务。如果你只使用 `state=started`，受管服务虽然现在会启动，但在重启后不会自动启动。

重启后再次出现。它正在使用 `systemctl start myservice`，而没有使用 `systemctl enable myservice`。

例如，使用 `ansible all -m service -a "name=httpd state=started enabled=yes"` 来启用并启动 `httpd` 服务。（显然，在执行此操作之前，你必须先使用 `yum` 模块来安装 `httpd` 服务。）

##### `ping`

`ping` 模块是一个简单的模块，可用于检查主机是否已正确配置以便用 `Ansible` 管理。因此，它不仅仅是测试连通性，还测试可管理性。它不需要任何参数。只需使用 `ansible -m ping` 即可检查清单文件中所有主机的连通性。列表 4-2 显示了可用主机的响应，同时也显示了当主机不可用时你会看到的内容。要获得相同的结果，只需在清单文件中添加主机 `ansible3` 即可。在练习 4-2 中，你可以练习使用该模块以及这里讨论的其他模块。

### 列表 4-2 分析 `ping` 模块输出

```
[ansible@control ~] ansible all -m ping
ansible3 | UNREACHABLE => {
  "changed": false,
  "msg": "Failed to connect to the host via ssh:
  Could not resolve hostname ansible3: Name or service not
known",
  "unreachable": true
}
ansible2 | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python":
    "/usr/libexec/platform-python"
  },
  "changed": false,
  "ping": "pong"
}
ansible1 | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python":
    "/usr/libexec/platform-python"
  },
  "changed": false,
  "ping": "pong"
}
```

### 练习 4-2 在即时命令中使用模块

1. 使用 `ansible all -m ping` 验证清单文件中的所有主机都处于可管理状态。
