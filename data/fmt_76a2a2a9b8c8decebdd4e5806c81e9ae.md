
SetUID 程序是其权限中设置了特殊属性（标记）的可执行文件，允许用户在执行文件所有者的环境中运行该程序。这使得管理员可以将选定的应用程序、程序或文件以更高的权限提供给普通用户，而无需赋予任何管理权限。此类程序的一个例子是 `ping`。因为创建原始数据包被限制为 `root` 用户（创建原始数据包的能力允许攻击在包内注入恶意载荷），因此 `ping` 应用程序必须在启用 SetUID 并将用户设置为 `root` 的情况下运行。因此，例如，尽管你启动了 `ping` 程序，该程序在 `root` 用户的环境下运行，目的是向网络中放置互联网控制消息协议（ICMP）包。此示例中的 `ping` 工具被称为“Setroot”。需要以 `root` 权限运行的程序开发者有义务额外注重安全。普通用户不应该能够通过使用此类程序在系统上执行危险的操作。这意味着需要在程序中编写检查逻辑，并必须仔细移除潜在漏洞。理想情况下，这些程序应该是短小且用途单一的。这有助于评估代码是否存在可能损害系统或允许用户获得不应拥有的权限的漏洞。

## 第 15 章 本地安全 327

从日常角度来看，让系统中尽可能少保留 SetUID root 程序是管理员的利益所在。这里的风险平衡在于用户对功能/服务的可用性与可能发生坏事的风险之间的平衡。对于 `mount`、`traceroute` 和 `su` 等一些常用程序，考虑到它们为系统带来的价值，风险很低。众为人知的 SetUID 程序（如 X Window System）构成了低到中等的风险；鉴于 X Window System 的暴露面，它不太可能是任何问题的根源。如果你运行的是纯服务器环境且不需要 X Window System，那么将其移除也绝无害处。

对于由 Web 服务器执行的 SetUID 程序几乎总是一件坏事。使用此类应用程序时要谨慎，并寻找替代方案。其暴露性大得多，因为网络输入（可能来自任何地方）可能会触发此程序并影响其执行。如果你发现必须以 `root` 权限 SetUID 运行运行某个程序，另一种替代方案是查找是否可以在 `chroot` 环境中运行该程序（在本章稍后的“chroot”部分进行讨论）。

> SetUID 程序的替代方案是内核提供的能力（capabilities）功能。例如，可以通过为流行的 `ping` 分配其运行所需的精确能力（`CAP_NET_RAW`），使其变为非 SetUID。查看以下 man页以了解更多关于能力的信息：`getcap`, `setcap`, `capabilities`, 和 `getcaps`。要查看任何现代 Fedora 发行版上 `ping` 所需要的任何特殊能力，请输入：

```
# getcap "which ping"
```

### 查找和创建 SetUID 程序

SetUID 程序具有特殊的文件属性，内核利用该属性来确定是否应该覆盖授予应用程序的默认权限。简单的文件列表 (`ls -l`) 会显示文件的权限并揭示这一小的事实。这是一个示例：

```
[master@server -]$ ls -l /usr/bin/mount
-rwxr-xr-x. 1 root root 44248 Oct 24 07:00 /usr/bin/mount
```

如果权限字段中的第四个字符是 `s`，则该程序是 SetUID。如果文件的所有者是 `root`，则该程序是 SetUID root。在 `mount` 二进制文件的情况下，我们可以看到它将带有 `root` 权限执行。

> 你可以使用 `stat` 工具来查看文件权限的八进制表示。例如，要查看 `mount` 命令的八进制模式权限 (`4755`)，请输入：

```
$ stat -c 'a %a %n' 'which mount'
-rwxrws-xr-x 4755 /bin/mount
```

另一个示例是 `passwd` 工具，在此所示：

```
[master@server -]$ ls -l /usr/bin/passwd
-rwxr-xr-x. 1 root root 27864 Aug 17 17:50 /usr/bin/passwd
```

![](img/206cceb3dded456e2347d07189576dd7_358_0.png)

## 328 第三部分 网络与安全

与 `mount` 一样，我们看到权限的第四个字符是 `s`，所有者是 `root`。因此，`passwd` 程序是 SetUID root。

要确定运行中的进程是否为 SetUID，你可以使用 `ps` 命令查看进程的实际用户及其有效用户，如下所示：

```
[master@server ~]$ ps ax -o pid,euser,user,comm
```

这这将输出所有运行的程序及其进程 ID (`pid`)、有效用户 (`euser`)、真实用户 (`user`) 和命令名称 (`comm`)。如果有效用户与真实用户不同，则它可能是一个 SetUID 程序。

注意：某些（必然）由 `root` 用户启动的应用程序可以将其权限交给以低特权用户运行，以提高安全性。例如，Apache 服务器可能由 `root` 用户启动，以允许其绑定到 TCP 端口 80（记住特权用户可以绑定到低于 1024 的端口），但如果它随后放弃权限并以无权限用户（通常为 "nobody"、"apache"、"www-data" 或 "www"）启动其所有线程。

极少情况下，例如，如果我们有一个名为 `myprogram` 的程序并想将其设置为 SetUID，我们会执行以下操作：

```
[master@server ~]$ chmod 4755 myprogram && sudo chown root myprogram
[master@server ~]$ ls -l myprogram
-rwxr-xr-x. 1 root      43160 Jul 13 2026      myprogram
```

确保系统具有绝对最少且必要的 SetUID 程序可以是一个良好的维护措施。典型的 Linux 发行版可以很容易地拥有几个不必要的 SetUID 文件和可执行文件。遍历目录查找 SetUID 程序可能很累人且容易出错。因此，与其手动这样做，你可以使用 `find` 命令，如下：

```bash
$ find / -perm -4000 -ls
```

要搜索为 SetGID 文件，请输入：

```bash
$ find / -type f -perm -2000 -ls
```

要使用单个 `find` 命令同时搜索 SetUID 和 SetGID 文件并使用 `stat` 命令查看八进制模式，请输入：

```bash
$ find / -type f \( -perm -4000 -o -perm -2000 \) | xargs stat -c '%A %n'
```
