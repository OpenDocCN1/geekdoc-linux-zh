
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
