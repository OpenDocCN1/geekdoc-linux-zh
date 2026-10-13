
# Red Hat Enterprise Linux 8：使用 RHEL 系统角色的管理与配置任务

使用 Red Hat Ansible Automation Platform Playbooks 应用 RHEL System Roles 以执行系统管理任务

# 摘要

本文介绍了在 Red Hat Enterprise Linux 8 上使用 Ansible 配置系统角色。标题重点关注于：RHEL System Roles 是 Ansible 角色、模块和 Playbooks 的集合，提供稳定且一致的配置接口来管理和配置 Red Hat Enterprise Linux。它们被设计为与 Red Hat Enterprise Linux 8 的多个主要发行版本向前兼容。

## 11.4 通过本地机器设置身份验证

# 让开源更具包容性

红帽致力于在我们的代码、文档和网络属性中替换存在问题的语言。我们将从以下四个术语开始：`master`、`slave`、`blacklist` 和 `whitelist`。由于这项工作的艰巨性，这些更改将在接下来的几个版本中逐步实施。更多详情请参阅我们的首席技术官 Chris Wright 的消息。

# 对红帽文档提供反馈

感谢您对我们的文档提供的建议。请告诉我们如何改进。请按以下步骤操作：

针对特定段落的简单注释：

1. 确保您正在以 *多页 HTML* 格式查看文档。此外，确保您在文档右上角看到 **反馈** 按钮。

2. 使用鼠标光标选中您想要注释的文本。

3. 点击选中文本下方出现的 **添加反馈** 弹出。

4. 按照显示的说明操作。

提交更复杂的反馈，请创建 Bugzilla 工单：

1. 访问 Bugzilla 网站。

2. 在组件字段中使用 **Documentation**。

3. 在 **描述** 字段中填写您的改进建议。包含指向相关文档部分的链接。

4. 点击 **提交缺陷**。

# 第 1 章.开始使用 RHEL 系统角色

本节解释了什么是 RHEL 系统角色。此外，它描述了如何通过 Ansible playbook 应用特定角色来执行各种系统管理任务。

## 1.1. RHEL 系统角色简介

RHEL 系统角色是 Ansible 角色和模块的集合。RHEL 系统角色提供了一个配置接口，用于远程管理多个 RHEL 系统。该接口能够跨多个版本的 RHEL 进行系统配置，并采用新的主版本发布。

在 Red Hat Enterprise Linux 8 上，该接口目前包含以下角色：

- `kdump`
- `network`
- `selinux`
- `storage`
- `certificate`
- `kernel_settings`
- `logging`
- `metrics`
- `nbde_client` 和 `nbde_server`
- `timesync`
- `tlog`

所有角色均由 AppStream 存储中的 `rhel-system-roles` 软件包提供。

### 额外资源

- Red Hat Enterprise Linux 系统角色
- `/usr/share/doc/rhel-system-roles` 文档 [1]
- SELinux 系统角色简介
- 存储角色简介
- 使用 RHEL 中的系统角色进行管理和配置任务

## 1.2. RHEL 系统角色术语

您可以在本文档中找到以下术语：

### Ansible playbook

Playbooks 是 Ansible 的配置、部署和编排语言。它们可以描述您希望远程系统确保的策略，或者通用 IT 流程中的一组步骤。

### 控制节点

任何安装了 Ansible 的机器。您可以从任何控制节点运行命令和 playbooks，调用 `/usr/bin/ansible` 或 `/usr/bin/ansible-playbook`。您可以使用任何安装了 Python 的控制机作为控制节点——笔记本电脑、共享桌面和服务器都可以运行 Ansible。但是，您不能使用 Windows 机器作为控制节点。您可以拥有多个控制节点。

### 清单

受管理节点列表。清单文件有时被称为“主机文件”。您的清单可以指定每个受管理节点的 IP 地址等信息。清单还组织了受管理节点，创建并嵌套组以便于扩展。要了解更多关于清单的信息，请参阅“使用清单”章节。

### 受管理节点

您使用 Ansible 管理的网络设备、服务器或两者兼有。受管理节点有时也被称为“主机”。受管理节点上不安装 Ansible。

## 1.3. 应用角色

以下步骤描述了如何应用特定角色。

### 前提条件

- 确保在要作为控制节点的系统上安装了 `rhel-system-roles` 软件包：

```
# yum install rhel-system-roles
```

- 您需要 `ansible` 软件包来运行 RHEL 系统角色的 playbooks。确保 Ansible 存储库已启用，并且在要作为控制节点的系统上安装了 `ansible` 软件包。

- 如果您没有 Red Hat Ansible Engine 订阅，可以使用 Red Hat Enterprise Linux 订阅提供的受限支持版本的 Red Hat Ansible Engine。在这种情况下，请按照以下步骤操作：

  - 启用 RHEL Ansible Engine 存储库：

    ```
    # subscription-manager refresh
    # subscription-manager repos --enable ansible-2-for-rhel-8_x86_64-rpms
    ```

  - 安装 Ansible Engine：

    ```
    # yum install ansible
    ```

- 如果您有 Red Hat Ansible Engine 订阅，请按照《如何下载和安装 Red Hat Ansible Engine》中描述的程序操作。

- 确保您能够创建 Ansible 清单。清单代表了主机、主机组以及 Ansible playbooks 使用的一些配置参数。

Playbooks 通常是人类可读的，并定义在 ini、yaml、json 和其他文件格式中。

- 确保您能够创建 Ansible playbook。Playbooks 是 Ansible 的配置、部署和编排语言。通过使用 playbooks，您可以创建和管理远程机器的配置，部署多个远程机器，或编排任何手动顺序过程的步骤。

一个 playbook 是一个或多个 play 的列表。每个 play 都可以包含 Ansible 变量、任务或规则。

Playbooks 是人类可读的，并定义在 yaml 格式中。

### 步骤

1. 创建包含您想要管理的机的所需的 Ansible 清单。这里是一个使用名为 `inventory` 文件的示例：

```ini
[webservers]
host1
host2
host3
```

2. 创建一个包含所需角色的 Ansible playbook。示例示例了如何通过选项使用角色：

```yaml
---
hosts: webservers
roles:
  - rhel-system-roles.network
  - rhel-system-roles.timesync
```

> 注意：每个角色都包含一个 README 文件，记录了如何使用该角色以及支持的参数值。此类文档位于：

```
/usr/share/doc/rhel-system-roles/SUBSY/
```

将 `SUBSY` 替换为角色名称，例如 `selinux`、`kdump`、`network`、`timesync` 或 `storage`。

3. 在特定主机上执行 playbook，必须执行以下操作之一：

- 修改 playbook 使用 `hosts:all`，并执行命令：

```bash
ansible-playbook your_playbook.yml
```

- 修改清单以确保要使用的主机定义在一个组中，并执行命令：

```bash
ansible-playbook -i inventory_file.ini your_playbook.yml
```

## 注意

注意 `-i` 标志指定了可用清单。如果您有多个主机，但只想选择一个主机来运行 playbook，您可以在 playbook 中添加变量来选择主机。例如：



```yaml
#### Ansible Playbook | example-playbook.yml
---
hosts: "{{ target_host }}"
roles:
  - rhel-system-roles.network
  - rhel-system-roles.timesync
```

Playbook 执行命令：

```bash
#### ansible-playbook -i host1..hostn -e target_host=host5 example-playbook.yml
```

## 额外资源

* Ansible playbooks

* 在 Ansible playbook 中使用角色

* Ansible playbooks 示例

* 如何创建和使用清单？

* `ansible-playbook`

## 1.4. 额外资源

- Red Hat Enterprise Linux (RHEL) 系统角色 知识库文章

- 使用 RHEL 系统角色管理本地存储

- 使用 RHEL 系统角色在多个系统上部署相同的 SELinux 配置

[1] 此文档随 `rhel-system-roles` 软件包自动安装。

# 第 2 章.在您的系统中安装 RHEL 系统角色

要使用 RHEL 系统角色，请在您的系统上安装所需的软件包。

### 前提条件

- 您已拥有 Red Hat Ansible Engine 订阅。请参阅步骤 [如何下载和安装 Red Hat Ansible Engine？](https://www.redhat.com/en/articles/red-hat-ansible-management/how-to-download-and-install-red-hat-ansible-engine)

### 步骤

1. 在您想要作为控制节点的系统上安装 `rhel-system-roles` 软件包：

```bash
#### yum install rhel-system-roles
```

如果您没有 Red Hat Ansible Engine 订阅，可以使用 Red Hat Enterprise Linux 订阅附带的受限支持 Red Hat Ansible Engine 版本。在这种情况下，请按照以下步骤操作：

a. 启用 RHEL Ansible Engine 存储库：

```bash
### subscription-manager refresh
### subscription-manager repos --enable ansible-2-for-rhel-8-x86_64-rpms
```

b. 安装 Ansible Engine：

```bash
### yum install ansible
```

完成后，您将能够创建 Ansible playbook。

### 额外资源

- [Red Hat Enterprise Linux (RHEL) 系统角色](https://docs.redhat.com/en/red-hat-enterprise-linux/8/)

- `ansible-playbook` 手页。

# 第 3 章.安装与使用集合 (COLLECTIONS)

## 3.1. ANSI Collections 简介

Ansible Collections 是分发、维护和消费自动化的新方式。通过结合 playbook、角色、模块和插件等类型的 Ansible 内容，您可以从灵活性和扩展性的改进中获益。

Ansible Collections 是 RHEL 系统角色格式的一种可选方案。在 Ansible Collection 格式中使用 RHEL 系统角色与使用传统的 RHEL 系统角色格式 (FQCN) 是相同的。区别在于 Ansible 使用了**全限定集合名称** (fully qualified collection name) 概念，它由命名空间和**集合名称**组成。我们使用的命名空间是 **redhat**，**集合名称**是 **rhel_system_roles**。因此，虽然内核传统的 RHEL 系统角色格式显示为 *rhel-system-roles.kernel_settings*，但使用集合**全限定集合名称**的内核角色将显示为 *redhat.rhel_system_roles.kernel_settings*。

`命名空间`和`集合名称`的组合保证了对象的唯一性。它确保了对象可以在不同的 Ansible Collections 和命名空间之间共享而不会产生冲突。

### 额外资源

- 您可以通过 Automation Hub 访问 Red Hat 集合。

## 3.2. 集合结构

Collections 是 Ansible 内容的包格式。其数据结构如下：

- `docs/`：集合的本地位置，如果角色提供了文档，则在此处包含示例

- `galaxy.yml`：`MANIFEST.json` 的源数据，该文件将是 Ansible Collection 软件包的一部分

- `playbooks/`：此目录下包含可用的 playbook

    - `tasks/`：此处包含用于 `include_tasks`/`import_tasks` 任务使用的“任务列表文件”

- `plugins/`：所有 Ansible 插件和模块均位于此处，各位于自己的子目录下

    - `modules/`：Ansible 模块

    - `modules_utils/`：开发模块的通用代码

    - `lookup/`：查找插件

    - `filter/`：Jinja2 过滤器插件

    - `connection/`：如果不使用默认连接，则需要连接插件

- `roles/`：Ansible 角色的目录

- `tests/`：集合内容的测试用

## 3.3. 使用 CLI 安装集合

Collections 是 Ansible 内容的一种分发格式，可以包含 playbook、角色、模块和插件。

您可以通过 Ansible Galaxy、浏览器或使用命令行安装 Collections。

### 前提条件

- 已安装 Red Hat Ansible engine 2.9 及更高版本。

- 已安装 `python3-jmespath` 软件包。

- 存在一个列出托管节点的清单文件 (`inventory file`)。

### 步骤

- 通过 RPM 软件包安装集合：

```
#### yum install rhel-system-roles
```

安装完成后，这些角色将以 `redhat.rhel_system_roles.<role_name>` 的形式可用。此外，您可以在 `/usr/share/ansible/collections/ansible_collections/` 找到每个角色的文档。

#### 验证步骤

验证 Collections 是否已安装：

1. 复制一个：

```bash
cp /usr/share/ansible/collections/ansible_collections/redhat/rhel_system_roles/. /tmp/
```

2. 编辑文件，将 `"hosts: all"` 替换为 `"hosts: localhost"`。

3. 在检查模式 (`check mode`)下运行 playbook：

```bash
$ ansible-playbook --check
```

命令返回 `value=0`。

## 3.4. 从 CLI 安装集合

如果您在使用 Automation Hub，可以遵循以下步骤：

### 前提条件

- 已安装 Red Hat Ansible engine 2.9 及更高版本。

- 已安装 `python3-jmespath` 软件包。

- 存在一个列出托管节点的清单文件。

### 步骤

1. 通过 Galaxy 安装集合：

```
#### ansible-galaxy collection install redhat.rhel_system_roles
```

安装完成后，这些角色将以 `redhat.rhel_system_roles.<role_name>` 的形式可用。此外，您可以在 `/usr/share/ansible/collections/ansible_collections/` 找到每个角色的文档。

#### 验证步骤

验证 Collections 是否已安装：

1. 复制一个：

```bash
cp /usr/share/ansible/collections/ansible_collections/redhat/rhel_system_roles/. /tmp/
```

2. 编辑文件，将 `"hosts: all"` 替换为 `"hosts: localhost"`。

3. 在检查模式下运行 playbook：

```bash
$ ansible-playbook --check
```

命令返回 `value=0`。

## 3.5. 使用 Collections 应用本地日志系统角色

以下是用 Collections 在一组独立机器上准备并应用日志的示例。

### 前提条件



- 已安装 `Galaxy` collection。

### 步骤

1. 创建定义所需角色的 playbook：

   a. 创建一个新的 YAML 文件并用编辑器打开，例如：

```yaml
#### logging-playbook.yml
```

   b. 向 YAML 文件插入以下内容：

```yaml
---
- name: Deploying basics input and implicit files output
hosts:
  - all
roles:
  - redhat.rhel_system_roles.logging
vars:
  logging_inputs:
    - name: system_input
      type: basics
  logging_outputs:
    - name: files_output
      type: files
  logging_flows:
    - name: flow1
      inputs: [system_input]
      outputs: [files_output]
```

2. 在特定的清单上执行 playbook：

```bash
#### ansible-playbook -i inventory-file logging-playbook.yml
```

其中：

- `inventory-file` 是您的清单文件名。
- `logging-playbook.yml` 是您使用的 playbook。

#### 验证步骤

1. 测试 `/etc/rsyslog.conf` 文件的语法：

```bash
#### rsyslog -N 1
rsyslog: version 8.1911.0-6.el8, config validation run (level 1), master config
/etc/rsyslog.conf
rsyslog: End of config validation run..
```

2. 验证系统向日志发送消息：

   a. 发送一条测试消息：

```bash
#### logger test
```

   b. 查看 `/var/log/messages` 日志，例如：

```bash
### cat /var/log/messages
Aug 5 13:48:31 hostname root[6778]: test
```

`hostname` 是客户端系统的主机名。日志显示了输入 `logger` 命令的用户名，在此例中为 `root`。

# 第 4 章. 使用 ANSIBLE ROLES 永久配置内核参数

对于对 Red Hat Ansible Engine 拥有良好知识的经验丰富的用户，可以使用 `kernel_settings` 角色（role）同时在多个客户端上配置内核参数。

- 提供了一个友好的界面和高效的输入设置功能。
- 将所有预期的内核参数集中在一个处管理。

在您从控制机上运行 `kernel_settings` 角色后，内核参数将应用于被独立管理的系统，并在重启后依然保持有效。

## 4.1. KERNEL SETTINGS 角色简介

RHEL System Roles 是来自 Ansible Automation Platform 的系列角色和模块，它们提供了一致的配置接口，用于远程管理多个系统。

RHEL System Roles 的引入是为了通过 `kernel_settings` 系统角色实现内核的自动化配置。`rhel-system-roles` 软件包包含了该系统角色以及相关的参考文档。

要以自动化方式在一个台或多个系统上应用内核参数，可以在 playbook（剧本）中使用 `kernel_settings` 角色，并选择一个或多个角色变量。playbook 是由一个或多个易读的 play（任务）组成的列表，采用 YAML 格式编写。

您可以使用清单文件（inventory file）定义一组系统，让 Ansible Engine 根据 playbook 进行配置。

通过 `kernel_settings` 角色，您可以配置：

- 使用 `kernel_settings_sysctl` 角色变量配置内核参数
- 使用 `kernel_settings_sysfs` 角色变量配置各种内核子系统、硬件设备和设备驱动
- 使用 `kernel_settings_systemd_cpu_affinity` 角色变量配置系统管理器及其派生进程的 CPU 亲和性
- 使用 `kernel_settings_transparent_hugepages` 和 `kernel_settings_transparent_hugepages_defrag` 变量配置内核内存子系统的巨页（hugepages）

### 资源

- `/usr/share/doc/rhel-system-roles/kernel_settings/` 目录下的 `README.md` 和 `README.html` 文件
- 使用 playbook 的说明
- 如何构建您的清单

## 4.2. 使用 KERNEL SETTINGS 角色应用选定的内核参数

# 使用 System Roles 进行 Red Hat Enterprise Linux 8 的管理与配置任务

按照以下步骤准备并应用 Ansible playbook，以在多个操作系统上远程配置内核参数并具有持久化效果。

### 前提条件

- 您的 Red Hat Ansible Engine 已订阅到该系统（也称为控制机），您希望从中运行 `kernel_settings` 角色。更多信息请参阅《如何下载和安装 Red Hat Ansible Engine》文章。
- 控制机上已启用 Ansible Engine 仓库。
- 控制机上已安装 Ansible Engine。

![](img/7076193df8761a1565038e17afc88b0b_21_0.png)

> 注意

您不需要在想要配置内核参数的系统（也称为托管主机）上安装 Ansible Engine。

- 控制机上已安装 `rhel-system-roles` 软件包。
- 控制机上存在托管主机的清单，且 Ansible Engine 能够连接到它们。

### 步骤

1. 可选地，为了演示目的查看清单文件：

```yaml
#### /home/doe/<ansible_project_name>/inventory
[testingservers]
doe@192.168.122.98
doe@192.168.122.226

[db-servers]
db1.example.com
db2.example.com

[webservers]
web1.example.com
web2.example.com
192.0.2.42
```

该文件定义了 `[testingservers]` 组和其他组。它允许您针对特定的系统集合运行 Ansible Engine。

2. 创建配置文件以为 Ansible Engine 设置默认值和权限提升。

a. 创建一个新的 YAML 文件并用文本编辑器打开，例如：

```yaml
#### /home/doe/<ansible_project_name>/ansible.cfg
```

b. 在文件中插入以下内容：

```ini
[defaults]
inventory = /inventory

[privilege_escalation]
become = true
become_method = sudo
become_user = root
become_ask_pass = true
```

`[defaults]` 部分定义了托管主机清单文件的路径。`[privilege_escalation]` 部分定义了在托管主机上提升到 root 的权限。这对于成功配置内核参数是必要的。运行 Ansible playbook 时，系统会提示输入密码。用户在连接到托管主机后会自动通过 sudo 切换到 root。

3. 创建使用 `kernel_settings` 角色的 Ansible playbook。

a. 创建一个 YAML 文件并用文本编辑器打开，例如：

```yaml
#### vi /home/jdoe/<ansible_project_name>/kernel_roles.yml
```

该文件代表一个 playbook，通常包含一组有序的任务（也称为 play），针对从清单文件中选的特定托管主机运行。

b. 在文件中插入以下内容：

```yaml
---
- name: Configure kernel_settings
  hosts: all
  roles:
    - kernel_settings
```

4. 可选地验证语法是否正确。

```bash
#### ansible-playbook --check kernel_roles.yml
```

5. 执行您的 playbook。



```bash
#### ansible-playbook kernel_roles.yml
```

输出显示 play 成功完成。

6. 重启您的托管主机并检查内核参数以验证它们已应用。

## 使用 RHEL System Roles 进行 Red Hat Enterprise Linux 8 管理与配置任务

```yaml
vars:
  network_connections:
    - name: enp7s0
      interface_name: enp7s0
      type: ethernet
      autoconnect: yes
      ip:
        address:
          - 192.0.2.1/24
          - 2001:db8::1/64
        gateway4: 192.0.2.254
        gateway6: 2001:db8::ffff
        dns:
          - 192.0.2.200
          - 2001:db8::ffb
      dns_search:
        - example.com
      state: up
```

- 3. 执行 playbook：

  - 要以 root 身份连接到托管主机，输入：

    - `ansible-playbook -u root ~/ethernet-static-IP.yml`

  - 要以用户身份连接到托管主机，输入：

    - `ansible-playbook -u user_name --ask-become ~/ethernet-static-IP.yml`

`--ask-become` 确保 `ansible-playbook` 命令会提示输入 `user_name` 选项中用户的 sudo 密码。

如果你未指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录控制节点的用户身份连接到托管主机。

### 更多资源

- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `ansible-playbook(1)` 帮助页

## 5.2. 使用 RHEL SYSTEM ROLES 通过接口名称配置动态以太网连接

本过程描述了如何通过运行 Ansible playbook 使用 RHEL System Roles 为 `enp7s0` 接口远程添加动态以太网连接。通过此设置，网络连接将从 DHCP 服务器请求该连接的 IP 设置。在控制节点上运行此过程。

### 前提条件

- 网络中可用的 DHCP 服务器。

- 控制节点上已安装 `ansible` 和 `rhel-system-roles` 软件包。

- 如果在运行 playbook 时使用不同于 **root** 的远程用户，则该用户在托管节点上具有适当的 sudo 权限。

- 主机使用 NetworkManager 配置网络。

### 步骤

- 1. 如果要执行 playbook 中指令的主机尚未加入清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` Ansible 清单清单文件中：

```
node.example.com
```

- 2. 创建包含以下内容的 `~/ethernet-dynamic-IP.yml` playbook：

```yaml
---
- name: Configure an Ethernet connection with dynamic IP
hosts: node.example.com
become: true
tasks:
  - include_role:
      name: linux-system-roles.network

vars:
  network_connections:
    - name: enp7s0
      interface_name: enp7s0
      type: ethernet
      autoconfig: yes
      ip:
        dhcp4: yes
        auto6: yes
      state: up
```

- 3. 执行 playbook：

  - 要以 **root** 身份连接到托管主机，输入：

```bash
#### ansible-playbook -u root ~/ethernet-dynamic-IP.yml
```

  - 要以用户身份连接到托管主机，输入：

```bash
#### ansible-playbook -u user_name --ask-become-pass ~/ethernet-dynamic-IP.yml
```

`ask-become-pass` 选项确保 `ansible-playbook` 命令会提示输入 `user_name` 选项中定义用户的 `sudo` 密码。

如果你未指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录控制节点的用户身份连接到托管主机。

### 更多资源

- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `ansible-playbook(1)` 帮助页

## 5.3. 使用 SYSTEM ROLES 配置 VLAN 标签标记

你可以使用 RHEL 网络 Role 来配置 VLAN 标签标记。本过程描述了如何添加一个以太网连接以及一个使用该连接的 ID 为 10 的 VLAN。作为父设备，VLAN 连接包含了 IP、默认网关和 DNS 配置。

请根据你的环境相应调整计划。例如：

- 若将 VLAN 作为其他连接（如 bond 绑定）的端口使用，请省略 IP 属性，并在父级配置中设置 IP 配置。

- 若在 VLAN 中使用 team、bridge 或 bond 设备，请调整你在 VLAN 中使用的端口的 `interface_name` 和 `type` 属性。

前提条件

- 控制节点上已上安装了 `ansible` 和 `rhel-system-roles` 软件包。

- 如果在运行 playbook 时使用远程用户，则该用户在托管节点上具有适当的 sudo 权限。

步骤

- 如果要执行 playbook 中指令的主机尚未加入清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` Ansible 清单清单文件中：

```
node.example.com
```

- 创建包含以下内容的 `~/vlan-ethernet.yml` playbook：

```yaml
---
- name: Configure a VLAN that uses an Ethernet
hosts: node.example.com
become: true
tasks:
  - include_role:
      name: linux-system-roles.network

vars:
  network_connections:
    - name: enp7s
      interface_name: enp7s
      type: ethernet
      autoconnect: yes
      state: up
      ip:
        dhcp4: no
        auto6: no
    - name: vlan
      type: vlan
      id: 10
      ip:
        address:
          - 192.0.2.1/24
          - 2001:db8::1/64
        gateway4: 192.0.2.254
        gateway6: 2001:db8::ffff
        dns:
          - 192.0.2.200
          - 2001:db8::ffb
      dns_search:
        - example.com
```

作为父设备，VLAN 连接包含了 IP、默认网关和 DNS 配置。

- 3. 要以 root 身份连接到托管主机，输入：

```bash
#### ansible-playbook -u root ~/vlan-.yml
```

  - 要以用户身份连接到托管主机，输入：

```bash
#### ansible-playbook -u user_name --ask-become-pass ~/vlan-.yml
```

`ask-become-pass` 选项确保 `ansible-playbook` 命令会提示输入 `user_name` 选项中定义用户的 sudo 密码。

如果你未指定 `user_name` 选项，`ansible-playbook` 将以当前登录控制节点的用户身份连接到托管主机。

更多资源



- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `ansible-playbook(1)` 帮助页

## 5.4. 使用 SYSTEM ROLES 配置桥接 (Bridge)

你可以使用 RHEL Role 来配置桥接。本过程描述了如何通过运行 Ansible playbook 使用 RHEL System Roles 远程添加桥接。

> 注意：桥接通常由多个物理接口组成。

### 前提条件

- 控制节点上已安装了 `ansible` 和 `rhel-system-roles` 软件包。

- 如果在运行 playbook 时使用远程用户，则该用户在托管节点上具有适当的 sudo 权限。

### 步骤

- 1. 如果要执行 playbook 中指令的主机尚未加入清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` Ansible 清单清单文件中：

```
node.example.com
```

- 2. 创建包含以下内容的 `~/bridge.yml` playbook：

```yaml
---
- name: Configure a bridge with dynamic IP
hosts: node.example.com
become: true
tasks:
  - include_role:
      name: linux-system-roles.network

vars:
  network_connections:
    - name: br0
      interface_name: br0
      type: bridge
      state: up
      ip:
        dhcp4: yes
        auto6: yes
      interfaces:
        - enp7s0
        - enp8s0
    - name: enp7s0
      interface_name: enp7s0
      type: ethernet
      master: br0
```

- 3. 执行 playbook：

  - 要以 `root` 身份连接到托管主机，输入：

```bash
#### ansible-playbook -u root ~/bridge.yml
```

  - 要以用户身份连接到托管主机，输入：

```bash
#### ansible-playbook -u user_name --ask-become-pass ~/bridge.yml
```

`ask-become-pass` 选项确保 `ansible-playbook` 命令会提示输入 `user_name` 选项中定义用户的 `sudo` 密码。

如果你未指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录控制节点的用户身份连接到托管主机。

## 在 RHEL 中使用 System Roles 执行 Red Hat Enterprise Linux 8 管理和配置任务

```
become: true
tasks:
  - include_role:
    name: linux-system-roles.network
```

```yaml
vars:
  network_connections:
    # 定义 bond 配置
    - name: bond0
      type: bond
      interface_name: bond0
    ip:
      address:
        - "192.0.2.1/24"
        - "2001:db8::1::64"
      gateway4: 192.0.2.254
      gateway6: 2001:db8::1::fffe
      dns:
        - 192.0.2.200
        - 2001:db8::1::ffbb
    dns_search:
        - example.com
    bond:
      mode: active-backup
      state: up
```

```yaml
### 为 bond 添加一个以太网配置
  - name: bond0-port1
    interface_name: enp7s0
    type: ethernet
    controller: bond0
    state: up
```

```yaml
### 为 bond 添加第二个以太网配置
  - name: bond0-port2
    interface_name: en-p8s0
    type: ethernet
    controller: bond0
    state: up
```

+ 3. 运行 playbook：

  - 要以 root 用户身份连接到托管主机，输入：

    - `ansible-playbook -u root ~/bond-ether.yml`

  - 要以用户身份连接到托管主机，输入：

    - `ansible-playbook -u user_name --ask-become-pass ~/bond-ether.yml`

`--ask-become-pass` 选项会让 `ansible-playbook` 命令提示输入 `-u user_name` 中定义的用户的密码。

如果你未指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录到控制节点的用户身份连接到托管主机。

# 第 5 章：使用 SYSTEM ROLES 配置网络连接

### 额外资源

- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `ansible-playbook(1)` 手页

## 5.6. 使用 RHEL SYSTEM ROLES 配置带有 802.1X 网络身份认证的静态以太网连接

使用 RHEL System Roles，你可以自动化创建一个使用 802.1X 标准认证客户端的以太网连接。本过程描述了如何通过运行 Ansible playbook 为 `enp9s` 接口远程添加一个具有以下设置的以太网连接：

- 静态 IPv4 地址 - 192.0.2.1，配合 /24 子网掩码

- 静态 IPv6 地址 - 2001:db8::1::，配合 /64 子网掩码

- IPv4 默认网关 - 192.0.2.254

- IPv6 默认网关 - 2001:db8::1::fffe

- IPv4 DNS 服务器 - 192.0.2.200

- IPv6 DNS 服务器 - 2001:db8::1::ffbb

- DNS 搜索域 - example.com

- 使用 TLS 可扩展身份验证协议 (EAP) 的 802.1X 网络身份认证

在 Ansible 控制节点上运行此过程。

### 前提条件

- 控制节点上安装了 `ansible` 和 `rhel-system-roles` 软件包。

- 如果运行 playbook 时使用非 root 的其他远程用户，你必须在托管节点上拥有适当的 sudo 权限。

- 网络支持 802.1X 网络身份认证。

- 托管节点使用 NetworkManager。

- TLS 身份认证所需的文件存在控制节点上：

- 客户端密钥存储在 `/srv/data/client.key`。

- 客户端证书存储在 `/srv/data/client.crt`。

- 证书颁发机构 (CA) 证书存储在 `/srv/data/ca.crt`。

### 操作步骤

- 如果要执行 playbook 指令的主机尚未列入清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` 清清单文件中：

```
node.example.com
```

2. 创建包含以下内容的 `~/enable-802.1x.yml` playbook：



```yaml
---
- name: 配置带有 802.1X 身份认证的以太网连接
hosts: node.example.com
become: true
tasks:
  - name: 拷贝 802.1X 身份认证的密钥
    copy:
      src: "/srv/data/client.key"
      dest: "/etc/pki/tls/private/client.key"
      mode: 600
  - name: 拷贝 802.1X 身份认证的客户端证书
    copy:
      src: "/srv/data/client.crt"
      dest: "/etc/pki/tls/certs/client.crt"
  - name: 拷贝 802.1X 身份认证的 CA 证书
    copy:
      src: "/srv/data/ca.crt"
      dest: "/etc/pki/ca-trust/anchors/ca.crt"
  - include_role:
    name: linux-system-roles.network
    vars:
      network_connections:
        name: enp1s0
        type: ethernet
        autoconnect: yes
        ip:
          address:
            - 192.0.2.1/24
            - 2001:db8::1/64
          gateway4: 192.0.2.254
          gateway6: 2001:db8::1::fffe
          dns:
            - 192.0.2.200
            - 2001:db8::1::ffbb
          dns_search:
            - example.com
      802.1x:
        identity: user_name
        eap: tls
        private_key: "/etc/pki/tls/private/client.key"
        private_password: "password"
        client_cert: "/etc/pki/tls/certs/client.crt"
        ca_cert: "/etc/pki/ca-trust/anchors/ca.crt"
        domain_suffix: example.com
        state: up
```

### 3. 运行 playbook

- 要以 root 用户身份连接到托管主机，输入：

  - `ansible-playbook -u root ~/enable-802.1x.yml`

- 要以用户身份连接到托管主机，输入：

  - `ansible-playbook -u user_name --ask-become-pass ~/ethernet-static.yml`

`--ask-become-pass` 选项确保 `ansible-playbook` 命令提示输入 `-u user_name` 选项定义的用户的密码。

如果你未指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录到控制节点的用户身份连接到托管主机。

额外资源

- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `ansible-playbook(1)` 手页

## 5.7 使用 SYSTEM ROLES 为现有连接设置默认网关

可以使用 RHEL System Role 设置默认网关。

### 注意

当运行使用 RHEL System Role 的 play 时，如果设置与 play 中的不匹配，System Role 将覆盖同名的连接。因此，即使连接已存在，也要在 play 中指定整个网络配置。否则，角色会将这些值重置为默认值。

根据连接是否存在，该过程将创建或更新具有以下设置的 `enp1s0` 连接：

- 静态 IPv4 地址 - 198.51.100.20，配合 /24 子网掩码
- 静态 IPv6 地址 - 2001:db8::1::，配合 /64 子网掩码
- IPv4 默认网关 - 198.51.100.254
- IPv6 默认网关 - 2001:db8::1::fffe
- IPv4 DNS 服务器 - 198.51.100.200
- IPv6 DNS 服务器 - 2001:db8::1::ffbb
- DNS 搜索域 - example.com

### 前提条件

- 控制节点上安装了 `ansible` 和 `rhel-system-roles` 软件包。
- 如果运行 playbook 时使用非 root 的远程用户，该用户在托管节点上拥有适当的 sudo 权限。

### 操作步骤

1. 如果要执行 playbook 指令的主机尚未列入清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` Ansible 清单文件中：

```
node.example.com
```

2. 创建包含以下内容的 `~/ethernet-connection.yml` playbook：

```yaml
---
- name: 配置带有静态 IP 和默认网关的以太网连接
  hosts: node.example.com
  become: true
  tasks:
    - include_role:
        name: linux-system-roles.network

vars:
  network_connections:
    - name: enp1s0
      type: ethernet
      autoconnect: yes
      ip:
          address:
            - 192.0.2.1/24
            - 2001:db8::1/64
          gateway4: 192.0.2.254
          gateway6: 2001:db8::1::fffe
          dns:
            - 192.0.2.200
            - 2001:db8::1::ffbb
          dns_search:
            - example.com
  state: up
```

### 额外资源

- `/usr/share/ansible/roles/rhel-system-roles/network/README`

- `ansible-playbook(1)` 手页

## 5.8. 使用 RHEL 系统角色配置静态路由

你可以使用网络 RHEL 系统角色（System Role）来配置静态路由。

![](img/7076193df8761a1565038e17afc88b0b_36_0.png)

> 重要
>
> 当你运行使用网络 RHEL 系统角色的 play 时，如果设置与 play 中指定的设置不匹配，该系统角色将覆盖同名的现有连接配置。因此，请务必在 play 中指定网络连接配置的完整内容，即使例如 IP 配置已经存在。否则，该角色会将这些值重置为默认值。

根据配置是否已存在，该过程将创建或更新具有以下设置的 `enp7s0` 连接：

- 静态 IPv4 地址 - 198.51.100.20，配合 /24 子子网掩码
- 静态 IPv6 地址 - 2001:db8:1::1，配合 /64 子子网掩码
- IPv4 默认网关 - 198.51.100.254
- IPv6 默认网关 - 2001:db8:1::fffe
- IPv4 DNS 服务器 - 198.51.100.200
- IPv6 DNS 服务器域名 - 2001:db8:1::ffbb
- DNS 服务器域名 - example.com
- 192.0.2.0/24，网关为 198.51.100.101
- 203.0.113.0/24，网关为 198.51.100.22

### 前提条件

- 控制节点上安装了 `ansible` 和 `rhel-system-roles` 软件包。
- 如果在运行 playbook 时使用 root 以外的用户，则该用户在受管节点上具有适当的 sudo 权限。

### 步骤

1. 如果要在 playbook 中执行指令的主机尚未加入清单机清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` Ansible 清单文件中：

```
node.example.com
```

2. 创建包含以下内容的 `~/add-static-routes.yml` playbook：



```yaml
---
name: 配置带有静态 IP 和额外路由的以太网连接
hosts: node.example.com
become: true
tasks:
  - include_role:
      name: linux-system-roles.network
    vars:
      network_connections:
        - name: enp7s0
          type: ethernet
          autoconnect: yes
          ip:
            address:
              - 198.51.100.20/24
              - 2001:db8::1/64
            gateway4: 198.51.100.254
            gateway6: 2001:db8::1fffe
          dns:
            - 198.51.100.200
            - 2001:db8::1ffb
          dns_search:
            - example.com
          route:
            - network: 192.0.2.0
              prefix: 24
              gateway: 198.51.100.1
            - network: 203.0.113.0
              prefix: 24
              gateway: 198.51.100.2
      state: up
```

### 3. 运行 playbook

- 以 root 用户身份连接到受管节点，输入：

```
ansible-playbook -u root ~/add-static-routes.yml
```

- 以用户身份连接到受管节点，输入：

```
ansible-playbook -u user_name --ask-become-pass ~/add-static-routes.yml
```

`--ask-become-pass` 选项确保 `ansible-playbook` 命令提示输入 `-u user_name` 选项定义用户的 sudo 密码。如果你没有指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录控制节点的用户身份连接到受管节点。

### 验证步骤

- 显示路由表：

```
ip route
default via 198.51.100.254 dev enp7s0 proto metric 100
192.0.2.0/24 via 198.51.100.101 dev enp7s0 proto metric 100
203.0.113.0/24 via 198.51.100.22 dev enp7s0 proto metric 100
```

## 5.9. 使用系统角色设置 TOOL 特性

你可以使用网络 RHEL 系统角色配置网络连接的 ethtool 特性。

> 重要
>
> 当你运行使用网络 RHEL 系统角色的 play 时，如果设置与 play 中指定的设置不匹配，该系统角色将覆盖同名的现有连接配置。因此，请务必在 play 中指定网络连接配置的完整内容，即使例如 IP 配置已经存在。否则，该角色会将这些值重置为默认值。

### 使用 RHEL 中的 System Roles 进行 Red Hat Enterprise Linux 管理和配置任务

- 如果您在运行 playbook 时使用远程 root 用户，则该用户在托管节点上具有相应的 sudo 权限。

### 操作步骤

- 1. 如果您想要在 playbook 中执行指令的宿主机尚未尚未清单清单，请将该主机的 IP 或名称添加到 `/etc/ansible/hosts` Ansible 清单文件中：

```
node.example.com
```

- 2. 创建一个包含以下内容的 `~/configure-ethernet-device-with-ethtoolcoalesce-settings.yml` playbook：

```yaml
name: Configure an Ethernet connection with ethtool coalesce settings
hosts: node.example.com
become: true
tasks:
  - include_role:
      name: linux-system-roles.network

vars:
  network_connections:
    - name: enp1s0
      type: ethernet
      autoconnect: yes
      ip:
        address:
        - 198.51.100.20/24
        - 2001:db8:1::/64
      gateway4: 198.51.100.254
      gateway6: 2001:db8:1::fffe
      dns:
        - 198.51.100.200
        - 2001:db8:1::ffbb
      dns_search:
        - example.com
  ethtool:
    coalesce:
      rx_frames: 128
      tx_frames: 128
      state: up
```

- 3. 运行 playbook

- 要以 root 用户连接到托管主机，输入：

`ansible-playbook -u root ~/configure-ethernet-device-with-ethtoolcoalesce-settings.yml`

- 要以用户身份连接到托管主机，输入：

`ansible-playbook -u user_name --ask-become-pass ~/configure-ethernet-device-with-ethtoolcoalesce-settings.yml`

`--become-pass` 选项确保 `ansible-playbook` 命令会提示输入在 `-u user_name` 选项中定义的用户的 sudo 密码。

如果您未指定 `-u user_name` 选项，`ansible-playbook` 将以当前登录控制节点的用户身份连接到托管主机。

### 额外资源

- `/usr/share/ansible/roles/rhel-system-roles.network/README.md`

- `ansible-playbook(1)` man page

# 第 6 章 使用 SYSTEM ROLES 配置 SELINUX

## 6.1. SELINUX 系统角色简介

RHEL System Roles 是 Ansible 角色和模块的集合，提供了一个一致的配置接口，用于远程管理多个 RHEL 系统。SELinux 系统角色允许以下操作：

- 清理与 SELinux 布尔值（booleans）、文件上下文、端口和登录相关的策略修改。
- 设置 SELinux 策略布尔值、文件上下文、端口和登录。
- 恢复指定文件或目录上的文件上下文。
- 管理 SELinux 模块。

下表提供了 SELinux 系统角色中可用输入变量的概述。

表 6.1. SELinux 角色变量

| 角色变量 | 说明 | CLI 替代方案 |
| --- | --- | --- |
| `selinux_policy` | 选择保护目标进程或多级安全保护的策略。 | `/etc/selinux/config` 中的 `SELINUXTYPE` |
| `selinux_state` | 切换 SELinux 模式。参见 `ansible-doc selinux` | `/etc/selinux/config` 中的 `setforce` 和 `SELINUX` |
| `selinux_booleans` | 启用和禁用 SELinux 布尔值。参见 `ansible-doc seboolean`。 | `setsebool` |
| `selinux_fcontexts` | 添加或删除 SELinux 文件上下文映射。参见 `ansible-doc fcontext`。 | `semanage fcontext` |
| `selinux_restore_dirs` | 恢复文件系统树上的 SELinux 标签。 | `restorecon -R` |
| `selinux_ports` | 设置端口上的 SELinux 标签。参见 `ansible-doc deport.` | `semanage port` |



| `selinux_logins` | 将用户映射到 SELinux 用户。参见 `ansible-doc login`。 | `semanage login` |

| `selinux_modules` | 安装、启用、禁用或删除 SELinux 模块。 | `semodule` |

由 `rhel-system-roles` 软件包安装的 `example-selinux-playbook.yml` 示例 playbook 演示了如何在强制模式（enforcing mode）下设置目标策略。该 playbook 还应用了若干本地策略，并恢复了你在 `/tmp/test_dir/` 中经过验证的上下文。

有关 SELinux 变量的详细参考，请安装 `rhel-system-roles` 软件包，并查看 `/usr/share/doc/rhel-system-roles/selinux/` 目录下的 `README.md` 或 `README.html` 文件。

额外资源

- RHEL System Roles 简介。

## 6.2. 使用 SELINUX 系统角色在多个系统上应用 SELINUX 设置

按照以下步骤准备并应用带有已验证设置的 Ansible playbook。

### 先决条件

- 您的 RHEL 订阅已绑定。

### 操作步骤

- 启用存储库：

```bash
### subscription-manager repos --enable
```

- 安装 Ansible：

```bash
### subscription-manager ansible
```

- 安装 `rhel-system-roles` 软件包：

```bash
#### yum install rhel-system-roles
```

- 准备您的 playbook：

```bash
### cp /usr/share/doc/rhel-system-roles/selinux/example-selinux-playbook.yml my-selinux.yml
```

- 修改 playbook 内容以符合场景：

```bash
# vi my-selinux.yml
```

- 在 `host1`、`host2` 和 `host3` 上运行您的 playbook：

```bash
### ansible-playbook -i host1,host2,host3 my-selinux.yml
```

# 第 7 章 使用 LOGGING ROLE

作为系统管理员，您可以使用 Logging Role 配置 RHEL 主机作为日志服务器，从许多客户端系统收集日志。

## 7.1. LOGGING ROLE

通过 Logging Role，您可以在本地和远程主机上部署日志配置。

要在多个系统上应用日志角色，您需要在 playbook 中定义日志配置。playbook 是一个或多个剧（plays）的列表。playbook 是易读的，并以 YAML 格式编写。有关 playbook 的更多信息，请参阅 Ansible 文档。

您希望 Ansible 配置的系统集在清单文件中定义。有关如何构建清单的更多信息，请参阅 Ansible 文档。

日志日志解决方案提供了多种读取日志的方法和多种日志输出。

例如，日志系统可以接收以下输入：

- 本地文件

- `systemd/journal`

- 网络上的另一个日志系统

此外，日志系统可以具有以下输出：

- 存储在 `/var/log` 目录下的本地文件

- 发送到 Elasticsearch

- 转发到另一个日志系统

通过日志角色，您可以组合输入和输出以满足需求。例如，可以配置一种日志解决方案，将 journal 的输入存储在本地文件中，而将文件的输入既转发到另一个日志系统存储在本地文件中。

## 7.2. LOGGING ROLE 参数

在 Logging Role playbook 中，您在 `logging_inputs` 参数中定义输入，在 `logging_outputs` 参数中定义输出，并在 `logging_flows` 参数中定义输入与输出之间的关系。Logging Role 使用额外选项处理这些变量以配置日志系统。您还可以启用加密。

> 注意
>
> 目前 Logging Role 中唯一可用的日志系统是 Rsyslog。

- `logging_inputs`: 日志解决方案的输入列表。

  - `name`: 输入的唯一名称。在 `logging_flows: inputs` 列表未使用，也是生成文件名的一部分。

- `type`: 输入元素的类型。该类型指定一个任务类型，该类型对应 `files/rsyslog/tasks,vars/inputs/` 目录下的目录名。

- `basics`: 配置来自 `systemd` 或 `unix socket` 的输入。

- `kernel_message`: 如果设置为 `true`，则使用默认的 `imlog`。默认为 `false`。

- `use_imusock`: 使用 `imsock` 代替 `imjournal`。默认为 `false`。

- `ratimiter_burst`: 在 `ratimiter_interval` 间隔内可以发送的最大消息数。如果 `use_imusock` 为 `false`，默认为 `20000`。如果 `use_imusock` 为 `true`，则默认为 `200`。

- `ratimiter_interval`: 评估 `ratimiter_burst` 的间隔。如果 `use_imusock` 为 `false`，默认为 `600` 秒。如果 `use_imusock` 为 `true`，则默认为 `0`。这表示速率限制已关闭。

- `persist_state_interval`: 每隔 `persist_state_interval` 数量的消息，就会持久化一次 Journal 状态。默认为 `10`。仅在 `use_imusock` 为 `false` 时有效。

- `files`: 配置来自本地文件的输入。

- `remote`: 配置来自网络上其他日志系统的输入。

- `state`: 配置文件的状态。存在（`present`）或不存在（`absent`）。默认位 `present`。

- `logging_outputs`: 日志解决方案的输出列表。

- `files`: 配置到本地文件的输出。

- `forwards`: 配置转发到另一个日志系统的输出。

- `remote_files`: 配置从另一个日志系统到本地文件的输出。

- `logging_flows`: 定义日志输入和日志输出之间关系的流列表。`logging_flows` 变量具有以下键值：

- `name`: 流的唯一名称

- `inputs`: `logging_inputs` 名称值的列表

- `outputs`: `logging_outputs` 名称值的列表。

额外资源

- 伴随 `rhel-system-roles` 软件包安装的文档位于：`/usr/share/ansible/roles/rhel-system-roles.logging/README.html`

## 7.3. 应用本地日志系统角色

按照以下步骤准备并应用 Red Hat Ansible playbook，以在多台独立的机器上配置日志解决方案。每台机器都将在本地记录日志。

### 先决条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意
>
> 你并不需要在想要部署日志解决方案的系统上安装 Red Hat Ansible Engine。

- 你在运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。

> 注意
>
> 你不需要安装 `rsyslog`，因为系统角色在部署时会安装 `rsyslog`。

- 你有一个列出要配置日志系统的系统的文件。

### 步骤

- 1. 创建一个定义所需角色的 playbook：

    a. 创建一个新的 YAML 文件并用文本编辑器打开它，例如：

```
# vi logging-playbook.yml
```

    b. 插入以下内容：

```
---
- name: Deploying basics input and implicit files output
hosts: all
roles:
  - linux-system-roles.logging
vars:
  logging_inputs:
    - name: system_input
      type: basics
  logging_outputs:
    - name: files_output
      type: files
  logging_flows:
    - name: flow1
      inputs: [system_input]
      outputs: [files_output]
```

- 2. 在特定的清单上执行 playbook：

```
#### ansible-playbook -i inventory-file /path/to/file/logging-playbook.yml
```



其中：`inventory-file` 是清单文件。`logging-playbook.yml` 是你使用的 playbook。

### 验证

- 1. 测试 `/etc/rsyslog.conf` 文件的语法：

```
#### rsyslog -N 1
syslog: version 8.911.0-6.el8, config validation run (level 1), master config
/etc/rsyslog.conf
syslog: End of config validation run. Bye.
```

- 1. 验证系统是否向日志发送了消息：

    a. 发送测试消息：

```
#### logger test
```

    b. 查看 `/var/log/messages` 日志，例如：

```
### cat /var/log/messages
Aug 5 13:48:31 hostname root[6778]: test
```

其中 `hostname` 是客户端系统的主机名。注意日志包含了输入 `logger` 命令的用户名，在此例中为 `root`。

## 7.4. 在本地日志系统角色中过滤日志

你可以部署一个基于 `rsyslog` 属性过滤器的日志过滤解决方案。

### 先决条件

- 拥有一个或多个受管理节点的访问权限，这些系统是你想要用日志系统角色配置的系统。
- 拥有控制节点的访问权限，该节点是你通过 Red Hat Ansible Engine 配置其他系统的系统。

在控制节点上：

- 已安装 Red Hat Ansible Engine
- 已安装 `rhel-system-roles` 软件包
- 有一个列出受管理节点的清单文件。

### 步骤

- 1. 创建一个包含以下内容的 `playbook.yml` 文件：

```
- name: Deploying files input and configured files output
hosts: all
roles:
  - linux-system-roles.logging
vars:
  logging_inputs:
    - name: files_input0
      type: files
      input_log_path: /var/log/containerA*/.log
    - name: files_input1
      type: files
      input_log_path: /var/log/containerB/*.log
logging_outputs:
  - name: files_output0
    type: files
    property: msg
    property_op: contains
    property_value: error
    path: /var/log/errors.log
  - name: files_output1
    type: files
    property: msg
    property_op: "contains"
    property_value: error
    path: /var/log/others.log
logging_flows:
  - name: flow0
    inputs: [files_input0, files_input1]
    outputs: [files_output0, files_output1]
```

使用此配置，所有包含 `error` 字符串的消息都会记录在 `/var/log/errors.log`，其他消息记录在 `/var/log/others.log`。

你可以根据过滤过滤字符串替换 `error` 值。

你可以根据喜好修改变量。

- 1. 可选：验证 playbook 语法。

   `# ansible-playbook --check playbook.yml`

- 2. 在清单上运行 playbook：

   `# ansible-playbook -i inventory-file playbook.yml`

#### 验证

- 1. 测试 `/etc/rsyslog.conf` 文件的语法：

```
#### rsyslog -N 1
syslog: version 8.911.0-6.el8, config validation run (level 1), master config
/etc/rsyslog.conf
syslog: End of config validation run. Bye.
```

- 2. 验证系统是否向日志发送了包含 `error` 字符串的消息：

    a. 发送测试消息：

    `# logger error`

    b. 查看 `/var/log/errors.log` 日志，例如：

```
#### cat /var/log/errors.log
Aug 5 13:48:31 hostname[6778]: error
```

其中 `hostname` 是客户端系统的主机名。注意日志包含了输入 `logger` 命令的用户名，在此例中为 `root`。

```yaml
roles:
  - linux-system-roles.logging
vars:
  logging_inputs:
    - name: remote_udp
      type: remote
      udp_ports: [ 601]
    - name: remote_tcp
      type: remote
      tcp_ports: [ 601]
  logging_outputs:
    - name: remote_files_output
      type: remote_files
  logging_flows:
    - name: flow_0
      inputs: [remote_udp_input, remote_tcp_input]
      outputs: [remote_files_output]
```

- name: Deploying basics in and forwards

hosts:

  roles:

    - linux-system-roles.logging

vars:

  logging_inputs:

    - name: basic_input

      type: basics

  logging_outputs:

    - name: forward_output0

      type: forwards

      severity: info

      target:host1.example.com

      udp_port: 601

    - name: forward_output1

      type: forwards

      facility: mail

      target:host1.example.com

      tcp_port: 601

logging_flows:

    - name: flows0

      inputs: [basic_input]

      outputs: [forward_output0, forward_output1]

[basic_input]

[forward_output0, forward_output1]

其中 `host1.example.com` 是日志服务器。

> 注意

您可以修改 playbook 中的参数以适应您的需求。

![](img/7076193df8761a1565038e17afc88b0b_52_0.png)

## 使用 RHEL 中的系统角色进行 Red Hat Enterprise Linux 8 管理和配置任务

> > 警告

日志解决方案仅适用于服务器或客户端系统 SELinux 策略中定义的端口，且默认的 SELinux 策略包含端口 `601`、`514`、`6514`、`10514` 和 `20514`。如需使用不同的端口，请在客户端和服务器系统上修改 SELinux 策略。目前尚不支持通过系统角色配置防火墙。

- 2. 创建列出服务器和客户端的清单文件：

    a. 创建一个新文件并在文本编辑器中打开它，例如：

        ```
        vi inventory.ini
        ```

    b. 将以下内容插入清单文件中：

        ```
        [servers]
        ansible ansible_host=host1.example.com
        [clients]
        client ansible_host=host2.example.com
        ```

- 其中：

* `host1.example.com` 是日志服务器。
* `host2.example.com` 是日志客户端。

- 3. 在您的清单上执行 playbook。



```
ansible-playbook -i /path/to/file/inventory.ini /path/to/file/_logging-playbook.yml
```

其中：

* `inventory.ini` 是清单文件。
* `logging-playbook.yml` 是您创建的 playbook。

#### 验证

1. 在客户端和服务器系统上，测试 `/etc/rsyslog.conf` 文件的语法：

```
# rsyslog -N 1
rsyslog: version 8.911.0-6.el8, config validation run (level 1), master config
/etc/rsyslog.conf
rsyslog: End of config validation run. Bye.
```

2. 验证客户端是否向服务器发送了消息：

a. 在客户端系统上，发送一条测试消息：

b. 在服务器系统上，查看 `/var/log/messages` 日志，例如：

```
### cat /var/log/messages
Aug 5 13:48:31 host2.example.com root[6788]: test
```

其中 `host2.example.com` 是客户端系统的主机名。注意，日志中包含了输入 `logger` 命令的用户名，在此例中为 `root`。

### 额外资源

- 开始使用 RHEL 系统角色
- `/usr/share/ansible/roles/rhel-system-roles.logging/README.html` 中的 `rhel-system-roles` 软件包
- RHEL 系统角色

## 7.6. 额外资源

- 开始使用 RHEL 系统角色
- 安装 `rhel-system-roles` 软件包的文档，位于 `/usr/share/ansible/roles/rhel-system-roles.logging/README.html`。
- RHEL 系统角色。
- `ansible-playbook(1)` 手帮助页。

# 第8章. 使用 SSH 系统角色配置安全通信

作为管理员，您可以使用 Red Hat Ansible Automation Platform，通过 SSHD 系统角色配置 SSH 服务器，并使用 SSH 系统角色在任意数量的 RHEL 系统上同时进行一致的配置 SSH 客户端。

# 8.1. SSH 系统角色变量

在 SSH 系统角色 playbook 中，您可以根据自己的偏好和限制定义 SSH 配置文件的参数。

如果您不配置这些变量，系统角色将生成一个与 RHEL 默认值相匹配的 `sshd_config` 文件。

在所有情况下，布尔值在 SSH 配置中会正确渲染为 `yes` 和 `no`。您可以使用列表定义多行配置项：

- `sshd_ListenAddress`:
  - `0.0.0.0`

渲染为：

- `ListenAddress 0.0.0`

## SSH 系统角色的变量

- `sshd_enable`:
如果设置为 `False`，则该角色被完全禁用。默认为 `True`。

- `sshd_skip_defaults`:
如果设置为 `True`，系统角色不会应用默认值。相反，使用 `sshd` 字典指定完整的配置集。如果设置为 `False`，则不管理服务，这意味着它在启动时不会启用。在容器内或 AIX 上运行时默认为 `True`。

- `sshd_allow_reload`:
如果设置为 `False`，`sshd` 在配置更改后不会重加载。这有助于故障排除。要应用更改的配置，请手动重加载 `sshd`。除 AIX 外，默认值与 `sshd_manage_service` 相同，后者默认为 `True`。

- `sshd_install_service`:
如果设置为 `True`，该角色将安装 `sshd` 服务文件。除非您正在配置第二个实例并更改了 `sshd_service` 变量，否则默认为 `False`。该角色使用以下模板：
- `sshd_service_template` (default: `templates/sshd_service.j2`)
- `sshd_service_template_at` (default: `templates/sshd@service.j2`)
- `sshd_service_template_socket` (default: `templates/sshd.socket.j2`)

- `sshd_service`:
此变量更改 `sshd` 服务名称，适用于配置第二个 `sshd` 服务实例。

- `sshd`:
包含配置的字典。例如：

```
sshd:
  Compression: yes
  ListenAddress: 0.0.0
```

- `sshd_Option`:
可以使用由 `sshd` 前缀和选项名称变量来定义选项，而不是字典。变量会覆盖 `sshd` 字典中的值。例如：

```
sshd_Compression: no
```

- `sshd_match`:
`match` 部分的字典列表或字典。注意这些变量不会覆盖 `sshd` 字典中的 `match` 块。所有源将反映在结果文件中。

### SSHD 角色的辅助变量

您可以使用这些变量覆盖每个支持平台的默认值。

- `sshd_packages`:
您可以使用此变量覆盖默认的软件包列表。

- `sshd_config_owner`, `sshd_config_group` 和 `sshd_config_mode`:
您可以设置此角色生成的 openssh 配置文件的所有者和权限。

- `sshd_config_file`:
该角色设置 openssh 服务器配置的路径。

- `sshd_binary`:
openssh 的 `sshd` 可执行文件路径。

- `sshd_service`:
`sshd` 服务的名称。默认情况下，此变量包含目标平台使用的 `sshd` 服务名称。当角色使用 `sshd_install_service` 变量时，也可以用它设置自定义 `sshd` 服务名称。

- `sshd_verify_hostkeys`:
默认为 `auto`。设置为 `auto` 时，它会列出配置文件中存在的主主机并生成不存在的路径。此外，权限和文件设置为默认值。这在部署阶段使用该角色以确保服务可以启动。要禁用此检查，请将此变量设置为空列表 `[]`。

- `sshd_hostkey_owner`, `sshd_hostkey_group`, `sshd_hostkey_mode`:
使用这些变量设置 `sshd_verify_hostkeys` 密钥的所有者和权限。

- `sshd_sysconfig`:
在基于 RHEL 的系统上，此变量配置 ssh 服务的额外细节。如果设置为 `true`，它还会根据以下配置解析 `/etc/sysconfig/sshd` 文件。默认为 `false`。

- `sshd_sysconfig_override_crypto_policy`:
在 RHEL 中，设置为 `true` 时，此变量将覆盖全局加密策略。默认为 `false`。

- `sshd_sysconfig_use_strong_rng`:
在基于 RHEL 的系统上，此变量可以强制 `sshd` 根据作为参数提供的字节数重新种子随机数生成器。默认值为 `0`，禁用此功能。如果系统没有硬件随机数生成器，请勿开启此项。

# 8.2. 使用 SSH 系统角色配置 OpenSSH 服务器

您可以通过运行 Ansible playbook 使用 SSHD 系统角色配置多个 SSH 服务器。

### 前提条件

- 访问一个或多个受管理节点的权限（即希望使用 SSHD 系统角色配置的系统）。
- 访问控制节点的权限（即 Red Hat Ansible Engine 配置其他系统的系统）。

在控制节点上：

- 安装了 Red Hat Ansible Engine。
- 安装了 `rhel-system-roles` 软件包。
- 一个列出受管理节点的清单文件。

### 步骤

1. 复制 SSHD 色的示例 playbook：

```bash
#### cp /usr/share/doc/rhel-system-roles/sshd/example-root-login-playbook.yml path/custom-playbook.yml
```

2. 使用文本编辑器打开复制的 playbook，例如：

```bash
# vim path/custom-playbook.yml
---
- hosts: all
tasks:
  - name: 配置 sshd 以防止特定子网以外的 root 和密码登录
```

## 第 8 章：使用 SSH 系统角色配置安全通信



```yaml
include_role:
  name: rhel-system-roles.sshd
vars:
  sshd:
    # 仅从特定子网允许 root 登录和密码登录
    PermitRootLogin: no
    PasswordAuthentication: no
    Match:
      - Condition: "Address 192.0.2.0/24"
        PermitRootLogin: yes
        PasswordAuthentication: yes
```

该剧本（playbook）将受控节点配置为 SSH 服务器，配置如下：

- 禁用了密码登录和 root 用户登录
- 仅从子网 `192.0.2.0/24` 启用密码登录和 root 用户登录

你可以根据喜好修改变量。有关更多信息，请参阅 SSHD 服务器系统角色变量。

### 可选：验证剧本语法

```bash
ansible-playbook --syntax-check path/custom-playbook.yml
```

### 在你的清单文件上运行剧本

```bash
ansible-playbook -i inventory_file path/custom-playbook.yml
...
PLAY RECAP
****************************************************

localhost : ok=12 changed=2 unreachable=0 failed=0
skipped=10 rescued=0 ignored=0
```

#### 验证

1. 登录到 SSH 服务器：

```bash
$ ssh user1@10.1.1.1
```

其中：

- `user1` 是 SSH 服务器上的一个用户。
- `10.1.1.1` 是 SSH 服务器的 IP 地址。

2. 检查 SSH 服务器上 `sshd_config` 文件的内容：

```bash
# vim /etc/ssh/sshd_config
# Ansible managed
HostKey /etc/ssh/ssh_host_rsa_key
```

```bash
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
AcceptEnv LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
AcceptEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
AcceptEnv LC_IDENTIFICATION LC_ALL_LANGUAGE
AcceptEnv XMODIFIERS
AuthorizedKeysFile .ssh/authorized_keys
ChallengeResponseAuthentication no
GSSAPICAuthentication yes
GSSAPICleanupCredentials no
PasswordAuthentication no
PermitRootLogin no
Subsystem sftp /usr/lib/exec/openssl/sftp-server
SyslogFacility AUTHPRIV
UsePAM yes
X11Forwarding yes
Match Address 192.0.2.0/24
PasswordAuthentication yes
PermitRootLogin yes
```

3. 检查你是否可以从 `192.0.2.0/24` 子网以 root 身份连接服务器：

a. 确定你的 IP 地址：

```bash
$ hostname -l
192.0.2.1
```

如果 IP 地址在 `192.0.2.1 - 192.0.2.254` 范围内，你就可以连接到服务器。

b. 以 root 身份连接到服务器：

```bash
$ ssh root@10.1.1.1
```

额外资源

- `/usr/share/doc/rhel-system-roles/sshd/README.md` 文件。
- `ansible-playbook(1)` 手页。

## 8.3 SSH 系统角色变量

在 SSH 系统角色中，你可以根据自己的喜好和限制为客户端 SSH 配置文件定义参数。

如果你不配置这些变量，系统角色将生成一个与 RHEL 默认设置匹配的全局 `ssh_config` 文件。

在所有情况下，布尔值在 ssh 配置中会正确渲染为 `yes` 或 `no`。你可以使用列表定义多行配置项。例如：

```yaml
LocalForward:
- 22 localhost:2222
- 403 localhost:4003
```

渲染为：

```text
LocalForward 22 localhost:2222
LocalForward 403 localhost:4003
```

> 注意
> 配置选项对大小写敏感。

### SSH 系统角色的变量

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

#### `ssh_skip_defaults`

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

#### `ssh_drop_in_name`

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

#### `ssh_skip_defaults`

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

#### `ssh_drop_in_name`

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

#### `ssh_skip_defaults`

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

#### `ssh_drop_in_name`

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。



### ssh_skip_defaults

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

### ssh_drop_in_name

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
>
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

### ssh_user

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

## 第 9 章：跨系统设置自定义加密策略

作为管理员，你可以使用加密策略角色在 RHEL 上通过 Red Hat Automation Platform 快速且一致地配置多个不同的系统。

### 9.1 加密策略系统角色变量与事实

在加密策略系统角色剧本中，你可以根据喜好和限制为加密策略配置定义参数。

如果你不配置这些变量，系统角色将不会配置系统，仅报告事实。

加密策略角色的可选变量

`crypto_policies_policy`

确定系统角色应用于受控节点的加密策略级别。有关不同加密策略级别的详细信息，请参阅系统级加密策略。

`crypto_policies_reload`

如果设置为 `yes`，在应用策略后受影响的服务（当前为 helpsec、bind 和 ssh 服务）将加载。默认值为 `yes`。

`crypto_policies_reboot_ok`

如果设置为 `yes`，且系统角色更改加密策略后需要重启，它将设置 `crypto_policies_reboot_required`。默认值为 `no`。

由加密策略角色设置的事实

`crypto_policies_active`

列出当前选择的策略。

`crypto_policies_available_policies`

列出系统中所有范围内策略级别。

`crypto_policies_available_modules`

列出系统中所有范围内子策略模块。

### 9.2 使用加密策略角色设置自定义加密策略

你可以使用加密策略角色从单个控制节点一致地配置大量受控节点。

访问一个或多个受管理节点的权限，这些节点是您希望使用加密策略系统角色（Crypto Policies System Role）配置的系统。

访问控制节点的权限，控制节点是 Red Hat Ansible Engine 用于配置其他系统的系统。

在控制节点上：

- 已安装 Red Hat Ansible Engine



- 已安装 `rhel-system-roles` 软件包
- 一个列出受管理节点的清单文件。

### 步骤

- 创建一个包含以下内容的新 `playbook.yml` 文件：

```
---
- hosts: all
tasks:
  - name: Configure crypto policies
    include_role:
    - name: linux-system-roles.crypto_policies
vars:
  - crypto_policies_policy: FUTURE
  - crypto_policies_reboot_ok: true
```

你可以将 `FUTURE` 值替换为您偏的加密策略，例如：`DEFAULT`、`LEGACY` 和 `FIPSOPSP`。

`crypto_policies_reboot_ok: true` 变量会导致系统在更改加密策略后重启。

有关更多详细信息，请参阅加密策略系统角色变量和事实（Crypto Policies System Role variables and facts）。

- 可选：验证 playbook 语法。

```
ansible-playbook --syntax-check playbook.yml
```

- 在您的清单文件上运行 playbook：

```
ansible-playbook -i inventory_file playbook.yml
```

#### 验证

- 在控制节点上，创建另一个名为例如 `verify_playbook.yml` 的 playbook。

```
- hosts: all
tasks:
  - name: Verify active crypto policy
    include_role:
    - name: linux-system-roles.crypto_policies
debug:
  - var: crypto_policies_active
```

此 playbook 不更改系统上的任何配置，仅报告受管理节点上激活的策略。

2. 在同一清单文件上运行 playbook：

```
ansible-playbook -i inventory_file verify_playbook.yml

TASK [debug] *********************
ok: [host] => {
  "crypto_policies_active": "FUTURE"
}
```

`crypto_policies_active` 变量显示受管理节点上激活的策略。

## 9.3. 附加资源

- `/usr/share/ansible/roles/rhel-system-roles/crypto_policies/README.md` 文件。
- `ansible-playbook(1)` 手页。
- 安装 RHEL 系统角色 ..
- 应用系统角色。

# 第 10 章. 使用 CLEVIS 和 TANG 系统角色

## 10.1. CLEVIS 和 TANG 系统角色简介

RHEL 系统角色是 Ansible 角色和模块的集合，提供了一个一致的配置接口，用于远程管理 RHEL 解密。

RHEL 8.3 引入了 Ansible 角色，用于使用 Clevis 和 Tang 自动化部署基于策略的解密（PBD）解决方案。`rhel-system-roles` 软件包包含了这些系统角色、相关示例以及相关参考文档。

`nbnd_client` 角色允许您以自动化方式部署多个 Clevis 客户端。注意，`nbnd_client` 角色仅支持绑定（bindings），您无法将其用于 TPM2。

`nbnd_client` 角色需要已使用 LUKS 加密的卷。LUKS 支持将经 LUKS 加密的卷绑定到一个或多个网络边界加密（NBDE）服务器 - Tang。您可以使用密码保留现有的卷加密，也可以将其移除。在移除密码后，您可以仅使用 NBDE 解锁该卷。当卷最初使用临时密钥或密码加密，且您在提供提供系统后将其移除时，这种方法非常有用。

如果您同时提供了密码和密钥文件，该角色将使用您先提供的任何一个值。如果没有找到任何一个值，它将尝试从现有的绑定中检索密码。

PBD 将绑定定义为设备到槽位（slot）的映射。这意味着您可以对同一个设备拥有多个绑定。默认槽位为 1。

`nbnd_client` 角色还提供了 `state` 变量。使用 `present` 值来创建新绑定或更新现有绑定。与 `clevis bind` 命令不同，您可以使用 `state: present` 来覆盖设备槽位中的现有绑定。`absent` 值会移除指定的绑定。

使用 `nbnd_server`，您可以将 Tang 服务器作为自动化加密解决方案的一部分进行部署和管理。该角色支持以下功能：

- 轮换 Tang 密钥
- 部署和备份 Tang 密钥

### 附加资源

- 有关网络边界加密（NBDE）角色变量的详细参考，请安装 `rhel-system-roles` 软件包，并查看 `/usr/share/doc/rhel-system-roles/nbnd_client/` 和 `/usr/share/ansible/roles/rhel-system-roles/nbnd_server/` 目录下的 `README.md` 和 `README.html` 文件。
- 示例角色 playbooks，请安装 `rhel-system-roles` 软件包，并查看 `/usr/share/ansible/roles/rhel-system-roles/nbnd_server/` 目录。
- 有关 RHEL 系统角色的更多信息，请参阅 `系统角色简介`

## 10.2. 使用 NBDE_SERVER 系统角色设置多个 TANG 服务器

使用 RHEL 系统角色进行 Red Hat Enterprise Linux 管理和配置任务

按照以下步骤准备并应用包含 Tang 设置的 Ansible playbook。

### 前提条件

- 您的 Red Hat Ansible Engine 已连接到系统。参见相关文章。

### 步骤

1. 启用 RHEL 仓库，例如：

```
subscription-manager
```

2. 安装 Ansible Engine：

```
yum
```

3. 安装系统角色：

```
yum install rhel-system-roles
```

4. 准备包含 Tang 设置的 playbook。您可以从零开始，也可以使用示例之一：

```
cp /usr/share/ansible/roles/rhel-system-roles.nbnd_server/examples/playbook.yml .
```

5. 在文本编辑器中编辑 playbook，例如：

```
vi playbook.yml
```

6. 添加必要的参数。以下示例了轮换：

```
---
- hosts: all
vars:
  nbde_server: yes

roles:
- linux-system-roles
```

7. 应用完成的 playbook：

```
ansible-playbook -i inventory_file playbook.yml
```

### 重要

在安装了 Clevis 的系统上使用 grub 工具确保在启动早期可以使用 Tang 的网络：

```
grubby --update-kernel=ALL --args="rd.neednet=1"
```

## 10.3. 使用 NBDE_CLIENT 角色设置多个 CLEVIS 客户端

`nbnd_client` 角色仅支持绑定。这意味着您无法将其用于 TPM2。

以下示例配置了 Clevis 客户端，以便在两个服务器中任一可用时自动解锁这些 LUKS 加密的卷：

```
---
hosts: all
vars:
  nbde_client:
    device: /dev/rhel/root
    encryption_key_src: /etc/luks/keyfile
    servers:
      - http://server1.example.com
      - http://server2.example.com
    device: /dev/rhel/swap
    encryption_key_src: /etc/luks/keyfile
    servers:
      - http://server1.example.com
      - http://server2.example.com
```

roles:

- linux-system-roles.nbde_client

# 第 11 章。使用 RHEL 系统角色请求证书



使用证书系统角色（Certificate System Role），你可以使用 Red Hat Ansible Engine 来颁发和管理证书。

本章涵盖了以下主题：

- 证书系统角色
- 使用证书系统角色请求新的自签名证书
- 使用证书系统角色从 IdM CA 请求新的自签名证书

## 11.1. 证书系统角色

使用证书系统角色，你可以使用 Red Hat Ansible Engine 管理 TLS 和 SSL 证书的颁发和续签。

该角色使用 `certmonger` 作为证书提供程序，目前支持颁发和续签自签名证书，以及使用 IdM 集成证书颁发机构（CA）。

你可以在使用证书系统角色的 Ansible playbook 中中使用以下变量：

```
certificate_wait
指定任务是否应该等待证书颁发。
certificate_requests
表示要颁发的每份证书及其参数。
```

额外资源

- 有关 `certificate_requests` 变量中使用的参数详情以及关于证书系统角色的更多信息，请参见 `/usr/share/ansible/roles/rhel-system-roles/certificate/README.md` 文件。
- 有关 RHEL 系统角色以及如何应用它们的详情，请参阅[开始使用 RHEL 系统角色](https://docs.redhat.com/en/system-roles)。

## 11.2. 使用证书系统角色请求新的自签名证书

使用证书系统角色，你可以使用 Red Hat Ansible Engine 颁发自签名证书。

此过程使用 `certmonger` 提供程序，并通过 `getcert` 命令请求证书。

> 注意
>
> 默认情况下，`certmonger` 会在证书过期前自动尝试续签。你可以通过在 Ansible playbook 中将 `auto_renew` 参数设置为 `no` 来禁用此功能。

### 在 RHEL 中使用系统角色进行 Red Hat Enterprise Linux 8 管理和配置任务

#### 前提条件

- 你已经在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意
>
> 你不需要在想要部署证书解决方案的系统中安装 Ansible。

- 你已经在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。有关 RHEL 系统角色以及如何应用它们的详情，请参阅[开始使用 RHEL 系统角色](https://docs.redhat.com/en/system-roles)。

#### 步骤

1. 可选：创建一个清单文件，例如 `inventory.file`：

```
$ touch inventory.file
```

2. 打开你的清单文件并定义你想要请求证书的主机，例如：

```
[webserver]
server.idm.example.com
```

- 设置 `hosts` 包含你想要请求证书的主机，例如 `webserver`。
- 设置 `certificate_requests` 参数包含以下内容：
- 设置 `name` 参数为证书所需的名称，例如 `mycert`。
- 设置 `dns` 参数为要包含证书中的域名，例如 `*.example.com`。
- 设置 `ca` 参数为 `self-sign`。
- 在 `roles` 下设置 `rhel-system-roles.certificate` 角色。这是本示例的 playbook 文件：

```
---
- hosts: webserver
vars:
  certificate_requests:
  - name: mycert
    dns: *.example.com
    ca: self-sign
roles:
  - rhel-system-roles.certificate
```

3. 保存文件。

4. 运行 playbook。

```
$ ansible-playbook -i inventory.file request-certificate.yml
```

额外资源

- 有关 `certificate_requests` 变量中使用的参数详情以及关于证书系统角色的更多信息，请参见 `/usr/share/ansible/roles/rhel-system-roles.README.md` 文件。
- 有关 `ansible-playbook` 命令的详情，请参阅 `ansible-playbook(1)` 手册。

## 11.3. 使用证书系统角色从 IdM CA 请求证书

使用证书系统角色，你可以使用 Red Hat Ansible Engine 通过集成证书颁发机构（CA）颁发证书，从而高效地管理多个系统的证书链。

此过程使用 `certmonger` 提供程序，并通过 `getcert` 命令请求证书。

> 注意
>
> 默认情况下，`certmonger` 会在证书过期前自动尝试续签。你可以通过在 Ansible playbook 中将 `auto_renew` 参数设置为 `no` 来禁用此功能。

#### 前提条件

- 你已经在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意
>
> 你不需要在想要部署证书解决方案的系统中安装 Ansible。

- 你已经在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。

有关 RHEL 系统角色以及如何应用它们的详情，请参阅开始使用 RHEL 系统角色。

#### 步骤

1. 可选：创建一个清单文件，例如 `inventory.file`：

```
$ touch inventory.file
```

2. 打开你的清单文件并定义你想要请求证书的主机，例如：

```
[webserver]
server.idm.example.com
```

3. 创建一个 playbook 文件，例如 `request-certificate.yml`：

- 设置 `hosts` 包含你想要请求证书的主机，例如 `webserver`。
- 设置 `certificate_requests` 变量包含以下内容：
  - 设置 `name` 参数为证书所需的名称，例如 `mycert`。
  - 设置 `dns` 参数为要包含证书中的域名，例如 `*.example.com`。
  - 设置 `principal` 参数为 Kerberos 主体，例如 `HTTP@example.com`。
  - 设置 `ca` 参数为 `ip`。
- 在 `roles` 下设置 `rhel-system-roles.certificate` 角色。

这是本示例的 playbook 文件：

```
---
- hosts: webserver
vars:
  certificate_requests:
    - name: mycert
      dns: *.example.com
      principal: HTTP@example.com
      ca: ip
roles:
  - rhel-system-roles.certificate
```

4. 保存文件。

5. 运行 playbook。

```
$ ansible-playbook -i inventory.file request-certificate.yml
```

## 11.4. 使用证书系统角色在证书颁发前或之后指定运行命令

使用证书系统角色，你可以使用 Red Hat Ansible Engine 在证书颁发或续签前后执行命令。

在以下示例中，管理员确保在颁发或续签 `www.example.com` 的自签名证书之前停止 `http` 服务，之后重启它。

> 注意
>
> 默认情况下，`certmonger` 会在证书过期前自动尝试续签。你可以通过在 Ansible playbook 中将 `autoauto_renew` 参数设置为 `no` 来禁用此功能。

- 将 `run_before` 参数设置为您希望在该证书颁发或更新之前执行的命令，例如 `systemctl stop httpd.service`。
- 将 `run_after` 参数设置为您希望在该证书颁发或更新之后执行的命令，例如 `systemctl start httpd.service`。
- 在 `roles` 下设置 `run-system-roles.certificate` 角色。

这是该示例的 playbook 文件：



```yaml
---
hosts: webserver
vars:
  certificate_requests:
    name: mycert
    dns: www.example.com
    ca: self-sign
  run_before: systemctl stop httpd.service
  run_after: systemctl start httpd.service
roles:
  - linux-system-roles.certificate
```

- 4. 保存文件。

- 5. 运行 playbook：

`$ ansible-playbook -i inventory.file request-certificate.yml`

附加资源

- 有关 `certificate_requests` 变量中使用的参数以及关于证书系统角色（Certificate System Role）的更多信息，请参阅 `/usr/share/ansible/roles/rhel-system-roles.certificate/README.md` 文件。

- 有关 `ansible-playbook` 命令的详情，请参阅 `ansible-playbook(1)` 手页。

# 第 12 章 使用 RHEL 系统角色配置 KDUMP

要使用 Ansible 管理 dump，您可以使用 `kdump` 角色，它是 RHEL 8 中可用的 RHEL 系统角色之一。

使用 `kdump` 允许您指定保存系统内存内容的位置，以便稍后分析。

关于 RHEL 系统角色以及如何应用它们的更多信息，请参阅《RHEL 系统角色简介》。

## 12.1. KDUMP RHEL 系统角色

`kdump` 系统角色允许您在多个系统上设置基本的内核 dump 参数。

## 12.2. KDUMP 角色参数

| 角色变量 | 说明 |
| :--- | :--- |
| `kdump_path` | 写入 vmcore 的路径。如果 `kdump_target` 不为空，则路径相对于该 dump 目标。否则，它必须是根文件系统中的绝对路径。 |

附加资源

- `makedumpfile(8)` 手页。

- 有关 `kdump` 中使用的参数以及关于 `kdump` 系统角色的更多信息，请参阅 `/usr/share/ansible/roles/rhel-system-roles.log/README.md` 文件。

## 12.3. 使用 RHEL 系统角色配置 KDUMP

您可以通过运行 Ansible playbook，使用 `kdump` 系统角色在多个系统上设置基本的内核 dump 参数。

> 警告

`kdump` 角色将通过替换 `/etc/kdump.conf` 文件来完全替换托管主机的 `kdump` 配置。此外，如果应用了 `kdump` 角色，所有之前的 `kdump` 设置也会被替换（即使它们没有通过角色变量指定），这将替换 `/etc/sysconfig/kdump` 文件。

## 使用系统角色进行 Red Hat Enterprise Linux 8 管理和配置任务

### 前提条件

- 您在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意

您不需要在想要部署 `kdump` 解决方案的系统上安装 Red Hat Ansible Automation Platform。

- 您在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。

- 您有一个清单文件，其中列出了您想要在其部署 `kdump` 的系统。

### 步骤

- 1. 创建一个包含以下内容的 `playbook.yml` 文件：

```yaml
---
- hosts: kdump-test
vars:
  kdump_path: /var/crash
roles:
  - rhel-system-roles.kdump
```

- 2. 可选：验证 playbook 语法。

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在您的清单文件上运行 playbook：

```bash
#### ansible-playbook -i inventory_file/path/to/file/playbook.yml
```

### 附加资源

- 关于 `kdump` 角色变量的详细参考，请参阅 `/usr/share/doc/rhel-system-roles/kdump` 目录下的 `README.md` 或 `README.html` 文件。

- 参见第 1.3 节，“应用角色”。

- 随 `rhel-system-roles` 软件包安装的文档：`/usr/share/ansible/roles/rhel-system-roles.kdump/README.html`

# 第 13 章 使用 RHEL 系统角色管理本地存储

要使用 Ansible 管理 LVM 和文件系统（FS），您可以使用 `storage` 角色，它是 RHEL 8 中可用的 RHEL 系统角色之一。

使用 `storage` 角色允许您自动对从 RHEL 7.7 开始的所有版本 RHEL 的多台机器上的磁盘文件系统和逻辑卷进行行政管理。

关于 RHEL 系统角色以及如何应用它们的更多信息，请参阅《RHEL 系统角色简介》。

## 13.1. STORAGE 角色简介

`storage` 角色可以管理：

- 未分区的磁盘文件系统

- 完整的 LVM 卷组，包括逻辑卷和文件系统

通过 `storage` 角色，您可以执行以下任务：

- 创建文件系统

- 删除文件系统

- 挂载文件系统

- 卸载文件系统

- 创建 LVM 卷组

- 删除 LVM 卷组

- 创建逻辑卷

- 删除逻辑卷

- 创建 RAID

- 删除 RAID

- 创建 LVM 池

- 删除 LVM 池

## 13.2. 标识存储设备的参数

`storage` 角色通过 `disks:` 属性识别卷。

`storage_volumes`

要管理的文件系统列表。目前支持的池是 LVM。

## 13.3. 在块设备上创建 XFS 的示例 playbook

本节提供了一个 playbook 示例。该 playbook 应用 `storage` 角色在块设备上创建 XFS。

> 警告

`storage` 角色只能在未分区的磁盘或逻辑卷上创建文件系统。

示例 13.1 在 `/dev/sdb` 上创建 XFS 的 playbook

```yaml
---
- hosts: all
vars:
  storage_volumes:
    - name: barefs
      type: disk
      disks:
        - sdb
      fs_type: xfs
roles:
  - rhel-system-roles.storage
```

- 示例卷名 `barefs` 是任意的。

- 您可以省略 `fs_type: xfs` 行，因为 XFS 是 RHEL 的默认文件系统。

- 如果要在 LV 上创建文件系统，请为 `disks:` 属性提供 LVM 设置。详情请参见管理逻辑卷的示例。

附加资源

- `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.4. 持久挂载文件系统的示例 playbook

本节提供了一个 Ansible playbook 示例。该 playbook 应用 `storage` 角色立即并持久地挂载 XFS 文件系统。

示例 13.2 将 `/dev/sdb` 挂载到 `/mnt/data` 的 playbook

```yaml
---
- hosts: all
vars:
  storage_volumes:
    name: barefs
    type: disk
    disks:
      - sdb
    fs_type: xfs
  mount_point: /mnt/data
roles:
  - rhel-system-roles.storage
```

- 该 playbook 将文件添加到 `/etc/fstab` 并立即挂载文件系统。

- 如果 `/dev/sdb` 设备或挂载点目录不存在，playbook 将创建它们。

附加资源

- `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.5. 管理逻辑卷的示例 playbook

本节提供了一个 Ansible playbook 示例。该 playbook 应用 `storage` 角色在卷组中创建 LVM 逻辑卷。

示例 13.3 在 `myvg` 卷组中创建 `mylv` 逻辑卷的 playbook



```yaml
---
- hosts: all
vars:
  storage_pools:
    name: myvg
    disks:
      - sda
      - sdb
      - sdc
volumes:
  name: mylv
  size: 2G
  fs_type: ext4
```

mount_point: /mnt

roles:

- rhel-system-roles.storage

- * myvg 卷组包含以下磁盘：

  * /dev/sda

  * /dev/sdb

  * /dev/sdc

- * 如果 myvg 卷组已存在，playbook 将将逻辑卷添加到卷组中。

* 如果 myvg 卷组不存在，playbook 将创建它。

* Playbook 会在 mylv 逻辑卷上创建一个 Ext4 文件系统，并将该文件系统持久地挂载到 /mnt。

额外资源

- * `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.6. 启用在线块丢弃（ONLINE BLOCK DISCARD）的示例 Ansible Playbook

本节提供了一个 Ansible playbook。该 playbook 应用了存储角色来挂载启用了在线块丢弃（online block discard）的 XFS 文件系统。

示例 13.4. 在 /mnt/data/ 上启用在线块丢弃的 playbook。

```yaml
---
- hosts: all
  vars:
    storage_volumes:
    - name: barefs
      type: disk
      disks:
      - sdb
      fs_type: xfs
      mount_point: /mnt/data
      mount_options: discard
roles:
  - rhel-system-roles.storage
```

额外资源

- * 持久挂载文件系统的示例 Ansible playbook 

- * `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.7. 创建并挂载 EXT4 文件系统的示例 Ansible Playbook

本节提供了一个示例 Ansible playbook。该 playbook 应用了存储角色来创建并挂载一个 Ext4 文件系统。

示例 13.5. 在 /dev/sdb 上创建 Ext4 并将其挂载到 /mnt/data 的 playbook。

```yaml
---
hosts: all
vars:
  storage_volumes:
    - name: barefs
      type: disk
  disks:
    - sdb
  fs_type: ext4
  fs_label: label-name
  mount_point: /mnt/data
roles:
  - rhel-system-roles.storage
```

- * Playbook 在 `/dev/sdb` 磁盘上创建文件系统。

- * Playbook 将文件系统持久地挂载到 `/mnt/data` 目录。

- * 文件系统的标签为 `label-name`。

额外资源

- * `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.8. 创建并挂载 EXT3 文件系统的示例 Ansible Playbook

本节提供了一个示例 Ansible playbook。该 playbook 应用了存储角色来创建并挂载一个 Ext3 文件系统。

示例 13.6. 在 /dev/sdb 上创建 Ext3 并将其挂载到 /mnt/data 的 playbook。

```yaml
---
hosts: all
vars:
  storage_volumes:
    - name: barefs
      type: disk
  disks:
    - sdb
  fs_type: ext3
  fs_label: label-name
```

# 在 RHEL 中使用 System Roles 进行 Red Hat Enterprise Linux 8 管理和配置任务

```yaml
mount_point: /mnt/data
roles:
  rhel-system-roles.storage
```

- * Playbook 在 `/dev/sdb` 磁盘上创建文件系统。

- * Playbook 将文件系统持久地挂载到 `/mnt/data` 目录。

- * 文件系统的标签为 `label-name`。

额外资源

- * `/usr/share/ansible/roles/rhel-system-roles.storage.README.md`。

## 13.9. 使用 RHEL SYSTEM ROLE 调整现有 EXT4 或 EXT3 文件系统大小的示例 playbook

本节提供了一个 Ansible playbook。该 playbook 应用了存储角色来调整块设备上现有的 Ext4 或 Ext3 文件系统的大小。

示例 13.7. 在磁盘上设置挂载到 /opt/barefs 的单卷 playbook。

```yaml
---
- name: Create a disk device mounted on /opt/barefs
- hosts: all
  vars:
    storage_volumes:
    - name: barefs
      type: disk
      disks:
        - /dev/sdb
      size: 12GiB
      fs_type: ext4
      mount_point: /opt/barefs
  roles:
  - rhel-system-roles.storage
```

- * 如果上一个示例中的卷已经存在，要调整卷的大小，你需要调整同一个 playbook，只需为参数 `size` 提供一个不同的值。例如：

示例 13.8. 调整 /dev/sdb 上 ext4 大小的 playbook。

```yaml
---
- name: Create a disk device mounted on /opt/barefs
- hosts: all
  vars:
    storage_volumes:
    - name: barefs
      type: disk
      disks:
        - /dev/sdb
```

## 第 13 章.管理本地存储的 RHEL SYSTEM ROLES

```yaml
size: 10 GiB
fs_type: ext4
mount_point: /opt/barefs
roles:
- rhel-system-roles.storage
```

卷名称（示例中的 barefs）目前是任意的。存储角色通过 `disks` 下列出的磁盘设备来识别该卷：

![image](707619df8761a56503825)

> NOTE

卷名称（示例中的 barefs）目前是任意的。存储角色通过 `disks` 下列出的磁盘设备来识别该卷。

额外资源

- * `/usr/share/ansible/roles/rhel-system-roles.storage.md`。

## 13.10. 使用 STORAGE SYSTEM ROLE 调整现有 EXT4 或 EXT3 文件系统大小的示例 playbook

本节提供了一个 Ansible playbook。该 playbook 应用了存储角色来调整块设备上现有的 Ext4 或 Ext3 文件系统的大小。

> WARNING

卷名称（示例中的 barefs）目前是任意的。存储角色通过 `disks` 下列出的磁盘设备来识别该卷。

示例 13.9. 在 /dev/sdb 上创建 Ext4 并将其挂载到 /mnt/data 的 playbook。

# 使用 System Roles 进行 Red Hat Enterprise Linux 8 管理和配置任务

```yaml
---
- hosts: all
  vars:
    storage_volumes:
    - name: barefs
      type: disk
      disks:
        - sdb
fs_type:
mount:
/mnt/data
roles:
  - rhel-system-roles.storage
```

- * Playbook 在 `/dev/sdb` 磁盘上创建文件系统。

- * Playbook 将文件系统持久地挂载到 `/mnt/data` 目录。

- * 文件系统的标签为 `label-name`。

额外资源



- `/usr/share/ansible/roles/rhel-system-roles.storage.md`。

## 13.11. 使用 STORAGE RHEL SYSTEM ROLE 创建 SWAP 分区的示例 playbook

本节提供了一个 Ansible playbook。该 playbook 应用了存储角色，在块设备上创建交换分区（如果已存在则修改交换分区），使用默认参数。

示例 13.10. 在 `/dev/sdb` 上创建 XFS 的 playbook。

```yaml
---
- name: Create a disk device with swap
- hosts: all
  vars:
    storage_volumes:
    - name: barefs
      type: disk
      disks:
        - /dev/sdb
      size: 15GiB
      fs_type: swap
      mount_point: /opt/barefs
  roles:
  - rhel-system-roles.storage
```

> NOTE

卷名称（示例中的 `barefs`）目前是任意的。存储角色通过 `disks` 下列出的磁盘设备来识别该卷。

额外资源

- `/usr/share/ansible/roles/rhel-system-roles.storage.md`。

## 13.12. 使用 STORAGE ROLE 配置 RAID 卷

使用存储 System Role，可以使用 Red Hat Ansible Platform 在 RHEL 上配置 RAID 卷。在本节中你将学习如何使用可用参数设置 Ansible playbook 以配置满足需求的 RAID 卷。

前提条件

- 在运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> NOTE

你不需要在部署存储解决方案的系统上安装 Red Hat Automation Platform。

- 在运行 playbook 的系统上安装了 `rhel-system-roles` 包。

- 你有一个详细说明要使用存储 System Role 部署 RAID 卷的系统清单文件。

步骤

- 1. 创建包含以下内容的 `playbook.yml` 文件：

```yaml
---
- hosts: all
vars:
  storage_safe_mode: false
  storage_volumes:
    - name: data
      type: raid
      disks: [ssd, sde, sdf, sdg]
      raid_level: raid
      raid_chunk_size: 32 KiB
      mount_point: /mnt/data
  state: present
roles:
  - name: rhel-system-roles.storage
```

> WARNING

设备名称在某些情况下可能会发生变化，例如向系统添加新磁盘时。因此，为了防止数据丢失，我们不建议在 playbook 中使用特定的磁盘名称。

- 2. 可选。验证 playbook 语法。

```bash
#### ansible-playbook --syntax-check playbook.yml
```

3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file /path/to/file/playbook.yml
```

其他资源

- 管理 RAID。

- `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件。

## 13.13. 使用存储系统角色配置带 RAID 的 LVM 池

使用存储系统角色（storage System Role），你可以通过 Red Hat Ansible Automation Platform 在 RHEL 上配置带有 RAID 的 LVM 池。在本节中，你将学习如何使用可用参数设置 Ansible playbook，以配置带有 RAID 的 LVM 池。

### 前提条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意：

> 你不需要在想要部署存储解决方案的系统上安装 Red Hat Ansible Automation Platform。

- 你在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。

- 你有一个清单文件，详细列出了你想要使用存储系统角色配置带 RAID 的 LVM 池的系统。

### 步骤

- 1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
- hosts: all
vars:
  storage_safe_mode: false
  storage_pools:
  - name: my_pool
    type: lvm
    disks: [sdh, sdi]
    raid_level: raid1
  volumes:
  - name: my_pool
    size: "1 GIB"
    mount_point: "/mnt/app/shared"
    fs_type: xfs
    state: present
  - name: rhel-system-roles.storage
```

> 注意：

> 要创建带 RAID 的 LVM 池，必须使用 `raid_level` 参数指定 RAID 类型。

- 2. 可选。验证 playbook 语法。

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file /path/to/file/playbook.yml
```

其他资源

- 管理 RAID。

- `/usr/share/ansible/roles/rhel-system-roles.storage/README.md` 文件

## 13.14. 使用存储角色创建 LUKS 加密卷

你可以通过运行 Ansible playbook 来创建并配置使用 LUKS 加密的卷。

### 前提条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。

> 注意：

> 你不需要在要在想要创建卷的系统上安装 Red Hat Ansible Automation Platform。

- 你在 Ansible 控制器上安装了 `rhel-system-roles` 软件包。

- 你有一个清单文件，详细列出了你想要使用系统存储角色部署 LUKS 加密卷的系统。

### 步骤

- 1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
hosts: all
vars:
  storage_volumes:
  - name: barefs
    type: disk
    disks:
    - sdb
    fs_type: xfs
    fs_label: label_name
    mount_point: /mnt/data
    encryption: true
    encryption_password: your-password
    roles:
  - rhel-system-roles.storage
```

- 2. 可选：验证 playbook 语法：

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file/path/to/file/playbook.yml
```

其他资源

- 使用 LUKS 加密块设备

- `/usr/share/ansible/roles/rhel-system-roles/storage/README.md` 文件

## 13.15. 更多资源

- `/usr/share/doc/rhel-system-roles/storage/`

- `/usr/share/ansible/roles/rhel-system-roles.storage/`

## 第 14 章 使用 RHEL 系统角色配置时间同步

使用 `timesync` RHEL 系统角色，你可以通过 Red Hat Ansible Automation Platform 在多个目标机器上管理时间同步。

## 14.1. TIMESYNC 系统角色



你可以使用 `timesync` RHEL 系统角色在多个目标机器上管理时间同步。

`timesync` 角色会安装并配置 NTP 或 PTP 实现，作为 NTP 客户端或 PTP 副本运行，以便系统时与 NTP 服务器或 PTP 域中的主时（grandmasters）同步。

注意，使用 `timesync` 角色还便于迁移到 `chronology`，因为你可以在从 RHEL 6 开始的所有 Red Hat Enterprise Linux 版本上使用相同的 playbook，无论系统是使用 `ntp` 还是 `chronology` 来实现 NTP 协议。

## 14.2. 为单个服务器池应用 TIMESYNC 系统角色

以下示例展示了如何在仅有一个服务器池的情况下应用 `timesync` 角色。

> 警告：
>
> `timesync` 角色将替换被管理主机上给定的或检测到的提供服务的配置。之前的设置将丢失，即使它们没有在角色变量中指定。只有在未定义 `timesync_ntp_provider` 变量的情况下，才会保留对提供者的选择。

### 前提条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。
- 你在想要部署存储解决方案的系统上安装了 Red Hat Ansible Automation Platform。
- 你在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。
- 你有一个清单文件，详细列出了你想要配置 `timesync` 的系统。

### 步骤

- 1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
- hosts: timesync
vars:
  timesync_ntp_servers:
    - hostname: pool.ntp.org
      pool: yes
      iburst: yes
roles:
  - rhel-system-roles.timesync
```

- 2. 验证 playbook 语法：

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file/path/to/file/playbook.yml
```

## 14.3. TIMESYNC 系统变量

你可以向 `timesync` 角色传递变量 `timesync_ntp_servers`:

| 角色设置 | 描述 |
|--- |--- |
| hostname | 服务器的主名或地址 |
| minpoll | 最小轮询间隔。默认：6 |
| maxpoll | 最大轮询间隔。默认：10 |
| iburst | 快速同步标志。默认：no |
| pool | 表示该地址为独立服务器的标志。默认：no |

其他资源

- 如需 `timesync` 变量的详细参考，请安装 `rhel-system-roles` 软件包，并查看 `/usr/share/doc/rhel-system-roles/timesync` 目录下的 `README.md` 或 `README.html` 文件。

## 第 15 章 使用 RHEL 系统角色监控性能

作为系统管理员，你可以使用 `metrics` RHEL 系统角色来监控系统性能。

## 15.1. METRICS 系统角色简介

RHEL System Roles 是 Ansible 角色和模块的集合，提供了远程管理多个系统的统一接口。`metrics` 系统角色为本地系统配置性能分析服务，并可选包含本地系统监控的远程系统列表。`metrics` 角色允许你使用 `pcp` 监控性能，而无需单独配置 `pcp`，因为 `pcp` 的设置和部署由 playbook 处理。

表 15. Metrics 角色变量

| 角色变量 | 描述 | 使用示例 |
|---|---|---|
| metrics_monitored_hosts | 由目标主机分析的远程主机列表。这些主机将在目标主机上记录指标，请确保每个主机 `/var/log` 下有足够的磁盘空间。 | `_monitored_hosts: ["webserver.example.com","database.example.com"]` |
| metrics_retention_days | 配置性能数据删除前的保留天数。 | `metrics_retention_days: 14` |
| metrics_graph_service | 开启通过 `pcp` 和 `grafana` 进行性能数据可视化的布尔标志。默认为 false。 | `metrics_graph_service: false` |
| metrics_query_service | 开启通过 `redis` 记录指标的时间序列查询服务的布尔标志。默认为 false。 | `metrics_query_service: false` |
| metrics_provider | 指定使用的指标采集器。目前 `pcp` 是唯一支持的指标提供者。 | `metrics_provider: "pcp"` |

> 注意：
>
> 有关 `metrics_connections` 中使用的参数以及关于 `metrics` 系统角色的更多信息，请参 `/usr/share/ansible/roles/rhel-system-roles.metrics/README.md` 文件。

## 15.2. 使用指标系统角色通过可视化监控您的本地系统

本过程描述了如何使用指标系统角色（metrics System Role）监控您的本地系统，同时通过 `grafana` 提供数据可视化。

前提条件

- 您在想要监控的机器上安装了 Red Hat Ansible Engine。
- 您在想要监控的机器上安装了 `rhel-system-roles` 软件包。

步骤

- 1. 通过在 `/etc/ansible/hosts` Ansible 清单中添加以下内容来配置 localhost：

```yaml
localhost ansible_connection=local
```

- 2. 创建包含以下内容的 Ansible 剧本（playbook）：

```yaml
---
- hosts: localhost
vars:
  metrics_graph_service: yes
roles:
  - rhel-system-roles.metrics
```

- 3. 运行 Ansible 剧本：

```bash
# ansible-playbook name_of_your_playbook.yml
```

> 注意
>
> 由于 `metrics_graph_service` 布值设置为 "yes"，`grafana` 会自动安装并配置 `pcp` 作为数据源进行配置。

![](img/7076193df8761a1565038e17afc88b0b_93_0.png)

- 4. 要查看机器上收集的指标的可视化结果，请按照“访问 Grafana web UI”所述的方法访问 `grafana` 界面。

## 15.3. 使用指标系统角色设置一组独立系统进行监控

本过程描述了如何使用指标系统角色设置一组机器以便其进行监控。

前提条件

- 您在用于运行剧本的机器上安装了 Red Hat Ansible Engine。
- 您在用于运行剧本的机器上安装了 `rhel-system-roles` 软件包。

步骤

- 1. 通过剧本将您想要监控的机器的名称或 IP 添加到 `/etc/ansible/hosts` Ansible 清单文件中，并置于方括号括的标识组名下：

```ini
[remotes]
webserver.example.com
database.example.com
```

- 2. 创建包含以下内容的 Ansible 剧本：

```yaml
-
hosts: remotes
vars:
  metrics_retention_days: 0
roles:
  - rhel-system-roles.metrics
```

- 3. 运行 Ansible 剧本：

```bash
# ansible-playbook name_of_your_playbook.yml
```

## 15.4. 通过本地机器使用指标系统角色集中监控机器机器

本过程描述了如何使用指标系统角色设置您的本地机器，以集中监控一组机器，同时通过 `grafana` 提供数据可视化并通过 `redis` 进行数据查询。

前提条件

- 您在用于运行剧本的机器上安装了 Red Hat Ansible Engine。
- 您在用于运行剧本的机器上安装了 `rhel-system-roles` 软件包。

步骤

- 1. 创建包含以下内容的 Ansible 剧本：



```yaml
-
hosts: localhost
vars:
  metrics_graph_service: yes
  metrics_query_service: yes
  metrics_retention_days: 10
  metrics_monitored_hosts: ["database.example.com", "webserver.example.com"]
roles:
  - rhel-system-roles.metrics
```

### 2. 运行 Ansible 剧本

```bash
# ansible-playbook name_of_your_playbook.yml
```

> 注意
>
> 由于 `metrics_graph_service` 和 `metrics_query_service` 布值设置为 `"yes"`，`grafana` 会自动安装并配置 `pcp` 作为数据源，且 `pcp` 数据在 `redis` 中索引，允许使用 `pcp` 查询语言对数据进行复杂查询。

- 3. 要查看由您的机器集中收集的指标的可视化表示，请按照“访问 Grafana web UI”所述的方法访问该界面。

## 15.5. 在监控系统时使用指标系统角色设置身份验证

`PCP` 通过简单身份安全层 (`SASL`) 支持 `scram-sha-256` 身份验证机制。指标 `RHEL` 系统角色执行使用 `scram-sha-256` 身份验证机制的设置步骤。本过程描述了如何使用该角色设置身份验证。

### 前提条件

- 您在用于运行剧本的机器上安装了 Red Hat Ansible Engine。
- 您在用于运行剧本的机器上安装了 `rhel-system-roles` 软件包。

### 步骤

- 1. 在您要设置身份验证的 Ansible 剧本中包含以下变量：

```yaml
vars:
  metrics_username: your_username
  metrics_password: your_password
```

- 2. 运行 Ansible 剧本：

```bash
# ansible-playbook name_of_your_playbook.yml
```

### 验证步骤

- 验证 `sasl` 配置：

```bash
# pminfo -f -h "pcp://127.0.0.1?username=your_username" disk.dev/read
Password: 
```

## 15.6. 使用指标系统角色配置并启用指标

本过程描述了如何使用指标系统角色为您的本地系统配置并启用指标。

（注：原文中 15.6 的 OCR 文本不完整，已包含可用内容。）

### 前提条件

- 您已设置了 SSH 密钥，以便从控制节点访问目标系统，该系统将用于配置 tlog 系统角色（System Role）。
- 您有一个控制节点，该系统是 Ansible Engine 配置其他系统的来源。
- 您在控制节点上安装了 Red Hat Ansible Engine，并希望从该节点运行 playbook。
- 您在想要运行 playbook 的控制节点上安装了 `rhel-system-roles` 软件包。
- 您至少有一个想要配置 tlog 系统角色的系统。您不需要在部署 tlog 解决方案的系统上安装 Red Hat Automation Platform。

### 步骤

1. 创建一个新的新的 `playbook.yml` 文件，内容如下：

```yaml
- name: Deployment session recording
  hosts: all
  vars:
    tlog_scope_sssd: some
    tlog_users_sssd:
      - recordeduser
  roles:
    - rhel-system-roles.tlog
```

其中，

- `tlog_scope_sssd`:
  - `some`：指定您只想记录某些用户和组，而不是全部或一个都不记录。
- `tlog_users_sssd`:
  - `recordeduser`：指定您想要记录其会话的用户。注意，这不会为您添加该用户。您必须手动设置该用户。

2. 可选：验证 playbook 的语法。

```bash
#### ansible-playbook --syntax-check playbook.yml
```

3. 在您的清单文件（inventory file）上运行 playbook：

```bash
# ansible-playbook -i IP_Address /path/to/file/playbook.yml -v
```

结果是， playbook 安装了 `tlog` 角色，该角色供您定义的用户和组使用。`SSSD` 解析并读取这些用户和组，以便以 shell 用户身份叠加 `tlog` 会话。此外，如果系统上安装了 `cockpit` 软件包，playbook 还会安装 `cockpit-session-recording` 软件包，这是一个 Cockpit 模块，允许您在 Web 控制台界面查看和播放录制。

#### 验证步骤

要验证系统中是否创建了 SSSD 配置落地文件（drop file），请执行以下步骤：

1. 导航到创建 SSSD 配置落地文件的文件夹：

```bash
# cd /etc/sssd/conf.d
```

2. 检查文件内容：

```bash
# cat /etc/sssd/conf.d/sssd-session-recording.conf
```

您可以看到该文件包含了您在 playbook 中设置的参数。

## 16.4. 部署 TLOG REG 系统角色以排除组或用户列表

您可以在 RHEL 上使用 `tlog` 系统角色，来支持 SSSD 会话记录配置中的 `exclude_users` 和 `exclude_groups`。按照以下步骤准备并应用 Ansible playbook，以配置 RHEL 系统，排除某些用户或组的会话在 systemd journal 中的记录和日志记录。

### 前提条件

- 您已设置了 SSH 密钥，以便从控制节点访问想要配置 tlog 系统角色的目标系统。
- 您有一个控制节点，该系统是 Red Hat Ansible Engine 配置其他系统的来源。
- 您在控制节点上安装了 Red Hat Ansible Engine，并希望从该节点运行 playbook。
- 您在控制节点上安装了 `rhel-system-roles` 软件包。
- 您至少有一个想要配置 tlog 系统角色的系统。您不需要在部署 tlog 解决方案的系统上安装 Red Hat Automation Platform。

### 步骤

1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
- name: Deploy session recording excluding users and groups
  hosts: all
  vars:
    tlog_scope_sssd: all
    tlog_exclude_users_sssd:
      - jeff
      - james
    tlog_exclude_groups_sssd:
      - admins
  roles:
    - rhel-system-roles.tlog
```

其中，

- `tlog_scope_sssd`:
  - `all`：指定您想记录所有用户和组。
- `tlog_exclude_users_sssd`:
  - `usernames`：指定您想要从会话记录中排除的用户名。
- `tlog_exclude_groups_sssd`:
  - `admins`：指定您想要从会话记录中排除的组。

2. 可选：验证 playbook 的语法；

```bash
#### ansible-playbook --syntax-check playbook.yml
```

3. 在您的清单文件上运行 playbook：

```bash
# ansible-playbook -i IP_Address /path/to/file/playbook.yml -v
```

结果是， playbook 在您指定的系统上安装了 `tlog` 软件包。它还会创建 `/etc/sssd/conf.d/sssd-session-recording.conf` SSSD 配置落地文件，该文件可供除定义为排除之外的用户和组使用。`SSSD` 解析并读取这些用户和组，以 shell 用户身份叠加 `tlog`。此外，如果系统上安装了 `cockpit` 软件包，playbook 还会安装 `cockpit-session-recording` 软件包，这是一个 Cockpit 模块，允许您在 Web 控制台界面查看和播放录制。

![](img/7076193df8761a1565038e17afc88b0b_101_0.png)

> 注意



您无法对列在 `exclude_users` 列表的用户或属于 `exclude_groups` 列表中组的用户记录会话。

### 验证步骤

要验证系统中是否创建了 SSSD 配置落地文件，请执行以下步骤：

1. 导航到创建 SSSD 配置落地文件的文件夹：

```bash
# cd /etc/sssd/conf.d
```

2. 检查文件内容：

```bash
# cat sssd-session-recording.conf
```

## 第 16 章. 使用 TLOG RHEL 系统规则配置会话记录的系统

您可以看到该文件包含了您在 playbook 中设置的参数。

其他资源

- `/usr/share/doc/rhel-system-roles/tlog/` 和 `/usr/share/ansible/roles/rhel-system-roles/tlog/` 目录。
- 使用部署的 tlog 系统角色进行记录

### 16.5. 使用部署的 tlog 系统角色记录会话

一旦在系统上部署了 `tlog` 系统角色，您就可以使用命令行界面（CLI）记录会话。

前提条件

- 您已在目标系统上部署了 `tlog` 系统角色。
- SSSD 配置落地文件已创建在 `/etc/sssd/conf.d`。

步骤

1. 创建一个用户并为其分配密码：

```bash
# useradd recordeduser
# passwd recordeduser
```

2. 以创建的用户身份登录系统：

```bash
# ssh recordeduser@localhost
```

3. 当系统提示身份验证时输入 "yes"。

> 注意！您的会话正在被记录！

4. 完成会话记录后，输入：

```bash
# exit
```

结果是，用户会话已被记录并存储，您可以使用 journal 查看。

验证步骤

要在 journal 中查看您的记录会话，请执行以下步骤：

1. 运行以下命令：

```bash
# journalctl -o verbose -r
```

2. 搜索 tlog 记录日志条目的 `MESSAGE` 字段。

```bash
# journalctl -xl EXE=/usr/bin/tlog-rec-session
```

### 16.6. 使用 CLI 查看记录会话

您可以使用命令行界面（CLI）从 journal 中播放用户会话记录。

前提条件

- 您已记录了会话。

步骤

1. 在 CLI 终端上播放用户会话记录：

```bash
# journalctl -o verbose -r
```

2. 搜索 tlog 记录：

```bash
$ tlog-rec
```

您可以看到如下详细信息：

字体 会话记录的用户名

- `out_txt` 字段，录制会话的原始输出编码
- 标识符 `TLOG_REC=ID_number`

3. 复制标识符 `TLOG_REC=ID_number`。

4. 使用标识符 `TLOG_REC=ID_number` 播放录制：

```bash
# tlog-play -r journal -M TLOG_REC=ID_number
```

# 第 17 章：使用系统角色配置高可用集群

通过 `ha_cluster` 系统角色，你可以配置和管理一个使用订阅制 Pacemaker 高可用集群资源管理器的高可用集群。

![](img/7076193df8761a1565038e17afc88b0b_104_0.png)

注意

高可用集群（HA Cluster）角色目前以技术预览（Technology Preview）的形式提供。

HA 系统角色目前不支持约束条件（constraints）。在手动配置约束条件后运行该角色将移除这些约束条件以及任何不受该角色支持的配置。

## 17.1. HA_CLUSTER 系统角色变量

在 `ha_cluster` 系统角色剧本（playbook）中，你根据集群部署的需求定义高可用集群的变量。

你可以为 `ha_cluster` 系统角色设置的变量如下：

**`ha_cluster_enable_repos`**

一个布尔标志位，用于启用包含 `ha_cluster` 系统角色所需的软件包的存储库。当其设置为 `yes`（该变量的默认值）时，你必须对用作集群成员的系统拥有 RHEL 和 RHEL High Availability Add-On 的订阅支持，否则系统角色将失败。

**`ha_cluster_cluster_present`**

一个布尔标志位，如果设置为 `yes`，则将根据传递给角色的变量在主机上配置 HA。任何未在角色中指定且不受角色支持的集群配置将丢失。

如果 `ha_cluster_cluster_present` 设置为 `no`，则将从目标主机移除所有 HA 集群配置。

该变量的默认值为 `yes`。

以下示例移除了 node1 和 node2 上的所有集群配置：

```yaml
- hosts: node1 node2
vars:
  ha_cluster_cluster_present: no

roles:
  - rhel-system-roles.ha-cluster
```

**`ha_cluster_start_on_boot`**

一个布尔标志位，决定是否将集群服务配置为启动时启动。该变量的默认值为 `yes`。

**`ha_cluster_fence_agent_packages`**

要安装的隔离代理（fence agent）软件包列表。该变量的默认值为 `fence-agents-all, fence-virt`。

**`ha_cluster_extra_packages`**

要安装的所有软件包列表。该变量的默认值为 `packages`。此变量可用于安装角色未自动安装的额外软件包，例如自定义资源代理。

可以将隔离代理作为此列表的成员指定。但是，如果覆盖了此值，`ha_cluster_fence_agent_packages` 是推荐用于指定隔离代理变量。

**`ha_cluster_hacluster_password`**

一个字符串值，用于指定 `hacluster` 用户的密码。`hacluster` 用户对集群具有完全访问权限。建议按照“使用 Ansible Vault 加密内容”中的描述对密码进行 vault 加密。该变量没有默认密码值，且必须指定。

**`ha_cluster_corosync_key_src`**

Corosync 认证密钥（authkey）文件的路径，它是 Corosync 通信的身份验证和加密密钥。强烈建议为每个集群使用唯一的密钥值。密钥应为 256 字节的随机数据。

如果你为此变量指定了密钥，建议按照“使用 Ansible Vault 加密内容”中的描述对密钥进行 vault 加密。

如果没有指定密钥，将使用节点上已存在的密钥。如果节点上的密钥不同，则会将一个节点的密钥分发到其他节点，以确保所有节点拥有相同的密钥。如果节点没有任何密钥，则将生成新密钥并分发到节点。

如果设置了此变量，则忽略该密钥的 `ha_cluster_regenerate_keys`。

该变量的默认值为 `null`。

**`ha_cluster_pacemaker_key_src`**

Pacemaker 认证密钥文件的路径，强烈建议为每个集群使用唯一的密钥值。密钥应为 256 字节的随机数据。

如果你为此变量指定了密钥，建议按照“使用 Ansible Vault 加密内容”中的描述对密钥进行 vault 加密。

如果没有指定密钥，将使用节点上已存在的密钥。如果节点上的密钥不同，则会将一个节点的密钥分发到其他节点，以确保所有节点拥有相同的密钥。如果节点没有任何密钥，则将生成新密钥并分发到节点。

如果设置了此变量，则忽略该密钥的 `ha_cluster_regenerate_keys`。

该变量的默认值为 `null`。

**`ha_cluster_fence_virtvm_key_src`**

fence-virtvm 或 fence-fencing 预共享密钥文件的路径，它是 fence-virtvm 或 fence-fencing 隔离代理集群的认证密钥位置。

如果你为此变量指定了密钥，建议按照“使用 Ansible Vault 加密内容”中的描述对密钥进行 vault 加密。

如果没有指定密钥，将使用节点上已存在的密钥。如果节点上的密钥不同，则会将一个节点的密钥分发到其他节点，以确保所有节点拥有相同的密钥。如果节点没有任何密钥，将生成新密钥并分发到节点。如果 `ha_cluster` 系统角色以这种方式生成了新密钥，你需要将密钥复制到节点的虚拟化程序以确保隔离功能正常。

如果设置了此变量，则忽略该密钥的 `ha_cluster_regenerate_keys`。

**`ha_cluster_pcosync_key_src`**

fence-virtvm 或 fence-fencing 预共享密钥文件的路径，它是 fence-virtvm 或 fence-fencing 隔离代理集群的认证密钥位置。



如果你为此变量指定了密钥，建议按照“使用 Ansible Vault 加密内容”中的描述对密钥进行 vault 加密。

如果没有指定密钥，将使用节点上已存在的密钥。如果节点上的密钥不同，则会将一个节点的密钥分发到其他节点，以确保所有节点拥有相同的密钥。如果节点没有任何密钥，将生成新密钥并分发到节点。如果 `ha_cluster` 系统角色以这种方式生成了新密钥，你需要将密钥复制到节点的虚拟化程序以确保隔离功能正常。

如果设置了此变量，则忽略该密钥的 `ha_cluster_regenerate_keys`。

### `ha_cluster_regenerate_keys`

一个布尔标志位，如果设置为 `yes`，则根据传递给角色的变量在主机上配置 HA。任何未在角色中指定且不受角色支持的集群配置将丢失。

如果 `ha_cluster_cluster_present` 设置为 `no`，将从目标主机移除所有 HA 集群配置。

该变量的默认值为 `yes`。

### `ha_cluster_cluster_name`

集群名称。这是一个字符串，默认值为 `my-cluster`。

### `ha_cluster_cluster_properties`

Pacemaker 全局属性列表。仅支持一组集群属性。集群属性集的结构如下：

```yaml
ha_cluster_cluster_properties:
  attrs:
    - name: property1_name
      value: property1_value
    - name: property2_name
      value: property2_value
```

默认情况下未设置属性。以下示例配置了一个由 node1 和 node2 组成的集群，并设置了 `stonith-enabled` 和 `no-quorum-policy`。

```yaml
- hosts: node1 node2
vars:
  ha_cluster_cluster_name: my-cluster
  ha_cluster_hacluster_password: password
  ha_cluster_cluster_properties:
    attrs:
      - name: stonith-enabled
        value: 'true'
      - name: no-quorum-policy
        value: stop

roles:
  - rhel-system-roles.ha-cluster
```

### `ha_cluster_resource_primitives`

此变量定义了系统角色配置的 Pacemaker 资源，包括隔离资源。每个资源可以配置的项目如下：

- `id`（强制）：资源的 ID。
- `agent`（强制）：资源或隔离代理的名称，例如 `ocf:pacemaker:Dummy` 或 `stonith:fence_crm`。对于隔离代理必须指定 `stonith`。对于资源代理，可以使用短名称（如 `Dummy`）代替 `ocf:pacemaker:Dummy`。但是，如果安装了多个同名的代理，系统将无法决定使用哪个代理。因此，建议在指定资源代理时使用全名。
- `instance_attrs`（可选）：资源实例属性列表。目前仅支持一组。属性的准确名称、值以及是否为强制性取决于具体的资源或隔离代理。
- `meta_attrs`（可选）：资源元属性列表。目前仅支持一组。

## 第 17 章：使用系统角色配置高可用性集群

- `operations` (可选) - 资源的操作列表。
- `action` (强制性) - 由 pacemaker 资源代理或 stonith 代理定义的操作动作。
- `attrs` (强制性) - 操作选项，必须指定至少一个选项。

你通过 `ha_cluster` 系统角色配置的资源定义结构如下：

```yaml
- id: resource-id
  agent: resource-agent
  instance_attrs:
    - attrs:
        - name: attribute1_name
          value: attribute1_value
        - name: attribute2_name
          value: attribute2_value
  meta_attrs:
    - attrs:
        - name: meta_attribute1_name
          value: meta_attribute1_value
        - name: meta_attribute2_name
          value: meta_attribute2_value
  operations:
    - action: operation1-action
      attrs:
        - name: operation1_attribute1_name
          value: operation1_attribute1_value
        - name: operation1_attribute2_name
          value: operation1_attribute2_value
    - action: operation2-action
      attrs:
        - name: operation2_attribute1_name
          value: operation2_attribute1_value
        - name: operation2_attribute2_name
          value: operation2_attribute2_value
```

默认情况下，未定义资源。

如需包含资源配置的 `ha_cluster` 系统角色 playbook 示例，请参阅 [使用围隔离和资源配置高可用集群](https://example.com)

## `ha_cluster_resource_groups`

此变量定义了由系统角色配置的 pacemaker 资源组。你可以为每个资源组配置的项如下：

- `id` (强制性) - 组的 ID。
- `resources` (强制性) - 组的资源列表。每个资源通过其 ID 引用，且资源必须在 `ha_cluster_primitives` 变量中定义。必须列出一个资源。
- `meta_attrs` (可选) - 组元属性集合列表。目前仅支持一个集合。

你通过 `ha_cluster` 系统角色配置的资源组定义结构如下：

```yaml
ha_cluster_resource_groups:
  - id: group-id
    resource_ids:
      - resource1-id
      - resource2-id
    meta_attrs:
      - attrs:
          - name: group_meta_attribute1_name
            value: group_meta_attribute1_name
          - name: group_meta_attribute2_name
          value: group_meta_attribute2_name
```

默认情况下，未定义任何资源组。

如需包含资源组配置的 `ha_cluster` 系统角色 playbook 示例，请参阅使用围隔离和资源配置高可用集群。

## `ha_cluster_resource_clones`

此变量定义了由系统角色配置的 pacemaker 克隆。你可以为克隆配置的项如下：

- `resource_id` (强制性) - 要克隆的资源。该资源必须在 `ha_cluster_resource_primitives` 变量或 `ha_cluster_resource_groups` 变量中定义。
- `promotable` (可选) - 表示要创建的资源克隆是否为提升克隆，值为 yes 或 no。
- `id` (可选) - 克隆的自定义 ID。如果没有指定 ID，则将自动生成。如果集群不支持此选项，将显示警告。
- `meta_attrs` (可选) - 克隆元属性集合列表。目前仅支持一个集合。

你通过 `ha_cluster` 系统角色配置的资源克隆定义结构如下：



```yaml
ha_cluster_resource_clones:
  - resource_id: resource-to-be-cloned
    promotable: yes
    id: clone-id
    meta_attrs:
      - attrs:
          - name: meta_attribute1_name
            value: meta_attribute1_value
          - name: meta_attribute2_name
            value: meta_attribute2_value
```

默认情况下，未定义任何资源克隆。

如需包含资源克隆配置的 `ha_cluster` 系统角色 playbook 示例，请参阅使用围隔离和资源配置高可用集群。

## 17.2 为 HA_CLUSTER 指定清单

在使用 `ha_cluster` 系统角色 playbook 配置 HA 集群时，你需要在清单中配置节点的名称和地址。

对于清单中的每个节点，你可以可选地指定以下项：

- `node_name` - 集群中的节点名称。
- `pcs_address` - 用于与节点通信的地址。可以是名称、FDN 或 IP 地址，并可以包含端口号。
- `corosync_addresses` - Corosync 使用的地址列表。形成特定集群的所有节点必须具有相同数量的地址，且地址顺序很重要。

以下示例显示了 `node1` 和 `node2` 的清单。`node1` 和 `node2` 必须是完全限定域名，或者能够通过 `/etc/hosts` 文件解析到节点。

```yaml
all:
  hosts:
    node1:
      ha_cluster:
        node_name: node-A
        pcs_address: node1-address
      corosync_addresses:
        - 192.168.1.11
        - 192.168.2.11
    node2:
      ha_cluster:
        node_name: node-B
        pcs_address: node-2-address:2224
      corosync_addresses:
        - 192.168.1.12
        - 192.168.2.12
```

## 17.3 配置不运行任何资源的高可用集群

以下步骤使用 `ha_cluster` 系统角色，创建一个未配置围隔离且不运行任何资源的高可用集群。

### 前提条件

- 你在想要运行 playbook 的节点上安装了 Red Hat Ansible Engine。

> 注意
>
> 集群节点上不需要安装 Ansible。

## 17.4 配置带有围隔离和资源的高可用集群

以下步骤使用 `ha_cluster` 系统角色，创建一个配置了围隔离并运行资源的高可用集群。

`value: '30s'`

- `action: monitor`

`atrs:`

- `name: timeout`

`value: '5'`

- `name: interval`

`value: '1min'`

- `id: dummy-1`

- `agent: 'ocf:pacemaker:Dummy'`

- `id: dummy-2`

- `agent: 'ocf:pacemaker:Dummy'`

- `id: dummy-3`

- `agent: 'ocf:pacemaker:Dummy'`

- `id: simple-clone`

- `agent: 'ocf:pacemaker:Dummy'`

- `id: clone-with-options`

- `agent: 'ocf:pacemaker:Dummy'`

`ha_cluster_resource_groups:`

- `id: simple-group`

`resource_ids:`

- `dummy-1`

- `dummy-2`

`meta_attrs:`

`at attrs:`

- `name: target-role`

`value: Started`

- `name: is-managed`

`value: 'true'`

- `id: cloned-group`

`resource_ids:`

- `dummy-3`

`ha_cluster_resource_clones:`

- `resource_id: simple-clone`

- `resource_id: clone-with-options`

`promotable: yes`

`id: custom-cluster-id`

`meta_attrs:`

`at attrs:`

- `name: clone-max`

`value: '2'`

- `name: clone-node-max`

`value: '1'`

- `resource_id: cloned-group`

`promotable: yes`

`roles:`

- `rhel-system-roles.ha_cluster`

+ 3. 保存文件。

+ 4. 运行 playbook：

```bash
$ ansible-playbook -i inventory new-cluster.yml
```

## 17.5. 使用 ha_cluster 系统角色在高可用性集群中配置 APACHE HTTP 服务器

此过程使用 `ha_cluster` 系统角色，在包含两个节点的 Red Enterprise Linux Availability Add-on 中配置一个主/备用模式的 Apache HTTP 服务器。

### 前提条件

- 你在想要运行 playbook 的节点上已安装了 Red Hat Ansible Engine。

> 注意：
>
> 你不需要在集群成员节点上安装 Ansible Engine。

- 你在想要运行 playbook 的系统上已安装了 `rhel-system-roles` 软件包。有关 RHEL 系统角色以及如何应用它们的详细信息，请参阅[开始使用 RHEL 系统角色](Getting started with RHEL System Roles)。

- 你将作为集群成员运行 RHEL 的系统必须对 RHEL 和 RHEL High Availability Add-On 有有效的订阅支持。

- 你的系统包含公共 IP 地址，这是 Apache 所必需的。

- 你的系统包含集群节点的共享存储，使用 iSCSI、光纤通道或其他共享网络设备。

- 你已按照[在 Pacemaker 集群中配置带有 ext4 文件系统的 LVM 卷]的描述配置了 ext4 的 LVM 逻辑卷。

- 你已按照[配置 Apache HTTP 服务器]的描述配置了 Apache HTTP 服务器。

- 你的系统包含 APC 电源，将用于对集群节点进行隔离（fence）。

> 注意：
>
> `ha_cluster` 系统角色将替换指定节点上的任何现有集群配置。角色中未指定的任何设置将丢失。

### 步骤

- 1. 创建一个清单文件并指定集群中的节点，其描述见[为 ha_cluster 系统角色指定清单](Specifying an inventory for the ha_cluster system role)。

- 2. 创建一个 playbook 文件，例如 `http-cluster.yml`：以下示例 playbook 在主/备模式的双节点 HA 集群中配置之前创建的 Apache HTTP 服务器。

此示例使用了主机名为 `zapt.example.com` 的 APC 电。如果集群不使用任何隔离代理（fence agents），你只能在定义 `ha_cluster_fence_agent_packages` 变量时列出集群所需的隔离代理，如本示例所示。

在为生产环境创建 playbook 文件时，建议使用 Ansible Vault 加密密码，描述如[使用 Ansible Vault 加密内容](Encrypting content with Ansible Vault)所示。



```yaml
- hosts: z1.example.com z2.example.com
- rhel-system-roles.ha_cluster vars:_cluster_hacluster_password: ha_cluster_name: my_cluster
ha_cluster_fence_agent_packages:
  - fence-agents-apc-snmp
ha_cluster_resource_primitives:
  - id: myapc
    agent: stonith:fence_apc_snmp
    instance_attrs:
      - attrs:
          - name: ipaddr
          value: zapc.example.com
        - name: pcmk_host_map
          value: z1.example.com:1;z2.example.com:2
        - name: login
          value: apc
        - name: password
          value: apc
  - id: my_lvm
    agent: ocf:heartbeat:LVM-activate
    instance_attrs:
      - attrs:
          - name: vgname
          value: my_vg
        - name: vg_access_mode
          value: system_id
  - id: my_fs
    agent: Filesystem
    instance_attrs:
      - attrs:
          - name: device
          value: /dev/my_vg/my_lv
        - name: directory
          value: /var/www
        - name: ftype
          value: ext4
  - id: VirtualIP
    agent: IPaddr2
    instance_attrs:
      - attrs:
          - name: ip
          value: 198.51.100.3
        - name: cidr_netmask
          value: 24
  - id: Website
    agent: apache
    instance_attrs:
      - attrs:
          - name: ip
          value: 198.51.100.3
        - name: cidr_netmask
          value: 24
```

## 17. 使用 ROLES 配置高可用集群

### 17.5. 使用 HA_CLUSTER 角色在高可用集群中配置 APACHE HTTP 服务器

以下示例 playbook 在主/备模式的双节点 HA 集群中配置之前创建的 Apache HTTP 服务器。

此示例使用了主机名为 `zapt.example.com` 的 APC 电。

```yaml
- hosts: z1.example.com z2.example.com
- rhel-system-roles.ha_cluster vars:_cluster_hacluster_password: ha_cluster_name: my_cluster
ha_cluster_fence_agent_packages:
  - fence-agents-apc-snmp
ha_cluster_resource_primitives:
  - id: myapc
    agent: stonith:fence_apc_snmp
    instance_attrs:
      - attrs:
          - name: ipaddr
          value: zapc.example.com
        - name: pcmk_host_map
          value: z1.example.com:1;z2.example.com:2
        - name: login
          value: apc
        - name: password
          value: apc
  - id: my_lvm
    agent: ocf:heartbeat:LVM-activate
    instance_attrs:
      - attrs:
          - name: vgname
          value: my_vg
        - name: vg_access_mode
          value: system_id
  - id: my_fs
    agent: Filesystem
    instance_attrs:
      - attrs:
          - name: device
          value: /dev/my_vg/my_lv
        - name: directory
          value: /var/www
        - name: ftype
          value: ext4
  - id: VirtualIP
    agent: IPaddr2
    instance_attrs:
      - attrs:
          - name: ip
          value: 198.51.100.3
        - name: cidr_netmask
          value: 24
  - id: Website
    agent: apache
    instance_attrs:
      - attrs:
          - name: ip
          value: 198.51.100.3
        - name: cidr_netmask
          value: 24
```

+ 3. 保存文件。

+ 4. 运行 playbook：

```bash
$ ansible-playbook -i inventory new-cluster.yml
```

## 17.5. 使用 HA_CLUSTER 角色在高可用集群中配置 APACHE HTTP 服务器

此过程使用 `ha_cluster` 系统角色，在包含两个节点的 Red Enterprise Linux Availability Add-on 中配置一个主/备模式的 Apache HTTP 服务器。

### 前提条件

- 你在想要运行 playbook 的节点上已安装了 Red Hat Ansible Engine。

> 注意：
>
> 你不需要在集群成员节点上安装 Ansible Engine。

- 你在想要运行 playbook 的系统上已安装了 `rhel-system-roles` 软件包。有关 RHEL 系统角色以及如何应用它们的详细信息，请参阅[开始使用 RHEL 系统角色](Getting started with RHEL System Roles)。

- 你将作为集群成员运行 RHEL 的系统必须对 RHEL 和 RHEL High Availability Add-On 有有效的订阅支持。

- 你的系统包含公共 IP 地址，这是 Apache 所必需的。

- 你的系统包含集群节点的共享存储，使用 iSCSI、光纤通道或其他共享网络设备。

- 你已按照[在 Pacemaker 集群中配置带有 ext4 文件系统的 LVM 卷]的描述配置了 ext4 的 LVM 逻辑卷。

- 你已按照[配置 Apache HTTP 服务器]的描述配置了 Apache HTTP 服务器。

- 你的系统包含 APC 电，将用于对集群节点进行隔离（fence）。

> 注意：
>
> `ha_cluster` 系统角色将替换指定节点上的任何集群配置。角色中未指定的任何设置将丢失。

### 步骤

- 1. 创建一个清单文件并指定集群中的节点，其描述见[为 ha_cluster 系统角色指定清单](Specifying an inventory for the ha_cluster system role)。

- 2. 创建一个 playbook 文件，例如 `http-cluster.yml`：以下示例 playbook 在主/备模式的双节点 HA 集群中配置之前创建的 Apache HTTP 服务器。

此示例使用了主机名为 `zapt.example.com` 的 APC 电。如果集群不使用任何隔离代理（fence agents），你只能在定义 `ha_cluster_fence_agent_packages` 变量时列出集群所需的隔离代理，如本示例所示。



在为生产环境创建 playbook 文件时，建议使用 Ansible Vault 加密密码，描述如[使用 Ansible Vault 加密内容](Encrypting content with Ansible Vault)所示。

```yaml
- hosts: z1.example.com z2.example.com
- rhel-system-roles.ha_cluster vars:_cluster_hacluster_password: ha_cluster_name: my_cluster
ha_cluster_fence_agent_packages:
  - fence-agents-apc-snmp
ha_cluster_resource_primitives:
  - id: myapc
    agent: stonith:fence_apc_snmp
    instance_attrs:
      - attrs:
          - name: ipaddr
          value: zapc.example.com
        - name: pcmk_host_map
          value: z1.example.com:1;z2.example.com:2
        - name: login
          value: apc
        - name: password
          value: apc
  - id: my_lvm
    agent: ocf:heartbeat:LVM-activate
    instance_attrs:
      - attrs:
          - name: vgname
          value: my_vg
        - name: vg_access_mode
          value: system_id
  - id: my_fs
    agent: Filesystem
    instance_attrs:
      - attrs:
          - name: device
          value: /dev/my_vg/my_lv
        - name: directory
          value: /var/www
        - name: ftype
          value: ext4
  - id: VirtualIP
    agent: IPaddr2
    instance_attrs:
      - attrs:
          - name: ip
          value: 198.51.100.3
        - name: cidr_netmask
          value: 24
  - id: Website
    agent: apache
    instance_attrs:
      - attrs:
          - name: ip
          value: 198.51.100.3
        - name: cidr_netmask
          value: 24
```

- 3. 保存文件。
- 2. 位于 `z1.example.com` 运行，可以通过浏览器查看的资源。
