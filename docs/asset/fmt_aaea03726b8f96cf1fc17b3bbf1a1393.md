
```
options {
sync (); # 写入文件前的缓冲区行数
perm(0640); # 创建文件的权限值。
keep_hostname(yes); # 保留原始主机名。
}
```

要启用监听器，源 (`src`) 需要使用 `udp` 语句，如示例 8-52 所示。

### 示例 8-52 syslog-ng 服务器的源示例

```
source src {
#
# 包含内部 syslog-ng 消息
# 注意：需要 internal() 源！
#
internal();
#
# 用于本地记录的默认日志套接字：
#
unix-dgram("/dev/log");

#
# 取消注释以处理来自网络的日志消息：
udp("0.0.0.0") port(514));

};
```

重启 `syslog` 服务以加载 `syslog-ng` 配置文件，如示例 8-53 所示。

### 示例 8-53 重启 syslog-ng 服务器以更新配置

``` 
evensyslog-server-1:"# service syslog restart
Shutting down syslog services done
Starting syslog services done
```

要测试监听器，你可以使用 `lsof`，如示例 8-52 所示。

### 示例 8-54 使用 lsof 命令测试监听器

```
syslog-server-1:"# lsof -i UDP:514
COMMAND PID USER FD TYPE SIZE/OFF NODE NAME
syslog-ng 60700 root 4u IPv4 327255 0t0 UDP *:shell
```

如果你愿意，也可以使用 TCP，但为了启动一个简单的

## 8.8.3 服务器配置

复杂的服务器配置不在本书的讨论范围内。`syslog-ng` 的默认配置带有根据要记录的 facility 拆分文件的定义。图 8-9 显示了一个集中的 `syslog-ng` 服务器接收来自 `syslog-ng` 客户端的日志副本。

![](img/2db39dd28fa1ef80e2c2d208b955dfbd_187_0.png)

图 8-9 集中的 syslog-ng 服务器和一些 syslog-ng 客户端

测试环境的全局选项在示例 8-51 中。

### 示例 8-51 syslog-ng 服务器的全局选项

```
options {
sync (); # 写入文件前的缓冲区行数
perm(0640); # 创建文件的权限值。
keep_hostname(yes); # 保留原始主机名。
}
```

要启用监听器，源 (`src`) 需要使用 `udp` 语句，如示例 8-52 所示。

### 示例 8-52 syslog-ng 服务器的源示例

```
source src {
#
# 包含内部 syslog-ng 消息
# 注意：需要 internal() 源！
#
internal();
#
# 用于本地记录的默认日志套接字：
#
unix-dgram("/dev/log");

#
# 取消注释以处理来自网络的日志消息：
udp("0.0.0.0") port(514));

};
```

重启 `syslog` 服务以加载 `syslog-ng` 配置文件，如示例 8-53 所示。

### 示例 8-53 重启 syslog-ng 服务器以更新配置

```
syslog-server-1:"# service syslog restart
Shutting down syslog services done
Starting syslog services done
```

要测试监听器，你可以使用 `lsof`，如示例 8-52 所示。

### 示例 8-54 使用 lsof 命令测试监听器

```
syslog-server-1:"# lsof -i UDP:514
COMMAND PID USER FD TYPE SIZE/OFF NODE NAME
syslog-ng 60700 root 4u IPv4 327255 0t0 UDP *:shell
```

如果你愿意，也可以使用 TCP，但为了启动一个简单的

如第 173 页的示例 8-50 所示，`log` 语句需要源、过滤器和目标。

在部署 Samba 之前，请确保在任何迁移活动之前已进行适当的分析和规划。书中提供的清单列出了在迁移过程中需要考虑的许多领域，以防止问题的出现。

此示例假设 z/VM 虚拟机已经建立并安装了 Linux 操作系统。该 Linux 虚拟机命名为 `LNUSDB2`，安装了 SUSE Linux Enterprise 11 SP3，配有 1 个虚拟 CPU 和 1 GB 虚拟内存。通过 LDAP，Samba 服务器在 LinuxONE 上运行时通常不需要大量的 CPU 或 RAM。假设已经设置好并提供了可用的适当的 RPM 仓库安装源，用于安装应用程序软件。

关于 Samba 的更详细文档可以从以下网站找到：

```
http://www.samba.org
```

此示例是一个独立的服务器，具有本地的、非复制的目录服务。将 x86 上的 Samba 安装迁移到 LinuxONE 应该是轻而易举的。

## 8.9.1 安装 Samba 软件

安装软件相对简单：

- 在 SUSE Linux Enterprise Server 上安装 Samba 及其依赖包，请执行此命令：

  `zypper install samba`

- 在 Red Hat Enterprise Linux 上安装 Samba 及其依赖包，请执行此命令：

  `yum install samba`

## 8.9.2 配置 Samba

本节描述了如何在 SUSE Linux Enterprise Server 和 RHEL 上首次配置 Samba。

### 使用 YaST 在 SUSE Linux Enterprise Server 上配置 SAMBA 配置文件服务器

创建可用配置的所有活动都通过 Samba YaST 模块提供便利。通过使用 YaST 中的几个面板，可以很快地配置并运行 Samba 服务。

要配置 Samba 服务器，启动 YaST 并选择“网络服务 -> Samba 服务器”。按照示例 8-59 所示，使用您的网络信息完成所示的字段。

> 示例 8-59 在 YaST 上初始配置 Samba
> 
> 工作组名称或域：从您现有的工作组或域中选择您的名称
> 
> Samba 服务器类型 (PDC, BDC 或 独立)：指定您的服务器是否应作为
> 
> 启动服务：在服务器重启后，选择在启动期间启动
> 
> 防火墙设置：如果您在此服务器内部运行防火墙服务器，请勾选在防火墙中打开端口选项
> 
> Samba root 密码：为您的 Samba 服务选择一个密码

178 从 x86 迁移到 LinuxONE 的实用迁移

图 8-11 显示了 YaST2 面板中的配置信息。

![](img/2db39dd28fa1ef80e2c2d208b955dfbd_192_0.png)

完成此任务后，您应该能够从客户端机器映射到该服务器。

> 注意：如果您打算使用基础 Linux 身份验证（即使用 passwd 文件），则你必须使用命令 `smpassword -a <userid>` 更改 Samba 用户密码。

### Samba 的 LDAP 设置

许多公司使用 LDAP 提供单点登录，其中用户密码在服务之间共享。创建可用配置的活动通过 OpenLDAP 服务器 YaST 模块提供便利。虽然 SAMBA 上的 LDAP 配置是一项重要功能，但该配置超出了本书的范围。

有关如何在 Samba 上设置 LDAP 的信息，请参 Samba 官方网站：

`http://www.samba.org`

### 配置文件

您可以手动设置 Samba 的配置文件。SUSE Linux Enterprise Server 上的主配置文件存储在 `/etc/samba/smb.conf` 中，包含两个部分：

- `[ global ]` 用于常规设置
- `[ ]` 用于指定有关共享文件和打印机的特定设置

有关 SUSE Linux Enterprise Server 上 Samba 配置的更多详细信息，请参阅《SUSE Linux Enterprise Server 11 管理指南》中的 Samba 部分：

`bit.ly/Zxelvc`

> 注意：RHEL 6 与 SUSE Linux Enterprise Server 11 使用相同的 Samba 主配置文件结构。

### 启动和停止 Samba 服务

`smb` 服务控制服务器守护进程并可以被停止。通过示例 8-61 所示的命令停止并启动 Samba 服务。

在 SLES 和 RHEL 上停止和启动服务：

停止服务：`/etc/init.d/smb`

启动服务：`/etc/init.d/smb`

![](img/2db39dd28fa1ef80e2c2d208b955dfbd_194_0)

# 第 部分

## 附录

本节包含一个附录，提供了额外的用例：

- 附录 A，“额外用例”，位于第 183 页

## 额外用例
