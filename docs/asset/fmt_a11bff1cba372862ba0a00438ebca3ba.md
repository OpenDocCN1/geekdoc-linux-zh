
# www.united.com 额外内容

提示

## 恢复访问

如果对你想要计算机的访问被切断，可以检查以下几点来纠正该问题：

- `/etc/hosts.deny`：检查计算机 IP 地址是否被误添加到此文件中。这会导致网络服务被拒绝。
- `/var/portsentry/portsentry.block`：检查是否误添加了该文件的计算机 IP 地址条目。
- `route`：使用 `route` 命令查看是否阻止了主机。
- `ipchains`：使用 `-l` 命令查看是否创建了防火墙。

![](img/0823b2119053dace3be4993846bb1ee1_617_0.png)

为了确保访问不再被切断，你可以将计算机地址添加到 `portsentry.ignore`。

## 获取更多信息

### CERT

CERT 协调中心是卡内基梅隆大学软件工程研究所（SII）的一部分。CERT 的全称为计算机响应小组（Computer Response Team）。它于1988年由 DARPA（国防高级计划署）应对著名的蠕虫病毒而创立。自1988年以来，CERT 扩大了其目标，包括：

- 协助创建应急小组。
- 在响应大规模事件时协调团队的努力。
- 为应急专业人员提供培训。
- 研究漏洞原因、预防措施以及大型网络的生存能力。

作为这些工作的一部分，CERT 发布公告来警告新发现的问题，并解释如何保护它们。这些公告可以在 CERT 网站获取。你也可以通过订阅 CERT 邮件列表将 CERT 公告发送到你的电子邮箱。

要订阅 CERT 邮件列表，请向 `majordomo@cert.org` 发送邮件。在正文中输入：

```
subscribe cert-advisory
```

要从列表中移除你的，请向 `majordomo@cert.org` 发送邮件。在正文中输入：

```
unsubscribe cert-advisory
```
