
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
