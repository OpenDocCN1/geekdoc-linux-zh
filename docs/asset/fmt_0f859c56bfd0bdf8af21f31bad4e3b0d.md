
进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在表达式 `cvar = avar + bvar` 中，加法运算符（`+`）将 `avar` 与 `bvar` 相加，得到它们的和 `cvar`

在 `List.of(arg0, arg1, arg2)` 中，`List` 接口的工厂方法 `of()` 接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用 `cmd` 命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
[root@host]# subscription-manager list --available
```
- 4. 使用订阅的池 ID（pool ID）将该池附加到系统。

```
[root@host]# subscription-manager repos --enable ansible-2-for-rhel-8-x86_64-rpms
```
- 6. 安装 Red Hat Ansible Engine。

如果你正在使用 Red Hat Enterprise Linux 订阅提供的受限支持版本，请使用以下步骤：
- 1. 启用 Red Hat Ansible Engine 仓库。

```
root@host]# subscription-manager repos --enable ansible-2-for-rhel-8-x86_64-rpms
```

```
[root@host ~] yum install ansible
```

```
[root@host ~] yum install python36
```

```
[student@workstation ~]$ lab intro-install start
```

```
[student@workstation ~]$ sudo yum install ansible
```
Loaded plugins: langpacks, search-disabled-repos

--> Running transaction check

Is this ok [y/d/N]: y

- 2. 验证已安装 Ansible。执行带版本选项的 `ansible` 命令。

```
ansible 2.8.0

configured module search path = ['/home/student/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']

python version = 3.6.8 (Default, 3 2019, 17:26:03) [GCC 8.2.1
```

- 3. 使用 `setup` 模块验证 localhost 的 `ansible_python_version`。

```
"ansible_python_version": "3.6.8",
```

```
$student@workstation ~$ lab intro-install finish
```

- Ansible 是一个开源自动化平台，可以适应许多不同的工作流和环境。
- Ansible Playbooks（剧本文件）是人类可读的文本文件，描述了 IT 基础设施的预期状态。
- Ansible 使用 SSH 等标准网络协议连接到被托管主机，并在被托管主机上运行代码或命令，以确保它们处于 Ansible 指定的状态中。

# 第 2 章

## 部署 ANSIBLE

| 目标 | 配置 Ansible 管理主机并运行即时（ad hoc）Ansible 命令。 |

| 目标 | - 描述 Ansible 清单概念并管理静态清单文件。<br>- 描述 Ansible 配置文件的位置、Ansible 如何选择这些文件，并编辑它们以对默认设置应用更改。<br>- 使用即时命令运行单个 Ansible 自动化任务，并解释即时命令的一些用例。 |

| 实验 | - 部署 Ansible |

## 构建 Ansible 清单

## 目标

完成本节后，你应该能够描述 Ansible 清单概念并管理静态清单文件。

## 定义清单

清单（Inventory）定义了 Ansible 将管理的主机集合。这些主机还可以被分配到组，并对组进行统一管理。组可以包含子组，主机可以是多个组的成员。清单还可以为其定义的主机和组设置变量。

主机清单通过两种不同的方式定义。静态主机清单可以通过文本文件定义。动态主机清单可以根据需要，使用脚本或其他程序利用外部信息生成。

## 使用静态清单指定被托管主机

静态清单是一个指定 Ansible 目标被托管主机的文本文件。你可以使用多种格式编写此文件，包括 INI 格式或 YAML。INI 格式非常常见，并将用于本课程中的大多数示例。

> 注意 Ansible 支持多种静态清单格式。在本节中，我们重点关注最常用的 INI 格式。

在最简单的形式下，INI 格式的静态清单文件是被托管主机的主机名或 IP 地址的列表，每个地址占一行：

```
web2.example.com
db2.example.com
```

通常，你将被托管主机组织成主机组。主机组允许你更有效地对一组系统运行 Ansible。在这种情况下，每个章节以用方括号 [] 包围的主机组名开头。随后是该组中每个被托管主机的主机名或 IP 地址，每个占一行。

在接后的示例中，主机清单定义了两个组：webservers（Web 服务器）和 db-servers（数据库服务器）。

# 第 2 章 | 部署 Ansible

```
web1.example.com
192.0.2.42

[db-servers]
db2.example.com


[webservers]
web2.example.com
```

```
db1.example.com
```

```
web1.example.com
```

```
web2.example.com
```

```
web1.example.com
db1.example.com
```

```
192.0.2.42

始终存在两个主机组：
- `all` 组包含清单中显式列出的所有主机。

[usa]
washington2.example.com
[canada]
ontario2.example.com
[north-america]
usa

- a-c 匹配所有以 a、b 或 c 开头的主机。
如果数字范围中使用前导零，它们将否忽略。下面的示例使用了范围：

```
washington1.example.com

ontario1.example.com
```

## 验证清单

当不确定时，使用 `ansible` 命令来验证机器是否存在于清单中：

```
hosts (1):

[user@controlnode ~$ ansible web1.example.com --list-hosts
```

你可以运行命令列出组中的所有主机：

```
hosts (2):

  ontario2.example.com
```

清单中包含一个与主机同名的主机组，`ansible` 命令会打印警告并针对主机。该主机组将被忽略。

有多种方法处理这种情况，最简单的方法是确保主机组名称与主机相同。

## 覆盖清单位置

`/etc/ansible/hosts` 文件是系统的默认清单文件。然而，通常不使用该文件，而是在 Ansible 配置中定义不同的清单位置。该文件将在下一节介绍。

你在课程中运行 Ansible 即时命令和 playbook 时使用的 `ansible` 和 `ansible-playbook` 命令也可以通过 `--inventory PATHNAME` 或 `-i PATHNAME` 选项指定清单的位置，其中 `PATHNAME` 是所需清单的路径。

## 在清单中定义变量

变量的值可以在主机清单文件中指定。这些变量仅适用于特定的主机或组。通常最好在特殊目录中定义*清单变量*，而不是直接定义在清单文件中。这个主题在课程的其他地方有深入讨论。

当您运行 Ansible 时，程序会执行此操作：随着新主机的添加和旧主机的移除，可以使用服务提供的最新信息来填充清单。

此主题将在课程的稍后部分详细讨论。

> 参考文献

http://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html

## 引导练习

## 构建 ANSIBLE 清单

在此练习中，你将创建一个包含主机和组的新静态清单。

预期结果

以 `student` 身份登录到工作站，并使用 `student` 作为密码。

在工作站上，运行 `lab deploy-inventory start` 命令。此启动脚本可确保托管主机 servera、serverb、serverc 和 serverd 在网络上是可用的。

- 1. 修改 `/etc/ansible/hosts` 以将 `servera.lab.example.com` 包含为托管主机。

- 1.1 将 `servera.lab.example.com` 添加到默认清单文件 `/etc/ansible/hosts` 的末尾。

```
$student@workstation ~]$ sudo vim /etc/ansible/hosts
... output omitted...
## db --[99:181]-node.example.com
```

```
servera.lab.example.com
```

- 1.2 继续编辑 `/etc/ansible/hosts` 清单文件，在文件底部添加 `[webservers]` 组，并将 `serverb.lab.example.com` 服务器作为该组成员。
