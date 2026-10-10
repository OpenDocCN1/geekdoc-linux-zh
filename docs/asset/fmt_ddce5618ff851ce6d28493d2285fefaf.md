
> 注意：如果 SNMP 配置不当，会带来潜在的安全风险。在配置 Squid 时请务必小心。

Squid 守护进程 (`/usr/sbin/squid`) 可以在系统启动时自动启动。设置完成后，Squid 的大部分配置都在 `/etc/squid/squid.conf` 文件中完成。`squid.conf` 文件包含了大量关于如何配置 Squid 的信息（该文件包含 4300 多行注释和示例，尽管只有 35 行有效设置）。

有关 Squid 代理服务器的更多信息，请参考 Squid Web 代理缓存主页 (`www.squid-cache.org`)。

## 启动 squid 守护进程

当你安装 Fedora RHEL 时，你有机会安装 Squid (`squid` 包)。如果你不确定是否安装了 Squid，请输入以下命令：

```bash
# rpm -q squid
squid-3.0.STABLE2-2.fc9.i386
```

如果未安装 `squid`，你可以从随本书提供的 DVD 中安装，或者通过输入 `yum install squid` 从网络安装。接下来，你可以检查 `squid` 是否配置为运行。要做到这一点，请输入：

```bash
# chkconfig --list squid
squid 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

如果 `squid` 服务在运行级别 3、4 和 5 中处于关闭（默认情况下这些运行级别是关闭的），你可以设置它在启动时自动启动。要设置 `squid` 守护进程在启动时启动，请输入：

```bash
# chkconfig squid on
```

此时，`squid` 守护进程应该会在系统启动时自动启动。默认情况下，`squid` 守护进程将带有 `-D` 选项运行。`-D` 选项允许 Squid 在没有活动互联网连接的情况下启动。如果你想为 `squid` 守护进程添加其他选项，可以编辑 `/etc/squid/squid` 配置文件。寻找类似于下面的内容的行：

```bash
SQUID_OPTS="-D"
```

你可以在引号内向 `-D` 选项添加任何选项。这些选项中的大部分对调试 Squid 很有用：

- `-a port`: 替换端口 `a`，该端口将代替默认端口号 (`3128`) 用于提供 HTTP 代理请求。这对于临时尝试备端口很有用。
- `-f squidfile`: 使用此选项指定备用的 `squid.conf` 文件（`/etc/squid/squid.conf` 之外）。将 `squidfile` 替换为备 `squid.conf` 的名称。这是在替换旧文件之前尝试新 `squid.conf` 文件的好方法。
- `-d level`: 将调试级别更改为 `level` 指定的数字。这会导致调试信息发送到 stderr。
- `-X`: 使用此选项检查你的 `squid.conf` 文件中的值是否正确。它会在解释 `squid.conf` 文件时开启完全调试。

你可以通过输入 `/etc/init.d/squid restart` 重启 `squid` 服务。在 `squid` 守护进程运行时，你有几种方法可以使用这些选项运行 `squid` 命令来更改守护进程的工作方式：

## 第四部分：Fedora RHEL 网络与服务器设置

- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt`: 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k kill`: 立即杀死 Squid。
- `squid -k reconfigure`: 导致 Squid 重新读取其配置文件。
- `squid -k shutdown`: 导致 Squid 在短暂等待当前连接退出后退出。
