
Connection to servera.lab.example.com closed.

```
## 完成

在工作站上，运行 `lab data-secret finish` 脚本清理本次练习。
```

[student@workstation ~$] lab data-secret finish

```
练习结束。

# 管理事实

## 目标
完成本节后，你应当能够引用关于主机的数据并配置自定义事实。

## 描述事实
Ansible 事实是 Ansible 自动发现的变量。事实包含可以像普通变量一样使用的主机特定信息。从托管主机收集的一些事实可能：

- 主机名
- 内核版本
- 网络接口
- IP 地址
- 操作系统版本
- CPU 数量
- 可用磁盘空间

事实是获取托管主机状态并根据该状态采取行动的方便方法。例如，根据事实重启服务器。

通常，每个 play 在执行第一个任务之前都会运行 `setup` 模块。要查看从托管主机收集了哪些事实，可以运行一个收集事实并使用 `debug` 模块的短 playbook。

# 第 4 章 | 管理变量和事实

```
- name: Fact dump
  hosts: all
  name: Print all facts
  debug:
    var: ansible_facts
```

当运行该 playbook 时，事实将以 JSON 格式显示在作业输出中：

```
[user@demo] ~$ ansible-playbook facts.yml
```

```
PLAY [Fact dump] *************************************************

TASK [Gathering Facts] *****************************************************

ok: [demo1.example.com]

TASK [Print all facts] *****************************************************

ok: [demo1.example.com] => {

  "ansible_ipv4_addresses": [

    "172.250.250.10"

  ],

  "ansible_ipv6_addresses": [

    "fe80:5054:ff:fe00:fa0a"

  ],

  "ansible_local": {

    "apporor": {

      "status": "disabled",

      "architecture": "x86_64",

      "bios_date": "01/01/2011",

      "bios_version": "0.5.1",

      "cmdline": {

        "BOOT_IMAGE": "/boot/vmlinuz-3.10.0-327.el7.x86_64",

        "LANG": "en_US.UTF-8",

        "console": "ttyS0,11520n8",

        "crashkernel": "auto",

        "net.interfaces": "",

        "no_timer_check": true,

        "ro": true

      },

      "root": "UUID:2240a0b6-e869-4011-acae-31b2e8c0c5a3"}
```

playbook 以 JSON 格式显示 `ansible_facts` 变量的内容，表现为变量的哈希/字典。你可以浏览输出以查看收集了哪些事实，找到你可能在 play 中使用的事实。

下表显示了可能从托管节点收集并对 playbook 中有用的某些事实：

## 第 4 章 | 管理变量与 Facts

### Ansible Facts 示例

| 事实 (FACT) | 变量 (VARIABLE) |
|---|---|
| 短主机名 | `ansible_facts['hostname']` |
| 完全限定域名 | `ansible_facts['fqdn']` |
| 主 IPv4 地址（基于路由） | `ansible_facts['default_ipv4']['address']` |
| 所有网络接口的名称列表 | `ansible_facts['interfaces']` |
| /dev/vda1 分区的大小 | `ansible_facts['devices']['vda']['vda1']['size']` |
| DNS 服务器列表 | `ansible_facts['dns']['nameservers']` |
| 当前运行内核的版本 | `ansible_facts['kernel']` |

> 请记住，当变量的值为哈希/hash/字典时，可以使用两种语法来获取值。参考上表中的示例：
>
> * `ansible_facts['default_ipv4']['address']` 可以写为 `ansible_facts.default_ipv4.address`
> * `ansible_facts['dns']['nameservers']` 也可以写为 `ansible_facts.dns.nameservers`

当在 playbook 中使用 fact 时，Ansible 会动态将 fact 的变量名替换为以下值：

```
- hosts: all
  tasks:
    - name: 打印各种 Ansible facts
    - debug:
        msg:
          {{ ansible_facts.fqdn }} 的默认 IPv4 地址
          是 {{ ansible_facts.default_ipv4.address }}
```

以下输出显示了 Ansible 如何查询被管理节点并动态获取系统信息以更新变量。Facts 也可以用于创建符合特定标准的动态主机组。

```
[user@demo ~]$ ansible-playbook playbook.yml

PLAY *********************************************************************
```

# TASK [Gathering Facts] *********************************************************************

ok: [demo1.example.com]

TASK [Prints Ansible Facts] ***********************************
ok: [demo1.example.com] = {
  "msg": "The default IPv4 address of demo1.example.com is\n  172.25.250.10"
}

PLAY RECAP
demo1.example.com : ok=2 changed=0 unreachable=0 failed=0

# 作为变量注入的 ANSIBLE FACTS

在 Ansible 5 之前，facts 是以带有 `ansible_indent_` 前缀的字符串注入到 `ansible_facts_variable` 部分的。例如，`ansible_facts['distribution']` fact 会被称为 `ansible_distribution`。

许多旧的 playbook 使用 facts 作为变量，而不是位于 `ansible_facts_variable` 命名空间下的语法。你可以使用即时命令（ad hoc command）运行 setup 模块来以这种形式打印所有 facts 的值。示例中，在被管理主机 demo1.example.com 上运行 setup 模块的即时命令。

```
[user@demo ~] ansible demo1.example.com -m setup
```

demo1.example.com : SUCCESS => {

"ansible_facts": {

    "ansible_all_ipv4_addresses": [

      "172.25.250.10"

    ],

    "ansible_all_ipv6_addresses": [

      "fe80:5054:ff:fe0a0"

    ],

    "ansible_apparmor": {

      "status": "disabled"

    },

    "ansible_architecture": "x86_64",

    "ansible_bios_date": "01/01/2011",

    "ansible_bios_version": "0.5.1",
