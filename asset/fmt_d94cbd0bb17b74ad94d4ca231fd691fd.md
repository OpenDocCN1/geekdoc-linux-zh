
```bash
# systemctl enable httpd.service
# systemctl start httpd.service
# systemctl status httpd.service
* httpd.service - The Apache HTTP Server
Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled;
vendor preset: disabled)
Drop-In: /usr/lib/systemd/system/httpd.service.d/-php-fpm.conf
Active: active (running) since 2019-09-02 16:16:56 EDT; 21min ago
Docs: httpd.service(8)
Main PID: 11773 (/usr/bin/httpd)
Status: "Total requests: 14; Idle/Busy workers 100/0;Requests/sec: 0.0111; Bytes served/s"
Tasks: 214 (limit: 2294)
Memory: 24M
CGroup: system.slice/httpd.service
  -11773 /usr/bin/httpd -DFOREGROUND
  -11774 /usr/bin/httpd -DFOREGROUND
  -11775 /usr/bin/httpd -DFOREGROUND
  -11776 /usr/bin/httpd -DFOREGROUND
  -11777 /usr/bin/httpd -DFOREGROUND
  -11778 /usr/bin/httpd -DFOREGROUND
```

当 `httpd` 服务启动时，默认会启动五个或六个 `httpd` 守护进程（取决于你的 Linux 系统）来响应 Web 服务器的请求。你可以通过 `httpd.conf` 文件中的设置（在本章后面的“理解 Apache 配置文件”中描述）来配置启动更多或更少的 `httpd` 守护进程。
要更改 `httpd` 守护进程的行为，可以通过运行 `systemctl edit httpd` 来编辑 `httpd` 服务。
由于存在不同版本的 `httpd`，请检查 man 手页（`man httpd`）以查看可以向 `httpd` 守护进程传递哪些选项。例如，运行 `systemctl edit httpd` 并添加如下条目：

```ini
[Service]
Environment=OPTIONS='-e debug'
```

# 第 17 章：配置 Web 服务器

保存更改（`Ctrl+O`, `Ctrl+X`）。添加 `-e debug` 会增加日志级别，使得尽可能多的 Apache 信息发送到日志文件中。重启 `httpd` 服务使更改生效。使用 `ps` 命令确保你采取的选项已生效：

```bash
$ ps -ef grep httpd
root 14575 1 08:49 ? 00:00:01 /usr/sbin/httpd -e debug-DFOREGROUND
apache 14572 1 08:49 ? 00:00:00 /usr/sbin/httpd -e debug-DFOREGROUND
```

如果你添加了调试选项（`-e debug`），请记住在调试完成后再次运行 `systemctl edit httpd` 并移除该条目以移除，然后重启服务。一直开启调试会迅速填满你的日志文件。

# Apache 安全性

为了保护 Apache，你需要了解标准的 Linux 安全功能（权限、所有权、防火墙和增强型 Linux/SELinux）以及 Apache 特有的安全功能。以下章节描述了与 Apache 相关的安全功能。

# Apache 文件权限和所有权

`httpd` 守护进程以 `apache` 用户和 `apache` 组运行。默认情况下，HTML 内容存储在 `/var/www/html` 目录（由 `httpd.conf` 文件中的 `DocumentRoot` 变量决定）。
为了让 `httpd` 守护进程能够访问这些内容，适用于标准的 Linux 权限：如果“其他”用户没有读取权限，则文件必须对 `apache` 用户或组具有读取权限，这样文件才能被读取并提供给客户端。同样，`httpd` 守护进程访问内容时经过的任何目录必须对 `apache` 用户、`apache` 组或其他用户具有执行权限。
虽然你不能以 `apache` 用户登录（`/sbin/nologin` 是默认设置），但你可以以 root 身份创建内容并更改其所有权（`chown`）或权限（`chmod`）。然而，通常会添加单独的用户或组账户，以创建所有人可读但仅限该用户或该组写入的内容。

# Apache 与防火墙

如果你在 Linux 中锁定了防火墙，你需要开放几个端口以便客户端能够与 Apache 通信。标准 Web 服务（HTTP）可以通过 TCP 端口 80 访问；安全 Web 服务（HTTPS）可以通过 TCP 端口 443 访问（仅在你安装了前述的 `mod_ssl` 包时才使用 443 端口）。
要验证 `httpd` 服务使用了哪些端口，请使用 `netstat` 命令：

```bash
# netstat -tupln | grep httpd
tcp6 0 0 ::80 *:* LISTEN 29169/httpd
tcp6 0 0 ::443 *:* LISTEN 29169/httpd
```

# 第四部分：成为 Linux 员

输出显示 `httpd` 进程（进程 ID 29169）正在所有地址的端口 80 (`:::80`) 和端口 443 (`:::443`)。这两个端口都与 TCP 协议关联。要在 Fedora 或 Red Hat Enterprise Linux 中开放端口，你需要添加防火墙规则。
在当前的 Fedora 30 或 RHEL 7 系统上，打开防火墙窗口（在 Activities 界面输入 Firewall 并按回车）。在那里，选择 public 区域，勾选 http 和 https 服务旁边的复选框。端口将立即开放。
对于 RHEL 6 或更早版本，在 `/etc/sysconfig/iptables` 文件中添加以下规则（位于 `DROP` 或 `REJECT` 之前）：

```bash
-A INPUT -m state --state NEW -m tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m tcp --dport 443 -j ACCEPT
```

重启 `iptables`（`service restart`）使规则生效。

# Apache 与 SELinux

如果增强型 Linux（SELinux）设置为强制模式（enforcing）（这是 Fedora 和 Red Hat Enterprise Linux 的默认设置），SELinux 为你的 `httpd` 服务增加了另一层安全保护。从本质上说，SELinux 实际上保护服务免受破坏 `httpd` 守护进程的人的影响。SELinux 通过创建策略来实现：
- 拒绝访问未设置正确文件上下文的文件。对于 SELinux 中的 `httpd`，内容、配置文件、日志文件、脚本和其他 http 相关文件有不同的文件上下文。任何未设置正确上下文的文件都可以被 `httpd` 进程访问。
- 通过将此类功能的开关（Booleans）设置为关闭状态，防止不安全的功能（例如文件上传和明文身份验证）。你可以根据需要选择性地开启开关。
- 防止 `httpd` 守护进程访问非标准功能，正如默认端口之外的端口预期的那样。
SELinux 的描述包含在第 24 章“增强 Linux”。
关闭 SELinux 如果你发现 SELinux 导致了问题，可以将其设置为许可模式（missive）。这允许 SELinux 记录违规但不阻止。你可以通过编辑 `/etc/sysconfig/selinux` 文件并将 `SELINUX` 值设置为 `permissive` 来实现。

```ini
SELINUX=permissive
```

## 第四部分：成为 Linux 服务器管理员

位置是以标签的形式配置的，该标签包含位置类型和资源位置，其后是该位置的配置选项，并以结束标签结尾。这种形式通常被称为配置块，看起来与 HTML 代码非常相似。一种特殊类型的配置块被称为**位置块 (location block)**，用于将指令的范围限制在特定的文件或目录。这些块包含以下内容：

```
<locationstagifier>
(匹配指定符的对象的特定选项放在此块中)
</locationstagifier>
```

存在不同类型的的位置标签，并根据所指定的资源位置类型进行选择。起始标签中包含的指定符根据位置标签的类型进行处理。你通常使用和遇到的位置标签有 Directory（目录）、Files（文件）和 Location（位置），它们分别将指令的范围限制在特定的目录、文件或位置。
