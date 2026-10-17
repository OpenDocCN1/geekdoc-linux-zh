
# 使用 Ansible Tower 自动化任务

## 自动化框架

虽然运行 `Ansible playbooks` 和命令对于自动化和后续修改主机组非常有效，但对于完全管理的企业，你可以通过 `Ansible Tower` 更进一步。`Ansible Tower` 提供了一个基于 Web 的界面，用于使用 `Ansible playbooks` 和其他组件管理整个 IT 基础设施。通过将 `Ansible` 资产集中在一个地方，你就有了一个接收通知的单一位置。你可以管理企业中不同的角色。

`Ansible Tower` 界面使得持续更新你配置的资产变得简单。你不需要记住命令行选项，只需点击即可完成配置。

## 第 29 章：使用 Ansible 自动化应用程序和基础设施

启动你的 `Ansible`。清单管理是图形化的，作业调度可以通过直观、可视化的方式完成。

`Ansible Tower` 提供了 `REST API`，可以帮助你将现有的基础设施工具集成到 `Ansible` 中。因此，你通常只需要继续现有的流程，但改用 `Ansible` 来管理它们。

你可以从 `Ansible` 官网（`https://www.ansible.com/products/tower`）了解更多关于 `Ansible Tower` 的信息。

### 总结

`Ansible` 提供了一种独特的格式化语言和工具集，用于自动化你在本书其他部分学过的许多任务。一旦你学会了如何运行 `Ansible playbooks`，你就可以识别出系统上所需的精确配置，并轻松地将该配置部署到一个或多个主机系统上。

通过 `Ansible playbooks`，你定义了应用程序及其周围组件的精确状态，并将其应用于 Linux 主机系统、网络设备或其他目标。你可以保存这些 `playbooks` 并重复使用，以便在其他系统上产生类似的结果，或者通过即时命令（`ad-hoc`）它们来创建新的、不同的结果。

`Ansible` 还可以使用即时命令来更新系统。从命令行，你可以添加用户、复制文件、安装软件，或几乎是你可以用 `playbooks` 完成的任何操作。通过这些命令，你可以快速地对多个主机应用一组更改，或者响应某个需要立即修复到一组主机上的问题。

在本章中，你学习了构成 `Ansible` 集合的不同组件。你创建了自己用于部署简单 Web 服务器的 `playbook`。然后，你运行了一些即时命令来修改你部署该 `playbook` 的系统。

# 练习题

这些练习题测试了你在系统上安装 `Ansible`、创建第一个 `Ansible playbook` 以及运行几个 `Ansible` 即时命令的能力。这些任务假设你正在运行 `Fedora` 或红帽企业级 Linux（`RHEL`）系统（尽管某些任务可以在其他 Linux 系统上运行）。

虽然 `Ansible` 旨在将任务部署到远程系统，但此处的练习将让你在单个系统上尝试运行 `playbook` 和一些命令。如果你遇到困难，附录 B 中列出了任务的解答（尽管在 Linux 中，你通常可以通过多种方式完成某项任务）。

- 1. 在你的 `Fedora` 或 `RHEL` 系统上安装 `Ansible`。
- 2. 为你想要用于执行这些练习的用户添加 `sudo` 权限。

# 第六部分：接触云计算

- 3. 创建一个 `Ansible playbook` 的开头（命名为 `my_playbook.yaml`），包含以下内容。

```yaml
name: Create web server

hosts: localhost

tasks:
  name: Install httpd
    yum:
      name: httpd
      state: present
```
