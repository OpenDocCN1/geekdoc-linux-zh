
单个网络设备在 `/etc/sysconfig/network-scripts` 目录中配置。

网络配置工具包括基于控制台的 `system-config-network` 命令和网络管理器中的“网络连接”工具。

主机名配置文件包括 `/etc/nsswitch.conf`、`/etc/hosts` 和 `/etc/resolv.conf`。

![](img/9139201cfcaf4292284a0eed074928e5_191_0.png)

## 自测

以下问题将帮助你衡量对本章所介绍材料的理解程度。由于 Red Hat 考试中没有选择题，本书中也没有选择题。这些问题专门测试你对本章的理解。在 Red Hat 考试中，重要的是取得结果，而不是死记硬背琐碎的知识。

### Shell

- 1. 默认 Linux Shell 的名称是什么？
- 2. 从 GUI，什么键组合切换到虚拟控制台 3？

### 标准命令行工具

- 3. 创建 `/abc/def/ghi/jkl` 系列目录的单个命令是什么？
- 4. 表示当前用户主目录的符号是什么？

### 文本文件管理

- 5. 列出 `/var/log/messages` 文件最后十行的命令是什么？
- 6. 从 `/var/log/dmesg` 文件返回包含术语 Linux 的行的命令是什么？

### 本地在线文档

- 7. 搜索 man 手册数据库中引用 `passwd` 命令和配置文件的手册的命令是什么？
- 8. 如果存在假设的 `abcde` 命令和文件的 man 手册，且位于第 5 节和第 8 节，输入确保调出第 5 节 man 手册的命令？

### 网络基础

- 9. 在 IPv4 地址中，网络地址为 `192.168.100.0`，广播地址为 `192.168.100.255`，可分配的 IP 地址范围是什么？
- 10. 根据问题 9 中描述的地址，什么命令将 IPv4 地址 `192.168.100.100` 分配给网络设备 `eth0`？

### 网络配置与故障排除

- 11. 包含本地系统主机名的配置文件的完整路径是什么？
- 12. 本地系统第一个以太网适配器相关配置文件的完整路径是什么？

## 实验问题

其中一些实验涉及配置练习。你应该只在测试机器上进行这些练习。假设你是在诸如 KVM 之类的虚拟机上运行这些练习。Red Hat 以电子方式提供考试。因此，本章及以后章节的大多数实验都可以在随书附带的 CD 上找到，位于 `Chapter3/` 子目录中。如果尚未在系统上设置 RHEL 6，请参阅第 1 章以获取安装说明。每个实验的答案在填空题的自测答案之后。

## 自测答案

### Shell

- 1. 默认的 Linux Shell 是 `bash`，也称为 Bourne-Again shell。
- 2. 从 GUI 切换到虚拟控制台 3 的键组合是 `CTRL-ALT-F3`。

### 标准命令行工具

- 3. 创建 `/abc/def/ghi/jkl` 系列目录的单个命令是 `mkdir -p /abc/def/ghi/jkl`。
- 4. 表示当前用户主目录的符号是波浪号 (`~`)。

### 文本文件管理

- 5. 列出 `/var/log/messages` 文件最后十行的命令是 `tail -n10 /var/log/messages`。
- 6. 从 `/var/log/dmesg` 文件返回包含术语 Linux 的行的命令是 `grep Linux /var/log/dmesg`。其他变体也是可以接受的，例如 `cat /var/log/dmesg | grep Linux`。

### 本地在线文档

- 7. 搜索 man 手册数据库中引用 `passwd` 命令和配置文件的手册的命令是 `whatis passwd`。`apropos` 和 `man -k` 命令更进一步，因为它们列出命令或描述中包含文本 "`passwd`" 的 man 手册。
- 8. 调出假设的 `abcde` 命令和文件的第 5 节 man 手册的命令是 `man 5 abcde`。

### 网络基础

- 9. 所提及 IPv4 网络中可分配的 IP 地址范围是 `192.168.100.1` 到 `192.168.100.254`。
- 10. 根据问题 9 中描述的地址，将 IPv4 地址 `192.168.100.100` 分配给网络设备 `eth0` 的命令是 `ifconfig eth0 192.168.100.100`。

### 网络配置与故障排除

- 11. 包含本地系统主机名的配置文件完整路径是 `/etc/hosts`。
- 12. 本地系统第一个以太网适配器相关配置文件的完整路径是 `/etc/sysconfig/network-scripts/ifcfg-eth0`。如果你习惯使用 Network Connections 工具配置网卡，`ifcfg-System_eth0` 也是可以接受的。

## 实验答案

### Lab 1

本实验测试了通过最不起眼的设置停用网络的情况，即 `/etc/sysconfig/network` 文件中的 `NETWORKING` 指令。当设置为 `no` 时，该设置会停用系统上的网络。其他内容没有改变；特定网卡的 IP 地址信息仍然正确。当然，你仍然可以通过其他方式激活网络，但除非在所提及的文件中 `NETWORKING=yes`，否则此类更改不会在重启后保留。

本实验使用的脚本将 `/etc/sysconfig/network` 的原始副本保存到 `/root/backup` 目录中。现在实验已完成，你可以将该文件恢复到其原始位置。请注意，不可变标志已应用于复制的文件；要从 `/root/backup` 目录中删除它，你必须先使用 `chattr -i` 命令移除不可变标志。

### Lab 2

本实验为第一个以太网适配器 `eth0` 设置了无效的 IP 地址配置。第 1 章中配置的系统的标准基于 `192.168.122.0/24` 网络。`/etc/sysconfig/network-scripts` 目录中的配置文件可能因适配器的配置方式而名称略有不同。该目录中的原始文件已移动到 `/root/backup` 目录。如果重建该配置文件的工作失败，请从该 `/root/backup/` 目录恢复原始配置文件。

请注意，不可变标志已应用于复制的文件；要从 `/root/backup` 目录中删除它，你必须先使用 `chattr -i` 命令移除不可变标志。事实上，在 Lab 3 正常工作之前，你必须运行以下命令：

```
# chattr -i /root/backup/*
```

### Lab 3

本实验停用系统上的第一个以太网设备，如果该设备具有默认的 `eth0` 设备文件名，则有效。它也应该有效，如果你运行了 Network Manager Network Connections 工具且没有更改太多默认值，因为 Ch3Lab3 脚本也会停用 `System_eth0` 设备文件。

### Lab 4

本实验替换了 `/etc/resolv.conf` 文件。如果本地网络已使用 `192.168.1.111` IP 地址上的 DNS 服务器，本实验不应引起任何问题。该文件的原始版本已移动到 `/root/backup` 目录。如果重建该配置文件的工作失败，请从该备份目录恢复原始配置文件。

### Lab 5

在本实验中，你将在第 1 章中描述的每个系统上设置 `/etc/hosts` 文件。除 Network Manager 添加的本地系统设置外，所有三个系统上的 `/etc/hosts` 中的数据可能相同。具体来说，该文件应包含以下条目：

```
192.168.122.50  server1 server1.example.com
192.168.122.150  tester1 tester1.example.com
192.168.100.100  outsider1 outsider1.example.org
```

系统位于不同的 IP 网络并不重要。只要系统之间存在路由路径，每个 `/etc/hosts` 文件中的这些数据就会生效。只要数据一致，与 Network Manager 插入的数据重复也不是问题。事实上，可以为一个 IP 地址设置多个名称；例如，如果我在 `192.168.122.50` 系统上设置一个 Web 服务器，我可以在 `/etc/hosts` 中添加以下条目。

```
192.168.122.50  www.example.com
```

### Lab 6

前四行来自 `eth0` 网卡的原始配置。虽然 `DEVICE`、`HWADDR`、`NM_CONTROLLED` 和 `ONBOOT` 指令相关的值没有改变，但 RHEL 6 安装提供的格式是不同的。

### Lab 7

如果你使用过 Network Connections 工具，可能存在 `ifcfg-System_eth0` 文件代替 `ifcfg-eth0` 文件。`system-config-network` 工具仍然可以处理该文件。只需相应地进行替换即可。一定要学习 `USERCTL`、`BOOTPROTO` 和 `DNS1` 等指令相关的设置。

![](img/9139201cfcaf4292284a0eed074928e5_197_0.png)

# 4. RHCSA 级别的安全选项

## 认证目标

### 4.01 基本文件权限
