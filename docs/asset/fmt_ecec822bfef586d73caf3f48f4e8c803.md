
```
; 这是起始记录 (SOA) 记录。与正向查找表相同。
@ mydomain.name. postmaster.mydomain.name. (
1990811 ; 序列号
3600 ; 1 小时刷新
300 ; 5 分钟重试
172800 ; 2 天过期
43200 ) 12 小时最小

; 列出使用的名称服务器。其他区域未解析的条目将转到你的 ISP 名称服务器。
IN NS mydomain.name.
IN NS isp.domain.com.

; 如你所示，只要它们属于 123.12.* B 类，我们就可以映射我们的其他 C 类
40.41 PTR spock.mydomain.name.
41.41 PTR mail.mydomain.name.
42.41 PTR kirk.mydomain.name.
24.42 PTR tsingtao.mydomain.name.
250.42 PTR redstripe.mydomain.name.
24.43 PTR kirin.mydomain.name.
66.64 PTR sapporo.mydomain.name.

; 反向查找文件中不应列出别名（规范）名称（显而易见）。
```

任何需要映射不同 B 类地址（例如 126.27*）的反向查找文件都可以创建，其格式与上面的示例反向查找文件相似。

- 5. 确保 `named` 守护进程正在运行。该进程通常在系统启动时从 `/etc/rc.d/init.d/named` 文件启动。你也可以手动启动和停止进程；分别输入 `named start` 和 `named stop`。

- 6. 每当对 DNS 表进行更改时，应通过输入 `/etc/rc.d/init.d/named restart` 重启 DNS 服务器。然后你可能希望使用 `nslookup` 等工具查询你添加或更改的机器来测试你的更改。

# 第 7 章 自定义配置与管理问题

关于配置 DNS 服务的更多信息可以参考“DNS-HOWTO”指南：http://metalab.unc.edu/Linux/HOWTO/DNS-HOWTO-5.html。

## 7.3. 使用 TACACS 进行 Internet 用户身份验证

在我工作的单位，对于拨号 Internet 用户（他们连接到我们的调制调器池，调制调器池连接到到 Cisco 250x 访问服务器）进行 TACACS 认证，我们使用的是 Vikas 版本的“tacacssd”。

编译并安装 Vikas 包后，最新版本可以从 ftp/ftp.navya.com/pub/vikas 获取；我不认为该包有 RPM 格式提供，您应该在 `/etc/inetd.conf` 文件中添加以下条目，以便当接收到 TACACS 请求时，`inetd` 进程会加载该守护进程。

```
# TACACS 是一种用于 Cisco 路由器产品的用户认证协议。
tacacs dagram udp root /etc/tacacssd tacacssd c /etc/tacacssd-conf
```

接下来，您应该编辑 `/etc/tacacssd-conf` 文件并根据系统需要进行自定义（不过，您可能可以直接使用默认设置）。

> 注意：如果您正在使用影子密码（详见第 6.6 节），您在使用此包时会遇到一些问题。遗憾的是，Red Hat 用于用户认证的 PAM（可插认证模块）不受此包的支持。我使用的一种变通方法是在 `/usr/local/tacacs/etc/` 中保留一个独立的“passwd”文件，它与 `/etc/` 中的文件匹配，但不非影子加密。这有点麻烦，如果您选择这样做，请务必对另一个密码文件设置权限，以确保只有 root 可读取：

```
chmod a-wr,u+r /usr/local/tacacs/etc/passwd
```

如果您确实使用了影子密码，那么您肯定需要编辑 `/etc/xtacsd-conf` 文件以及非影子密码文件的位置（假设您使用了上述建议的变通方法）。

下一步是配置您的访问服务器，使用 TACACS 对所需设备（如拨号调制调器）的登录进行认证。以下是实现此操作的示例会话：

```
mail:/tftpboot# telnet xyzrouter

Escape character is '^'.
User Access Verification
Password: ****
xyzrouter# enable
Password: ****
xyzrouter# config terminal
Enter configuration commands, one per line. End with CNTL/Z.
xyzrouter(config)# tacacs-server attempts 3
xyzrouter(config)# tacacs-server authenticate connections
xyzrouter(config)# tacacs-server extended
xyzrouter(config)# tacacs-server host 123.12.41.41
xyzrouter(config)# tacacs-server notify connections
xyzrouter(config)# tacacs-server notify enable
xyzrouter(config)# tacacs-server notify logouts
xyzrouter(config)# tacacs-server notify slip
xyzrouter(config-line)# line 2 10
xyzrouter(config)# login tacacs
xyzrouter(config)# exit
xyzrouter# write
Building configuration...
[OK]
xyzrouter# exit
```

Connection closed by foreign host.

所有 TACACS 活动日志消息将记录在 `/var/log/messages` 中供您查阅。

## 7.4. 使用 Samba 提供 Windows 风格的文件和打印服务

Linux 可以使用 Samba 包提供 SMB 服务（例如 Wf、Win95 和 NT 风格的网络文件和打印共享）。本节将描述如何配置共享以及如何从客户端机器访问它们。

Samba 包包含在 Red Hat 发行版中，您可以通过输入命令检查其是否已安装以及版本：

```
rpm -q samba
```

如果尚未安装，您将需要使用 RPM 工具进行安装。具体方法请参阅第 10.1 节。

您应该关注的最重要的 Samba 文件有：

- `/etc/smb.conf`：Samba 配置文件，在其中设置共享和其他配置参数（见下文）

- `/var/log/samba/`：Samba 日志文件的位置

- `/home/samba/`：建议的文件共享设置位置。然而，您应该选择一个文件系统上有足够空间来容纳您要存储的文件。个人而言，我通常设置一个挂载在 `/archive/` 的大分区，并将共享放在这里。

`/etc/smb.conf` 文件包含了有关文件和打印共享的配置信息。文件的前几行包含全局配置指令，这些指令适用于所有共享（除非按共享进行覆盖），随后是共享部分。

在许多情况下，Samba 安装自带的默认 `smb.conf` 文件即可满足您的需求，仅需少许更改。

以下是该文件的示例（我对其深度自定义，以向您展示一些最重要且有趣的选项）：

```
# 适用于所有共享的项（除非按共享进行覆盖）
[global]
  # 客户端空置 X 分钟后断开连接
  # 以避免消耗
  # 资源。大多数客户端将自动
  # 重新连接，因此启用它是一个好主意。
  dead time = 10
```
