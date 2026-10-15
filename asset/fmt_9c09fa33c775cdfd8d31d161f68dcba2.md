
drwx-xr-x+ 2 jane WinUsers 24 abr 17 08:55 Saved Games

drwx-xr-x+ 2 jane WinUsers 85 abr 17 08:55 Searches

drwx-xr-x+ 2 jane WinUsers 24 abr 17 08:55 Videos

## 实现系统策略

Windows NT Server 版本使用 `poledit.exe` 程序（图 15-10）创建策略，这些策略以后可以应用于域中的所有用户计算机，或仅适用于其中的一部分。遗憾的是，Samba 没有原生工具在 NT 环境中创建系统策略。我们可以在运行 `poledit.exe` 的 Windows 工作站上创建这些策略，并在 Samba 服务器上应用它们。

413.

# 第 15 章 作为 PDC 和 BDC 的 Samba

![](img/dfa44432604022575079471b648e25ca_421_0.png)

**图 15-10.** 策略编辑器 (`poledit.exe`)

策略编辑器允许我们自定义计算机、用户或两者的设置（图 15-11）。有很多选项可以适应我们的需求；例如，我们可以编辑登录横幅（图 15-12）。

![](img/dfa44432604022575079471b648e25ca_422_0.png)

**图 15-11.** 计算机和用户设置

416.

Technet24

## 第 15 章 作为 PDC 和 BDC 的 SAMBA

我们需要 PDC 和 BDC 这两台服务器都拥有域内账户的相同信息。由于 PDC 目前使用的是后端 (`tdbsam`)，这可以通过简单复制 `/var/lib/samba/private/passdb.tdb` 文件来轻松实现。如果我们还想让组映射或打印机相关信息保持一致，我们必须复制相应的 `.tdb` 文件，在这种情况下为 `group_mapping.tdb` 和 `printers.tdb`。然而，也有一些 `.tdb` 文件应该是每台服务器独有的。

```bash
[root@kilo ~]# sc juliet.linuxaholics.com:/var/lib/samba/private/passdb.tdb /var/lib/samba/private/passdb.tdb
```

```bash
[root@kilo ~]# pdbedit -L
root:0:root
john:24294967295:
zULU:4294967295:ZULU$
antonio:4294967295:
jane:4294967295:
```

为了保持 PDC 和 BDC 中这些信息一致，我们应该创建一个定期执行的 cron 任务（定时任务）。

注意：这不是配置 BDC 的优化方法。Samba 官方文档说明，不建议通过这种方式复制 `.tdb` 文件，因为文件可能处于打开状态，复制时可能会导致错误和不一致。相反，Samba 推荐使用 `ldaps` 作为后端。这对于生产环境显然是一个更好的解决方案，因为信息存储在 LDAP 服务器中，PDC 和 BDC 都可以访问。但是，对于我们正在使用的这种实验环境，复制 `.tdb` 文件作为一种概念证明是可以在接受的方案。

所有的 DC 都应该在 `/var/lib/samba/private/secrets.tdb` 文件中存储相同的域 SID。我们可以通过以下 `net` 子命令来实现：

```bash
[root@kilo ~]# net rpc getsids
```

不过，我们可能会遇到这个错误：

`Unable to find a suitable server for domain MY_SAMBA_DOMAIN`

如果是那样，我们将编辑 `smb.conf` 文件，将我们的 Samba 服务器配置为 PDC 服务器的 WINS 客户端。

```ini
wins server = juliet.linuxaholics.com
```

现在命令应该可以无问题地执行了。

```bash
[root@kilo ~#] net rpc getsid
Storing SID S-1-5-21-852636792-403353388-521036446 for Domain MY_SAMBA_DOMAIN in secrets.tdb
```

如果我们运行 `testpam`，它将识别该服务器为 BDC。

```bash
[root@kilo ~#] testpam
.
.
```
Server role: ROLE_DOMAIN_BDC
```
.
.
```

然而，为了让我们的服务器作为 BDC 运行，我们仍然需要修改几个 SELinux 布尔值。

```bash
[root@kilo ~#] setsebool -P samba_domain_controller on
[root@kilo ~#] setsebool -P samba_run_unconfined on
```

为了完成配置，我们将为服务器分配一个 NetBIOS 名称并在防火墙中开放服务。

```bash
[root@kilo ~#] cat etc/samba/smb.conf
.
.
```

```ini
netbios name = KILO_BDC
```

```
.
.
```

## 第 15 章 作为 PDC 和 BDC 的 SAMBA

```bash
[root@kilo ~]# firewall-cmd --add-service=samba
success
[root@kilo ~]# firewall-cmd --permanent --add-service=samba
success
```
