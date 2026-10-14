
当 Efax 正在等待传入传真时，你可以使用传真状态命令检查 Efax 守护进程的状态：

```text
$ fax status
USER       PID %CPU %MEM  SIZE   RSS TTY STAT START   TIME COMMAND
root       253  0.1  0.6   936    456 p0  S <   13:22  0:00 /usr/bin/efax -d/dev/
ttys0

from: /var/spool/fax/modem.253

```

```text
efax: 28:14 opened /dev/ttys0
efax: 28:16 waiting for activity
```

如果 Efax 正在作为守护进程运行以等待传入传真，你可以使用传真停止命令停止该守护进程。

> **提示**
>
> 如果你希望 Efax 在系统每次启动时进入等待模式，请将 `fax wait` 命令添加到系统的 `/etc/rc.d/rc.local` 启动文件中，守护进程将在每次启动时运行。

### 设置传真打印服务器

Efax 可以轻松地与你的打印假脱机程序集成，允许用户通过打印来发送传真。使用 Efax 配置传真打印服务器涉及三个步骤：

1. 配置打印机队列。
2. 准备 `faxlpr` 脚本。
3. 准备假脱机目录。

#### 配置打印机队列

要通过 Efax 打印到传真，请编辑你的 `/etc/printcap` 文件，为传真打印机队列创建一个条目，该条目使用输入过滤器将打印作业发送到 `faxlpr` 脚本。通常，此条目如下所示：

```text
fax:\
        :sd=/var/spool/fax:\
        :lp=/dev/null:\
        :if=/usr/bin/faxlpr:
```

此条目创建了一个名为 `fax` 的打印机队列，该队列使用打印假脱机目录 `/var/spool/fax`。`lp=/dev/null` 字段表示输入过滤器生成的任何输出都被发送到空设备，因此不会到达打印机。`if=/usr/bin/faxlpr` 字段表示 `lpr` 应将发送到此打印机的所有文件重定向到 `/usr/bin/faxlpr` 脚本。

#### 准备 `faxlpr` 脚本

传真脚本有一个特殊属性。如果它以名称 `faxlpr` 被调用，则假定你正在尝试通过 lpd 打印机守护进程发送传真，而不是在命令行上发送。

这意味着你需要创建一个名为 `faxlpr` 的指向传真脚本的链接，以便它可以以该名称作为打印机队列的输入过滤器被调用。使用 `ln` 命令创建链接：

```bash
# ln /usr/bin/fax /usr/bin/faxlpr
```

#### 准备假脱机目录

在 `/etc/printcap` 文件中创建的打印机队列使用假脱机目录 `/var/spool/fax`。你需要检查此目录是否存在，如果不存在，则使用适当的权限（全局可读和可写）创建它：

```bash
# mkdir /var/spool/fax
# chmod 777 /var/spool/fax
```

假脱机目录需要一个锁定文件，该文件对所有用户可读，但仅对 root 用户可写。按如下方式创建此文件：

```bash
# touch /var/spool/fax/lock ; chmod 644 /var/spool/fax/lock
```

#### 通过打印机队列发送传真

将 Fax 配置为接受通过打印机队列 `fax` 的打印作业后，你可以通过将文档打印到该队列来通过传真发送文档。为此，你需要使用 `lpr` 命令的 `-J` 选项指定目标电话号码：

```bash
$ lpr -Pfax -J 14165551212 <file to fax>
```

任何使用 `lpr` 打印并向打印机生成 PostScript 输出的应用程序都可以通过这种方式打印到传真队列。

通过利用 Linux 打印到远程打印队列的功能，你可以使用此打印服务器为网络提供打印服务。为此，需要以下步骤：

1. 确保你的传真服务器系统具有必要的安全设置，以允许每个需要使用传真服务器的客户端进行打印。这通过使用 `hosts.allow`、`hosts.equiv` 和 `hosts.lpd` 文件来完成，如第 18 章“一般安全问题”中所述。
2. 在每个需要打印到传真打印队列的客户端系统上，将以下条目添加到 `/etc/printcap`：

```text
fax:\
    :sd=/var/spool/lpd/fax:\
    :mx#0:\
    :sh:\
    :rm=<fax server host name>:\
    :rp=fax:
```

- 3. 在每个将打印到传真队列的客户端系统上，创建假脱机目录 `/var/spool/lpd/fax`。

### 使用 Qfax 扩展 Efax

尽管 Efax 可以轻松用于为小型企业和工作组部署传出传真服务器，但它缺少构建更强大、大规模传真服务器所需的一些关键功能。其中一些缺失功能由 Qfax 软件包提供：

- 通过电子邮件发送传出传真
- 自动生成封面页
- 对传出传真进行假脱机处理

#### 安装 Qfax

Qfax 的当前版本是 1.3，可从 `http://metalab.unc.edu/pub/Linux/apps/serialcomm/fax/qfax1.3.tar.gz` 获取文件 `qfax1.3.tar.gz`。下载该文件并使用以下命令将其解压到方便的位置：

```bash
tar zxvf qfax1.3.tar.gz
```

Qfax 会被解压到当前目录中，因此请确保你正位于想要放置源代码发行版的确切目录中。Qfax 不会解压到当前目录的子目录中。

解压 Qfax 之后，安装需要以下几个步骤：

- 1. 创建传真用户。
- 2. 创建 FaxMaster 邮件别名。
- 3. 创建电子邮件到传真网关。
- 4. 为传真创建假脱机目录。
- 5. 创建传真配置目录。
- 6. 配置 Qfax。
- 7. 指定特权用户。
- 8. 编辑 `fax.rc` 文件。
- 9. 创建 `fax.db` 文件。
- 10. 创建 `.fax` 文件。
- 11. 编译并安装 Qfax。
- 12. 安排传真队列处理。

这些步骤假定你已经安装并配置好了 Efax。

> **提示**
>
> 如果你想在网络环境中使用 Efax，你可能需要在 Sendmail 服务器上安装 Efax、Qfax 和传真调制解调器，该服务器将处理你网络中用户发送的所有邮件消息。

#### 创建传真用户

安装 Qfax 时，它会以非 root 用户身份运行 Efax，这在单用户系统上并不常见。相反，Efax 应配置为以 uucp 用户身份运行。uucp 用户在大多数 Linux 系统上都很常见。然而，这个名称在脚本中不太容易识别和使用。因此，比较方便的做法是创建第二个用户 `fax`，其用户 ID 和组 ID 与系统上的 uucp 用户相同。例如，如果你的 uucp 用户在 `/etc/passwd` 中的条目是：

```
uucp:*:10:15:UUCP Agent:/usr/lib/uucp:/bin/false
```

那么你需要在 `/etc/passwd` 文件中添加以下条目：

```
fax:*:10:15:Fax Agent:/var/spool/fax:/bin/false
```

请注意，该帐户的主目录是你的传真假脱机目录，这将在安装过程的后续步骤中发挥作用。

要将此条目添加到 `/etc/passwd` 文件中，你可以使用 `vipw` 命令编辑该文件，该命令会在你的默认文本编辑器中安全地打开该文件。

#### 创建 FaxMaster 邮件别名

Qfax 将出于管理目的向 FaxMaster 邮件帐户生成消息。要在 sendmail 系统上创建此别名，你需要在 `/etc/aliases` 文件中添加一个条目。该条目的格式如下：

```
FaxMaster: <user name>
```

用户名应该是接收 Qfax 发送到 FaxMaster 邮件别名的所有电子邮件的用户的名称。

当条目位于 `/etc/aliases` 文件中并保存该文件后，你需要使用 `newaliases` 命令重建 sendmail 别名数据库。

#### 创建电子邮件到传真网关

Qfax 期望由电子邮件生成的传出传真使用 `<person>@<company>.fax` 的形式来寻址。为了使其正常工作，sendmail 需要知道如何重定向发送到 `.fax` 域的传真。

这需要三个步骤：

- 1. 创建地址重写规则。
- 2. 创建邮件程序定义。
- 3. 绕过名称服务。

#### 创建地址重写规则

`/etc/sendmail.cf` 文件包含一系列称为规则集 0 的规则，如第 16 章“使用 sendmail 的 Linux 邮件服务”中所讨论的。在本节中，你会看到一系列与错误消息相关的消息，包括几个 `$#error` 条目，例如：
