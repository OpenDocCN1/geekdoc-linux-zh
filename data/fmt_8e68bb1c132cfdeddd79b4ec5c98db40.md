
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
