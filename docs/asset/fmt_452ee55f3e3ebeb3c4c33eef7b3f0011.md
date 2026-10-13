
因此，在排除包括 `[printers]` 在内的任何打印共享故障之前，请确保客户端和服务器机器互相 `ping` 通。如果不能，请检查网络。
接下来，确保你可以在客户端列表（网络邻居或 `smbclient -L Address`）中看到 `[global]` 定义的工作组。如果不能，请针对打印机整体排查 Samba 的问题。使用 `testparam`（本章稍后讨论）验证 `smb.conf` 的内部一致性。
接下来，确保打印机工作正常。打印机名称可以根据共享的 `printer name=` 行推断。如果共享中没有 `printer name=`，则可以从客户端请求推断。执行以下操作：

```
lp -P printcap_printer_name /etc/fstab
```

这应该将 `/etc/fstab` 打印到 `/etc/printcap` 中定义的 `printcap_printer_name` 物理打印机。`/etc/fstab` 是一个理想的测试文件，因为它短且存在于所有 Red Hat Linux 机器上。一旦机器可以 `ping` 通，且你能看到 `[global]` 部分定义的工作组，就可以开始排除 Samba 打印共享的故障了。

## 配置服务

第二部分

许多 Samba 打印机问题的出现是因为 `printcap printer` 命令不起作用。如果 `printcap printer` 是网络打印机而不是本地打印机，情况尤其如此。首先尝试在打印机共享中加入以下行：

```
print command = lpr -P %s %s; rm %s
```

该命令将文件 `%s`（从客户端传递的池文件）打印到打印机 `%p`（从客户端传递的打印机名称）。你会发现这与之前描述的 `printcap printer` 中执行的命令相同，因此它应该可以工作。
如果仍然不起作用，请验证 `path=` 条目指向一个用户具有读和写权限的目录。确保任何 `printer name=` 条目都指向 `/etc/printcap` 中定义的可用打印机。确保该条目具有 `printable=yes` 或 `print=yes` 条目；它不是 Samba 共享。打印机共享具有有效的 `users=` 条目，请确保相关用户是这些用户之一。
如果仍然无法工作，似乎可以安装你自己的测试点。临时创建一个模式为 777 的目录 `/home/freeall`（所有人均可读、写、执行），注释掉 `smb.conf` 中的任何 `print command=` 行，并添加以下行：

```
print command = cp %s /home/freeall/%s.test;rm %s
```

这将要打印的文件复制到 `/home/freeall` 中，文件名与 `printcap printer` 打印机相同，但带有 `.test` 扩展名。这提供了几项信息。首先，文件名告诉你是它正尝试打印到哪个打印机。你可以检查 `/etc/printcap` 或 `printtool` 以确认该打印机是否存在。你可以打印该文件并查看它是否正常输出。
如果文件不存在，说明 `print command` 命令的客户端侧出现了问题。务必检查客户端上的队列，查看其是否被阻塞。有时，服务器上的单次失败会导致打印队列阻塞。此外，确保所有用户都 reality读、写和执行 `/home/freeall` 目录；否则打印将在权限上产生覆盖。问题解决后，出于安全考虑，务必删除你创建的 `/home/freeall` 测试目录。
另一个方便的故障排除工具是检查 Samba 日志。它们通常包含有用的错误信息。如果日志文件未在 `smb.conf` 的 `[global]` 部分定义，请查看 `/var/log/samba` 目录。
除了这些提示，请记住故障排除只是保持冷静并缩小问题范围的问题。

## 共享文件和打印服务

在配置好 Samba 服务器的默认设置后，你可以创建特定的共享目录，仅限制某些用户组或对所有人可用。例如，假设你想让一个目录仅对一个用户可用。要做到这一点，你需要创建一个新章节并填入所需信息。通常，你需要向 SMB 服务器指定用户、目录路径和配置信息，如下所示：

```
[jacksdir]
comment = Jack 的远程源代码目录
path = /usr/local/src
valid users = tackett
browseable = yes
public = no
writable = yes
create mode = 0700
```

此示例节创建了一个名为 `jacksdir` 的共享目录。 是将共享名称保持在九字符以内，以避免 `testpar` 工具出现警告，并避免在无法使用更长共享名的旧版 SMB 客户端上出现问题。本地服务器上的目录路径为 `/usr/local/src`。`browseable` 条目设置为 `yes`，`jacksdir` 将出现在客户端的网络浏览列表（如 Windows 资源管理器）中。然而，由于 `public` 条目设置为 `no` 且 `valid users` 条目仅列出了 `tackett`，只有用户 `tackett` 可以使用 Samba 此目录。你可以通过在 `valid users` 条目中指定（在组名前前加上 `@` 符号）授予更多用户和组访问权限。以下是给予 `devel` 组权限后的 `valid users`：

`valid users = tackett, @devel`

通过在共享中放置 `printer ok=yes`（或同义词）和打印机名称来创建打印机。这是一个示例：

```
[vals_lp]
print ok = yes
printer name = lp_mine
path = /home/everyone
valid users = valerie, @devel
browseable = yes
```

由于 `browseable=yes`，客户端上列出的打印机为 `vals_lp`。它通过 `printcap lp_mine` 打印。它的池目录为 `/home/everyone`，有效用户是 `valerie` 和 `devel` 组。
此类打印机共享与 `[printers]` 部分之间的主要区别在于，`[printers]` 部分显示所有 `printcap` 打印机但不可浏览，而像前面的打印机共享仅显示值出现在 `printer name=` 选项中的打印机，并且仅当出现 `browseable=yes` 选项时显示。`[printers]` 部分没有或不需要 `printer name=` 条目，因为其目的是向客户端显示所有打印机并允许访问所有打印机。
本章 `[printers]` 部分之前列出的所有打印机故障排除提示适用于打印机共享。

## 优化 Samba 性能

Samba 执行出色，因此性能通常不是问题。如果性能成为问题，有几个选项可以评估。

> 注意 作者测试了以下所有的 Samba 配置性能增强技术，但在一个使用 Celeron 333、64MB 内存、7200rpm 14.4GB 磁盘、100Mb 布线的低负载 Samba 服务器上，通过一个 11MB 文件的往返测试，未能获得任何显著的性能提升。结论是，增益取决于许多因素。底线是性能受瓶颈限制，要提高性能，定位性能瓶颈至关重要。一旦完成，就可以制定性能增强计划。

最好的瓶颈分析技术之一是有意减慢怀疑的瓶颈。如果系统吞吐量以类似的比例下降，你就找到了瓶颈。如果系统吞吐量仅略微下降，请继续寻找。
Samba 的 `wide links` 默认设置为 `yes`。设置可以获得安全收益。然而，在某些环境中报告了巨大的性能成本。如果在重负载环境中将 `wide links` 设置为 `no`，你可能尝试将其改为 `yes`。
如果 `wide links=` 设置为 `yes`，通过在 `[global]` 部分设置 `getwd cache= yes` 可以获得进一步的优化。（默认是 `no`。）
对虚拟内存利用的微调也可以改进 Samba。文档中专门记录了两个微调。

> 警告 在先咨询并理解文件 `/usr/doc/kernel-doc-2.2.5/sysctl/vm.txt` 内容之前，不要尝试进行以下 `bdflush` 和 `buffem` 微调。每个值在那个文件中都有解释。如果该文件不存在，请安装内核文档。它的名称类似于 `kernel-doc-2.2.5-15.i386.rpm`。

```
echo 80 50 64 64 80 6000 1884 2* /proc/sys/vm/bdflush
echo 60 80 80* /proc/sys/vm/buffem
```

其他可能的增强技术包括更快的硬件和布线、更好的服务器硬盘、更多的服务器内存或服务器 CPU 升级。

## 测试你的配置

创建配置文件后，你应该测试其正确性。首先让客户端和服务器 `ping` 对方的 IP 地址。如果没有功能网络，Samba 将无法工作。
接下来使用 `testparam`。`testparam` 是检查 `/etc/smb.conf` 配置内部正确性的简单测试程序。如果此程序报告没有问题，你就可以放心地使用配置文件，相信 `smbd` 将成功加载配置。
