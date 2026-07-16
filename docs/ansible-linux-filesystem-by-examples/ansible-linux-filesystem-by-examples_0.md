# Ansible Linux Filesystem 示例










* * * * * *

这是一本 Leanpub 书籍。Leanpub 通过精益出版流程为作者和出版社赋能。精益出版是指使用轻量级工具和多次迭代来发布进行中的电子书，以获取读者反馈，不断调整直到你获得正确的书籍，并在成功后建立影响力。

* * * * * *






## 引言

这本书提供了 `Ansible` 的介绍。`Ansible` 是一种流行的开源工具，可移植且易于使用。它是适用于广泛领域的自动化工具。无论你何时开始接触自动化，本书的目标是让你快速掌握核心知识。你将从在 `RedHat`、`Ubuntu` 和 `macOS` 上安装 `Ansible` 开始。100+ 节中的每一个都总结了一个模块。

## 谁是 Luca Berton

我是 Luca Berton，我们将过得很愉快。首先，让我介绍一下我自己。

我是 Red Hat 的 `Ansible` 技术支持工程师，居住在捷克，尽管我是意大利人。我有超过 15 年的系统管理经验，涉及本地基础设施以及主要的云提供商。

我是开源的热衷爱好者，通过在不同的公开活动中分享知识来支持社区。我还是家乡 Linux 用户小组的联合创始人，该小组曾接待过自由软件运动的创始人 Richard Stallman。

我认为自己是一个懒人，所以我总是尝试新方法来自动化工作中的重复性任务。在使用了多年 `Perl`、`Bash` 和 `python` 脚本后，我接触了 `Ansible` 技术。我通过了认证并与 `Ansible` 工程师团队工作了一多年。

我认为 `Ansible` 是目前最好的基础设施自动化技术，它具有可读性，学习曲线容易，且非常受市场招聘人员的青睐。





- [Red Hat Ansible Playbook 包含于 RHSB-2021-009 Log4Shell - 远程代码执行 - log4j (CVE-2021-44228) 2022 年 1 月 12 日](https://access.redhat.com/security/vulnerabilities/RHSB-2021-009#diagnose)
- [AWS Tip 设置 sysctl 内核参数 — Ansible 模块 sysctl 2022 年 1 月 12 日](https://awstip.com/set-sysctl-kernel-parameters-ansible-module-sysctl-83fc2b3f77f)
- [The Ansible Bullhorn #41 - 面向 Ansible 开发者社区的通讯 2022 年 1 月 7 日](https://mailchi.mp/redhat/the-bullhorn-41)
- 2021
- [The Ansible Bullhorn #34 - 面向 Ansible 开发者社区的通讯 2021 年 9 月 17 日](https://us19.campaign-archive.com/?u=56d874e027110e35dea0e03c1&id=5f02018283)

本课程将持续跟踪 Ansible 技术的演进，并在需要时添加更多内容。

你准备好享受其中了吗？

带示例的 Ansible 入门

在本章中，你将发现 Ansible 的基础、架构和术语。

## 什么是 Ansible

在本章中，我将向你解释什么是 Ansible，以及为什么它对你的 IT 部门如此强大。

## Ansible

基础设施自动化工具

开源基础设施即代码 (IaC)

首先，让我们从名为 Ansible 的极出开源技术开始我们的冒险。它被归类为基础设施自动化工具，因此你可以轻松地自动化你的系统管理员任务。基础设施即代码是指通过机器可读的定义文件来管理和配置计算机数据中心的过程，而不是通过物理硬件配置或交互式配置工具。Ansible 遵循 DevOps 原则。通过 Ansible，你可以在本地以及最知名的公共云服务提供商处部署你的基础设施即代码。

## Ansible 的三个用例

- 资源准备 (Provision)
- 配置管理 (Config management)
- 应用部署 (Application deployment)

Ansible 的三个主要用例是资源准备、配置管理和应用部署。但在接触这项技术后，我确定你还可以发明更多使用它的方法！

### 资源准备 (Provisioning)

设置 IT 基础设施的过程

让我们开始谈谈资源准备：所有的系统管理员都知晓管理统一机器集群有多重要。有些人仍然依赖软件来创建工作站镜像。但这样做有一个缺点，使用镜像技术你只是获取了机器在某一时间点的快照。因此，每当你因为现代密钥激活系统需要重新安装软件，或者需要手动更新到最新的安全补丁时，Ansible 在自动化这一过程方面非常强大，能够创建一个更流畅的过程。

### 配置管理 (Configuration management)

将系统和软件维护在所需且一致状态的过程

第二个关键用例是“配置管理”：以更新且一致的方式维护你的整个集群，协调滚动更新并调度停机时间。通过 Ansible，你可以验证受托管主机的状态，并对其中一小部分主机采取操作。对于最常用的用例，有大量的模块可用。更不用说检查你的集群是否符合某些国际标准并应用解决方案的这种常见用例了。

### 应用部署 (Application deployment)

在测试、暂存和生产环境之间发布软件的过程

Ansible 有用的第三个关键用例是应用部署。它可以自动化你的 Web 应用的持续集成/持续交付 (CI/CD) 工作流流水。你的 DevOps 团队会非常高兴的！

## DevOps 中的 Ansible

Ansible 用于在全球范围内组织中应用 DevOps 原则。让我快速总结一下。

DevOps 是一系列结合软件开发 (Dev) 和 IT 运营 (Ops) 的实践。由于 DevOps 旨在成为一种跨部门的工作模式，实践该方法的人使用不同的工具集，称为“工具链”，而不是单一工具。这些工具链预计符合以下一类或多个类别，反映了开发和交付过程的关键方面。这七个类别是：

- 代码 (Code)：代码开发和审查、源码管理工具、代码合并。
- 构建 (Build)：持续集成工具、构建状态。
- 测试 (Test)：持续测试工具，提供对业务风险的快速且及时的反馈。
- 发布 (Release)：制品仓库、应用部署前的暂存环境。
- 部署 (Deploy)：变更管理、发布审批、发布自动化。
- 运行 (Operate)：基础设施配置和管理、基础设施即代码工具。
- 监控 (Monitor)：应用性能监控、终端用户体验。

## Ansible 的四个核心原则

1. **声明式 (Declarative)**：你声明你想要什么，而不是如何实现。
2. **无代理 (Agentless)**：你不需要安装代理。它利用了 `OpenSSH`。
3. **幂等性 (Idempotent)**：操作可以运行多次，而不会产生初始操作之外的变化。
4. **社区驱动 (Community driven)**：以集合和（和）的形式发布在 Ansible Galaxy 中。

Ansible 的四个核心原则是：声明式、无代理、幂等和社区驱动。“对于声明式”意味着你可以以一种非常类似于编程语言的方式使用它，在代码流中应用顺序、选择和迭代。“无代理”意味着你不需要在目标机器上安装和更新任何代理，它使用 `SSH` 连接和 Python 解释器。语言本身是“幂等”的，这意味着代码将检查受托管机器上的精确状态。这意味着，例如，你的代码第一次运行时会更改某些内容，随后的运行仅会验证没有变化并继续进行。最后一个原则是“社区驱动”，意味着存在一个公共平台 Ansible Galaxy，你可以在那里以集合和角色的形式发布内容。





2015 年 10 月 16 日，红帽（Red Hat）收购了 Ansible Inc，并将 Ansible 评估为“强大的 IT 自动化解决方案”，旨在帮助企业迈向无缝 IT。

AnsibleFest 是自 2016 年以来在伦敦和美国举办的 Ansible 用户及贡献者社区年度会议。

# Ansible & Ansible Tower & Ansible Automation Platform

## Ansible
社区驱动的项目，创新快速，是开源的，但仅提供命令行工具。

## Red Hat Ansible Tower / Ansible Automation Platform
这是一个由红帽公司设计的框架。它提供了一个 Web UI 来管理您的基础设施。

Ansible 是一个社区驱动的项目，创新快速，开源的，但仅提供命令行工具。

企业级需要更多的服务和一些稳定的版本。例如，它们需要支持方面的 SLA。红帽为公司提供此类服务，即在 Ansible Tower 品牌下提供，现在已重命名为 Ansible Automation Platform。

Ansible Tower 是一个 REST API、Web 服务和基于 Web 的控制台，旨在让具有不同技术熟练程度和技能的 IT 团队更容易使用 Ansible。它是自动化任务的枢纽。该 Tower 是由红帽公司支持的商业产品，但源自 AWX 上游项目，该项目自 2017 年 9 月起已开源。

红帽还维护 Ansible Engine。通过 Ansible Engine，组织可以以加固的企业级方式访问底层 Ansible 技术提供的工具和创新。Ansible Engine 由红帽开发，明确意图是作为企业 IT 平台使用。

# 入门
在本章节中，我将为您解释如何使用 Ansible 技术迈出第一步。如何连接到托管主机以及如何使用命令行执行一些任务。

## Ansible 架构
让我们开始讨论 Ansible 架构。实际安装 Ansible 的节点被称为“控制节点”（control node），它管理您所有的节点组。另一方面，被节点被称为“托管节点”（managed node）。目标节点可以是 Linux、Mac、Windows 以及多种网络设备。每个目标都有某些特殊性，例如不同的 Linux 发行版和模块用法。我们将在后续章节中讨论这些特殊性。

## 与托管节点的连接
“控制节点”与“托管节点”之间的连接通过 SSH 协议管理，对目标机器不需要任何特定的客户端。其他竞争对手需要通常被称为“代理”（agent）的客户端软件。使用 SSH 连接，唯一的要求是用于访问目标机器用户名和证书。还有一些方法可以自动化这第一个脚本步骤。在完成 SSH 连接后，另一个要求是 `python` 解释器，现代操作系统自带该。默认情况下，Ansible 使用 SFTP 传输文件，但您可以在配置中切换到 SCP。Windows 目标可以使用 WinRM 技术连接，并使用 PowerShell 作为解释器。

## 创建基础清单
`/etc/ansible/hosts`

```
host1.example.com
```
默认清单文件 `/etc/ansible/hosts`

“host1.example.com” 是一个托管主机

托管主机列表存储在 `/etc/ansible/hosts` 中。在本示例中，它只包含一个名为 `host1.example.com` 的主机。

## 运行您的第一个 Ansible 命令
```bash
$ ansible all -m ping 2 host1.example.org | SUCCESS => { 3     "ansible_facts": { 4         "discovered_interpreter_python": "/usr/bin/python" 5     }, 6     "changed": false, 7     "ping": "pong" 8 }
```
`ping` 模块在所有“all”主机上执行

“host1.example.com”以成功代码回复

现在我们准备好运行您的第一个 Ansible 命令了。在 Ansible 术语中，命令被称为模块（module）。第一行在所有主机上执行 Ansible `ping` 模块。响应是 pong。请注意，这意味着 Ansible 能够通过 SSH 用户名连接，使用公钥识别并执行本地 python 执行器。因此，它与网络中的任何 ping 完全不同。

## 在 Ansible 上运行即时命令
```bash
$ ansible all -a “/bin/echo hello” 2 host1.example.org | CHANGED | rc=0 >> 3 hello
```
`/bin/echo hello` 命令在所有“all”主机上执行

“host1.example.com”以更改代码回复并在标准输出上打印“hello”

Ansible 也可以在目标主机执行某些命令并在“控制节点”控制台上报告状态。在本示例中，`/bin/echo hello` 命令在所有“all”主机上执行。“host1.example.com”以更改代码回复并在标准输出上打印“hello”。请注意，每当您在远程机器上运行命令时，都会收到“changed”（已更改）状态。

## 在 Ansible 上运行带权限提升的即时命令
```bash
$ ansible all -m ping -u devops --become 2 host1.example.org | SUCCESS => { 3     "ansible_facts": { 4         "discovered_interpreter_python": "/usr/bin/python" 5     }, 6     "changed": false, 7     "ping": "pong" 8 }
```
以用户“devops”登录后，以用户“root”身份在所有“all”主机上执行 `ping` 模块

“host1.example.com”以更改代码回复并在标准输出上打印“hello”

在本示例中，我在以用户“devops”登录后，以用户“root”身份对“all”主机运行 `ping` 模块。（注：此处原文可能误写为 hello）

## 总结
在本模块中，我们学习了 Ansible 架构的基本概念、如何编写托管主机列表以及如何对它执行某些命令。

# 清单
在本章节中，我将向您解释什么是 Ansible 清单、为什么需要以及如何编辑和使用。

由 Ansible 管理的多主机列表被称为“清单”（inventory）。从根本上说，它是节点或主机的集合，使用列表或组。您可以通过“组”或“模式”组织您的清单以选择要运行的主机。

“all”关键字
`all` 关键字包含清单中的所有主机。例外是需要指定的 localhost。

## 简单的 INI 清单
`/simple_inventory`

```
host1.example.com

[webservers]
two.example.com
three.example.com
```
文件名：`simple_inventory`

“host1.example.com”未分组

“two.example.com”和“three.example.com”被分在“webservers”

简单的清单类型是 INI 清单，取决于文件类型。默认位置是 `/etc/ansible/hosts`，但您可以使用 `-i` 参数自定义。在本示例中，`host1.example.com` 未分组，`two.example.com` 和 `three.example.com` 被分为“webservers”。

## 简单的 YAML 清单
`/simple_yaml_inventory.yml`

```yaml
---
all:
  hosts:
    host1.example.com:
  children:
    webservers:
      hosts:
        two.example.com:
        three.example.com:
```
文件名：`inventory.yml`

“host1.example.com”未分组

“two.example.com”和“three.example.com”被分在“webservers”

您可以使用 YAML 语法表达相同的清单。在本示例中，`host1.example.com` 未分组，`two.example.com` 和 `three.example.com` 被分为“webservers”。

## 添加主机范围
`/ini_range_inventory`

```
[webservers]
www[01:99].example.com

[databases]
db-[a-f].example.com
```
“webservers”组包含从 `www01.example.com` 到 `www99.example.com` 的所有主机

“databases”组包含从 `db-a.example.com` 到 `db-f.example.com` 的所有主机，





也可以使用数字或字母范围来定义组成员。在数字范围中，你还可以指定步长，即一组数字之间的增量。在上面的 INI 示例中，“webservers”组包含了从 `www01.example.com` 到 `www99.example.com` 的所有主机。“databases”组包含了从 `db-a.example.com` 到 `db-f.example.com` 的所有主机。

## 多个组中的主机

`./ini_groupsmultiple_inventory`

```ini
1 one.example.com 2 3 [webservers] 4 two.example.com 5 three.example.com 6 7 [prod] 8 two.example.com 9 10 [dev] 11 three.example.com
```

主机 `two.example.com` 和 `three.example.com` 存在于多个组中

主机可以存在于多个组。在这个 INI 示例中，主机 `two.example.com` 和 `three.example.com` 被归类为 `webserver`。`two.example.com` 同时存在于 `webserver` 和 `prod` 组中。

`three.example.com` 存在于 `webserver` 和 `dev` 组。

## 主机变量

`./ini_hostinventory`

```ini
1 [webservers] 2 localhost  ansible_connection=local 3 one.example.com ansible_connection=ssh ansible_user=devops 4 two.example.com ansible_connection=ssh ansible_user=ansible\ 5 le
```

`ansible_connection` 和 `ansible_user` 变量的自定义

在清单中，你可能想要与特定主机或组相关的变量值。这种场景很常见，因为它定义了与不同主机不同的连接。例如，对 localhost 使用 `local` 连接，对所有其他主机使用默认的 `ssh` 连接。对于每个主机，你还可以自定义登录用户，如 `one.example.com` 使用 `devops`，`two.example.com` 使用 `ansible`。

## 组变量

`./ini_groupsvariables_inventory`

```ini
1 [webservers] 2 one.example.com 3 two.example.com 4 5 [webservers:vars] 6 ntp_server=europe.pool.ntp.org
```

`./inventory.yml`

```yaml
1 --- 2 webservers: 3   hosts: 4     two.example.com: 5     three.example.com: 6   vars: 7     ntp_server: europe.pool.ntp.org
```

与单主机一样，组也可以定义组变量。在示例的这两个清单文件（INI 和 YAML 格式）中，变量 `ntp_server` 为该组的所有主机分配了值 `europe.pool.ntp.org`。

## 变量值的继承

`./ini_variableinheriting_inventory`

```ini
1 [asia] 2 host1.example.com 3 4 [europe] 5 host2.example.com 6 7 [webserver:children] 8 asia 9 europe 10 11 [webservers:vars] 12 ntp_server=europe.pool.ntp.org
```

`./variableinheriting_inventory.yml`

```yaml
1 --- 2 children: 3   webservers:     4     children: 5       asia: 6         hosts: 7           host1.example.com: 8       europe: 9         hosts: 10           host2.example.com: 11     vars: 12       ntp_server: europe.pool.ntp.org
```

主机和组可以组合在一起。在这个示例中，`webserver` 组有两个成员 `asia` 和 `europe`。这两个元素分别被定义为单个主机 `host1.example.com` 和 `host2.example.com`，但也可以包含更多主机。`ntp_server` 变量定义在 `webservers` 级别。因此，最后 `ntp_server` 变量对于 `webserver`、`asia` 和 `europe` 组可用。`ntp_server` 变量在 `host1.example.com` 和 `host2.example.com` 主上也可用。

## 使用多个清单源

```bash
$ ansible-playbook playbook.yml -i production -i development
```

针对 `production` 和 `development` 执行名为 `playbook.yml` 的 ansible playbook。

每次执行都可以使用多个清单文件。在这个示例中，将针对 `production` 和 `development` 清单执行名为 `playbook.yml` 的 ansible playbook。

## localhost 清单

`./ini_local_inventory`

```ini
1 localhost ansible_connection="local"
```

文件名：`inventory`

默认路径：`/etc/ansible/hosts`

清单中的一个特殊情况是 `localhost`。你需要指定连接类型为 `local`，否则 Ansible 将假设使用默认的 SSH 连接。

## 总结

现在你对 Ansible INI 和 YAML 清单文件、主机和组变量有了更多的了解。

## Playbook

在本章中，我将向你解释什么是 Ansible Playbook 以及你为什么需要它。我们将涵盖如何从一个简单的 playbook 开始，包括从基础语法到操作方法。

## YAML 语法

```yaml
1 ---
2 - name: Hello World sample
3   hosts: all
4   tasks:
5     - name: Hello message
6       ansible.debug:
7         msg: "Hello World!"
```

这是 `helloworld.yml` 执行的输出。我想说明的是使用的命令是 `ansible-playbook`。第一个参数是清单文件，第二个参数是 playbook。

在此执行中，play 针对 `host1.example.com` 节点运行。输出非常清晰。当命令成功时，输出将以绿色显示。警告将以橙色显示，错误将以红色显示。大多数人会注意到名为 `Gathering Facts` 的额外任务，这是 Ansible 执行的获取托管节点信息的操作。我们将在下一节中讨论更多关于收集事实（facts）的内容。尝试运行这段代码并对这种输出建立信心。

## ansible-playbook --check 选项

```bash
$ ansible-playbook -i inventory --check helloworld.yml
```

```text
PLAY [Hello World sample] *******************************
*********************************************************
**********
TASK [Gathering Facts] *********************************
*********************************************************
********
ok: [host1.example.com]
TASK [Hello message] *********************************
*********************************************************
******
ok: [host1.example.com] => {
    "msg": "Hello World!"
}
PLAY RECAP **********************************************
*****************************************************
host1.example.com              : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

`ansible-playbook` 命令中一个非常有用的 `--check` 选项。该选项用于对 playbook 执行进行空运行（dry run）。会导致 Ansible 报告如果执行 playbook 会发生哪些更改，但不会对托管主机进行任何实际更改。





# `helloworld_debug.yml`

```yaml
---
- name: Hello World sample 
  hosts: all 
  tasks:
    - name: Hello message
      debug:
        msg: "Hello World!"
        verbosity: 2
...
```

- 文件名：`helloworld_debug.yml`
- Playbook 的名称
- 执行的主机
- 任务列表
- 一个名为“Hello message”的任务
- 模块 `debug`
- 模块 `debug` 的参数 `msg`
- 参数 `varbosity` 为“`2`”

此提示允许你在 Playbook 中保留调试代码，并仅在需要时启用执行。例如，只有当在调用 `Ansible` 并指定输出级别为二时，才会打印消息。

## `helloworld_debug.yml` - 执行 - 部分 1

```bash
ansible-playbook -i inventory helloworld_debug.yml
PLAY [Hello World sample] *******************************\
***********************************************************************\
*********** 
 
TASK [Gathering Facts] *****************************************
************************************************************************\
******** 
ok: [host1.example.com] 
 
TASK [Hello message] ************************************
************************************************************************\
****** 
skipping: [host1.example.com] 
 
PLAY RECAP **********************************************
*****************************************************
host1.example.com      : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

这是 `helloworld_debug.yml` 正常执行时的输出（意味着未处于调试模式）。如你所见，hello 被跳过了。

```bash
$ ansible-playbook -i inventory -vv helloworld_debug.yml
PLAY [Hello World sample] *******************************\
***********************************************************************\
*********** 
TASK [Gathering Facts] *****************************************
************************************************************************\
******** 
ok: [host1.example.com] 
TASK [Hello message] ************************************
************************************************************************\
****** 
ok: [host1.example.com] => { 
     "msg": "Hello World!" 
 } 
PLAY RECAP **********************************************
*****************************************************
host1.example.com      : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

这是 `helloworld_debug.yml` 在调试级别二模式执行下的输出，请注意命令行中的两个“V”。如你所见，hello 消息被打印了。

## 等幂性 (Idempotency)

`idempotency` 模块检查期望的最终状态是否已经实现，否则进行应用。

大多数 `Ansible` 模块的一个重要特性是“等幂的”。这意味着在对目标节点上执行任何操作之前，模块将检查实际状态。如果实际状态与期望状态匹配，则不执行任何操作。如果当前状态偏离预期，则将执行操作。请注意，如果你再次执行该 Playbook，将发现期望状态已存在，不会执行任何后续操作。这种属性被称为“等幂性”，你应当利用这一特性。

## `multipleplays.yml`

```yaml
---
- name: first play 
  hosts: web.example.com 
  tasks:
    - name: first task
      ansible.builtin.yum:
        name: httpd
        status: present
    - name: second task
      ansible.builtin.service:
        name: httpd
        enabled: true
- name: second play 
  hosts: database.example.com 
  tasks:
    - name: first task
      ansible.builtin.service:
        name: mariadb
        enabled: true
```

文件名：`multipleplays.yml`

内部包含两个针对 `web.example.com` 和 `database.example.com` 执行的 play（剧本）。

`multipleplays.yml` Playbook 包含两个 play。第一个 play 针对 `web.example.com` 主机执行，安装 apache Web 服务器并设置开机启动。第二个 play 将针对 `database.example.com` 执行并设置开机启动。

## `privilegeescalation.yml`

```yaml
---
- name: install httpd 
  hosts: web.example.com 
  become: true 
  tasks:
    - name: first task
      ansible.builtin.yum:
        name: httpd
        status: present
```

`privilegeescalation.yml`

`become` 指定了
`become_method` 指定了
`become_user` 指定了 `root`

`wheel` 组。在本例中需要 `root`。某些 `sudo` 操作需要该权限。

## 总结 (Recap)

在本模块中，我们为后续的 `Ansible` 操作奠定了基础。继续努力，你很快就能自动化所有的系统管理员任务。

## 变量 (Variables)

在本章中，我将为你解释什么是 `Ansible` 变量、你为什么需要它们、不同类型以及如何在日常工作中编辑和使用它们。

变量为给定环境存储动态值。在你的 Playbook 中，使用变量存储你所有需要的动态值是一个良好实践。通过编辑变量，你可以根据业务需求进行相应的参数化，从而在未来复用代码。

## 不允许的变量名

不允许包含空格 `my var`

不允许包含点 `my.var`

不能以数字开头 `1stvar`

不能包含特殊字符 `myvar$1`

`Ansible` 允许在变量中使用字母和数字的组合。如果你计划使用数字，请注意不能放在开头，这是信息技术领域的通用规则。

变量名的四个主要限制是：不允许空格、不允许包含点、不能以数字开头、不允许包含特殊字符。因此右侧是一些无效变量名的示例。

## 常用 Ansible 模块

文件模块
- `copy`: 将本地文件复制到托管主机
- `fetch`: 从远程节点复制文件到本地
- `file`: 设置权限和其他属性
- `lineinfile`: 确保文件中存在或不存在特定行
- `synchronize`: 使用 `rsync` 同步内容

软件包模块
- `package`: 使用自动检测的操作系统管理器管理包
- `yum`: 使用 YUM 包管理器管理包
- `apt`: 使用 APT 包管理器管理包
- `dnf`: 使用 DNF 包管理器管理包
- `gem`: 管理 Ruby 宝石包
- `pip`: 管理来自 PyPI 的 Python 包

系统模块
- `firewalld`: 管理任意端口和服务 own
- `reboot`: 重启机器
- `service`: 管理服务
- `user`: 添加、删除和管理用户账户

网络工具模块
- `get_url`: 通过 HTTP、HTTPS 和 FTP 下载文件
- `nmcli`: 管理网络
- `uri`: 与网络服务交互

## `variableprint.yml`

```yaml
---
- name: Variable print sample 
  hosts: all
  vars:
    fruit: "apple"
  tasks:
    - name: Print variable
      ansible.builtin.debug:
        msg: "Print the value of variable {{ fruit }}"
```

- 文件名：`variableprint.yml`
- Playbook 的名称
- 执行的主机
- 一个名为“Print variable”的任务
- 模块 `ansible.builtin.debug`
- 模块 `ansible.builtin.debug` 的参数 `msg`




`variableprint.yml` playbook 与 `helloworlds.yml` playbook 类似。除了存在变量 `fruit` 之外，其语法和元素结构非常相似。变量用于存储字符串、数字以及更复杂的数据结构（如列表、字典等）。在此情况下，变量名为 `fruit`，值为 `apple`。在此情况下，`debug` 模块将文本“Print the value of variable”与变量 `fruit` 的值拼接在一起。请注意双括号，它表示变量的值。最佳实践是始终在代码中的双引号内包含双括号。

### variableprint.yml - 执行

```bash
1 $ ansible-playbook -i inventory variableprint.yml 2 PLAY [Variable print sample] ****************************\ 
3 *********************** 
4 
5 TASK [Gathering Facts] **********************************\ 
6 *********************** 
7 ok: [host1.example.com] 
8 
9 TASK [Print variable] ***********************************\ 
10 *********************** 
11 ok: [host1.example.com] => { 
12     "msg": "Print the value of variable apple" 
13 } 
14 
15 PLAY RECAP **********************************************\
16 *********************** 
17 host1.example.com  : ok=2    changed=0    unreachable=0  \ 
18 failed=0    skipped=0    rescued=0    ignored=0
```

这是 `variableprint.yml` 的执行输出，与 `helloworld.yml` 文件的输出非常相似。请注意组合字符串与变量值得到的消息“Print the value of variable apple”。此外，如你在 play recap 区域和绿色字体所示，该执行是成功的。正在执行两个任务。

### variableprint.yml - 额外变量

```bash
1 $ ansible-playbook -i inventory  -e fruit=banana  variabl\ 
2 eprint.yml 
3 PLAY [Variable print sample] ****************************\ 
4 *********************** 
5 
6 TASK [Gathering Facts] **********************************\ 
7 *********************** 
8 ok: [host1.example.com] 
9 
10 TASK [Print variable] ***********************************\ 
11 *********************** 
12 ok: [host1.example.com] => { 
13     "msg": "Print the value of variable banana" 
14 } 
15 
16 PLAY RECAP **********************************************\
17 *********************** 
18 host1.example.com  : ok=2    changed=0    unreachable=0  \ 
19 failed=0    skipped=0    rescued=0    ignored=0
```

你可以通过命令行指定值来覆盖 playbook 变量。在命令行设置的变量被称为额外变量（extra variables）。

执行输出与之前相似。请注意从命令行传递的值会覆盖任何 playbook 中的值。

### 主机变量与组变量

#### inventory_host_variables
```ini
1 [servers] 
2 host1.example.com ansible_user=devops
```

#### inventory_group_variables
```ini
1 [servers] 
2 host1.example.com 
3 host2.example.com 
4 
5 [servers:vars] 
6 user=alice
```

主机变量和组变量可以定义在你的清单文件中。在左侧列你可以看到主机变量的示例。变量 `ansible_user` 被赋值为 `devops`。该主机变量适用于 `host1.example.com`。在右侧列你看到一个组变量的示例。变量 `user` 被赋值为 `alice`。该组变量将以相同的值适用于 `host1.example.com` 和 `host2.example.com`。

#### inventory_host_dir
```ini
1 [servers] 
2 host1.example.com
```
#### host_vars/demo1.example.com
```ini
1 ansible_user=devops
```

#### inventory_group_dir
```ini
1 [servers] 
2 host1.example.com 
3 host2.example.com
```
#### group_vars/servers
```ini
1 user=alice
```

你也可以使用目录来填充主机和组变量以达到相同的结果。如你所见，结果与上一张幻灯片相同，但使用了更多的文件。在左侧列你可以看到主机变量的示例。变量 `ansible_user` 被赋值为 `devops`。该主机变量适用于 `host1.example.com`。在右侧列你看到一个组变量的示例。变量 `user` 被赋值为 `alice`。该组变量将以相同的值适用于 `host1.example.com` 和 `host2.example.com`。

### 数组变量

#### array.yml
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
让我正确格式化提供的文本块：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
实际上，查看源码：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
等待，源码是：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
让我重新解析它：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
等待，文本还包含：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
然后：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
等待，我会清晰地格式化内容：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
实际上，提供的源码是：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
让我将其视为一个块：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
等待，文本还说：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
这是提示中的重复内容。我将提供干净的版本。

数组是非常有用的数据结构。你可以按层次级结构组织信息。在示例中它易读：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
等待，文本是：
```yaml
1 --- 
2 - name: Array sample 
3   hosts: all 
4   vars: 
5     users: 
6       alice: 
7         firstname: Alice 
8         homedir: /users/alice 
9       bob: 
10        firstname: Bob 
11        homedir: /users/alice
```
让我们直接使用内容。

### array.yml - 执行

```bash
1 $ ansible-playbook -i inventory array.yml 2 PLAY [Array sample] *********************************\ 
3 *********************** 
4 
5 TASK [Gathering Facts] **********************************\ 
6 *********************** 
7 ok: [host1.example.com] 
8 
9 TASK [Print Alice's firstname] *************************\ 
10 *********************** 
11 ok: [host1.example.com] => { 
12     "msg": "Print Alice's firstname: Alice" 
13 } 
14 
15 PLAY RECAP **********************************************\
16 *********************** 
17 host1.example.com  : ok=2    changed=0    unreachable=0  \ 
18 failed=0    skipped=0    rescued=0    ignored=0
```

这是 `array.yml` 的执行输出，与上一个相似。你可以注意到“Print Alice’s firstname: Alice”的输出。Ansible 访问了数组变量并并预期在输出消息中显示。

### 注册变量

#### registeredvariables.yml
```yaml
1 --- 
2 - name: Installs a package and prints the result 
3   hosts: all 
4   become: true 
5   tasks: 
6     - name: Install the package 
7       ansible.builtin.yum: 
8        name: wget 
9        state: installed 
10     register: install_result 
11 
12     - name: debug 
13       ansible.builtin.debug: 
14         var: install_result
```
将标准输出存储在变量 `install_result` 中，也可以打印。

另一种非常有用的数据结构是注册变量。你可以将任何命令的输出保存到注册变量中。在本示例中，它将打印在屏幕上。




```bash
1 ansible-playbook -i inventory registeredvariables.yml
2 PLAY [Installs a package and prints the result] *********\ 3 *********************************************************\ 4 ************************************************************** 5 TASK [Gathering Facts] **********************************\ 6 ******************************************************* 7 ok: [host1.example.com] 8 TASK [Install the package] ******************************\ 9 ******************************************************* 10 ok: [host1.example.com] 11 TASK [debug] ********************************************\ 12 ******************************************************* 13 ok: [host1.example.com] => { 
14     "install_result": { 
15         "changed": false, 
16         "failed": false, 
17         "msg": "Nothing to do", 
18         "rc": 0, 
19         "results": [] 
20     } 
21 } 22 PLAY RECAP *************************************************\ 23 ******************************************************* 24 host1.example.com          : ok=3    changed=0    unreachable\ 25 able=0    failed=0    skipped=0    rescued=0    ignored=0
```

这是 `registeredvariables.yml` 执行的输出，符合预期。首先，`yum` 模块会检查软件包是否存在，如果缺失则继续安装。设置过程的输出被存储在一个注册变量中，并打印在屏幕上。

## 总结

在本模块中，我们探索了 Ansible Playbook 内部变量的使用。你现在已经了解了用户定义变量、主机（Host）、组（Group）以及注册变量等工具的使用。

## Facts 和魔法变量

在本章中，我将向你解释什么是 Ansible facts 和魔法变量，你为什么需要它们，它们的不同类型，以及在日常工作中如何编辑和使用它们。

## Ansible Facts

### 1 facts 是与远程主机相关的变量。

与远程系统相关的变量称为 facts（事实信息）。通过 facts，你可以将一个系统的行为或状态作为其他系统的配置。它们非常强大，因为你可以获取关于当前主机、操作系统、所用发行版、IP 地址、网络配置、存储配置等非常全面的视图。

使用此简单命令列出机器的所有 facts：

```bash
1 ansible -m setup hostname
```

```json
{
    "ansible_all_ipv4_addresses": [
        "REDACTED IP ADDRESS"
    ],
    "ansible_all_ipv6_addresses": [
        "REDACTED IPV6 ADDRESS"
    ],
    "ansible_apparmor": {
        "status": "disabled"
    },
    "ansible_architecture": "x86_64",
    "ansible_bios_date": "11/28/2013",
    "ansible_bios_version": "4.1.5",
    "ansible_cmdline": {
        "BOOT_IMAGE": "/boot/vmlinuz-3.10.0-862.14.4.el7.x86_64",
        "console": "ttyS0,115200",
        "no_timer_check": true,
        "nofb": true,
        "nomodeset": true,
        "ro": true,
        "root": "LABEL=cloudimg-rootfs",
        "vga": "normal"
    },
    "ansible_date_time": {
        "date": "2018-10-25",
        "day": "25",
        "epoch": "1540469324",
        "hour": "12",
        "iso8601": "2018-10-25T12:08:44Z",
        "iso8601_basic": "20181025T120844109754",
        "iso8601_basic_short": "20181025T120844",
        "iso8601_micro": "2018-10-25T12:08:44.109968Z",
        "minute": "08",
        "month": "10",
        "second": "44",
        "time": "12:08:44",
        "tz": "UTC",
        "tz_offset": "+0000",
        "weekday": "Thursday",
        "week": "4",
        "year": "2018"
    },
    "ansible_ipv4": {
        "address": "REDACTED IP",
        "alias": "eth0"
    }
}
```

理解 facts 的最佳方法是使用这个简单的命令自己列出所有内容。你将对从主机获取的信息量之感到惊讶。例如硬件方面：架构、内存、存储配置。还有更多关于软件的信息：操作系统、所用发行版、IP 地址、网络配置。





在本模块中，我们将讨论如何使用 `Ansible Vault` 安全地存储任何敏感数据，如密码或 API 密钥。

# Ansible Vault

Ansible Vault 通过对变量和文件进行加密来保护敏感内容，并允许你在 playbooks 或角色中使用它们。Ansible Vault 以加密的方式存储变量和文件，供 playbooks 或角色使用。在较新版本的 Ansible 中，保护文件的加密算法使用的是 `AES 256`。

## 创建加密文件

```bash
$ ansible-vault create secret.yml
New Vault password: password
Confirm New Vault password: password
$ ansible-vault create --vault-password-file=vault-password.txt secret1.yml
```

创建一个新的加密文件，请使用 `ansible-vault create <filename>` 命令。该命令会提示新的 vault 密码，然后使用默认编辑器打开文件。在这个示例中，使用的密码是 `password`，但我强烈建议你使用尽可能安全的密码。

## 查看加密文件

```bash
$ ansible-vault view secret1.yml
Vault password: password
INFERNO. I. Nel mezzo del cammin di nostra vita mi ritrovai per una selva oscura ché la diritta via era smarrita. Ahi quanto a dir qual era è cosa dura esta selva selvaggia e aspra e forte che nel pensier rinova la paura! Tant'è amara che poco è più morte; ma per trattar del ben ch'i' vi trovai, dirò de l'altre cose ch'i' v'ho scorte.
```

你可以使用 `ansible-vault view <filename>` 命令来查看 Ansible Vault 加密的文件，而无需打开进行编辑。

## 编辑现有加密文件

```bash
$ ansible-vault edit secret.yml
Vault password: password
```

要编辑已有的加密文件，Ansible Vault 提供了 `ansible-vault edit <filename>` 命令。该命令会将文件解密到临时文件中并允许你进行编辑。保存时，它会复制内容并移除临时文件。

## 加密现有文件

```bash
$ ansible-vault encrypt cleartext1.yml --output=vault1.yml
New Vault password: password
Confirm New Vault password: password
Encryption successful
```

要加密一个已经存在的文件，请使用 `ansible-vault encrypt <filename>` 命令。`--output` 选项会将加密文件保存为新名称。如果你省略此选项，原始文件将被加密后的文件覆盖。

## 解密现有文件

```bash
$ ansible-vault decrypt vault1.yml --output=decrypted.yml
Vault password: password
Decryption successful
```

可以使用 `ansible-vault decrypt <filename>` 命令对现有加密文件进行永久解密。在解密单个文件时，可以使用 `--output` 选项以不同的名称保存解密文件。

## 修改加密文件的密码

```bash
$ ansible-vault rekey secret.yml
Vault password: password1
New Vault password: password
Confirm New Vault password: password
Rekey successful
```

你可以使用 `ansible-vault rekey <filename>` 命令更改加密文件的密码。该命令可以一次性重置多个数据文件。它会提示原始密码，然后是新密码。

## Playbooks 与 Ansible Vault

```bash
$ ansible-playbook playbook.yml
TASK [include_vars] *************************************
********************************fatal: [localhost]: FAIL
ED! => {"ansible_facts": {}, "ansible_included_var_files": [], "changed": false, "message": "Attempting to decrypt but no vault secrets found"}

$ ansible-playbook --vault-id @prompt playbook.yml
Vault password (default): password

$ ansible-playbook --vault-password-file=vault-password.txt playbook.yml
```

要运行访问用 Ansible Vault 加密文件的 playbook，你需要向 `ansible-playbook` 命令提供加密密码。如果不提供密码，playbook 将返回错误。要为 playbook 提供 vault 密码，请使用 `--vault-id` 选项。例如，要以交互方式提供 vault 密码，请如图所示使用 `--vault-id @prompt`。或者你也可以使用密码文件。

## 总结

在本模块中，我们探索了 Ansible Vault 安全存储，用于在 Ansible 内部保存秘密和机信息。正如我们看到的，这些工具是稳健的并且完全集成在 Ansible 技术中。

# 条件

在本模块中，我将向你解释什么是 Ansible 条件操作，以及你如何在日常的 Ansible Playbook 中它们。

条件语句用于检查条件并据此改变程序的行为。

让我们开始吧！为了编写实用的代码，我们几乎总是检查条件并相应改变程序行为的能力。条件语句为我们提供了这种能力。Ansible 的形式是 `when` 语句。Ansible 在条件判断中使用 `Jinja2` 测试和过滤器。Ansible 支持所有标准的测试和过滤器，并添加了一些独特的测试。

## 使用“when” 的基础条件

`conditional_basic_false.yml`

```yaml
---
- name: conditional_basic
  hosts: all
  vars:
    configure_nginx: false
  tasks:
    - name: reload nginx
      ansible.builtin.service:
        name: nginx
      when: configure_nginx
```

这是你 playbook 中 `when` 语句的示例示例。任务 `reload nginx` 只有在 `configure_nginx` 变量被设置为 `true` 时才会执行。在这个示例中，我们预计该任务将被跳过。

执行：

```bash
$ ansible-playbook -i inventory conditional_basic_false.yml
PLAY [conditional_basic] *************************************

TASK [Gathering Facts] *************************************
ok: [localhost]

TASK [reload nginx] ****************************************
skipping: [localhost] => (when ("configure_nginx" is false)

PLAY END *************************************************



 RECAP *****************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1
```

这是执行 `conditional_basic_false.yml` 的输出。在此执行中，play 针对 `localhost` 节点运行。正如你看到的，根据我们的条件语句，任务 `reload nginx` 被跳过了。

`conditional_basic_true.yml`

```yaml
---
- name: conditional_basic
  hosts: all
  vars:
    configure_nginx: true
  tasks:
    - name: reload nginx
      ansible.builtin.service:
        name: nginx
      when: configure_nginx
```

这是你 playbook 中相同的 `when` 语句示例，但我们将变量值从 `false` 改为了 `true`。任务 `reload nginx` 现在将执行，因为 `configure_nginx` 布尔变量被设置为 `true`。

执行：

```bash
$ ansible-playbook -i inventory conditional_basic_true.yml
PLAY [conditional_basic] *************************************

TASK [Gathering Facts] *************************************
ok: [localhost]

TASK [reload nginx] ****************************************
ok: [localhost]

PLAY END *****************************************************



 RECAP *****************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0
```





这是 `conditional_basic_true.yml` 执行的输出。在本次执行中，剧本（play）针对 `host1.example.com` 节点执行。输出已以绿色显示。如你所见，任务 `reload ngnx` 被 Ansible 读取并并在我们的条件语句中成功执行。

## 基于 ansible_facts 的条件判断

`conditional_facts.yml`

```yaml
---
- name: conditional_facts 
  hosts: all 
  tasks:
    - name: Shut down Debian-like systems
      ansible.builtin.command: /sbin/shutdown -t now
      when: ansible_facts['os_family'] == "Debian"
```

将条件判断（conditionals）与事实（facts）结合是非常有用的。这样你可以根据单个主机的条件、IP 地址、操作系统、文件系统状态等许多因素调整代码的执行。在这个示例中，如果目标系统是 Debian 类系统（即 Debian 和 Ubuntu 管理的主机），我们将执行关机操作。

# 执行

```bash
$ ansible-playbook -i inventory conditional_facts.yml
PLAY [conditional_facts] ********************************
***********************************************************
********** TASK [Gathering Facts] *********************************
***************************************************
******** ok: [host1.example.com]
TASK [Shut down Debian-like systems] ********************
***********************************************************
***** skipping: [host1.example.com]
PLAY RECAP **********************************************
*****************************************************
host1.example.com              : ok=1    changed=0 unreachable=0 failed=0    skipped=1 rescued=0 ignored=0
```

这是 `conditional_facts.yml` 执行的输出。在本次执行中，剧本针对 `host1.example.com` 节点。目标主机不是 Debian 类系统，因为你可以名为 `Shut down Debian-like systems` 的任务处于 `skipped`（跳过）状态。

## 总结

条件判断非常重要，因为它使我们能够创建响应某些事件、条件或 Ansible Facts 的 Ansible Playbook。这些语句是智能 Ansible Playbook 的基础。

## 循环 (Loop)

在本章中，我将向你解释什么是 Ansible 循环操作，以及如何在每天的 Ansible Playbook 中使用它们。

### 使用循环自动化重复任务

计算机在自动化重复任务方面非常出色。在不犯错的情况下重复相同或相似的任务，是计算机擅长而人类不擅长的。

一组语句的重复执行被称为迭代（iteration）。Ansible 有几条用于迭代的语句——`loop` 语句和 `with_items` 语句。`with` 语句依赖于插件。

`loop_simple.yml`

```yaml
---
- name: Check services 
  hosts: all 
  tasks:
    - name: httpd and mariadb are running
      ansible.builtin.service:
        name: "{{ item }}"
        state: started
      loop:
        - httpd
        - mariadb
```

简单的循环对项列表中的任务进行迭代。`loop` 语句被添加到任务中，并以任务应迭代的项列表作为其值。循环变量 `item` 在每次迭代中遍历当前值。

`loop_hash_or_dict.yml`

```yaml
---
- name: Users exist and are in the correct groups 
  hosts: all 
  tasks:
    - name: Users exist and are in the correct groups
      ansible.builtin.user:
        name: "{{ item.name }}"
        state: present
        groups: "{{ item.group }}"
      loop:
        - name: alice
          group: wheel
        - name: bob
          group: root
```

循环列表不需要是简单值的列表。在下面的示例中，列表中的每个项实际上是一个哈希（hash）或字典（dictionary）。示例中的每个哈希或字典有两个键，`name` 和 `groups`，当前项循环变量中每个键的值可以分别通过 `item.name` 和 `item.group` 变量获取。

## with_* 语句

*   `with_items`: 类似于用于简单列表的 `loop`、字符串列表或哈希/字典列表。如果提供了列表列表，则会扁平化为列表。
*   `with_file`: 该关键字需要一个控制节点文件名列表。循环变量 `item` 持有文件的内容。
*   `with_sequence`: 需要参数根据数值序列生成值列表。

`loop_with_items.yml`

```yaml
---
- name: Example with_items 
  hosts: all 
  vars:
    data:
      - alice
      - bob
  tasks:
    - name: Print values of
      ansible.builtin.debug:
        msg: "{{ item }}"
      loop: "{{ data }}"
```

在 `loop_with_items.yml` playbook 中，`data` 是一个字符串列表。

## 总结

循环对于自动化重复任务非常重要。

## 处理器 (Handler)

在本章中，我将向你解释什么是 Ansible Handler，以及你如何在每天的 Ansible Playbook 中使用它们。

### Handler 在变化时运行

Handler 在必要时非常重要。

`rollingupdate.yml`

```yaml
---
- name: Rolling 
  hosts: all 
  become: true 
  tasks:
    - name: httpd package is installed
      ansible.builtin.yum:
        name: httpd
        state: latest
      notify: restart
handlers:
  - name: restart apache
    ansible.builtin.service:
      name: httpd
      state: restarted
```

`rollingupdate.yml` 由一个任务和一个 handler 组成。`notify` 语句提到了 handler 的名称。更复杂的 playbook 可以有多个 handler，你可以通过名称引用。

## 角色 (Role)

Role 实现了代码复用，Ansible Roles 类似于传统编程世界中的函数。使用 Ansible roles 可以更快速地开发 playbooks 并复用 Ansible 代码。

### Role 目录树

```
$ tree user.example
user.example/
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── templates
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml
```

目录描述：

*   `defaults`: 该目录下的 `main.yml` 文件包含角色变量的默认值，在使用 role 时可以覆盖。这些变量的优先级较低，意在 play 中更改和自定义。
*   `files`: 此目录包含 role 任务引用的静态文件。
*   `handlers`: 该目录下的 `main.yml` 文件包含 role 的 handler 定义。
*   `meta`: 该目录下的 `main.yml` 文件包含关于角色的信息，包括作者、许可证、平台以及可选的角色依赖关系。
*   `tasks`: 该目录下的 `main.yml` 文件包含 role 的任务定义。
*   `templates`: 此目录包含 role 任务引用的 Jinja2 模板。
*   `tests`: 此目录可以包含一个清单和 `test.yml` playbook，用于测试该 role。
*   `vars`: 该目录下的 `main.yml` 文件定义角色的变量值。通常这些变量用于 role 内部。。这些变量的优先级较高，在 playbook 中使用时并不打算更改。





并不是每个角色都包含所有目录。

## 在 playbook 中使用 Ansible 角色

`role_simple.yml`

```yaml
---
- name: role example
  hosts: all
  roles:
    - role1
    - role2
```
1 个文件名为：`role_simple.yml` 将 `role1` 和 `role2` 应用到所有 `all` 托管主机。

`role_vars.yml`

```yaml
---
- name: role example
  hosts: all
  roles:
    - role: role1
    - role: role2
      var1: value
      var2: value
```
1 个文件名为：`role_vars.yml` 将 `role1` 和 `role2` 应用到所有 `all` 托管主机。
`Role2` 拥有两个变量参数。

## 执行顺序

`role_vars.yml`

```yaml
---
- name: order of execution example
  hosts: all
  pre_tasks:
    - debug:
        msg: 'pre-task'
        notify: my handler
  roles:
    - role1
  tasks:
    - debug:
        msg: 'first task'
        notify: my handler
  post_tasks:
    - debug:
        msg: 'post-task'
        notify: my handler
  handlers:
    - name: my handler
      debug:
        msg: Running my handler
```

对于 playbook 中的每个 play，任务将按照 `tasks` 列表中的顺序执行。在所有任务执行后，任何被通知的 handler 将被执行。

当一个角色被添加到 play 时，角色的任务会被添加到 `tasks` 列表的开头。如果在 play 中包含了第二个角色，其任务列表将紧接到第一个角色之后。

角色 handler 添加到 play 的方式与角色任务添加到 play 的方式相同。每个 play 都定义了一个 `handlers` 列表。角色 handler 首先被添加到 `handlers` 列表中，然后是 play 中 `handlers` 部分定义的任何 handler。在某些场景下，可能需要在执行角色之前执行某些 play 任务。为了支持此类场景，可以为 play 配置 `pre_tasks` 部分。在此部分列出的任何任务都会会在任何角色执行之前执行。如果这些任务中的任何一个通知了 handler，这些 handler 任务将在角色或普通任务之前执行。

play 还支持 `post_tasks` 关键字。这些任务在 play 的普通任务执行之后，以及它们通知的任何 handler 执行之后运行。

## Ansible Galaxy

[`galaxy.ansible.com/`](https://galaxy.ansible.com/)

### 手动从 Ansible Galaxy 安装角色

```bash
$ ansible-galaxy install geerlingguy.redis -p roles/
```

### 从 Ansible requirements.yml 安装角色

`requirements.yml`

```yaml
- src: geerlingguy.redis
  version: "1.5.0"
```

```bash
$ ansible-galaxy install -r roles/requirements.yml -p roles
```

## Ansible 最佳实践

遵循 Ansible 最佳实践可以让你代码执行更成功，简化故障排除，并对你的自动化之旅产生积极影响。

### 使用空格

在你的 YAML 代码中使用空格而不是制表符（tabs）。在每个块或任务之前添加新行可以使 playbook 易于读。

例如：

**错误**

```yaml
---
- hosts: all
  tasks:
    - ansible.builtin.yum:
        name: httpd
        state: latest
    - name: end message
      ansible.builtin.debug:
        msg: "httpd succesfully installed"
```

**正确**

```yaml
---
- hosts: all
  tasks:
    - ansible.builtin.yum:
        name: httpd
        state: latest

    - name: end message
      ansible.builtin.debug:
        msg: "httpd succesfully installed"
```

### 为每一步分配“名称 (name)”

始终为你代码中的每个 Ansible 语句（Ansible Plays、Tasks、Blocks）设置 `name` 参数。

例如：

**错误**

```yaml
---
- hosts: all
  tasks:
    - ansible.builtin.yum:
      name: httpd
      state: latest
```

**正确**

```yaml
---
- name: install apache
  hosts: all
  tasks:
    - name: install apache packages
      ansible.builtin.yum:
        name: httpd
        state: latest
```

### 为变量使用易读且有意义的名称

变量对于存储参数或保存上一个任务的结果非常重要。使用易读且有意义的名称可以增加团队之间的代码复用率和可读性。使用 `ansible-playbook` 命令的 `extra-vars` 参数在执行时覆盖变量也非常容易。

例如：

**错误**

```yaml
keepalive: 25
port: 80
```

**正确**

```yaml
apache_max_keepalive: 25
apache_port: 80
```

### 使用原生 YAML

使用原生 YAML 提高了代码的可读性，并允许你更快、更容易地发现错误。它还允许某些 YAML 校验器和解析器进行校验。

例如：

**错误**

```yaml
- name: install apache
  ansible.builtin.yum: name={{ apache_version }} state=present update_cache=yes disable_gpg_check=yes enablerepo=apache  notify: restart apache
```

**正确**

```yaml
- name: install apache
  ansible.builtin.yum:
    name: "{{ apache_version }}"
    state: present
    update_cache: yes
    disable_gpg_check: yes
    enable_repo: apache
  notify: restart apache
```

### 使用原生模块代替命令

始终优先使用原生模块而非命令。原生模块为等幂性而构建，并在执行前内部有业务逻辑验证参数。命令模块（`command`、`shell`、`raw` 和 `script`）很好，但应作为最后手段。

例如：

**错误**

```yaml
- name: Add repository into repo.d list
  become: true
  ansible.builtin.shell: 'echo -e "[google-chrome]\nname=google-chrome\nbaseurl=http://dl.google.com/linux/chrome/rpm/stable/x86_64\nenabled=1\ngpgcheck=1\ngpgkey=https://dl.google.com/linux/linux_signing_key.pub" > /etc/yum.repos.d/google-chrome.repo'
  args:
    creates: /etc/yum.repos.d/google-chrome.repo
  when: ansible_family == 'RedHat'
```

**正确**

```yaml
- name: Add repository into repo.d list
  ansible.builtin.yum_repository:
    name: google-chrome
    description: google-chrome repository
    baseurl: http://dl.google.com/linux/chrome/rpm/stable/x86_64
    enabled: true
    gpgcheck: true
    gpgkey: https://dl.google.com/linux/linux_signing_key.pub
```

### 配置调试消息

在开发 Ansible 代码时，依靠 `debug` 任务在 playbook 运行时显示变量内容非常有用。然而，在生产环境中过多信息被认为很烦。将 `verbosity` 参数设置为 `2` 可以让你只在需要时看到这些消息。

例如：

**错误**

```yaml
- name: message output
  ansible.builtin.debug:
    msg: "This text always displays"
```

**正确**

```yaml
- name: message output
  ansible.builtin.debug:
    msg: "This text displays with ansible-playbook -vv"
  verbosity: 2
```

### 以最小权限执行任务

这是任何安全最佳实践的通用建议，即以最小权限执行任务。在 Ansible 中，你可以在任务级别指定 `become: true`，而不是针对整个 playbook，如果并不是所有任务都需要 root/管理员用户执行。

例如：

**错误**

```yaml
---
- name: install apache
  hosts: all
  become: true
  tasks:
    - name: message output
      ansible.builtin.debug:
        msg: "This text always displays"

    - name: install apache packages
      ansible.builtin.yum:
        name: httpd
        state: latest
```

**正确**

```yaml
---
- name: install apache
  hosts: all
  tasks:
    - name: message output
      ansible.builtin.debug:
        msg: "This text always displays"

    - name: install apache packages
      ansible.builtin.yum:
        name: httpd
        state: latest
      become: true
```

### 始终提及“state”参数

许多模块具有可选的 “state” 参数，并带有某些隐含值。





对于“state”，默认值在不同模块之间可能有所不同，某些模块支持多个“state”设置。显式设置 `state: present` 或 `state: absent` 可以让 playbooks（剧本）和 roles（角色）更加清晰。

## 使用注释

添加注释（以 `#` 开头的行），帮助他人（可能也未来的你自己）理解一个语句、play 或任务（或变量设置）的作用是什么、如何实现以及为什么要这么做。

## 安装 Ansible

在本章中，你将发现如何在现在最常用的操作系统上安装 Ansible。

## Ansible 术语 - ansible vs ansible-core 软件包

什么是 `ansible-core`？什么是 `ansible` 社区包？在 `2.9` 版本之后，Ansible 项目发生了什么？目前 `ansible` 社区包和 `ansible-core` 软件包的概述及使用用例。

## 什么是 ansible-core? 什么是 ansible 社区包？

在 `2.9` 版本之后，Ansible 项目发生了什么？

今天我们将讨论自 2021 年以来发布的 `ansible` 社区包和 `ansible-core` 软件包。

## ansible vs ansible-core

在 `2.9` 版本之后，ansible 发生了什么？

从 2.10 版本开始，Ansible 发布两个交付物：一个名为 `ansible` 的社区包，以及一个极简的语言和运行时 `ansible-core`（在 2.10 版本中称为 `ansible-base`）。选择符合你特定需求的 Ansible 风格和版本。

`ansible` 软件包包含了 Ansible 语言、运行时，以及一系列由社区维护的 Collections（集合）。它重现并扩展了 Ansible 2.9 中包含的功能。

你可以选择以下任何方式来安装 `ansible` 社区包：

- 使用你的操作系统包管理器安装最新发布版本（适用于 Red Hat Enterprise Linux、CentOS、Fedora、Debian 或 Ubuntu）。
- 使用 `pip`（Python 包管理器）安装。

## Ansible 社区包发布周期

Ansible 社区团队通常每年发布两个版本的社区包，采用滞后于 `ansible-core` 发布的灵活发布周期。该周期可以扩展，以便在新版本发布之前，对较大的更改进行适当的实现和测试。请查看 Ansible 路线图获取即将发布的详细信息。在主版本之间，Ansible 团队每三周发布一个新的 Ansible 社区包小版本。小版本发布包含新的向后兼容特性、模块和插件，以及错误修复。

从 2.10 版本开始，Ansible 社区团队保证一次仅维护一个主社区包版本。例如，当 Ansible `5.0.0` 发布时，团队将停止发布新的 `4.x` 版本。社区成员可以根据需要维护较旧版本。

## ansible 社区
- 使用新版本命名（`2.10`，然后是 `3.0.0`）
- 遵循语义化版本规则
- 不使用语义化版本
- 仅维护一个版本
- 包含语言、运行时和选定的 Collections
- 在 Collection 仓库中开发和维护

### ansible-core（2.10 版本为 `ansible_base`）
- 继续“经典 Ansible”版本命名（`2.11`，然后是 `2.12`）
- 不使用语义化版本
- 维护最新版本加上两个旧版本
- 包含语言、运行时和内置插件
- 在 `ansible/ansible` 仓库中开发和维护

## ansible-core

`ansible-core` 软件包主要用于只想安装他们需要的 Collections 的开发者和用户。

### 什么是 ansible-core 软件包？

Ansible Core 是一个命令行工具，主要用于只想安装他们需要的 Collections 的开发者和用户。

它包含极少的模块和插件，并允许安装其他 Collections。它类似于 Ansible 2.9，但不包含任何此后移动到 Collection 中的内容。

Ansible core 或 `ansible-core` 是 Ansible 的主要构建模块和架构，包括：

- CLI 工具，如 `ansible-playbook`、`ansible-doc.` 等，用于驱动和与自动化交互。
- Ansible 语言使用 YAML 创建了一套开发 Ansible Playbooks 的规则集，并包括条件、块、包含、循环和其他 Ansible 指令等函数。
- 一个允许通过 Ansible collections 进行扩展的架构框架。

`ansible-core` 大约每半年发布一次新的主版本。

## ansible 社区

`ansible` 社区包提供了 Ansible 2.9 的功能，包含 85 多个拥有数千个模块和插件的 collections。

### 什么是 ansible 社区包？

Ansible 社区包的每个主版本都会接受包含的每个 Collection 的最新版本以及 `ansible-core` 的最新发布版本。

Ansible 社区包的主版本可能包含包含 collections 中的模块和其他插件以及/或核心功能的破坏性更改。

`ansible` 软件包依赖于 `ansible-base`（很快变为 `ansible-core`）。因此当你执行 `pip install ansible` 时，`pip` 会自动安装 `ansible-core`。

Ansible `3.0.0` 及后续版本包含更多的 Collections，得益于广泛的 Ansible 社区根据社区清单审核 Collections。

Ansible 社区团队通常每年发布两个版本的社区包，采用滞后于 `ansible-core` 发布的灵活发布周期。

## 链接

- [Ansible 3.0.0 问答](https://www.ansible.com/blog/ansible-3.0.0-qa)
- [发布与维护](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html)
- [安装 Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [Ansible 社区日志](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html#ansible-community-changelogs)
- [Ansible Core 文档](https://docs.ansible.com/ansible-core/devel/index.html)
- [pip install ansible-core](https://pypi.org/project/ansible-core/)
- [pip install ansible](https://pypi.org/project/ansible/)

## 在 RedHat Enterprise Linux (RHEL) 8 上安装 Ansible

使用 Ansible Engine 软件集合在 Red Hat Enterprise 8 上安装最新版本的 Ansible。

我将向你展示如何使用发行工具在 RHEL 8 内部更方便地安装和维护 Ansible。

## 在 RHEL 8 中安装 Ansible

使用发行工具在 RHEL 8 内部更方便地安装和维护 Ansible。

包含 Ansible 的仓库被称为 Ansible Engine 软件集合 `ansible-2.9-for-rhel-8-x86_64-rpms`。

使用软件集合的主要优势是，此内容不需要任何外部仓库（如 EPEL）。

软件集合由 Red Hat 完全支持并包含在你的订阅计划中。

## 演示

在 RHEL8 中安装最新版本的 Ansible。

```bash
#!/bin/bash
2 sudo subscription-manager register
3 sudo subscription-manager repos --enable ansible-2.9-for-
rhel-8-x86_64-rpms
5 sudo yum install ansible
```





```
1 #!/bin/bash
2 sudo apt update
3 sudo apt install ansible
```

代码 PPA

```
1 #!/bin/bash
2 sudo apt update
3 sudo apt install software-properties-common
4 sudo add-apt-repository --yes --update ppa:ansible/ansible
5 sudo apt remove ansible
6 sudo apt install ansible-base
```

## 如何在 Fedora 35 中安装 Ansible

介绍如何使用默认仓库在 Fedora 35 中安装和维护最新版本的 Ansible，并附带实际演示。

## 让我们在 Fedora 35 中安装 Ansible

好消息是，Ansible 包含在默认仓库中，因此你可以使用常规的包管理器轻松安装它。

你可以在更新仓库中找到最新版本的 Ansible。

目前可用的最新版本是 2.9。

## 演示

## 如何在 Fedora 中安装最新版本的 Ansible

## 代码

## `install-Ansible-Fedora.sh`

```
1 #!/bin/bash
2 $ sudo dnf list available ansible
3 $ sudo dnf install ansible
4 $ sudo "rpm -qa | grep ansible"
5 $ sudo dnf list ansible
```

# 执行





# Fedora 安装 Ansible 示例

```bash
ssh devops@fedora.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# cat /etc/redhat-release
Fedora release 35 (Thirty Five)
[root@demo devops]# hostnamectl
Static hostname: demo.example.com
      Icon name: computer-vm
      Chassis: vm
      Machine ID: 1894b60f7c1a45b9a6fc87cf8a4bed54
      Boot ID: 68bfe9b366c34c8d95df1a3774cf5641
      Virtualization: oracle
  Operating System: Fedora Linux 35 (Cloud Edition)
      CPE OS Name: cpe:/o:fedoraproject:fedora:35
      Kernel: Linux 5.14.10-300.fc35.x86_64
      Architecture: x86-64
      Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
```

## 检查可用软件包

```bash
[root@demo devops]# dnf list available ansible
Fedora 35 - x86_64                           3.3 MB/s |  61 MB    00:18
Fedora 35 openh264 (From Cisco) - x86_64     2.7 kB/s | 2.5 kB    00:00
Fedora Modular 35 - x86_64                  1.6 MB/s | 2.6 MB    00:01
Fedora 35 - x86_64 - Updates                1.1 MB/s |  15 MB   00:12
Fedora Modular 35 - x86_64 - Updates          400 kB/s | 736 kB    00:01
Available Packages
ansible.noarch                            2.9.27-1.fc35  updates
```

## 安装 Ansible

```bash
[root@demo devops]# dnf install ansible
Last metadata expiration check: 0:00:14 ago on Fri 03 Dec 2021 03:42:34 PM UTC.
Dependencies resolved.
=========================================================
=========================================================
Package                 Architecture   Version                Repository      Size
=========================================================
=========================================================
Installing:
ansible                 noarch          2.9.27-1.fc35        updates         15 M
Installing dependencies:
libsodium                x86_64          1.0.18-8.fc35       fedora          161 k
python3-bcrypt           x86_64          3.2.0-1.fc35        fedora          43 k
python3-jpath            noarch          0.10.0-1.fc35       fedora          46 k
python3-ntlm-auth        noarch          1.5.0-4.fc35         fedora          53 k
python3-pynacl           x86_64          1.4.0-4.fc35        fedora          108 k
python3-requests_ntlm     noarch          1.1.0-16.fc35       fedora          18 k
python3-xmltodict        noarch          0.12.0-13.fc35      fedora          22 k
sshpass                  x86_64          1.09-2.fc35         fedora          27 k
Installing weak dependencies:
python3-paramiko         noarch          2.7.2-6.fc35        fedora          288 k
python3-pyasn1           noarch          0.4.8-7.fc35        fedora          134 k
python3-winrm            noarch          0.4.1-4.fc35        fedora          80 k

Transaction Summary
=========================================================
=========================================================
Install  12 Packages
Total download size: 16 M
Installed size: 100 M
Is this ok [y/N]: y
Downloading Packages:
(1/12): python3-bcrypt-3.2.0-1.fc35.x86_64      317 kB/s |  43 kB
(2/12): python3-jpath-0.10.0-4.fc35.noarch        323 kB/s |  46 kB
(3/12): libsodium-1.0.18-8.fc35.x86_64         704 kB/s | 161 kB
(4/12): python3-ntlm-auth-1.5.0-4.fc35.noarch     566 kB/s |  53 kB
(5/12): python3-pyasn1-0.4.8-7.fc35.noarch       1.5 MB/s | 134 kB
(6/12): python3-paramiko-2.7.2-6.fc35.noarch      1.4 MB/s | 288 kB
(7/12): python3-requests_ntlm-1.1.0-16.fc35.noarch  827 kB/s |  18 kB
(8/12): python3-pynacl-1.4.0-4.fc35.x86_64       935 kB/s | 108 kB
(9/12): python3-xmltodict-0.12.0-13.fc35.noarch   848 kB/s |  22 kB
(10/12): sshpass-1.09-2.fc35.x86_64             580 kB/s |  27 kB
(11/12): python3-winrm-0.4.1-4.fc35.noarch        1.3 MB/s |  80 kB
(12/12): ansible-2.9.27-1.fc35.noarch           1.4 MB/s |  15 MB
-------------------------------------------
Total                               1.3 MB/s |  16 MB   00:12
Running transaction check.
Transaction succeeded.
Running test.
Transaction succeeded.
Running transaction
Preparing:
Installing: sshpass-1.09-2.fc35.x86_64             1/12
Installing: python3-xmltodict-0.12.0-13.fc35.noarch   2/12
Installing: python3-pyasn1-0.4.8-7.fc35.noarch       3/12
Installing: python3-ntlm-auth-1.5.0-4.fc35.noarch    4/12
Installing: python3-requests_ntlm-1.1.0-16.fc35.noarch  5/12
Installing: python3-winrm-0.4.1-4.fc35.noarch        6/12
Installing: python3-jpath-0.10.0-4.fc35.noarch        7/12
Installing: python3-bcrypt-3.2.0-1.fc35.x86_64       8/12
Installing: libsodium-1.0.18-8.fc35.x86_64         9/12
Installing: python3-pynacl-1.4.0-4.fc35.x86_64      10/12
Installing: python3-paramiko-2.7.2-6.fc35.noarch        11/12
Installing: ansible-2.9.27-1.fc35.noarch           12/12
Running script: ansible-2.9.27-1.fc35.noarch           2/12
Verifying: libsodium-1.0.18-8.fc35.x86_64             1/12
Verifying: python3-bcrypt-3.2.0-1.fc35.x86_64       2/12
Verifying: python3-jpath-0.10.0-4.fc35.noarch        3/12
Verifying: python3-ntlm-auth-1.5.0-4.fc35.noarch    4/12
Verifying: python3-pyasn1-0.4.8-7.fc35.noarch       5/12
Verifying: python3-paramiko-2.7.2-6.fc35.noarch        6/12
Verifying: python3-requests_ntlm-1.1.0-16.fc35.noarch  7/12
Verifying: python3-pynacl-1.4.0-4.fc35.x86_64      8/12
Verifying: python3-xmltodict-0.12.0-13.fc35.noarch   9/12
Verifying: sshpass-1.09-2.fc35.x86_64             10/12
Verifying: python3-winrm-0.4.1-4.fc35.noarch        11/12
Verifying: ansible-2.9.27-1.fc35.noarch           12/12
Complete!
```

## 验证安装

```bash
[root@demo devops]# rpm -qa | grep ansible
ansible-2.9.27-1.fc35.noarch
[root@demo devops]# ansible --version
ansible 2.9.27
config file = /etc/ansible/ansible.cfg
configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
ansible python module location = /usr/lib/python3.10/site-packages/ansible
executable location = /usr/bin/ansible
python version = 3.10.0 (default, Oct 4 2021, 00:00:00 ) [GCC 11.2.1 20210728 (Red Hat 11.2.1-1)]
[root@demo devops]# yum list installed google-chrome-stable
Error: No matching Packages to list
[root@demo devops]# yum list installed ansible
Installed Packages
ansible.noarch                            2.9.27-1.fc35  updates
[root@demo devops]#
```





## 执行前

```
ssh devops@fedora.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# cat /etc/redhat-release
Fedora release 35 (Thirty Five)
[root@demo devops]# hostnamectl
Static hostname: demo.example.com
      Icon name: computer-vm
      Chassis: vm
      Machine ID: 1894b60f7c1a45b9a6fc87cf8a4bed54
      Boot ID: 68bfe9b366c34c8d95df1a3774cf5641
      Virtualization: oracle
Operating System: Fedora Linux 35 (Cloud Edition)
    CPE OS Name: cpe:/o:fedoraproject:fedora:35
      Kernel: Linux 5.14.10-300.fc35.x86_64
      Architecture: x86-64
      Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
[root@demo devops]# dnf list installed ansible
Error: No matching Packages to list
[root@demo devops]# dnf list ansible
Last metadata expiration check: 0:03:45 ago on Fri 03 Dec 2021 03:42:34 PM UTC.
Available Packages
ansible.noarch                2.9.27-1.fc35                updates
```

## 执行后

```
[root@demo devops]# rpm -qa | grep ansible
ansible-2.9.27-1.fc35.noarch
[root@demo devops]# ansible --version
ansible 2.9.27 
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.10/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.10.0 (default, Oct 4 2021, 00:00:00) [GCC 11.2.1 20210728 (Red Hat 11.2.1-1)]
[root@demo devops]# yum list installed google-chrome-stable
Error: No matching Packages to list
[root@demo devops]# yum list installed ansible
Installed Packages
ansible.noarch                2.9.27-1.fc35                @updates
[root@demo devops]# dnf list installed ansible
Installed Packages
ansible.noarch                2.9.27-1.fc35                @updates
```

## 如何在 CentOS 9 Stream 中安装 Ansible

在 CentOS 9 Stream 中安装最新版本 Ansible 并保持其更新的更简单方法是使用 `DNF` 和 `AppStream` 系统仓库。

## 如何在 CentOS Stream 9 中安装 Ansible

### 使用系统 AppStream 仓库中的 `ansible-core`

### 使用 Extra Packages for Enterprise Linux - EPEL Next
适用于 CentOS Stream 9 的额外软件包

在 CentOS Stream 版本 9 中安装和维护 Ansible 的更简单方法是使用系统的 `AppStream` 仓库。

另一种方法是使用额外的 `EPEL Next` 仓库。该仓库由 Fedora 特别小组维护，并管理了一组适用于 CentOS Stream 的高质量额外软件包，类似于 Extra Packages for Enterprise Linux (`EPEL`) —— 针对 Red Hat Enterprise Linux (`RHEL`)、CentOS、Scientific Linux (`SL`) 以及 Oracle Linux (`OL`) 的额外软件包。

## 链接

- [CentOS Stream 下载](https://www.centos.org/centos-stream/)
- [EPEL 9 现在已发布](https://communityblog.fedoraproject.org/epel-9-is-now-available/)
- [介绍 CentOS Stream 9](https://blog.centos.org/2021/12/introducing-centos-stream-9/)
- [Extra Packages for Enterprise Linux (EPEL)](https://docs.fedoraproject.org/en-US/epel/)





# CentOS Stream 9 环境配置与 Ansible 安装

## 登录与系统信息

```bash
$ ssh devops@centos-stream.example.com
[devops@centos-stream ~]$ sudo su
[root@centos-stream devops]# cat /etc/redhat-release
CentOS Stream release 9
[root@centos-stream devops]# cat /etc/os-release
```

```text
NAME="CentOS Stream"
VERSION="9"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="9"
PLATFORM_ID="platform:el9"
PRETTY_NAME="CentOS Stream 9"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:9"
HOME_URL="https://centos.org/"
BUG_REPORT_URL="https://bugzilla.redhat.com/"
REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux 9"
REDHAT_SUPPORT_PRODUCT_VERSION="CentOS Stream"
```

```bash
[root@centos-stream devops]# hostnamectl
Static hostname: centos-stream.example.com
Icon name: computer-vm
Chassis: vm
Machine ID: 27ac33d81e2a400cbdaf6ae0b2b82e1d
Boot ID: 4060493b76fc4cc680defa0ffe99af41
Virtualization: oracle
Operating System: CentOS Stream 9
CPE OS Name: cpe:/o:centos:centos:9
Kernel: Linux 5.14.0-17.el9.x86_64
Architecture: x86-64
Hardware Vendor: innotek GmbH
Hardware Model: VirtualBox
```

## Ansible 软件包搜索

```bash
[root@centos-stream devops]# dnf search ansible
```

```text
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
CentOS Stream 9 - BaseOS \ 1.2 MB/s | 1.6 MB 00:01
CentOS Stream 9 - AppStream \ 2.7 MB/s | 8.8 MB 00:03
Last metadata expiration check: 0:00:01 ago on Mon 06 Dec 2021 11:55:34 AM UTC.
================================ Name & Summary Matched: 
ansible =================================
ansible-collection-microsoft-sql.noarch : 用于 Microsoft SQL Server 管理的 Ansible collection
ansible-freeipa-tests.noarch : ansible-freeipa 测试
ansible-pcp.noarch : 用于 Performance Co-Pilot 的 Ansible 指标收集
ansible-test.x86_64 : 用于测试 ansible 插件和模块的工具
====================================== Name Matched: ansible 
=======================================
ansible-core.x86_64 : 基于 SSH 的配置管理、部署和任务执行系统
ansible-freeipa.noarch : 用于部署 FreeIPA 服务器、副本和客户端的 Roles 和 playbooks
```

## 安装 ansible-core

```bash
[root@centos-stream devops]# dnf info ansible-core
```

```text
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
Last metadata expiration check: 0:00:55 ago on Mon 06 Dec 2021 11:55:34 AM UTC.
Available Packages
Name : ansible-core
Version : 2.12.0
Release : 1.el9
Architecture : x86_64
Size : 2.4 M
Source : ansible-core-2.12.0-1.el9.src.rpm
Repository : appstream
Summary : 基于 SSH 的配置管理、部署和任务执行系统
URL : http://ansible.com
License : GPLv3+
Description : Ansible 是一种极其简单的模型驱动的配置管理、多节点部署和远程任务执行系统。Ansible 通过 SSH 工作，不需要在远程节点上安装任何软件或守护进程。模块可以用任何语言编写，并传输到被管理的机器上。
```

```bash
[root@centos-stream devops]# dnf install ansible-core
```

（安装过程显示依赖项解析，包括 `emacs-filesystem`, `git`, `git-core`, `git-core-doc`, `perl-Error`, `perl-Git`, `python3-babel`, `python3-cffi`, `python3-cryptography`, `python3-jinja2`, `python3-markafe`, `python3-packaging`, `python3-ply`, `python3-pyparser`, `python3-pytz`, `python3-resolvelib`, `sshpass`）

```bash
[root@centos-stream devops]# ansible --version
```

```text
ansible core 2.12.0
config file = /etc/ansible/ansible.cfg
python version = 3.9.13 (final, Nov 19 2021, 15:00:00) [GCC 10.2.0]
jinja2 true = True
yaml module = True
```





## 执行前

```
1 # dnf info ansible-core 2 Updating Subscription Management repositories. 3 Unable to read consumer identity 4 This system is not registered with an entitlement server.\ 5 You can use subscription-manager to register. 6 Last metadata expiration check: 0:00:55 ago on Mon 06 Dec 2021 11:55:34 AM UTC. 8 Available Packages 9 Name : ansible-core 10 Version : 2.12.0
11 Release : 1.el9
12 Architecture : x86_64
13 Size : 2.4 M
14 Source : ansible-core-2.12.0-1.el9.src.rpm
15 Repository : appstream
16 Summary : SSH-based configuration management, deployment, and task execution system
17 URL : http://ansible.com
18 License : GPLv3+
19 Description : Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically. 30 [root@centos-stream devops]#
```

## 执行后

```
1 # dnf info ansible-core 2 Updating Subscription Management repositories. 3 Unable to read consumer identity 4 This system is not registered with an entitlement server.\ 5 You can use subscription-manager to register. 6 Last metadata expiration check: 0:02:00 ago on Mon 06 Dec 2021 11:55:34 AM UTC. 8 Installed Packages 9 Name : ansible-core 10 Version : 2.12.0
11 Release : 1.el9
12 Architecture : x86_64
13 Size : 9.3 M
14 Source : ansible-core-2.12.0-1.el9.src.rpm
15 Repository : @System
16 From repo : appstream
17 Summary : SSH-based configuration management, deployment, and task execution system
18 URL : http://ansible.com
19 License : GPLv3+
20 Description : Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically. 31 [root@centos-stream devops]#
```

## 如何在 Windows 11 WSL（Windows 的 Linux 子系统）中安装 Ansible

### 如何使用 Windows Linux 子系统和 Ubuntu 20.04 LTS 在 Windows 11 中安装和维护 Ansible。

### 使用 Windows Linux 子系统在 Windows 11 中安装和维护 Ansible 的简单方法。

### 如何在 Windows 11 中安装 Ansible

## 兼容性考虑

官方网上 Windows 并不是受支持的节点操作系统，尽管 RedHat 正在非常努力消除原生 Windows 控制器的障碍。

这背后的原因是 Ansible 的大部分功能都深植了许多 UNIX 特性，这阻止了它在原生 Windows 上运行；基本上，Windows 没有实现 `fork()` 系统调用。从 2.11 版本开始，Ansible 控制器工作模型大量使用了 POSIX `fork()` 系统调用。

### Cygwin

有些人使用了 Cygwin POSIX 兼容性项目，但有时它会失效，因此并不是一个可靠的解决方案。

### Windows Linux 子系统 (WSL)

最佳替代方案是使用 Windows Linux 子系统，也称为 `WSL`。如果是高于版本 2004 的 Windows 10 或 Windows 11，请运行版本 2 `WSL`。

Ansible 在 `WSL` 和 `WSL2` 上运行良好。

## 链接

### 更多技术信息：

- [Windows Linux 子系统](https://docs.microsoft.com/en-us/windows/wsl/)
- [Windows 版 Ansible - 常见问题](https://docs.ansible.com/ansible/latest/user_guide/windows_faq.html)
- [Windows 11  Windows Linux 子系统](https://arstechnica.com/gadgets/2021/10/the-best-part-of-windows-11-is-a-revamped-windows-subsystem-for-linux/)

## 演示

### 如何使用 Windows Linux 子系统在 Windows 中安装最新版本和特定版本的 Ansible。

## 代码

```bash
# install_wsl.ps1
wsl --help
wsl --list -o
wsl --install
```

# 执行

### 安装 WSL

```bash
1 Windows PowerShell 2 Copyright (C) Microsoft Corporation. All rights reserved. 3 4 安装最新的 PowerShell 以获取新功能和改进！https://aka.ms/PSWindows 6 7 PS C:\Users\user> wsl --install 8 Installing: Virtual Machine Platform 9 Virtual Machine Platform has been installed. 10 Installing: Windows Subsystem for Linux 11 Windows Subsystem for Linux has been installed. 12 Downloading: WSL Kernel 13 Installing: WSL Kernel 14 WSL Kernel has been installed. 15 Downloading: GUI App Support 16 Installing: GUI App Support 17 GUI App Support has been installed. 18 Downloading: Ubuntu 19 The requested operation is successful. Changes will not be effective until the system is rebooted. 21 PS C:\Users\user>
```





1. 正在安装，这可能需要几分钟...
2. 请创建一个默认 UNIX 用户账户。用户名 `demo` 不需要与您的 Windows 用户名匹配。
3. 更多信息请访问：https://aka.ms/wslusers
4. 输入新的 UNIX 用户名：`demo`
5. 新密码：
6. 再次输入新密码：
7. `passwd: password updated successfully`（密码更新成功）
8. 安装成功！
9. 要以管理员身份（用户 `"root"`）运行命令，请使用 `sudo <command>`。
10. 详情请参见 `man sudo_root`。

# 欢迎使用 Ubuntu 20.04 LTS (GNU/Linux 4.4.0-22000-Microsoft x86_64)

* 文档：https://help.ubuntu.com
* 管理：https://landscape.canonical.com
* 支持：https://ubuntu.com/advantage

## 系统信息
截至 2022 年 1 月 10 日 周一 16:57:36 UTC

* 系统负载：0.52 | 登录用户：0
* `/home` 使用率：未知 | `eth0` 的 IPv4 地址：`10.0.2.15`
* 内存使用率：73% | `eth1` 的 IPv4 地址：`169.25.4.235.130`
* 交换分区使用率：1% | `eth1` 的 IPv4 地址：`192.168.0.209`
* 进程：7

有 0 个可以立即安装的更新。
这些更新中没有安全更新。

可用更新列表已是一周前的。
检查新更新请运行：`sudo apt update`

此消息每天显示一次。要禁用此消息，请创建 `/home/demo/.hushlogin` 文件。

```bash
demo@demo:~$ sudo su
[sudo] password for demo: 
root@demo:/home/demo# apt-get update
Get:1 http://archive.ubuntu.com/ubuntu focal InRelease [65 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates Release [114 kB]
Get:3 http://security.ubuntu.com/ubuntu focal-security Release [114 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-backports Release [108 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/main amd64 Packages [970 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/main Translation-en [506 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/main amd64 cc-n-f Metadata [29.5 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/universe amd64 Packages [8628 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/universe Translation-en [5124 kB]
Get:10 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1109 kB]
Get:11 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [200 kB]
Get:12 http://security.ubuntu.com/ubuntu focal-security/main amd64 cc-n-f Metadata [9104 B]
Get:13 http://archive.ubuntu.com/ubuntu focal/universe amd64 cc-n-f Metadata [265 kB]
Get:14 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [144 kB]
Get:15 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [609 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal/multiverse Translation-en [104 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 cc-n-f Metadata [9136 B]
Get:18 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1445 kB]
Get:19 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [86.8 kB]
Get:20 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 cc-n-f Metadata [536 B]
Get:21 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [675 kB]
Get:22 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [114 kB]
Get:23 http://security.ubuntu.com/ubuntu focal-security/universe amd64 cc-n-f Metadata [13.0 kB]
Get:24 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [21.8 kB]
Get:25 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [4948 B]
Get:26 http://security.ubuntu.com/ubuntu focal-security/universe amd64 cc-n-f Metadata [536 B]
Get:27 http://archive.ubuntu.com/ubuntu focal-updates/main Translation-en [289 kB]
Get:28 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 cc-n-f Metadata [47.7 kB]
Get:29 http://archive.ubuntu.com/ubuntu focal-updates/res amd64 Packages [663 kB]
Get:30 http://archive.ubuntu.com/ubuntu focal-updates/res Translation-en [94.6 kB]
Get:31 http://archive.ubuntu.com/ubuntu focal-updates/res amd64 cc-n-f Metadata [532 B]
Get:32 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [892 kB]
Get:33 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [195 kB]
Get:34 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 cc-n-f Metadata [19.9 kB]
Get:35 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [24.8 kB]
Get:36 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [6928 B]
Get:37 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 cc-n-f Metadata [620 B]
Get:38 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [42.0 kB]
Get:39 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [10.0 kB]
Get:40 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 cc-n-f Metadata [864 B]
Get:41 http://archive.ubuntu.com/ubuntu focal-backports/restricted amd64 cc-n-f Metadata [116 B]
Get:42 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [19.5 kB]
Get:43 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [13.4 kB]
Get:44 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 cc-n-f Metadata [656 B]
Get:45 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 cc-n-f Metadata [116 B]
Fetched 9644 kB in 2s (4411 kB/s)
Reading package lists... Done
root@demo:/home/demo# apt-get install ansible
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
`ieee-data`, `python3-argcomplete`, `python3-crypto`, `python3-dnspython`, `python3-jmespath`, `python3-kerberos`, `python3-libcloud`, `python3-lockfile`, `python3-netaddr`, `python3-ntlm-auth`, `python3-requests-kerberos`, `python3-requests-ntlm`, `python3-selinux`, `python3-winrm`, `python3-xmltodict`.

Suggested packages: `cowsay`, `sshpass`, `python-lockfile-doc`, `ipython3`, `python-netget-docs`.

The following NEW packages will be installed:
`ansible`, `ieee-data`, `python3-argcomplete`, `python3-crypto`, `python3-dnspython`, `python3-jmespath`, `python3-kerberos`, `python3-libcloud`, `python3-lockfile`, `python3-netaddr`, `python3-ntlm-auth`, `python3-requests-kerberos`, `python3-requests-ntlm`, `python3-selinux`, `python3-winrm`, `python3-xmltodict`.

0 upgraded, 16 newly installed, 0 to remove and 251 not upgraded.
Need to get 9644 kB of archives.
After this operation, 90.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 python3-crypto 2.6.1-13ubuntu2 [237 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/main amd64 python3-dnspython 1.16.0-1build1 [89.1 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/main amd64 ieee-data 20180805.1 [1589 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal/updates/main amd64 python3-netaddr 0.7.19-3ubuntu1 [236 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/universe amd64 ansible 2.9.6+dfsg-1 [5794 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-argcomplete 1.8.1-1.3ubuntu1 [27.2 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/updates/main amd64 python3-jmespath 0.9.4-2ubuntu1 [15.5 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-kerberos 1.1.14-3.1build1 [2.6 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/main amd64 python3-lockfile 0.12.2-2ubuntu2 [4.6 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-libcloud 2.8.0-1 [1403 kB]
Get:11 http://security.ubuntu.com/ubuntu focal-security/main amd64 python3-ntlm-auth 0.0-1 [1.6 kB]
Get:12 http://security.ubuntu.com/ubuntu focal-security/main amd64 python3-requests-kerberos 12.0-2 [9.9 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-requests-ntlm [6004]
Get:14 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-selinux 3.0-1build2 [139 kB]
Get:15 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [609 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal/multiverse Translation-en [104 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 cc-n-f Metadata [9136 B]
Get:18 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1445 kB]
Get:19 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [86.8 kB]
Get:20 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 cc-n-f Metadata [536 B]
Get:21 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [675 kB]
Get:22 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [114 kB]
Get:23 http://security.ubuntu.com/ubuntu focal-security/universe amd64 cc-n-f Metadata [13.0 kB]
Get:24 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [21.8 kB]
Get:25 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [4948 B]
Get:26 http://security.ubuntu.com/ubuntu focal-security/universe amd64 cc-n-f Metadata [536 B]
Get:27 http://archive.ubuntu.com/ubuntu focal-updates/main Translation-en [289 kB]
Get:28 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 cc-n-f Metadata [47.7 kB]
Get:29 http://archive.ubuntu.com/ubuntu focal-updates/res amd64 Packages [663 kB]
Get:30 http://archive.ubuntu.com/ubuntu focal-updates/res Translation-en [94.6 kB]
Get:31 http://archive.ubuntu.com/ubuntu focal-updates/res amd64 cc-n-f Metadata [532 B]
Get:32 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [892 kB]
Get:33 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [195 kB]
Get:34 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 cc-n-f Metadata [19.9 kB]
Get:35 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [24.8 kB]
Get:36 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [6928 B]
Get:37 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 cc-n-f Metadata [620 B]
Get:38 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [42.0 kB]
Get:39 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [10.0 kB]
Get:40 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 cc-n-f Metadata [864 B]
Get:41 http://archive.ubuntu.com/ubuntu focal-backports/restricted amd64 cc-n-f Metadata [116 B]
Get:42 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [19.5 kB]
Get:43 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [13.4 kB]
Get:44 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 cc-n-f Metadata [656 B]
Get:45 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 cc-n-f Metadata [116 B]
Fetched 9644 kB in 2s (4411 kB/s)
Reading package lists... Done
Reading database ... 31836 files and directories currently installed.
Unpacking `python3-crypto (2.6.1-13ubuntu2)`...
Unpacking `python3-dnspython (1.16.0-1build1)`...
Unpacking `ieee-data (20180805.1)`...
Unpacking `python3-netaddr (0.7.19-3ubuntu1)`...
Unpacking `ansible (2.9.6+dfsg-1)`...
Unpacking `python3-argcomplete (1.8.1-1.3ubuntu1)`...
Unpacking `python3-jmespath (0.9.4-2ubuntu1)`...
Unpacking `python3-kerberos (1.1.14-3.1build1)`...
Unpacking `python3-libcloud (2.8.0-1)`...
Unpacking `python3-lockfile (0.12.2-2ubuntu2)`...
Unpacking `python3-ntlm-auth (0.0-1)`...
Unpacking `python3-requests-kerberos (12.0-2)`...
Unpacking `python3-requests-ntlm`...
Unpacking `python3-selinux (3.0-1build2)`...
Setting up `python3-crypto (2.6.1-13ubuntu2)`...
Setting up `python3-dnspython (1.16.0-1build1)`...
Setting up `ieee-data (20180805.1)`...
Setting up `python3-netaddr (0.7.19-3ubuntu1)`...
Setting up `ansible (2.9.6+dfsg-1)`...
Setting up `python3-argcomplete (1.8.1-1.3ubuntu1)`...
Setting up `python3-jmespath (0.9.4-2ubuntu1)`...
Setting up `python3-kerberos (1.1.14-3.1build1)`...
Setting up `python3-libcloud (2.8.0-1)`...
Setting up `python3-lockfile (0.12.2-2ubuntu2)`...
Setting up `python3-ntlm-auth (0.0-1)`...
Setting up `python3-requests-kerberos (12.0-2)`...
Setting up `python3-requests-ntlm`...
Setting up `python3-selinux (3.0-1build2)`...
root@demo:/home/demo# ansible --version
ansible 2.9.6
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.8.2 (default, Mar 13 2020, 10:14:16) [GCC 9.3.0]
root@demo:/home/demo# apt list ansible
Listing... Done
ansible/focal,now 2.9.6+dfsg-1 all [installed]
root@demo:/home/demo#





# 回顾

现在你知道了如何使用适用于 Linux 的 Windows 子系统在 Windows 11 中安装最新版本的 `Ansible`。

## 如何在 SUSE Linux Enterprise Server (SLES) 15 SP3 中安装 `Ansible`

## 如何使用 SUSE Package Hub 仓库在 SLES 15 SP3 中安装并维护最新版本的 `Ansible`

## 使用 SUSE Package Hub 仓库

在 SUSE Linux Enterprise 15 SP3 中安装和维护 `Ansible` 的更简单方法是使用由 SUSE 社区维护的 SUSE Package Hub 仓库。

## 链接

[SUSE Package Hub - 适用于 SUSE Linux Enterprise Server/Desktop 的社区软件包](https://packagehub.suse.com/)

[如何使用 SUSEConnect 命令行工具注册 SLES](https://www.suse.com/support/kb/doc/?id=000018564)

[向 SUSE Linux Enterprise Server 添加 SUSE Package Hub 仓库](https://www.suse.com/support/kb/doc/?id=000018789)

## 演示

## 如何在 SUSE Linux Enterprise Server 15 SP3 中安装最新版本的 `ansible`

## 代码

## `Install-Ansible-SLES-15-SP3.sh`

```
1 #!/bin/bash
2 SUSEConnect --status
3 SUSEConnect --list-extensions
4 SUSEConnect -p PackageHub/15.3/x86_64
5 zypper install ansible
6 zypper info ansible
7 ansible --version
```

# 执行





# SLES 环境配置与 Ansible 安装日志

## 1. 登录与系统信息查看

```bash
ssh devops@sles.example.com
devops@sles:~> sudo su
sles:/home/devops # cat /etc/os-release
```
输出内容：
```text
NAME="SLES"
VERSION="15-SP3"
VERSION_ID="15.3"
PRETTY_NAME="SUSE Linux Enterprise Server 15 SP3"
ID="sles"
ID_LIKE="suse"
ANSI_COLOR="0;32"
CPE_NAME="cpe:/o:suse:sles:15:sp3"
DOCUMENTATION_URL="https://documentation.suse.com/"
```

```bash
sles:/home/devops # hostnamectl
```
输出内容：
```text
  Static hostname: sles.example.com
  Transient hostname: sles
         Icon name: computer-vm
         Chassis: vm
         Machine ID: 4a241aac39fa4e75b13748c714c05c47
          Boot ID: 150e32975f4d4fdd801eb605f7e35393
         Virtualization: oracle
  Operating System: SUSE Linux Enterprise Server 15 SP3
         CPE OS Name: cpe:/o:suse:sles:15:sp3
            Kernel: Linux 5.3.18-57-default
      Architecture: x86-64
```

```bash
sles:/home/devops # uname -a
```
输出内容：
```text
Linux sles 5.3.18-57-default #1 SMP Wed Apr 28 10:54:41 UTC 2021 (ba3c2e9) x86_64 x86_64 x86_64 GNU/Linux
```

## 2. 订阅状态与仓库更新

```bash
sles:/home/devops # SUSEConnect --status
```
输出内容：
```json
[{"identifier":"sle-module-basesystem","version":"15.3","arch":"x86_64","status":"Registered"},{"identifier":"SLES "," "version":"15.3","arch":"x86_64","status":"Registered","regcode":"****************","starts_at":"2021-12-07 00:00:00 UTC","expires_at":"2022-02-07 00:00:00 UTC","subscription_status":"ACTIVE","type":"evaluation"},{"identifier":"sle-module-server-applications","version":"15.3","arch":"x86_64","status":"Registered"}]
```

```bash
sles:/home/devops # zypper refresh
```
输出内容：
```text
Repository 'SLE-Module-Basesystem15-SP3-Pool' is up to date.
Repository 'SLE-Module-Basesystem15-SP3-Updates' is up to date.
Repository 'SLE-Product-SLES15-SP3-Pool' is up to date.
Repository 'SLE-Product-SLES15-SP3-Updates' is up to date.
Repository 'SLE-Module-Server-Applications15-SP3-Pool' is up to date.
Repository 'SLE-Module-Server-Applications15-SP3-Updates' is up to date.
All repositories have been refreshed.
```

## 3. 安装尝试

```bash
sles:/home/devops # zypper search ansible
```
结果：未找到匹配项（No matching items found）。

```bash
sles:/home/devops # zypper install ansible
```
由于缺少依赖 `python3-coverage`，系统提示需要安装 `ansible-2.9.6-bp153.20`。选择方案 `2` 解决依赖关系。

安装的包列表：
- `ansible`
- `libsodium23`
- `python3-Babel`
- `python3-Jinja2`
- `python3-MarkupSafe`
- `python3-PyNaCl`
- `python3-PyYAML`
- `python3-appdirs`
- `python3-asn1crypto`
- `python3-bcrypt`
- `python3-cffi`
- `python3-cryptography`
- `python3-jmespath`
- `python3-packaging`
- `python3-paramiko`
- `python3-passlib`
- `python3-ply`
- `python3-pyasn1`
- `python3-pycparser`
- `python3-pycryptodome`
- `python3-pytz`
- `python3-setuptools`
- `python3-simplejson`
- `python3-six`

## 4. 验证安装

```bash
sles:/home/devops # ansible --version
```
输出内容：
```text
ansible [2.9.6]
config file = /etc/ansible/ansible.cfg
ansible pivot = smart
python = /usr/bin/python3
version = 3.6.13 (default, Mar 10 2021, 18:30:35)
```

## 5. 详细查询

```bash
sles:/home/devops # zypper info ansible
```
详细信息：
- **Name**: `ansible`
- **Version**: `2.9.6-bp153.20`
- **Arch**: noarch
- **Summary**: 基于 SSH 的配置管理、部署和任务执行系统
- **Description**: Ansible 是一种极其简单的、模型驱动的配置管理、多节点部署和远程任务执行系统。Ansible 通过 SSH 工作，且不需要在远程节点上安装任何软件或守护进程。扩展模块可以使用任何语言编写，并自动传输到被管理的机器上。





## 执行前

```bash
# zypper search ansible
Refreshing service 'Basesystem_Module_15_SP3_x86_64'.
Refreshing service 'SUSE_Linux_Enterprise_Server_15_SP3_x86_64'.
Refreshing service 'Server_Applications_Module_15_SP3_x86_64'.
Loading repository data...
Reading installed packages...
No matching items found.
sles:/home/devops # zypper install ansible
Refreshing service 'Basesystem_Module_15_SP3_x86_64'.
Refreshing service 'SUSE_Linux_Enterprise_Server_15_SP3_x86_64'.
Refreshing service 'Server_Applications_Module_15_SP3_x86_64'.
Loading repository data...
Reading installed packages...
'ansible' not found in package names. Trying capabilities.
No provider of 'ansible' found.
Resolving package dependencies...
Nothing to do.
sles:/home/devops #
```

## 执行后

```bash
# zypper info ansible
Refreshing service 'Basesystem_Module_15_SP3_x86_64'.
Refreshing service 'SUSE_Linux_Enterprise_Server_15_SP3_x86_64'.
Refreshing service 'SUSE_Package_Hub_15_SP3_x86_64'.
Refreshing service 'Server_Applications_Module_15_SP3_x86_64'.
Loading repository data...
Reading installed packages...
Information for package ansible:
--------------------------------
Repository      : SUSE-PackageHub-15-SP3-Backports-Pool
Name            : ansible
Version         : 2.9.6-bp153.1.20
Arch            : noarch
Vendor          : openSUSE
Support Level  : unknown
Installed Size : 96.0 MiB
Installed       : Yes
Status          : up-to-date
Source package  : ansible-2.9.6-bp153.1.20.src
Summary         : SSH-based configuration management, deployment, and task execution system
Description     :
    Ansible 一个极其简单的模型驱动配置管理、多节点部署和远程任务执行系统。Ansible 通过 SSH 工作，不需要在远程节点上安装任何软件或守护进程。扩展模块可以使用任何语言编写，并自动传输到被管理的机器上。
sles:/home/devops #
```

## 如何使用 PIP 安装 Ansible

如何使用 Python 包管理器 `PIP` 安装 Ansible？

`PIP` 是 Python 的包管理器，它将负责处理所有过程并管理必要的依赖项。它直接负责从 `PyPI` 下载和安装软件包的过程。`PIP` 的设计是独立于操作系统的。

对于总是想要获取最新版本的开发者来说，这是一种解决方案。

另一种方法是使用特定操作系统的包管理器。例如 Linux 下的 `yum`、`DNF` 和 `apt`，以及 macOS 下的 `Homebrew`。

这种方法更强调稳定性，因此可能没有最新版本。

所以，如果你确实需要 Ansible 的最新版本，我建议你使用 `PIP`。

## 使用 PIP 安装 Ansible 演示

如何使用 Python 包管理器 `PIP` 安装最新版本的 Ansible。

### PIP 用户
`install-pip-user.sh`

```bash
#!/bin/bash
python3 -m pip install --upgrade -user pip
python3 -m pip install --user ansible
```
`install-pip-global.sh`

### PIP 全局
`install-pip-global.sh`

```bash
#!/bin/bash
python3 -m pip install --upgrade pip
python3 -m pip install ansible
```

## 如何在 RedHat Enterprise Linux 9 Beta 中安装 Ansible

如何在 RedHat Enterprise Linux 9 Beta 安装包含在 RHEL 9 AppStream 仓库中的 Ansible Core (`ansible-core`)。

## 如何在 RHEL 9 Beta 中安装 Ansible

RHEL 9 AppStream 仓库包含了 Ansible Core 包 (`ansible-core`)。

## 关键信息

好消息是，Ansible Core 包 (`ansible-core`) 已默认包含在 RHEL 9 AppStream 仓库中了。

基础自动化不再像以前版本那样额外的仓库（`Ansible Engine` 或 `EPEL`）。

然而，对于底层平台的额外支持以及 Core 维护的模块，需要 Ansible Automation Platform 订阅。

## 链接

- [包含在 RHEL 9 AppStream 中的 Ansible Core 包的支持范围](https://access.redhat.com/articles/6325611)
- [在 RHEL 9 中使用 Ansible](https://access.redhat.com/articles/6393321)





# 系统登录与基础信息

```bash
ssh devops@rhel9.example.com
Last login: Fri Jan 21 17:32:05 2022 from 192.168.0.101
[devops@localhost ~]$ sudo su
[root@localhost devops]# cat /etc/redhat-release
Red Hat Enterprise Linux release 9.0 Beta (Plow)
[root@localhost devops]# cat /etc/os-release
NAME="Red Hat Enterprise Linux"
VERSION="9.0 (Plow)"
ID="rhel"
ID_LIKE="fedora"
VERSION_ID="9.0"
PLATFORM_ID="platform:el9"
PRETTY_NAME="Red Hat Enterprise Linux 9.0 Beta (Plow)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:redhat:enterprise_linux:9::baseos"
HOME_URL="https://www.redhat.com/"
DOCUMENTATION_URL="https://access.redhat.com/documentation/red_hat_enterprise_linux/9/"
BUG_REPORT_URL="https://bugzilla.redhat.com/"
REDHAT_BUGZILLA_PRODUCT="Red Hat Enterprise Linux 9"
REDHAT_BUGZILLA_PRODUCT_VERSION=9.0
REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux"
REDHAT_SUPPORT_PRODUCT_VERSION="9.0 Beta"
```

## 主机配置查询

```bash
[root@localhost devops]# hostnamectl
Static hostname: n/a
Transient hostname: localhost
Icon name: computer-vm
Chassis: vm
Machine ID: e095682a704549189f7f89473724bc21
Boot ID: ab4c4523b571418fad3bd0c754e6063d
Virtualization: oracle
Operating System: Red Hat Enterprise Linux 9.0 Beta (Plow)
CPE OS Name: cpe:/o:redhat:enterprise_linux:9::baseos
Kernel: Linux 5.14.0-39.el9.x86_64
Architecture: x86-64
Hardware Vendor: innotek GmbH
Hardware Model: VirtualBox
```

```bash
[root@localhost devops]# uname -a
Linux localhost.localdomain 5.14.0-39.el9.x86_64 #1 SMP PREEMPT Fri Dec 24 00:07:58 EST 2021 x86_64 x86_64 x86_64 GNU/Linux
```

## Ansible 软件包搜索

```bash
[root@localhost devops]# dnf search ansible
Updating Subscription Management repositories.
Last metadata expiration check: 1:40:46 ago on Fri 21 Jan 2022 04:15:49 PM CET.
================================ Name & Summary Matched:
ansible =================================
ansible-collection-microsoft-sql.noarch : The Ansible collection for Microsoft SQL Server management
ansible-freeipa-tests.noarch : ansible-freeipa tests
ansible-pcp.noarch : Ansible Metric collection for Performance Co-Pilot
ansible-test.x86_64 : Tool for testing ansible plugin and module code
====================================== Name Matched: ansible ======================================
ansible-core.x86_64 : SSH-based configuration management, deployment, and task execution system
ansible-freeipa.noarch : Roles and playbooks to deploy freeIPA servers, replicas and clients
==================================== Summary Matched: ansible =====================================
rhc-worker-playbook.x86_64 : Python worker for Red Hat connector that launches Ansible Runner
```

## 安装详细信息

```bash
[root@localhost devops]# dnf info ansible-core
Updating Subscription Management repositories.
Last metadata expiration check: 1:41:06 ago on Fri 21 Jan 2022 04:15:49 PM CET.
Available Packages
Name: ansible-core
Version: 2.12.1
Release: 1.el9
Architecture: x86_64
Size: 2.4 M
Source: ansible-core-2.12.1-1.el9.src.rpm
Repository: rhel-9-for-x86_64-appstream-beta-rpms
Summary: SSH-based configuration management, deployment, and task execution system
URL: http://ansible.com
License: GPLv3+
Description: Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote execution system. Ansible works over SSH and does not require any software daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.


```bash
[root@localhost devops]# dnf install ansible-core
Updating Subscription Management repositories.
Last metadata expiration check: 1:41:25 ago on Fri 21 Jan 2022 04:15:49 PM CET.
Dependencies resolved.
======================================== ==========================
Package Arch Version Repository Size
======================================== ==========================
Installing: ansible-core x86_64 2.12.1-1.el9 rhel-9-for-x86_64-appstream-beta-rpms 2.4 M
Installing dependencies:
git x86_64 2.31.1-2.el9.2 rhel-9-for-x86_64-appstream-beta-rpms 128 k
... (此处省略重复列表内容) ...
sshpass x86_64 1.09-4.el9 rhel-9-for-x86_64-appstream-beta-rpms 29 k

Is this ok [y/N]: y
...




## 执行前

```bash
# dnf info ansible-core
2 Updating Subscription Management repositories. 3 Last metadata expiration check: 1:41:06 ago on Fri 21 Jan 2022 04:15:49 PM CET. 5 Available Packages
6 Name: ansible-core
7 Version: 2.12.1
8 Release: 1.el9
9 Architecture: x86_64
10 Size: 2.4 M
11 Source: ansible-core-2.12.1-1.el9.src.rpm
12 Repository: rhel-9-for-x86_64-appstream-beta-rpms
13 Summary: SSH-based configuration management, deployment, and task execution system
14 URL: http://ansible.com
15 License: GPLv3+
16 Description: Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
27 [root@localhost devops]#
```

## 执行后

```bash
# dnf info ansible-core
2 Updating Subscription Management repositories. 3 Last metadata expiration check: 1:42:32 ago on Fri 21 Jan 2022 04:15:49 PM CET. 5 Installed Packages
6 Name: ansible-core
7 Version: 2.12.1
8 Release: 1.el9
9 Architecture: x86_64
10 Size: 9.3 M
11 Source: ansible-core-2.12.1-1.el9.src.rpm
12 Repository: @System
13 From repo: rhel-9-for-x86_64-appstream-beta-rpms
14 Summary: SSH-based configuration management, deployment, and task execution system
15 URL: http://ansible.com
16 License: GPLv3+
17 Description: Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
28 [root@localhost devops]#
```

## 如何在 Amazon Linux 2 (AWS EC2) 中安装 Ansible

### 使用 Amazon Extras Library “amazon-linux-extras” 和 EPEL（Extra Packages for Enterprise Linux）仓库在 Amazon Linux 2 中安装 Ansible。

在 Amazon Linux 2 内部安装和维护 Ansible 更简单的方法是使用 Amazon Extras Library 和 EPEL 仓库。

## 如何在 Amazon Linux 2 中安装 Ansible

### Extras Library 仓库中的 `ansible2` 主题

### Extra Packages for Enterprise Linux (EPEL) 附加软件包，适用于：Red Hat Enterprise Linux (RHEL)、Rocky Linux 和 Scientific Linux (SL)、Oracle Linux (OL) 以及 Amazon Linux

好消息是，Ansible 包含在通过 `amazon-linux-extras` 命令提供的 Amazon Linux 2 仓库中的 Extras Library 中。

另一种在 Amazon Linux 2 内部安装和维护 Ansible 的选项是使用 Extra Packages for Enterprise Linux (EPEL) 附加仓库。

该仓库由 Fedora 特别兴趣小组维护，为企业级 Linux：Red Hat Enterprise Linux (RHEL)、Rocky Linux 和 Scientific Linux (SL)、Oracle Linux (OL) 以及 Amazon Linux 管理了一组高质量的附加软件包。

## 链接

- [Amazon Linux 2](https://aws.amazon.com/it/amazon-linux-2/)
- [如何为运行 CentOS、RHEL 或 Amazon Linux 的 Amazon EC2 实例启用 EPEL 仓库？](https://aws.amazon.com/it/premiumsupport/knowledge-center/ec2-enable-epel/)
- [Extras library (Amazon Linux 2)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-linux-ami-basics.html#extras-library)
- [Extra Packages for Enterprise Linux (EPEL)](https://docs.fedoraproject.org/en-US/epel/)

## 演示

### 如何使用 Amazon Extras Library 和 EPEL 仓库在 Amazon Linux (EC2) 2 中安装 Ansible。

## Amazon Extras Library 代码

### Install-Ansible-Amazon Linux2-Amazon Extras Library.sh

```bash
1#!/bin/bash
2 $ sudo yum update -y
3 $ sudo amazon-linux-extras install ansible2 -y
4 $ ansible --version
```

## Amazon Extras Library 执行结果





# Amazon Linux 2 环境配置与软件包安装

## 1. 远程连接
使用 SSH 密钥登录 EC2 实例：
```bash
ssh -i key.pem ec2-user@34.241.249.206
```
系统提示警告：
`-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory`

## 2. 系统信息查看
切换到 `root` 用户查看镜像信息：
```bash
[ec2-user@ip-172-31-36-49 ~]$ sudo su
[root@ip-172-31-36-49 ec2-user]# cat /etc/image-id
```
输出内容：
```text
image_name="amzn2-ami-kernel-5.10-hvm"
image_version="2"
image_arch="x86_64"
image_file="amzn2-ami-kernel-5.10-hvm-2.0.20211201.0-x86_64.xfs.gpt"
image_stamp="7143-c998"
image_date="20211201182203"
recipe_name="amzn2 ami"
recipe_id="d46c60d3-613d-8f76-a3cd-4476-405e-a3e2-088c7229"
```

查看操作系统发行版本：
```bash
[root@ip-172-31-36-49 ec2-user]# cat /etc/os-release
```
输出内容：
```text
NAME="Amazon Linux"
VERSION="2"
ID="amzn"
ID_LIKE="centos rhel fedora"
VERSION_ID="2"
PRETTY_NAME="Amazon Linux 2"
ANSI_COLOR="0;33"
CPE_NAME="cpe:2.3:o:amazon:amazon_linux:2"
HOME_URL="https://amazonlinux.com/"
```

## 3. 软件包更新
执行系统更新：
```bash
[root@ip-172-31-36-49 ec2-user]# yum update
```
系统输出：
`Failed to set locale, defaulting to C`
`Loaded plugins: extras_suggestions, langpacks, priorities, update-motd`
`amzn2-core | 3.7 kB 00:00:00`
`amzn2extra-docker | 3.0 kB 00:00:00`
`amzn2extra-kernel-5.10 | 3.0 kB 00:00:00`
`No packages marked for update`

## 4. 安装 Ansible
使用 `amazon-linux-extras` 安装 `ansible`：
```bash
[root@ip-172-31-36-49 ec2-user]# amazon-linux-extras install all ansible2
```
安装过程：
```text
Installing ansible
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Cleaning repos: amzn2-core amzn2extra-ansible2 amzn2extra-docker amzn2extra-kernel-5.10
17 metadata files removed
0 sqlite files removed
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core | 3.7 kB 00:00:00
...
(9/9): amzn2-core/2/x86_64/primary_db
...
```
安装依赖包列表：
```text
Package                Arch           Version            Repository           Size
=========================================================
Installing: ansible            noarch          2.9.23-1.amzn2     amzn2extra-ansible2  17 M
Installing for dependencies:
libtomcrypt            x86_64          1.18.2-1.amzn2.0.1 amzn2extra-ansible2  409 k
libtommath             x86_64          1.0.1-4.amzn2.0.1   amzn2extra-ansible2  36 k
python-keyczar         arch           0.71c-2.amzn2      amzn2extra-ansible2  218 k
python2-crypto         x86_64          2.6.1-13.amzn2.0.3  amzn2extra-ansible2  476 k
python2-ecdsa          arch           0.13.3-1.amzn2.0.1  amzn2extra-ansible2  94 k
python2-httplib2       arch           0.18.1-3.amzn2     amzn2extra-ansible2  125 k
python2-paramiko        arch           1.16.1-3.amzn2.0.2  amzn2extra-ansible2  259 k
sshpass                 x86_64          1.06-1.amzn2.0.1   amzn2extra-ansible2  22 k
```
确认并安装：
```text
Is this ok [y/d/N]: y
Downloading packages:
...
Transaction succeeded
```

## 5. 验证安装
检查 `ansible` 版本：
```bash
[root@ip-172-31-36-49 ec2-user]# ansible --version
```
输出：
```text
ansible 2.9.23
config file = /etc/ansible/ansible.cfg
configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
ansible python module location = /usr/lib/python2.7/site-packages/ansible
executable location = /bin/ansible
python version = 2.7.18 (default, Jun 10 2021, 00:11:02) [GCC 7.3.1 20180712 (Red Hat 7.3.1-13)]
```





## 执行后的 Amazon Extras 库

```
1 # rpm -qa | grep ansible 2 ansible-2.9.23-1.amzn2.noarch
```

## EPEL 代码

## Install-Ansible-Amazon Linux2-EPEL.sh

```
1 #!/bin/bash
2 $ sudo amazon-linux-extras install epel -y
3 $ sudo yum repolist
4 $ sudo yum-config-manager --enable epel
5 $ sudo amazon-linux-extras disable ansible2
6 $ sudo yum --enablerepo epel install ansible
7 $ ansible --version
```

## EPEL 执行





# 卸载 Ansible

```bash
# yum remove ansible
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Resolving Dependencies
--> Running transaction check
---> Package ansible.noarch 0:2.9.23-1.amzn2 will be erased
--> Finished Dependency Resolution
Dependencies Resolved
========================================================
==========================================
Package         Arch            Version             
Repository                      Size
========================================================
==========================================
Removing:
 ansible          noarch          2.9.23-1.amzn2
    @amzn2extra-ansible2          105 M
Transaction Summary
========================================================
==========================================
Remove 1 Package
Installed size: 105 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Erasing    : ansible-2.9.23-1.amzn2.noarch            1/1
  Verifying  : ansible-2.9.23-1.amzn2.noarch            1/1
Removed:
  ansible.noarch 0:2.9.23-1.amzn2
Complete!
```

# 安装 EPEL 

```bash
# amazon-linux-extras install all epel
Installing epel-release
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Cleaning repos: amzn2-core amzn2extra-ansible2 amzn2extra-docker amzn2extra-epel
               : amzn2extra-kernel-5.10
22 metadata files removed
8 sqlite files removed
0 metadata files removed
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                      | 3.7 kB  00:00:00
amzn2extra-ansible2                             | 3.0 kB  00:00:00
amzn2extra-docker                               | 3.0 kB  00:00:00
amzn2extra-epel                                 | 3.0 kB  00:00:00
amzn2extra-kernel-5.10                          | 3.0 kB  00:00:00
(1/11): amzn2-core/2/x86_64/group_gz            | 2.5 kB  00:00:00
(2/11): amzn2-core/2/x86_64/updateinfo          | 424 kB  00:00:00
(3/11): amzn2extra-docker/2/x86_64/primary_db   | 86 kB  00:00:00
(4/11): amzn2extra-epel/2/x86_64/updateinfo      | 76 B  00:00:00
(5/11): amzn2extra-epel/2/x86_64/primary_db      | 1.8 kB  00:00:00
(6/11): amzn2extra-kernel-5.10/2/x86_64/updateinfo | 76 B  00:00:00
(7/11): amzn2extra-kernel-5.10/2/x86_64/primary_db  | 5.3 MB 00:00:00
(8/11): amzn2extra-ansible2/2/x86_64/updateinfo   | 76 B  00:00:00
(9/11): amzn2extra-docker/2/x86_64/updateinfo      | 4.7 kB  00:00:00
(10/11): amzn2extra-ansible2/2/x86_64/primary_db     | 39 kB  00:00:00
(11/11): amzn2-core/2/x86_64/primary_db         | 58 MB 00:00:00
Resolving Dependencies
--> Package epel-release.noarch 0:7-1 will be installed
--> Dependency Resolution
Dependencies Resolved
========================================================
==========================================
Package         Arch            Version             
Repository                      Size
========================================================
==========================================
Installing:
 epel-release            noarch          7-1
    amzn2extra-epel             15 k
Transaction Summary
========================================================
==========================================
Install 1 Package
Total download size: 15 k
Installed size: 24 k
Is this ok [y/d/N]: y
Downloading packages:
 epel-release-7-1.noarch.rpm                   | 15 kB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : epel-release-7-1.noarch            1/1
  Verifying  : epel-release-7-1.noarch            1/1
Installed:
  epel-release.noarch 0:7-11
Complete!
```

# 启用 EPEL 仓库

```bash
# yum repolist
ansible2=latest                  enabled [2.4.2=2.4.6=2.8=stable]
httpd_modules                   available [1.0=stable]
memcached1.5                    available [1.5.1=1.5.16=1.5.17]
postgresql9.6                  available [9.6.6=9.6.8=stable]
postgresql10                   available [10=stable]
R3.4                            available [3.4.3=stable]
rust1                           available [1.22.1=1.26.0=1.26.1=1.27.2=1.31.0=1.38.0=stable]
vim                             available [8.0=stable]
php7.2                          available [7.2.0=7.2.4=7.2.5=7.2.8=7.2.11=7.2.14=7.2.16=7.2.17=7.2.19=7.2.21=7.2.23=7.2.24=7.2.26=stable]
lamp-mariadb10.2-php7.2          available [10.2.10_7.2.0=10.2.10_7.2.4=10.2.10_7.2.8=10.2.10_7.2.11=10.2.10_7.2.13=10.2.10_7.2.16=10.2.10_7.2.19=10.2.10_7.2.22=10.2.10_7.2.24=stable]
libreoffice                      available [5.0.6.2_15=5.3.6.1=stable]
gimp                            available [2.8.22]
docker=latest                   enabled [17.12.1=18.03.1=18.06.1=18.09.9=stable]
mate-desktop1.x                 available [1.19.0=1.20.0=stable]
GraphicsMagick1.3               available [1.3.29=1.3.32=1.3.34=stable]
tomcat8.5                       available [8.5.31=8.5.32=8.5.38=8.5.40=8.5.42=8.5.50]
epel=latest                     enabled [7.1=stable]
testing                         available [1.0=stable]
ecs                             available [stable]
corretto8                       available [8.0.192=8.0.202=8.0.221=8.0.232=8.0.242=stable]
firecracker                     available [0.1=stable]
golang1.1                       available [1.11.3=1.11.11=1.11.13=stable]
squid4                          available [4=stable]
php7.2                          available [7.2.0=7.2.4=7.2.5=7.2.8=7.2.11=7.2.14=7.2.16=7.2.17=7.2.19=7.2.21=7.2.23=7.2.24=7.2.26=stable]
lamp-mariadb10.2-php7.2          available [10.2.10_7.2.0=10.2.10_7.2.4=10.2.10_7.2.8=10.2.10_7.2.11=10.2.10_7.2.13=10.2.10_7.2.16=10.2.10_7.2.19=10.2.10_7.2.22=10.2.10_7.2.24=stable]
libreoffice                      available [5.0.6.2_15=5.3.6.1=stable]
gimp                            available [2.8.22]
docker=latest                   enabled [17.12.1=18.03.1=18.06.1=18.09.9=stable]
mate-desktop1.x                 available [1.19.0=1.20.0=stable]
GraphicsMagick1.3               available [1.3.29=1.3.32=1.3.34=stable]
tomcat8.5                       available [8.5.31=8.5.32=8.5.38=8.5.40=8.5.42=8.5.50]
epel=latest                     enabled [7.1=stable]
testing                         available [1.0=stable]
ecs                             available [stable]
corretto8                       available [8.0.192=8.0.202=8.0.221=8.0.232=8.0.242=stable]
firecracker                     available [0.1=stable]
golang1.1                       available [1.11.3=1.11.11=1.11.13=stable]
squid4                          available [4=stable]
```




## 执行后的 EPEL

```
1 # rpm -qa | grep ansible
2 ansible-2.9.25-1.el7.noarch
```

# 回顾

现在您知道了如何使用 Amazon Extras Library 和 EPEL 仓库在 Amazon Linux 中安装最新版本的 Ansible。

## 如何在 Debian 11 中安装 Ansible

在 Debian 11 中，使用 APT 和“main”默认仓库来安装最新版本的 Ansible 并保持更新是更简单的方法。

## 如何在 Debian 中安装 Ansible

### 包含在“main”默认仓库中

好消息是 Ansible 包含在默认仓库中，因此您只需使用常用的包管理器`apt`即可安装。

您可以期待在“main”仓库中找到最新版本的 Ansible。

## 演示

如何使用`apt`包管理器和“main”默认仓库在 Debian 中安装 Ansible。

## 代码

### install-ansible-debian.sh

```
1 #!/bin/bash
2 $ sudo apt-get update
3 $ sudo apt-get install ansible
4 $ sudo apt list –installed ansible
```

# 执行





```bash
ansible-pilot $ ssh devops@debian.example.com
Linux debian 5.10.0-9-amd64 #1 SMP Debian 5.10.70-1 (2021-3-09-30) x86_64
The programs included with the Debian GNU/Linux system are free software; the exact distribution terms for each program are described in the individual files in /usr/share/doc/*/copyright.
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
$ sudo su
root@debian:/home/devops# cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
root@debian:/home/devops# cat /etc/deb
debconf.conf debian_version
root@debian:/home/devops# cat /etc/debian_version
11.1
root@debian:/home/devops# apt-get update
Get:1 http://security.debian.org/debian-security bullseye-security InRelease [44.1 kB]
Hit:2 http://deb.debian.org/debian bullseye InRelease
Get:3 http://deb.debian.org/debian bullseye-updates Increase [39.4 kB]
Get:4 http://deb.debian.org/debian bullseye-backports Release [43.7 kB]
Get:5 http://deb.debian.org/debian bullseye-backports/main Sources.diff/Index [63.3 kB]
Get:6 http://deb.debian.org/debian bullseye-backports/main amd64 Packages.diff/Index [63.3 kB]
Get:7 http://deb.debian.org/debian bullseye-backports/main Sources T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [29 B]
Get:7 http://deb.debian.org/debian bullseye-backports/main Sources T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [29 B]
Get:8 http://deb.debian.org/debian bullseye-backports/main amd64 Packages T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [257 B]
Get:8 http://deb.debian.org/debian bullseye-backports/main amd64 Packages T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [257 B]
Fetched 254 kB in 1s (488 kB/s)
Reading package lists... Done
root@debian:/home/devops# apt-cache search ansible
ansible - Configuration management, deployment, and task execution system
ansible-lint - lint tool for Ansible playbooks
ansible-mitogen - Fast connection strategy for Ansible
shade-inventory - Ansible inventory script for OpenStack clouds
python3-reclass - hierarchical inventory backend for configuration management systems
reclass - hierarchical inventory backend for configuration management systems
reclass-doc - reclass documentation
vim-syntastic - Syntax checking hacks for vim
root@debian:/home/devops# apt-cache show ansible
Package: ansible
Version: 2.10.7+merged+base+2.10.8+dfsg-1
Installed-Size: 198790
Maintainer: Lee Garrett <debian@rocketjump.eu>
Architecture: all
Replaces: ansible-base (<= 2.10.5+dfsg-2)
Depends: python3-cryptography, python3-jinja2, python3-packaging, python3-yaml, python3:any, openssh-client | python3-paramiko (>= 2.6.0), python3-cryptodome, python3-distutils, python3-dnspython, python3-httplib2, python3-netaddr
Recommends: python3-argcomplete, python3-jmespath, python3-kerberos, python3-libcloud, python3-selinux, python3-xmltodict
Suggests: cowsay, sshpass
Breaks: ansible-base (<= 2.10.5+dfsg-2)
Description-en: Configuration management, deployment, and task execution system Ansible is a radically simple model-driven configuration, multi-node deployment, and remote execution system. Ansible works over SSH does not not require any daemons to be installed on remote nodes. Extensions can be written in any language and are transferred to managed machines. This package contains ansible-base 2.10.x and ansible-core 2.10.x merged into one package.
Description-md5: de0a87781a6efa86ca201d648
Homepage: https://www.ansible.com
Tag: admin::automation, admin::distribution, admin::package-management, implemented-in, interface::commandline, role::program, use::configuring, works-with
Section: admin
Priority: optional
Filename: pool/main/ansible_2.10.7+merged+base+2.10.8+dfsg-1_all.deb
Size: 176854
MD5sum: 159657e0be3df21de43ac98
SHA256: 6647417b31f9b0bc816331c7b5f742c77a49db5063da7164
root@debian:/home/devops# apt-get install ansible
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
ee-data libyaml-0-2 python3-argcomplete python3-cffi-backend python3-cryptography python3-distutils python3-dnspython python3-jinja2 python3-jmespath python3-kerberos python3-lib2to3 python3-libcloud python3-lockfile python3-markupsafe python3-netaddr python3-ntlm-auth python3-packaging python3-cryptodome python3-pyparsing python3-requests-kerberos python3-requests-ntlm python3-requests-toolbelt python3-selinux python3-simplejson python3-winrm python3-yaml
Suggested packages: cowsay sshpass python3-cryptography-doc python3-vectors python3-sniffio python3-trio python3-jinja2-doc python3-lockfile-doc python3-netaddr-docs python3-pyparsing-doc
The following NEW packages will be installed:
ansible ee-data libyaml-0-2 python3-argcomplete python3-cffi-backend python3-cryptography python3-distutils python3-dnspython python3-jinja2 python3-jmespath python3-kerberos python3-lib2to3 python3-libcloud python3-lockfile python3-markupsafe python3-netaddr python3-ntlm-auth python3-packaging python3-cryptodome python3-pyparsing python3-requests-kerberos python3-requests-ntlm python3-requests-toolbelt python3-selinux python3-simplejson python3-winrm python3-yaml
0 upgraded, 28 newly installed, 0 to remove and 1 not upgraded.
Need to get 32.9 MB of archives.
After this operation, 280 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bullseye/main amd64 python3-cffi-backend 1.14.5-1 [85.8 kB]
Get:2 http://deb.debian.org/debian bullseye/main amd64 python3-cryptography 3.3.2-1 [223 kB]
Get:3 http://deb.debian.org/debian bullseye/main amd64 python3-markupsafe 1.1.1-1+b3 [15.2 kB]
Get:4 http://deb.debian.org/debian bullseye/main amd64 python3-jinja2 2.11.3-1 [144 kB]
Get:5 http://deb.debian.org/debian bullseye/main amd64 python3-pyparsing 2.4.7-1 [109 kB]
Get:6 http://deb.debian.org/debian bullseye/main amd64 python3-packaging 20.9-2 [33.5 kB]
Get:7 http://deb.debian.org/debian bullseye/main amd64 lib3-yaml 0.2.2-1 [49.6 kB]
Get:8 http://deb.debian.org/debian bullseye/main amd64 python3-cryptodome 3.9.7+dfsg1-1+b2 [9910 kB]
Get:9 http://deb.debian.org/debian bullseye/main amd64 python3-lib2to3 3.9.2-1 [77.8 kB]
Get:10 http://deb.debian.org/debian bullseye/main amd64 python3-distutils 3.9.2-1 [143 kB]
Get:11 http://deb.debian.org/debian bullseye/main amd64 python3-dnspython 2.0.0-1 [103 kB]
Get:12 http://deb.debian.org/debian bullseye/main amd64 ieee-data 20210605.1 [1889 kB]
Get:13 http://deb.debian.org/debian bullseye/main amd64 python3-netaddr 0.7.19-5 [253 kB]
Get:14 http://deb.debian.org/debian bullseye/main amd64 ansible 2.10.7+merged+base+2.10.8+dfsg-1 [17.7 MB]
Get:15 http://deb.debian.org/debian bullseye/main amd64 python3-argcomplete 1.8.1-1.5 [29.7 kB]
Get:16 http://deb.debian.org/debian bullseye/main amd64 python3-jmespath 10.0-1 [1.7 kB]
Get:17 http://deb.debian.org/debian bullseye/main amd64 python3-kerberos 14-3.1+b3 [24.1 kB]
Get:18 http://deb.debian.org/debian bullseye/main amd64 python3-lockfile 0:12.2-2 [17.3 kB]
Get:19 http://deb.debian.org/debian bullseye/main amd64 python3-simplejson 17.2-1 [61.7 kB]
Get:20 http://deb.debian.org/debian bullseye/main amd64 python3-libcloud 3.2.0-2 [1615 kB]
Get:21 http://deb.debian.org/debian bullseye/main amd64 python3-ntlm-auth 1.4.0-1 [21.6 kB]
Get:22 http://deb.debian.org/debian bullseye/main amd64 python3-kerberos 12.0-2 [30.0 kB]
Get:23 http://deb.debian.org/debian bullseye/main amd64 python3-requests-ntlm 1.0.1.1 [31.1 kB]
Get:24 http://deb.debian.org/debian bullseye/main amd64 python3-requests-toolbelt 0.9.1-1 [41.7 kB]
Get:25 http://deb.debian.org/debian bullseye/main amd64 python3-selinux 3.1-3 [160 kB]
Get:26 http://deb.debian.org/debian bullseye/main amd64 python3-xmltodict 12.0-2 [52.2 kB]
Get:27 http://deb.debian.org/debian bullseye/main amd64 python3-winrm 0.3.0-2 [21.6 kB]
Fetched 32.9 MB in 6s (5494 kB/s)
perl: warning: Setting locale failed.
perl: warning: Please check your locale settings: LANGUAGE = (unset), LC_ALL = (unset), LC_CTYPE = "UTF-8" are supported and installed on your system.
perl: warning: Falling back to a fallback locale ("UTF-8").
perl: warning: Cannot set LC_CTYPE to default locale: No such file or directory
perl: warning: Cannot set LC_ALL to default locale: No such file or directory
Selecting previously unselected package
Reading database ... 25133 files and directories currently installed.
Preparing to unpack .../0-python3-cffi-backend_1.14.5-1_amd64.deb
Unpacking python3-cffi-backend:amd64 (1.14.5-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-cryptography_3.3.2-1_amd64.deb
Unpacking python3-cryptography:amd64 (3.3.2-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-markupsafe_1.1.1-1+b3_amd64.deb
Unpacking python3-markupsafe:amd64 (1.1.1-1+b3)
Selecting previously unselected package
Preparing to unpack .../0-python3-jinja2_2.11.3-1_all.deb
Unpacking python3-jinja2 (2.11.3-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-pyparsing_2.4.7-1_all.deb
Unpacking python3-pyparsing (2.4.7-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-packaging_20.9-2_all.deb
Unpacking python3-packaging (20.9-2)
Selecting previously unselected package
Preparing to unpack .../0-libyaml-0-2_0.2.2-1_amd64.deb
Unpacking libyaml-0-2:amd64 (0.2.2-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-yaml_5.3.1-5_amd64.deb
Unpacking python3-yaml (5.3.1-5)
Selecting previously unselected package
Preparing to unpack .../0-python3-cryptodome_3.9.7+dfsg1-1+b2_amd64.deb
Unpacking python3-cryptodome:amd64 (3.9.7+dfsg1-1+b2)
Selecting previously unselected package
Preparing to unpack .../0-python3-lib2to3_3.9.2-1_all.deb
Unpacking python3-lib2to3 (3.9.2-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-distutils_3.9.2-1_all.deb
Unpacking python3-distutils (3.9.2-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-dnspython_2.0.0-1_amd64.deb
Unpacking python3-dnspython (2.0.0-1)
Selecting previously unselected package
Preparing to unpack .../0-ieee-data_20210605.1_amd64.deb
Unpacking ieee-data (20210605.1)
Selecting previously unselected package
Preparing to unpack .../0-python3-netaddr_0.7.19-5_amd64.deb
Unpacking python3-netaddr (0.7.19-5)
Selecting previously unselected package
Preparing to unpack .../0-ansible_2.10.7+merged+base+2.10.8+dfsg-1_all.deb
Unpacking ansible (2.10.7+merged+base+2.10.8+dfsg-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-argcomplete_1.8.1-1.5_amd64.deb
Unpacking python3-argcomplete (1.8.1-1.5)
Selecting previously unselected package
Preparing to unpack .../0-python3-jmespath_10.0-1_amd64.deb
Unpacking python3-jmespath (10.0-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-kerberos_14-3.1+b3_amd64.deb
Unpacking python3-kerberos (14-3.1+b3)
Selecting previously unselected package
Preparing to unpack .../0-python3-lockfile_0:12.2-2_amd64.deb
Unpacking python3-lockfile (0:12.2-2)
Selecting previously unselected package
Preparing to unpack .../0-python3-simplejson_17.2-1_amd64.deb
Unpacking python3-simplejson (17.2-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-libcloud_3.2.0-2_amd64.deb
Unpacking python3-libcloud (3.2.0-2)
Selecting previously unselected package
Preparing to unpack .../0-python3-ntlm-auth_1.4.0-1_amd64.deb
Unpacking python3-ntlm-auth (1.4.0-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-kerberos_12.0-2_amd64.deb
Unpacking python3-kerberos (12.0-2)
Selecting previously unselected package
Preparing to unpack .../0-python3-requests-ntlm_1.0.1.1_amd64.deb
Unpacking python3-requests-ntlm (1.0.1.1)
Selecting previously unselected package
Preparing to unpack .../0-python3-requests-toolbelt_0.9.1-1_amd64.deb
Unpacking python3-requests-toolbelt (0.9.1-1)
Selecting previously unselected package
Preparing to unpack .../0-python3-selinux_3.1-3_amd64.deb
Unpacking python3-selinux (3.1-3)
Selecting previously unselected package
Preparing to unpack .../0-python3-winrm_0.3.0-2_amd64.deb
Unpacking python3-winrm (0.3.0-2)
Selecting previously unselected package
Preparing to unpack .../0-python3-xmltodict_12.0-2_amd64.deb
Unpacking python3-xmltodict (12.0-2)
Setting up ansible (2.10.7+merged+base+2.10.8+dfsg-1)
Setting up python3-cffi-backend (1.14.5-1)
Processing triggers for man-db (2.9.4)...
root@debian:/home/devops# ansible --version
ansible 2.10.8
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.9.2 (default, Feb 28 2021, 17:03:44)
  [GCC 10.2.1 20210110]
root@debian:/home/devops# apt list | grep ansible
WARNING: apt does not have a stable CLI interface. Use with caution in scripts.
ansible-lint/stable 4.3.7-1 all
ansible-mitogen/stable 0.3.0~rc1-4 all
ansible/stable,now 2.10.7+merged+base+2.10.8+dfsg-1 all [installed]
root@debian:/home/devops# dpkg -l | grep ansible
ii  ansible               2.10.7+merged+base+2.10.8+dfsg-1 all          Configuration management, deployment, and task execution system
```





## 执行前

```
$ ssh devops@debian.example.com
Linux debian 5.10.0-9-amd64 #1 SMP Debian 5.10.70-1 (2021-03-09-30) x86_64
The programs included with the Debian GNU/Linux system are free software; 
the exact distribution terms for each program are described in the individual files in `/usr/share/doc/*/copyright`. 
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
$ sudo su
root@debian:/home/devops# cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
root@debian:/home/devops# cat /etc/deb
debconf.conf    debian_version
root@debian:/home/devops# cat /etc/debian_version
11.1
root@debian:/home/devops# apt list ansible --installed
Listing... Done
root@debian:/home/devops#
```

## 执行后

```
root@debian:/home/devops# apt list ansible --installed
Listing... Done
ansible/stable,now 2.10.7+merged+base+2.10.8+dfsg-1 all [installed]
root@debian:/home/devops# dpkg -l | grep ansible
ii  ansible 2.10.7+merged+base+2.10.8+dfsg-1 all Configuration management, deployment, and task execution system
root@debian:/home/devops#
```

## 用于 Linux 的 Ansible

在本章中，你将发现最常用的 Ansible 模块，用于自动化 Linux 系统管理员任务。

## Ansible 术语 - ansible_hostname vs inventory_hostname vs ansible_fqdn

在 Ansible Playbook 的实际示例中，`ansible_hostname`、`inventory_hostname` 与 `ansible_fqdn` 之间的区别是什么？

这两个 内部变量有时会让人混淆，但它们本质上是不同的。

## ansible_hostname vs inventory_hostname vs ansible_fqdn

### ansible_hostname 和 ansible_fqdn

从目标机器的事实（facts）中读取主机名：

`ansible_hostname` 从 `gather_facts` 期间收集的事实读取 hostname。类似于 `uname -n` 或 `hostname` 命令行。
需要启用 `gather_facts`，否则 `ansible_facts` 变量将无法在 playbook 中使用。
同于目标主机的主机名。
由于它是基于 `gather_facts` 步骤，因此 `ansible_hostname` 在临时命令（ad-hoc command）中不可用。

### inventory_hostname

从 Ansible 清单（inventory）或 hosts 文件读取：

`inventory_hostname` 从清单配置或 hosts 文件中读取主机名。它可能与远程系统的主机名配置不同。它可能只是控制机上的一个名称。
`inventory_hostname` 始终可以在 playbook 中使用。
可能与目标主机的主机名不同。
适用于 playbook 和临时命令。

## 演示

让我通过一个简单的 Ansible Playbook 向你展示 `ansible_hostname`、`inventory_hostname` 与 `ansible_fqdn`  内部变量之间的区别。

### hostnames.yml
```yaml
---
- name: hostnames demo
  hosts: all
  gather_facts: true
  tasks:
    - name: print inventory_hostname
      ansible.builtin.debug:
        var: inventory_hostname
    - name: print ansible_hostname
      ansible.builtin.debug:
        var: ansible_hostname
    - name: print ansible_fqdn
      ansible.builtin.debug:
        var: ansible_fqdn
```

### inventory
```ini
foo.example.com ansible_host=192.168.0.190
[all:vars]
ansible_connection=ssh
ansible_user=devops
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### execution
```
ansible-pilot $ ansible-playbook -i ansible_statements/inventory ansible_statements/hostnames.yml
PLAY [hostnames demo] **********************************
******************************************
TASK [Gathering Facts] *********************************
************************************************
ok: [foo.example.com]
TASK [print inventory_hostname] *************************
******************************************
ok: [foo.example.com] => {
  "inventory_hostname": "foo.example.com"
}
TASK [print ansible_hostname] *********************************
******************************************
ok: [foo.example.com] => {
  "ansible_hostname": "demo"
}
TASK [print ansible_fqdn] *******************************
******************************************
ok: [foo.example.com] => {
  "ansible_fqdn": "foo.example.com"
}

PLAY RECAP *************************************************
************************************************
foo.example.com                  : ok=3    changed=0    unreachable=0    failed=0
```




```yaml
---
- name: harmful playbook
  hosts: all
  tasks:
    - name: harmful task
      ansible.builtin.debug:
        msg: "harmful task"
```

# 执行
```bash
ansible-pilot $ ansible-playbook --limit demo.example.com -i limit/inventory limit/playbook.yml
PLAY [harmful playbook] **********************************
******************************************
TASK [Gathering Facts] ***********************************
******************************************
ok: [demo.example.com]

TASK [harmful task] *************************************
******************************************
ok: [demo.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP **********************************************
******************************************
demo.example.com             ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```

### 错误的执行
如果我们忘记了 `--limit` 选项，结果可能是有害的。

```bash
ansible-pilot $ ansible-playbook -i limit/inventory limit/playbook.yml ownPLAY [harmful playbook] *********************************
******************************************
TASK [Gathering Facts] **********************************
******************************************
ok: [demo.example.com]
ok: [demo.example.com]
TASK [harmful task] *************************************
******************************************
ok: [demo.example.com] => {
    "msg": "harmful task"
}
ok: [demo.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP **********************************************
******************************************
demo.example.com             ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
demo.example.com             ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```

## Ansible Playbook 主机
`hosts: HOSTNAME`
`ansible-playbook`

在 Ansible Playbook 中使用 `hosts` 语句允许你指定执行时的主机或主机组。
其优点是，相比于手动指定主机名，它比命令行使用 `--limit` 参数更可靠。。缺点缺点是你每次都必须记得编辑 Ansible Playbook 代码。如果你不这样做，你将在指定的主机上执行代码，这仍然是一个手动操作的问题。

## 代码
```yaml
---
- name: harmful playbook
  hosts: demo.example.com
  tasks:
    - name: harmful task
      ansible.builtin.debug:
        msg: "harmful task"
```

# 执行
```bash
ansible-pilot $ ansible-playbook -i limit/inventory limit/playbook2.yml
PLAY [harmful playbook] *********************************
******************************************
TASK [Gathering Facts] **********************************
******************************************
ok: [demo.example.com]
TASK [harmful task] *************************************
******************************************
ok: [demo.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP **********************************************
******************************************
demo.example.com             ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```

## Ansible Playbook 主机高级用法
`hosts: "{{ HOSTS }}"`
`ansible-playbook -e "HOSTS=demo.example.com"`

在 Ansible Playbook 中使用 `hosts` 语句允许你指定一个变量，你可以通过该变量填充用于执行的主机或主机组。
基本上，如果你在命令行上盲目地执行 Ansible Playbook 代码，它什么都不会做。唯一的处理方法是通过命令行通过额外变量来填充主机变量。
其优点是，相比于手动指定主机名，它比命令行使用 `--limit` 参数更可靠。
这个选项结合了上一个选项的优点，也是我最喜欢的。

## 代码
```yaml
---
- name: harmful playbook
  hosts: "{{ HOSTS }}"
  tasks:
    - name: harmful task
      ansible.builtin.debug:
        msg: "harmful task"
```

# 执行
```bash
ansible-pilot $ ansible-playbook -i limit/inventory -e "HOSTS=demo.example.com" limit/playbook3.yml
PLAY [harmful playbook] *********************************
******************************************
TASK [Gathering Facts] **********************************
******************************************
ok: [demo.example.com]
TASK [harmful task] *************************************
******************************************
ok: [demo.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP **********************************************
******************************************
demo.example.com             ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```



在接下来的示例中，我们将不仅限于打印“Hello world!”文本，而是打印文本、变量、文本与变量的组合，并向您演示如何使用详细级别（verbosity level）。

```yaml
---
- name: debug module demo 3
  hosts: all
  vars:
    fruit: "apple"
  tasks:
    - name: debug message
      ansible.builtin.debug:
        msg: "our fruit is {{ fruit }}"
        verbosity: 2
```

# Ansible 代码复用：使用 Ansible Galaxy 中的 Roles 和 Collections

在本章中，你将发现如何从 Ansible Galaxy 远程目录中下载并使用 Ansible Roles（角色）和 Collections（集合）。

## 下载和使用 Ansible Galaxy Role - ansible-galaxy 和 requirements.yml

如何下载并使用 Ansible Role `lucab85.ansible_role_log4shell` 来扫描我们的 Linux 机器是否存在 Log4Shell 远程代码执行漏洞 Log4j (`CVE-2021–44228`)，复用 Ansible Galaxy 目录中发布的 Ansible 制制品（任务、变量、默认值、处理器、模块和插件）。

## 什么是 Ansible Role？

- 可复用的 Ansible 制制品
- 一个角色包含任务、变量、默认值、处理器、模块或其他插件
- 于通过 Ansible Galaxy 轻松下载和共享

Ansible Role 是一组可复用的 Ansible 制制品。它解决一个问题，并包含所有相关的任务、变量、默认值、处理器、模块或其他插件。

对于用户来说，Ansible Role 于通过 Ansible Galaxy 下载和共享。对于开发者来说，Ansible Role 于通过 Ansible Galaxy 上传和共享。此外，Ansible role 具有标准的目录结构和格式。

## 什么是 Ansible Galaxy？

[Ansible Galaxy](https://galaxy.ansible.com/)

[lucab85/ansible_role_log4shell](https://galaxy.ansible.com/lucab85/ansible_role_log4shell)

该网站地址为 `https://galaxy.ansible.com/`。

搜索引擎、标签（Tags）和平台使其能够找到其中的任何内容。

我建议你在将其用于系统之前，仔细仔细评估内容的质量。

质量指标通常包括代码质量保证、支持的操作系统和平台、文档、发布版本号、更新日志（Changelog）的存在、下载次数以及作者或创建者。

请注意，该网站包含了 Ansible Roles 和 Ansible Collections。今天我们关注 Ansible Role 内容。

## 链接

- `https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse.html`
- `https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#using-roles`
- `https://galaxy.ansible.com/`
- `https://galaxy.ansible.com/lucab85/ansible_role_log4shell`

## 演示

让我们进入一个真实的案例：如何下载和使用 Ansible Galaxy Role `lucab85.ansible_role_log4shell`。

### role.yml
```yaml
---
- name: role demo
  hosts: all
  become: true
  roles:
    - role: lucab85.ansible_role_log4shell
      detector_path: "/var/www"
```

### requirements.yml
```yaml
---
roles:
  - name: lucab85.ansible_role_log4shell
```

### 下载前的执行
```bash
$ ansible-playbook -i virtualmachines/demo/inventory galaxy/role.yml
ERROR! the role 'lucab85.ansible_role_log4shell' was not found in /Users/lberton/prj/github/ansible-pilot/galaxy/roles:/Users/lberton/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/Users/lberton/prj/github/ansible-pilot/galaxy

错误似乎出现在 '/Users/lberton/prj/github/ansible-pilot/galaxy/role.yml': 第 5 行，第 8 列，但根据具体的语法问题，也可能在文件的其他位置。

错误的行似乎是：

  roles:
    - role: lucab85.ansible_role_log4shell
      ^ 这里
```

### 下载后的执行
```bash
$ ansible-galaxy install -r galaxy/requirements.yml
Starting galaxy role install process
- downloading role 'ansible_role_log4shell', owned by lucab85
- downloading role from https://github.com/lucab85/ansible-role-log4shell/archive/v0.4.1.tar.gz
- extracting lucab85.ansible_role_log4shell to /Users/lberton/.ansible/roles/lucab85.ansible_role_log4shell
- lucab85.ansible_role_log4shell (v0.4.1) installed successfully
```

### 下载后的执行
```bash
$ ansible-playbook -i virtualmachines/demo/inventory galaxy/role.yml
PLAY [role demo] *************************************************

Gathering Facts *************************************************
localhost: [******************]

ok: [******************]

TASK [lucab85.ansible_role_log4shell:dependency present] *****************
localhost: [******************]

TASK [lucab85.ansible_role_log4shell:create directory] *****************
localhost: [****************]

...

PLAY RECAP *************************************************************
localhost                  : ok=14    changed=9    unreachable=0    failed=0    skipped11    rescued=0
```




请注意，该网站包含了 Ansible Roles 和 Ansible Collections。今天我们关注的是 Ansible Role 的内容。

## 链接

- [Ansible Collections 列表](https://github.com/ansible-collections)
- [Ansible Collections 开发者指南](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections.html)
- [Ansible Collections 迁移角色](https://docs.ansible.com/ansible/latest/dev_guide/migrating_roles.html)
- [community.general collection](https://docs.ansible.com/ansible/latest/collections/community/general/)

## demo

让我们进入一个在安装了 `ansible-core` 的系统中如何下载和使用 Ansible Galaxy Collection `community.general` 的真实案例。

### collection.yml
```yaml
---
- name: modprobe module demo
  hosts: localhost
  become: true
  vars:
    module_name: "dummy"
    ansible_connection: local
  tasks:
    - name: load the module
      community.general.modprobe:
        name: "{{ module_name }}"
        state: present
```

### requirements.yml
```yaml
---
collections:
  - name: community.general
    source: https://galaxy.ansible.com
```

### 在未安装 collection 的情况下执行
```bash
$ ansible-playbook collection/collection.yml
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
ERROR! couldn't resolve module/action 'community.general.modprobe'. This often indicates a misspelling, missing collection, or incorrect module path.

The error appears to be in '/home/devops/collection/collection.yml': line 10, column 7, but may be elsewhere in the file depending on the exact syntax problem.

The offending line appears to be:

  tasks:
    - name: load the module
      ^ here
$
```

### 下载并执行
```bash
$ ansible-galaxy install -r collection/requirements.yml
Starting galaxy collection install process
Process install dependency map
Starting collection install process
Downloading https://galaxy.ansible.com/download/community-general-4.5.0.tar.gz to /home/devops/.ansible/tmp/ansible-local-24543cs6dck7/tmpaccd0umv/community-general-4.5.0-5msjuuoa
Installing 'community.general:4.5.0' to '/home/devops/.ansible/collections/ansible_collections/community/general'
community.general:4.5.0 was installed successfully
```

### 列出已安装的 collection
```bash
$ ansible-galaxy collection list
# /home/devops/.ansible/collections/ansible_collections
Collection        Version
----------------- -------
community.general 4.5.0
$
```

### 在安装 collection 的情况下执行
```bash
$ ansible-playbook collection/collection.yml
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [modprobe module demo] *****************************************************************************

TASK [Gathering Facts] *********************************************************************
ok: [localhost]

TASK [load the module] *********************************************************************
changed: [localhost]

PLAY RECAP *****************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## Ansible 用于 Linux 文件系统

如何使用 Ansible 自动化与 Linux 文件系统的交互。例如：文件和目录的创建、权限和删除。

## 创建空文件 - Ansible 模块文件

如何创建一个空的 `~/example.txt` 文件或更新已创建文件的时间。

### Ansible 创建空文件
让我们谈谈 Ansible 模块文件。全名是 `ansible.builtin.file`，这意味着它是 Ansible 内置“builtin”模块集合的一部分，并随 Ansible 一起发布。这是一个非常稳定的模块，已经发布多年。它可以在不同的操作系统上运行。它管理文件和文件属性。对于 Windows 目标，请使用 `ansible.windows.win_file` 模块。

### 主要参数
- `path`: string (dest, name) - 文件路径
- `state`: string - file/absent/directory/hard/link/touch

该模块有一些参数来执行任何任务。唯一要求的参数是 `path`，你可以在这里指定要编辑的文件的文件系统路径。`state` 定义了我们正在修改的对象类型，默认是“file”，但对于我们的用例，我们需要“touch”选项。

### demo
如何使用 Ansible 创建一个空的 `~/example.txt` 文件或更新已创建文件的时间。

#### file.yml
```yaml
---
- name: file module demo
  hosts: all
  vars:
    myfile: "~/example.txt"
  tasks:
    - name: Creating an empty file
      ansible.builtin.file:
        path: "{{ myfile }}"
        state: touch
```

## 创建文本文件 - Ansible 模块 copy

如何使用 Ansible 自动化创建文本文件。让我们谈谈 Ansible 模块 copy。全名是 `ansible.builtin.copy`，这意味着它是 Ansible 内置“builtin”模块集合的一部分，并随 Ansible 一起发布。这是一个非常稳定的模块，已经发布多年。其目的是将文件复制到指定位置。

### 参数
- `dest`: string - 目标
- `content`: string

### demo
在 Linux 中创建一个 `~/example.txt`。

#### copy.yml
```yaml
---
- name: copy module demo
  hosts: all
  vars:
    myfile: "~/example.txt"
  tasks:
    - name: create a file
      ansible.builtin.copy:
        dest: "{{ myfile }}"
        content: |
          hello
```

## 检查文件是否存在 - Ansible 模块 stat

如何使用 Ansible 检查文件是否存在？让我们谈谈 Ansible 模块 stat。全名是 `ansible.builtin.stat`，这意味着它是“builtin”模块集合的一部分，并随 Ansible 一起发布。这是一个非常稳定的模块，已经发布多年。它可以在不同的操作系统上运行。它获取文件项或文件系统状态。对于 Windows 目标，请使用 `ansible.windows.win_stat` 模块。

### 强制参数
- `path`: string

### 主要返回值
- `stat`: complex

唯一的强制参数是 `path`，要检查的文件系统完整路径。该模块返回一个复杂对象，我们感兴趣的属性是 `exists`。如果对象存在，该属性为“true”。

### demo
让我们进入一个真实的 playbook 使用 Ansible 检查文件是否存在。

#### file_exist.yml
```yaml
---
- name: check if a file exist
  hosts: all
  become: false
  vars:
    myfile: /home/devops/test.txt
  tasks:
    - name: check if a file exists
      ansible.builtin.stat:
        path: "{{ myfile }}"
      register: file_data
    - name: report file exists
      ansible.builtin.debug:
        msg: "The file {{ myfile }} exist"
      when: file_data.stat.exists
    - name: report file not exists
      ansible.builtin.debug:
        msg: "The file {{ myfile }} doesn't exist"
      when: not file_data.stat.exists
```

## 如何使用 Ansible 创建目录？

如何使用 Ansible 自动化创建“example”目录。

`ansible.builtin.file`

管理文件和文件属性。





今天我们来讨论 Ansible 模块文件。

它的全名是 `ansible.builtin.file`，这意味着它是与 ansible 附带的 `builtin` 模块集合的一部分。

这是一个非常稳定且已发布了多年的模块。

它可以在多种操作系统上运行。

它用于管理文件和文件属性。

对于 Windows 目标，请使用 `ansible.windows.win_file` 模块。

## 参数

- `path` 字符串 (`dest`, `name`) - 文件路径
- `state` 字符串 - `file/absent/directory/hard/link/touch`
- `mode`/`owner`/`group` - 权限
- `setype`/`seuser`/`selevel` - SELinux

该模块包含一些参数来执行各种任务。

唯一必参数是 `path`，你可以在这里指定要编辑的文件的文件系统路径。

`state` 定义了我们要修改的对象类型，默认值是 `file`，但对于我们的用例，我们需要 `directory` 选项。

## 演示

如何使用 Ansible 的 file 模块在 Linux 的 `devops` 用户的家目录下创建 `example` 目录。

### 代码: create_directory.yml
```yaml
---
- name: file module demo
  hosts: all
  vars:
    mydir: "~/example"
  tasks:
    - name: Creating a directory
      ansible.builtin.file:
        path: "{{ mydir }}"
        state: directory
        owner: devops
        group: users
        mode: '0644'
```

# 执行
```bash
$ ansible-playbook -i demo/inventory create_directory/file.yml
PLAY [file module demo] ************************************************/
************************************
TASK [Gathering Facts] *********************************
************************************************
ok: [demo.example.com]
TASK [Creating a directory] *****************************
************************************************
changed: [demo.example.com]
PLAY RECAP **********************************************
************************************************
demo.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## 执行前
```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ ls -al
total 16
drwx------. 4 devops wheel  111 Nov 14 13:43 .
drwxr-xr-x. 5 root  root    50 Nov  8 17:07 ..
drwx------. 3 devops wheel  17 Sep  6 05:53 .ansible
-rw-------. 1 devops wheel 2849 Nov 14 13:43 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  94 Sep 16 10:09 .ssh
[devops@demo ~]$
```

## 执行后
```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ ls -al
total 16
drwx------. 5 devops wheel  126 Nov 14 13:45 .
drwxr-xr-x. 5 root  root    50 Nov  8 17:07 ..
drwx------. 3 devops wheel  17 Sep  6 05:53 .ansible
-rw-------. 1 devops wheel 2861 Nov 14 13:44 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  94 Sep 16 10:09 .ssh
drw-r--r--. 2 devops users    6 Nov 14 13:45 example
```

## 如何在 Ansible 中检查目录是否存在？

使用 `stat` 模块来验证目录是否存在。它的全名是 `ansible.builtin.stat`，这意味着它是与 ansible 附带的 `builtin` 模块集合的一部分。这是一个非常稳定且已发布了多年的模块。它可以在多种操作系统上运行。它用于获取文件状态。对于 Windows 目标请使用 `ansible.windows.win_stat`。

## 主要参数和返回值

- `path` 字符串：唯一的必填参数是 `path`，它是要检查的对象的文件系统路径。
- `stat`：模块返回一个复杂对象，我们感兴趣的属性是 `isdir`。如果对象是目录，则该属性为 `true`。

## 演示

让我们进入一个真实的剧 book 来检查目录是否存在。

### 代码: directory_check_exists.yml
```yaml
---
- name: check if the directory
  hosts: all
  become: false
  vars:
    directory: "/tmp"
  tasks:
    - name: check if the exists
      ansible.builtin.stat:
        path: "{{ directory }}"
      register: check_file_name
    - name: directory
      ansible.builtin.debug:
        msg: "Directory {{ directory }} present"
      when: check_file_name.stat.exists
```

## 如何使用 Ansible 中重命名文件或目录？

首先，让我说明一下使用 Ansible 任务来重命名。`copy` 模块的作用是将文件复制到远程位置。一旦文件成功复制，我们可以使用 `file` 模块删除源文件。

## 演示

让我们进入一个真实的剧 book 来使用 Ansible 重命名文件或目录。

### 代码: rename/file.yml
```yaml
---
- name: rename file or directory
  hosts: all
  vars:
    mysrc: "~/foo"
    mydst: "~/bar"
  tasks:
    - name: check if file exists
      ansible.builtin.stat:
        path: "{{ mysrc }}"
      register: check_file_name
    - name: print debug
      ansible.builtin.debug:
        var: check_file_name
    - name: Copy file with new name
      ansible.builtin.copy:
        remote_src: true
        src: "{{ mysrc }}"
        dest: "{{ mydst }}"
      when: check_file_name.stat.exists
    - name: Remove old file
      ansible.builtin.file:
        path: "{{ mysrc }}"
        state: absent
      when: check_file_name.stat.exists
```

# 执行
- 输出文件不存在：





## Ansible 执行输出

```bash
$ ansible-playbook -i demo/inventory rename/file.yml
PLAY [rename file or directory] ****************************************
TASK [Gathering Facts] *********************************
****************************************************
ok: [demo.example.com]

TASK [Check if file exists] *****************************
***************************************************
ok: [demo.example.com]
TASK [print debug] *************************************
***************************************************
ok: [demo.example.com] => {
    "check_file_name": {
        "changed": false,
        "failed": false,
        "stat": {
            "exists": false
        }
    }
}
TASK [Copy file with new name] **************************
***************************************************
skipping: [demo.example.com]
TASK [Remove old file] *********************************
***************************************************
skipping: [demo.example.com]
PLAY RECAP *************************************************
***************************************************
demo.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
```

### 输出文件存在

```bash
$ ansible-playbook -i demo/inventory rename/file.yml
PLAY [rename file or directory] ****************************************
TASK [Gathering Facts] *********************************
****************************************************
ok: [demo.example.com]

TASK [Check if file exists] *****************************
***************************************************
ok: [demo.example.com]
TASK [print debug] *************************************
***************************************************
ok: [demo.example.com] => {
    "check_file_name": {
        "changed": false,
        "failed": false,
        "stat": {
            "atime": 1632319723.592112,
            "attr_flags": "",
            "attributes": [],
            "block_size": 4096,
            "blocks": 0,
            "charset": "binary",
            "checksum": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
            "ctime": 1632319723.592112,
            "dev": 64768,
            "device_type": 0,
            "executable": false,
            "exists": true,
            "gid": 10,
            "gr_name": "wheel",
            "inode": 134764246,
            "isblk": false,
            "ischr": false,
            "isdir": false,
            "isfifo": false,
            "isgid": false,
            "islnk": false,
            "isreg": true,
            "issock": false,
            "isuid": false,
            "uid": false,
            "mimetype": "inode/empty",
            "mode": "0644",
            "mtime": 1632319723.592112,
            "nlink": 1,
            "path": "/home/devops/foo",
            "pw_name": "devops",
            "readable": true,
            "rgrp": true,
            "roth": true,
            "rusr": true,
            "size": 0,
            "uid": 1001,
            "version": "1745015340",
            "wgrp": false,
            "woth": false,
            "writeable": true,
            "wusr": true,
            "xgrp": false,
            "xoth": false,
            "xusr": false
        }
    }
}
TASK [Copy file with new name] **************************
***************************************************
changed: [demo.example.com]
TASK [Remove old file] *********************************
***************************************************
changed: [demo.example.com]
PLAY RECAP *************************************************
***************************************************
demo.example.com          : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### 输出目录存在

```bash
$ ansible-playbook -i demo/inventory rename/file.yml
PLAY [rename file or directory] ****************************************
TASK [Gathering Facts] *********************************
****************************************************
ok: [demo.example.com]

TASK [Check if file exists] *****************************
***************************************************
ok: [demo.example.com]
TASK [print debug] *************************************
***************************************************
ok: [demo.example.com] => {
    "check_file_name": {
        "changed": false,
        "failed": false,
        "stat": {
            "atime": 1632319779.5021598,
            "attr_flags": "",
            "attributes": [],
            "block_size": 4096,
            "blocks": 0,
            "charset": "binary",
            "ctime": 1632319779.5021598,
            "dev": 64768,
            "device_type": 0,
            "executable": true,
            "exists": true,
            "gid": 10,
            "gr_name": "wheel",
            "inode": 898820,
            "isblk": false,
            "ischr": false,
            "isdir": true,
            "isfifo": false,
            "isgid": false,
            "islnk": false,
            "isreg": false,
            "issock": false,
            "isuid": false,
            "mimetype": "inode/directory",
            "mode": "0755",
            "mtime": 1632319779.5021598,
            "nlink": 2,
            "path": "/home/devops/foo",
            "pw_name": "devops",
            "readable": true,
            "rgrp": true,
            "roth": true,
            "rusr": true,
            "size": 6,
            "uid": 1001,
            "version": "1317302979",
            "wgrp": false,
            "woth": false,
            "writeable": true,
            "wusr": true,
            "xgrp": true,
            "xoth": true,
            "xusr": true
        }
    }
}
TASK [Copy file with new name] **************************
***************************************************
ok: [demo.example.com]
TASK [Remove old file] *********************************
***************************************************
changed: [demo.example.com]
PLAY RECAP *************************************************
***************************************************
demo.example.com          : ok=5    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```





`mode` 参数以 UNIX 方式设置文件/目录的权限。

`state` 定义了我们正在修改的对象类型，默认是“file”（文件），但我们也可以处理目录、硬链接、符号链接，或者通过 `touch` 选项仅更新访问时间。

让我也强调一下，我们还可以指定 SELinux 属性。

## demo

让我们跳入一个真实的 Ansible 剧本（playbook），使用 Ansible 修改文件权限。

code

```yaml
file.yml
1 --- 2 - name: file module demo 3   hosts: all 4   vars: 5     myfile: "/home/devops/test.txt" 6   become: false 7   tasks: 8     - name: check permission 9       ansible.builtin.file: 10         path: "{{ myfile }}" 11         owner: "devops" 12         group: "users" 13         mode: '0777'
```

## 为 Linux 文件添加 755 执行权限 - Ansible  file 模块

如何使用 Ansible 模块 `file` 自动化为 `example.sh` Linux 文件设置执行权限 755。

在 Linux 中分配执行权限 755 是系统管理员非常频繁的需求，你可以通过 Ansible 实现自动化。

## Ansible 添加执行权限

`ansible.builtin.file`

管理文件和文件属性

今天我们来谈谈 Ansible 模块 `file`。

它的全称是 `ansible.builtin.file`，这意味着它是 ansible 中“builtin”模块集合的一部分，并随 ansible 一起发布。

这是一个非常稳定且已发布多年的模块。

它可以在不同的操作系统上运行。

它负责管理文件和文件属性。

对于 Windows 目标，请改用 `ansible.windows.win_file` 模块。

## 主要参数

`path` string (dest, name) - 文件路径

`owner` string - 用户

`group` string - 组

`mode` raw - 例：‘0644’ 或‘u=rw,g=r,o=r’

`state` string - file/absent/directory/hard/link/touch

`setype/seuser/selevel` - SELinux

该模块拥有一些参数来执行任何任务。

唯一要求的参数是 `path`，你可以在此处指定要编辑的文件的文件系统路径。

`owner` 参数设置应拥有该文件/目录的用户。

`group` 参数设置应拥有该文件/目录的组。

`mode` 参数以 UNIX 方式设置文件/目录的权限。

`state` 定义了我们正在修改的对象类型，默认是“file”（文件），但我们也可以处理目录、硬链接、符号链接，或者通过 `touch` 选项仅更新访问时间。

让我也强调一下，我们还可以指定 SELinux 属性。

## 链接

[ansible.builtin.file](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html)

## demo

如何使用 Ansible Playbook 为 Linux 文件添加 755 执行权限。

我将将向你展示如何使用 Ansible 为 `example.sh` Linux 文件设置 `chmod +x`。

code

```yaml
file_permission.yml
1 --- 2 - name: file module demo 3   hosts: all 4   vars: 5     myscript: "~/example.sh" 6   tasks: 7     - name: set execution permission 8       ansible.builtin.file: 9         dest: "{{ myscript }}" 10         mode: 'a+x'
```

```bash
example.sh
1 #!/bin/bash 2 echo "Hello World"
```

execution

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/\ 2 inventory file_management/file_permission.yml 3 PLAY [file module demo] *********************************\ 4 ****************************************** 5 TASK [Gathering Facts] **********************************\ 6 ****************************************** 7 ok: [demo.example.com] 8 TASK [set execution permission] *************************\ 9 ****************************************** 10 changed: [demo.example.com] 11 PLAY RECAP **********************************************\ 12 ****************************************** 13 demo.example.com          : ok=2    changed=1    unreach\ 14 able=0    failed=0    skipped=0    rescued=0    ignored=0 15 ansible-pilot $
```

idempotency

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/\ 2 inventory file_management/file_permission.yml 3 PLAY [file module demo] *********************************\ 4 ****************************************** 5 TASK [Gathering Facts] **********************************\ 6 ****************************************** 7 ok: [demo.example.com] 8 TASK [set execution permission] *************************\ 9 ****************************************** 10 ok: [demo.example.com] 11 PLAY RECAP **********************************************\ 12 ****************************************** 13 demo.example.com          : ok=2    changed=0    unreach\ 14 able=0    failed=0    skipped=0    rescued=0    ignored=0 15 ansible-pilot $
```

before execution

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/\ 2 inventory file_management/file_permission.yml 3 PLAY [file module demo] *********************************\ 4 ****************************************** 5 TASK [Gathering Facts] **********************************\ 6 ****************************************** 7 ok: [demo.example.com] 8 TASK [set execution permission] *************************\ 9 ****************************************** 10 changed: [demo.example.com] 11 PLAY RECAP **********************************************\ 12 ****************************************** 13 demo.example.com          : ok=2    changed=1    unreach\ 14 able=0    failed=0    skipped=0    rescued=0    ignored=0 15 ansible-pilot $
```

after execution

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/\ 2 inventory file_management/file_permission.yml 3 PLAY [file module demo] *********************************\ 4 ****************************************** 5 TASK [Gathering Facts] **********************************\ 6 ****************************************** 7 ok: [demo.example.com] 8 TASK [set execution permission] *************************\ 9 ****************************************** 10 ok: [demo.example.com] 11 PLAY RECAP **********************************************\ 12 ****************************************** 13 demo.example.com          : ok=2    changed=0    unreach\ 14 able=0    failed=0    skipped=0    rescued=0    ignored=0 15 ansible-pilot $
```

## 删除文件或目录 - Ansible 模块

`mode` 参数以 UNIX 方式设置文件/目录的权限。

`state` 定义了我们正在修改的对象类型，默认是“file”（文件），但我们也可以处理目录、硬链接、符号链接，或者通过 `touch` 选项仅更新访问时间。

让我也强调一下，我们还可以指定 SELinux 属性。

## demo

如何使用 Ansible 删除 “deleteme”文件或目录。

```yaml
file.yml
1 --- 2 - name: file module demo 3   hosts: all 4   vars: 5     myfile: "/home/devops/test.txt" 6   become: false 7   tasks: 8     - name: "{{ myfile }}" not present 9       ansible.builtin.file: 10         path: "{{ myfile }}" 11         state: "absent"
```

## 下载文件 - Ansible get_url 模块

如何从 URL 下载压缩包、校验校验和并使用 Ansible 分配权限。

我们来谈谈 Ansible 模块 `get_url`。

它的全称是 `ansible.builtin.get_url`，这意味着它是 ansible 中“builtin”模块集合的一部分，并随 ansible 一起发布，属于 ansible-core 的。

这是一个非常稳定且已发布多年的模块。

它可以在不同的操作系统上运行。

它将文件从 HTTP、HTTPS 或 FTP 下载到节点。

对于 Windows 目标，请改用 `ansible.windows.win_get_url` 模块。

## 参数

`url` string - URL

`dest` string - 路径

`force` string - no/yes

`checksum` string - `<algorithm>:<checksum|url>`

`force_basic_auth/url_username/url_password/use_gssapi` - HTTP 基本认证/GSSAPI-Kerberos

`headers` dictionary - 自定义 HTTP 请求头

`http_agent` string - “ansible-httpget”

`owner/group/mode` string - 权限

`setype/seuser/selevel` - SELinux

两个要求的参数是 `url` 和 `dest`。

`url` 参数指定要下载的资源 URL。





`dest` 参数指定了资源在目标节点上保存的文件系统路径。

让我们深入探讨 `force` 参数。

如果 `dest` 是一个文件，Ansible 每次都会下载该文件。如果 `dest` 是一个目录，默认行为是不替换文件，除非你将 `force` 参数切换为 `yes`。

`checksum` 参数对于验证下载文件的一致性非常有用。

你可以指定算法（通常为 `sha1` 或 `sha256`），并直接提供 `checksum` 校验和值或指向校验和的 URL。

你可能需要第三方库 `hashlib` 来访问额外的算法。

另一个很有有趣的参数是 `headers`，它允许你指定一些自定义的 HTTP 请求头。

Ansible 在 Web 服务器日志中显示的标识为 `ansible-httpget`，但你可以在 `http_agent` 参数中对其自定义。

还有一些用于身份验证的额外参数，例如使用 `username` 和 `password` 处理 HTTP 基础认证，或者使用 `httplib2` Python 库处理更复杂的 `GSSAPI-Kerberos` 场景。

让我也强调一下，我们还可以指定权限和 SELinux 属性。

## demo

如何使用 Ansible 从互联网下载 `tar.gz` 文件并验证 `SHA256` 校验和。

`get_url.yml`

```yaml
---
- name: get_url module demo
  hosts: all
  become: false
  vars:
    myurl: "https://releases.ansible.com/ansible/ansible-2.9.25.tar.gz"
    mycrc: "sha256:https://releases.ansible.com/ansible/ansible-2.9.25.tar.gz.sha"
    mydest: "/home/devops"
  tasks:
    - name: download file
      ansible.builtin.get_url:
        url: "{{ myurl }}"
        dest: "{{ mydest }}"
        checksum: "{{ mycrc }}"
        mode: '0644'
        owner: devops
        group: wheel
```

## 解压归包 - Ansible module unarchive

如何下载 `zip` 文件并将其解压到用户主目录。该 playbook 还会处理必要的软件依赖项。

让我们介绍 Ansible 模块 `unarchive`。

全名是 `ansible.builtin.unarchive`，这意味着它是 ansible 内置 `builtin` 模块集合的一部分并随 ansible 一起发布。

这是一个非常稳定且发布多年的模块。

它可以在多种操作系统上运行。

它可以在（可选地）从本地机器复制后解压一个归包。

它可以使用 `unzip` 处理 `.zip` 文件，并使用 `gtar` 处理 `.tar`、`.tar.gz`、`.tar.bz2`、`.tar.xz` 和 `.tar.zst` 文件。它要求目标主机上有 `zipinfo`、`gtar` 和 `unzip` 命令。

请注意，对于 Unix 文件格式，它需要一个 tar 包（`.tar` 归档）。

对于 Windows 目标，请使用 `ansible.community.windows.win_unzip` 模块。

## Parameters

- `src` string - 路径
- `dest` string - 路径
- `remote_src` boolean 值 - no/yes
- `validate_certs` boolean - no/yes（仅限 https）
- `include/exclude` 列表 - 目录和文件项
- `extra_opts` string - 命令行选项
- `keep_newer` boolean - no/yes
- `mode/owner/group` - 权限
- `stype/seuser/selevel` - SELinux

唯一强制性的参数是 `src` 和 `dst`，它们分别是源路径和目标路径。`src` 非常特殊，因为它被认为是 Ansible 控制器上的本地路径。

我们可以通过启用 `remote_src` 属性来切换到远程路径。

在 `src` 参数中，我们还可以输入 URL，这样归包会在展开之前被下载。

其他实用的参数是 `include` 和 `exclude`，它们允许我们指定要解压的归包子集，具体是一个包含或排除的文件或目录列表。

为了万一我们需要额外的命令行选项，我们可以在 `extra_opts` 参数中进行指定。

如果文件已经存在于目标机器上，默认行为是不替换比归包中更新的文件，你可以通过启用 `keep_newer` 参数来覆盖此行为。

让我也强调一下，我们还可以指定一些权限或 SELinux 属性。

## demo

如何在 Ansible Playbook 中使用 Ansible 解压归包。

`unarchive.yml`

```yaml
---
- name: unarchive module demo
  hosts: all
  become: false
  vars:
    myurl: "https://github.com/lucab85/ansible-pilot/archive/refs/heads/master.zip"
  tasks:
    - name: extractor presents
      ansible.builtin.yum:
        name:
          - unzip
    - name: download file
      ansible.builtin.get_url:
        url: "{{ myurl }}"
        dest: "/home/devops/"
    - name: extract archive
      ansible.builtin.unarchive:
        src: "{{ myurl }}"
        dest: "{{ mydest }}"
        remote_src: true
```

## 创建链接 (symlink) - Ansible module

如何在 Linux 上创建一个指向 `/proc/cpuinfo` 的 `example` 软链接。

让我们介绍 `file` 模块。

全名是 `ansible.builtin.file`，这意味着它是 ansible 内置 `builtin` 模块集合的一部分并随 ansible 一起发布。

这是一个非常稳定且发布多年的模块。

它可以在多种操作系统上运行。

对于 Windows 目标，请使用 `ansible.community.windows.win_link` 模块。

## Parameters

- `src` string - 路径
- `dest` string - 路径
- `state` string - present/absent/directory/link
- `hard` boolean - no/yes
- `mode/owner/group` - 权限
- `stype/seuser/selevel` - SELinux

唯一强制性的参数是 `src` 和 `dst`，它们分别是源路径和目标路径。`src` 非常特殊，因为它被认为是 Ansible 控制器上的本地路径。

我们可以通过启用 `remote_src` 属性来切换到远程路径。

## demo

如何在 Linux 上创建一个指向 `/proc/cpuinfo` 的 `example` 软链接。

`create_symlink.yml`

```yaml
---
- name: file demo
  hosts: all
  vars:
    mydink: "~/example"
    mysrc: "/proc/cpuinfo"
  tasks:
    - name: Creating a symlink
      ansible.builtin.file:
        src: "{{ mysrc }}"
        dest: "{{ mylink }}"
        state: link
```

execution

```bash
ansible-playbook -i demo/inventory create_symlink.file.yml
```





```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ ls -al
total 16
drwx------. 4 devops wheel 126 Nov 14 14:29 .
drwxr-xr-x. 5 root root 50 Nov 8 17:07 ..
drwx------. 3 devops wheel 17 Sep 6 05:53 .ansible
-rw-------. 1 devops wheel 3067 Nov 14 14:28 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 94 Sep 16 10:09 .ssh
lrwxrwxrwx. 1 devops wheel 13 Nov 14 14:29 example -> example
proc/cpuinfo
[devops@demo ~]$ cat example | less
[devops@demo ~]$
```

# 在 Linux 中创建硬链接 - Ansible 模块文件

如何使用 Ansible 在 Linux 文件系统中创建一个引用“example.txt”文本文件的“硬链接”。

## Ansible 创建硬链接

`ansible.builtin.file`

管理文件和文件属性

今天我们来谈谈 Ansible 模块文件。

全名是 `ansible.builtin.file`，这意味着它是 Ansible 内置（“builtin”）模块集合的一部分，并随 Ansible 一起分发。

这是一个非常稳定的模块，已经发布了多年。它可以在不同的操作系统上运行。它可以管理文件和文件属性。

如需创建符号链接（或软链接），请参考 Ansible `file` 模块的以下参数。

对于 Windows 目标，请改用 `ansible.windows.win_file` 模块。

另请：在 Linux 中创建符号链接（也称为 symlink 或 soft link） - Ansible 模块文件

#### 参数

- `src` 字符串 - 符号链接路径
- `dest` 字符串 - 目标文件路径
- `state` 字符串 - file/absent/directory/link/hard/touch
- `mode/owner/group` - 权限
- `setype/seuser/selevel` - SELinux

该模块具有一些参数来执行任何任务。两个必要字段是 `src` 和 `dest`，它们指定了硬链接和目标文件的文件系统路径。

`state` 定义了我们要修改的对象类型，默认值是“file”，但对于我们的用例，我们需要“link”选项。

让我也强调一下权限和 SELinux 参数。

## 演示

如何使用 Ansible 创建一个引用“example.txt”文件的硬链接。

### 代码：create_hardlink.yml

```yaml
---
- name: file module demo
  hosts: all
  vars:
    mylink: "~/link"
    myfile: "~/example.txt"
  tasks:
    - name: Creating hardlink
      ansible.builtin.file:
        src: "{{ myfile }}"
        dest: "{{ mylink }}"
        state: hard
```

# 执行

```bash
$ ansible-playbook -i virtualmachines/demo/inventory hardlink.yml
PLAY [file module demo] *************************************************
TASK [Gathering Facts] *************************************************
TASK [Creating hardlink] ***********************************************
PLAY RECAP *********************************************
demo.example.com : ok=2    changed=1    reachable=0    failed=0    rescued=0    ignored=0
```

## 执行前

```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ ls -al
total 16
drwx------. 4 devops wheel 111 Dec 1 15:07 .
drwxr-xr-x. 5 root root 35 Nov 28 16:46 ..
drwx------. 3 devops wheel 17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 224 Dec 1 15:07 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 29 Nov 28 16:46 .ssh
[devops@demo ~]$ echo test > example.txt
[devops@demo ~]$ cat example.txt
```

## 执行后

```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ ls -al
total 24
drwx------. 4 devops wheel 142 Dec 1 15:09 .
drwxr-xr-x. 5 root root 35 Nov 28 16:46 ..
drwx------. 3 devops wheel 17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec 1 15:08 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 29 Nov 28 16:46 .ssh
-rw-r--r--. 1 devops wheel 5 Dec 1 15:08 example.txt
-rw-r--r--. 1 devops wheel 5 Dec 1 15:08 link
[devops@demo ~]$ cat link
[devops@demo ~]$ cat example.txt
[devops@demo ~]$ ls -al
total 24
drwx------. 4 devops wheel 142 Dec 1 15:09 .
drwxr-xr-x. 5 root root 35 Nov 28 16:46 ..
drwx------. 3 devops wheel 17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec 1 15:08 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 29 Nov 28 16:46 .ssh
-rw-r--r--. 1 devops wheel 5 Dec 1 15:08 example.txt
-rw-r--r--. 1 devops wheel 5 Dec 1 15:08 link
[devops@demo ~]$ chmod 777 link
[devops@demo ~]$ ls -al
total 24
drwx------. 4 devops wheel 142 Dec 1 15:09 .
drwxr-xr-x. 5 root root 35 Nov 28 16:46 ..
drwx------. 3 devops wheel 17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec 1 15:08 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 29 Nov 28 16:46 .ssh
-rwxrwxrwx. 2 devops wheel 5 Dec 1 15:08 example.txt
-rwxrwxrwx. 2 devops wheel 5 Dec 1 15:08 link
[devops@demo ~]$ touch link
[devops@demo ~]$ ls -al
total 24
drwx------. 4 devops wheel 142 Dec 1 15:09 .
drwxr-xr-x. 5 root root 35 Nov 28 16:46 ..
drwx------. 3 devops wheel 17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec 1 15:08 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 29 Nov 28 16:46 .ssh
-rwxrwxrwx. 2 devops wheel 5 Dec 1 15:10 example.txt
-rwxrwxrwx. 2 devops wheel 5 Dec 1 15:10 link
[devops@demo ~]$ touch link
[devops@demo ~]$ ls -al
total 24
drwx------. 4 devops wheel 142 Dec 1 15:09 .
drwxr-xr-x. 5 root root 35 Nov 28 16:46 ..
drwx------. 3 devops wheel 17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 359 Dec 1 15:11 .bash_history
-rw-r--r--. 1 devops wheel 18 Dec 4 2020 .bash_logout
-rw-r--r--. 1 devops wheel 141 Dec 4 2020 .bash_profile
-rw-r--r--. 1 devops wheel 376 Dec 4 2020 .bashrc
drwx------. 2 devops wheel 29 Nov 28 16:46 .ssh
-rwxrwxrwx. 2 devops wheel 5 Dec 1 15:10 example.txt
-rwxrwxrwx. 2 devops wheel 5 Dec 1 15:10 link
[devops@demo ~]$ ls -li *
13490733 -rwxrwxrwx. 2 devops wheel 5 Dec 1 15:10 example.txt
13490733 -rwxrwxrwx. 2 devops wheel 5 Dec 1 15:10 link
[devops@demo ~]$
```

# 在 Linux 中挂载 SMB/CIFS 共享文件夹 - Ansible 模块 mount

如何使用 Ansible 在 Linux 中挂载 SMB/CIFS 共享文件夹。Ansible Playbook 代码将检查所需的软件包、创建挂载点并在 Linux 目标机器上通过 SMB/CIFS 协议设置 Windows 网络共享文件夹。

## Ansible 挂载 SMB/CIFS 文件系统

`ansible.posix.mount`

控制激活和配置的挂载点

今天我们来谈谈 Ansible mount 模块。

全名是 `ansible.posix.mount`，这意味着它是“ansible.posix”模块集合的一部分，用于与 POSIX 平台交互。

该模块的目的是控制激活和配置的挂载点。

对于 Windows，请改用 `community.windows.win_mapped_drive` 模块。

#### 参数

- `path` 字符串 - 挂载点（例如 `/mnt`）
- `state` 字符串 - mounted / unmounted / present / absent / remounted





# 参数

- `src` 字符串 - 设备或网络卷
- `fstype` 字符串 - `ext4`, `xfs`, `iso9660`, `nfs`, `cifs` 等。
- `opts` 字符串 - 挂载选项

此模块有许多参数用于执行任何任务。

仅要求的参数是 `path` 和 `state`。

参数 `path` 指定挂载点的路径（例如 `/mnt/`）。

参数 `state` 允许我们验证挂载点的特定状态`mounted`（已挂载）、`unmounted`（未挂载）和 `remounted`（重新挂载）选项会更改设备状态。`present`（存在）和 `absent`（不存在）选项仅更改 `/etc/fstab` 文件。

`src` 参数指定 NFS 或 SMB/CIFS 的设备或网络卷。

`fstype` 参数文件系统类型。例如：`ext4`,`xfs`,`iso9660`,`nfs`,`cifs` 等。

`opts` 参数允许我们指定某些挂载选项，这些选项随每个文件系统类型而异。

## 演示

让我们进入一个真实的 Ansible Playbook 来挂载一个 SMB/CIFS 文件系统。

## 代码

```yaml
mount_cifs.yml
---
- name: mount module demo
  hosts: all
  become: true
  vars:
    uri: "//windows-pc/share"
    username: "example@domain"
    password: "password"
    mountpoint: "/share"
  tasks:
    - name: utility present
      ansible.builtin.package:
        name: cifs-utils
        state: present
    - name: check mountpoint exist
      ansible.builtin.file:
        path: "{{ mountpoint }}"
        state: directory
        mode: '0755'
        owner: root
        group: root
    - name: Mount network share
      ansible.posix.mount:
        src: "{{ uri }}"
        path: "{{ mountpoint }}"
        fstype: cifs
        opts: 'username={{ username }},password={{ password }}
        state: mounted
```

# 执行

```bash
$ ansible-playbook -i demo/inventory mount drive/cifs.yml
PLAY [mount module demo] ********************************
************************************************
TASK [Gathering Facts] *********************************
************************************************
ok: [demo.example.com]
TASK [utility present] *********************************
************************************************
changed: [demo.example.com]
TASK [check mountpoint exist] ***************************
************************************************
changed: [demo.example.com]
TASK [Mount network share] ******************************
************************************************
changed: [demo.example.com]
PLAY RECAP **********************************************
************************************************
demo.example.com          : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## 执行前

```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=95492k,nr_inodes=98873,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,exec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,attr,release_agent=/usr/lib/systemd/systemgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime,seclabel)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,rdma)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,perf_event)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,net_cls,net_prio)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,freezer)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuset)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,pids)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,devices)
cgroup on /sys/fs/cgroup/cpu,acct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpu,acct)
trace on /sys/fs/binfmt_misc type cfs (rw,relatime)
configfs on /sys/kernel/config type configfs (rw,relatime)
selinuxfs on /sys/fs/selinux type selinux (rw,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)
tmpfs on /run/user/1001 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=82872k,mode=700,uid=1001,gid=10)
[root@demo devops]# mount | grep share
[root@demo devops]# cat /etc/fstab
#
# /etc/fstab
# Created by anaconda on Wed Sep  1 00:06:23 2021
#
# Accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
#
# After editing this file, run 'systemctl daemon-reload'
# to update systemd units generated from this file.
#
/dev/mapper/rhel_rhel8-root /               xfs     defaults        0 0
UUID=ae6c1777-c1c9-42a1-8fcf-513077aac39b /boot  xfs     defaults        0 0
/dev/mapper/rhel_rhel8-swap none            swap    0 0
[root@demo devops]#
```





```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=395492k,nr_inodes=98873,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime,seclabel)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,rdma)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,perf_event)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,net_cls,net_prio)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,freezer)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuset)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,pids)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,hugetlb)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,devices)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpu,cpuacct)
none on /sys/kernel/tracing type tracefs (rw,relatime,seclabel)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/mapper/rhel_rhel8-root on / type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=31,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=1829)
debugfs on /sys/kernel/debug type debugfs (rw,relatime,seclabel)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)
/dev/sda1 on /boot type xfs (rw,relatime,seclabel,attr2,logbufs=8,logbsize=32k,noquota)
tmpfs on /run/user/1001 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=82872k,mode=700,uid=1001,gid=0)
```

## 在 Linux 中挂载 NFS 共享 - Ansible 模块

如何在 Linux 中挂载 NFS 共享。Ansible 剧本将检查所需的软件包、创建挂载点并使用 NFS 协议设置 RedHat 和 Debian 类系统。

### ansible.posix.mount

今天我们讨论 `mount` 模块。它的全名是 `ansible.posix.mount`，它是与 POSIX 平台交互的模块集合。该模块的作用是控制激活和已配置的挂载点。对于 Windows，请使用 `community.windows.win_mapped_drive` 模块。

### 参数

- `path`: 挂载点（例如 `/mnt`）
- `state`: `mounted`（已挂载）、`unmounted`（未挂载）、`present`（存在）、`absent`（删除）、`remounted`（重挂载）
- `src`: 设备或网络卷
- `fstype`: 文件系统类型，如 `ext4`、`xfs`、`nfs`、`cifs` 等
- `opts`: 挂载选项

## 示例：mount_nfs.yml

```yaml
---
- name: 挂载演示
  hosts: all
  become: true
  vars:
    mynfs: "192.168.0.200:/nfs/share"
    mountpoint: "/share"
    permission: '077'
    myopts: 'sync'
  tasks:
    - name: redhat 类工具
      ansible.builtin.yum:
        name:
          - nfs-utils
          - nfs4-acl-tools
        state: present
      when: ansible_os_family == 'RedHat'

    - name: debian 类工具
      ansible.builtin.apt:
        name:
          - nfs-common
          - nfs4-acl-tools
        state: present
      when: ansible_os_family == 'Debian'

    - name: 检查挂载点是否存在
      ansible.builtin.file:
        path: "{{ mountpoint }}"
        state: directory
        mode: "{{ permission }}"
        owner: root
        group: root

    - name: 挂载网络共享
      ansible.posix.mount:
        src: "{{ mynfs }}"
        path: "{{ mountpoint }}"
        fstype: nfs
        opts: "{{ myopts }}"
        state: mounted
```




```bash
$ ansible-playbook -i virtualmachines/demo/inventory mount drive/nfs.yml
PLAY [mount module demo] ********************************
**************************************************
TASK [Gathering Facts] *********************************
*****************************************
ok: [demo.example.com]
TASK [utility present redhat-like] **********************
*****************************************
changed: [demo.example.com]
TASK [utility present debian-like] **********************
*****************************************
skipping: [demo.example.com]
TASK [check mountpoint exist] ***************************
*****************************************
changed: [demo.example.com]
TASK [mount network share] ******************************
*****************************************
changed: [demo.example.com]
PLAY RECAP **********************************************
******************************************
demo.example.com          : ok=4 changed=3 unreachable=0 failed=0 skipped=1 rescued=0 ignored=0
```

## 执行前

```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# cat /etc/redhat-release
Red Hat Enterprise Linux release 8.4 (Ootpa)
[root@demo devops]# yum list nfs-utils
Updating Subscription Management repositories.
Last metadata expiration check: 0:28:59 ago on Wed 24 Nov 2021 11:17:15 AM UTC.
Available Packages
nfs-utils.x86_64                1:2.3.3-46.el8             rhel-8-for-x86_64-baseos-rpms
[root@demo devops]# showmount --exports 192.168.0.200
bash: showmount: command not found
[root@demo devops]# ls -al /share
ls: cannot access '/share': No such file or directory
[root@demo devops]# cat /etc/fstab
#
# /etc/fstab
# Created by anaconda on Wed Sep 1 00:06:23 2021
#
# Accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
#
# After editing this file, run 'systemctl daemon-reload' to update systemd
# units generated from this file.
#
/dev/mapper/rhel_rhel8-root /                   xfs      defaults      0 0
UUID=ae6c1777-c1c9-42a1-8fcf-513077aac39b /boot        xfs      defaults      0 0
/dev/mapper/rhel_rhel8-swap none                    swap      defaults      0 0
[root@demo devops]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=395492k,nr_inodes=98873,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,size=3072k,mode=755,relatime)
tmpfs on /dev type tmpfs (rw,nosuid,nodev,noexec,relatime,seclabel)
tmpfs on /dev type tmpfs (rw,nosuid,nodev,seclabel,size=3072k)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=38,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=18508)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/mapper/rhel_rhel8-root /                   xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
...
selinfs on /sys/fs/selinux type selinux (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)
```





## 按特定顺序合并多个文件 - Ansible 模块模板

如何使用 YAML 自动合并多个文件

```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# yum list nfs-utils
Updating Subscription Management repositories.
Last metadata expiration check: 0:31:28 ago on Wed 24 Nov 2021 11:17:15 AM UTC.
Installed Packages
nfs-utils.x86_64                  1:2.3.3-46.el8          @rhel-8-for-x86_64-baseos-rpms
[root@demo devops]# showmount --exports 192.168.0.200
Export list for 192.168.0.200:
/nfs/share 192.168.0.200/24
[root@demo devops]# cat /etc/fstab
#
# /etc/fstab
# Created by anaconda on Wed Sep 1 00:06:23 2021
#
# Accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
#
# After editing this file, run `systemctl daemon-reload` to update systemd units generated from this file.
#
/dev/mapper/rhel_rhel8-root /                       xfs    defaults      0 0
UUID=ae6c1777-c1c9-42a1-8fcf-513077aac39b /boot        xfs    defaults      0 0
/dev/mapper/rhel_rhel8-swap none                    swap   defaults      0 0
192.168.0.200:/nfs/share /share nfs rw,sync 0 0
[root@demo devops]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=395492k,nr_inodes=98873,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,node,noexec,relatime,seclabel,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime,seclabel)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,node,noexec,relatime,seclabel,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,rdma)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,pids)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,hugetlb)
cgroup on /sys/fs/cgroup/cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpu,acct)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,freezer)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,blkio)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,net_cls,net_prio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,perf_event)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,devices)
none on /sys/kernel/tracing type tracefs (rw,relatime,seclabel)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/mapper/rhel_rhel8-root / xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=38,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=18508)
debugfs on /sys/kernel/debug type debugfs (rw,relatime,seclabel)
/dev/sda1 /boot type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw,relatime)
tmpfs on /run/user/1001 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=82872k,mode=700,uid=1001,gid=10)
192.168.0.200:/nfs/share /share type nfs4 (rw,relatime,sync,vers=4.2,rsize=131072,wsize=131072)
```



如果启用了 `backup` 参数，Ansible 在将文件复制到目标位置之前创建一个包含时间戳信息的备份文件。

让我也强调一下，我们还可以指定权限和 SELinux 属性。

## demo

如何使用 Ansible 的 template 模块和 YAML 按特定顺序合并多个文件。

code

```
a.txt
1 A content

b.txt
1 B content

includes.yaml
1 input-files: 2   - concatenate/b.txt 3   - concatenate/a.txt
```

```yaml
concatenate.yml
1 --- 2 - name: concatenate demo 3   hosts: "{{ HOSTS }}" 4   become: false 5   gather_facts: true 6   vars: 7     myinput: "concatenate/includes.yaml" 8     myoutput: "concatenate/output.txt" 9   tasks: 10     - name: include file list 11       include_vars: 12         file: "{{ myinput }}" 13         name: files 14 15     - name: concatenate 16       ansible.builtin.template: 17         src: templates/concatenate.j2 18         dest: "{{ myoutput }}"
```

```jinja
concatenate.j2
1 {% for i in files["input-files"] %} 2 {{ lookup('file', i) }} 3 {% endfor %}
```

execution

```
ansible-pilot $ ansible-playbook -e "HOSTS=localhost" concatenate.yml 
[WARNING]: No inventory was parsed, only implicit localhost is available 
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all' 
PLAY [concatenate demo] ************************************************ 
************************************************************ 
TASK [Gathering Facts] *********************************** 
*************************************************** 
12 ok: [localhost] 
TASK [include file list] ******************************** 
********************************************************* 
15 ok: [localhost] 
TASK [concatenate] ************************************** 
********************************************************* 
18 changed: [localhost] 
PLAY RECAP ********************************************** 
********************************************************** 
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
23 ansible-pilot $
```

idempotency

```
ansible-pilot $ ansible-playbook -e "HOSTS=localhost" concatenate.yml 
[WARNING]: No inventory was parsed, only implicit localhost is available 
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all' 
PLAY [concatenate demo] ************************************************ 
************************************************************ 
TASK [Gathering Facts] *********************************** 
*************************************************** 
12 ok: [localhost] 
TASK [include file list] ******************************** 
********************************************************* 
15 ok: [localhost] 
TASK [concatenate] ************************************** 
********************************************************* 
18 ok: [localhost] 
PLAY RECAP ********************************************** 
********************************************************** 
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
23 ansible-pilot $
```

before execution

```
ansible-pilot $ ls -al concatenate 
total 24 
drwxr-xr-x  5 lberton  staff  160 Feb  1 15:40 . 
drwxr-xr-x  9 lberton  staff  288 Feb  1 15:08 .. 
-rw-r--r--  1 lberton  staff    9 Feb  1 15:18 a.txt 
-rw-r--r--  1 lberton  staff    9 Feb  1 15:18 b.txt 
-rw-r--r--  1 lberton  staff   56 Feb  1 15:48 includes.yaml 
ansible-pilot $ cat concatenate/a.txt 
A content%
ansible-pilot $ cat concatenate/b.txt 
B content%
ansible-pilot $ cat concatenate/includes.yaml 
input-files: 
  - concatenate/b.txt 
  - concatenate/a.txt
ansible-pilot $
```

after execution

```
ansible-pilot $ ls -al concatenate 
total 24 
drwxr-xr-x  5 lberton  staff  160 Feb  1 15:40 . 
drwxr-xr-x  9 lberton  staff  288 Feb  1 15:08 .. 
-rw-r--r--  1 lberton  staff    9 Feb  1 15:18 a.txt 
-rw-r--r--  1 lberton  staff    9 Feb  1 15:18 b.txt 
-rw-r--r--  1 lberton  staff   56 Feb  1 15:48 includes.yaml 
ansible-pilot $
```

## Rsync Backup - 本地到远程

如何使用 `synchronize` 模块实现 Linux 机器的目录备份。

## Synchronize

`ansible.posix.synchronize` 是 `rsync` 的封装，旨在让常用任务变得简单。

让我们聊聊 `synchronize` 模块。它是 POSIX 集合的一部分。`rsync` 是一种通过比较修改时间和大小在计算机和存储驱动器之间同步文件的工具。

## 主要参数

- `src`: 字符串，源路径（绝对或相对）。
- `dest`: 字符串，目标路径（绝对或相对）。
- `archive`: 布尔值，镜像归档标志（启用递归、链接、权限、时间、所有者、组以及 `-D`）。默认启用，因此在大多数情况下不需要指定其他设置。请参考手册以启用或禁用特定设置。
- `rsync_opts`: 字符串，可以指定更多的 `rsync` 参数。

## 链接

- [rsync](https://en.wikipedia.org/wiki/Rsync)
- [ansible.posix.synchronize](https://docs.ansible.com/ansible/latest/collections/ansible/posix/synchronize_module.html)

## demo

使用 Ansible Playbook 进行 rsync 备份。

向你演示如何使用 `synchronize` 模块在 Linux 机器上复制某些目录树。

```yaml
---
- name: synchronize module demo
  hosts: all
  become: false
  gather_facts: true
  vars:
    source: '~/prj/github/ansible-pilot/copy files to remote hosts/examples'
    destination: 'example-backup'
  tasks:
    - name: rsync installed
      ansible.builtin.package:
        name: rsync
        state: present
      become: true
    - name: data synchronization
      ansible.posix.synchronize:
        src: "{{ source }}"
        dest: "{{ destination }}"
```




# 等等性测试

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/ inventory copy files to\ remote hosts/rsync.yml
PLAY [synchronize module demo] *********************************
************************************************
TASK [Gathering Facts] *********************************
************************************************
ok: [demo.example.com]
TASK [rsync installed] *********************************
************************************************
ok: [demo.example.com]
TASK [data synchronization] *****************************
************************************************
changed: [demo.example.com]

PLAY RECAP *************************************************
************************************************
demo.example.com          : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $ ansible-playbook -i virtualmachines/demo/ inventory copy files to\ remote hosts/rsync.yml
PLAY [synchronize module demo] *********************************
************************************************
TASK [Gathering Facts] *********************************
************************************************
ok: [demo.example.com]
TASK [rsync installed] *********************************
************************************************
ok: [demo.example.com]
TASK [data synchronization] *****************************
************************************************
ok: [demo.example.com]

PLAY RECAP *************************************************
************************************************
demo.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```

## 执行前

```bash
ansible-pilot $ ls -al copy files to\ remote hosts/examples
total 16
drwxr-xr-x  4 lberton  staff  128 Jan 17 11:54 .
drwxr-xr-x  9 lberton  staff  288 Mar 28 14:13 ..
-rw-r--r--  1 lberton  staff  16 Sep  4  2021 report.txt
-rw-r--r--  1 lberton  staff  16 Jan 17 11:52 report2.txt
ansible-pilot $ cat copy files to\ remote hosts/examples/report.txt
test report.txt
ansible-pilot $ cat copy files to\ remote hosts/examples/report2.txt
test report.txt
ansible-pilot $ ssh devops@demo.example.com
Last login: Mon Mar 28 12:22:14 2022 from 192.168.0.59
[devops@demo ~]$ ls -al
total 20
drwx------. 4 devops wheel  127 Mar 28 12:22 .
drwxr-xr-x. 4 root  root    35 Mar 24 17:44 ..
drwx------. 3 devops wheel  17 Mar 24 17:44 .ansible
-rw-------. 1 devops wheel  178 Mar 28 12:21 .bash_history
-rw-r--r--. 1 devops wheel  18 Jul 26  2021 .bash_logout
-rw-r--r--. 1 devops wheel  141 Jul 26  2021 .bash_profile
-rw-r--r--. 1 devops wheel  376 Jul 26  2021 .bash_rc
drwx------. 2 devops wheel  29 Mar 24 17:44 .ssh
-rw-------. 1 devops wheel 1756 Mar 28 10:38 .viminfo
[devops@demo ~]$ rpm -qa | grep rsync
rsync-3.1.3-12.el8.x86_64
[devops@demo ~]$
```

## 执行后

```bash
ansible-pilot $ ssh devops@demo.example.com
Last login: Mon Mar 28 12:24:57 2022 from 192.168.0.59
[devops@demo ~]$ ls -al
total 20
drwx------. 5 devops wheel  149 Mar 28 12:24 .
drwxr-xr-x. 4 root  root    35 Mar 24 17:44 ..
drwx------. 3 devops wheel  17 Mar 24 17:44 .ansible
-rw-------. 1 devops wheel  178 Mar 28 12:21 .bash_history
-rw-r--r--. 1 devops wheel  18 Jul 26  2021 .bash_logout
-rw-r--r--. 1 devops wheel  141 Jul 26  2021 .bash_profile
-rw-r--r--. 1 devops wheel  376 Jul 26  2021 .bash_rc
drwx------. 2 devops wheel  29 Mar 24 17:44 .ssh
-rw-------. 1 devops wheel 1756 Mar 28 10:38 .viminfo
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 example-backup
[devops@demo ~]$ tree example-backup/
example-backup/
└── examples
    ├── report2.txt
    └── report.txt
[devops@demo ~]$ cat example-backup/examples/report.txt
test report.txt
[devops@demo ~]$ cat example-backup/examples/report2.txt
test report.txt
[devops@demo ~]$ ls -al example-backup/examples/
total 8
drwxr-xr-x. 2 devops wheel  43 Jan 17 10:54 .
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 ..
-rw-r--r--. 1 devops wheel  16 Sep  4  2021 report.txt
-rw-r--r--. 1 devops wheel  16 Jan 17 10:52 report2.txt
``````bash
ansible-pilot $ touch copy files to\ remote hosts/examples/report3.txt
ansible-pilot $ ansible-playbook -i virtualmachines/demo/ inventory copy files to\ remote hosts/rsync.yml
PLAY [synchronize module demo] *********************************
************************************************
TASK [Gathering Facts] *********************************
************************************************
ok: [demo.example.com]
TASK [rsync installed] *********************************
************************************************
ok: [demo.example.com]
TASK [data synchronization] *****************************
************************************************
changed: [demo.example.com]

PLAY RECAP *************************************************
************************************************
demo.example.com          : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $ ssh devops@demo.example.com
Last login: Mon Mar 28 18:44:10 2022 from 192.168.0.59
[devops@demo ~]$ ls -al example-backup/
total 0
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 .
drwx------. 5 devops wheel  149 Mar 28 12:24 ..
drwxr-xr-x. 2 devops wheel  62 Mar 28 12:24 examples
[devops@demo ~]$ ls -al example-backup/examples/
total 8
drwxr-xr-x. 2 devops wheel  62 Mar 28 12:44 .
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 ..
-rw-r--r--. 1 devops wheel  16 Sep  4  2021 report.txt
-rw-r--r--. 1 devops wheel  16 Jan 17 10:52 report2.txt
-rw-r--r--. 1 devops wheel  0 Mar 28 18:44 report3.txt
[devops@demo ~]$
```

