
对 `playbook.yml` 进行以下更改，使其更易管理，并对其进行调整，以确保未来的执行使用滚动更新，防止所有四个 Web 服务器同时不可用。

- 1. 使用通配符主机模式简化 playbook 中的托管主机列表。使用 `inventory/inventory.py` 动态清单脚本验证通配符主机模式。
- 2. 重构 playbook，将 playbook 中的前三个任务保留位于 `tasks/web-tasks.yml` 的外部任务文件中。使用 `import_tasks` 功能将该任务文件整合到 playbook 中。
- 3. 重构 playbook，将 playbook 中的第四、第五和第六个任务保留位于 `tasks/firewall_tasks.yml` 的外部任务文件中。使用 `import_tasks` 功能将该任务文件整合到 playbook 中。
- 4. `tasks/web-tasks.yml` 和 `tasks/firewall_tasks.yml` 文件之间存在一些任务重复。将安装软件包和启用服务的任务移动到名为 `tasks/install_and_enable.yml` 的新文件中，并使用变量。

`RH29-1-RHEL8.0-an-1-20190531`

# 第 7 章 | 管理大型项目

用 `import_tasks` 语句替换原始任务，并传入适当的变量值。

- 5. 如果以后 `files/tune.conf` 文件发生更改，可能会触发 `httpd` 服务的处理器，因此在 `playbook.yml` 中实现滚动更新功能，并将滚动更新批处理大小设置为两个主机。
- 6. 验证 `playbook.yml` 的更改已正确完成，然后执行 playbook。

# 评估

运行 `lab-review grade` 命令以确认本次练习成功。修正任何报告的失败并重新运行脚本直到成功。

```
[student@workstation ~]$ lab projects-review grade
```

## 结束

在工作站上，运行 `lab-projects-review finish` 脚本以清理实验中创建的资源。

```
[student@workstation ~]$ lab projects-review finish
```

实验结束。

```
[student@workstation ~]$ cd ~/projects-review
[student@workstation projects-review]$ cat ansible.cfg
[defaults]
inventory = inventory
...输出已省略...
```

# 第 7 章 | 管理大型项目

```
[student@workstation projects-review]$ 11
total 16
-rw-rw-r--. 1 student 33 Dec 19 00:48.cfg
-drwxrxr-x. 2 student 4096 Dec 18 22:35 files
-drwxrxr-x. 2 student 4096 Dec 19 01:18 inventory
-rw-rw-r--. 1 student 959 Dec 18 23:48 playbook.yml
[student@workstation projects-review]$ 11 inventory/
total 4
-rwwxrxr-x. 1 student 612 Dec 19 01:18 inventory.py
```

1.2. 使 `inventory/inventory.py` 动态清单具有可执行权限，然后使用 `--list` 选项执行清单脚本以显示清单中的完整主机列表。

```
[student@workstation projects-review]$ chmod 755 inventory/inventory.py
[student@workstation projects-review]$ inventory/inventory.py --list
"all": {
  "hosts": [
    "server.lab.example.com",
    "servc.lab.example.com",
    "serverd.lab.example.com",
    "workstation.lab.example.com"
  ],
  "vars":
  ))
```

1.3. 验证主机模式 `*.lab.example.com` 正确识别了 `playbook.yml` 目标的四个托管主机。

```
[student@workstation projects-review]$ ansible server*.lab.example.com \
> --list-hosts
hosts (4):
server.lab.example.com
serverd.lab.example.com
servera.lab.example.com
serverc.lab.example.com
```

1.4. 将 `playbook.yml` 中的主机列表替换为 `server*.lab.example.com` 主机模式。

- - name: 安装并配置 Web 服务器
hosts: server*.lab.example.com
...输出省略...

`RH29-1-RHEL8.0-an-1-20190531 28`

# 第 7 章 | 管理大型项目

2. 重构 playbook，将 playbook 中的前三个任务保留位于 `tasks/web-tasks.yml` 的外部任务文件中。使用 `import_tasks` 功能将该任务文件整合到 playbook 中。

2.1. 创建 `tasks` 子目录。

```
[student@workstation projects-review]$ mkdir tasks
```
