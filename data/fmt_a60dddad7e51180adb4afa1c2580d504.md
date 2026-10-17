
```
PLAY [Configuration]
********************************************************************
TASK [Gathering Facts]
********************************************************************
ok: [server.lab.example.com]
TASK [rhel-system-roles.network : Check which services are running]
********************************************************************
ok: [server.lab.example.com]
TASK [rhel-system-roles.network : Check which packages are installed]
********************************************************************
ok: [server.lab.example.com]
TASK [rhel-system-roles.network : Print network provider]
********************************************************************
ok: [server.lab.example.com] => {
  "msg": "Using network provider: nm"
}
TASK [rhel-system-roles.network : Install packages]
********************************************************************
skipping: [server.lab.example.com]
TASK [rhel-system-roles.network : Enable network service]
********************************************************************
ok: [server.lab.example.com]
TASK [rhel-system-roles.network : Configure networking]
********************************************************************
changed: [server.lab.example.com]
[WARNING]: the configured path /home/student/.ansible/roles does not
exist.
TASK [rhel-system-roles.network : Configure connectivity]
********************************************************************
ok: [server.lab.example.com]
```

# 第 5 章，实现任务控制

在 Ansible Playbook 中管理任务控制、处理器和任务错误。

- 实现循环以编写高效的任务，以控制任务的运行时机。
- 实现仅当另一个任务更改了受托管主机时才运行的任务。
- 控制任务失败时的处理方式以及导致任务失败的条件。

# 第 6 章，将文件部署到受托管主机

通过 Ansible 在受托管主机上部署、管理和调整文件。

- 在受托管主机上创建、安装、编辑和删除文件，并管理这些文件的权限、所有权、SELinux 上文和其他特性。
- 使用 Jinja2 模板自定义文件并将其部署到受托管主机。

# 第 7 章，管理大型项目

编写为更大更复杂的项目优化的 playbook。

- 编写复杂的模式，以便为 play 或临时命令（ad hoc command）高效选择主机。
- 描述动态清单的性质和目的，然后安装并使用现有脚本作为 Ansible 清单源。
- 调整 Ansible 打开受托管主机的并发连接数，以及 Ansible 如何通过 play 的任务处理受托管主机组。
- 通过从外部文件导入或包含 playbook 和任务来管理大型项目，可以是无条件的，也可以基于条件测试。

# 第 8 章，通过角色简化 Playbook

使用 Ansible 角色更快速地开发 playbook 并复用 Ansible 代码。

- 描述什么是角色、它的结构如何以及你如何在 playbook 中使用它。
- 在 playbook 的项目目录中创建角色，并将其作为 playbook 中某个 play 的一部分运行。
- 从 Ansible Galaxy或其他来源（如 Git 仓库）选择并检索角色，并在 playbook中使用它们。
- 编写利用 Red Enterprise Linux System Roles 执行标准操作的 playbook。

# 第 9 章，排查 Ansible故障

排除 playbook 和受托管主机的问题。

- 排查新 playbook 的通用问题并修复它们。

# 第 10 章，自动化 Linux 管理任务

使用 Ansible 自动化常见的 Linux 系统管理任务。

- 在受托管主机上订阅系统、配置软件通道和存储库并管理 RPM 包。
- 在受托管主机上管理 Linux 用户和组、配置 SSH 并修改 Sudo 配置。
- 管理受托管主机上的服务启动、使用 `at`、`cron`、`systemd`、`reboot` 调度进程并控制默认启动目标。
- 划分存储设备、配置 LVM、格式化分区或逻辑卷、挂载文件系统并添加交换文件或空间。

## 实验

### 部署 ANSIBLE

在复习中，你将在工作站上安装 Ansible，将其作为控制节点，并配置连接到受托管主机 `servera` 和 `serverb`。使用临时命令在受托管主机上执行操作。

#### 成果

你应该能够：

- 安装 Ansible。
- 使用临时命令在受托管主机上执行操作。

#### 指南

在工作站上安装并配置 Ansible。证明你可以构建标准列表中指定的临时命令来修改受托管主机，并验证修改符合预期：

- 在工作站上安装 Ansible，使其能够作为控制节点。
- 在控制节点上，创建一个清单文件 `/home/student/review-deploy/inventory`，其中包含一个名为 `dev` 的组。该组应由受托管主机 `servera`、`lab.example.com` 和 `serverb.lab.example.com` 组成。
- 在 `/home/student/review-deploy/ansible.cfg` 创建 Ansible 配置文件。该配置文件应指向清单文件 `/home/student/review-deploy/inventory`。
- 使用权限提权执行临时命令，修改 `servera` 和 `serverb` 上的 `/etc/motd` 文件内容，使其包含字符串 `Managed by Ansiblen`。使用 `devops` 作为远程用户。
- 执行临时命令以验证 `servera` 和 `serverb` 上的 `/etc/motd` 文件内容是否相同。

#### 评估

在工作站上，运行实验 `lab review-deploy grade` 命令以确认练习成功。纠正任何报告的失败并重新运行命令直到成功。

```
$student@workstation~$ lab review-deploy grade
```

#### 结束

在工作站上，运行实验 `lab review-deploy finish` 命令来清理本次练习。

```
$student@workstation~$ lab review-deploy finish
```

实验此结束。

# 第 11 章 | 综合复习：使用 Ansible 实现自动化

## 解决方案

### 部署 ANSIBLE

在复习中，你将在工作站上安装 Ansible，将其作为控制节点，并配置连接到受托管主机 `server` 和 `server`。使用临时命令在受托管主机上执行操作。

#### 成果

你应该能够：

- 安装 Ansible。
- 使用临时命令在受托管主机上执行操作。

#### 指南

在工作站上安装并配置 Ansible。证明你可以构建标准列表中指定的临时命令来修改受托管主机，并验证修改符合预期：

- 在工作站上安装 Ansible，使其能够作为控制节点。
- 在控制节点上，创建一个清单文件 `/home/student/review-deploy/inventory`，其中包含一个名为 `dev` 的组。该组应由受托管主机 `server.lab.example.com` 和 `serverb.lab.example.com` 组成。
