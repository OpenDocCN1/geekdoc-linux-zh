
在第 22 章中，你学习了如何向防火墙的区域（zones）中添加服务文件。`firewalld` 带有许多默认服务，不要将其与 `systemd` 混淆，它们是完全不同的。你可以使用 `firewall-cmd --get-services` 列出这些服务。此命令显示所有防火墙服务，这些服务以 XML 文件格式存储在 `/usr/lib/firewalld/services/` 和 `/etc/firewalld/` 目录下。

> 提示：在 RHEL 7 上，许多服务（如 `systemd`、`firewall`、`modprobe` 等）具有不应修改的默认配置文件。这些默认配置文件存储在 `/usr/lib` 目录中。永远不要更改它们，因为当产生配置文件的 RPM 包更新时，它们可能会被覆盖。自定义配置文件应该存储在 `/etc` 目录下，防火墙也是如此，它将自定义配置文件存储在 `/etc/firewalld`。这些自定义文件可能与 `/usr/lib/firewalld` 中的默认文件具有相同名称，但后者始终具有优先级。这不仅适用于 firewall，也适用于其他存储其服务文件的服务。

注：防火墙也是如此，它将自定义配置文件存储在 `/etc/firewalld`。这些自定义文件可能与 `/usr/lib/firewalld` 中的默认文件具有相同名称，但后者始终具有优先级。这不仅适用于 firewall，也适用于其他存储其服务文件的服务。

在某些情况下，你需要使用 `firewall-cmd` 允许端口。

在本章中，你将学习如何使用 firewall 来配置防火墙。但在考试中，红帽期望你创建一个配置。他们通常不会告诉你是如何做，只要求它能正常工作。所以，如果你能用 `iptables` 完成，那没问题。

# 创建防火墙

## 32.1 创建防火墙服务

1. 使用 `cp /usr/lib/firewalld/services/ssh.xml /etc/firewalld/services/` 基于现服务文件文件。

2. 打开 `/etc/firewalld/services/ssh.xml`。它应该显示内容（见 3.11）

```
<?xml version="1.0" encoding="--8
<service>
  <short>SSH</short>
  <description>Secure Shell (SSH) 是一种用于远程登录和执行命令的协议。它提供了加密通信。如果你计划通过防火墙接口通过 SSH 访问机器，请启用此选项。你需要安装 openssh-server 包使此选项有效。</description>
  <port protocol="tcp" port="22"/>
</service>
```

3. 在服务文件中，将设置为 22 的端口更改为新端口（2022）。

4. 修改描述显示这是一个修改过的服务文件。

5. 保存更改，并使用 `mv /etc/firewalld/services/ssh.xml /etc/firewalld/services/ssh-custom`。

6. 输入 `firewall-cmd --get-services`。注意你还没有看到新的服务文件。

7. 输入 `firewall-cmd --reload` 并重复 `firewall-cmd --get-services`。你会看到新的服务文件。

8. 输入 `firewall-cmd --add-service ssh-custom --permanent`，然后执行 `firewall-cmd --reload`。

9. 输入 `firewall-cmd --list-services`。你会看到新服务已添加到默认区域。

10. 注意，这个练习展示了如何创建一个防火墙服务。为了让进程在新的端口可用，还要修改进程配置。阅读第 39 章“管理 SSH”，获取更多关于如何对 ssh 服务进行操作的详细信息。

# 配置防火墙富规则

到为止，你一直在使用防火墙服务。虽然很方便，但防火墙服务提供的选项有时有限。这就是为什么防火墙也提供了允许流量的替代解决方案。目前有两种解决方案：

- 直接规则允许管理员在防火墙配置中添加详细的手写规则。它们提供了高级功能，但较难管理。它们使用的语法类似于 `iptables` 语法，允许管理员以类似 `iptables` 的方式操作防火墙。对于 RHCE 考试，你不需要知道如何创建直接规则。

- 富规则为管理员提供了一种易于使用的表达式语言，用于定义无法默认防火墙语法创建的自定义规则。

> 提示：不要在直接规则上浪费时间；在 RHCE 考试中你只需要知道如何配置富规则。

# 富规则语法

富规则用于创建允许/拒绝规则，但具有高级选项，例如：

* 日志配置

* 端口转发

* 伪装

* 速率限制

* 允许/拒绝来自特定区域的连接

富规则（rich rule）的基本语法如下：

+ Rule
  - [source] [destination]
  - [service|port|protocol|icmp-block|masquerade|forward-port]
  - [log] [audit]
  - [accept|reject|drop]

> 在你尝试记忆富规则语法之前，请查看 `man 5 firewall.richlanguage`。该帮助页包含了如何创建富规则的良好示例，这将帮助你在考试时轻松地找到正确的语法。

## 排序

在使用富规则时，很容易创建冲突的规则。例如，你可能拒绝整个网络的访问，但又允许访问该网络中的一个特定节点。由于可能会创建冲突规则，在处理富规则时，顺序也变得重要。区域内的基本排序规则如下：

+ 1. 直接规则
2. 端口转发和伪装规则
3. 日志规则
4. 允许规则
5. 拒绝规则

通常情况下，不会被任何规则匹配的规则将被拒绝，但这取决于取决于默认区域的配置。例如，如果使用了信任区域（trusted zone），则不匹配任何项的数据包将允许允许。

## 管理富规则

在使用富规则时有四种基本操作。表 32.2 描述了这些操作。

## 710 Red Hat RHCSA/RHCE 7 指南

## 表 32.2 富规则基本操作

| 操作 | 解释 |
|--- |--- |
| `--add-rich-rule='<RULE>'` | 将 `<RULE>` 添加到默认区域或指定的区域。 |
| `--remove-rich-rule='<RULE>'` | 从默认区域或指定的区域移除 `<RULE>`。 |
| `--query-rich-rule='<RULE>'` | 查询 `<RULE>` 是否已添加到某个区域。如果规则存在则返回 0，如果不存在则返回 1，且不提供任何详细信息。 |
| `--list-rich-rules` | 列出默认区域或作为参数指定的区域的所有富规则。 |

> 提示：为了方便测试富规则，你可以带超时时间将规则添加到运行时配置中。一旦超时时间过去，该富规则将被自动移除。这确保了你在对富规则配置犯错误后不会被锁在外部，这在在远程服务器上配置防火墙时非常有用。要为富规则添加超时时间，请在 `firewall-cmd` 规则末尾添加 `--timeout=XX`。

为了帮助你学习富规则语法，练习 32.2 将带你完成向区域添加富规则的过程。请注意，没有任何规则被设置为 `--permanent`，因为这个练习仅用于演示富规则的工作原理。

## 练习 32.2 使用富规则

+ 1. 从 root shell，输入 `firewall-cmd --zone=dmz --add-rich-rule='rule family=ipv4 source=10.0.0.0/32 reject' --timeout=60`。

2. 输入 `firewall-cmd --list-all --zones=dmz` 以验证规则是否已成功添加。

3. 现在输入 `firewall-cmd --add-rich-rule='service name=http log value=3/m accept' --zone=dmz`。

4. 再次输入 `firewall-cmd --list-all --zone=dmz` 以验证规则是否已成功添加。注意你在练习第 1 步中添加的规则现在消失了。

5. 输入 `firewall-cmd --add-rich-rule='protocol icmp accept' --zone=dmz`。此规则允许所有互联网控制消息协议（ICMP）流量进入非军事化区（DMZ）。

## 第32 章：高级防火墙配置
