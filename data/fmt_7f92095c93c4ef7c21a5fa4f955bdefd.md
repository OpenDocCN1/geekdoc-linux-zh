
- 8. [原文中第 8 项缺失]
- 9. [原文中第 9 项缺失]
- 10. [原文中第 10 项缺失]
- 11. [原文中第 11 项缺失]
- 12. [原文中第 12 项缺失]
- 13. [原文中第 13 项缺失]
- 14. [原文中第 14 项缺失]
- 15. [原文中第 15 项缺失]
- 16. [原文中第 16 项缺失]

# RHCSCA 示例考试 1 457

随后，在 `server1.example.com` 上执行以下命令应显示“Success!”测试页面（替换 `tester1` 的 IP 地址）：

```bash
# curl http://<ip_address_of_tester1>:8234
```

- 17. 以用户身份运行以下命令启动容器：

```bash
$ mkdir /html

$ podman run -d --name httpd \
-v /home/mike/html:/var/www/html \
-p 8080:8080 \
registry.access.redhat.com/ubi9/httpd-24
```

执行命令为容器服务生成系统配置：

```bash
$ podman generate systemd --name httpd --new-files
```

该命令会生成 `container-httpd.service`。接下来，将此文件复制到 `/home/mike/.config/systemd/user` 目录。如果该目录不存在，你需要创建它：

```bash
$ mkdir -p /home/mike/.config/systemd/user

$ cp container-httpd.service ~/.config/systemd/
```

之后，你需要停止并删除当前的 `httpd` 容器：

```bash
$ podman stop httpd

$ podman rm httpd
```

现在，是刷新系统并设置服务在系统启动时自动启动了：

```bash
$ systemctl --user daemon-reload

$ systemctl --user enable container-httpd.service

$ loginctl enable-linger
```

要验证所有设置是否正确，重启系统并检查容器正在运行：

```bash
$ systemctl --user status container-httpd.service

$ podman ps
```

- 18. 就像所有的红帽考试一样，确保你的修改在系统重启后依然至关重要。因此，重启系统并验证你的配置仍然完全可用。

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

# 附录 C

# RHCSAM 示例考试 2 答案

RHCSAM 示例考试 2 中的问题将帮助衡量你对书中涵盖材料的理解。正如引言所示，你应该能够在 3 小时内完成 RHCSAM 考试。然而，我们将本次实验的时间限制在 2.5 小时，以便让你在时间限制下工作。

RHCSAM 考试采用“闭卷”格式。尽管如此，你允许参考 Red Hat Enterprise Linux 计算机上提供的任何文档。虽然测试中心允许记录笔记，这些笔记不能带出考场。

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

# 460 附录 C RHCSA 示例考试 2 答案

在大多数情况下，没有单一的解决方案或方法来解决问题或安装服务。由于 Linux 中大量的选项，无法涵盖所有可能的场景。

对于后续练习，请避免使用生产计算机。这些练习中的任何微小错误都可能导致 Linux 无法启动。如果你无法通过这些练习提供的步骤进行恢复，你可能需要重新安装 Red Hat Linux。因此，你可能无法恢复保存在本地系统上的任何数据。

红帽采用电子化考试，这就是为什么书中的考试可以通过 McGraw Hill 伴随网站访问。该考试名为 RHCSampleexam2，并以 Microsoft Word 格式提供。关于将 RHEL 9 设置为适合练习考试的系统的说明，请参阅附录 A。

# RHCSA 示例考试 2 讨论

在此讨论中，我们将简要说明满足 RHCSA 示例考试 2 列出要求的方法。

- 1. 完成此任务，请查看第 5 章中的练习 5-2，“恢复根密码”。
- 2. 假设网络接口名为 `eth0`，执行以下命令：

```bash
# nmcli con eth0 ipv4.method auto

# nmcli con eth0 ipv4.gateway ""

# nmcli con eth0 ipv4.address ""

# nmcli down eth0

# nmcli up eth0

# hostname set-hostname server1.example.com
```

- 3. 完成此任务，请查看第 4 章中的练习 4-2，“将系统订阅到红帽订阅管理”。然后，使用以下命令安装 `tmux` RPM 包：

```bash
# dnf install tmux
```

- 4. 使用 `parted` 命令创建分区。假设你的硬盘为 `/dev/vda`，新分区为 3，且从 19GB 处有一些空闲。通过 `parted /dev/vda` 启动 `parted` 单元并输入

```text
(parted) unit mib

(parted) print

(parted) mkpart primary 19000MiB 19500MiB

(parted) quit
```

- 5. 运行以下命令格式化文件系统并创建挂载点：

```bash
# mkfs.xfs /dev/vda3

# mkdir /sysadmins
```

向 `/fstab` 文件添加条目。你将使用分区的 UUID（通用唯一标识符）进行此操作。

- 6. 使用 `parted` 命令创建分区。假设你的硬盘为 `/dev/vda`，新分区为 3，且从 19GB 处有一些空闲。通过 `parted /dev/vda` 启动 `parted` 单元并输入

```text
(parted) unit mib

(parted) print

(parted) mkpart primary 19000MiB 19500MiB

(parted) quit
```

- 7. 运行以下命令格式化文件系统并创建挂载点：

```bash
# mkfs.xfs /dev/vda3

# mkdir /sysadmins
```

- 8. 格式化文件系统：

```bash
# mkfs
```

向 `/fstab` 文件添加条目。你将使用分区的 UUID（通用唯一标识符）进行此操作。

- 1. 完成此任务，请查看第 5 章中的练习 5-2，“恢复根密码”。
- 2. 假设网络接口名为 `eth0`，执行以下命令：

```bash
# nmcli con eth0 ipv4.method auto

# nmcli con eth0 ipv4.gateway ""

# nmcli con eth0 ipv4.address ""

# nmcli down eth0

# nmcli up eth0

# hostname set-hostname server1.example.com
```

- 3. 完成此任务，请查看第 4 章中的练习 4-2，“将系统订阅到红帽订阅管理”。然后，使用以下命令安装 `tmux` RPM 包：

```bash
# dnf install tmux
```

- 4. 使用 `parted` 命令创建分区。假设你的硬盘为 `/dev/vda`，新分区为 3，且从 19GB 处有一些空闲。通过 `parted /dev/vda` 启动 `parted` 单元并输入

```text
(parted) unit mib

(parted) print

(parted) mkpart primary 19000MiB 19500MiB

(parted) quit
```

- 5. 运行以下命令格式化文件系统并创建挂载点：

```bash
# mkfs.xfs /dev/vda3

# mkdir /sysadmins
```

- 6. 使用 `parted` 命令创建分区。假设你的硬盘为 `/dev/vda`，新分区为 3，且从 19GB 处有一些空闲。通过 `parted /dev/vda` 启动 `parted` 单元并输入

```text
(parted) unit mib

(parted) print

(parted) mkpart primary 19000MiB 19500MiB

(parted) quit
```

- 7. 格式化文件系统：

```bash
# mkfs
```

- 8. 格式化文件系统：

```bash
# mkfs
```
