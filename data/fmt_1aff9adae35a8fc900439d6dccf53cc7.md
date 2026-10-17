
kadmin.local: `ktadd -k /usr/local/kerberos/var/krb5kdc/kadm5.keytab`

`#admin/admin kadmin/changepw`

... [ Output from ktadd command ]

kadmin.local: `exit`

您现在应该可以启动 `kadmin` 服务器了，它也会像 `krb5kdc` 一样立即在后台运行。

## kadmin

如果 `krb5kdc` 和 `kadmin` 都成功启动，您的 KDC 机器几乎就准备好使用了。剩余的任务是从您的初始化脚本中启动 `krb5kdc` 和 `kadmin`。最简单的方法是在 `/etc/rc.d/rc.local` 文件中执行。几行这样的代码就足够了：

```bash
# Start the Kerberos services

PATH=$PATH:/usr/local/kerberos/bin:/usr/local/kerberos/sbin

krb5kdc
```

完成这些更改后，您的 KDC 宿主机每次启动时都会自动启动 Kerberos 服务。

## 管理 Kerberos 5

现在 KDC 正在运行，战斗已经胜利。您需要的大部分信息与在网络上管理 Kerberos 服务时遇到的各种任务有关。

### 添加管理员主实体

尽管您有一个工作的 KDC，但目前还没有管理员，这使得您的 KDC 几乎毫无用处，因为所有主机都需要管理员访问。要添加管理员，首先启动 `kadmin.local` 并使用 `add_principal` 命令添加用户。

```
# kadmin.local: add_principal tester

Enter password for principal "tester@MYNET.NET":

Re-enter password for principal "tester@MYNET.NET":
```

现在已经创建了一个名为 `tester` 的用户。为了测试 KDC 服务器，我们将使用 `kinit` 工具（我们将在本小时稍后详细讨论）为 `tester` 获取一个票据。然后，使用 `klist` 显示票据信息。

```
# kinit tester

Password for tester@MYNET.NET:

# klist cache: FILE:/tmp/krb5_cc_0

Default principal: tester@MYNET.NET
```

### Kerberos 简介

现在 `jake` 被归类为管理员并能够启动 `kadmin`。然而，赋予每个管理员的内部仍然没有权限。赋予每个管理员的权限集通过位于 `/usr/local/kerberos/var/krb5dc` 的名为 `kadm.local` 的访问控制列表进行控制。文件中的每行包含一个管理员的完整名称及其拥有的权限。这些权限见表 17.1。

#### 表 17.1 Kerberos 管理 ACL

| 权限 | 描述 |
| :--- | :--- |
| a | 允许添加主实体或策略 |
| d | 允许删除主实体或策略 |
| m | 允许修改主实体或策略 |
| c | 允许更改主实体密码 |
| i | 允许运行数据库查询 |
| 1 | 允许列出数据库中的主实体 |
| * 或 x | admin（所有权限）的缩写 |

> 管理员的默认 ACL 权限没有任何权限。因此，如果您没有为新创建的管理员在 ACL 文件中添加条目，该管理员将能够启动 `kadmin` 但无法在内部进行任何操作。编辑 ACL 文件后，您必须重启 `kadmin` 以使更改生效。遗憾的是，`-HUP` 信号对 `kadmin` 没有预期效果，因此唯一的选择是将其杀死并重启：

```
# killall kadmin; kadmin
#
```

用户现在应该能够在 realm 内任何主机上使用 `kadmin`，只要他拥有有效的 Kerberos 票据。

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_284_0.png)

### 添加和配置主机主体 (Host Principals)

在网络上的任何主机完全参与启用 Kerberos 的服务之前，该主机必须被添加到 KDC 数据库并进行正确配置以使用新的服务集。

首先，下载并安装 Kerberos，遵循与 KDC 相同的说明，但在 `make install` 步骤之后。一旦通过 `make install` 将 Kerberos 树安装到 `/usr/local/kerberos/bin`，创建 `/usr/local/kerberos/etc` 目录并从 KDC 主机的 `/usr/local/kerberos/etc` 拷贝 `kb5.conf` 和 `kdc.conf` 文件。将 `/usr/local/kerberos/bin` 和 `/usr/local/kerberos/sbin` 目录添加到 `PATH` 变量中。

现在，在新主机上变为超级用户并使用 `kinit` 命令获取管理员账户的票据。例如，记得我们已经为 `jake` 创建了管理员账户，在新主机上输入命令 `kinit jake` 并输入 `jake` 的密码。

```
newhost$ su

Password:

newhost# kinit jake

Password for jake@MYNET.NET:

newhost#
```

获取票据后，启动管理实用程序并使用 `add_principal` 命令为当前主机添加一个主体，格式为 `host/f.q.d.n`，其中 `f.q.d.n` 被替换为主机条目的完全限定域名。确保为你添加的每个主机选择一个无可置疑的密码。

```
newhost# kadmin

Authenticating as principal jake/admin@MYNET.NET with password:

Enter password:

kadmin: add_principal host/gxstation.myn.net

Enter password for principal "host/gxstation.myn.net@MYNET.NET":

Re-enter password for principal "host/gxstation.myn.net@MYNET.NET":

Principal "host/gxstation.myn.net@MYNET.NET" created.

kadmin:
```

`kadmin` 内部的最后一步是为当前主机添加 keytab 条目。这是通过 `ktadd` 命令完成的。

```
kadmin: ktadd host/gxstation.myn.net

... [Output of ktadd operation]

kadmin: exit

newhost#
```

当前主机已添加到 KDC 主机在领域内的已知主机数据库中，并且在新主机上的 `/etc/krb5.keytab` 处创建了 keytab 文件。

### Kerberos 简介

尽管 KDC 数据库信息已就绪，但所有原始（未经过 Kerberos 处理的）的服务在新主机上仍然运行。为了确保安全，主机必须停止响应来自旧（不安全）协议的请求。它们必须被新的、仅限 Kerberos 的版本取代。

再次将额外的协议信息添加到 `/etc/services`，并注意消除具有重复端口号或重复服务名的条目：

```
newhost# cd $HOME/krb5-1.2.1/src/config-files

newhost# cat services.append >>/etc/services

newhost#
```
