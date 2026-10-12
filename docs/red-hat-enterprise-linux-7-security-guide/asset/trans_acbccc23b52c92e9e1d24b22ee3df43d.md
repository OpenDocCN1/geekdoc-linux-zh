

- [7] “数据加密标准。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Data_Encryption_Standard
- [8] “数据加密标准。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Data_Encryption_Standard
- [9] “公钥加密。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Public-key_cryptography
- [10] “公钥加密。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Public-key_cryptography
- [11] “公钥加密。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Public-key_cryptography
- [12] “公钥加密。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Public-key_cryptography
- [13] “公钥加密。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Public-key_cryptography
- [14] “迪菲-赫尔曼（Diffie-Hellman）。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Diffie-Hellman
- [15] “迪菲-赫尔曼（Diffie-Hellman）。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Diffie-Hellman
- [16] “迪菲-赫尔曼（Diffie-Hellman）。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Diffie-Hellman
- [17] “迪菲-赫尔曼（Diffie-Hellman）。” *维基百科*。2009年11月14日  
  http://en.wikipedia.org/wiki/Diffie-Hellman
- [18] “数字签名算法（DSA）。” *维基百科*。2010年2月24日  
  http://en.wikipedia.org/wiki/Digital_Signature_Algorithm
- [19] “TLS/SSL。” *维基百科*。2010年2月24日  
  http://en.wikipedia.org/wiki/Transport_Layer_Security
- [20] “Cramer-Shoup 加密系统。” *维基百科*。2010年2月24日  
  http://en.wikipedia.org/wiki/Cramer-Shoup_cryptosystem
- [21] “ElGamal 加密” *维基百科*。2010年2月24日  
  http://en.wikipedia.org/wiki/ElGamal_encryption

# 附录 B. 审计系统参考

## B.1. 审计事件字段

表 B.1 “事件字段” 列出了当前支持的所有审计事件字段。事件字段是审计日志文件中等号前面的值。

### 表 B.1. 事件字段

| 事件字段 | 说明 |
| :--- | :--- |
| a0, a1, a2, a3 | 记录系统调用的前四个参数，以十六进制编码表示。 |
| acct | 记录用户账户名称。 |
| addr | 记录 IPv4 或 IPv6 地址。此字段通常跟随主机名之后，包含主机名解析到的地址。 |
| arch | 记录系统 CPU 架构的信息，以十六进制编码表示。 |
| audit | 记录审计用户 ID。此 ID 在用户登录时分配给用户，并由每个进程继承，即使用户身份发生变化（例如，使用 `su - john` 切换用户账户）。 |
| capability | 记录用于设置特定 Linux 能力位的位数。有关 Linux 能力的更多信息，请参阅 `capabilities(7)` 手册页。 |
| cap_fe | 记录与设置有效文件系统基础能力位相关的数据。 |
| cap_fi | 记录与设置继承的文件系统基础能力相关的数据。 |
| cap_fp | 记录与设置允许的文件系统基础能力相关的数据。 |
| cap_fver | 记录文件系统基础能力的版本。 |
| cap_pe | 记录与设置有效进程基础能力相关的数据。 |
| cap_pi | 记录与设置继承的进程基础能力相关的数据。 |
| cap_pp | 记录与设置的允许进程基础能力相关的数据。 |
| cgroup | 记录在生成审计事件时包含该进程的 cgroup 路径。 |
| cmd | 记录执行的完整命令行。这对于 shell 解释器很有用，其中 `exe` 字段记录例如 `/bin/bash` 作为 shell 解释器，而 `cmd` 字段记录执行的其余命令行，例如 `hello world.sh --help`。 |
| comm | 记录执行的命令。这对于 shell 解释器很有用，其中 `exe` 字段记录例如 `/bin/bash` 作为 shell 解释器，而 `comm` 字段记录执行的脚本名称，例如 `hello world.sh`。 |
| cwd | 记录调用系统调用所在的目录路径。 |
| data | 记录与 TTY 记录关联的数据。 |
| dev | 记录包含事件记录中文件或目录的设备的主次 ID。 |
| devmajor | 记录主要设备 ID。 |
| devminor | 记录次要设备 ID。 |
| egid | 记录启动所分析进程的用户的有效组 ID。 |
| euid | 记录启动所分析进程的用户的 有效用户 ID。 |
| exe | 记录用于启动所分析进程的可执行文件路径。 |
| exit | 记录系统调用返回的退出代码。此值因系统调用而异。您可以使用以下命令将其值解释为人类可读的等价值：`ausearch --interpret --exit exit_code` |
| family | 记录使用的地址协议类型，即 IPv4 或 IPv6。 |
| filetype | 记录文件类型。 |
| flags | 记录文件系统名称标志。 |
| fsgid | 记录启动所分析进程的用户的文件系统组 ID。 |
| fsuid | 记录启动所分析进程的用户的文件系统用户 ID。 |
| gid | 记录组 ID。 |
| hostname | 记录主机名。 |
| icmp type | 记录接收到的互联网控制消息协议（ICMP）包类型。包含此字段的审计消息通常由 `iptables` 生成。 |
| id | 记录被更改的账户的用户 ID。 |
| inode | 记录与审计事件中记录的文件或目录关联的 inode 号。 |
| inode_gid | 记录 inode 所有者的组 ID。 |
| inode_uid | 记录 inode 所有者的用户 ID。 |
| items | 记录附加到此记录的路径记录数量。 |
| key | 记录与在审计日志中生成了特定事件的规则关联的用户定义字符串。 |
| list | 记录审计规则列表 ID。以下是已知 ID 的列表：<br>- **0 - user**<br>- **1 - task**<br>- **4 - exit**<br>- **5 - exclude** |
| mode | 记录文件或目录权限，以数字记法编码。 |
| msg | 记录记录的时间戳和唯一 ID，或由内核或用户空间应用程序提供的各种特定事件的 `<name>=<value>` 对。 |
| msgtype | 记录基于用户的 AVC 拒绝情况下返回的消息类型。消息类型由 D-Bus 确定。 |
| name | 记录作为参数传递给系统调用的文件或目录的完整路径。 |
| new-disk | 记录分配给虚拟机的新磁盘资源名称。 |
| new-mem | 记录分配给虚拟机的新内存资源量。 |
| new-vcpu | 记录分配给虚拟机的新虚拟 CPU 资源数量。 |
| new-net | 记录分配给虚拟机的新网络接口资源的 MAC 地址。 |
| new_gid | 记录分配给用户的组 ID。 |
| ouuid | 记录登录以访问系统（例如，相对于使用 SU）并启动目标进程的用户 ID。此字段专属于类型为 OBJ_PID 的记录。 |
| ocomm | 记录用于启动目标进程的命令。此字段专属于类型为 OBJ_PID 的记录。 |
| opid | 记录目标进程的进程 ID。此字段专属于类型为 OBJ_PID 的记录。 |
| oses | 记录目标进程的会话 ID。此字段专属于类型为 OBJ_PID 的记录。 |
| ouid | 记录目标进程的真实用户 ID |
| obj | 记录对象的 SELinux 上下文。对象可以是文件、目录、套接字，或接收主体动作的任何内容。 |
| objtype | 记录系统调用上下文中 PATH 记录对象的意图。 |
| obj_gid | 记录对象的组 ID。 |
| obj_lev_high | 记录对象的高 SELinux 级别。 |
| obj_lev_low | 记录对象的低 SELinux 级别。 |
| obj_role | 记录对象的 SELinux 角色。 |
| obj_uid | 记录对象的 UID |
| obj_user | 记录与对象关联的用户。 |
| ogid | 记录对象所有者的组 ID。 |
| old-disk | 当新磁盘资源分配给虚拟机时，记录旧磁盘资源的名称。 |

