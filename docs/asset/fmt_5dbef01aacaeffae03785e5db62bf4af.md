
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

- 10. 安装 `autofs` `nfs-utils` 软件包：

```bash
# dnf install autofs nfs-utils
# systemctl enable autofs --now
```

然后，将以下行添加到 `/etc/automisc`:
`dvd-fstype=iso960,ro,nosuid,nodev ://dev/cdrom`

# 464 附录 C RHCSA 样例考试 2 解

创建挂载 NFS 共享的目录：

```bash
# mkdir /mnt/nfs
```

然后，将以下行添加到 `/etc/fstab` 中（替换 `tester1example.com` 的 IP 地址）：

```
<ip_of_tester1>/exports/nfshare /mnt/nfs nfs defaults 0 0
```

要挂载文件系统，运行：

```bash
# mount /mnt/nfs
```

- 15. 以 `server1.example.com` 上用户 `mark` 的身份，生成一个长度为 4096 位的 RSA SSH 密钥对：

```bash
$ ssh-keygen -t rsa -b 4096
```

现在，在 `tester1.example.com` 上创建用户：

```bash
# useradd mike
# echo "changeme" | passwd --stdin mike
```

然后，在 `server1.example.com` 上，将公钥拷贝到目标服务器 `tester1.example.com`。你可以使用 `ssh-copy-id` 命令完成此（替换 `tester1example.com` 的 IP 地址）：

```bash
$ ssh-copy-id mike@ip_of_tester1
```

系统将提示你输入 `tester1.example.com` 上 `mike` 的密码以允许拷贝操作。现在，来自 `server1.example.com` 的用户 `mark` 应该能够通过密钥认证 SSH 登录 `tester1.example.com`。当你启动 SSH 连接时，将提示你输入密钥的短语。

- 16. 确保已安装 `tuned` RPM 且服务正在运行。如果没有运行，请安装该包、启动服务并将其设置为自自启动：

```bash
# dnf install tuned
# systemctl start tuned
# systemctl enable tuned
```

现在，要激活 `virtual-guest` 配置文件，请使用 `tuned-adm` 工具：

```bash
# tuned-adm profile virtual-guest
```

要验证该配置，可以使用以下命令：

```bash
# tuned-adm active
```

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

# RHCSA 样例考试 2 讨论 465

- 17. 以用户 `bill` 的身份，创建一个包含以下内容的 `Containerfile`：

```dockerfile
# 使用 Red Hat UBI 9 镜像作为基础镜像
FROM registry.access.redhat.com/ubi9/ubi:latest
# 执行 "sleep id" 命令
CMD ["sleep", "id"]
```

使用以下命令构建镜像：

```bash
$ podman build -t ubi-test
```
