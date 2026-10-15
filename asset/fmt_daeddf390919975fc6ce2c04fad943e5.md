
# ~ check-enhancements gimp

## mp-gnic:
Installed: (none)
Candidate: `2.4.5-1`

## mp-getprint:
Installed: (none)
Candidate: `5.3.1-1`

## mp-help-ca:
Installed: (none)
Candidate: `2.8.2-1`

## mp-help-de:
Installed: (none)
Candidate: `2.8.2-1`

## mp-help-el:
Installed: (none)
Candidate: `2.8.2-1`

---

图 7：使用 `check-enhancements` 列出了增加了功能但运行并非必需的软件包。

严重漏洞总数：`2837`
具有补丁的数量：`205`
已准备好修复并等待上传的数量：`52`
被忽略的数量：`5`
关于当前稳定版本的数量：`267`
关于下一个发布版本的数量：`1345`

漏洞标签说明：

- `pending`（等待中）
- `patch`（补丁）
- `help`（帮助）
- `mono`
- `unreproducible`（不可复现）
- `security`（安全）
- `upstream`（上游）
- `it-strengthen-or-buster-ignore`（在 `strengthen` 中加强或在 `buster` 中忽略）

第二组标签指示了漏洞适用范围：`O` 代表旧版 (`essie` 此处原文为 essie，通常指 oldstable，但依原文保留 essie)，`S` 代表稳定版 (`stretch`)，`T` 代表测试版，`U` 代表不稳定版 (`sid`) 或 `E` 代表实验版。

图 8：通过 `popbugs`，你可以收集你系统中带有严重漏洞的最常用软件包。

### checkrestart

运行 `checkrestart`（图 10）可以找到系统更新添加了新库后哪些进程需要重启，因为这些进程仍在使用旧的已删除版本。它可以配合 `--package (-p)` 运行，这样它就只有15年的历史了（此处原文语义略显奇怪，但保留原意：意指该功能历史悠久或限制？原文说“only 15 years of history”，可能指包版本历史。保留原文）。同样，如果你以任何方式与软件包打交道，Debian Goodies 会熟悉你。如果你的 Debian 衍生包带有该包，将跟踪哪些相关产品可能是问题所在。没有选项——只有过去问题的历史。如果软件包安装引起的问题与其他几十个包有关，则这些信息可能不会被使用。注意，通用发布版被列为破坏了包（图 9）。

软件包文件的位置，或使用 `--all (-a)`，这可能会树目录中的文件中产生假阳报。此外，可以使用 `apt list -f=<file>` 过滤结果，创建一个从结果中的正则表达式列表。限制结果的其他方法是排除与 `--ignore-service (--MIME)` 或 `--conflicting-ids (-F=pkgID)` 关联的文件。输出长度可以通过 `--verbose` 选项或 `--t (-)` 进行限制。

# Info

- Debian Goodies: `https://packages.debian.in/search?keywords=debian-goodies&search-names=stable&section=all`

### 软件包工具箱

也许 Debian Goodies 相对不为人知的原因是它是

```bash
bb:@name=$S which --pkg-broke vim

libcrepc3:amd64
liblinux1:amd64
libattr1:amd64
libcl1:amd64
libgpm2:amd64
xd
gcc-base:amd64
libgcc1:amd64
vim
vim-common
vim-runtime
lib6:amd64
libintfo6:amd64
```

| 日期 | 时间 |
|---|---|
| Sat Sep 28 | 14:20:58 |
| Sat Sep 28 | 14:20:59 |
| Sat Sep 28 | 14:21:37 |
| Sat Sep 28 | 14:22:15 |
| Sat Sep 28 | 14:23:58 |
| Sat Sep 28 | 15:02:55 |
| Sat Sep 28 | 14:27:47 |
| Sat Sep 28 | 15:31:51 |
| Sat Sep 28 | 15:11:32 |
| Sat Sep 28 | 15:52:56 |
| Sat Feb 15 | 10:24:20 |

图 9：当使用 `--pkg-broke` 时，请记住通用发布版被列为破坏了包，即使那里无事可做。

```bash
root@name:~#checkrestart

Found 0 processes using old versions of upgraded files

(68 distinct programs)

(44 packages)
```

这 9 个包中似乎包含了用于重启它们的 `systemd` 服务定义或 `init` 脚本。
以下软件包似乎包含可重启其服务的定义：

| 服务 | PID / 路径 |
|---|---|
| `udev` | `459` / `/lib/systemd/udev` |
| `rpcbind` | `789` / `/sbin/rpcbind` |
| `udisks2` | `820` / `/usr/lib/udisks2/udisks` |

图 10：系统更新后，`checkrestart` 显示了哪些服务需要重启。

# 深度解析

## Charly 的专栏 - DenyHosts

系统管理员的日常工作：`DenyHosts`

### 智能门卫

当涉及到防御 `SSH` 端口 `22` 上不想要的登录测试时，`DenyHosts`，Charly 也喜欢通过 `DenyHosts` 而不是 `Fail2ban` 来登录自己（此处原文语义“login himself via DenyHosts”可能是指使用 DenyHosts 工具进行防护）。今天我想向大家介绍 `DenyHosts`，它的功能与 `Fail2ban` 相似，但有一个优势。`DenyHosts` 不释放 `IP` 地址这一点被许多用户视为一个缺点。对我来说，这取决于你对工具的个人偏好。我倾向于 `DenyHosts`。

接下来是配置中最重要的步骤：你需要将想要阻止的所有系统的 `IP` 地址添加到 `/etc/hosts.deny`。

```bash
sudo apt install denyhosts
```

为了满足你的需求，要安装 `DenyHosts`，输入：

```bash
sudo apt install denyhosts
```

在调整值以满足你的需求后，是时候考虑 `/etc/hosts` 了。

`DenyHosts` 将所有尝试写入 `/var/log/auth.log`（图 1）。你会看到阈值，`/etc/hosts.deny` 中的 `IP` 地址被输入系统并被 `iptables` 拦截。

```bash
Nov 3 22:21:48 lightpi1 sshd[7477]: Invalid user char from 10.0.0.233 port 5368

Nov 3322:221448pi1 sshd[7477]: pam_unix(sshd:auth): check pass; user unknown

Nov 3 22:21:48 lightpi1 sshd[7477]: pam_unix(sshd:auth): authentication failure;
logname= uid=0 eid=0 tty=ssh root from=10.0.0.253
```
