
$student@workstation system-network$

```
- 1.2. 验证 `server1a.example.com` 是否属于 `webservers` 主机组。该服务器有一个服务器网络接口。
```

$student@workstation system-network$ `cat` `inventory`

[webservers]

server1a.example.com

- 2. 使用 `ansible-galaxy` 命令验证系统角色是否可用。如果没有可用角色，你需要安装 `ansible-system-roles` 包。

```
$student@workstation system-network]$ `ansible-galaxy` `list`

/usr/share/ansible/roles

- rhel-system-roles.kafka, (unknown version)

- rhel-system-roles.network, (unknown version)

- rhel-system-roles.postfix, (unknown version)

- rhel-system-roles.selinux, (unknown version)

- rhel-system-roles.timesync, (unknown version)
```

![](img/c66fec31e9528c7da22e5fa5113dfa6e_477_0.png)

- - rhel-system-roles.kafka, (unknown version)
- rhel-system-roles.network, (unknown version)
- rhel-system-roles.postfix, (unknown version)
- rhel-system-roles.selinux, (unknown version)
- rhel-system-roles.timesync, (unknown version)

- 3. 使用 `ansible-galaxy` 命令验证系统角色是否可用。（等等，OCR 文本似乎存在碎片化/重复）

R1294-RHEL8.0-en-1-20190531 461

- 3. 使用 `ansible-galaxy` 命令验证系统角色是否可用。如果没有可用角色，你需要安装 `ansible-system-roles` 包。

- 3.1. 作为工作站上的 student 用户，切换到 `/home/student/system-network` 工作目录。
- 3.2. 验证 `server1a.example.com` 是否属于 `webservers` 主机组。该服务器有一个服务器网络接口。
- 3.3. 创建一个使用 `rhel-system-roles` 来配置网络接口的 playbook。
- 3.4. 查看该角色的 `README.md` 文件。
- 3.5. 运行 playbook 以配置网络接口。

## 第 10 章 | 自动化 Linux 管理任务

## 实验

# 自动化 Linux 管理任务

## 性能检查清单

在本实验中，你将使用 playbook（剧本）对受托管主机进行配置并执行管理任务。

## 学习目标

你应该能够创建 playbook，用于配置受托管主机的软件仓库、用户和组、逻辑卷、定时任务（cron jobs）以及额外的网络接口。

## 准备工作

在工作站上运行实验脚本以确认环境已准备好开始实验。该脚本创建一个名为 `system-review` 的工作目录，并向其中填充 Ansible 配置文件、主机清单和实验文件。

```
student@workstation~$ `lab` `system-review` `start`
```

- 1. 在 `webservers` 主机组上创建并执行一个 playbook，用于配置位于 http://materials.example.com/yum/repository 的 Yum 内部仓库，并安装该仓库中的 `-mysql` 软件包。所有 RPM 包都用管理 GPG 密钥对进行了签名。GPG 公钥可以通过 http://materials.example.com/repository/RPM-GPG-KEY-example 获取。
- 2. 在 `webservers` 主机组上创建并执行一个 playbook，创建 `webadmin` 用户组，并向该组添加两个用户 `ops1` 和 `ops2`。
- 3. 在 `webservers` 主机组上创建并执行一个 playbook，使用 `/dev/vdb` 设备创建一个名为 `apache-vg` 的逻辑卷。这也建立了两个名为 `content-lv` 和 `log-lv1` 的逻辑卷，它们都由 `apache-vg` 卷支持。最后，在每个逻辑卷上创建 VFS 文件系统，并将 `content-volume` 挂载到 /var/var，`log-lv1` 本地卷挂载到 /var/log/bind。实验脚本在 ~/system-review 中创建了两个文件：`storage.yml` 为 playbook 提供初始骨架，`storage_vars.xml` 为不同模块所需的所有变量提供值。
- 4. 在 `webservers` 主机组上创建并执行一个 playbook，使用 cron 模块执行 `/etc/cron.d/usage` cron 文件，以调度循环的 cron 任务。该任务应在周一至周五每两个月的 09:00 和 16:59 以 devops 身份运行。任务应将当前磁盘使用情况追加到文件 /home/devops/disk_usage。
- 5. 在 `webservers` 主机组上创建并执行一个 playbook，使用 `linux-system-roles.network` 角色为备用网络接口 ens4 配置 172.25.250.40/24 IP 地址。
- 6. 在工作站上运行 `lab system-review grade` 对对你的工作进行评分。

46 RH294-RHEL.8.0-en-1-20190531

## 完成

在工作站上运行 `lab system-review finish` 脚本以清理在本实验中创建的资源。

```
[student@workstation ~]$ `lab` `system-review` `finish`
```

实验结束。

# 自动化 Linux 管理任务

## 性能检查清单

在本实验中，你将使用 playbook 对受托管主机进行配置并执行管理任务。

## 学习目标

你应该能够创建 playbook，用于配置受托管主机的仓库、用户和组、逻辑卷、定时任务以及额外的网络接口。

## 准备工作

在工作站上运行实验脚本以确认环境已准备好开始实验。该脚本创建一个名为 `system-review` 的工作目录，并向其中填充 Ansible 配置文件、主机清单和实验文件。

```
[student@workstation -~$ `lab` `system-review` `start`
```

- 1. 在 `webservers` 主机组上创建并执行一个 playbook，用于配置位于 http://materials.example.com/yum/repository 的 Yum 内部仓库，并安装该仓库中的 `example-mold` 软件包。所有 RPM 包都用组织 GPG 密钥对进行了签名。GPG 公钥可以通过 http://materials.example.com/repository/RPM-GPG-KEY-example 获取。
- 1.1. 作为工作站用户，切换到 /home/student/system-review 工作目录。

```
[student@workstation -~$ `cd` ~/system-review

[student@workstation system-review ~$]
```
