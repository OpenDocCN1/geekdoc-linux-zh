
## 继续练习

2. 输入 `ansible ansible1 -m yum -a "name=httpd state=installed"` 在主机 `ansible1` 上安装 `httpd` 软件包。
3. 使用 `ansible all -m command -a "rpm -qa | grep httpd"` 验证软件包已安装。分析输出，你可以看到 `rpm -qa` 命令在被管理主机上成功运行，但管道被忽略了。
4. 使用 `ansible all -m shell -a "rpm -qa | grep httpd"`。在输出中，你可以看到节点 `ansible2` 给出了“非零返回码”消息，这意味着命令没有成功完成。你还可以在 `ansible1` 上看到匹配的软件包列表。最后，你会看到一条警告消息，说明你应该使用 `yum` 模块。注意，`shell` 模块和 `command` 模块都报告了已更改状态作为结果，即使实际上没有发生任何变化。
5. 使用 `ansible all -m yum -a "list=httpd"` 并将其输出与步骤 4 中使用的命令的输出进行比较。
6. 使用 `ansible all -m command -a "systemctl status httpd"` 验证 `httpd` 服务的当前状态。它应该显示 `ansible2` 上未找到服务，且 `ansible1` 上的服务处于活动且禁用状态。
7. 使用 `ansible all -m service -a "name=httpd enabled=yes state=started"` 在 `ansible1` 上启动并启用 `httpd` 服务。
8. 再次运行命令 `ansible all -m command -a "systemctl status httpd"` 以验证修改已应用。

## 浏览可用模块

如前所述，要成功使用 Ansible，你需要了解模块。当然，有很多模块，为了确定哪些模块可用，你可以使用 `ansible-doc -l`。此命令列出了安装在你的系统上的所有模块。当你在一个安装了默认 Ansible 的 CentOS 8.1 运行的系统上使用它时，你会发现安装的模块数量不少于 3387 个！

事实是，Ansible 有许多可用的模块——多到你永远用不完它们，而且多到在某些情况下，你可以在不同的模块之间选择来完成相同的任务。当你初次使用 Ansible 时，寻找合适的模块可能是困难的。通过学习本认证指南，你将学习一些最实用的模块，但始终建议你搜索是否有更好的模块。你可以通过使用 `ansible-doc -l` 并使用 Linux `grep` 工具过滤输出来实现这一点。例如，使用命令 `ansible-doc -l | grep vmware` 来查看 Ansible 中所有用于管理 VMware 环境的模块。

## 查阅模块文档

Ansible 模块有良好的文档。你可以使用 `ansible-doc` 命令找到所有安装模块的文档。除了 Ansible 安装中始终可用的 `ansible-doc` 命令外，你还可以访问 Ansible 文档网站，其地址为 `https://docs.ansible.com`。

> **考试贴士**
>
> 考试期间可以使用文档，所以请学习如何使用它。你可以访问 `ansible-doc` 命令。

## 使用 ansible-doc

`ansible-doc` 命令提供了关于所有模块的信息。列表 4-3 显示了 `ping` 命令的结果。

### 列表 4-3 分析 ping 命令输出

```text
PING (/usr/lib/python3.6/packages/ansible/modules/system/ping.py)
  一个简单的测试模块，它总是返回
'pong' 在被管理主机上成功。它不仅测试连通性，还测试可管理性。它不需要任何参数。这需要配置 Python
如 `/usr/libexec/platform-python`。
 选项 (=是强制的):

- data 返回 'ping' 返回值的数据。如果此参数设置为 'crash'，模块将引发异常。[默认: pong]类型

RETURN VALUES:
nping:
  description: 与 data 参数提供的值
  returned: success
  type: str
  sample: pong
```

接下来，你会看到是谁负责维护某个模块。这是一个非常重要的信息，可以帮助你根据特定目的选择最佳模块。通常情况下，寻找由 Ansible 团队（Ansible Core Team）维护的模块是一个好主意，但如果你正在处理特定的网络设备，使用该设备供应商提供的模块可能是更好的主意。

以下元素是所有选项的列表。大多数模块都有选项，且许多模块至少有一个强制性选项。如果你的模块有强制性选项，你会发现该选项被标记为 `=option`（而不是 `-option`）。接下来的“SEE ALSO”（另参阅）部分提供了有关相关和/或类似模块的信息。查看这个部分是一个好主意，因为可能还有另一个模块能更完美地完成你的任务。

在 `ansible-doc` 输出的末尾，你会找到作者的名字，以及最重要的用法示例。在大多数情况下，这些示例显示了示例 playbook 代码。当你需要找到最常见用例的示例以及在 playbook 中实现该模块所需的 playbook 代码时，这些信息是最有用的。一直到输出的最后，你都能找到返回值。该部分提供了关于从该模块预期输出类型的信息。

默认情况下，`ansible-doc` 命令提供关于模块的完整文档。在编写 playbook 时，你通常感兴趣的是如何在 playbook 中使用必需参数。要获取这些信息，你可以使用 `ansible-doc -s modulename`。该命令的结果显示了一个示例 playbook 结构，其中列出了可以使用的参数列表以及每个参数的简短描述。由于 `ansible-doc -s` 的结果没有完整输出那么让人眼目，许多人喜欢使用这种方法。列表 4-4 显示了该命令的部分示例输出。

### 列表 4-4 使用 ansible-doc -s 显示用法信息

| name: 管理服务 | # 额外参数 |
| :--- | :--- |
| `service:` | 在命令行中提供。 |
| `enabled:` | 服务之一是否应在启动时启动。*state 和 enabled 之间至少需要其中一个。* |
| `name:` | # (必填) 服务的名称。 |
| `pattern:` | # 如果服务对状态命令没有响应，指定一个要查找的子字符串（类似于 `'ps'` 命令输出中对应的字符串），作为状态结果的替代。如果找到了该字符串，则认为该服务已启动。 |

`runlevel:`

（仅限 Gentoo）。

```bash
## 用于 OpenRC 初始化脚本
```

该服务所属的运行级别。

`sleep:`

在 `'restarted'` 之后

```bash
## 如果服务正在
```

在停止和启动命令之间的秒数。这有助于处理那些在向进程发送停止信号后立即退出的表现良好的初始化脚本。并不是所有的服务管理器都支持 `sleep`，例如当使用 `systemd` 时，此将被忽略。

## 使用 https://docs.ansible.com

除了 `ansible-doc` 提供的系统本地文档外，在考试中你也可以访问 `docs.ansible.com` 网站（见图 4-1）。在该网站上，你可以找到关于 Ansible 所需的所有知识，但在某些情况下，在哪里可以找到这些信息并不显而易见。因此，你必须在参加考试之前练习使用文档。特别是，你需要使用屏幕左上角的搜索栏。在适当的情况下，你还会在书中找到关于如何查找特定类型信息的指南。你可以在练习 4-3 中练习与文档的交互。

![](img/ea4c3f03927a5fe74f47acc2107727ea_153_0.png)

## 练习 4-3 使用文档

所有当前拥有该文件读取权限的用户。接下来，你可以运行脚本。

要从当前目录运行脚本，你通常会使用命令 `./myscript.sh`。在这条命令中，点 `.` 指向当前目录。如果当前目录不在 `$PATH` 变量中，则必须使用这个点。如果你想在不输入 `./` 的情况下运行脚本，你需要确保它所在的目录在 `$PATH` 变量中。你可以通过将脚本复制到 `/usr/local/bin` 目录来实现，该目录对于普通用户来说在 `$PATH` 变量中。

## 练习 4-4 从脚本运行即时命令

1. 在包含 `inventory` 和 `ansible.cfg` 文件的目录中，输入 `vim setup.sh` 来创建一个设置脚本。
2. 确保脚本包含以下行并保存文件：

```bash
#!/bin/bash
ansible all -m yum -a "name=vsftpd state=installed"
ansible all -m service -a "name=vsftpd sta... 
```

3. 输入 `chmod +x setup.sh` 使脚本具有可执行性。
4. 输入命令 `./setup.sh` 运行脚本并在托管主机上执行选定的任务。

## 总结

在本章中，你学习了如何使用即时命令（ad hoc commands）来设置托管主机并对托管主机进行快速检查。你还学习了 Ansible 模块以及如何使用适当工具获取 Ansible 模块的信息。在下一章中，你将学习如何使用剧本（playbooks），它们允许你以一致的方式使用 Ansible。

## 考试准备任务

正如引言中“如何使用此书”部分提到的，你有几种准备考试的方案：此处的练习、第 16 章“最终准备”以及配套网站上的考试模拟题。

## 回顾所有关键主题

回顾本章中最重要的主题，这些主题在页外边上用“关键主题”（Key Topics）图标标记。表 4-5 列出了这些关键主题的参考及其所在的页码。

![](img/ea4c3f03927a5fe74f47acc2107727ea_160_0.png)

### 表 4-5 第 4 章关键主题

| 关键主题元素 | 说明 | 页码 |
| :--- | :--- | :--- |
| 列表 | 即时命令的使用 | |

## 记忆表格

打印附录 D “记忆表格”（在配套网站上找到）的副本，或者至少打印本章章节，并记忆完成表格和列表。同样在配套网站上的附录 E “记忆表格答案”包含了完整的表格和列表，以检查你的工作。

## 定义关键术语

定义本章中的以下关键术语，并在词表中检查你的答案：

- 即时命令 (`ad hoc command`)
- `bash` 脚本
- 当前状态 (`current state`)
- 期望状态 (`desired state`)
- 等幂性 (`idempotent`)
- 模块 (`module`)

## 复习题

1. 在什么情况下你会使用即时命令？
2. 在托管主机上安装 Python 应该使用哪个模块？
3. 运行 `rpm -qa | grep httpd` 命令应该使用哪个模块？
4. 在 RHCE 考试中，你找不到安装软件的特定模块，因此你决定使用 `command` 模块安装软件。这可以吗？
5. 使用 `service` 模块启动并启用 `httpd` 服务应该使用哪些参数？
6. 你在 `user` 模块上使用 `ansible-doc` 发现该模块无法在 Windows 上创建用户。查看文档的哪个部分可以找到在 Windows 上需要使用的命令？
7. 你是一个 Python 程序员，想要为你的环境优化一个模块。你在哪里获取模块源码？
8. 执行运行即时命令的脚本时，你收到“permission denied”（拒绝访问）错误消息。最可能的解释是什么？
9. 你如何更改即时命令中使用的默认模块？
10. 获取可用于特定模块的剧本代码示例的最好方法是什么？

## 章末实验

在章末实验中，这次你将创建一个在托管主机上运行某些即时命令的脚本。

### 实验 4-1

创建一个名为 `install.sh` 的脚本，确保托管主机满足以下要求。主机是否已经满足这些要求并不重要；你的脚本的设计应当是：如果主机尚未配置，则根据这些要求设置托管主机。

- 安装 `httpd` Web 服务器。
- 启动并启用 `httpd` Web 服务器。
- 创建名为 `anna` 的用户。
- 将控制机上的 `/etc/hosts` 文件复制到托管主机的 `/tmp/` 目录。

## 第 5 章 开始使用剧本 (Playbooks)

本章涵盖了以下主题：

- 探索你的剧本
- 使用 YAML
- 管理多剧本 (Multiplay Playbooks)

本章涵盖了以下 RHCE 考试目标：

- 理解 Ansible 的核心组件
  - Plays（任务）
  - Playbooks（剧本）
- 创建 Ansible plays 和 playbooks
  - 创建剧本将系统配置为指定状态

## “我认识这些了吗？”测验

“我认识这些了吗？”测验可以让你评估是否应该阅读本章的所有任务，还是直接跳到“考试准备任务”部分。如果你对这些问题的答案或对这些主题知识的评估有疑问，请阅读整个章节。表 5-1 列出了本章的主题及其对应的“我认识这些了吗？”测验问题。

### 表 5-1 “我认识这些了吗？”章节映射

| 主题章节 | 问题 |
| :--- | :--- |
| 探索你的剧本 | 1, 2 |
| 使用 YAML | 3, 6, 7 |
| 管理多剧本 | 4, 5, 8-10 |

1. 本的第一行通常发现以下哪项？
   a. play 的名称
   b. 所选的 hosts
   c. `---`
   d. `...`
2. 每个 play 必须包含以下哪项参数？
   a. `hosts`
   b. `tasks`
   c. `name`
   d. `become`
3. 关于缩进的哪些陈述是正确的？
   a. 缩进用于识别父子对象的关系。
   b. 不可以使用空格。
   c. 不可以使用制表符。
   d. 没有缩进的 play 难以阅读。
4. 如何撤销剧本所做的修改？
   a. 使用 `ansible-playbook -u`。
   b. 使用 `ansible-playbook --force`。
   c. 你无法撤销剧本进行的更改。
   d. 你可以创建一个相反的剧本。
5. 在运行修改了系统的任务时，你预期看到什么状态？
   a. `ok`
   b. `changed`
   c. `modified`
   d. `applied`
6. 关于剧本中的 YAML 列表，哪些陈述是正确的？
   a. 任何模块都可以 YAML 列表来指定需要处理的项目。
   b. YAML 列表可以在 play 层使用，不能在 tasks 层使用。
   c. `service` 模块不支持 YAML 列表来管理多个服务器。
   d. YAML 列表可以运行多个模块。
7. 使用哪种选项将多行文本输入到文件，同时保留换行符以确保格式正确？
   a. `|`
   b. `>`
   c. `:`
   d. `\`
8. 你可以使用以下哪项验证剧本中的任务将触发更改？
   a. `--syntax-check`
   b. `--dry-run`
   c. `-vvv`
9. 以下哪项表明是多剧本的最佳用例？
   a. 在 `server1` 安装 Web 服务器；在 `server2` 安装数据库服务器。
   b. 在 `server1` 安装 FTP 服务器，之后使用 `localhost` 测试该服务器的连接性。
   c. 任务必须使用不同的用户账户运行。
   d. 一个 play 必须使用不同的权限提升参数。
10. 以下哪项不是使用多剧本的好处？
    a. 可以寻址不同的 `hosts`。
    b. Plays 可以以不同的用户账户运行。
    c. Plays 可以单独调度。
    d. 某些 plays 可以配置为在不提升权限的情况下运行。

Ansible 的核心在于运行 playbook。在本节中，你将学习如何从在命令行输入临时命令（ad hoc commands）任务过渡到编写 Ansible playbook。

## 从临时命令到 Playbook

在深入了解使用这些功能的细节之前，让我们先探索一下，运行一个 playbook。在第 4 章“使用临时命令”中，你学习了如何操作临时命令，并且在列表 4-5 中，你创建了一个 Bash 脚本来对受管节点运行其中一些命令。列表 5-1 显示了这些命令。

### 列表 5-1 从脚本中运行临时命令

```bash
#!/bin/bash
ansible all -m yum -a "name=httpd state=installed"
ansible all -m service -a "name=httpd state=started enabled=yes"
```
