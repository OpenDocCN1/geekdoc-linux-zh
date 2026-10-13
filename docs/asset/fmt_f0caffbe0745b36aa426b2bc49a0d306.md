
```
[user@controlnode ~]$ ansible-playbook packages.yml

PLAY [Display installed packages] ********************************

TASK [Gathering Facts] ****************************************
ok: [server.lab.com]

TASK [Gather info on installed packages] ***********************************
ok: [server.lab.com]

TASK [List installed packages] **************************************
ok: [server.lab.com] => {
  "ansible_facts.packages": {
    "arch": "x86_64",
    "epoch": 1,
    "name": "NetworkManager",
    "release": "14.18",
    "source": "rpm",
    "version": "1.14"
  }
}

TASK [Display NetworkManager version] **********************************
ok: [server.lab.com] => {
  "msg": "Version 1.14"
}
```

# 第 10 章 | 自动化Linux任务

## 管理包的替代模块

`Yum` 模块使用托管主机上的 `Yum` 软件包管理器来处理包操作。以下示例是在 `servera.lab.example.com` 托管主机上安装 `httpd` 包的 playbook。

```yaml
---
- name: Install the required packages on the web server
  hosts: servera.lab.example.com
  tasks:
    - name: Install the httpd packages
      yum:
        name: httpd
        state: present
```

- `name` 关键字给出要安装的包的名称。
- `state` 关键字指示包在托管主机上的预期状态。

**present**

如果该包不存在，Ansible 将安装该包。

**absent**

如果该包已安装，Ansible 将移除该包。

下表比较了 `yum` 模块的一些用法与等效的 `yum` 命令。

| ANSIBLE 任务 | YUM 命令 |
|---|---|
| name: 安装 httpd<br>yum:<br>name: httpd<br>state: present | `yum install httpd` |
| name: 安装或更新 httpd<br>yum:<br>name: httpd<br>state: latest | `yum update httpd` 或如果包尚未安装则执行 `yum install httpd`。 |
| name: 更新所有包<br>yum:<br>name: '*'<br>state: latest | `yum update` |
| name: 移除 httpd<br>yum:<br>name: httpd<br>state: absent | `yum remove httpd` |
| name: 安装开发工具<br>yum:<br>name: '@Development Tools'<br>state: present | `yum group install "Development Tools"` |

> 使用你的 Ansible 模块时，必须在组名前加加上 `@`。请记住你通过 `yum group list` 获取组列表。

- name: 移除开发工具
  yum:
    name: `@Development Tools`
    state: absent
  `yum group remove "Development Tools"`

- name: perl AppStream 模块
  yum:
    name: `@perl:5.26/minimal`
    state: present
  `yum module install perl:5.26/minimal`

> 要管理 Yum AppStream 模块，请在模块名称前加上 `@`。语法与 `yum` 命令相同。例如，你可以省略默认配置：`@perl:5.26`。记住你可以通过 `yum module list` 列出可用的 Yum AppStream 模块。

运行 `ansible-doc yum` 命令可以获取额外的参数和 playbook 示例。

## 优化多个包的安装

要对多个包进行操作，`name` 关键字接受列表。以下示例显示了在 `servera.lab.example.com` 上安装三个包的 playbook。
