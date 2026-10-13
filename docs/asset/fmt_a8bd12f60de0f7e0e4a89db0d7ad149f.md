
```bash
TASK [Gathering Facts]
**********************************************************************************
ok: [labhost1.example.com]
ok: [test1.example.com]
ok: [labhost2.example.com]
ok: [test2.example.com]
ok: [data.example.com]
```

## 列表

清单中的多个项目可以使用逻辑列表进行引用。逗号分隔的主机模式列表将匹配所有符合其中一个模式的主机。

如果你提供了一个逗号分隔的托管主机列表，那么所有托管主机都将被视为目标。

```bash
[student@controlnode ~]$ cat playbook.yml
---
hosts: labhost1.example.com,test2.example.com,192.168.2.2
[student@controlnode ~]$ ansible-playbook playbook.yml
```

## 参考文献

[操作模式 – Ansible 文档](https://docs.ansible.com/ansible/latest/latest/user_guide/intro_patterns.html)

[清单 – Ansible 文档](https://docs.ansible.com/ansible/latest/latest/user_guide/intro_inventory.html)

# 引导练习

## 使用主机模式选择主机

在此练习中，你将探索如何使用主机模式来指定清单中的主机，用于执行 play 或即时命令。你将获得几个示例清单来探索主机模式。

## 学习成果

你将能够使用不同的主机模式来访问清单中的各种主机。

## 开始之前

使用 `lab projects-host start` 命令以 student 身份登录工作站。该脚本将创建 `projects-host` 主机目录，并下载此练习所需的 Ansible 配置和主机清单文件。

```
[student@workstation -]$ lab projects-host start
```

- 1. 在工作站上，切换到练习的工作目录 `/home/student/projects-host` 并查看目录内容。

- 1.1. 列出目录内容。

```
[student@workstation projects-host]$ ls ansible.cfg inventory1 inventory2 playbook.yml
```

- 1.2. 检查示例清单文件 `inventory1`。注意清单的组织方式。探索清单中哪些主机和组，以及使用了哪些域名。

```
srv1.example.com
srv2.example.com
s1.lab.example.com
s2.example.com
```

```
[web]
jupiter.lab.example.com
saturn.example.com
```

```
[db]
```

```
db1.example.com
db2.example.com
db3.example.com
```

```
[ib]
db1.lab.example.com
db2.lab.example.com
```

```
[boston]
db1.example.com
jupiter.lab.example.com
db2.lab.example.com
```

```
[london]
db2.example.com
db3.example.com
file1.lab.example.com
lbi1.lab.example.com
```

```
[dev]
web1.lab.example.com
db3.example.com
```

```
[stage]
file2.example.com
db2.example.com
```

```
[prod]
db2.lab.example.com
db1.example.com
jupiter.lab.example.com
```

```
[function:children]
web
db
lb
city
```

```
[city:children]
boston
london
environ
```

```
[environments:children]
dev
stage
prod
new
```

```
[new]
172.25.25.23
172.25.25.44
172.25.25.32
```

- 1.3. 检查清单文件 `inventory2`。注意清单的组织方式。探索清单中哪些主机和组，以及使用了哪些域名。

```
workstation.lab.example.com
```

```
[london]
servera.lab.example.com
```

[berlin]

serverb.lab.example.com

```
[tokyo]
serverc.lab.example.com
```

[atlanta]

serverd.lab.example.com

```

```

[europe:children]

london

berlin

```

- 1.4. 最后，检查 playbook `playbook.yml` 的内容。注意 playbook 如何使用 `debug` 模块显示每个托管主机的名称。

- 2. 使用即时命令，确定 `dbi.example.com` 服务器是否存在于 `inventory1` 清单文件中。

```
[student@workstation projects-host]$ ansible dbi.example.com -i inventory1 \
  > --list-hosts
  hosts (1):
    dbi.example.com
```

# 第 7 章 | 管理大型项目

- 3. 使用即时命令，通过主机模式引用 `inventory1` 清单包含包含 IP 地址。

```
[student@workstation projects-host]$ ansible 172.25.252.44 -i inventory1 \
> --list-hosts
hosts (1):
172.25.252.44
```

- 4. 使用即时命令，使用组列出 `inventory1` 清单中的所有托管主机。

```
[student@workstation projects-host]$ ansible all -i inventory1 --list-hosts
hosts (17):
srv1.example.com
srv2.example.com
sdb1.example.com
sdb2.example.com
jupiter.lab.example.com
saturn.lab.example.com
dbi1.example.com
db2.example.com
db3.example.com
lab1.lab.example.com
lab2.lab.example.com
file1.lab.example.com
web1.lab.example.com
file2.example.com
172.25.252.23
172.25.252.44
172.25.252.32
```

- 5. 使用即时命令，使用星号 `*` 字符列出 `inventory1` 清单中所有以 `.example.com` 结尾的主机。

```
[student@workstation projects-host]$ ansible '*.example.com' -i inventory1 \
> --list-hosts
hosts (14):
jupiter.lab.example.com
saturn.example.com
dbi1.example.com
db2.example.com
db3.example.com
lab1.lab.example.com
lab2.lab.example.com
file1.lab.example.com
web1.lab.example.com
file2.example.com
srv1.example.com
srv2.example.com
db.example.com
```

- 6. 从上一个命令的输出可以看到，`*.example.com` 域名有 14 台主机。修改之前的即时命令主机模式，忽略 `*.lab.example.com` 域名的主机。

```
[student@workstation projects-host]$ ansible '*example.com,!*.lab.example.com' \
-i inventory1 --list-hosts
hosts (7):
saturn.example.com
```
