
# Ansible Linux 文件系统示例

![publisher's logo](img/image-6UFLYC34.png)

## 介绍

本书提供了 Ansible 语言的介绍。Ansible 是一种流行的开源自动化工具。它是免费、可移植且极其易用的。无论你是一个自动化领域的新手，本书的目标都是带你快速进入状态。我们将从一个一个示例开始。

## 关于 Luca Berton

我是 Luca Berton，我们将一起度过很多有趣的时光。首先，让我介绍一下自己。

曾在红帽担任 Ansible 技术支持工程师，常驻捷克，尽管我是意大利人。我担任系统管理员已超过 15 年，处理了本地部署以及主流云提供商的基础。我是开源的热热者，通过在不同的公开活动中分享知识来支持社区。我还是家乡 Linux 用户小组的联合创始人，该小组曾接待自由软件运动创始人理查德·斯托曼。

我认为自己是一个懒人，所以我总是尝试新方法来自动化工作中重复性的任务。在经历了多年的 Perl、Bash 和 Python 脚本编写后，我接触了 Ansible 技术。我通过了认证，并与 Ansible 工程师团队工作了一多年。我认为 Ansible 是目前最好的基础设施自动化技术，它是人类可读的，学习曲线容易，且非常受市场招聘人员青睐。

## 奖项与认可

### 2022

- [Ansible Anwendertffen - 从零到英雄：如何构建 Ansible Pilot 社区 - 作者 Luca Berton (Red Hat CZ) 15:15 - 16:00 2022 年 2 月 15 日](https://www.ansible-anwender.de/post/2022/01/register/)
- [Red Hat Ansible Playbook 包含在 RHSB-2021-009 Log4Shell 远程代码执行 - log4j (CVE-2021-44228) 2022 年 1 月 12 日](https://access.redhat.com/security/vulnerabilities/RHSB-2021-009#diagnose)
- [AWS 设置 sysctl 内核参数 — Ansible 模块 sysctl 2022 年 1 月 12 日](https://awstip.com/set-sysctl-kernel-parameters-ansible-module-sysctl-83fc2b3f77f)
- [Ansible Bullhorn #41 - Ansible 开发者社区通讯报 2022 年 1 月 7 日](https://mailchi.mp/redhat/the-bullhorn-41)

### 2021

- [Ansible Bullhorn #34 - Ansible 开发者社区通讯报 2021 年 9 月 17 日](https://us19.campaign-archive.com/?u=56d874e027110e35dea0e03c1&id=5f02018283)

本课程将持续跟踪 `Ansible` 演进，并在需要时添加更多内容。

你准备好享受其中了吗？

# 带示例的 Ansible 入门教程

在本章中，你将发现 Ansible 的基础、架构和术语。

## 什么是 Ansible

在本章中，我将向你解释什么是 Ansible，以及为什么它对你的 IT 部门如此强大。

### Ansible

- 基础设施自动化工具
- 开源基础设施即代码 (Infrastructure as code)

首先，让我们从名为 `Ansible` 的卓越开源技术开始我们的冒险吧。它被归类为基础设施自动化工具，因此你可以轻松地自动化你的系统管理员任务。基础设施即代码是通过机器可读的定义文件来管理和配置计算机数据中心的过程，而不是物理硬件配置或交互式配置工具。`Ansible` 遵循 DevOps 原则。通过 `Ansible`，你可以在本地以及最知名的公共云提供商上部署你的基础设施即代码。

## Ansible 的三个用例

- 部署 (Provision)
- 配置管理 (Config management)
- 应用部署 (Application deployment)

`Ansible` 的三个主要用例是部署、配置管理和应用部署。但在接触这项技术后，我确定你还能发明出更多使用它的方法！

### 部署 (Provisioning)

设置 IT 基础设施的过程。

让我们开始谈论部署：所有的系统管理员都知道管理一组统一的机器集群有多重要。某些人仍然依赖软件来创建工作站镜像。但这样做有一个缺点，使用镜像技术你只是获取了机器在某一个时间点的快照。因此，每当你因为现代密钥激活系统需要重新安装软件，或者需要手动更新到最新的安全补丁时，`Ansible` 在自动化这一过程非常强大，能够创建一个更顺畅的过程。

### 配置管理 (Configuration management)

将系统和软件维护在预期且一致状态的过程。

第二个关键用例是“配置管理”：以更新且一致的方式维护你的整个机器集群，协调滚动更新并调度停机时间。通过 `Ansible`，你可以验证受托管主机的状态，并对其中一小部分主机采取操作。对于最常用的用例，提供了大量的模块。更不用说检查你的集群是否符合某些国际标准并应用解决方案的常见用例了。

### 应用部署 (Application deployment)

在测试、暂存和生产环境之间发布软件的过程。

`Ansible` 有用的第三个关键用例是应用部署。例如，它可以自动化 Web 程序的持续集成/持续交付（CI/CD）工作流流水。你的 DevOps 团队会非常高兴！

## DevOps 中的 Ansible

`Ansible` 用于在全球范围内应用 DevOps 原则。让我快速总结一下。

DevOps 是一系列结合软件开发 (Dev) 和 IT 操作 (Ops) 的实践。由于 DevOps 旨在成为一种跨功能的工作模式，实践该方法的人使用不同的工具集称为“工具链”，而不是单一的工具。这些工具链预计符合以下一个或多个类别，反映了开发和交付过程的关键方面。这七类分别是：

1. **代码 (Code)**：代码开发和评审、源码管理工具、代码合并。
2. **构建 (Build)**：持续集成工具、构建状态。
3. **测试 (Test)**：能够对业务风险提供快速、及时反馈的持续测试工具。
4. **发布 (Release)**：制品仓库、应用部署前的暂存阶段。
5. **部署 (Deploy)**：变更管理、发布审批、发布自动化。
6. **运维 (Operate)**：基础设施配置和管理、基础设施即代码工具。
7. **监控 (Monitor)**：应用性能监控、终端用户体验。

## Ansible 的四个核心原则

1. **声明式 (Declarative)**：你声明你想要什么，而不是如何实现。
2. **无代理性 (Agentless)**：你不需要安装代理。它利用了 `OpenSSH`。
3. **幂等性 (Idempotent)**：一个操作可以运行多次而不会产生初始操作之外的变化。
4. **社区驱动 (Community driven)**：以集合和角色的形式发布在 `Ansible Galaxy` 中。

`ansible` 的四个核心原则是声明式的、无代理的、幂等的和社区驱动的。“声明式”意味着你可以以非常类似于编程语言的方式使用它，在代码流中应用序列、选择和迭代。“无代理”意味着你不需要在目标机器上安装和更新任何代理，它使用 `SSH` 连接和 `python` 解释器。语言本身是“幂等”的，这意味着代码将检查受托管主机的精确状态。社区驱动意味着以集合和角色的形式发布在 `Ansible Galaxy` 中。通过“声明式”意味着你可以以非常类似于编程语言的方式使用它，在代码流中应用序列、选择和迭代。“无代理”意味着你不需要在目标机器上安装和更新任何代理，它使用 `SSH` 连接和 `python` 解释器。语言本身是“幂等”的，这意味着代码将检查受托管主机的精确状态。社区驱动意味着以集合和角色的形式发布在 `Ansible Galaxy` 中。

## Ansible 的六个价值

- **简单**：`YAML` 可读。
- **强大**：配置管理、工作流编排、应用部署。
- **跨平台**：无代理支持所有操作系统、物理、虚拟、云。
- **与现有工具协作**：统一现有环境。
- **内置组件**：内置了 750 多个模块。
- **社区驱动**：每月下载 25 万，3500 名贡献者，1200 名 IRC 用户。

现在让我们来谈谈 `Ansible` 的六个价值。第一个是简单：代码使用 `YAML` 语言编写，这是一种人类可读的数据序列化语言。它广为人知且易于学习，通常用于存储或传输数据的应用程序。`Ansible` 是强大的：它在配置管理、工作流编排、应用部署方面经过了测试。第三个价值是天然跨平台：无代理支持所有主流操作系统、物理、虚拟、云和网络`Ansible` 的另一个价值是它可以与现有工具协作，轻松地统一现有环境。“内置组件”意味着 `Ansible` 内置了 750 多个模块来自动化最常见的任务。最后一个价值是 `Ansible` 是社区驱动的：每月有 25 万次下载，平均 3500 名贡献者，IRC 上有 1200 名用户。

## Ansible 历史

- **2012**：由 Michael DeHaan 开发
- **2015**：被 Red Hat 收购
- **2016**：AnsibleFest 活动
- **2020**：Red Hat Ansible 自动化平台 1.0
- **2021**：Red Hat Ansible 自动化平台 2.1

Ansible 历史的主要事件如下。

`Ansible` 的第一个版本发布于 2012 年 2 月 20 日。`Ansible` 工具由 Michael DeHaan 开发。`Ansible Inc.`（原名为 `AnsibleWorks Inc.`）是为了商业化支持和赞助该项目而成立的公司。

2015 年 10 月 16 日，红帽（Red Hat）收购了 Ansible Inc，并将 Ansible 评估为一种“强大的 IT 自动化解决方案”，旨在帮助企业实现无缝 IT 化。

AnsibleFest 是自 2016 年以来在伦敦和美国举办的 Ansible 用户及贡献者社区年度会议。

# Ansible、Ansible Tower 与 Ansible Automation Platform

### Ansible

一个社区驱动的项目，创新迭代快，开源的，但仅提供命令行工具。

### Red Hat Ansible Tower / Ansible Automation Platform

这是一个由红帽设计的框架。它提供了一个 Web UI，用于管理您的基础架构。

Ansible 是一个社区驱动的项目，创新迭代快，开源，但仅提供命令行工具。

企业级需要更多的服务和一些稳定版本。例如，它们需要支持方面的 SLA（服务水平协议）。红帽在 Ansible Tower 伞下为公司提供此类服务，该服务现已重命名为 Ansible Automation Platform。

Ansible Tower 是一个 REST API、Web 服务和基于 Web 的控制台，旨在让不同技术水平和技能的 IT 团队成员更方便地使用 Ansible。它是自动化任务的枢纽。该 Tower 是红帽公司支持的商业产品，但源自 AWX 上游项目，该项目自 2017 年 9 月起开源。

红帽还维护着 Ansible Engine。通过 Ansible Engine，组织可以以加固的企业级方式访问底层 Ansible 技术提供的工具和创新。Ansible Engine 由红帽开发，明确意图作为企业 IT 平台使用。

# 入门

在本章节中，我将向你解释如何开启 Ansible 技术之旅、如何连接到受管主机以及如何使用命令行执行一些简单任务。

# Ansible 架构

让我们开始谈论 Ansible 架构。实际安装 Ansible 的节点被称为“控制节点”（control node），它管理你所有的节点集群。另一方面，被管理的节点被称为“受管节点”（managed node）。目标节点可以是 Linux、Mac、Windows 以及多种网络设备。每个目标都有某些特性，例如不同的 Linux 发行版和模块用法。我们将在接下来的章节中讨论这些特性。

# 与受管节点的连接

“控制节点”与“受管节点”之间的连接通过 SSH 协议管理，不需要在目标机器上安装特定的客户端。竞争对手需要通常被称为“代理”（agent）的客户端软件。通过 SSH 连接，唯一的要求是访问目标机器的用户名和证书。还有一些方法可以自动化这第一个脚本步骤。在完成 SSH 连接后，另一个要求是 `python` 解释器，它是现代操作系统中自带的。默认情况下，Ansible 使用 SFTP 传输文件，但你可以在配置中切换到 SCP。Windows 目标可以使用 WinRM 技术连接，并使用 PowerShell 作为解释器。

# 创建基础清单

`/etc/ansible/hosts`

```
host1.example.com
```

默认清单文件 `/etc/ansible/hosts`。

`host1.example.com` 是一个受管主机。

受管主机列表存储在 `/etc/ansible/hosts` 中。在本示例中，它只包含一个名为 `host1.example.com` 的主机。

# 运行你的第一个 Ansible 命令

```text
$ ansible all -m ping
2 host1.example.org | SUCCESS => {
3     "ansible_facts": {
4         "discovered_interpreter_python": "/usr/bin/python"
5     },
6     "changed": false,
7     "ping": "pong"
8 }
```

`ping` 模块在 `all` 主机上执行。

`host1.example.com` 回了成功代码。

现在我们准备好运行你的第一个 Ansible 命令了。Ansible 命令在 Ansible 术语中被称为“模块”（module）。第一行在所有主机上执行了 Ansible `ping` 模块。响应是 pong。请注意，这意味着 Ansible 能够通过 SSH 用户名连接，使用公钥识别身份并执行本地 python 执行器。因此，它与网络中的任何 ping 完全不同。

# 在 Ansible 上运行即时命令

```text
$ ansible all -a “/bin/echo hello”
2 host1.example.org | CHANGED | rc=0 >>
3 hello
```

`/bin/echo hello` 命令在 `all` 主机上执行。

`host1.example.com` 回了变更代码并在标准输出上打印了 `hello`。

Ansible 还可以在目标主机上执行某些命令并在“控制节点”的控制台上报告状态。在本示例中，`/bin/echo hello` 命令在 `all` 主机上执行。`host1.example.com` 回了变更代码并在标准输出上打印了 `hello`。请注意，每当你在远程机器上运行命令时，你都会收到“changed”（变更）状态。

# 在 Ansible 上运行带权限提升的即时命令

```text
$ ansible all -m ping -u devops --become
2 host1.example.org | SUCCESS => {
3     "ansible_facts": {
4         "discovered_interpreter_python": "/usr/bin/python"
5     },
6     "changed": false,
7     "ping": "pong"
8 }
```

在以 `devops` 用户登录后，以 `root` 用户身份在 `all` 主机上执行 `ping` 模块。

`host1.example.com` 回了变更代码并在标准输出上打印了 `hello`。

在本示例中，我在以 `devops` 用户登录后，以 `root` 用户身份对 `all` 主机运行 `ping` 模块。`host1.example.com` 回了变更代码并在标准输出上打印了 `hello`。

## 总结

在本模块中我们学习了 Ansible 架构的基础概念、如何编写受管主机列表以及如何对其执行某些命令。

# 清单

在本章节中，我将向你解释什么是清单、为什么需要它以及不同类型的使用方法。

由 Ansible 管理的多主机列表被称为清单（inventory）。它从根本上是节点或主机的集合，使用组或模式进行选择。

## `all` 关键字

特殊关键字 `all` 表示清单中的所有主机。它在后续课程中将非常有用。例外是你需要指定的 `localhost`。

## 简单的 INI 清单

`./ini_simple_inventory`

```
host1.example.com

[webservers]
two.example.com
three.example.com
```

文件名 `ini_simple_inventory`。

`host1.example.com` 未分组。

最简单的清单类型是 INI 清单，取决于文件类型。默认位置是 `/etc/ansible/hosts`，但你可以通过 `-i` 参数自定义。在本示例中，主机 `host1.example.com` 未分组，`two.example.com` 和 `three.example.com` 被组为 `webserver`。

## 简单的 YAML 清单

`simple_yaml_inventory.yml`

```yaml
---
all:
  hosts:
    one.example.com:
  children:
    webservers:
      hosts:
        two.example.com:
        three.example.com
```

文件名 `inventory.yml`。

`one.example.com` 未分组。



`two.example.com` 和 `three.example.com` 被组为 `webserver`。

你可以使用 YAML 语法表达相同的清单。在本示例中，与 INI 示例相同。

## 添加主机范围

`./ini_range_inventory`

```
[webservers]
www[01:99].example.com

[databases]
db-[a-f].example.com
```

`webservers` 组包含从 `www01.example.com` 到 `www99.example.com` 的所有主机。

`databases` 组包含从 `db-a.example.com` 到 `db-f.example.com` 的所有主机。

组成员也可以使用数字或字母范围来定义。在数字范围内，你还可以指定一个步长（stride），即数字序列之间的增量。在这个 INI 示例中，`webservers` 组包含了从 `www01.example.com` 到 `www99.example.com` 的所有主机。`databases` 组包含了从 `db-a.example.com` 到 `db-f.example.com` 的所有主机。

## 多个组中的主机

`./ini_groupsmultiple_inventory`

```ini
1 one.example.com 2 3 [webservers] 4 two.example.com 5 three.example.com 6 7 [prod] 8 two.example.com 9 10 [dev] 11 three.example.com
```

主机 `two.example.com` 和 `three.example.com` 存在于多个组中。

主机可以存在于多个组。在这个 INI 示例中，主机 `two.example.com` 和 `three.example.com` 被分在 `webserver` 中。`two.example.com` 于 `webserver` 组同时也于 `prod` 组。

`three.example.com` 存在于 `webserver` 和 `dev` 组。

## 主机变量

`./ini_host_inventory`

```ini
1 [webservers] 2 localhost ansible_connection=local 3 one.example.com ansible_connection=ssh ansible_user=devops 4 two.example.com ansible_connection=ssh ansible_user=ansible\ 5 le
```

对 `ansible_connection` 和 `ansible_user` 变量进行自定义。

在清单中，你可能想要存储与特定主机或组相关的变量值。这种场景很常见，因为它定义了与不同主机不同的连接。例如，对 `localhost` 使用 `local` 连接，对所有其他主机使用默认的 `ssh` 连接。对于每个主机，你还可以自定义登录用户：`one.example.com` 使用 `devops`，`two.example.com` 使用 `ansible`。

## 组变量

`./ini_groupsvariables_inventory`

```ini
1 [webservers] 2 one.example.com 3 two.example.com 4 5 [webservers:vars] 6 ntp_server=europe.pool.ntp.org
```

`./inventory.yml`

```yaml
1 --- 2 webservers: 3   hosts: 4     two.example.com: 5     three.example.com: 6   vars: 7     ntp_server: europe.pool.ntp.org
```

正如单主机一样，也可以定义组变量。在示例的这两个清单文件（INI 和 YAML 格式）中，变量 `ntp_server` 为该组的所有主机被分配了值 `europe.pool.ntp.org`。

## 变量变量值的继承

`./ini_variableinheriting_inventory`

```ini
1 [asia] 2 host1.example.com 3 4 [europe] 5 host2.example.com 6 7 [webserver:children] 8 asia 9 europe 10 11 [webservers:vars] 12 ntp_server=europe.pool.ntp.org
```

`./variableinheriting_inventory.yml`

```yaml
1 --- 2 children: 3   webservers: 4     children: 5       asia: 6         hosts: 7           host1.example.com: 8       europe: 9         hosts: 10           host2.example.com: 11     vars: 12       ntp_server: europe.pool.ntp.org
```

主机和组可以组合在一起。在这个示例中，`webserver` 组有两个成员 `asia` 和 `europe`。这两个元素分别被定义为单个主机 `host1.example.com` 和 `host2.example.com`，但也可以包含更多主机。`ntp_server` 变量定义在 `webservers` 级别。因此最后 `ntp_server` 变量对 `webserver`、`asia` 和 `europe` 组可用。`ntp_server` 变量在 `host1.example.com` 和 `host2.example.com` 主机同样可用。

## 使用多个清单源

```bash
$ ansible-playbook playbook.yml -i production -i development
```

针对 `production` 和 `development` 执行名为 `playbook.yml` 的 ansible playbook。

在每次执行时可以使用多个清单文件。在这个示例中，将针对 `production` 和 `development` 清单执行名为 `playbook.yml` 的 ansible playbook。

## localhost 清单

`./ini_local_inventory`

```ini
1 localhost ansible_connection="local"
```

文件名：`inventory`

默认路径：`/etc/ansible/hosts`

清单中的一个特殊情况是 `localhost`。你需要指定连接类型为 `local`，否则 Ansible 将假定使用默认的 SSH 连接。

## 总结

现在你对 Ansible INI 和 YAML 清单文件、主机和组变量有了更多的了解。

## Playbook

在本章中，我将向你解释什么是 Ansible Playbook 以及你为什么需要它。我们将涵盖如何从一个简单的 playbook 开始，从基础语法到操作。

## YAML 语法

在本章中，我将向你解释什么是 Ansible Playbook 以及你为什么需要它。我们将涵盖如何从一个简单的 playbook 开始，从基础语法到操作。

YAML 是一种易读易写的数据序列化语言。它用于 Ansible playbook 和清单文件。

YAML 使用了几种数据类型：

- 键值对 (Key-value pairs)
- 列表 (Lists)
- 标量 (Scalars)
- 字典 (Dictionaries)

YAML 文件的示例：

```yaml
- name: My first playbook
  hosts: all
  tasks:
    - name: Print message
      debug:
        msg: "Hello World"
```

YAML 对缩进敏感，这意味着使用一致的空格数很重要。

## helloworld.yml

```yaml
---
- name: My first playbook
  hosts: all
  tasks:
    - name: Print message
      debug:
        msg: "Hello World!"
```

这是执行 `helloworld.yml` 的输出。我想让你注意，使用的命令是 `ansible-playbook`。第一个参数是清单文件，第二个是 playbook。

`helloworld_debug.yml`

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

1. 文件名：`helloworld_debug.yml`
2. Playbook 的名称
3. 执行主机
4. 任务列表
5. 一个名为“Hello message”的任务
6. `debug` 模块
7. `debug` 模块的参数 `msg`
8. 参数 `varbosity`（此处原文误）为“2”

此提示允许你将调试代码保留在 playbook 中，并仅在需要时启用执行。例如，只有在调用 Ansible 且指定输出级别为二时，才会打印消息。

## helloworld_debug.yml - 执行 - 部分 1

```bash
1 ansible-playbook -i inventory helloworld_debug.yml
2 PLAY [Hello World sample] *******************************\
3 *********************************************************\
4 ***********
5
6 TASK [Gathering Facts] **********************************\
7 *********************************************************\
8 ********
9 ok: [host1.example.com]
10
11 TASK [Hello message] ************************************\
12 *********************************************************\
13 ******
14 skipping: [host1.example.com]
15
16 PLAY RECAP **********************************************
17 *****************************************************
18 host1.example.com      : ok=1    changed=0    unreachable
19 e=0    failed=0    skipped=1    rescued=0    ignored=0
```

这是 `helloworld_debug.yml` 在正常执行（即非调试模式）时的输出。如你所见，hello 消息被跳过了。

## helloworld_debug.yml - 执行 - 部分 2

```bash
1 $ ansible-playbook -i inventory -vv helloworld_debug.yml
2 PLAY [Hello World sample] *******************************\
3 *********************************************************\
4 ***********
5 TASK [Gathering Facts] **********************************\
6 *********************************************************\
7 ********
8 ok: [host1.example.com]
9 TASK [Hello message] ************************************\
10 *********************************************************\
11 ******
12 ok: [host1.example.com] => {
13     "msg": "Hello World!"
14 }
15 PLAY RECAP **********************************************
16 *****************************************************
17 host1.example.com      : ok=2    changed=0    unreachable
18 e=0    failed=0    skipped=1    rescued=0    ignored=0
```

这是 `helloworld_debug.yml` 在调试级别二模式下执行时的输出，请注意命令行中的两个“V”。如你所见，hello 消息被打印了。

## 等幂性 (Idempotency)

1 等幂性
2 模块检查期望的最终状态是否已实现，否则执行

大多数 Ansible 模块的一个重要特性是“等幂性”的。这意味着在目标节点上执行任何操作之前，模块将检查实际状态。如果实际状态与预期状态匹配，则将不执行任何操作。如果当前状态偏离预期状态，则将发生操作。请注意，如果你再次执行该 playbook，将发现期望状态已存在，且不会执行进一步的操作。这一属性被称为“等幂性”，你应该充分利用它。

## multipleplays.yml

```yaml
1 ---
2 - name: first play
3   hosts: web.example.com
4   tasks:
5     - name: first task
6       ansible.builtin.yum:
         name: httpd
         status: present
7     - name: second task
8       ansible.builtin.service:
         name: httpd
         enabled: true
9 - name: second play
10  hosts: database.example.com
11  tasks:
12    - name: first task
13       ansible.builtin.service:
         name: mariadb
         enabled: true
```

文件名：`multipleplays.yml`

内部包含两个针对 `web.example.com` 和 `database.example.com` 执行的 play。

`multipleplays.yml` playbook 包含两个 play。第一个 play 在 `web.example.com` 主机上执行，安装 apache Web 服务器并设置开机自启。第二个 play 将在 `database.example.com` 上执行并设置开机自启。

## privilegeescalation.yml

```yaml
1 ---
2 - name: install httpd
3   hosts: web.example.com
4   become: true
5   become_method: sudo
6   become_user: root
7   tasks:
8     - name: first task
9       ansible.builtin.yum:
         name: httpd
         status: present
```

`privilegeescalation.yml`

`become` 指定必要的权限

`become_method` 指定方法

`become_user` 指定 root 用户

## 最常用的 Ansible 模块

文件模块 (Files modules)

`copy`: 将本地文件复制到托管主机

`fetch`: 从远程节点复制文件到本地

`file`: 设置权限和其他属性

`lineinfile`: 确保文件中存在某特定行

`synchronize`: 使用 `rsync` 同步内容

软件包模块 (Software package modules)

`package`: 管理操作系统原生软件包

`yum`: 使用 YUM 管理软件包

`apt`: 使用 APT 管理软件包

`dnf`: 使用 DNF 管理软件包

`gem`: 管理 Ruby 包

`pip`: 管理 Python 包

系统模块 (System modules)

`firewalld`: 管理任意端口和服务

`reboot`: 重启机器

`service`: 管理服务

`user`: 添加、删除和管理用户账户

网络工具模块 (Net tools modules)

`get_url`: 通过 HTTP、HTTPS 和 FTP 下载文件

`nmcli`: 管理网络

`uri`: 与 Web 服务交互

## 总结 (Recap)

在本模块中为后续操作奠定了基础。继续努力，很快就能自动化所有的系统任务。

## 变量 (Variables)



在本章中，我将为你解释什么是变量、为什么需要它们、不同类型以及如何使用它们。

## 变量为给环境存储动态值

在你的 Playbook 中，使用变量存储所有需要的动态值是一个良好的实践。通过编辑变量，你可以在未来复用代码，只需对业务需求进行参数化。

`variableprint.yml` playbook 与 `helloworlds.yml` playbook 类似。它们的语法和元素结构非常相似，区别在于存在变量 `fruit`。变量存储信息，如字符串、数字以及更复杂的数据结构（如列表、字典等）。在这种情况下，变量名为 `fruit`，值为 `apple`。在此案例中，`debug` 模块将文本 `Print the value of variable` 与变量 `fruit` 的值进行拼接。请注意双括号，它表示变量的值。一种最佳实践是始终在代码中的双引号内包含双括号。

### `variableprint.yml` - 执行

```text
1 $ ansible-playbook -i inventory variableprint.yml
2 PLAY [Variable print sample] ****************************\
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
15 PLAY RECAP **********************************************
16 ***********************
17 host1.example.com  : ok=2    changed=0    unreachable=0  \
18 failed=0    skipped=0    rescued=0    ignored=0
```

`variableprint.yml` 的执行输出与 `helloworld.yml` 文件的输出非常相似。请注意通过组合字符串与变量值而得到的消息 `Print the value of variable apple`。此外，正如执行摘要（play recap）区域和绿色所示，此执行是成功的。有两个任务正在执行。

### `variableprint.yml` - 额外变量

```text
1 $ ansible-playbook -i inventory -e fruit=banana variabl\
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
16 PLAY RECAP **********************************************
17 ***********************
18 host1.example.com  : ok=2    changed=0    unreachable=0  \
19 failed=0    skipped=0    rescued=0    ignored=0
```

你可以通过从命令行指定值来覆盖 playbook 变量。在命令行上设置的变量被称为额外变量（extra variables）。

`variableprint.yml` 的执行输出与之前的相似。请注意通过组合字符串与变量值而得到的消息 `Print the value of variable banana`。从命令行传递的值会覆盖任何 playbook 的值。

## 主机变量与组变量

### `inventory_host_variables`

```text
1 [servers]
2 host1.example.com ansible_user=devops
```

### `inventory_group_variables`

```text
1 [servers]
2 host1.example.com
3 host2.example.com
4
5 [servers:vars]
6 user=alice
```

主机变量和组变量可以定义在清单文件中。在左列中，你可以看到主机变量的示例。变量 `ansible_user` 被赋值为 `devops`。该主机变量适用于 `host1.example.com`。在右列中，你看到组变量的示例。变量 `user` 被赋值为 `alice`。该组变量将适用于 `host1.example.com` 和 `host2.example.com`，且值相同。

### `inventory_host_dir`

```text
1 [servers]
2 host1.example.com
```

### `host_vars/demo1.example.com`

```text
1 ansible_user=devops
```

### `inventory_group_dir`

```text
1 [servers]
2 host1.example.com
3 host2.example.com
```

### `group_vars/servers`

```text
1 user=alice
```

你也可以使用目录来填充主机和组变量以达到相同的结果。如你所见，结果将与之前的幻灯片相同，但使用了更多的文件。在左列中，你可以看到主机变量的示例。变量 `ansible_user` 被赋值为 `devops`。该主机变量适用于 `host1.example.com`。在右列中，你看到组变量的示例。变量 `user` 被赋值为 `alice`。该组变量将适用于 `host1.example.com` 和 `host2.example.com`，且值相同。

## 数组变量

### `array.yml`

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

`1 file name: array.yml 2 用户按层级结构组织。 3 4 返回 'Alice' 5 users.alice 6 返回 'Alice'`

数组（Array）是一种非常有用的数据结构。你可以按层级结构组织信息。在示例中，用户 alice 和 bob 的列表易易读。每个元素都有一些属性：firstname 和 homedir。

### `array.yml` - 执行

```text
1 $ ansible-playbook -i inventory array.yml
2 PLAY [Array sample] *********************************\
3 *************************************************\
4 *****
5 TASK [Gathering Facts] **********************************\
6 *************************************************\
7 *********
8 ok: [host1.example.com]
9 TASK [Print Alice's firstname] **************************\
10 *************************************************\
11 *ok: [host1.example.com] => {
12     "msg": "Print Alice's firstname: Alice"
13 }
14 PLAY RECAP **********************************************
15 *************************************
16 1.example.com  : ok=2    changed=0    unreachable\
17 able=0    failed=0    skipped=0    ignored=0
```

`array.yml` 的执行输出与之前的相似。你可以注意到输出 `Print Alice’s firstname: Alice`。Ansible 访问了数组变量的值并如预期显示在输出中。

## 注册变量

### `registeredvariables.yml`

```yaml
1 ---
2 - name: Installs a package and prints the result
3   hosts: all
4   become: true
5   tasks:
6     - name: Install the package
7       ansible.builtin.yum:
8         name: wget
9         state: installed
10        register: install_result
11
12    - name: debug
13      ansible.builtin.debug:
14        var: install_result
```

`1 file name: registeredvariables.yml 2 将标准输出存储在变量 install_result 中 4 也可以被打印`

另一种非常有用的数据结构是注册变量。你可以将任何命令的输出保存到注册变量中。在本示例中，它将打印在屏幕上。

```bash
$ ansible-playbook -i inventory registeredvariables.yml
PLAY [Installs a package and prints the result] *********
TASK [Gathering Facts] *********************************
ok: [host1.example.com]
TASK [Install the package] *****************************
ok: [host1.example.com]
TASK [debug] ************************************
ok: [host1.example.com] => {
    "install_result": {
        "changed": false,
        "failed": false,
        "msg": "Nothing to do",
        "rc": 0,
        "results": []
    }
}
PLAY RECAP *********************************************
host1.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

这是 `registeredvariables.yml` 执行后的输出，符合预期。首先，`yum` 模块会检查软件包是否存在，如果缺失则进行安装。设置过程的输出存储在一个注册变量中，并打印在屏幕上。

## 总结

在本模块中，我们探索了 Ansible Playbook 内部变量的使用。你现在已经了解了用户定义变量、主机变量、组变量和注册变量等工具。

# Facts 和魔法变量

在本章中，我将为你解释什么是 Ansible facts（事实）和魔法变量（magic variables），你为什么需要它们，它们的不同类型，以及如何在日常工作中编辑和使用它们。

## Ansible Facts

facts 是与远程主机相关的变量。

与远程系统相关的变量被称为 facts。通过 facts，你可以将一个系统的行为或状态作为其他系统的配置。它们非常强大，因为你可以获取关于当前主机、操作系统、所使用的发行版、IP 地址、网络配置、存储配置等的非常全面的视图。

### 使用临时命令（ad-hoc）列出机器的所有 facts

```bash
$ ansible -m setup hostname
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
        "iso8601_basic": "20181025T12084419754",
        "iso8601_basic_short": "20181025T120844",
        "iso8601_micro": "2018-10-25T12:08:44.10968Z",
        "minute": "08",
        "month": "10",
        "second": "44",
        "time": "12:08:44",
        "tz": "UTC",
        "tz_offset": "+000",
        "weekday": "Thursday",
        "weekday_number": "4",
        "year": "2018"
    },
    "ansible_default_ipv4": {
        "address": "REDACTED",
        "alias": "eth0",
    }
}
```

理解 Ansible facts 的最佳方法是使用此临时临时自行列出它们。你将对从主机获取的信息量感到惊讶。例如当前的硬件配置：架构、处理器、内存（ram）、可用内存、存储配置等。还有关于软件配置的更多信息：操作系统、所使用的发行版、IP 地址、网络配置、存储配置等。

### 使用 playbook 列出机器的所有 facts

`facts_printall.yml`

```yaml
---
- name: facts_printall
  hosts: all
  tasks:
    - name: Print all facts
      ansible.builtin.debug:
        var: ansible_facts
```

你也可以从 Ansible playbook 中访问相同数量的数据。在这个简单的示例中，你将列出清单中所有主机的 ansible facts。预期结果与之前的临时命令执行结果相同。

### `facts_printall.yml` - 执行



```bash
ansible-playbook -i inventory facts_printall.yml
PLAY [facts_printall] *****************
TASK [Gathering Facts] *********************************
ok: [host1.example.com]
TASK [Print all facts] *********************************
ok: [host1.example.com] => {
    "ansible_facts": {
        "architecture": "x86_64",
        "bios_date": "11/28/2013",
        "bios_version": "4.1.5",
        "cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-3.10.0-862.14.4.el7.x86_64",
            "console": "ttyS0,115200",
            "no_timer_check": true,
            "nofb": true,
            "nomodeset": true,
            "ro": true,
            "root": "LABEL=cloudimg-rootfs",
            "vga": "normal"
        },
        "date_time": {
            "date": "2018-10-25",
            "day": "25",
            "epoch": "1540469324",
            "hour": "12",
            "iso8601": "2018-10-25T12:08:44Z",
            "iso8601_basic": "20181025T12084419754",
            "iso8601_basic_short": "20181025T120844",
            "iso8601_micro": "2018-10-25T12:08:44.10968Z",
            "minute": "08",
            "month": "10",
            "second": "44",
            "time": "12:08:44",
            "tz": "UTC",
            "tz_offset": "+000",
            "weekday": "Thursday",
            "weekday_number": "4",
            "year": "2018"
        },
        "default_ipv4": {
            "address": "REDACTED",
            "alias": "eth0"
        }
    }
}
```

这是`facts_printall.yml`执行后的输出。在执行中，play 是针对`host1.example.com`运行的。输出包含了 Ansible 在`Gathering Facts`任务中自动获取的所有 facts。我鼓励你运行这段代码并熟悉 Ansible Facts。

### 引用一个 fact

`facts_printone.yml`

```yaml
---
- name: facts_printone
  hosts: all
  tasks:
    - name: Print a fact
      ansible.builtin.debug:
        var: "{{ ansible_facts['ansible_architecture'] }}"
```

你可以通过指定 fact 名称来方便地交互。在这个示例中，我们正在列出所有主机的架构。请根据需要自定义代码以匹配 ansible facts。

## 魔法变量

魔法变量是与 Ansible 相关的变量。

与系统相关的变量被称为 facts。通过 facts，你可以将一个系统的行为或状态作为其他系统的配置。

### 常见的魔法变量

- `hostvars`
- `groups`
- `group_names`
- `inventory_hostname`
- `ansible_version`

常见的魔法变量有`hostvars`、`groups`、`group_names`、`inventory_hostname`和`ansible_version`。通过`hostvars`魔法变量，你可以访问为 play 中任何主机定义的变量。当你需要从一个主机访问另一个主机的属性时，这非常有用。`groups`魔法变量列出了清单中所有的组。你可以结合使用`groups`和`hostvars`魔法变量来列出组内所有主机的 IP 地址。`group_names`是主机所属组的列表。`inventory_hostname`魔法变量包含清单中配置的主机名称。`ansible_version`魔法变量包含关于 Ansible 的版本信息。

在本模块中，我们将讨论如何使用`Ansible Vault`以安全的方式存储任何敏感数据，例如密码或 API 密钥。

`Ansible Vault`对变量和文件进行加密以保护敏感内容，并在剧本（playbooks）或角色（roles）中使用。Ansible Vault 以加密方式存储变量和文件，供你在剧本或角色中使用。在 Ansible 的最新版本中，用于保护文件的算法是`AES 256`。

## 创建加密文件

要创建一个新的加密文件，请使用`ansible-vault create filename`命令。该命令会提示输入新的 vault 密码，然后使用默认编辑器打开文件。在示例中使用的密码是`password`，但我强烈建议你使用尽可能安全的密码。

```bash
$ ansible-vault create secret.yml
New Vault password: password
Confirm New Vault password: password
$ ansible-vault create --vault-password-file=vault-password.txt secret1.yml
```

## 查看加密文件

你可以使用`ansible-vault view filename`命令来查看 Ansible Vault 加密的文件，而无需将其打开进行编辑。

```bash
$ ansible-vault view secret1.yml
Vault password: password
INFERNO. I.
Nel mezzo del cammin di nostra vita
mi ritrovai per una selva oscura
ché la diritta via era smarrita.
Ahi quanto a dir qual era è cosa dura
esta selva selvaggia e aspra e forte
che nel pensier rinova la paura!
Tant'è amara che poco è più morte;
ma per trattar del ben ch'i' vi trovai,
dirò de l'altre cose ch'i' v'ho scorte.
```

## 编辑现有加密文件

要编辑现有加密文件，Ansible Vault 提供了`ansible-vault edit filename`命令。该命令将文件解密到临时文件并允许你进行编辑。保存时，它会复制内容并删除临时文件。

```bash
$ ansible-vault edit secret.yml
Vault password: password
```

## 加密现有文件

要对已存在的文件加密，请使用`ansible-vault encrypt filename`命令。`--output`选项可以将加密文件保存为新名称。如果省略此选项，原始文件将被加密后的文件覆盖。

```bash
$ ansible-vault encrypt cleartext1.yml --output=vault1.yml
New Vault password: password
Confirm New Vault password: password
Encryption successful
```

## 解密现有文件

可以使用`ansible-vault decrypt filename`命令对现有加密文件进行永久解密。解密单个文件时，可以使用`--output`选项将解密后的文件保存为不同的名称。

```bash
$ ansible-vault decrypt vault1.yml --output=decrypted.yml
Vault password: password
Decryption successful
```

## 修改加密文件的密码

你可以使用`ansible-vault rekey filename`命令更改加密文件的密码。该命令可以一次更改多个数据文件的密钥。它会提示原始密码，然后是新密码。

```bash
$ ansible-vault rekey secret.yml
Vault password: password1
New Vault password: password
Confirm New Vault password: password
Rekey successful
```

## Playbooks 与 Ansible Vault

要运行访问了 Ansible Vault 加密文件的剧本，你需要为`ansible-playbook`命令提供加密密码。如果你不提供密码，剧本将返回错误。要为剧本提供 vault 密码，请使用`--vault-id`选项。例如，如插图所示，交互式提供 vault 密码请使用`--vault-id @prompt`。或者，你也可以使用密码文件。

```bash
$ ansible-playbook playbook.yml
TASK [include_vars] *************************************
********************************fatal: [localhost]: FAIL
ED! => {"ansible_facts": {}, "ansible_included_var_files": [], "changed": false, "message": "Attempting to decrypt but no vault secrets found"}

$ ansible-playbook --vault-id @prompt playbook.yml
Vault password (default): password

$ ansible-playbook --vault-password-file=vault-password.txt playbook.yml
```

## 总结

在本模块中，我们探索了 Ansible Vault 安全存储，用于在 Ansible 内部保存秘密和机密。正如我们看到的，这些工具是强大的，并且完全集成在 Ansible 技术中。

## 条件

在本模块中，我将向你解释什么是 Ansible 条件操作，以及你如何在日常 Ansible Playbook 中使用它们。

条件语句检查条件并相应地更改程序的行为。

让我们开始吧！为了编写实用的代码，我们几乎总是需要检查条件并相应更改程序行为的能力。条件语句赋予了我们这种能力。Ansible 的形式是`when`语句。Ansible 在条件中使用`Jinja2`测试和过滤器。Ansible 支持所有标准测试和过滤器，并添加了一些独特的。

### 使用“when”的基础条件

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

这是你在 Ansible playbook 中`when`语句的用法用法。任务`reload nginx`只有在`configure_nginx`变量被设置为`true`时才会执行。在这个示例中，我们预计该任务将被跳过。让我们看看输出。

执行：

```bash
$ ansible-playbook -i inventory conditional_basic_false.yml
PLAY [conditional_basic] *************************************
TASK [Gathering Facts] *************************************
ok: [host1.example.com]

TASK [reload nginx] *************************************
skipping: [host1.example.com]

PLAY RECAP *************************************************
host1.example.com    : ok=1  changed=0  unreachable=0  failed=0  skipped=1  ignored=0
```

这是`conditional_basic_false.yml`的输出。在这次执行中，play 针对`host1.example.com`节点。输出以绿色和蓝色显示。你可以看到任务`reload nginx`被 Ansible 读取但根据我们的条件被跳过了。

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

这是你 Ansible playbook 中`when`语句的相同的示例，但我们将变量值从`false`改为了`true`。现在任务`reload nginx`将会被执行，因为`configure_nginx`布尔变量被设置为`true`。让我们看看这段代码执行的输出。

执行：

```bash
$ ansible-playbook -i inventory conditional_basic_true.yml
PLAY [conditional_basic] *************************************
TASK [Gathering Facts] *************************************
ok: [host1.example.com]

TASK [reload nginx] *************************************
ok: [host1.example.com]

PLAY RECAP *************************************************
host1.example.com    : ok=2  changed=0  unreachable=0  failed=0  skipped=0  ignored=0
```

这是`conditional_basic_true.yml`执行的输出。在本次执行中，play 针对`host1.example.com`节点运行。输出以绿色高亮。如你所见，任务`reload ngnx`任务被 Ansible 读取并在我们的条件语句中成功执行。

## 基于 ansible_facts 的条件判断

`conditional_facts.yml`

```yaml
1 ---
2 - name: conditional_facts
3   hosts: all
4   tasks:
5   - name: Shut down Debian-like systems
6     ansible.builtin.command: /sbin/shutdown -t now
7     when: ansible_facts['os_family'] == "Debian"
```

将条件判断与事实（facts）结合起来非常有用。这样你就可以根据单个主机的条件、IP 地址、操作系统、文件系统状态等来调整代码的执行。在这个示例中，如果目标系统是 Debian 类系统（即 Debian 和 Ubuntu 管理的主机），我们将执行关机。

### 执行：



```bash
$ ansible-playbook -i inventory conditional_facts.yml
PLAY [conditional_facts] ********************************
*********************************************************
**********
TASK [Gathering Facts] *********************************
*********************************************************
********
ok: [host1.example.com]
TASK [Shut down Debian-like systems] ********************
*********************************************************
**********************
skipping: [host1.example.com]
PLAY RECAP **********************************************
*****************************************************
host1.example.com                  : ok=1    changed=0
unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

这是`conditional_facts.yml`执行的输出。在本次执行中，play 针对`host1.example.com`节点运行。目标主机不是 Debian 类系统，因为你可以注意到名为`Shut down Debian-like systems`的任务处于`skipped`跳过状态。

# 总结

条件判断非常重要，因为它们允许我们创建响应某些事件、条件或 Ansible Facts 的 Ansible Playbook。这些语句是智能 Ansible Playbook 的基础。

# 循环

在本章中，我向你解释什么是 Ansible 循环操作，以及你如何在日常的 Ansible Playbook 中使用它们。

## 1 循环自动化重复任务

计算机在自动化重复任务方面非常出色。在不产生错误的情况下重复相同或相似的任务是计算机擅长而人类不擅长的。

一组语句的重复执行被称为迭代。Ansible 有几个用于迭代的语句——`loop`语句和`with_items`语句。`with`语句依赖插件。

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

简单的循环会对列表中的项对任务进行迭代。`loop`语句被添加到任务中，并以任务应迭代的项列表作为值。循环变量`item`在每次迭代期间遍历当前值。

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

循环列表不需要是简单值的列表。在接下来的示例中，列表中的每个项实际上是一个哈希（hash）或字典（dictionary）。示例中的每个哈希或字典都有两个键：`name`和`groups`，当前项循环变量中每个键的值可以分别通过`item.name`和`item.group`变量获取。

# with_* 语句

## `with_items`

类似于用于简单列表的`loop`、字符串列表或哈希/字典列表。

## 如果提供了列表列表，则将其扁平为列表

## `with_file`

此关键字需要一个控制节点文件名列表。循环变量`item`持有文件内容。

## `with_sequence`

需要参数根据数值序列生成值列表。

# `loop_with_items.yml`

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
    with_items: data
```

在`loop_with_items.yml`playbook 中，`data`是一个字符串列表。

# 总结

条件判断非常重要，因为它们允许我们创建响应某些事件、条件或 Ansible Facts 的 Ansible Playbook。

# Handler

在本章中，我向你解释什么是 Ansible 循环操作以及你如何在日常的 Ansible Playbook 中使用它们。

## 在变化时运行 Handler

Handler 非常重要，因为它们允许在必要时执行某些步骤。

# `rollingupdate.yml`

```yaml
---
- name: Rolling update
  hosts: all
  become: true
  tasks:
  - name: latest httpd package is installed
    ansible.builtin.yum:
      name: httpd
      state: latest
  handlers:
  - name: restart apache
    ansible.builtin.service:
      name: httpd
      state: restarted
```

`rollingupdate.yml`由一个任务和一个 handler 组成。handler 代码在必要时执行。请注意`notify`语句提到的 handler 名称。

# Role

Role 实现 Ansible 代码复用

Role 类似于传统编程中的函数。使用 Ansible role 可以快速开发 playbook 并复用代码。

# Role 树目录结构

```text
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

`defaults`目录下的`main.yml`文件包含角色变量的默认值，可以在使用 role 时进行覆盖。这些变量的优先级较低，旨在在 play 中更改和自定义。

`files`此目录包含 role 任务引用的静态文件。

`handlers`目录下的`main.yml`文件包含 role 的 handler 定义。

`meta`目录下的`main.yml`文件包含关于 role 信息，包括作者、许可、平台和可选的 role 依赖。

`tasks`目录下的`main.yml`文件包含 role 的任务定义。

`templates`此目录包含 role 任务引用的 Jinja2 模板。

`tests`此目录可以包含一个用于测试 role 的 inventory 和`test.yml`playbook。

`vars`的`main.yml`文件定义了 role 的变量值。通常这些变量用于 role 内部。这些变量的优先级较高，在 playbook 中中使用时不打算更改。

并不是每个角色都包含所有这些目录。

# 在 playbook 中使用 Ansible 角色

`./role_simple.yml`

```yaml
---
- name: role example
  hosts: all
  roles:
    - role1
    - role2
```

1 个文件：`role_simple.yml`将`role1`和`role2`应用到所有`all`托管的主机。

`./role_vars.yml`

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

1 个文件：`role_vars.yml`将`role1`和`role2`应用到所有`all`托管的主机。`Role2`有两个变量参数。

# 执行顺序

`./role_vars.yml`

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

对于 playbook 中的每个 play，任务将按照`tasks`列表中的顺序执行。在所有任务执行后，任何被通知的处理器都将执行。

当一个角色被添加到 play 中时，角色的任务会被添加到`tasks`列表的开头。如果 play 中包含了第二个角色，则其任务列表将添加到第一个角色之后。

角色处理器添加到 play 中的方式与角色的任务添加到 play 中的方式相同。每个 play 均定义了一个`handlers`列表。角色处理器首先被添加到`handlers`列表，然后是任何在 play 的`handlers`章节中定义的句柄。在某些场景下，可能需要在执行角色之前执行某些 play 任务。为了支持此类场景，可以为 play 配置`pre_tasks`部分。在该部分中列出的任何任务都会在角色执行之前执行。如果这些任务中的任何一个通知了处理器，则这些处理器任务将在角色或普通任务之前执行。

play 还支持`post_tasks`关键字。这些任务在 play 的普通任务以及它们通知的任何处理器执行后运行。

# Ansible Galaxy

[`galaxy.ansible.com/`](https://galaxy.ansible.com/)

## 手动从 Ansible Galaxy 安装角色

```bash
$ ansible-galaxy install geerlingguy.redis -p roles/
```

## 从 Ansible Galaxy 的 requirements.yml 安装角色

`./requirements.yml`

```yaml
- src: geerlingguy.redis
  version: "1.5.0"
```

```bash
$ ansible-galaxy install -r roles/requirements.yml -p roles
```

# Ansible 最佳实践

遵循 Ansible 最佳实践可以让你你的代码成功执行，简化故障排除，并对你的自动化之旅产生积极影响。

## 使用空格

在你的 YAML 代码中使用空格而不是制表符（tabs）。在每个块或任务之前添加新行可以让 playbook 变得易于读。

例如：

错误

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

正确

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

## 为每一步分配一个“名称”（name）

为你的代码中的每个 Ansible 语句（Ansible Plays、Tasks、Blocks）始终设置`name`参数。

例如：

错误

```yaml
---
- hosts: all
  tasks:
    - ansible.builtin.yum:
        name: httpd
        state: latest
```

正确

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

## 为变量使用人类可读且有意义的名称

变量对于存储参数或保存之前任务的结果非常重要。使用人类可读且有意义的名称可以增加你团队之间的代码复用和可读性。使用`ansible-playbook`命令的`extra-vars`参数来覆盖变量也很容易。

例如：

错误

```yaml
keepalive: 25
po: 80
aaaa: 8080
```

正确

```yaml
apache_max_keepalive: 25
apache_port: 80
```

## 使用原生 YAML

原生 YAML 的使用提高了代码的可读性，并让你更快更快地发现错误。同时也允许使用某些 YAML 校验器和解析器进行验证。

例如：

错误

```yaml
- name: install apache
  ansible.builtin.yum: name={{ apache_version }} state=present update_cache=yes disable_gpg_check=yes enablepo=apache
  notify: restart
```

正确

```yaml
- name: install apache
  ansible.builtin.yum:
    name: {{ apache_version }}
    state: present
    update_cache: yes
    disable_gpg_check: yes
    enablepo: apache
  notify: restart
```

## 使用原生模块

始终优先使用原生模块而不是命令。`command`、`shell`和`script`应该作为最后的手段。

例如：

错误

```yaml
- name: Add repository into.d list
  become: true
  ansible.builtin.shell: 'echo -e "[google-chrome]\nname=google-chrome\nbaseurl=http://dl.google.com/linux/rpm/stable/x86_64\nenabled=1\ngpgcheck=1\ngpgkey=https://dl.google.com/linux/linux/key.pub" > /etc/yum.repos.d/google-chrome.repo'
  when: ansible_os_family == 'RedHat'
```



```yaml
- name: Add repository into.d list
  ansible.builtin.yum_repository:
    name: google-chrome
    description: google-chrome repository
    baseurl: http://dl.google.com/linux/rpm/stable/x86_64
    enabled: true
    gpgcheck: true
    gpgkey: https://dl.google.com/linux/linux/key.pub
```

### 配置调试消息

在开发 Ansible 代码时，依靠 `debug` 任务来显示变量的内容非常有用。然而，在生产环境中这可能被认为信息量太大。将 `verbosity` 参数设置为 `2` 可以让你只在需要时看到这些消息。

例如：

错误

```yaml
- name: message output
  ansible.builtin.debug:
    msg: "This text always displays"
```

正确

```yaml
- name: message output
  ansible.builtin.debug:
    msg: "This text displays with ansible-playbook -vv"
  verbosity: 2
```

### 以尽可能少的权限执行任务

这是对于以尽可能少的权限执行任务的安全实践通用建议。在 Ansible 中，你可以在任务级别指定 `become: true`，而不是针对整个 playbook，如果并不是所有任务都需要以 root/管理员用户身份执行。

例如：

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

正确

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

许多模块具有带有默认值的可选 `state` 参数。

对于“state”（状态），默认值在不同模块之间可能会有所不同，某些模块支持多个“state”设置。显式地设置 `state: present` 或 `state: absent` 可以让情节（playbooks）和角色（roles）更加清晰。

## 使用注释

添加注释（以“#”开头的行），帮助他人（可能也未来的你自己）理解一个语句、 playbook 或任务（或变量设置）的作用、如何实现以及为什么要这么做。

## 安装 Ansible

在本章中，你将发现如何在现在最常用的操作系统中安装 Ansible。

## Ansible 术语 - ansible 与 ansible-core 包

什么是 `ansible-core`？什么是 `ansible` 社区包？Ansible 项目在 2.9 版本之后发生了什么变化？现今 Ansible 社区和 `ansible-core` 包的概述及使用场景。

## 什么是 ansible-core? 什么是 ansible 社区包？

Ansible 项目在 2.9 版本之后发生了什么变化？

今天，我们将讨论 2021 年以来发布的 `ansible community`（Ansible 社区）和 `ansible-core` 包。

## ansible vs ansible-core

Ansible 在 2.9 版本之后发生了什么变化？

从 2.10 版本开始，Ansible 分发两个交付物：一个名为 `ansible` 的社区包，以及一个极简的语言和运行时 `ansible-core`（在 2.10 版本中称为 `ansible-base`）。请选择符合你特定需求的 Ansible 风格和版本。

`ansible` 包包含了 Ansible 语言和运行时，以及一系列由社区精选的集合（Collections）。它重现并扩展了 Ansible 2.9 中包含的功能。

你可以选择以下任何方式来安装 Ansible 社区包：

- 使用你操作系统的包管理器安装最新版本（适用于 Red Hat Enterprise Linux、CentOS、Fedora、Debian 或 Ubuntu）。

- 使用 `pip`（Python 包管理器）安装。

### Ansible 社区包发布周期

Ansible 社区团队通常每年发布两个社区包大版本，并采用灵活的发布周期，该周期滞后于 `ansible-core` 的发布。该周期可以延长，以便在发布新版本之前妥善地实现并测试更大的更改。请查看 Ansible 路线图（Ansible Road map）获取即将发布的发布详情。在大版本之间，Ansible 团队每三周会发布一个 Ansible 社区包的新小版本。小版本包含新的向后兼容的特性、模块和插件，以及错误修复。

从 2.10 版本开始，Ansible 社区团队保证一次仅维护一个社区包大版本。例如，当 Ansible 5.0.0 发布时，团队将停止发布新的 4.x 版本。社区成员可以根据需要维护旧版本。

| 特性 | ansible community | ansible-core (曾为 ansible-base 2.10) |

| :--- | :--- | :--- |

| 版本控制 | 使用新版本（2.10，然后是 3.0.0） | 继续“经典 Ansible”版本命名（2.11，然后是 2.12） |

| 语义版本化 | 遵循语义版本化规则 | 不使用语义版本化 |

| 维护 | 一次仅维护一个版本 | 维护最新版本加上两个旧版本 |

| 内容 | 包含语言、运行时和选定的 Collections | 包含语言、运行时和内置插件 |

| 开发 | 在 Collection 仓库中开发和维护 | 在 `ansible/ansible` 仓库中开发和维护 |

## ansible-core

`ansible-core` 包主要面向只想安装他们所需的 collections 的开发者和用户。

### 什么是 ansible-core 包？

Ansible Core 是一个命令行工具，主要面向只想安装他们所需的 collections 的开发者和用户。

它包含极少模块和插件，并允许安装其他 Collections。它类似于 Ansible 2.9，但不包含任何自那以后移动到 Collection 中的内容。

Ansible core 或 `ansible-core` 是 Ansible 的核心构建模块和架构，包括：

- CLI 工具，如 `ansible-playbook`、`ansible-doc.` 等，用于驱动和与自动化交互。

- Ansible 语言使用 YAML 创建一套开发 Ansible Playbooks 的规则，并包含了条件、块（blocks）、包含（includes）、循环和其他 Ansible 指令函数。

- 一个允许通过 Ansible collections 进行扩展的架构框架。

`ansible-core` 大约每年发布一次新的大版本。

## ansible community

Ansible 社区包提供了 Ansible 2.9 的功能，包含 85 多个 collections，其中含有数千个模块和插件。

### 什么是 ansible 社区包？

Ansible 社区包的每个大版本都会采用每个包含的 Collection 的最新版本以及 `ansible-core` 的最新版本。

Ansible 社区包的大版本可能包含包含的 Collections 中模块和其他插件以及/或核心功能中的破坏性更改（breaking changes）。

Ansible 包依赖于 `ansible-base`（很快变为 `ansible-core`）。因此当你执行 `pip install ansible` 时，`pip` 会自动安装 `ansible-core`。

Ansible 3.0.0 及后续版本包含了更多的 Collections，益于更广泛的 Ansible 社区根据社区清单审核 Collections。

Ansible 社区团队通常每年发布两个社区包大版本，并采用灵活的发布周期，该周期滞后于 `ansible-core` 的发布。

## 链接

- [Ansible 3.0.0 问答](https://www.ansible.com/blog/ansible-3.0.0-qa)

- [发布与维护](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html)

- [安装 Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

- [Ansible 社区日志](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html#ansible-community-changelogs)

- [Ansible Core 文档](https://docs.ansible.com/ansible-core/devel/index.html)

- [pip install ansible-core](https://pypi.org/project/ansible-core/)

- [pip install ansible](https://pypi.org/project/ansible/)

## 在 RedHat Enterprise Linux (RHEL) 8 上安装 Ansible

使用 Ansible Engine 在 RedHat Enterprise Linux 8 上安装 Ansible。

我将为你展示如何使用分发工具在 RHEL 8 内部更方便地安装和维护 Ansible。

## 在 RHEL 8 上安装 Ansible

使用分发工具在 RedHat Enterprise Linux 8 内部更方便地安装和维护 Ansible。

包含 Ansible 的仓库被称为 Ansible Engine 软件集合 `ansible-2.9-for-rhel-8-x86_64-rpms`。

使用软件集合的主要优势是，此不需要任何外部仓库（如 EPEL）。

软件集合由 Red Hat 完全支持，并包含在你的订阅计划中。

## Demo

在 RHEL8 上安装最新版本的 Ansible。

```bash
1 #!/bin/bash
2 sudo subscription-manager register
3 sudo subscription-manager repos --enable ansible-2.9-for-rhel-8-x86_64-rpms
5 sudo yum install ansible
```

```
1 #!/bin/bash
2 sudo apt update
3 sudo apt install ansible
```

## 代码 PPA

```
1 #!/bin/bash
2 sudo apt update
3 sudo apt install software-properties-common
4 sudo add-apt-repository --yes --update ppa:ansible/ansible
5 sudo apt remove ansible
6 sudo apt install ansible-base
```

# 如何在 Fedora 35 中安装 Ansible

## 如何使用默认仓库在 Fedora 35 中安装并维护最新版本的 Ansible，并附上实际操作演示。

让我们在 Fedora 35 中安装 Ansible。

好消息是，Ansible 已包含在默认仓库中，因此你可以直接用常用的包管理器进行安装。

在更新仓库中，你可以获得最新版本的 Ansible。

目前可用的最新版本是 2.9。

## 演示

如何在 Fedora 中安装最新版本的 Ansible。

## 代码

`install-Ansible-Fedora.sh`

```
1 #!/bin/bash
2 $ sudo dnf list available ansible
3 $ sudo dnf install ansible
4 $ sudo "rpm -qa | grep ansible"
5 $ sudo dnf list ansible
```

## 执行

# Fedora 安装 Ansible 示例

## 1. 连接与环境准备

```bash
$ ssh devops@fedora.example.com
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

## 2. 软件包查询

查询仓库中可用的 `ansible` 软件包：

```bash
[root@demo devops]# dnf list available ansible
Fedora 35 - x86_64                      3.3 MB/s |  61 MB   00:18
Fedora 35 openh264 (From Cisco) - x86_64  2.7 kB/s | 2.5 kB   00:00
Fedora Modular 35 - x86_64               1.6 MB/s | 2.6 MB   00:01
Fedora 35 - x86_64 - Updates             1.1 MB/s |  15 MB   00:12
Fedora Modular 35 - x86_64 - Updates      400 kB/s | 736 kB   00:01
Available Packages:
ansible.noarch                          2.9.27-1.fc35  updates
```

## 3. 安装 Ansible

执行安装命令 `dnf install ansible`：



## 安装 Ansible

执行以下命令安装 Ansible：

```bash
[root@demo devops]# dnf install ansible
Last metadata expiration check: 0:00:14 ago on Fri 03 Dec 2021 03:42:34 PM UTC.
Dependencies resolved.
========================================================
==========================================
Package                 Architecture    Version            Repository       Size
========================================================
==========================================
Installing:
ansible                 noarch          2.9.27-1.fc35      updates         15 M
Installing dependencies:
libsodium               x86_64          1.0.18-8.fc35      fedora          161 k
python3-bcrypt           x86_64          3.2.0-1.fc35      fedora          43 k
python3-jmes            noarch          0.10.0-1.fc35      fedora          46 k
python3-ntlm-auth       noarch          1.5.0-4.fc35       fedora          53 k
python3-pynacl           x86_64          1.4.0-4.fc35       fedora          108 k
python3-requests_ntlm   noarch          1.1.0-16.fc35      fedora          18 k
python3-xmltodict        noarch          0.12.0-13.fc35     fedora          22 k
sshpass                 x86_64          1.09-2.fc35       fedora          27 k
Installing weak dependencies:
python3-paramiko         noarch          2.7.2-6.fc35       fedora          288 k
python3-pyasn1          noarch          0.4.8-7.fc35       fedora          134 k
python3-winrm           noarch          0.4.1-4.fc35       fedora          80 k
Transaction Summary
========================================================
==========================================
Install  12 Packages
Total download size: 16 M
Installed size: 100 M
Is this ok [y/N]: y
Downloading Packages:
(1/12) python3-bcrypt-3.2.0-1.fc35.x86_64.rpm      317 kB/s |  43 kB   00:00
(2/12) python3-jmes-0.10.0-1.fc35.noarch.rpm      223 kB/s |  46 kB   00:00
(3/12) libsodium-1.0.18-8.fc35.x86_64.rpm      704 kB/s | 161 kB   00:00
(4/12) python3-ntlm-auth-1.5.0-4.fc35.noarch.rpm  566 kB/s |  53 kB   00:00
(5/12) python3-pyasn1-0.4.8-7.fc35.noarch.rpm      1.5 MB/s | 134 kB   00:00
(6/12) python3-paramiko-2.7.2-6.fc35.noarch     1.4 MB/s | 288 kB   00:00
(7/12) python3-requests_ntlm-1.1.0-16.fc35.noarch 827 kB/s |  18 kB   00:00
(8/12) python3-pynacl-1.4.0-4.fc35.x86_64.rpm      935 kB/s | 108 kB   00:00
(9/12) python3-xmltodict-0.12.0-13.fc35.noarch 848 kB/s |  22 kB   00:00
(10/12) sshpass-1.09-2.fc35.x86_64           580 kB/s |  27 kB   00:00
(11/12) python3-winrm-0.4.1-4.fc35.noarch      1.3 MB/s |  80 kB   00:00
(12/12) ansible-2.9.27-1.fc35.noarch          1.4 MB/s |  15 MB   00:11
---------------------------
--------------------------
Total                             1.3 MB/s |  16 MB   00:12
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Preparing:
(1/12) sshpass-1.09-2.fc35.x86_64
(2/12) python3-xmltodict-0.12.0-13.fc35.noarch
(3/12) python3-pyasn1-0.4.8-7.fc35.noarch
(4/12) python3-ntlm-auth-1.5.0-4.fc35.noarch
(5/12) python3-requests_ntlm-1.1.0-16.fc35.noarch
(6/12) python3-winrm-0.4.1-4.fc35.noarch
(7/12) python3-jmespath-0.10.0-4.fc35.noarch
(8/12) python3-bcrypt-3.2.0-1.fc35.x86_64
(9/12) libsodium-1.0.18-8.fc35.x86_64
(10/12) python3-pynacl-1.4.0-4.fc35.x86_64
(11/12) python3-paramiko-2.7.2-6.fc35.noarch
(12/12) ansible-2.9.27-1.fc35.noarch
Installing:
(1/12) sshpass-1.09-2.fc35.x86_64
(2/12) python3-xmltodict-0.12.0-13.fc35.noarch
(3/12) python3-pyasn1-0.4.8-7.fc35.noarch
(4/12) python3-ntlm-auth-1.5.0-4.fc35.noarch
(5/12) python3-requests_ntlm-1.1.0-16.fc35.noarch
(6/12) python3-winrm-0.4.1-4.fc35.noarch
(7/12) python3-jmespath-0.10.0-4.fc35.noarch
(8/12) python3-bcrypt-3.2.0-1.fc35.x86_64
(9/12) libsodium-1.0.18-8.fc35.x86_64
(10/12) python3-pynacl-1.4.0-4.fc35.x86_64
(11/12) python3-paramiko-2.7.2-6.fc35.noarch
(12/12) ansible-2.9.27-1.fc35.noarch
Running script: ansible-2.9.27-1.fc35.noarch
Verifying:
(1/12) libsodium-1.0.18-8.fc35.x86_64
(2/12) python3-bcrypt-3.2.0-1.fc35.x86_64
(3/12) python3-jmespath-0.10.0-4.fc35.noarch
(4/12) python3-ntlm-auth-1.5.0-4.fc35.noarch
(5/12) python3-pyasn1-0.4.8-7.fc35.noarch
(6/12) python3-pynacl-1.4.0-4.fc35.x86_64
(7/12) python3-requests_ntlm-1.1.0-16.fc35.noarch
(8/12) python3-winrm-0.4.1-4.fc35.noarch
(9/12) python3-xmltodict-0.12.0-13.fc35.noarch
(10/12) sshpass-1.09-2.fc35.x86_64
(11/12) python3-paramiko-2.7.2-6.fc35.noarch
(12/12) ansible-2.9.27-1.fc35.noarch
Complete!
```

## 验证安装

验证安装结果及版本：

```bash
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
Installed Packages:
ansible.noarch                          2.9.27-1.fc35  updates

[root@demo devops]# dnf list installed ansible
Installed Packages:
ansible.noarch                          2.9.27-1.fc35  updates
[root@demo devops]#
```

## 执行前

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
[root@demo devops]# dnf list installed ansible
Error: No matching Packages to list
[root@demo devops]# dnf list ansible
Last metadata expiration check: 0:03:45 ago on Fri 03 Dec 2021 03:42:34 PM UTC.
Available Packages
ansible.noarch                               2.9.27-1.fc35                updates
[root@demo devops]#
```

## 执行后

```bash
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
ansible.noarch                               2.9.27-1.fc35                @updates
[root@demo devops]# dnf list installed ansible
Installed Packages
ansible.noarch                               2.9.27-1.fc35                @updates
[root@demo devops]#
```

## 如何在 CentOS 9 Stream 中安装 Ansible

在 CentOS 9 Stream 中安装最新版本 Ansible 并保持其更新的简单方法是使用`DNF`和`AppStream`系统仓库。

## 如何在 CentOS Stream 9 中安装 Ansible

### 使用系统 AppStream 仓库中的`ansible-core`

### 使用 Extra Packages for Enterprise Linux - EPEL Next

针对 CentOS Stream 9 的额外软件包。

在 CentOS Stream 9 中安装和维护 Ansible 的简单方法是使用系统`AppStream`仓库。

另一种方法是使用额外的`EPEL Next`仓库。该仓库由 Fedora 特别兴趣小组维护，为 CentOS Stream 管理一组高质量的额外软件包，类似于针对 Red Hat Enterprise Linux (`RHEL`)、`CentOS`、Scientific Linux (`SL`) 以及 Oracle Linux (`OL`) 的 Extra Packages for Enterprise Linux (`EPEL`) 额外软件包。

## 链接

- [CentOS Stream 下载](https://www.centos.org/centos-stream/)
- [EPEL 9 现在已可用](https://communityblog.fedoraproject.org/epel-9-is-now-available/)



- [介绍 CentOS Stream 9](https://blog.centos.org/2021/12/introducing-centos-stream-9/)
- [Extra Packages for Enterprise Linux (EPEL)](https://docs.fedoraproject.org/en-US/epel/)

## 演示

介绍如何通过 `AppStream` 仓库在 CentOS Stream 版本 9 中安装 Ansible。

## 代码

### Install-Ansible-CentOS-Stream9.sh

```bash
#!/bin/bash
sudo dnf install ansible-core
```

# CentOS Stream 9 环境配置与 Ansible 安装

## 1. 登录与系统信息

通过 SSH 登录到服务器并切换到 root 用户：

```bash
$ ssh devops@centos-stream.example.com
[devops@centos-stream ~]$ sudo su
[root@centos-stream devops]# cat /etc/redhat-release
CentOS Stream release 9
```

查看`/etc/os-release`获取系统详细信息：

```bash
[root@centos-stream devops]# cat /etc/os-release
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

使用`hostnamectl`查看主机详细配置：

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

## 2. 搜索 Ansible

使用`dnf`搜索`ansible`相关软件包：

```bash
[root@centos-stream devops]# dnf search ansible
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
CentOS Stream 9 - BaseOS 1.2 MB/s | 1.6 MB 00:01
CentOS Stream 9 - AppStream 2.7 MB/s | 8.8 MB 00:03
Last metadata expiration check: 0:00:01 ago on Mon 06 Dec 2021 11:55:34 AM UTC.
================================= Name & Summary Matched:
ansible ==================================
ansible-collection-microsoft-sql.noarch : The Ansible collection for Microsoft SQL Server management
ansible-freeipa-tests.noarch : ansible-freeipa tests
ansible-pcp.noarch : Ansible Metric collection for Performance Co-Pilot
ansible-test.x86_64 : Tool for testing ansible plugin and module code
=======================================
Name Matched: ansible ======================================
ansible-core.x86_64 : SSH-based configuration management, deployment, and task execution system
ansible-freeipa.noarch : Roles and playbooks to deploy FreeIIPA servers, replicas and clients
```

## 3. 安装 ansible-core

查看`ansible-core`的详细信息：

```bash
[root@centos-stream devops]# dnf info ansible-core
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
Last metadata expiration check: 0:00:55 ago on Mon 06 Dec 2021 11:55:34 AM UTC.
Available Packages
Name         : ansible-core
Version      : 2.12.0
Release      : 1.el9
Architecture : x86_64
Size         : 2.4 M
Source       : ansible-core-2.12.0-1.el9.src.rpm
Repository   : appstream
Summary      : SSH-based configuration management, deployment, and task execution system
URL          : http://ansible.com
License      : GPL3+
Description  : Ansible is a radically simple model-driven configuration management, multi-node deployment, and task execution system. Ansible works over SSH and does not require any daemons to be installed on remote nodes. Modules can be written in any language and are transferred to managed machines.
```

安装`ansible-core`：

```bash
[root@centos-stream devops]# dnf install ansible-core
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
Last metadata expiration check: 0:1:13 ago on Mon 06 Dec 2021 11:55:4 AM UTC.
Dependencies resolved.
======================================== ==========================
Package               Architecture  Version           Repository    Size
======================================== ==========================
Installing: ansible-core          x86_64        2.12.0-1.el9    appstream      2.4 M
Installing dependencies:
emacs-filesystem      noarch        1:27.1-3.el9     appstream      9.2 k
git                   x86_64        2.31.1-2.el9     appstream      124 k
git-core              x86_64        2.31.1-2.el9.2  appstream      3.6 M
git-core-doc          noarch        2.31.1-2.el9.2  appstream      2.5 M
perl-Error            noarch        1:0.17029-7.el9  appstream      42 k
perl-Git             noarch        2.31.1-2.el9.2  appstream      43 k
python3-babel          noarch        2.9.1-2.el9     appstream      6.0 M
python3-ffi           x86_64        1.14.5-4.el9    appstream      254 k
python3-cryptography   x86_64        3.4.7-5.el9     appstream      780 k
python3-jinja2         noarch        2.11.3-4.el9    appstream      249 k
python3-markupsafe     x86_64        1.1.1-12.el9    appstream      35 k
python3-packaging      noarch        20.9-4.el9      appstream      78 k
python3-ply            noarch        3.11-13.el9     appstream      107 k
python3-pyparser       noarch        2.20-5.el9      appstream      135 k
python3-pytz           noarch        2021.1-4.el9    appstream      52 k
python3-resolvelib      noarch        0.5.4-5.el9     appstream      34 k
sshpass               x86_64        1.09-4.el9      appstream      28 k

Transaction Summary
========================================= ==========================
Install              18 Packages
Total download size: 16 M
Installed size: 75 M
Is this ok [y/N]: y
... (下载过程略) ...
Running transaction check.
Transaction check succeeded.
Running transaction test.
Transaction test succeeded.
Running transaction.
Preparing              : ansible-core (1/1)
Installing: git-core-2.31.1-2.el9.2.x86_64 (1/18)
Installing: git-core-doc-2.31.1-2.el9.2.noarch (2/18)
Installing: sshpass-1.09-4.el9.x86_64 (3/18)
Installing: python3-resolvelib-0.5.4-5.el9.noarch (4/18)
Installing: python3-pytz-2021.1-4.el9.noarch (5/18)
Installing: python3-babel-2.9.1-2.el9.noarch (6/18)
Installing: python3-ply-3.11-13.el9.noarch (7/18)
Installing: python3-pyparser-2.20-5.el9.noarch (8/18)
Installing: python3-ffiffi-.14.5-4.el9.x86_64 (9/18)
Installing: python3-cryptography-3.4.7-5.el9.x86_64 (10/18)
Installing: python3-jinja2-2.11.3-4.el9.noarch (11/18)
Installing: python3-markupsafe-1.1.1-12.el9.x86_64 (12/18)
Installing: python3-packaging-20.9-4.el9.noarch (13/18)
Installing: ansible-core-2.12.0-1.el9.x86_64 (14/18)
Running script: ansible-core-2.12.0-1.el9.x86_64
Verifying: ansible-core-2.12.0-1.el9.x86_64 (1/18)
Verifying: emacs-filesystem-1:27.1-3.el9.noarch (2/18)
Verifying: git-2.31.1-2.el9.2.x86_64 (3/18)
Verifying: git-core-2.31.1-2.el9.2.x86_64 (4/18)
Verifying: git-core-doc-2.31.1-2.el9.2.noarch (5/18)
Verifying: perl-Error-1:0.17029-7.el9.noarch (6/18)
Verifying: perl-Git-2.31.1-2.el9.2.noarch (7/18)
Verifying: python3-babel-2.9.1-2.el9.noarch (8/18)
Verifying: python3-ffi-1.14.5-4.el9.x86_64 (9/18)
Verifying: python3-cryptography-3.4.7-5.el9.x86_64 (10/18)
Verifying: python3-jinja2-2.11.3-4.el9.noarch (11/18)
Verifying: python3-markupsafe-1.1.1-12.el9.x86_64 (12/18)
Verifying: python3-packaging-20.9-4.el9.noarch (13/18)
Verifying: python3-ply-3.11-13.el9.noarch (14/18)
Verifying: python3-pyparser-2.20-5.el9.noarch (15/18)
Verifying: python3-pytz-2021.1-4.el9.noarch (16/18)
Verifying: python3-resolvelib-0.5.4-5.el9.noarch (17/18)
Verifying: sshpass-1.09-4.el9.x86_64 (18/18)
Complete!
```

## 4. 验证安装

检查`ansible`版本：



```bash
[root@centos-stream devops]# ansible --version
ansible [core 2.12.0]
config file = /etc/ansible/ansible.cfg
configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
ansible python module location = /usr/lib/python3.9/site-packages/ansible
ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
executable location = /bin/ansible
python version = 3.9.8 (main, Nov 8 2021, 00:00:00) [GCC 11.2.1 20211019 (Red Hat 11.2.1-6)]
jinja version = 2.11.3
libyaml = True
```

再次确认`ansible-core`信息：

```bash
[root@centos-stream devops]# dnf info ansible-core
... (已略)
```

## 执行前

```bash
# dnf info ansible-core
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
Last metadata expiration check: 0:00:55 ago on Mon 06 Dec 2021 11:55:34 AM UTC.
Available Packages
Name            : ansible-core
Version         : 2.12.0
Release         : 1.el9
Architecture    : x86_64
Size            : 2.4 M
Source          : ansible-core-2.12.0-1.el9.src.rpm
Repository      : appstream
Summary         : SSH-based configuration management, deployment, and task execution system
URL             : http://ansible.com
License         : GPLv3+
Description     : Ansible is a radically simple model-driven configuration management, multi-node deployment, and task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
[root@centos-stream devops]#
```

## 执行后

```bash
# dnf info ansible-core
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered with an entitlement server.
You can use subscription-manager to register.
Last metadata expiration check: 0:02:00 ago on Mon 06 Dec 2021 11:55:34 AM UTC.
Installed Packages
Name            : ansible-core
Version         : 2.12.0
Release         : 1.el9
Architecture    : x86_64
Size            : 9.3 M
Source          : ansible-core-2.12.0-1.el9.src.rpm
Repository      : @System
From repo        : appstream
Summary         : SSH-based configuration management, deployment, and task execution system
URL             : http://ansible.com
License         : GPLv3+
Description     : Ansible is a radically simple model-driven configuration management, multi-node deployment, and task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
[root@centos-stream devops]#
```

## 如何在 Windows 11 WSL Windows Linux 子系统中安装 Ansible

### 如何使用 Windows Subsystem for Linux 和 Ubuntu 20.04 LTS 在 Windows 11 中安装和维护 Ansible

### 使用 Windows Subsystem for Linux 在 Windows 11 中安装和维护 Ansible 的简单方法

### 如何在 Windows 11 中安装 Ansible

#### 官方支持

目前 Windows **并不是**控制节点支持的操作系统，尽管 RedHat 正在非常努力消除原生 Windows 控制器的障碍。

背后的原因是 Ansible 的大部分功能都深植了许多 UNIX 特性，这导致它无法在原生 Windows 上运行。从根本上说，Windows 没有`fork()`系统调用的实现。从 2.11 版本开始，Ansible 控制器工作模型大量使用了 POSIX `fork()`系统调用。

#### Cygwin

有些人使用了 Cygwin POSIX 兼容性项目，但有时它们会崩溃，因此这并不是一个可靠的解决方案。

#### Windows Subsystem for Linux

最佳替代方案是使用 Windows Subsystem for Linux，也称为`WSL`。如果 Windows 10 版本高于 2004 或使用 Windows 11，请运行`WSL`版本 2。Ansible 在`WSL`和`WSL2`上运行得良好。

## 链接

更多技术信息：

- [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/compare-versions)
- [Ansible on Windows FAQ](https://docs.ansible.com/ansible/latest/user_guide/windows_faq.html)
- [Windows Subsystem for Linux on Windows 11](https://arstechnica.com/gadgets/2021/10/the-best-part-of-windows-11-is-a-revamped-windows-subsystem-for-linux/)

## 演示

如何使用 Windows Subsystem for Linux 在 Windows 中安装最新或特定版本的 Ansible。

## 代码

```bash
install_wsl.ps1
wsl --help
wsl --list -o
wsl --install
```

## 执行

### 安装 WSL

```bash
Windows PowerShell
2 Copyright (C) Microsoft Corporation. All rights reserved.

Install the latest PowerShell for new features and improvements! https://aka.ms/PSWindows

PS C:\Users\user> wsl --install
Installing: Virtual Machine Platform
Virtual Machine Platform has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Downloading: WSL Kernel
Installing: WSL Kernel
WSL Kernel has been installed.
Downloading: GUI App Support
Installing: GUI App Support
GUI App Support has been installed.
Downloading: Ubuntu
The requested operation is successful. Changes will not be effective until the system is rebooted.
PS C:\Users\user>
```

## 设置 Ubuntu 20.04 LTS WSL 并安装 ansible

1. 正在安装，这可能需要几分钟……

2. 请创建一个默认的 UNIX 用户账户。用户名`demo`不需要与您的 Windows 用户名匹配。

3. 欲了解更多信息请访问：https://aka.ms/wslusers

4. 输入新的 UNIX 用户名：`demo`

5. 新密码：

6. 重新输入新密码：

7. `passwd`：密码更新成功

8. 安装成功！

9. 要管理员身份运行命令（用户`"root"`），请使用`sudo <command>`。

10. 详情请参见`man sudo_root`。

欢迎来到 Ubuntu 20.04 LTS (GNU/Linux 4.4.0-22000-Microsoft x86_64)

- 文档：https://help.ubuntu.com
- 管理：https://landscape.canonical.com
- 支持：https://ubuntu.com/advantage

系统信息，截至 2022 年 1 月 10 日 周一 16:57:36 UTC

系统负载：0.52  
登录用户：0

`/home`使用率：未知  
IPv4 地址`eth0`：10.0.2.15

内存使用率：73%  
IPv4 地址`eth1`：169.25.4.235.130

交换分区使用率：1%  
IPv4 地址`eth1`：192.168.0.209

进程数：7

有 0 个更新可以立即安装。这些更新中有 0 个安全更新。

可用更新列表已有一周未更新。要检查新更新，请运行：`sudo apt update`

此消息每天显示一次。要禁用它，请创建`/home/demo/.hushlogin`文件。



```bash
demo@demo:~$ sudo su
[sudo] password for demo:
root@demo:/home/demo# apt-get update
Get:1 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates In [114 kB]
Get:3 http://security.ubuntu.com/ubuntu focal-security In [114 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-backports In [108 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/main amd64 Packages [970 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/main Translation-en [506 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/main amd64 c-n-f Metadata [29.5 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal-universe amd64 Packages [8628 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/universe Translation-en [5124 kB]
Get:10 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1109 kB]
Get:11 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [200 kB]
Get:12 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [9104 B]
Get:13 http://archive.ubuntu.com/ubuntu focal-universe amd64 c-n-f Metadata [265 kB]
Get:14 http://archive.ubuntu.com/ubuntu focal-multiverse amd64 Packages [144 kB]
Get:15 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [609 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal-multiverse Translation-en [104 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal-multiverse amd64 c-n-f Metadata [9136 B]
Get:18 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1445 kB]
Get:19 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [86.8 kB]
Get:20 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Metadata [536 B]
Get:21 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [675 kB]
Get:22 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [114 kB]
Get:23 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [13.0 kB]
Get:24 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [21.8 kB]
Get:25 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [4948 B]
Get:26 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [536 B]
Get:27 http://archive.ubuntu.com/ubuntu focal-updates/main Translation-en [289 kB]
Get:28 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [14.7 kB]
Get:29 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [663 kB]
Get:30 http://archive.ubuntu.com/ubuntu focal-updates/restricted Translation-en [94.6 kB]
Get:31 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 c-n-f Metadata [532 B]
Get:32 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [892 kB]
Get:33 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [195 kB]
Get:34 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [19.9 kB]
Get:35 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [24.8 kB]
Get:36 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [6928 B]
Get:37 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [620 B]
Get:38 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [42.0 kB]
Get:39 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [10.0 kB]
Get:40 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 c-n-f Metadata [864 B]
Get:41 http://archive.ubuntu.com/ubuntu focal-backports/restricted amd64 Metadata [116 B]
Get:42 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [19.5 kB]
Get:43 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [13.4 kB]
Get:44 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 c-n-f Metadata [656 B]
Get:45 http://archive.ubuntu.com/ubuntu focal-backports/multiverse amd64 c-n-f Metadata [116 B]
Fetched 23.0 MB in 7s (3188 kB/s)
Reading package lists... Done
root@demo:/home/demo# apt-get install ansible
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
ee-data python3-crypto python3-dnysthon python3-mespath python3-kerberos python3-libcloud python3-lockfile python3-netaddr python3-ntlm-auth python3-requests-kerberos python3-requests-ntlm python3-selinux python3-winrm python3-xmltodict
Suggested packages: cowsay sshpass ipython-debian
The following NEW packages will be installed:
ansible ee-data python3-crypto python3-dnysthon python3-mespath python3-kerberos python3-libcloud python3-lockfile python3-netaddr python3-ntlm-auth python3-requests-kerberos python3-requests-ntlm python3-selinux python3-winrm python3-xmltodict
0 upgraded, 16 newly installed, 0 to remove and 0 not installed.
Need to get 9644 kB of archives. After this operation, 90.2 MB of additional disk space will be used. Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal/main python3-crypto 2.6.1-13ubuntu2 [237 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/main python3-dnysthon 1.16.0-1build1 [89.1 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/main ee-data 20180805.1 [1589 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-updates/main python3-netaddr 0.7.19-3ubuntu1 [236 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/universe ansible 2.9.6+dfsg-1 [5794 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/universe python3-argcomplete 1.8.1-3ubuntu1 [27.2 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main python3-mespath 0.9.4-2ubuntu1 [15.5 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/universe python3-kerberos 1.14-3.build1 [22.6 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/main python3-lockfile 0.12.2-ubuntu2 [14.6 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal/universe python3-libcloud 2.8.0-1 [1403 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal/universe python3-ntlm-auth 1.1.0-1 [19.6 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal/universe python3-requests-kerberos 0.12.0-2 [11.9 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal/universe python3-requests-ntlm 1.0.1 [6004 B]
Get:14 http://archive.ubuntu.com/ubuntu focal/universe python3-selinux 3.0-1build2 [139 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal/universe python3-xmltodict 0.12.0-1 [12.6 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal/universe python3-winrm 0.3.0-2 [21.7 kB]
Fetched 9644 kB in 2s (4411 kB/s)
Selecting previously unselected package python3-crypto. (Reading database ... 31836 files and directories currently installed.)
Preparing to unpack .../00-python3-crypto_2.6.1-13ubuntu2_amd64.deb ...
Unpacking python3-crypto (2.6.1-13ubuntu2) ...
Selecting previously unselected package python3-dnysthon.
Preparing to unpack .../01-python3-dnysthon_1.16.0-1build1_amd64.deb ...
Unpacking python3-dnysthon (1.16.0-1build1) ...
Selecting previously unselected package ee-data.
Preparing to unpack .../02-ieee-data_20180805.1_amd64.deb ...
Unpacking ee-data (20180805.1) ...
Selecting previously unselected package python3-netaddr.
Preparing to unpack .../03-python3-netaddr_0.7.19-3ubuntu1_amd64.deb ...
Unpacking python3-netaddr (0.7.19-3ubuntu1) ...
Selecting previously unselected package ansible.
Preparing to unpack .../04-ansible_2.9.6+dfsg-1_amd64.deb ...
Unpacking ansible (2.9.6+dfsg-1) ...
Selecting previously unselected package python3-argcomplete.
Preparing to unpack .../05-python3-argcomplete_1.8.1-3ubuntu1_amd64.deb ...
Unpacking python3-argcomplete (1.8.1-3ubuntu1) ...
Selecting previously unselected package python3-mespath.
Preparing to unpack .../06-python3-mespath_0.9.4-2ubuntu1_amd64.deb ...
Unpacking python3-mespath (0.9.4-2ubuntu1) ...
Selecting previously unselected package python3-kerberos.
Preparing to unpack .../07-python3-kerberos_1.14-3.build1_amd64.deb ...
Unpacking python3-kerberos (1.14-3.build1) ...
Selecting previously unselected package python3-lockfile.
Preparing to unpack .../08-python3-lockfile_0.12.2-ubuntu2_amd64.deb ...
Unpacking python3-lockfile (0.12.2-ubuntu2) ...
Selecting previously unselected package python3-libcloud.
Preparing to unpack .../09-python3-libcloud_2.8.0-1_amd64.deb ...
Unpacking python3-libcloud (2.8.0-1) ...
Selecting previously unselected package python3-ntlm-auth.
Preparing to unpack .../10-python3-ntlm-auth_1.1.0-1_amd64.deb ...
Unpacking python3-ntlm-auth (1.1.0-1) ...
Selecting previously unselected package python3-requests-kerberos.
Preparing to unpack .../11-python3-requests-kerberos_0.12.0-2_amd64.deb ...
Unpacking python3-requests-kerberos (0.12.0-2) ...
Selecting previously unselected package python3-requests-ntlm.
Preparing to unpack .../12-python3-requests-ntlm_1.0.1_amd64.deb ...
Unpacking python3-requests-ntlm (1.0.1) ...
Selecting previously unselected package python3-selinux.
Preparing to unpack .../13-python3-selinux_3.0-1build2_amd64.deb ...
Unpacking python3-selinux (3.0-1build2) ...
Selecting previously unselected package python3-xmltodict.
Preparing to unpack .../14-python3-xmltodict_0.12.0-1_amd64.deb ...
Unpacking python3-xmltodict (0.12.0-1) ...
Selecting previously unselected package python3-winrm.
Preparing to unpack .../15-python3-winrm_0.3.0-2_amd64.deb ...
Unpacking python3-winrm (0.3.0-2) ...
```



```bash
root@demo:/home/demo# ansible --version
ansible 2.9.6
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.8.2 (default, Mar 13 2020, 10:14:16) [GCC 9.3.0]
```

```bash
root@demo:/home/demo# apt list ansible
Listing... Done
ansible/focal,now 2.9.6+dfsg-1 all [installed]
```

```bash
root@demo:/home/demo#
```

# 回顾

现在你已了解如何使用适用于 Linux 的 Windows 子系统在 Windows 11 中安装最新版本的 Ansible。

## 如何在 SUSE Linux Enterprise Server (SLES) 15 SP3 中安装 Ansible

介绍如何使用 SUSE Package Hub 仓库在 SUSE Linux Enterprise Server (SLES) 15 SP3 中安装并保持 Ansible 为最新版本。

### 使用 SUSE Package Hub 仓库

在 SUSE Linux Enterprise 版本 15 SP3 中安装并维护 Ansible 的更简单方法是使用由 SUSE 社区维护的 SUSE Package Hub 仓库。

## 链接

[SUSE Package Hub - SUSE Linux Enterprise Server / Desktop 的社区软件包](https://packagehub.suse.com/)

[如何使用 SUSEConnect 命令行工具注册 SLES](https://www.suse.com/support/kb/doc/?id=000018564)

[向 SUSE Linux Enterprise Server 添加 SUSE Package Hub 仓库](https://www.suse.com/support/kb/doc/?id=000018789)

## 演示

如何在 SUSE Linux Enterprise Server 15 SP3 中安装最新版本的 Ansible。

## 代码

`Install-Ansible-SLES-15-SP3.sh`

```bash
1 #!/bin/bash
2 SUSEConnect --status
3 SUSEConnect --list-extensions
4 SUSEConnect -p PackageHub/15.3/x86_64
5 zypper install ansible
6 zypper info ansible
7 ansible --version
```

## 执行

# SLES 15 SP3 环境配置记录

## 登录与基础信息

```bash
ssh devops@sles.example.com
devops@sles:~> sudo su
sles:/home/devops # cat /etc/os-release
```

系统版本输出：

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

查看主机信息：

```bash
sles:/home/devops # hostnamectl
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

查看内核信息：

```bash
sles:/home/devops # uname -a
Linux sles 5.3.18-57-default #1 SMP Wed Apr 28 10:54:41 UTC 2021 (ba3c2e9) x86_64 x86_64 x86_64 GNU/Linux
```

## 软件包仓库与订阅管理

检查订阅状态：

```bash
sles:/home/devops # SUSEConnect --status
```

```json
[
  {"identifier":"sle-module-basesystem","version":"15.3","arch":"x86_64","status":"Registered"},
  {"identifier":"SLES ","version":"15.3","arch":"x86_64","status":"Registered","regcode":"****************","starts_at":"2021-12-07 00:00:00 UTC","expires_at":"2022-02-07 00:00:00 UTC","subscription_status":"ACTIVE","type":"evaluation"},
  {"identifier":"sle-module-server-applications","version":"15.3","arch":"x86_64","status":"Registered"}
]
```

刷新仓库：

```bash
sles:/home/devops # zypper refresh
```

Repository 'SLE-Module-Basesystem15-SP3-Pool' is up to date.  
Repository 'SLE-Module-Basesystem15-SP3-Updates' is up to date.  
Repository 'SLE-Product-SLES15-SP3-Pool' is up to date.  
Repository 'SLE-Product-SLES15-SP3-Updates' is up to date.  
Repository 'SLE-Module-Server-Applications15-SP3-Pool' is up to date.  
Repository 'SLE-Module-Server-Applications15-SP3-Updates' is up to date.  
All repositories have been refreshed.

## Ansible 安装尝试

搜索 `ansible`：

```bash
sles:/home/devops # zypper search ansible
```

结果：没有匹配的项。

尝试安装 `ansible`：

```bash
sles:/home/devops # zypper install ansible
```

结果：未找到 `ansible` 的提供者。

## 模块列表检查

查看可用模块：

```bash
sles:/home/devops # SUSEConnect --list-extensions
```

可用模块包括：

- Basesystem Module 15 SP3 x86_64（已激活）
- Containers Module 15 SP3 x86_64
- Desktop Applications Module 15 SP3 x86_64
- Development Tools Module 15 SP3 x86_64
- NVIDIA Compute Module 15 x86_64
- SUSE Linux Enterprise Workstation Extension 15 SP3 x86_64
- Python 2 Module 15 SP3 x86_64
- SUSE Cloud Platform Tools Module 15 SP3 x86_64
- SUSE Linux Enterprise Live Patching 15 SP3 x86_64
- SUSE Package Hub 15 SP3 x86_64
- Server Applications Module 15 SP3 x86_64（已激活）
- Legacy Module 15 SP3 x86_64
- Public Cloud Module 15 SP3 x86_64
- SUSE Linux Enterprise High Availability Extension 15 SP3 x86_64
- Web and Scripting Module 15 SP3 x86_64
- Transactional Server Module 15 SP3 x86_64

## 验证

检查 Ansible 版本：

```bash
sles:/home/devops # ansible --version
```

```text
ansible 2.9.6
config file = /etc/ansible/ansible.cfg
configured module path = ['/root/.ansible/plugins', '/usr/share/ansible/plugins']
module location = /usr/lib/python3.6/site-packages/ansible
executable location = /usr/bin/ansible
version = 3.6.13 (default, Mar 10 2021)
```

查看详细信息：

```bash
sles:/home/devops # zypper info ansible
```

```text
Information for package ansible:
Repository    : SUSE-PackageHub-15-SP3-Backports-Pool
Name          : ansible
Version       : 2.9.6-bp153.1.20
Arch          : noarch
Vendor        : openSUSE
Support Level : unknown
Installed Size : 96.0 MiB
Installed      : No
Status        : up-to-date (注：此处显示为未安装)
Summary       : SSH-based configuration management, deployment, and task execution system
Description   : Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
```

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
Installed Size  : 96.0 MiB
Installed       : Yes
Status          : up-to-date
Source package  : ansible-2.9.6-bp153.1.20.src
Summary         : 基于 SSH 的配置管理、部署和任务执行系统
Description     :
    Ansible 是一种极其简单的模型驱动的配置管理、多节点部署和远程任务执行系统。Ansible 通过 SSH 工作，且不需要在远程节点上安装任何软件或守护进程。扩展模块可以使用任何语言编写，并自动传输到被管理的机器。
sles:/home/devops #
```

## 如何使用 PIP 安装 Ansible

如何使用 Python 包管理器 `PIP` 安装 Ansible？

`PIP` 是 Python 的包管理器，它将处理所有安装过程并管理必要的依赖关系。它直接负责从 `PyPI` 下载和安装包的过程。`PIP` 的设计与操作系统无关。

对于始终想要获取最新发布版本的开发者来说，这可能是一个解决方案。

另一种方法是使用特定操作系统的包管理器。例如，Linux 下使用 `yum`、`DNF` 和 `apt`，macOS 下使用 `Homebrew`。

第二种方法更强调稳定性，因此可能无法获得最新版本。

所以，如果你确实需要 Ansible 的最新版本，我建议你使用 `PIP`。

## 使用 PIP 演示安装 Ansible

如何使用 Python 包管理器 `PIP` 安装最新版本的 Ansible。

### PIP 用户模式

`install-pip-user.sh`

```bash
#!/bin/bash
python3 -m pip install --upgrade -user pip
python3 -m pip install --user ansible
```

### PIP 全局模式

`install-pip-global.sh`

```bash
#!/bin/bash
python3 -m pip install --upgrade pip
python3 -m pip install ansible
```

## 如何在 RedHat Enterprise Linux 9 Beta 中安装 Ansible




# 如何在 RedHat Enterprise Linux 9 Beta 中安装 Ansible Core

## 背景信息

RHEL 9 AppStream 仓库已开箱自带了`ansible-core`包（`ansible-core`）。

对于基础自动化，不再像以前的版本那样需要额外的仓库（如`Ansible Engine`或`EPEL`）。

然而，如果需要对底层平台和 Core 维护模块提供额外支持，则需要 Ansible Automation Platform 订阅。

## 相关链接

- [RHEL 9 AppStream 中包含的 Ansible Core 包的支持范围](https://access.redhat.com/articles/6325611)
- [在 RHEL 9 中使用 Ansible](https://access.redhat.com/articles/6393321)

---

# 登录与系统环境

## 登录系统

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

## 系统信息查询

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
[root@localhost devops]# uname -a
Linux localhost.localdomain 5.14.0-39.el9.x86_64 #1 SMP PREEMPT Fri Dec 24 00:07:58 EST 2021 x86_64 x86_64 x86_64 GNU/Linux
```

## 搜索并查看 Ansible 包信息

```bash
[root@localhost devops]# dnf search ansible
Updating Subscription Management repositories.
Last metadata expiration check: 1:40:46 ago on Fri 21 Jan 2022 04:15:49 PM CET.
================================= Name & Summary Matched: ansible =================================================
ansible-collection-microsoft-sql.noarch : The Ansible collection for Microsoft SQL Server management
ansible-freeipa-tests.noarch : ansible-freeipa tests
ansible-pcp.noarch : Ansible Metric collection for Performance Co-Pilot
ansible-test.x86_64 : Tool for testing ansible plugin and module code
====================================== Name Matched: ansible ==================================================
ansible-core.x86_64 : SSH-based configuration management, deployment, and task execution system
ansible-freeipa.noarch : Roles and playbooks to deploy freeIPA servers, replicas and clients
==================================== Summary Matched: ansible =====================================
rhc-worker-playbook.x86_64 : Python worker for Red Hat Connector that launches Ansible Runner
```

```bash
[root@localhost devops]# dnf info ansible-core
Updating Subscription Management repositories.
Last metadata expiration check: 1:41:06 ago on Fri 21 Jan 2022 04:15:49 PM CET.
Available Packages
Name : ansible-core
Version : 2.12.1
Release : 1.el9
Architecture : x86_64
Size : 2.4 M
Source : ansible-core-2.12.1-1.el9.src.rpm
Repository : rhel-9-for-x86_64-appstream-rpms
Summary : SSH-based configuration management, deployment, and task execution system
URL : http://ansible.com
License : GPL3+
Description : Ansible is a radically simple model-driven multi-node deployment, and remote execution system. Ansible works over SSH and does not require any daemons to be installed on remote nodes. Extension can be written in any language and are transferred to managed machines automatically.
```




使用`dnf`命令安装`ansible-core`，执行以下命令：

```bash
[root@localhost devops]# dnf install ansible-core
```

执行后，系统进行依赖解析并显示以下信息：

```
Updating Subscription Management repositories.
Last metadata expiration check: 1:41:25 ago on Fri 21 Jan 2022 04:15:49 PM CET.
Dependencies resolved.
```

安装的软件包列表如下：

```
Package             Arch      Version            Repository                           Size
Installing: ansible-core  x86_64  2.12.1-1.el9 rhe-9-for-x86_64-appstream-rpms 2.4 M
Installing dependencies: git          x86_64  2.31.1-2.el9 rhe-9-for-x86_64-appstream-rpms 128 k
git-core            x86_64  2.31.1-2.el9 rhe-9-for-x86_64-appstream-rpms 3.6 M
git-core-doc        noarch    2.31.1-2.el9 rhe-9-for-x86_64-appstream-rpms 2.5 M
perl-AutoLoader     noarch    5.74-479.el9 rhe-9-for-x86_64-appstream-rpms 31 k
perl-B              x86_64  1.80-479.el9 rhe-9-for-x86_64-appstream-rpms 193 k
perl-Carp           noarch    1.50-460.el9 rhe-9-for-x86_64-appstream-rpms 31 k
perl-Class-Struct    noarch    0.66-479.el9 rhe-9-for-x86_64-appstream-rpms 32 k
perl-Data-Dumper    x86_64  2.174-462.el9 rhe-9-for-x86_64-appstream-rpms 58 k
perl-Digest          noarch    1.19-4.el9 rhe-9-for-x86_64-appstream-rpms 20 k
perl-Digest-MD5      x86_64  2.58-4.el9 rhe-9-for-x86_64-appstream-rpms 39 k
perl-DynaLoader      x86_64  1.47-479.el9 rhe-9-for-x86_64-appstream-rpms 35 k
perl-Encode          x86_64  3.08-462.el9 rhe-9-for-x86_64-appstream-rpms 17 k
perl-Errno           x86_64  1.30-479.el9 rhe-9-for-x86_64-appstream-rpms 24 k
perl-Error           noarch    1.7029-7.el9 rhe-9-for-x86_64-appstream-rpms 46 k
perl-Exporter         noarch    5.74-461.el9 rhe-9-for-x86_64-appstream-rpms 33 k
perl-Fcntl           x86_64  1.13-479.el9 rhe-9-for-x86_64-appstream-rpms 31 k
perl-File-Basename   noarch    2.85-479.el9 rhe-9-for-x86_64-appstream-rpms 27 k
perl-File-Find       noarch    1.37-479.el9 rhe-9-for-x86_64-appstream-rpms 35 k
perl-File-Path       noarch    2.18-4.el9 rhe-9-for-x86_64-appstream-rpms 37 k
perl-File-Temp       noarch    1.231.100-4.el9 rhe-9-for-x86_64-appstream-rpms 62 k
perl-File-stat       noarch    1.09-479.el9 rhe-9-for-x86_64-appstream-rpms 27 k
perl-Handle          noarch    2.03-479.el9 rhe-9-for-x86_64-appstream-rpms 25 k
perl-Getopt-Long      noarch    2.52-4.el9 rhe-9-for-x86_64-appstream-rpms 63 k
perl-Getopt-Std      noarch    1.12-479.el9 rhe-9-for-x86_64-appstream-rpms 25 k
perl-Git             noarch    2.31.1-2.el9.2 rhe-9-for-x86_64-appstream-rpms 44 k
perl-HTTP-Tiny       noarch    0.076-460.el9 rhe-9-for-x86_64-appstream-rpms 57 k
perl-IO              x86_64  1.43-479.el9 rhe-9-for-x86_64-appstream-rpms 102 k
perl-IPC-Open3       noarch    1.21-479.el9 rhe-9-for-x86_64-appstream-rpms 33 k
perl-libnet          noarch    3.13-4.el9 rhe-9-for-x86_64-appstream-rpms 45 k
perl-MIME-Base64      x86_64  3.16-4.el9 rhe-9-for-x86_64-appstream-rpms 34 k
perl-Mozilla-CA       noarch    2020520-6.el9 rhe-9-for-x86_64-appstream-rpms 14 k
perl-NDBM_File       x86_64  1.15-479.el9 rhe-9-for-x86_64-appstream-rpms 33 k
perl-Net-SSLe         x86_64  1.90-8.el9 rhe-9-for-x86_64-appstream-rpms 37 k
perl-POSIX            x86_64  1.94-479.el9 rhe-9-for-x86_64-appstream-rpms 107 k
perl-PathTools        x86_64  1.78-461.el9 rhe-9-for-x86_64-appstream-rpms 92 k
perl-Pod-Escapes      noarch    1.07-460.el9 rhe-9-for-x86_64-appstream-rpms 21 k
perl-Pod-Perldoc      noarch    2.28-461.el9 rhe-9-for-x86_64-appstream-rpms 91 k
perl-Pod-Simple       noarch    3.42-4.el9 rhe-9-for-x86_64-appstream-rpms 228 k
perl-Pod-Usage       noarch    2.01-4.el9 rhe-9-for-x86_64-appstream-rpms 43 k
perl-Scalar-Utils    x86_64  1.56-461.el9 rhe-9-for-x86_64-appstream-rpms 76 k
perl-SelectSaver      noarch    1.02-479.el9 rhe-9-for-x86_64-appstream-rpms 21 k
perl-Socket          x86_64  2.031-4.el9 rhe-9-for-x86_64-appstream-rpms 58 k
perl-Storable        x86_64  3.21-460.el9 rhe-9-for-x86_64-appstream-rpms 97 k
perl-Symbol           noarch    1.08-479.el9 rhe-9-for-x86_64-appstream-rpms 24 k
perl-Term-ANSIColor   noarch    5.01-461.el9 rhe-9-for-x86_64-appstream-rpms 50 k
perl-Term-Cap        noarch    1.17-460.el9 rhe-9-for-x86_64-appstream-rpms 24 k
perl-TermReadKey        x86_64  2.38-11.el9 rhe-9-for-x86_64-appstream-rpms 40 k
perl-Text-ParseWords  noarch    3.30-460.el9 rhe-9-for-x86_64-appstream-rpms 18 k
perl-Text-Tabs+Wrap   noarch    2013.0523-460.el9 rhe-9-for-x86_64-appstream-rpms 25 k
perl-Time-Local      noarch    1.300-7.el9 rhe-9-for-x86_64-appstream-rpms 36 k
perl-URI             noarch    5.09-3.el9 rhe-9-for-x86_64-appstream-rpms 125 k
python3-babel         noarch    2.9.1-2.el9
python3-base         noarch    2.27
python3-cffi          x86_64  1.14.5-4.el9
python3-cryptography   x86_64  3.4.7-5.el9
python3-jinja2        noarch    2.11.3-4.el9
python3-markupsafe    x86_64  1.1.1-12.el9
python3-packaging     noarch    20.9-4.el9
python3-ply           noarch    3.11-13.el9
python3-pyparser      noarch    2.20-5.el9
python3-pyparsing     noarch    2.4.7-7.1.el9
python3-pytz           noarch    2021.1-4.el9
python3-resolvelib      noarch    0.5.4-5.el9
sshpass               x86_64  1.09-4.el9
```

最终交易摘要如下：

```
Transaction Summary
Install 79 Packages
Total download size: 24 M
Installed size: 101 M
Is this ok [y/N]
```

## 执行前

在安装前，使用`dnf`命令查看可用的`ansible-core`信息：

```bash
# dnf info ansible-core
```

输出显示以下内容：

```
Updating Subscription Management repositories.
Last metadata expiration check: 1:41:06 ago on Fri 21 Jan 2022 04:15:49 PM CET.
Available Packages
Name         : ansible-core
Version      : 2.12.1
Release      : 1.el9
Architecture : x86_64
Size         : 2.4 M
Source       : ansible-core-2.12.1-1.el9.src.rpm
Repository   : rhel-9-for-x86_64-appstream-beta-rpms
Summary      : SSH-based configuration management, deployment, and task execution system
URL          : http://ansible.com
License      : GPLv3+
Description  : Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
[root@localhost devops]#
```

## 执行后

安装完成后，再次使用`dnf`命令验证`ansible-core`的安装信息：

```bash
# dnf info ansible-core
```

输出显示以下内容：

```
Updating Subscription Management repositories.
Last metadata expiration check: 1:42:32 ago on Fri 21 Jan 2022 04:15:49 PM CET.
Installed Packages
Name         : ansible-core
Version      : 2.12.1
Release      : 1.el9
Architecture : x86_64
Size         : 9.3 M
Source       : ansible-core-2.12.1-1.el9.src.rpm
Repository   : @System
From repo    : rhel-9-for-x86_64-appstream-beta-rpms
Summary      : SSH-based configuration management, deployment, and task execution system
URL          : http://ansible.com
License      : GPLv3+
Description  : Ansible is a radically simple model-driven configuration management, multi-node deployment, and remote task execution system. Ansible works over SSH and does not require any software or daemons to be installed on remote nodes. Extension modules can be written in any language and are transferred to managed machines automatically.
[root@localhost devops]#
```



# 如何在 Amazon Linux 2 (EC2) 中安装 Ansible

如何使用 Amazon Extras Library 和 `EPEL`（企业级 Linux 额外包）仓库在 Amazon Linux 2 中安装 Ansible。

在 Amazon Linux 2 中安装和维护 Ansible 更简单的方法是使用 Amazon Extras Library 和 `EPEL`。

## 如何在 Amazon Linux 2 中安装 Ansible

Extras Library 中的 `ansible2` 主题

Extra Packages for Enterprise Linux 中的 `ansible`

一种极其简单的模型驱动型配置管理、多节点部署和远程任务执行系统。Ansible 通过 SSH 运行，且不需要在远程节点上安装任何软件或守护进程。扩展模块可以使用任何语言编写，并自动传输到托管机器。

好消息是，通过 `amazon-linux-extras` 命令，在 Amazon Linux 2 仓库的 Extras Library 中已经包含了 `ansible2`。

另一种在 Amazon Linux 2 内部安装和维护 Ansible 的方法是使用企业级 Linux 额外包（`EPEL`）附加仓库。

该仓库由 Fedora 特别兴趣小组维护，为企业级 Linux：Red Hat Enterprise Linux (`RHEL`)、Rocky Linux 和 Scientific Linux (`SL`)、Oracle Linux (`OL`) 以及 Amazon Linux 管理了一组高质量的额外包。

## 链接

- [Amazon Linux 2](https://aws.amazon.com/it/amazon-linux-2/)
- [我如何为运行 CentOS、RHEL 或 Amazon Linux 的 Amazon EC2 实例启用 EPEL 仓库？](https://aws.amazon.com/it/premiumsupport/knowledge-center/ec2-enable-epel/)
- [Extras library (Amazon Linux 2)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-linux-ami-basics.html#extras-library)
- [Extra Packages for Enterprise Linux (EPEL)](https://docs.fedoraproject.org/en-US/epel/)

## 演示

如何使用 Amazon Extras Library 和 `EPEL` 仓库在 Amazon Linux (EC2) 2 中安装 Ansible。

## Amazon Extras Library 代码

`Install-Ansible-Amazon Linux2-Amazon Extras Library.sh`

```bash
#!/bin/bash

sudo yum update -y

sudo amazon-linux-extras install ansible2 -y

ansible --version
```

## Amazon Extras Library 执行

# Amazon Linux 2 Environment Configuration

## 1. Login to the Server
使用 `ssh` 连接至您的 Amazon Linux 2 实例：
```bash
ssh -i key.pem ec2-user@34.241.249.206
```
系统提示：
`-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory`

## 2. Basic Information Check
切换到 `root` 用户并查看系统镜像信息：
```bash
sudo su

cat /etc/image-id
```
输出：
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
cat /etc/os-release
```
输出：
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

## 3. Update Packages
执行 `yum update` 命令：
```bash
yum update
```
输出：
```text
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core | 3.7 kB | 00:00:00
amzn2extra-docker | 3.0 kB | 00:00:00
amzn2extra-kernel-5.10 | 3.0 kB | 00:00:00
No packages marked for update
```

## 4. Install Ansible
使用 `amazon-linux-extras` 安装 `ansible`：
```bash
amazon-linux-extras install all ansible2
```
安装过程：
```text
Installing ansible
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Cleaning repos: amzn2-core amzn2extra-ansible2 amzn2extra-docker amzn2extra-kernel-5.10
17 metadata removed
2 sqlite files removed
0 metadata removed
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core | 3.7 kB | 00:00:00
amzn2extra-ansible2 | 3.0 kB | 00:00:00
amzn2extra-docker | 3.0 kB | 00:00:00
amzn2extra-kernel-5.10 | 3.0 kB | 00:00:00
(1/9): amzn2-core/2/x86_64/group_gz | 2.5 kB | 00:00:00
(2/9): amzn2-core/2/x86_64/updateinfo | 424 kB | 00:00:00
(3/9): amzn2extra-docker/2/x86_64/primary_db | 86 kB | 00:00:00
(4/9): amzn2extra-kernel-5.10/2/x86_64/updateinfo | 76 B | 00:00:00
(5/9): amzn2extra-kernel-5.10/2/x86_64/primary_db | 5.3 MB | 00:00:00
(6/9): amzn2extra-ansible2/2/x86_64/primary_db | 39 kB | 00:00:00
(7/9): amzn2extra-docker/2/x86_64/updateinfo | 4.7 kB | 00:00:00
(8/9): amzn2extra-ansible2/2/x86_64/updateinfo | 76 B | 00:00:00
(9/9): amzn2-core/2/x86_64/primary_db | 58 MB | 00:00:00
Resolving Dependencies
Running transaction check
Package ansible.noarch 0:2.9.23-1.amzn2 will be installed
Processing Dependency: sshpass for ansible-2.9.23-1.amzn2
Processing Dependency: python-paramiko for ansible-2.9.23-1.amzn2
Processing Dependency: python-keyczar for ansible-2.9.23-1.amzn2
Processing Dependency: python-httplib2 for ansible-2.9.23-1.amzn2
Processing Dependency: python-crypto for ansible-2.9.23-1.amzn2
Running transaction check
Package python-keyczar.noarch 0.71c-c.2 will be installed
Package python2-crypto.x86_64 0:2..1-13.amzn2 will be installed
Processing Dependency: libtomcrypt.so.1()(64) for python2-crypto-2.6.13.amzn2
Package python2-httplib2.noarch 0:18.1-3.amzn2 will be installed
Package python2-paramiko.noarch 0:16.1-3.amzn2 will be installed
Processing Dependency: python2-ecdsa for python2-paramiko-16.1-3.amzn2
Package sshpass.x86_64 0.06-1.amzn2 will be stalled
Running transaction check
Package libtomcrypt.x86_64 0:18.2-1.amzn2 will be installed
Processing Dependency: libtommath >= 1.0 for libtomcrypt-18.2-1.amzn2
Processing Dependency: libtommath.so.1()(64) for libtomcrypt-18.2-1.amzn2
Package python2-ecdsa.noarch 0:13.3-1.amzn2 will be installed
Running transaction check
Package libtommath.x86_64 0:1.0-4.amzn2 will be installed
Finished Dependency Resolution
=========================================================
===========================================
Package                Arch          Version               Size
=========================================================
===========================================
Installing:
ansible                noarch         2.9.23-1.amzn2       amzn2extra-ansible2      17 M
Installing for dependencies:
libtomcrypt            x86_64         0.18.2-1.amzn2.0.1   amzn2extra-ansible2      409 k
libtommath             x86_64         0.1.0-4.amzn2.0.1     amzn2extra-ansible2      36 k
python-keyczar          noarch         0.71c-2.amzn2       amzn2extra-ansible2      218 k
python2-crypto          x86_64         2.6.1-13.amzn2.0.3   amzn2extra-ansible2      476 k
python2-ecdsa          noarch         0.13.3-1.amzn2.0.1    amzn2extra-ansible2      94 k
python2-httplib2       noarch         0.18.1-3.amzn2       amzn2extra-ansible2      125 k
python2-paramiko        noarch         0.16.1-3.amzn2.0.2    amzn2extra-ansible2      259 k
sshpass                 x86_64         1.06-1.amzn2.0.1     amzn2extra-ansible2      22 k
Transaction Summary
=========================================
===========================================
Install 1 Package (+8 Dependent packages)
Total download size: 19 M
Installed size: 110 M
Is this ok [y/d/N]: y
Downloading packages:
(1/9): libtomcrypt-1.18.2-1.amzn2.0.1.x86_64.rpm | 409 kB | 00:00:00
(2/9): libtommath-1.0.1-4.amzn2.0.1.x86_64.rpm | 36 kB | 00:00:00
(3/9): python-keyczar-0.71c-2.amzn2.noarch.rpm | 218 kB | 00:00:00
(4/9): python2-crypto-2.6.1-13.amzn2.0.3.x86_64.rpm | 476 kB | 00:00:00
(5/9): ansible-2.9.23-1.amzn2.noarch.rpm | 17 MB | 00:00:00
(6/9): python2-ecdsa-0.13.3-1.amzn2.0.1.noarch.rpm | 94 kB | 00:00:00
(7/9): python2-httplib2-0.18.1-3.amzn2.noarch.rpm | 125 kB | 00:00:00
(8/9): sshpass-1.06-1.amzn2.0.1.x86_64.rpm | 22 kB | 00:00:00
(9/9): python2-paramiko-16.1-3.amzn2.0.2.noarch.rpm | 259 kB | 00:00:00
----------------------------------------
Total                             44 MB/s | 18 MB | 00:00
Running check
Transaction test
Transaction succeeded
Running transaction
Installing: sshpass-1.06-1.amzn2.0.1.x86_64 1/9
Installing: python2-httplib2-0.18.1-3.amzn2.noarch 2/9
Installing: libtommath-1.0.1-4.amzn2.0.1.x86_64 3/9
Installing: libtomcrypt-1.18.2-1.amzn2.0.1.x86_64 4/9
Installing: python2-crypto-2.6.1-13.amzn2.0.3.x86_64 5/9
```



```text
Installing: python-keyczar-0.71c-2.amzn2.noarch 6/9

Installing: python2-ecdsa-0.13.3-1.amzn2.0.1.noarch 7/9

Installing: python2-paramiko-16.1-3.amzn2.0.2.noarch 8/9

Installing: ansible-2.9.23-1.amzn2.noarch 9/9

Complete!

ansible=latest enabled [2.4.2=2.4.6]
```

## 5. Verify Installation

Check `ansible` version:

```bash
ansible --version
```

Output:

```text
ansible 2.9.23

  config file = /etc/ansible/ansible.cfg

  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']

  ansible python module location = /usr/lib/python2.7/site-packages/ansible

  executable location = /bin/ansible

  python version = 2.7.18 (default, Jun 10 2021, 00:11:02) [GCC 7.3.1 20180712 (Red Hat 7.3.1-13)]
```

Confirm the package is installed:

```bash
rpm -qa | grep ansible
```

Output:

`ansible-2.9.23-1.amzn2`

## 执行后的 Amazon Extras 库

```text
1 # rpm -qa | grep ansible
2 ansible-2.9.23-1.amzn2.noarch
```

## EPEL 代码

### `Install-Ansible-Amazon Linux2-EPEL.sh`

```bash
1 #!/bin/bash

2 $ sudo amazon-linux-extras install epel -y

3 $ sudo yum repolist

4 $ sudo yum-config-manager --enable epel

5 $ sudo amazon-linux-extras disable ansible2

6 $ sudo yum --enablerepo epel install ansible

7 $ ansible --version
```

## EPEL 执行

# Ansible 相关操作日志

```bash
yum remove ansible

Failed to set locale, defaulting to C

Loaded plugins: extras_suggestions, langpacks, priorities, update-motd

Resolving Dependencies

--> Running transaction check

---> Package ansible.noarch 0:2.9.23-1.amzn2 will be erased

--> Finished Dependency Resolution

Dependencies Resolved

========================================================

==========================================

Package          Arch             Version            Repository               Size

========================================================

==========================================

Removing:

ansible          noarch          2.9.23-1.amzn2      @amzn2extra-ansible2      105 M

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

```bash
[root@ip-172-31-36-49 ec2-user]# amazon-linux-extras install all epel

Installing epel-release

Failed to set locale, defaulting to C

Loaded plugins: extras_suggestions, langpacks, priorities, update-motd

Cleaning repos: amzn2-core amzn2extra-ansible2 amzn2extra-docker amzn2extra-epel              : amzn2extra-kernel-5.10

22 metadata files removed

8 sqlite files removed

0 metadata files removed

Failed to set locale, defaulting to C

Loaded plugins: extras_suggestions, langpacks, priorities, update-motd

amzn2-core                           | 3.7 kB  00:00:00

amzn2extra-ansible2                  | 3.0 kB  00:00:00

amzn2extra-docker                    | 3.0 kB  00:00:00

amzn2extra-epel                     | 3.0 kB  00:00:00

amzn2extra-kernel-5.10               | 3.0 kB  00:00:00

(1/11) amzn2-core/2/x86_64/group_gz   | 2.5 kB  00:00:00

(2/11) amzn2-core/2/x86_64/updateinfo  | 424 kB  00:00:00

(3/11) amzn2extra-docker/2/x86_64/primary_db  | 86 kB  00:00:00

(4/11) amzn2extra-epel/2/x86_64/updateinfo  | 76 B  00:00:00

(5/11) amzn2extra-epel/2/x86_64/primary_db  | 1.8 kB  00:00:00

(6/11) amzn2extra-kernel-5.10/2/x86_64/updateinfo  | 76 B  00:00:00

(7/11) amzn2extra-kernel-5.10/2/x86_64/primary_db  | 5.3 MB  00:00:00

(8/11) amzn2extra-ansible2/2/x86_64/updateinfo  | 76 B  00:00:00

(9/11) amzn2extra-docker/2/x86_64/updateinfo  | 4.7 kB  00:00:00

(10/11) amzn2extra-ansible2/2/x86_64/primary_db  | 39 kB  00:00:00

(11/11) amzn2-core/2/x86_64/primary_db  | 58 MB  00:00:00

Resolving Dependencies

--> Running transaction check

---> epel-release.noarch 0:7-1 will be installed

--> Dependency Resolution

Dependencies Resolved

========================================================

==========================================

Package          Arch             Version            Repository               Size

========================================================

==========================================

Installing:

epel-release       noarch          7-1            amzn2extra-epel      15 k

Transaction Summary

========================================================

==========================================

Install 1 Package

Total download size: 15 k

Installed size: 24 k

Is this ok [y/d/N]: y

Downloading packages:

epel-release-7-1.noarch.rpm               | 15 kB  00:00:00

Running transaction check

Running transaction test

Transaction test succeeded

Running transaction

  Installing : epel-release-7-11.noarch            1/1

  Verifying  : epel-release-7-11.noarch            1/1

Installed:

  epel-release.noarch 0:7-11

Complete!
```



# 在 Amazon Linux 中通过 EPEL 安装 Ansible

## 启用 EPEL 仓库

执行以下命令启用 EPEL 仓库：

```
[root@ip-172-31-36-49 ec2-user]# yum-config-manager --enable epel
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
===========================
repo: epel
===========================
async = True
bandwidth = 0
basedir = /var/lib/yum/repos/x86_64/2
baseurl =
cache = 0
cachedir = /var/cache/yum/x86_64/2/epel
config_file_age = True
compare_providers = 80
cost = 1000
deltarpm_metadata_percentage = 100
enabled = True
groups = True
exclude =
ftp_disable = False
gpgdir = /var/lib/yum/repos/x86_64/2/epel
gpgcheck = True
gpgdir = /var/lib/yum/repos/x86_64/2/epel
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL
hdrdir = /var/cache/yum/x86_64/2/epel/headers
http_caching = all
includepages =
ip_resolve = True
keepcache = False
mdloadpolicy = sqlite
mdpolicy = group:small
mediaid =
metadata_expire = 21600
metadata_expire = read-only
metalink = https://mirrors.fedoraproject.org/metalink?repo=epel-7&arch=x86_64
minrate = 0
mirrorlist =
mirrorlist_expire = 86400
name = Extra Packages for Enterprise Linux 7 - x86_64
old_base_cache_dir =
password =
persistdir = /var/lib/yum/repos/x86_64/2/epel
pkgdir = /var/cache/yum/x86_64/2/epel/packages
priority = 99
proxy = False
proxy_dict =
proxy_password =
proxy_username =
repo_gpgcheck = False
report_instance = False
retries = 7
skip_if_unavailable = False
ssl_check_permissions = True
sslcert =
sslkey =
sslverify = True
throttle = 0
timeout = 5.0
ui_id = epel/x86_64
uirepo_vars = releasever,basearch
username =
```

## 安装 Ansible

```
[root@ip-172-31-36-49 ec2-user]# yum --enable po install ansible
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                           | 3.7 kB  00:00:00
amzn2extra-docker                    | 3.0 kB  00:00:00
amzn2extra-epel                     | 3.0 kB  00:00:00
amzn2extra-kernel-5.10               | 3.0 kB  00:00:00
epel/x86_64/metalink                 | 21 kB  00:00:00
209 packages excluded to repository priorities
Resolving Dependencies
--> Running transaction check
---> ansible.noarch 0:2.9.25-el7 will be installed
--> Dependency Resolution
Dependencies Resolved
========================================================
==========================================
Package          Arch             Version            Repository               Size
========================================================
==========================================
Installing:
ansible          noarch          2.9.25-el7            epel                      17 M
Transaction Summary
========================================================
==========================================
Install 1 Package
Total download size: 17 M
Installed size: 103 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/2/epel/packages/ansible-2.9.25-1.el7.noarch.rpm: Header V4 RSA/SHA256 Signature, key ID352c64e5: NOKEY
Public key for ansible-2.9.25-1.el7.noarch.rpm is not installed
ansible-2.9.25-1.el7.noarch.rpm               | 17 MB  00:00:03
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Importing GPG key 0x352C64E5:
Userid  : "Fedora EPEL (7) <epel@fedoraproject.org>"
Fingerprint: 91e97d7c4a5e96f17f3e888f6a2feea2352c64e5
Package  : epel-release-7-11.noarch (@amzn2extra-epel)
From  : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : ansible-2.9.25-1.el7.noarch            1/1
  Verifying  : ansible-2.9.25-1.el7.noarch            1/1
Installed:
  ansible.noarch 0:2.9.25-el7
Complete!
```

## 验证安装

```bash
[root@ip-172-31-36-49 ec2-user]# ansible --version
ansible 2.9.25
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /bin/ansible
  python version = 2.7.18 (default, Jun 10 2021, 00:11:02 ) [GCC 7.3.1 20180712 (Red Hat 7.3.1-13)]
```

```bash
[root@ip-172-31-36-49 ec2-user]# rpm -qa | grep ansible
ansible-2.9.25-1.el7.noarch
```

## 执行后的 EPEL

```
1 # rpm -qa | grep ansible
2 ansible-2.9.25-1.el7.noarch
```

# 回顾

现在你知道了如何使用 Amazon Extras Library 和 EPEL 仓库在 Amazon Linux 中安装最新版本的 Ansible。

## 如何在 Debian 11 中安装 Ansible

使用`APT`和“main”默认仓库在 Debian 11 中安装最新版本的 Ansible 并保持更新的更简单方法。

## 如何在 Debian 中安装 Ansible

### 包含在“main”默认仓库中

好消息是 Ansible 包含在默认仓库中，因此你可以简单地使用你常用的包管理器`apt`来安装它。

你可以期待在“main”仓库中获得最新版本的 Ansible。

## 演示

如何使用`apt`包管理器和“main”默认仓库在 Debian 中安装 Ansible。

## 代码

`install-ansible-debian.sh`

```
1 #!/bin/bash
2 $ sudo apt-get update
3 $ sudo apt-get install ansible
4 $ sudo apt list –installed ansible
```

## 执行

# Debian 系统环境与 Ansible 安装

```bash
ansible-pilot $ ssh devops@debian.example.com

Linux debian 5.10.0-9-amd64 #1 SMP Debian 5.10.70-1 (2021-09-30) x86_64

The programs included with the Debian GNU/Linux system are free software; the exact distribution terms for each program are described in the individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
```

```bash
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
```

```bash
root@debian:/home/devops# cat /etc/deb
debconf.conf    debian_version
root@debian:/home/devops# cat /etc/debian_version
11.1
```

## 更新软件包列表

```bash
root@debian:/home/devops# apt-get update
Get:1 http://security.debian.org/debian-security bullseye-security InRelease [44.1 kB]
Hit:2 http://deb.debian.org/debian bullseye InRelease
Get:3 http://deb.debian.org/debian bullseye-updates In [39.4 kB]
Get:4 http://deb.debian.org/debian bullseye-backports Release [43.7 kB]
Get:5 http://deb.debian.org/debian bullseye-backports/main Sources.diff/Index [63.3 kB]
Get:6 http://deb.debian.org/debian bullseye-backports/main amd64 Packages.diff/Index [63.3 kB]
Get:7 http://deb.debian.org/debian bullseye-backports/main Sources T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [29 B]
Get:7 http://deb.debian.org/debian bullseye-backports/main Sources T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [29 B]
Get:8 http://deb.debian.org/debian bullseye-backports/main amd64 Packages T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [257 B]
Get:8 http://deb.debian.org/debian bullseye-backports/main amd64 Packages T-2021-12-02-0202.04-F-2021-12-02-0202.04.pdiff [257 B]
Fetched 254 kB in 1s (488 kB/s)
Reading package lists... Done
```

## 搜索 Ansible

```bash
root@debian:/home/devops# apt-cache search ansible
ansible - Configuration management, deployment, and task execution system
ansible-lint - lint tool for Ansible playbooks
ansible-mitogen - Fast connection strategy for Ansible
shade-inventory - Ansible inventory script for OpenStack clouds
python3-reclass - hierarchical inventory backend for configuration management systems
reclass - hierarchical inventory backend for configuration management systems
reclass-doc - reclass documentation
vim-syntastic - Syntax checking hacks for vim
```

## 查看 Ansible 信息

```bash
root@debian:/home/devops# apt-cache show ansible
Package: ansible
Version: 2.10.7+merged+base+2.10.8+dfsg-1
Installed-Size: 198790
Maintainer: Lee Garrett <debian@rocketjump.eu>
Architecture: all
Replaces: ansible-base (<= 2.10.5+dfsg-2)
Depends: python3-cryptography, python3-jinja2, python3-packaging, python3-yaml, python3:any, openssh-client | python3-paramiko (>= 2.6.0), python3-pycryptome, python3-distutils, python3-dnspython, python3-httplib2, python3-netaddr
```



Recommends: `python3-argcomplete`, `python3-jmespath`, `python3-kerberos`, `python3-libcloud`, `python3-selinux`, `python3-yaml`, `python3-todict`

Suggests: `cowsay`, `sshpass`

Breaks: `ansible-base` (<= 2.10.5+dfsg-2)

Description-en: Configuration management, deployment, and task execution system Ansible is a radically simple-driven configuration management, multi-node deployment, and remote execution system. Ansible works over SSH and does not require any daemons to be installed on remote nodes. Modules can be written in any language and are transferred to managed machines automatically. This package contains `ansible-base` 2.10.x and `ansible-collections` 2.10.x merged into one package.

Description-md5: `de0a87781a6b86ca20d1d4ce8`

Homepage: https://www.ansible.com

Tag: automation,configuring,distribution,package-management,implemented-in:python,line,program,running,works-with:software

Section: admin

Priority: optional

Filename: `pool/main/ansible/ansible_2.10.7+merged+base+2.10.8+dfsg-1_all.deb`

Size: 17685468

MD5sum: `159657e0be3d3f21fde43db1ac98cd`

SHA256: `6647417b31f9b0bc816331c5f7424c7a49db50d`

## 安装 Ansible

```bash
root@debian:/home/devops# apt-get install ansible

Reading package lists... Done

Building dependency tree...

Reading state... Done

The following additional packages will be installed:

  ieee-data python3-argcomplete python3-cffi-backend python3-cryptography python3-distutils python3-dnspython python3-jinja2 python3-kerberos python3-libcloud python3-lockfile python3-markafe python3-netaddr python3-nss python3-packaging python3-pycryptome python3-pyparsing python3-requests python3-selinux python3-simple python3-todict python3-winrm python3-yaml-02

The following NEW packages will be installed:

  ansible ieee-data python3-argcomplete python3-cffi-backend python3-cryptography python3-distutils python3-dnspython python3-yaml-02 python3-jinja2 python3-jmespath python3-kerberos python3-libcloud python3-lockfile python3-markafe python3-netaddr python3-nss python3-packaging python3-pycryptome python3-pyparsing python3-requests python3-selinux python3-simple python3-todict python3-winrm

32 packages installed, 0 upgraded, 0 to remove and REQUIRED.

Do you want to continue? [Y/n] y

...
```

## 验证安装

```bash
root@debian:/home/devops# ansible --version

ansible 2.10.8

  config file = None

  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']

  ansible python module location = /usr/lib/python3/dist-packages/ansible

  executable location = /usr/bin/ansible

  python version = 3.9.2 (default, Feb 28 2021, 17:03:44)

[GCC 10.2.1 2021010]
```

```bash
root@debian:/home/devops# apt list | grep ansible

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

ansible-lint/stable 4.3.7-1 all

ansible-mitogen/stable 0.3.0~rc1-4 all

ansible/stable,now 2.10.7+merged+base+2.10.8+dfsg-1 all [installed]
```

## 执行前

```bash
$ ssh devops@debian.example.com

2 Linux debian 5.10.0-9-amd64 #1 SMP Debian 5.10.70-1 (2021-3-09-30) x86_64 4 The programs included with the Debian GNU/Linux system are 5 free software; 6 the exact distribution terms for each program are described in the 8 individual files in /usr/share/doc/*/copyright. 9 Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent 11 permitted by applicable law. 12

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

```bash
root@debian:/home/devops# apt list ansible --installed

Listing... Done

ansible/stable,now 2.10.7+merged+base+2.10.8+dfsg-1 all [installed]

root@debian:/home/devops# dpkg -l | grep ansible

ii  ansible                      2.10.7+merged+base+2.10.8+dfsg-1 all      Configuration management, deployment, and task execution system

root@debian:/home/devops#
```

## Linux 版 Ansible

在本章中，你将发现最常用的 Ansible 模块，用于自动化 Linux 管理员任务。

## Ansible 术语 - `ansible_hostname` vs `inventory_hostname` vs `ansible_fqdn`

在 Playbook 的实际示例中，`ansible_hostname`、`inventory_hostname` 和 `ansible_fqdn` 之间的区别是什么？这两个内部变量有时会让人混淆，但它们从本质上是不同的。

## `ansible_hostname` vs `inventory_hostname` vs `ansible_fqdn`

`ansible_hostname` 和 `ansible_fqdn` 从目标机器的事实（facts）中读取：`ansible_hostname` 从 `gather_facts` 期间收集的事实读取主机名。类似于 `uname -n` 命令。需要启用 `gather_facts`，否则 `ansible_facts` 变量将无法在 playbook 中使用。它等同于目标主机的主机名。

`inventory_hostname` 从 Ansible 清单（inventory）或文件读取：它从 `inventory` 配置或 hosts 文件读取主机名。它可能与远程系统的主机名不同。它可能只是控制机上的一个名称，始终可以在你的 playbook 中使用。对于 playbook 和即时命令（ad-hoc command），它都可能与目标主机的主机名不同。

## 演示

让我通过一个简单的 Playbook 向你展示 `ansible_hostname`、`inventory_hostname` 和 `ansible_fqdn` 内部变量之间的区别。

```yaml
---
- name: hostnames

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

执行

```bash
ansible-pilot $ ansible-playbook -i statements/hostnames.yml

PLAY [hostnames] *************************************************

TASK [Gathering Facts] *************************************************

ok: [foo.example.com]

TASK [print inventory_hostname] *************************************

ok: [foo.example.com] => {

    "inventory_hostname": "foo.example.com"

}

TASK [print ansible_hostname] *****************************************

ok: [foo.example.com] => {

    "ansible_hostname": "demo"

}

TASK [print ansible_fqdn] ****************************************

ok: [foo.example.com] => {

    "ansible_fqdn": "demo.example.com"

}

PLAY RECAP *****************************************************************

foo.example.com: ok=4    changed=0  unreachable=0  failed=0  skipped=0  rescued=0  ignored=0

ansible-pilot $
```

#### 等等性（Idempotency）

```bash
ansible-pilot $ ansible-playbook -i statements/hostnames.yml

PLAY [hostnames] *************************************************

TASK [Gathering Facts] *************************************************

ok: [foo.example.com]

TASK [print inventory_hostname] *************************************

ok: [foo.example.com] => {

    "inventory_hostname": "foo.example.com"

}

TASK [print ansible_hostname] *****************************************

ok: [foo.example.com] => {

    "ansible_hostname": "demo"

}

TASK [print ansible_fqdn] ****************************************

ok: [foo.example.com] => {

    "ansible_fqdn": "demo.example.com"

}

PLAY RECAP *****************************************************************

foo.example.com: ok=4    changed=0  unreachable=0  failed=0  skipped=0  rescued=0  ignored=0
```

## 总结

现在你对内部变量 `ansible_hostname`、`inventory_hostname` 和 `ansible_fqdn` 有了更多了解。

```yaml
---
- name: harmful playbook

  hosts: all

  tasks:

    - name: harmful task

      ansible.builtin.debug:

        msg: "harmful task"
```

### 执行结果

```bash
ansible-pilot $ ansible-playbook --limit demo.example.com -i limit/inventory limit/playbook.yml

PLAY [harmful playbook] *****************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************

ok: [demo.example.com]

TASK [harmful task] *****************************************************************************************************

ok: [demo.example.com] => {

    "msg": "harmful task"

}
```



```text
PLAY RECAP *********************************************************************************************************************

demo.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible-pilot $
```

### 错误的执行

如果我们忘记了`--limit`选项，结果可能会非常有害。

```bash
ansible-pilot $ ansible-playbook -i limit/inventory limit /playbook.yml

PLAY [harmful playbook] *****************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************

ok: [demo.example.com]

ok: [demo2.example.com]

TASK [harmful task] *****************************************************************************************************

ok: [demo.example.com] => {
    "msg": "harmful task"
}

ok: [demo2.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP *********************************************************************************************************************

demo.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

demo2.example.com         : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible-pilot $
```

## Ansible Playbook 主机

`hosts: HOSTNAME`

`ansible-playbook PLAYBOOK`

在 Ansible Playbook 中使用`hosts`语句允许你为执行指定特定的主机或主机组。

其优点是，这比在命令行上使用`--limit`参数手动指定主机名更可靠。

缺点是，你每次都必须记得编辑 Ansible Playbook 代码。如果你忘记这样做，你将在指定的主机上执行代码，这仍然是一个潜在的人工操作问题。

### 代码示例

`playbook2.yml`

```yaml
---
- name: harmful playbook
  hosts: demo.example.com
  tasks:
    - name: harmful task
      ansible.builtin.debug:
        msg: "harmful task"
```

### 执行结果

```bash
ansible-pilot $ ansible-playbook -i limit/inventory limit /playbook2.yml

PLAY [harmful playbook] *****************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************

ok: [demo.example.com]

TASK [harmful task] *****************************************************************************************************

ok: [demo.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP *********************************************************************************************************************

demo.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible-pilot $
```

## Ansible Playbook 主机高级用法

`hosts: "{{ HOSTS }}"`

`ansible-playbook -e "HOSTS=demo.example.com" PLAYBOOK`

在 Ansible Playbook 中使用`hosts`语句允许你指定一个变量，你可以通过该变量为执行填充一个主机或主机组。

基本上，如果你在命令行上盲目执行 Ansible Playbook 代码，它将无所作为。唯一的处理方法是通过命令行通过额外变量来填充主机变量。

其优点是，这比使用`--limit`参数手动指定主机名更可靠。

### 代码示例

`playbook3.yml`

```yaml
---
- name: harmful playbook
  hosts: "{{ HOSTS }}"
  tasks:
    - name: harmful task
      ansible.builtin.debug:
        msg: "harmful task"
```

### 执行结果

```bash
ansible-pilot $ ansible-playbook -i limit/inventory -e "HOSTS=demo.example.com" /playbook3.yml

PLAY [harmful playbook] *********************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************

ok: [demo.example.com]

TASK [harmful task] *****************************************************************************************************

ok: [demo.example.com] => {
    "msg": "harmful task"
}

PLAY RECAP ********************************************************************************************************************

demo.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible-pilot $
```

## 链接

[模式：目标主机和组](https://docs.ansible.com/ansible/latest/user_guide/intro_patterns.html)

## 测试主机可用性：Ansible ping

让我们谈谈 Ansible`ping`模块。它的全名是`ansible.builtin.ping`，这意味着它是`builtin`模块集合的一部分并随 Ansible 一起发布。这是一个非常稳定且存在多年的模块。它验证 Ansible 能够登录到被管理主机，并且存在可以执行我们代码的 Python 解释器。因此，在网络上下文中它非常不同。它是 Windows 对应的`win_ping`模块。

### 主要参数和返回值

- `data`字符串：人们通常不指定任何参数或使用返回值。对于参数，可以将行为从默认的`pong`更改为在失败时抛出异常的`crash`。
- `ping`字符串：默认默认值为`pong`字符串，但你可以通过`data`参数进行自定义。

### 示例

如何使用`ping`模块测试主机可用性。

```yaml
---
- name: ping demo
  hosts: all
  become: false
  tasks:
    - name: test connection
      ansible.builtin.ping:
```

在接下来的示例中，我们将超越打印“Hello world!”文本的范畴，通过打印文本、变量、文本与变量，并向你演示如何使用详细程度级别（verbosity level）。

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

在本章中，你将发现如何从 Ansible Galaxy 远程目录下载并使用 Ansible Roles 和 Collection（集合）。

## 下载并使用 Ansible Galaxy Role：ansible-galaxy 和 requirements.yml

如何下载并使用 Ansible Role`lucab85.ansible_role_log4shell`来扫描我们的 Linux 机器，以检查 Log4Shell 远程代码执行 Log4j（CVE-2021–44228），并复用在 Ansible Galaxy 目录中发布的 Ansible 制品（任务、变量、默认值、处理器、模块和插件）。

## 什么是 Ansible Role？

- 可复用的 Ansible 制件
- 一个角色包含任务、变量、默认值、处理器、模块或其他插件
- 可以通过 Ansible Galaxy 轻松下载和共享

Ansible Role 是一组可复用的 Ansible 制件。它解决一个问题并包含所有相关的任务、变量、默认值、处理器、模块或其他插件。

对于用户来说，Ansible Role 容易通过 Ansible Galaxy 下载和共享。对于开发者来说，Ansible Role 容易通过 Ansible Galaxy 上传和共享。此外，Ansible Role 具有定义的标准目录结构和格式。

## 什么是 Ansible Galaxy？

[Ansible Galaxy](https://galaxy.ansible.com/)

[lucab85/ansible_role_log4shell](https://galaxy.ansible.com/lucab85/ansible_role_log4shell)

该网站可以通过 URL`https://galaxy.ansible.com/`访问。搜索引擎、标签和平台让你轻松找到其中的任何内容。

我建议你在将其用于系统之前，仔细评估其内容的质量。

质量指标通常包括代码质量保证、支持的操作系统和平台、文档、发布版本、是否存在变更日志（Changelog）、下载次数以及作者或创建。

请注意，该网站包含了 Ansible Roles 和 Ansible Collections。今天我们关注的是 Ansible Role 内容。

## 链接

- `https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse.html`
- `https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#using-roles`
- `https://galaxy.ansible.com/`
- `https://galaxy.ansible.com/lucab85/ansible_role_log4shell`

## demo

让我们进入真实场景：如何下载并使用 Ansible Galaxy Role`lucab85.ansible_role_log4shell`。

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

错误似乎出现在 '/Users/lberton/prj/github/ansible-pilot/galaxy/role.yml'：第 5 行，第 8 列，但根据具体的语法问题，也可能在文件的其他位置。

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

PLAY [role demo] *****************************************************

TASK [Gathering Facts] *************************************************

ok: [localhost]

TASK [lucab85.ansible_role_log4shell : dependency present] *****************

changed: [localhost]

... (skipped tasks)

TASK [lucab85.ansible_role_log4shell : create directory] *****************

changed: [localhost]

...
```



# Ansible 执行结果

```text
PLAY RECAP *************************************************************

localhost                  : ok=14    changed=9    unreachable=0    failed=0    skipped=1    rescued=0
```

请注意，网站包含 `Ansible Roles` 和 `Ansible Collections`。今天我们关注的是 `Ansible Role` 内容。

## 链接

- [Ansible Collections 列表](https://github.com/ansible-collections)
- [Ansible Collections 开发指南](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections.html)
- [Ansible Collections 迁移角色](https://docs.ansible.com/ansible/latest/dev_guide/migrating_roles.html)
- [community.general collection](https://docs.ansible.com/ansible/latest/collections/community/general/)

## Demo

让我们在安装了 `ansible-core` 的系统中，进入一个真实的场景——“如何下载并使用 Ansible Galaxy Collection” `community.general`。

### 代码

`collection.yml`

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

`requirements.yml`

```yaml
---
collections:
  - name: community.general
    source: https://galaxy.ansible.com
```

### 在未安装 Collection 时执行

```bash
$ ansible-playbook collection/collection.yml

[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

ERROR! couldn't resolve module/action 'community.general.modprobe'. This often indicates a misspelling, missing collection, or incorrect module path.

错误似乎出现在 '/home/devops/collection/collection.yml': 第 10 行，第 7 列，但可能在文件的其他位置，取决于具体的语法问题。

出现问题的行似乎是：

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

### 列出已安装的 Collection

```bash
$ ansible-galaxy collection list

# /home/devops/.ansible/collections/ansible_collections

Collection        Version
----------------- -------
community.general 4.5.0

$
```

### 安装 Collection 后执行

```bash
$ ansible-playbook collection/collection.yml

[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [modprobe module demo] *****************************

******************************************

TASK [Gathering Facts] *************************************

******************************************

ok: [localhost]

TASK [load the module] *************************************

******************************************

changed: [localhost]

PLAY RECAP **********************************************

******************************************

localhost                   : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

$
```

## Ansible 用于 Linux 文件系统

如何使用 Ansible 自动化与 Linux 文件系统的交互。例如：文件和目录的创建、权限和删除。

## 创建空文件：Ansible 模块

如何创建一个空的 `~/example.txt` 文件或更新已创建的时间。

### Ansible 创建空文件

让我们来聊聊 Ansible 模块。它的全名是 `ansible.builtin.file`，这意味着它是 Ansible 内置 `builtin` 模块集合的一部分，并随 Ansible 一起发布。

这是一个非常稳定的模块，已经发布多年。它可以在多种操作系统上运行。它管理文件和文件属性。

对于 Windows 目标，请使用 `ansible.windows.win_file` 模块。

### 主要参数

- `path` string (`dest`, `name`) - 文件路径
- `state` string - 文件/不存在 (`file`/`absent`)

它管理文件和文件属性。对于 Windows 目标，请使用 `ansible.windows.win_file` 模块。

### Demo

`file.yml`

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

今天我们来讨论 Ansible 模块文件。

它的全名为 `ansible.builtin.file`，这意味着它是 `ansible` 内置 `builtin` 模块集合的一部分，并随其一同发布。

这是一个非常稳定且已发布多年的模块。它适用于多种操作系统。它用于管理文件和文件属性。

对于 Windows 目标，请使用 `ansible.windows.win_file` 模块。

## 参数

- `path` 字符串 (`dest`, `name`) - 文件路径
- `state` 字符串 - `file/absent/directory/hard/link/touch`
- `mode`/`owner`/`group` - 权限
- `setype`/`seuser`/`selevel` - SELinux

该模块拥有一些参数来执行任务。

必需的参数是 `path`，你可以在此处指定要编辑的文件的文件系统路径。

`state` 定义了我们要修改的对象类型，默认值为 `file`，但对于我们的使用场景，我们需要 `directory` 选项。

## 演示

如何使用 Ansible 的 `file` 模块在 Linux 的 `devops` 用户家目录下创建 `example` 目录。

### 代码

`create_directory.yml`

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

### 执行

```bash
$ ansible-playbook -i demo/inventory create_directory/file.yml

PLAY [file module demo] *********************************

************************************

TASK [Gathering Facts] ***********************************

************************************

ok: [demo.example.com]

TASK [Creating a directory] *****************************

************************************

changed: [demo.example.com]

PLAY RECAP **********************************************

************************************

demo.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### 执行前

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

### 执行后

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

[devops@demo ~]$
```

## 如何在 Ansible 中检查目录是否存在？

使用 `stat` 模块来验证目录是否存在。其全名为 `ansible.builtin.stat`，这意味着它是 `ansible` 内置 `builtin` 模块集合的一部分，并随其一同发布。这是一个非常稳定且已发布多年的模块。它适用于多种操作系统。它获取文件系统的状态。对于 Windows 目标，请使用 `ansible.windows.win_stat` 模块。

## 主要参数和返回值

- `path`：强制参数是 `path`，是要检查的对象的文件系统完整路径。
- `stat`：模块返回一个复杂对象，我们感兴趣的属性是 `isdir`。如果对象是目录，则该属性为 `true`。

## 演示

让我们进入一个真实的 playbook 来检查目录是否存在。

### 代码

`directory_check_exists.yml`

```yaml
---
- name: check if the directory exists
  hosts: all
  become: false
  vars:
    directory: "/tmp"
  tasks:
    - name: Check if exists
      ansible.builtin.stat:
        path: "{{ directory }}"
      register: check_file_name

    - name: Directory found
      ansible.builtin.debug:
        msg: "{{ directory }} present"
      when: check_file_name.stat.isdir
```

# Ansible 执行输出

```bash
$ ansible-playbook -i demo/inventory rename/file.yml

PLAY [重命名文件或目录] *********************************

***************************************************

TASK [收集信息] ***********************************

***************************************************

ok: [demo.example.com]

TASK [检查文件是否存在] *****************************

***************************************************

ok: [demo.example.com]

TASK [打印调试信息] **************************************
```



***************************************************

```
ok: [demo.example.com] => {

    "check_file_name": {

        "changed": false,

        "failed": false,

        "stat": {

            "exists": false

        }

    }

}
```

TASK [使用新名称复制文件] **************************

***************************************************

```
skipping: [demo.example.com]
```

TASK [删除旧文件] ***********************************

***************************************************

```
skipping: [demo.example.com]
```

PLAY RECAP **********************************************

***************************************************

```
demo.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
```

## 输出文件存在

```bash
$ ansible-playbook -i demo/inventory rename/file.yml
```

```
PLAY [重命名文件或目录] *********************************

***************************************************

TASK [收集信息] ***********************************

***************************************************

ok: [demo.example.com]

TASK [检查文件是否存在] *****************************

***************************************************

ok: [demo.example.com]

TASK [打印调试信息] **************************************

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

            "checksum": "da39a3ee5e6b4b0d3255bfef95601890afdd80709",

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
```

TASK [使用新名称复制文件] **************************

***************************************************

```
changed: [demo.example.com]
```

TASK [删除旧文件] ***********************************

***************************************************

```
changed: [demo.example.com]
```

PLAY RECAP **********************************************

***************************************************

```
demo.example.com          : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## 输出目录存在

```bash
$ ansible-playbook -i demo/inventory rename/file.yml
```

```
PLAY [重命名文件或目录] *********************************

***************************************************

TASK [收集信息] ***********************************

***************************************************

ok: [demo.example.com]

TASK [检查文件是否存在] *****************************

***************************************************

ok: [demo.example.com]

TASK [打印调试信息] **************************************

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

            "mimetype": "inode/empty",

            "mode": "0644",

            "mtime": 1632319779.5021598,

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
```

TASK [使用新名称复制文件] **************************

***************************************************

```
ok: [demo.example.com]
```

TASK [删除旧文件] ***********************************

***************************************************

```
ok: [demo.example.com]
```

PLAY RECAP **********************************************

***************************************************

```
demo.example.com          : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

# 修改文件权限 - Ansible file 模块

如何使用 Ansible 修改文件或目录权限？

我将向你演示如何修改`test.txt`文件的`chmod`和用户组。

如何自动化修改文件/目录权限？

今天我们讨论的是`file`模块。它的全名是`ansible.builtin.file`，这意味着它是`builtin`模块集合的一部分，并随 ansible 一起发布。这是一个非常稳定且已发布多年的模块。它支持不同的操作系统。它可以管理文件及其属性。对于 Windows 目标，请使用`ansible.windows.win_file`模块。

## 主要参数

- `path` (`dest`, `name`): 文件路径
- `owner`: 用户
- `group`: 组
- `mode` 原始字符串：例如`0644`或`u=rw,g=r,o=r`
- `state`: `file`/absent`/directory`/hard`/link`/touch`
- `setype`/`seuser`/`selevel`: SELinux

该模块包含一些参数用于执行任务。唯一的必填参数是`path`，你可以在这里指定要编辑的文件系统路径。`owner` 参数设置文件/目录的所有者。`group` 参数设置文件/目录的所属组。

`mode` 参数以 UNIX 方式设置文件/目录的权限。

`state` 定义了我们正在修改的对象类型，默认是`file`，但我们也可以处理目录、硬链接、符号链接，或通过`touch` 选项仅更新访问时间。

让我也强调一下，我们还可以指定 SELinux 属性。

## demo

让我们进入一个真实的剧本（playbook），使用 Ansible 修改文件权限。

```yaml

file.yml

1 --- 2 - name: file module demo 3   hosts: all 4   vars: 5     myfile: "/home/devops/test.txt" 6   become: false 7   tasks: 8     - name: check permission 9       ansible.builtin.file: 10         path: "{{ myfile }}" 11         owner: "devops" 12         group: "users" 13         mode: '0777'
```



# 为 Linux 文件添加执行权限 755——Ansible `file` 模块

如何使用 Ansible 的 `file` 模块自动化地为 `example.sh` Linux 文件设置 755 执行权限。

在 Linux 中分配执行权限 755 是系统管理员非常频繁的需求，你可以通过 Ansible 实现其自动化。

## Ansible 添加执行权限

`ansible.builtin.file`

管理文件和文件属性。

今天我们来讨论 Ansible 模块 `file`。

它的全名是 `ansible.builtin.file`，这意味着它是 `builtin` 模块集合的一部分，并随 Ansible 一起分发。

这是一个非常稳定且已发布多年的模块。

它可以在不同的操作系统上运行。

它管理文件和文件属性。

对于 Windows 目标，请使用 `ansible.windows.win_file` 模块。

## 主要参数

- `path` string (`dest`、`name`)——文件路径
- `owner` string——用户
- `group` string——组
- `mode` raw——例：`0644` 或 `u=rw,g=r,o=r`
- `state` string——`file`/`absent`/`directory`/`hard`/`link`/`touch`
- `setype`/`seuser`/`selevel`——SELinux

该模块有一些参数来执行任何任务。

唯一要求的参数是 `path`，你可以在此指定要编辑的文件的文件系统路径。

`owner` 参数设置应拥有该文件或目录的用户。

`group` 参数设置应拥有该文件或目录的组。

`mode` 参数以 UNIX 方式设置文件或目录的权限。

`state` 定义了我们正在修改的对象类型，默认是 `file`，但我们也可以处理目录、硬链接、符号链接，或通过 `touch` 选项仅更新访问时间。

让我也强调一下，我们还可以指定 SELinux 属性。

## Links

[`ansible.builtin.file`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html)

## Demo

如何使用 Ansible Playbook 为 Linux 文件添加 755 执行权限。

我将向你展示如何使用 Ansible 为 `example.sh` Linux 文件设置 `chmod +x`。

`file_permission.yml`

```yaml
---
- name: file module demo
  hosts: all
  vars:
    myscript: "~/example.sh"
  tasks:
    - name: set execution permission
      ansible.builtin.file:
        dest: "{{ myscript }}"
        mode: 'a+x'
```

`example.sh`

```bash
#!/bin/bash
echo "Hello World"
```

### Execution

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/ inventory file_management/file_permission.yml
PLAY [file module demo] *********************************
TASK [Gathering Facts] **********************************
ok: [demo.example.com]
TASK [set execution permission] *************************
changed: [demo.example.com]
PLAY RECAP **********************************************
demo.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```

### Idempotency

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/ inventory file_management/file_permission.yml
PLAY [file module demo] *********************************
TASK [Gathering Facts] **********************************
ok: [demo.example.com]
TASK [set execution permission] *************************
ok: [demo.example.com]
PLAY RECAP **********************************************
demo.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $
```

（注：剩余文本包含冗余或杂的片段，已清理以保持核心清晰度。）

- `path` string (`dest`、`name`)——文件路径
- `owner` string——用户
- `group` string——组
- `mode` raw——例：`0644` 或 `u=rw,g=r,o=r`
- `state` string——`file`/`absent`/`directory`/`hard`/`link`/`touch`
- `setype`/`seuser`/`selevel`——SELinux

## 概述

`dest` 参数指定了资源在目标节点上保存的文件系统路径。

让我们深入研究 `force` 参数。

如果 `dest` 是一个文件，Ansible 每次都会下载该文件。如果 `dest` 是一个目录，默认行为是不替换文件，除非你将 `force` 参数切换为 `yes`。

`checksum` 参数非常有用，用于验证下载文件的一致性。

你可以指定算法（通常为 `sha1` 或 `sha256`），并直接提供校验和值或校验和的 URL。

你可能需要第三方库 `hashlib` 来访问额外的算法。

另一个有意思的参数是 `headers`，它允许你指定一些自定义的 HTTP 请求头。

在 Web 服务器的日志中，Ansible 是以 `ansible-httpget` 的身份自荐呈现的，但你可以通过 `http_agent` 参数对其进行自定义。

还有一些额外的身份认证参数，例如处理带有用户名和密码的 HTTP 认证，或者使用 Python 库 `httplib2` 处理更复杂的 GSSAPI-Kerberos 场景。

让我也强调一下，我们还可以指定权限和 SELinux 属性。

## Demo

如何使用 Ansible 从互联网下载 tar.gz 文件并验证 SHA256 校验和。

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

# 解压存档——Ansible `unarchive` 模块

如何下载 zip 文件并将其解压到用户主目录下。该 Playbook 还会处理必要的软件依赖项。

让我们 true Ansible 模块 `unarchive`。

全名是 `ansible.builtin.unarchive`，这意味着它是 Ansible `builtin` 模块集合的一部分，并随 Ansible 一起发布。

这是一个非常稳定且已发布多年的模块。

它可以在不同的操作系统中工作。

它会在（可选地）从本地机器复制存档后解压它。

它可以使用 `unzip` 处理 `.zip` 文件，可以使用 `gtar` 处理 `.tar`、`.tar.gz`、`.tar.bz2`、`.tar.xz` 和 `.tar.zst` 文件。它要求目标主机上有 `zipinfo`、`gtar` 和 `unzip` 命令。

请注意，对于 Unix 文件格式，它需要一个 tar 包（`.tar` 存档）。

对于 Windows 目标，请使用 `ansible.windows.win_unzip` 模块。

## 参数

- `src` string——路径
- `dest` string——路径
- `remote_src` boolean——否/是
- `validate_certs` boolean——否/是（仅限 HTTPS）
- `include`/`exclude` 列表——目录和文件条目
- `extra_opts` string——命令行选项
- `keep_newer` boolean——否/是
- `mode`/`owner`/`group`——权限
- `setype`/`seuser`/`selevel`——SELinux

唯一的强制性参数是 `src` 和 `dst`，它们是源路径和目标路径。`src` 特别特殊，因为它应该是 Ansible 控制器上的本地路径。

我们可以通过启用 `remote_src` 切换到远程路径。

在 `src` 参数中，我们可以指定 URL。

其他有用的参数是 `include` 和 `exclude`，允许我们指定文件或目录。

`extra_opts` 允许我们指定命令行选项。

如果文件已经存在且比存档新，则 `keep_newer` 参数可以防止覆盖。

让我也强调一下，我们还可以指定权限和 SELinux 属性。

## Demo

使用 Ansible 解压存档。

`unarchive.yml`

```yaml
---
- name: unarchive module demo
  hosts: all
  become: false
  vars:
    "https://github.com/lucab85/archive/refs/heads/master.zip": "myurl"
    "/home/devops/": "mydest"
  tasks:
    - name: extractor
      ansible.builtin.yum:
        name: unzip

    - name: extract
      ansible.builtin.unarchive:
        src: "{{ myurl }}"
        dest: "{{ mydest }}"
        remote_src: true
```

# 创建链接——Ansible 模块

在 Ansible 中创建一个链接。

`link` 模块创建一个硬链接。

让我也强调一下，我们还可以指定权限和 SELinux 属性。

# 创建链接（软链接）——Ansible

在 Linux 上创建一个指向 `/proc/cpuinfo` 的 `example` 软链接。

`create_symlink.yml`

```yaml
---
- name: file demo
  hosts: all
  vars:
    mydlink: "~/example"
    mysrc: "/proc/cpuinfo"
  tasks:
    - name: Creating a symlink
      ansible.builtin.file:
        src: "{{ mysrc }}"
        dest: "{{ mylink }}"
        state: link
```

### Execution

```bash
$ ansible-playbook -i demo/inventory create_symlink.yml

PLAY [file demo] *********************************

TASK [Gathering Facts] *********************************

ok: [demo.example.com]

TASK [Creating a symlink] *******************************

changed: [demo.example.com]

PLAY RECAP **********************************************

demo.example.com: ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### Before Execution

```bash
$ ssh devops@demo.com

[devops@demo ~]$ ls -al

total 16

drwx------. 4 devops wheel  111 Nov 14 14:26 .
drwxr-xr-x. 5 root root     50 Nov  8 17:07 ..
drwx------. 3 devops wheel  17 Sep  6 05:53 .ansible
-rw-------. 1 devops wheel 3055 Nov 14 14:26 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  94 Sep 16 10:09 .ssh
```



# 在 Linux 中创建硬链接：Ansible 文件模块

如何使用 Ansible 在 Linux 文件系统中创建一个引用`example.txt`文本文件的“硬链接”。

## Ansible 创建硬链接

`ansible.builtin.file`

管理文件和文件属性。

今天我们来讨论 Ansible 文件模块。

它的全名是`ansible.builtin.file`，这意味着它是 Ansible 内置`builtin`模块集合的一部分，并随 Ansible 一起分发。

这是一个非常稳定的模块，已经发布了多年。

它可以在多种操作系统上运行，也可以管理文件和文件属性。

如需创建符号链接（或软链接），请参阅 Ansible`file`模块的后续参数。

对于 Windows 目标，请改用`ansible.windows.win_file`模块。

另参见：在 Linux 中创建符号链接（也称为 symlink 或 soft link）- Ansible 模块文件。

## 参数

- `src`字符串 - 符号链接路径
- `dest`字符串 - 目标文件路径
- `state`字符串 - 文件/不存在/目录/链接/硬/touch
- `mode`/`owner`/`group` - 权限
- `setype`/`seuser`/`selevel` - SELinux

该模块包含一些参数以执行任何任务。

两个必需字段是`src`和`dest`，它们指定了硬链接和目标文件的文件系统路径。

`state`定义了我们要修改的对象类型，默认是`file`，但对于我们的用例，我们需要`link`选项。

让我也强调一下权限和 SELinux 参数。

## 演示

如何使用 Ansible 创建引用`example.txt`文件的硬链接。

### `create_hardlink.yml`

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

## 执行

```bash
$ ansible-playbook -i virtualmachines/demo/inventory link/hardlink.yml

PLAY [file module demo] *********************************

TASK [Gathering Facts] ***********************************

TASK [Creating hardlink] ********************************

PLAY RECAP *********************************************

demo.example.com : ok=2    changed=1    unreachable=0    failed=0    skipped=0    ignored=0
```

## 执行前

```bash
$ ssh devops@demo.example.com

[devops@demo ~]$ ls -al

total 16

drwx------. 4 devops wheel  126 Nov 14 14:29 .
drwxr-xr-x. 5 root  root    50 Nov  8 17:07 ..
drwx------. 3 devops wheel  17 Sep  6 05:53 .ansible
-rw-------. 1 devops wheel 3067 Nov 14 14:28 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  94 Sep 16 10:09 .ssh
lrwxrwxrwx. 1 devops wheel  13 Nov 14 14:29 example -> \
proc/cpuinfo

[devops@demo ~]$ cat example | less

[devops@demo ~]$

[devops@demo ~]$ echo test > example.txt

[devops@demo ~]$ cat example.txt
```

## 执行后

```bash
$ ssh devops@demo.example.com

[devops@demo ~]$ ls -al

total 24

drwx------. 4 devops wheel 142 Dec  1 15:09 .
drwxr-xr-x. 4 root  root    35 Nov 28 16:46 ..
drwx------. 3 devops wheel  17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec  1 15:08 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  29 Nov 28 16:46 .ssh
-rw-r--r--. 2 devops wheel  5 Dec  1 15:08 example.txt
-rw-r--r--. 2 devops wheel  5 Dec  1 15:08 link

[devops@demo ~]$ cat link
test

[devops@demo ~]$ cat example.txt
test

[devops@demo ~]$ ls -al

total 24

drwx------. 4 devops wheel 142 Dec  1 15:09 .
drwxr-xr-x. 4 root  root    35 Nov 28 16:46 ..
drwx------. 3 devops wheel  17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec  1 15:08 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  29 Nov 28 16:46 .ssh
-rw-r--r--. 2 devops wheel  5 Dec  1 15:08 example.txt
-rw-r--r--. 2 devops wheel  5 Dec  1 15:08 link

[devops@demo ~]$ chmod 777 link

[devops@demo ~]$ ls -al

total 24

drwx------. 4 devops wheel 142 Dec  1 15:09 .
drwxr-xr-x. 4 root  root    35 Nov 28 16:46 ..
drwx------. 3 devops wheel  17 Nov 28 16:46 .ansible
-rw-------. 1 devops wheel 276 Dec  1 15:08 .bash_history
-rw-r--r--. 1 devops wheel  18 Dec  4  2020 .bash_logout
-rw-r--r--. 1 devops wheel  141 Dec  4  2020 .bash_profile
-rw-r--r--. 1 devops wheel  376 Dec  4  2020 .bashrc
drwx------. 2 devops wheel  29 Nov 28 16:46 .ssh
-rwxrwxrwx. 2 devops wheel  5 Dec  1 15:08 example.txt
-rwxrwxrwx. 2 devops wheel  5 Dec  1 15:08 link

[devops@demo ~]$
```

- `src`字符串 - 设备或网络卷
- `fstype`字符串 - `ext4`、`xfs`、`iso9660`、`nfs`、`cifs`等
- `opts`字符串 - 挂载选项

此模块有许多参数用于执行任何任务。

仅必需参数是`path`和`state`。

参数`path`指定挂载点的路径（例如`/mnt/`）。

参数`state`允许我们验证挂载点的特定状态。`mounted`、`unmounted`和`remounted`选项更改设备状态。`present`和`absent`选项仅更改`/etc/fstab`文件。

`src`参数指定 NFS 或 SMB/CIFS 的设备或网络卷。

`fstype`参数指定文件系统类型。例如：`ext4`、`xfs`、`iso9660`、`nfs`、`cifs`等。

`opts`参数允许我们指定某些挂载选项，这些选项因每个文件系统类型而异。

## 演示

让我们通过一个真实的 Ansible Playbook 来挂载 SMB/CIFS 文件系统。

### `mount_cifs.yml`

```yaml
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
        mode: "0755"
        owner: root
        group: root

    - name: Mount network share
      ansible.posix.mount:
        src: "{{ uri }}"
        path: "{{ mountpoint }}"
        fstype: cifs
        opts: "username={{ username }},password={{ password }}"
        state: mounted
```

### 执行

```bash
$ ansible-playbook -i demo/inventory mount drive/cifs.yml

PLAY [mount module demo] ********************************

TASK [Gathering Facts] *********************************
ok: [demo.example.com]

TASK [utility present] *********************************
changed: [demo.example.com]

TASK [check mountpoint exist] ***************************
changed: [demo.example.com]

TASK [Mount network share] ******************************
changed: [demo.example.com]

PLAY RECAP **********************************************
demo.example.com          : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### 执行前

```bash
$ ssh devops@demo.example.com

[devops@demo ~]$ sudo su

[root@demo devops]# mount

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=95492k,nr_inodes=98873,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime,seclabel)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,size=7555)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,exec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/lib/systemd/systemd-agent,name=systemd)
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
```



## 挂载信息

```text
cgroup on /sys/fs/cgroup/cpu,acct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpu,acct)

selinux on /sys/fs/selinux type selinux (rw,relatime)

configfs on /sys/kernel/config type configfs (rw,relatime)

tracing on /sys/kernel/tracing type tracefs (rw,relatime)

debugfs on /sys/kernel/debug type debugfs (rw,relatime,seclabel)

mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)

hugetbfs on /dev/hugepages type hugetbfs (rw,relatime,seclabel,pagesize=2M)

tmpfs on /run/user/1001 type tmpfs (rw,nosuid,nodev,seclabel,size=82872k,mode=700,uid=1001,gid=10)

[root@demo devops]# mount | grep share

[root@demo devops]# cat /etc/fstab

#

# /etc/fstab

# Created by anaconda on Wed Sep  1 00:06:23 2021

#

# Accessible filesystems, by reference, are maintained under '/dev/disk/'.

# See man pages fstab(5), findfs(8), mount(8) andor blkid(8) for more info.

#

# After editing this file, run 'systemctl daemon-reload'

# to update systemd units generated from this file.

#

# /dev/mapper/rhel_rhel8-root /             xfs     defaults        0 0

# UUID=ae6c1777-c1c9-42a1-8fcf-513077aac39b /boot   xfs     defaults        0 0

# /dev/mapper/rhel_rhel8-swap none            defaults        0 0

[root@demo devops]#
```

```bash
1 $ ssh devops@demo.example.com
2 [devops@demo ~]$ sudo su
3 [root@demo devops]# mount

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

systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=31,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=18292)

debugfs on /sys/kernel/debug type debugfs (rw,relatime,seclabel)

mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)

hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)

/dev/sda1 on /boot type xfs (rw,relatime,seclabel,attr2,logbufs=8,logbsize=32k,noquota)

tmpfs on /run/user/1001 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=82872k,mode=700,uid=1001,gid=0)

//windows-pc/share on /share type cifs (rw,nosuid,nodev,relatime,seclabel,username=devops,password)
```

```bash
$ ansible-playbook -i virtualmachines/demo/inventory mount drive/nfs.yml

PLAY [mount module demo] ******************************** ******************************************

TASK [Gathering Facts] ********************************* ******************************************

ok: [demo.example.com]

TASK [utility present redhat-like] ********************** **************************

changed: [demo.example.com]

TASK [utility present debian-like] ********************** ******************************************

skipping: [demo.example.com]

TASK [check mountpoint exist] *************************** ******************************************

changed: [demo.example.com]

TASK [mount network share] ****************************** **************************

changed: [demo.example.com]

PLAY RECAP ********************************************** **************************

demo.example.com          : ok=4    changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

## 执行前

```bash
$ ssh devops@demo.example.com
[devops@demo ~]$ sudo su
[root@demo devops]# cat /etc/redhat-release
Red Hat Enterprise Linux 8.4 (Ootpa)
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
```

```text
#

# /etc/fstab

# Created by anaconda on Wed Sep  1 00:06:23 2021

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
```

```bash
[root@demo devops]# mount
```

```text
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)

proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)

devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=395492k,nr_inodes=98873,mode=755)

securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)

tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)

devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime)
```

## 按特定顺序合并多个文件——Ansible 模块模板和 YAML

```bash
$ ssh devops@demo.example.com

[devops@demo ~]$ sudo su

[root@demo devops]# yum list nfs-utils

Updating Subscription Management repositories.

Last metadata expiration check: 0:31:28 ago on Wed 24 Nov 2021 11:17:15 AM UTC.

Installed Packages

nfs-utils.x86_64                  1:2.3.3-46.el8             @rhel-8-for-x86_64-baseos-rpms

[root@demo devops]# showmount --exports 192.168.0.200

Export list for 192.168.0.200:

/nfs/share 192.168.0.200/24

[root@demo devops]# cat /etc/fstab
```

```text
# /etc/fstab

# Created by anaconda on Wed Sep 1 00:06:23 2021

#

# Accessible filesystems, by reference, are maintained under '/dev/disk/'.

# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.

#

# After editing this file, run 'systemctl daemon-reload' to update systemd units generated from this file.

#

/dev/mapper/rhel_rhel8-root /               xfs      defaults      0 0

UUID=ae6c1777-c1c9-42a1-8fcf-513077aac39b /boot        xfs      defaults      0 0
```



```
/dev/mapper/rhel_rhel8-swap none            swap      defaults      0 0

192.168.0.200:/nfs/share /share nfs rw,sync 0 0
```

```bash
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

cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuset)

cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,rdma)

cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,pids)

cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,hugetlb)

cgroup on /sys/fs/cgroup/cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuacct)

cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,freezer)

cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,blkio)

cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,net_cls,net_prio)

cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,perf_event)

cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,memory)

cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,devices)

none on /sys/kernel/tracing type tracefs (rw,relatime)

configfs on /sys/kernel/config type configfs (rw,relatime)

/dev/mapper/rhel_rhel8-root / xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)

selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)

mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)

hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)

systemd-1 on /proc/sys/fs/bin
```

```bash
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

cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuset)

cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,rdma)

cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,pids)

cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,hugetlb)

cgroup on /sys/fs/cgroup/cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,cpuacct)

cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,freezer)

cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,blkio)

cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,net_cls,net_prio)

cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,perf_event)

cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,memory)

cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,seclabel,devices)

none on /sys/kernel/tracing type tracefs (rw,relatime)

configfs on /sys/kernel/config type configfs (rw,relatime)

/dev/mapper/rhel_rhel8-root / xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)

selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)

mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)

hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel,pagesize=2M)

systemd-1 on /proc/sys/fs/bin
```

如果启用了`backup`参数，Ansible 会在文件复制到目标位置之前创建一个包含时间信息的备份文件。

让我同时也强调一下，我们还可以指定权限和 SELinux 属性。

## demo

如何使用 Ansible template 模块和 YAML 按特定顺序合并多个文件。

### code

```text
a.txt

1 A content

b.txt

1 B content
```

`includes.yaml`

```yaml
input-files: 

  - concatenate/b.txt

  - concatenate/a.txt
```

`concatenate.yml`

```yaml
---

- name: concatenate demo

  hosts: "{{ HOSTS }}"

  become: false

  gather_facts: true

  vars:

    myinput: "concatenate/includes.yaml"

    myoutput: "concatenate/output.txt"

  tasks:

    - name: include file list

      include_vars:

        file: "{{ myinput }}"

        name: files

    - name: concatenate

      ansible.builtin.template:

        src: templates/concatenate.j2

        dest: "{{ myoutput }}"
```

`concatenate.j2`

```jinja2
{% for i in files["input-files"] %}

{{ lookup('file', i) }}

{% endfor %}
```

### execution

```bash
ansible-pilot $ ansible-playbook -e "HOSTS=localhost" concatenate.yml

[WARNING]: No inventory was parsed, only implicit localhost is available

[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [concatenate demo] ************************************************

******************************************

TASK [Gathering Facts] *********************************

******************************************

ok: [localhost]

TASK [include file list] ********************************

******************************************

ok: [localhost]

TASK [concatenate] *************************************

******************************************

changed: [localhost]

PLAY RECAP **********************************************

******************************************

localhost                  ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible-pilot $
```

### idempotency

```bash
ansible-pilot $ ansible-playbook -e "HOSTS=localhost" concatenate.yml

[WARNING]: No inventory was parsed, only implicit localhost is available

[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [concatenate demo] ************************************************

******************************************

TASK [Gathering Facts] *********************************

******************************************

ok: [localhost]

TASK [include file list] ********************************

******************************************

ok: [localhost]

TASK [concatenate] *************************************

******************************************

ok: [localhost]

PLAY RECAP **********************************************

******************************************

localhost                  ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible-pilot $
```

### before execution



`ansible-pilot $ ls -al concatenate`

```
total 24
drwxr-xr-x  5 lberton staff  160 Feb  1 15:40 .
drwxr-xr-x  9 lberton staff  288 Feb  1 15:08 ..
-rw-r--r--  1 lberton staff    9 Feb  1 15:18 a.txt
-rw-r--r--  1 lberton staff    9 Feb  1 15:18 b.txt
-rw-r--r--  1 lberton staff   56 Feb  1 15:48 includes.yaml
```

`ansible-pilot $ cat concatenate/a.txt`

```
A content%
```

`ansible-pilot $ cat concatenate/b.txt`

```
B content%
```

`ansible-pilot $ cat concatenate/includes.yaml`

```
input-files: 
  - concatenate/b.txt
  - concatenate/a.txt
```

after execution

```bash
ansible-pilot $ ls -al concatenate

total 24
drwxr-xr-x  5 lberton staff  160 Feb  1 15:40 .
drwxr-xr-x  9 lberton staff  288 Feb  1 15:08 ..
-rw-r--r--  1 lberton staff    9 Feb  1 15:18 a.txt
-rw-r--r--  1 lberton staff    9 Feb  1 15:18 b.txt
-rw-r--r--  1 lberton staff   56 Feb  1 15:48 includes.yaml

ansible-pilot $ cat concatenate/a.txt

A content%

ansible-pilot $ cat concatenate/b.txt

B content%

ansible-pilot $ cat concatenate/includes.yaml

input-files: 
  - concatenate/b.txt
  - concatenate/a.txt
```

## 使用 Rsync - 本地到远程

如何使用 `synchronize` 模块通过 `rsync` 工具在 Linux 上同步某些目录树。

```yaml
---
- name: synchronize module demo
  hosts: all
  become: false
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
        src: '{{ source }}'
        dest: '{{ destination }}'
```

## Ansible 使用 rsync

`ansible.posix.synchronize` 是 `rsync` 的一个封装，用于简化 playbook 中的常用任务。它是 POSIX 集合的一部分。

## 主要参数

- `src`: string - 源路径或相对路径
- `dest`: string - 目标路径或相对路径
- `archive`: boolean - 镜像 Rsync 标志，启用递归、链接、权限、时间、所有者、组以及 `-D`
- `rsync_opts`: string - 无

参数列表很长，但这些是 `synchronize` 的重要选项。`src` 和 `dest` 是强制性的。`src` 参数是必需的，指定了要同步到目标主机的源。路径可以是绝对路径或相对路径。`dest` 参数也是，指定了从源主机同步到目标主机的路径。根据需求可以是本地或远程。最有用的参数是 `archive`，它默认启用，因此在大多数情况下不需要指定任何内容。请参阅手册以启用/禁用某些特定设置。

可以通过 `rsync_opts` 参数指定更多 Rsync 参数。

## 等幂性测试

```bash
ansible-pilot $ ansible-playbook -i virtualmachines/demo/inventory copy\ files\ to\ remote\ hosts/rsync.yml

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

ansible-pilot $ ansible-playbook -i virtualmachines/demo/inventory copy\ files\ to\ remote\ hosts/rsync.yml

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
ansible-pilot $ ls -al copy\ files\ to\ remote\ hosts/examples

total 16
drwxr-xr-x  4 lberton  staff  128 Jan 17 11:54 .
drwxr-xr-x  9 lberton  staff  288 Mar 28 14:13 ..
-rw-r--r--  1 lberton  staff   16 Sep  4  2021 report.txt
-rw-r--r--  1 lberton  staff  16 Jan 17 11:52 report2.txt

ansible-pilot $ cat copy\ files\ to\ remote\ hosts/examples/report.txt

test report.txt

ansible-pilot $ cat copy\ files\ to\ remote\ hosts/examples/report2.txt

test report.txt

ansible-pilot $ ssh devops@demo.example.com

Last login: Mon Mar 28 12:22:14 2022 from 192.168.0.59
[devops@demo ~]$ ls -al

total 20
drwx------. 4 devops wheel  127 Mar 28 12:22 .
drwxr-xr-x. 4 root  root     35 Mar 24 17:44 ..
drwx------. 3 devops wheel  17 Mar 24 17:44 .ansible
-rw-------. 1 devops wheel  178 Mar 28 12:21 .bash_history
-rw-r--r--. 1 devops wheel  18 Jul 26  2021 .bash_logout
-rw-r--r--. 1 devops wheel  141 Jul 26  2021 .bash_profile
-rw-r--r--. 1 devops wheel  376 Jul 26  2021 .bashrc
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
drwxr-xr-x. 4 root  root     35 Mar 24 17:44 ..
drwx------. 3 devops wheel  17 Mar 24 17:44 .ansible
-rw-------. 1 devops wheel  178 Mar 28 12:24 .bash_history
-rw-r--r--. 1 devops wheel  18 Jul 26  2021 .bash_logout
-rw-r--r--. 1 devops wheel  141 Jul 26  2021 .bash_profile
-rw-r--r--. 1 devops wheel  376 Jul 26  2021 .bashrc
drwx------. 2 devops wheel  29 Mar 24 17:44 .ssh
-rw-------. 1 devops wheel 1756 Mar 28 10:38 .viminfo
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 example-backup

[devops@demo ~]$ tree example-backup

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
drwxr-xr-x. 2 devops wheel  62 Mar 28 12:44 .
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 ..
-rw-r--r--. 1 devops wheel  16 Sep  4  2021 report.txt
-rw-r--r--. 1 devops wheel  16 Jan 17 10:52 report2.txt

[devops@demo ~]$
```

## 源目录中的变化

```bash
ansible-pilot $ touch copy\ files\ to\ remote\ hosts/examples/report3.txt

ansible-pilot $ ansible-playbook -i virtualmachines/demo/inventory copy\ files\ to\ remote\ hosts/rsync.yml

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
[devops@demo ~]$ ls -al example-backup

total 0
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 .
drwx------. 5 devops wheel  149 Mar 28 12:24 ..

[devops@demo ~]$ tree example-backup

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
drwxr-xr-x. 2 devops wheel  62 Mar 28 12:44 .
drwxr-xr-x. 3 devops wheel  22 Mar 28 12:24 ..
-rw-r--r--. 1 devops wheel  16 Sep  4  2021 report.txt
```



```text
-rw-r--r--. 1 devops wheel  16 Jan 17 10:52 report2.txt
-rw-r--r--. 1 devops wheel  0 Mar 28 18:44 report3.txt

[devops@demo ~]$
```
