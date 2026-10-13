
如果你的负载需要更好的管理并且检查服务器健康状况很重要，你最好的选择是使用新的 director 产品获取硬件解决方案，例如 Web Director（www.radware.com/）、Ace Director（www.alteon.com/）或 Local Director（www.cisco.com/）。我曾使用 Web Director 取得了巨大成功。

# 第 9 章

## 电子邮件服务

### 为 SMTP 服务器设置 DNS

DNS 配置中的邮件交换（MX）记录用于标识域的 SMTP 邮件服务器资源。假设你想将名为 `mail.yourdomain.com` 的主机指定为 `yourdomain.com` 域的 SMTP 邮件服务器。`yourdomain.com` 的起始授权（SOA）记录必须包含如下一行

```
IN MX preference-value mail-server-hostname.
```

其中 `preference-value` 是一个正整数，仅在你有多个 SMTP 邮件服务器时才有用。如果你只有一个 SMTP 邮件服务器，此数字可以是任意值。例如，以下设置将单个 SMTP 邮件服务器 `mail.yourdomain.com` 的首选项级别设置为 5：

```
IN MX 5 mail.yourdomain.com.
```

以下是在多服务器场景中的示例，其中首选项编号起着至关重要的作用：

```
IN MX 10 fast-mail-server.ad-engine.com.
IN MX 20 slow-mail-server.ad-engine.com.
```

当互联网上的任何人的 SMTP 邮件服务器想要向 `someone@ad-engine.com` 发送邮件时，它首先执行 DNS 查询以定位 `ad-engine.com` 的 MX 记录。返回给 SMTP 邮件服务器的 MX 记录将与刚才显示的相同。然后 SMTP 邮件服务器选择 `fast-mail-server.ad-engine.com` 作为投递的首选邮件服务器，因为它在两个可用服务器中具有更高的优先级（即较低的首选项编号）。

然后 SMTP 邮件服务器尝试使用端口 25 与 `fast-mail-server.ad-engine.com` 计算机建立 SMTP 连接。如果 `fast-mail-server.ad-engine.com` 服务器因任何原因不可用，则会选择 `slow-mail-server.ad-engine.com` 服务器进行投递。因此，拥有多个 MX 记录为你的邮件投递系统提供了冗余，如果电子邮件是组织中的关键部分，这非常重要。

![](img/c2419364ebb911c809b6a79991707c27_209_0.png)

#### 注意

在 MX 记录中始终使用具有自己的 A 记录的主机名。换句话说，不要在 MX 记录中使用主机别名。有关详细信息，请参阅 RFC 1123。

在使用适当的 MX 记录设置 DNS 后，按如下方式测试配置：
- 1. 从 shell 运行 `nslookup` 程序。
- 2. 当你在 `nslookup` 提示符下时，输入 `set q=mx` 以告诉 `nslookup` 你想要执行 MX 记录查询。
- 3. 输入你的域名。

如果你已按上述讨论配置了 DNS，你将看到之前创建的 MX 记录（s）。另一方面，如果你没有获得 MX 记录或 `nslookup` 返回错误，请修复你的 DNS 配置，重新启动 DNS 服务器并再次执行此测试。

### 设置 SMTP 邮件服务器

设置 SMTP 服务器的第一步是决定为你的 Red Hat Linux 系统使用哪个 SMTP 邮件服务器。有许多 SMTP 邮件服务器产品可用。然而，由于其悠久的全球部署历史，`sendmail` 脱颖而出。它也是 Red Hat Linux 的默认 SMTP 邮件服务器。因此，本章使用 `sendmail` 作为 SMTP 服务器。

### 安装 sendmail

就像你在 Red Hat 系统上安装的任何其他服务器软件一样，`sendmail` 以 RPM 包的形式提供。然而，你需要为 `sendmail` 安装多个 RPM 包：
- `sendmail-<version>.<architecture>.rpm`. 主要发行版
- `sendmail-cf-<version>.<architecture>.rpm`. `sendmail` 配置文件发行版
- `sendmail-config-<version>.<architecture>.rpm`. 辅助配置文件发行版
- `sendmail-doc-<version>.<architecture>.rpm`. 文档发行版

安装这些包非常简单；运行 `rpm -ivh package name` 安装每个包。

#### 提示

![](img/c2419364ebb911c809b6a79991707c27_210_0.png)

如果你在 Red Hat Linux 安装期间安装了旧版本的 `sendmail`，请在安装新版本之前删除 `sendmail` 包，因为它们可能不完全兼容。要卸载 RPM 包，请使用 `rpm -e package name` 命令。你也可以使用 `rpm -q partial package name` 命令来定位 RPM 包的确切包名。

安装包后，你就可以配置 `sendmail` 了。`sendmail` 的主要配置文件是 `/etc/sendmail.cf`。

### 启动和停止 sendmail

虽然你尚未配置 `sendmail` 服务器，但仍可以运行它。要手动启动 `sendmail`，请运行以下命令：

```
/usr/sbin/sendmail -q<queue processing interval>
```

用时间替换 `queue processing interval`。通常，时间以分钟或小时为单位指定。例如，要每 15 分钟处理一次邮件队列，使用 `-q15m`，或者要每小时处理一次队列，使用 `-q1h`。你也可以指定秒（s）、天（d）或周（w）。例如，要让 `sendmail` 每一个半小时处理一次队列，请指定 `-q1h30m`。

![](img/c2419364ebb911c809b6a79991707c27_211_0.png)

#### 提示

如果你没有全天候的互联网连接，你可以使用 `/usr/sbin/sendmail -bd -o DeliveryMode=d` 以延迟模式启动 `sendmail`，这样在下次通过 `/usr/sbin/sendmail -q` 运行之前会避免使用 DNS。如果你定期连接，可以将 `/usr/sbin/sendmail -q` 放入 `cron` 作业中，这样当你的连接可用时，队列会自动处理。

如果你希望 `sendmail` 在每次启动后自动启动，请从默认的运行级别目录创建一个符号链接（以 Sxx 开头，其中 xx 为数字）到 `/etc/rc.d/init.d/sendmail` 脚本。例如，要在多用户系统（运行级别 3）每次启动后运行 `sendmail`，我可以创建以下符号链接：

```
ln -s /etc/rc.d/init.d/sendmail
/etc/rc.d/rc3.d/S85sendmail
```

这确保 `sendmail` 在每次启动后自动启动。`/etc/rc.d/init.d/sendmail` 脚本使用 `-bd` 选项启动 `sendmail`。你可能希望修改 `/etc/rc.d/init.d/sendmail` 脚本以反映你站点的队列间隔要求。此外，你可能希望在以下行之前添加以下代码：

```
daemon /usr/sbin/sendmail -bd
```

在脚本中以便在启动时自动对配置文件运行 `newaliases` 和 `makemap`：

```
newaliases
for i in virtusertable access domaintable mailertable
do
if [ -f /etc/mail/$i ] ; then
echo "Making $i database for sendmail..."
makemap hash /etc/mail/$i < /etc/mail/$i
sleep 1
fi
done
sleep 1
```

这确保每次启动服务器进程时，所有配置数据库都会重建。

你也可以很方便地使用 `/etc/rc.d/init.d/sendmail` 脚本来启动、停止和重启 `sendmail`。要停止 `sendmail`，运行

```
/etc/rc.d/init.d/sendmail stop
```

要重启 `sendmail`，运行

```
/etc/rc.d/init.d/sendmail restart
```

你还可以通过使用 `-q` 选项强制 `sendmail` 立即处理其队列：

```
/usr/sbin/sendmail -q
```

如果你希望部分处理队列，可以使用 `-qString` 选项仅处理发件人地址包含指定字符串的消息队列。例如，以下命令强制 `sendmail` 处理发件人为 `kabir` 的所有排队邮件：

```
/usr/sbin/sendmail -qSkabir
```

当队列中有大量邮件等待时，这非常方便。
