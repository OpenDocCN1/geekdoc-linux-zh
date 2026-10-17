
| UNIT | LOAD | ACTIVE | SUB |
| :--- | :--- | :--- | :--- |
| .slice | loaded | active | Root Slice |
| system-cups.slice | loaded | active | CUPS Slice |
| system-getty.slice | loaded | active | Slice /system/getty |
| system-modprobe.slice | loaded | active | Slice /system/modprobe |
| system-sshd-keygen.slice | loaded | active | Slice /system/sshd-keygen |
| system-systemd-fsck.slice | loaded | active | Slice /system/systemd-fsck |
| system-systemd-zram-setup.slice | loaded | active | Slice /system/systemd-zram-setup |
| system-telnet.slice | loaded | active | Slice /system/telnet |
| system.slice | loaded | active | System Slice |
| user-0.slice | loaded | active | User Slice UID 0 |
| user-1000.slice | loaded | active | User Slice of UID 1000 |
| user-983.slice | loaded | active | User Slice of UID 983 |
| user.slice | loaded | active | User and Session Slice |

图例：`LOAD` → 反映单元定义是否已正确加载。
`ACTIVE` → 高级单元激活状态，即 `SUB` 的泛化。
`SUB` → 低级激活状态，值取决于单元类型。
列出已加载单元文件使用 `systemctl list-unit-files`。

关于上述数据首先要注意的一点是，它显示了 0 (root) 和 1000 的用户 slice，这只显示了 slice 而不是属于每个 slice 的服务，因此从这些数据中显而易见的是，每当用户登录时都会创建一个 slice。这可以提供将该用户的所有任务作为一个单一 cgroup 实体进行管理的手段。

到为止一切顺利，但 cgroups 是分级的，所有的服务单元都作为这些 cgroups 之一的成员运行。查看该层级结构非常简单，使用一个旧命令和一个新命令。

## 实验 11-2：CGROUPS

`ps` 命令可以用于映射进程及其在 cgroup 层级结构中的位置。注意，必须使用 `ps` 命令指定所需的列。我大幅减少了此命令的输出量，但尽量保留了足够的内容，以便你可以获取在你的系统中可能发现的内容。

```
[root@studentvm1 ~] ps -eo pid,user,cgroup,args
```

| PID | USER | CGRO | COMMAND |
| :--- | :--- | :--- | :--- |
| 1154 | root | /system.slice/dbus | /usr/sbin/dbus |
| 1175 | root | /system.slice/sshd | /usr/sbin/sshd [listener] |
| 1442 | root | /user.slice/user-0.slice | sshhd [priv] |
| 1454 | root | /user.slice/user-0.slice | sshd@pts/0 |
| 1455 | root | /user.slice/user-0.slice | -bash |
| 1489 | root | /user.slice/user-0.slice | screen |
| 1490 | root | /user.slice/user-0.slice | SCREEN |
| 1494 | root | /user.slice/user-0.slice | /bin/bash |
| 4097 | root | /user.slice/user-0.slice | less |
| 2359 | root | /user.slice/user-0.slice | /bin/bash |
| 2454 | root | /user.slice/user-0.slice | sshd [priv] |
| 2456 | root | /user.slice/user-0.slice | sshd@pts/3 |
| 2457 | root | /user.slice/user-0.slice | -bash |
| 3014 | root | /user.slice/user-1000.slice | sshd [priv] |
| 3027 | root | /user.slice/user-1000.slice | sshd@pts/4 |
| 3028 | root | /user.slice/user-1000.slice | -bash |
| 1195 | root | /system.slice/colord | /usr/libexec/colord |

我们可以使用 `systemd-cgls` 命令查看整个层级结构，它更简单，因为不需要复杂的选项。我也缩短了这个树形视图。这是在 studentVM1 上完成的，大约 230 行；我的主工作站的数据量大约有 400 行。

```
[root@studentvm1 ~] systemd-cgls
```

Control group `/`:

 -.slice

  |-user.slice (#1323)

    |-user-0.slice (#6141)

      |-session-2.scope (#6421)

| | | |
| :--- | :--- | :--- |
| | → user.invocation_id: cfd09d6c3cd641d8988ddc23e22 | 916195 |
| | → trusted.invocation_id: cfd09d6c3cd641d8988ddc23e229 | 16195 |
| | | init.scope (#11061) | |
| | | 3017 /usr/lib/systemd/systemd --user | |
| | | 3019 (sd-pam) | |
| | session-5.scope (#11221) | |
| | → user.invocation_id: a8749076931f425d851c59fd | 956c4652 |
| | → trusted.invocation_id: a8749076931f425d851c59fd | 956c4652 |
| | | 3014 sshd: student [priv] | |
| | | 3027 sshd: student@pts/4 | |
| | <SNIP> | | |
| | session-7.scope (#14461) | | |
| | | user.invocation_id: f3e31059e0904df08d644856 aac639b | |
| | | trusted.invocation_id: f3e31059e0904df08d644856 aac639b | 314 |

## 第 11 章使用 Cgroups 进行资源管理

| | | 1429 lightdm --session-child 13 20 | | |
| | | 4133 /usr/bin/gnome-keyring-daemon --daemon --login | | |
| | | 4136 xfce4-session | | |
| | | 4300 /usr/bin/VBoxClient --clipboard | | | |
| | | 4301 /usr/bin/VBoxClient --clipboard | | | |
| | | 4315 /usr/bin/VBoxClient --seamless | | | |
| | | --4316 /usr/bin/VBoxClient --seamless | | | |
| | | --4321 /usr/bin/VBoxClient --draganddrop | | | |
| | | --4326 /usr/bin/VBoxClient --draganddrop | | | |
| | | --4328 /usr/bin/VBoxClient --msvga-session | | | |
| | | --4329 /usr/bin/VBoxClient --msvga-session | | | |
| | | --4340 /usr/bin/ssh-agent /bin/sh -c exec -l /bin/bash -c "startxfce4" | | | |
| | | --4395 /usr/bin/gpg-agent --sh --daemon | | | |
| | | --4396 xfm4 --display :0.0 --sm-client-id 2e797127-2992-4c6f-a503-2f64940ab467 | | | |
| | | --4409 xsettingsd --display :0.0 --sm-client-id 288d2bcdf-3264-4caf-ac93-bf55214688 | | | |
| | | --4412 xfce4-panel --display :0.0 --sm-client-id 2f57b404c-e176-4440-9830-4472e6757db0 | | | |
| | | --4416 Thunar --sm-client-id 21b424243-7ead-4e9e-9fc5-c3b1421df3fa-daemon | | | |

<SNIP>

此树视图显示了所有的用户和系统切片（slices）以及在每个 cgroup 中运行的服务和程序。注意，在上述列表 `user-1000.slice` 中，名为“scope”（作用范围）的单元将相关程序组合成一个可管理的单元。`user-1000.slice/session-7.scope` cgroup 包含了 TUI 桌面程序层次结构，从 LXDM 显示管理器会话开始，以及其所有的子任务，包括 Bash shell 和 thunar gui scope 单元。scope 单元不在配置文件中定义，而是作为启动一个或多个相关程序组的结果动态生成的。scope 单元不会创建或启动作为该 cgroup 一部分运行的进程。

scope 内的所有进程都是平等的，没有内部层级结构，scope 的生命始于第一个进程的创建，结束于最后一个进程的销毁。

在你的桌面上打开几个窗口，例如终端模拟器、Libreoffice 或你想要的任何程序，然后切换到一个可用的虚拟控制台并启动类似 `top` 或 `midnight commander` 的程序。在你的主机上运行 `systemd-cgroups` 命令，并注意整体层级结构和 scope 单元。

`systemd-cgroups` 命令比我找到过的任何其他命令都能对 cgroup 层级结构和构成它的单元提供最完整的表示。我更倾向于它对树结构的清晰整洁的表示。

3. 操作系统首先检查 `/etc/hosts` 文件以查看主机名是否存在其中。如果是，则将该条目的的 IP 地址返回给浏览器。如果没有，我们则进入下一步。在这种情况下，我们假设主机名不在 `/etc/hosts` 中。

4. 随后将主机名发送到 `/etc/resolv.conf` 中指定的第一个名称服务器。在这种情况下，第一个名称服务器的 IP 地址是我自己的内部名称服务器。对于本示例，我的名称服务器没有缓存 `www.example.net` 的 IP 地址，因此必须去更远的地方查找。因此，我们继续下一步。

5. 本地名称服务器将请求发送到远程名称服务器。这可以是两种目标类型之一，其中一种是转发器（forwarder）。转发器仅仅是另一个名称服务器，例如你互联网服务供应商（ISP）的服务器，或者像 Google（8.8.8.8 或 8.8.4.4）这样的公共名称服务器。另一种目标类型是顶级根服务器（top-level root name servers）。根服务器通常不会返回 `www.example.net` 的目标 IP 地址；它们返回的是该域的权威名称服务器（authoritative name server）。权威名称服务器是唯一有权维护和修改域名数据的服务器。

6. 本地名称服务器被配置为使用根服务器，因此 `.com` 顶级域的根服务器会返回 `example.net` 权威名称服务器的 IP 地址。该 IP 地址可能是三个（编写本文时）名称服务器之一：`ns1.redhot.com`、`ns2.redhot.com` 或 `ns3.redhot.com`。

7. 本地名称服务器将查询发送到权威名称服务器，后者返回 `www.example.net` 的 IP 地址。

8. 浏览器使用 `www.example.net` 的 IP 地址发送网页请求，该网页被下载到浏览器中。

这种名称搜索的一个重要副作用是，结果会被我的本地名称服务器缓存一段时间。这意味着下一次当我（或我网络上的任何人）访问 `example.net` 时，IP 地址可能已经存储在本地缓存中，从而避免了进行远程查找。

## resolv.conf

我们从探索 `/etc/resolv.conf` 文件开始，它是确定 `systemd-resolved.service` 如何确切工作的关键。

## 历史用法

该文件曾是一个 ASCII 纯文本文件，包含一个最多三个三个域名服务器的列表，用于将主机名解析为 IP 地址。它仍然可以那样的使用，但那将绕过 `systemd-resolved`。当然，这可能是一个预想要的结果，就像当 `NetworkManager` 接管此服务以及 `systemd-resolved` 首次引入并存在一些问题时对我来说一样。现在一切运行良好，所以在我的大大多数主机上，我已经好几年不需要那样做了。

`resolv.conf` 文件还包含了当主机名没有附加全限定域名名（FQDN）时需要搜索的域名。例如，一个全限定域名名将是 `host1.example.com`。这可以无问题地进行搜索。但假设我只使用主机名行而不使用域名名。在这种情况下，搜索的域名将附加到主机名之后。

一个典型的 `/etc/resolv.conf` 文件过去如图 12-1 所示。它是 `/etc` 中指向 `/run/NetworkManager/resolv.conf` 的链接，并包含了搜索域以及三个名称服务器的 IP 地址。

**图 12-1.** `systemd-resolved` 出现之前的典型 `/etc/resolv.conf` 文件

列表中的第一个名称服务器是我的内部名称服务器。第二和第三是备选的外部名称服务器。我使用 Google 服务器，是因为我信任它们是可靠的，并且其 DNS 数据库中拥有最新的信息——远比我 ISP 的多。无论我在特定时间使用哪家 ISP，我都会遇到很多中断、配置不当或未及时更新的名称服务器。这是我决定建立自己的内部名称服务器的原因之一。我们将在本章稍后的部分为我们的虚拟网络建立一个。

## 当前用法

`/etc/resolv.conf` 的当前用法是指指向存文件（stub file） `/run/systemd/resolve/stub-resolv.conf` 的符号链接（symlink），或者指向 `/run/systemd/resolve/resolv.conf`。所链接的文件决定了 `systemd-resolved` 应该如何处理名称解析请求。默认设置是 `/etc/resolv.conf` 链接到 `/run/systemd/resolve/stub-resolv.conf`，这使得可以使用 `systemd-resolved`，尽管 `systemd-resolved.service` 也必须处于运行状态。

### 实验 12-1: RESOLV.CONF

让我们先查看 `/etc/resolv.conf`。如你所见，它是指向 `/run/systemd/resolve/stub-resolv.conf` 的链接。

```
[root@testvml1 ~]# cd /etc
ls -l resolv.conf -> ../run/systemd/resolve/stub-resolv.conf
[root@testvml1 /etc]# cat resolv.conf
nameserver 127.0.0.53
options timeout:2 ndots:5
search example.com
```

```
[root@testvml1 /etc]# cat /run/systemd/resolve/stub-resolv.conf
nameserver 127.0.0.53
options timeout:2 ndots:5
```

`/etc/resolv.conf` 文件是指向存文件的链接。存文件决定了 `systemd-resolved` 应该如何处理名称解析请求。默认设置是 `/etc/resolv.conf` 链接到 `/run/systemd/resolve/stub-resolv.conf`，这可以使用 `systemd-resolved`，尽管 `systemd-resolved.service` 也必须处于运行状态。

## 名称服务策略

目前有三种策略可以将名称解析为 IP 地址。每种策略都有自己的工具、优势和用例。其中两种几乎不需要操作。其中一种 mDNS 非常“嘈杂”，并且会产生大量的流量。我们将在本节中探索三种策略：`/etc/hosts` 文件、多播 DNS (mDNS) 和 nss。

## /etc/hosts 文件
