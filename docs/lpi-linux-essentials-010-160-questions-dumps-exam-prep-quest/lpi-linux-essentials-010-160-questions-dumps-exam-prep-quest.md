
# LPI Linux Essentials 010-160 习题题库：最新版 LPI 010-160 考试备题指南

作者：Maxim Books

## 关于 Maxim Books

Maxim Books 是一家在美国德克萨斯州达拉斯市注册成立的图书出版公司，可以通过网络和本地访问，发布教育材料、认证指南书、诗歌以及许多其他类型的书籍。我们让作者和作家能够轻松地通过数字书籍+纸质传输的方式，在全球范围内专业地规划、分发、营销和销售他们的书籍。Maxim Books 成立于 2018 年，并向更多国家扩展其业务。

注意：问题的答案位于书末

## 第 1 题

硬盘驱动（HDD）和固态硬盘（SSD）之间的区别是什么？（选择两项）

- A. 硬盘具有电机和移动部件，而固态硬盘没有。
- B. 硬盘可能会因为物理损坏而故障，而固态硬盘不会故障。
- C. 固态硬盘存储的数据量可以是硬盘的许多倍。
- D. `/dev/sda` 是硬盘设备，而 `/dev/sda` 是固态硬盘。
- E. 固态硬盘提供存储数据的访问速度比硬盘更快。

## 第 2 题

反向 DNS 为 IP 地址分配主机名。IP 地址 `198.51.100.165` 的名称是如何存储在 DNS 服务器上的？

- A. 在 `165.100.51.198.ipv4.arpa` 的 A 记录中。
- B. 在 `165.100.51.198.in-addr.arpa` 的 PTR 记录中。
- C. 在 `198-51-100-165.rev.arpa` 的 RNAME 记录中。
- D. 在 `165.100.51.198.rev` 的 ARPA 记录中。
- E. 在 `arpa.in-addr.198.51.100.165` 的 REV 记录中。

## 第 3 题

`top` 命令可以显示哪些信息？

- A. 按大小排序的现有文件。
- B. 按 CPU 或 RAM 消耗排序的运行进程。
- C. 按登录次数排序的用户账户。
- D. 按成员数量排序的用户组。
- E. 按文件数量排序的用户账户。

## 第 4 题

下列哪种命令可以将 DNS 名称解析为 IP 地址？

- A. `dnsname`
- B. `dns`
- C. `query`
- D. `host`
- E. `iplookup`

## 第 5 题

下列输出中哪一个来自 `free` 命令？

A. `21:04:15 up 14 days, 7:43, 3 users, load average: 0.89, 1.00, 0.99`

B.
| avg-cpu: | %user | %nice | %system | %iowait | %steal | %idle |
|---|---|---|---|---|---|---|
| 34.04 | 0.03 | 13.88 | 1.06 | 0.00 | 50.99 |

C.
| Filesystem | Size | Used | Avail | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/mapper/vg_ssd-root | 25G | 20G | 3.6G | 85% | / |

D. `1.8M /tmp`

E.
| total | used | free | shared | buff/cache | available |
|---|---|---|---|---|---|
| Mem: | 16123128 | 12565680 | 2011624 | 412128 | 1545824 | 7180416 |

## 第 6 题

用户 `root` 的 UID 是什么？

- A. 1
- B. -1
- C. 255
- D. 65536
- E. 0

## 第 7 题

关于文件所有者，哪个说法是正确的？

- A. 每个文件都恰好属于一个用户和一个组。
- B. 文件所有者在访问文件时始终拥有完全权限。
- C. 拥有文件的用户必须是该文件组的成员。
- D. 当用户被删除时，所有由该用户拥有的文件都会消失。
- E. 文件所有者一旦分配给所有者就无法更改。

## 第 8 题

`/etc/passwd` 中存储了哪些信息？（选择三项）

- A. 用户的存储空间限制
- B. 数值用户 ID (UID)
- C. 用户名
- D. 加密密码
- E. 用户的默认 shell

## 第 9 题

下列哪些 `tar` 选项处理压缩？（选择两项）

- A. `-bz`
- B. `-z`
- C. `-g`
- D. `-j`
- E. `-z`

## 第 10 题

按下哪个键可以退出 `less`？

- A. `l`
- B. `x`
- C. `e`
- D. `q`
- E. `!`

## 第 11 题

下列哪个命令可以对 `export-logs` 命令的输出进行排序？

- A. `export-logs < sort`
- B. `export-logs > sort`
- C. `export-logs & sort`
- D. `export-logs | sort`
- E. `export-logs <> sort`

## 第 12 题

一个目录包含以下文件：

- `a.txt`
- `b.txt`
- `c.cav`

以下 shell 脚本的输出是什么？

```bash
for file in *.txt
do
echo $file
done
```

- A. `*.txt`
- B. `a b`
- C. `c.cav`
- D. `.txt`
- E. `a, b`

## 第 13 题

下列哪个命令递归搜索 `/home` 目录下所有以 `.txt` 结尾的文件？

- A. `find /home -type f`
- B. `find /home "*.txt"`
- C. `find /home -name "*.txt"`
- D. `find /home/*.txt`
- E. `/home`

## 第 14 题

当前目录包含以下内容：

```
-rw-r--r-- 1 root root Oct 27 10:00 file.txt
```

下列哪个命令会搜索：

- A. `*.txt`
- B. `.txt`
- C. `/home file.txt`
- D. `/home`
- E. `/txt`

## 第 15 题

什么是发行版（distribution）？

- A. Linux 内核。
- B. 软件包集合。
- C. 基于 Linux 的操作系统。
- D. 文件系统。
- E. 工具集。

## 第 16 题

哪些包管理工具用于 Red Hat 系统？

- A. `portage`
- B. `rpm`
- C. `apt-get`
- D. `dpkg`
- E. `yum`

## 第 17 题

为什么 cookie 被认为是危险的？

- A. Cookie 支持身份识别和跟踪。
- B. Cookie 任何人都可以访问。
- C. Cookie 占用大量存储。
- D. 删除 cookie 会丢失。
- E. Cookie 可能包含病毒和恶意软件。

## 第 18 题

哪些是云供应商提供的服务？（选择三项）

- A. 平台服务 (PaaS)
- B. 基础设施服务 (IaaS)
- C. 互联网服务 (IaaS)
- D. 图形服务 (GaaS)
- E. 软件服务 (SaaS)

## 第 19 题

提示符中的以下哪个字符表示 shell 以 root 权限运行？

- A. `!`
- B. `#`
- C. `*`
- D. `&`
- E. `$`

## 第 20 题

关于递归目录列表，哪个说法是正确的？

- A. 它包含子目录的内容。
- B. 它包含列出目录的权限。
- C. 它包含文件系统的细节，如节点。
- D. 它包含文件的所有权信息。
- E. 它包含每个文件的内容预览。

## 第 21 题

下列哪个目录包含安装软件包的信息、文档和示例配置？

- A. `/usr/share/doc/`
- B. `/etc/defaults/`
- C. `/var/info/`
- D. `/doc/`
- E. `/usr/examples/`

## 第 22 题

下列哪个命令将目录 `new/dir/` 添加到 `PATH` 环境变量？

- A. `$PATH=/new/dir: $PATH`
- B. `PATH=/new/dir: PATH`
- C. `export PATH=/new/dir: PATH`
- D. `export PATH=/new/dir: $PATH`
- E. `export PATH=/new/dir: $PATH`

## 第 23 题

用户当前位于 `/home/user/Downloads/` 并运行命令 `ls ../Documents/`

假设它存在，显示的是哪个目录的内容？

- A. `/home/user/Documents/`
- B. `/home/user/Documents/Downloads/`
- C. `/home/user/Downloads/Documents/`
- D. `/Documents/`
- E. `/home/user/Documents`

## 第 24 题

下列哪种协议用于自动 IP 地址配置？

- A. `NFS`
- B. `LDAP`
- C. `SMTP`
- D. `DNS`
- E. `DHCP`

## 第 25 题

以下哪个设备代表硬盘分区？

- A. `/dev/ttyS0`
- B. `/dev/sata0`
- C. `/dev/part0`
- D. `/dev/sda2`
- E. `/dev/sda/p2`

## 第 26 题

在 `/proc/` 目录下可以找到什么？

- A. 每个已安装的程序对应一个目录。
- B. 每个硬件设备对应一个设备文件。
- C. 每个现有账户对应一个文件。
- D. 每个运行中的进程对应一个目录。
- E. 每个运行的服务对应一个日志文件。

## 第 27 题

需要安装一个新的服务器来托管未来几年的服务。在此期间，该服务器应该从其使用的 Linux 发行版接收重要的安全更新。

以下哪些 Linux 发行版满足这些要求？（选择两个。）

- A. Ubuntu Linux LTS
- B. Fedora Linux
- C. Debian GNU/Linux Unstable
- D. Ubuntu Linux non-LTS
- E. Red Hat Enterprise Linux

## 第 28 题

如果以下目录位于其独立的专用文件系统中，则必须以读写权限挂载哪个？

- A. `/opt`
- B. `/lib`
- C. `/etc`
- D. `/var`
- E. `/usr`

## 第 29 题

应该更改文件 `doku.odt` 的所有者。新所有者名为 `tux`。哪个命令可以完成此更改？

- A. `chmod u=tux doku.odt`
- B. `newuser doku.odt tux`
- C. `chown tux doku.odt`
- D. `transfer tux: doku.odt`
- E. `passwd doku.odt:tux`

## 第 30 题

当文件所有者账户删除时，位于家目录之外的文件会发生什么？（选择两个。）

- A. 在文件系统检查期间，文件会被移动到 `/lost+found`。
- B. 文件将从文件系统中删除。
- C. 在列出文件详情时会显示原所有者的 UID。
- D. 用户 `root` 被设置为文件的新所有者。
- E. 文件的所有权和权限保持不变。

## 第 31 题

关于 Linux 文件系统中的链接，以下说法是正确的？

- A. 符号链接只能指向文件而不能指向目录。
- B. 硬链接只能指向目录而永远不能指向文件。
- C. 当符号链接的目标被移动时，链接会自动更新。
- D. 符号链接可以指向另一个文件系统上的文件。
- E. 只有 `root` 用户可以创建硬链接。

## 第 32 题

哪些文件是以下输出信息的来源？

`uid=1000 (bob) gid=1000 (bob) groups=1000 (bob), 10 (wheel), 150 (wireshark), 989 (docker), 1001 (libvirt)`

- A. `/etc/id`
- B. `/etc/passwd`
- C. `/etc/group`
- D. `/home/index`
- E. `/var/db/users`

## 第 33 题

`passwd` 命令可以完成以下哪些任务？（选择两个。）

- A. 修改用户的用户名。
- B. 修改用户的密码。
- C. 创建新的用户账户。
- D. 创建新的用户组。
- E. 锁定用户账户。

## 第 34 题

哪个命令仅显示文件名且不显示额外信息？

- A. `ls -a`
- B. `ls -lh`
- C. `ls -l`
- D. `ls -alh`
- E. `ls -nl`

## 第 35 题

以下哪个命令将 `data.csv` 文件的行按字母顺序排序？

- A. `a..z data.csv`
- B. `sort data.csv`
- C. `abc data.csv`
- D. `wc -s data.csv`
- E. `grep --sort data.csv`

## 第 36 题

以下哪个示例显示了 shell 脚本中 `for` 循环通用结构？

- A. `for *.txt as file => echo $file`
- B. `for *.txt (echo $)`
- C. `for file in *.txt do echo $i done`
- D. `for ls *.txt exec {} \;`
- E. `foreach @{file}{echo $}`

## 第 37 题

shell 脚本在成功执行后的返回值是什么？

- A. 1
- B. 0
- C. -1
- D. -255
- E. 255

## 第 38 题

关于典型的 shell 脚本，以下哪些说法是正确的？（选择两个。）

- A. 它设置了执行权限位。
- B. 它以双字符序列 `#!` 开头。
- C. 它位于 `/usr/local/scripts/`
- D. 它位于 `/etc/bash/scripts/`
- E. 它被编译为与机器架构兼容的二进制文件。

## 第 39 题

以下哪个命令提取压缩归档文件 `file1.tar.gz` 的内容？

- A. `tar -czf file1.tar.gz`
- B. `ztar file1.tar.gz`
- C. `tar -xzf file1.tar.gz`
- D. `tar --extract file1.tar.gz`
- E. `detar file1.tar.gz`

## 第 40 题

以下哪个命令可以在 `operating-systems.txt` 文件中找到包含 `linux` 术语的所有行，忽略大小写？

- A. `igrep linux operating-systems.txt`
- B. `less -i linux operating-systems.txt`
- C. `grep -i linux operating-systems.txt`
- D. `cut linux operating-systems.txt`
- E. `cut [Li] [Ii] [Nn] [Uu] [Xx] operating-systems.txt`

## 第 41 题

以下哪些程序是 Web 服务器？（选择两个。）

- A. Apache HTTPD
- B. Postfix
- C. Curl
- D. Dovecot
- E. NGINX

## 第 42 题

以下哪个 Linux 发行版源自 Red Hat Enterprise Linux？

- A. Raspbian
- B. openSUSE
- C. Debian
- D. Ubuntu
- E. CentOS

## 第 43 题

隐私浏览器窗口和普通 Web 浏览器窗口之间的区别是什么？（选择三个。）

- A. 隐私浏览器窗口不允许打印或存储网站。
- B. 隐私浏览器窗口不会持久化地存储 cookie。
- C. 隐私浏览器窗口不支持登录网站。
- D. 隐私浏览器窗口不会在浏览器历史中保留记录。
- E. 隐私浏览器窗口不会发送常规存储的 cookie。

## 第 44 题

在基于 Linux 的操作系统中安装新应用程序的首选来源是什么？

- A. 供应商的版本管理系统
- B. CD-ROM 光盘
- C. 发行版的包仓库
- D. 供应商的网站
- E. 零售店

## 答案

- 1. 正确答案: AE
- 2. 正确答案: B
- 3. 正确答案: B
- 4. 正确答案: D
- 5. 正确答案: E
- 6. 正确答案: E
- 7. 正确答案: A
- 8. 正确答案: BCE
- 9. 正确答案: BD
- 10. 正确答案: D
- 11. 正确答案: D
- 12. 正确答案: E
- 13. 正确答案: D
- 14. 正确答案: B
- 15. 正确答案: B
- 16. 正确答案: B
- 17. 正确答案: A
- 18. 正确答案: ABE
- 19. 正确答案: B
- 20. 正确答案: A
- 21. 正确答案: A
- 22. 正确答案: E
- 23. 正确答案: BDE
- 24. 正确答案: C
- 25. 正确答案: D
- 26. 正确答案: D
- 27. 正确答案: AE
- 28. 正确答案: D
- 29. 正确答案: C
- 30. 正确答案: CE
- 31. 正确答案: D
- 32. 正确答案: BC
- 33. 正确答案: CE
- 34. 正确答案: A
- 35. 正确答案: B
- 36. 正确答案: C
- 37. 正确答案: B
- 38. 正确答案: AE
- 39. 正确答案: C
- 40. 正确答案: C
- 41. 正确答案: AE
- 42. 正确答案: E
- 43. 正确答案: BDE
- 44. 正确答案: C
