
此示例为三台计算机授予打印访问权限：主机当前网络上的 `polk`、`tyler.threeroomco.com` 以及 `192.168.2.19`。正如你所见，你可以仅按主机名、完全限定域名（FQDN）或 IP 地址列出名称。FQDN 和 IP 地址是最安全的形式。

> **注意：** 你可以使用仅包含 `+` 的行来表示所有计算机都可以向你的打印机打印。我不建议这样做，不过。即使你的计算机目前未直接连接到互联网，如果你以后更改该配置，很容易忘记更改 `/etc/hosts.lpd` 中的条目，从而使你的系统对任何想浪费你的纸张、墨水和碳粉的恶作剧者开放。

默认情况下，将客户端机器的名称或 IP 地址放在 `/etc/hosts.lpd` 中会给予客户端计算机对服务器上所有打印机的完全访问权限。此方法不会授予对任何其他系统资源的访问权限。例如，`/etc/hosts.lpd` 不会授予对第 10 章“ NFS：与其它 UNIX 系统共享文件”第 241 页所述的 NFS 导出访问权限。为此，你必须编辑 `/etc/exports` 文件。

## 编辑 `/etc/hosts.equiv`

`/etc/hosts.equiv` 文件的工作方式与 `/etc/hosts.lpd` 文件非常相似——你将信任的客户端计算机列在文件中，这些机器能够不受限制地向你的系统打印。

问题在于 `/etc/hosts.equiv` 做的远不止给予这些客户端机器访问本地打印机队列的权限。它还以其他方式给予这些机器的用户访问你的机器的权限，例如通过 `rlogin` 程序，该程序允许用户无需提供密码即可从受信任主机登录到远程计算机。

例如，假设你的计算机 `fillmore` 的 `/etc/hosts.equiv` 文件列出了 `polk` 和 `tyler`。那么，任何在 `fillmore` 以及 `polk` 或 `tyler` 上都有账户的用户都可以无需提供密码即可访问 `fillmore`。这在某些情况下可能很方便，但也可能是一个巨大的安全漏洞。如果 `polk` 的安全性薄弱，例如，入侵者就可以轻松获得对 `fillmore` 的访问权限。

> **警告：** 与 `/etc/hosts.lpd` 一样，`/etc/hosts.equiv` 中仅包含字符 `+` 的行会使任何主机都成为受信任主机。这是天文数字级别的安全漏洞。我建议你检查你的系统，以确保它未以这种方式配置。

总体而言，我建议除非你完全了解安全影响并且愿意承担风险，否则不要使用 `/etc/hosts.equiv` 文件。仅提供打印机访问权限时，`/etc/hosts.lpd` 已足够。

> **提示：** 为了降低与 `/etc/hosts.equiv` 相关的风险，你可以通过在 `/etc/inetd.conf` 中注释掉其行来禁用使用它的服务——主要是 `rlogin` 和 `rsh`。我建议除了删除 `/etc/hosts.equiv` 之外还要这样做。

## 控制对你的打印机的访问

假设你想将对打印机的访问限制为某些用户或用户组，无论是本地还是远程系统。Linux 的打印机队列系统通过 `/etc/printcap` 文件中的选项提供此功能。具体来说，有两个感兴趣的选项：

- `rs`—此选项是二进制的（要么存在要么不存在），控制当远程用户在本地系统上没有账户时，远程用户是否可以打印到本地队列。当 `rs` 选项不存在时，任何用户都可以打印，只要主机系统在 `/etc/hosts.lpd` 或 `/etc/hosts.equiv` 中获得批准。因此，计算机 `polk` 上的用户 `sally` 即使在 `fillmore` 上没有对应的账户也可以在 `fillmore` 上的队列上打印。但是，如果你在 `fillmore` 上的 `/etc/printcap` 中添加 `rs` 选项，`sally` 将无法打印到 `fillmore` 的任何队列。然而，用户 `joe` 在两个系统上都有账户，即使在 `fillmore` 上设置了 `rs` 也可以打印。

### Note

Linux 的打印机队列软件的多个版本对 `rs` 特性的实现存在缺陷。例如在 Red Hat 5.2 中，软件将所有队列都当作已启用 `rs` 选项处理，无论 `/etc/printcap` 中是否指定。在 Red Hat 6.0 中，只要设置了 `rs`，`lpd` 就会锁定所有远程用户——即使这些用户在服务器计算机上拥有有效账户。在撰写本文时，Red Hat 尚未对此问题发布官方修复，尽管它已在 Red Hat 正在随 Red Hat 6.1 测试版分发的 `lpr` 包中得到修复。该修复版本包含在本書附带的 CD-ROM 的 `sams-extras/printing` 目录中。如果您需要 `rs` 功能，应安装此更新的 `lpr` 包。

- `rg=`—此选项指定受限组打印机。例如，如果您指定 `rg=faculty`，则该打印机将仅对 `faculty` 组可访问。您可以使用此功能限制任意用户组的访问。为此，创建一个用于打印机访问的特殊组，将您希望拥有访问权限的所有用户添加到该组，并在 `/etc/printcap` 文件中添加适当的 `rg=` 选项。

必须认识到这些特性是按打印机为基础应用的。您可以为一台打印机提供不受限制的访问，但限制同一系统上另一台打印机的访问。`rg=` 选项也适用于服务器计算机上的本地用户。

作为这两种访问控制方法的示例，请考虑以下示例 `/etc/printcap` 条目：

```
bigcolor:\n    :sd=/var/spool/lpd/lp:\n    :mx#0:\n    :sh:\n    :rs:\n    :rg=layout:\n    :lp=/dev/lp0:\n    :if=/var/spool/lpd/lp/filter:
```

此条目将对打印机 `bigcolor` 的访问限制为拥有本地系统账户且属于 `layout` 组的用户。

#### Tip

`rs` 选项仅适用于使用原生 Linux/UNIX 打印机共享机制限制打印，但 `rg=` 选项也可以与 Samba 一起使用。您可以像这里所述一样限制打印机访问，只要您的 Samba 用户使用自己的密码登录，您就可以以这种方式限制打印机访问。

## Printing to a Remote UNIX Printer from Linux

由于原生 UNIX/Linux 风格的打印涉及 UNIX 或 Linux 客户端，因此了解此类打印机配置的客户端非常重要。在很大程度上，此配置的工作方式与第 14 章“Preparing to Share a Printer”，第 351 页所述类似。不过也有一些独特细节。

## Using printtool to Configure Printing

启动 `printtool` 并单击 Add 以添加打印机队列后，`printtool` 会询问您要添加什么类型的打印机。选择 Remote Unix (lpd) Queue，然后不是显示 Edit Local Printer Entry 对话框，`printtool` 会显示 Edit Remote Unix (lpd) Queue Entry 对话框，如图 15.1 所示。

![](img/5d4d3092919d1d16884788127447cc6d_405_0.png)

### FIGURE 15.1

创建用于远程 UNIX 或 Linux 打印机的本地队列时，必须指定远程主机和打印机队列。

Edit Remote Unix (lpd) Queue Entry 对话框的工作方式与第 14 章所述的 Edit Local Printer Entry 对话框非常相似。唯一的区别是，您必须输入远程计算机的名称和该计算机上目标打印机的队列名称，而不是打印机设备文件的名称。其他字段，包括打印机名称、spool 目录、文件大小限制和输入过滤器，与本地打印机的工作方式完全相同。

#### NOTE

打印机队列在一个计算机上的名称可能与另一台计算机上的名称不同。例如，打印服务器 `fillmore` 上的打印机队列 `bigcolor` 可能从远程计算机 `polk` 以 `epson1520` 访问。然而，为了所有相关人员的 sanity，最好尝试协调打印机队列名称。如果名称冲突不可避免（例如，因为多个打印服务器上存在名称冲突的现有队列），请尝试使用服务器和队列名称的组合作为客户端计算机队列名称，如 `fillmore_bigcolor` 或 `fm_bigcolor`，以标识 `fillmore` 上的 `bigcolor` 打印机。或者，您也可以以类似的方式使用打印机的位置，如 `fl2_bigcolor` 表示 2 楼的 `bigcolor` 打印机。

## Configuring `/etc/printcap` Manually

远程打印机队列的 `/etc/printcap` 条目与本地队列的条目非常相似。与基于 `printtool` 的配置一样，您只需更改打印机设备指定的方式。不是在 `/etc/printcap` 中使用 `lp=` 选项，您需要指定 `rm=` 和 `rp=` 参数，分别指定远程系统的名称和远程系统上的打印机队列名称。例如，以下是远程打印机队列的示例 `/etc/printcap` 条目：

```
bigcolor:\
:sd=/var/spool/lpd/lp:\
:mx#0:\
:sh:\
:rm=fillmore.threeroomco.com\
:rp=bigcolor:\
```
