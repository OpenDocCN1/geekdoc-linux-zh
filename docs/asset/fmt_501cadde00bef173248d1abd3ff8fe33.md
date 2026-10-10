
正如您所见，`Tripwire` 准确显示了哪些文件被修改以及这些文件属于哪些规则。如果这些修改是可以接受的，您可以保留报告中相应部分的 'x' 标记（表示选中）并退出编辑器。`Tripwire` 将会更新数据库。例如，如果您保留这两个文件的 x 标记，当下次运行完整性检查器时，它将不会发现这些违规，因为 `Tripwire` 数据库已经更新以纳入这些修改过的文件。然而，如果上述某个修改并非预期且看起来可疑，那么 `Tripwire` 就完成了它的工作！

**提示** 如果您想查看 `/var/lib/tripwire/report` 目录中的报告，您可以随时运行 `/usr/sbin/twprint -m r --twfile reportfilename` 命令。

## 以自动化方式运行 Tripwire 以检测完整性

您还可以通过创建一个小的脚本来将 `Tripwire` 作为 cron 任务运行，例如清单 23-7 中所示的脚本。

### 清单 23-7: /etc/cron.daily/tripwire-check

```sh
#!/bin/sh

HOST_NAME=`uname -n`

if [ ! -e /var/lib/tripwire/${HOST_NAME}.twd ]; then
    echo "***     错误: 未找到 $HOST_NAME 的 Tripwire 数据库。 ***"
    echo "*** 请运行 \"/etc/tripwire/twinstall.sh\" 和/或 \"tripwire --init\"。 ***"
else
    test -f /etc/tripwire/tw.cfg &&  /usr/sbin/tripwire --check
fi
```

该脚本检查 `Tripwire` 数据库文件是否存在；如果存在，脚本然后查找配置文件，找到后以非交互模式运行 `/usr/sbin/tripwire` 命令。这将生成一个报告文件，如果您配置了一个或多个使用 `emailto` 属性的规则，电子邮件将会发送给相应的人员。

## 更新 Tripwire 数据库

每当文件系统中发生更改，若不同步更新数据库将产生误报时，您需要更新 `Tripwire` 数据库。例如，如果您修改了配置文件，或移除了 `Tripwire` 正在为您“监控”的程序，`Tripwire` 将生成违规报告。因此，每当您有意更改某些内容时，必须通过重新初始化数据库（使用 `/usr/sbin/tripwire --init` 命令）或使用 `/usr/sbin/tripwire --update` 命令简单更新数据库来更新数据库。更新方法应该能为您节省一些时间，因为它不需要重新创建整个数据库。

同样，当您更改 `Tripwire` 策略文件 `/etc/tripwire/tw.pol` 时，需要更新数据库。再次，与其使用 `--init` 选项重新初始化整个数据库，您可以使用 `/usr/sbin/tripwire --update-policy /etc/tripwire/tw.pol` 命令指示程序应用策略更改并更新数据库。

在创建 `Tripwire` 数据库后，每次更新策略文件时都需要更新数据库。与其每次更改（或实验）策略文件时都重新初始化数据库，您可以运行 `tripwire --update-policy /etc/tripwire/tw.pol` 命令来更新数据库。这将节省大量时间。

## 通过电子邮件获取 Tripwire 报告

如果您在规则中使用 `emailto` 属性，您可以从 `Tripwire` 接收违规（甚至非违规）报告。如果您将 `Tripwire` 检查作为 cron 任务运行，这特别有用（参见本章前面“以自动化方式运行 Tripwire 以检测完整性”部分）。

在从 `Tripwire` 接收电子邮件之前，您必须配置 `/etc/tripwire/twcq.txt` 文件中的电子邮件设置，并使用 `/usr/sbin/twadmin --create-cfgfile /etc/tripwire/twcq.txt` 命令重建配置文件。控制电子邮件的设置在表 23-4 中有解释。

| 属性 | 含义 | |
|---|---|---|
| `MAILMETHOD = SMTP \| SENDMAIL` | 默认: `MAILMETHOD = SENDMAIL` | 此属性用于设置 `Tripwire` 使用的邮件传输方法。默认设置允许 `Tripwire` 使用 `Sendmail` 守护进程，这必须使用稍后讨论的 `MAILPROGRAM` 属性指定。由于大多数流行的 `Sendmail` 替代邮件守护程序（如 `qmail` 和 `postfix`）的工作方式与 `Sendmail` 非常相似，您仍然可以将此项设置为 `SENDMAIL`，并使用 `MAILPROGRAM` 指定您的替代守护程序的路径。然而，如果您在运行 `Tripwire` 程序的机器上没有运行 `Sendmail` 或类似 `Sendmail` 的守护程序，您可以将此属性设置为 `SMTP`，并指定 `SMTPHOST` 和 `SMTPPORT` 编号属性。假设 `SMTPHOST` 允许您的系统中继消息，`Tripwire` 将通过 `SMTP` 端口连接到主机并传递消息，这些消息稍后将由主机传递到适当的目的地。 |
| `SMTPHOST = 主机名 \| IP 地址` | 默认: 无 | 此属性允许您指定邮件服务器的主机名。仅当在运行 `Tripwire` 的同一系统中没有邮件功能时才使用此属性。您可以使用 `nslookup -qmx yourdomain.in` 命令查找邮件服务器的 IP 或主机名。 |
| `SMTPPORT = 端口号` | 默认: 无 | 此属性指定远程邮件服务器的 TCP 端口号。通常，应将其设置为 25。只有当您将 `MAILMETHOD` 设置为 `SMTP` 时才需要此属性。 |

| 属性 | 含义 |
| --- | --- |
| `MAILPROGRAM = /path/to/mail/program` | 默认：`MAILPROGRAM = /usr/sbin/sendmail -oi -t` |

该属性指定邮件守护进程的路径以及运行它所需提供的任何参数。只有在使用 `MAILMETHOD = SENDMAIL` 时，此属性才有意义。

| 属性 | 含义 |
| --- | --- |
| `EMAILREPORTLEVEL = 0 - 4` | 默认：`EMAILREPORTLEVEL = 3` |

该属性指定通过电子邮件报告的信息级别。请保持默认设置不变。

| 属性 | 含义 |
| --- | --- |
| `MAILNOVIOLATIONS = true \| false` | 默认：`MAILNOVIOLATIONS = true` |

如果您希望在不检测到违规行为时不接收电子邮件，请将其设置为 `false`。

要测试您的电子邮件设置，您可以运行 `Tripwire`，并使用 `/usr/sbin/tripwire -m t -email your@emailaddr` 命令。别忘了将 `your@emailaddr` 更改为您自己的电子邮件地址。

## 使用 Linux 入侵检测系统 (LIDS) 保护 Apache

*Root（根用户）是所有恶意的根源。* 上述陈述可能只对全世界的 Unix/Linux 系统管理员有意义。一旦确认存在未授权的 root 访问，损害控制似乎就无望了，或者完全取决于入侵者的仁慈。

在标准的 Linux 系统中，几个子系统通常处于未受保护状态。文件系统往往像西部荒野一样开放。系统中有许多重要文件，如 `/bin/login`，因为未受保护，常被黑客利用。如果黑客入侵，他可以上传修改后的登录程序版本作为 `/bin/login`，以便未来自由访问系统。但事实是，像 `/bin/login` 这样的文件（即程序）不需要频繁变更（如果变更的话）；因此，它们绝不能处于未受保护状态。与文件系统类似，运行中的进程也未受保护。许多进程以 root 权限运行，这意味着当使用缓冲区溢出等技巧进行利用时，入侵者将获得系统的完全 root 访问权限。

降低 root 用户的权限可以增强系统安全性。`LIDS` 做到了这一点。实际上它还做了很多其他事情。它在内核中实现了一个非常低级别的安全模型，以提供安全防护、事件检测和事件响应功能。例如，`LIDS` 可以：

- 保护重要文件和目录免受未授权访问，无论它们位于哪种本地文件系统上。选定的文件和目录可以保护，防止 root 用户修改，这意味着未授权的 root 访问不会将入侵者变成我们所有人都害怕的超级大恶。
- 保护重要进程，防止任何人（包括 root 用户）终止它们。同样，这降低了 root 用户的能力。
- 防止未授权程序进行原始 I/O 操作。它还可以保护硬盘的主引导记录 (MBR)。

`LIDS` 可以检测某人使用端口扫描器扫描您的系统，并可通过电子邮件通知系统管理员扫描事件。`LIDS` 还可以在注意到任何施加规则的违规时通知系统管理员。当某人违反此类规则时，`LIDS` 可以在 `LIDS` 保护的防篡改日志文件中记录关于违规的详细消息。事实上，`LIDS` 不仅可以记录并发送关于检测到违规的电子邮件，它还可以立即关闭用户的交互式会话！

`LIDS` 是一个内核补丁和管理工具套件，从 Linux 操作系统内核内部增强安全性。因为在 `LIDS` 安全模型中，主体、对象和访问类型都在内核中，所以它被称为参考监视器。`LIDS` 项目网站是 www.lids.org/about.html。

`LIDS` 使 Linux 系统能够运行定制的内核，您必须从可靠的内核网站（如 www.kernel.org）获取最新的内核源代码。在下载并将内核解压到 `/usr/src/linux` 后，下载适用于您想要使用的特定内核的 `LIDS` 补丁。例如，如果您使用的是内核 2.4.1，请确保从 `LIDS` 项目网站下载 `LIDS` 补丁。通常 `LIDS` 补丁和管理工具包被称为 `lids-x.x.x.y.y.tar.gz`，其中 `x.x.x` 代表 `LIDS` 版本号，`y.y.y` 代表内核版本（例如，`lids-1.0.5-2.4.1`）。在以下说明中，我针对内核 2.4.1 使用 `LIDS` 1.0.5。请根据需要更改版本号。使用 `tar xvfz lids-1.0.5-2.4.1.tar.gz` 命令将 `LIDS` 源发行版解压到 `/usr/local/src` 目录。现在您可以准备修补内核了。

> 确保 `/usr/src/linux` 指向您下载的最新内核源代码发行版。您可以简单运行 `ls -l /usr/src/linux` 来查看符号链接指向哪个目录。如果它指向旧的内核源代码，使用 `rm -f /usr/src/linux` 删除链接，并使用 `ln -s /usr/src/linux-version /usr/src/linux` 重新链接，其中 `version` 是您下载的内核版本。例如，`ln -s /usr/src/linux-2.4.1 /usr/src/linux` 将最新的内核 2.4.1 源代码链接到 `/usr/src/linux`。

### 使用 LIDS 修补、编译和安装内核

要为您的系统编译 `LIDS`，您需要应用 `LIDS` 补丁后重新编译 Linux 内核。此过程描述如下：

1. 作为 root，将 `LIDS` 补丁包解压到您选择的合适目录。我通常将在本地编译软件的源代码放在 `/usr/local/src` 目录中。在这些步骤中，我假设您也这样做；如果不使用相同的目录，请对说明进行适当修改。因此，从 `/usr/local/src` 目录，运行 `tar xzvt lids-1.0.5-2.4.1.tar.gz` 命令。这将创建一个名为 `lids-1.0.5-2.4.1` 的新子目录。
2. 更改目录到 `/usr/src/linux`，并运行 `patch -p < /usr/local/src/lids-1.0.5-2.4.1.patch` 命令来修补内核源代码发行版。
3. 从 `/usr/src/linux` 目录运行 `make menuconfig` 命令以启动基于菜单的内核配置程序。您也可以使用 `make config` 或 `make xconfig` 命令来配置内核，但我更喜欢第一个，并假设您也使用它。
4. 从主菜单选择 `Code maturity level options` 子菜单，通过按空格键选择 `Prompt for development and/or incomplete code/drivers` 选项。退出此子菜单。
5. 转到 `General setup` 子菜单，选择 `Sysctl support` 并退出子菜单。
6. 从主菜单选择 `Linux Intrusion Detection System` 子菜单，只有完成第 4 步和第 5 步时才会出现此子菜单。此子菜单应列在主菜单底部，因此您可能需要向下滚动一点。
7. 从 `LIDS` 子菜单选择 `Linux Intrusion Detection System support (EXPERIMENTAL) (NEW)` 选项。您将看到如下所示的选项列表。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_719_0.png)

8. 对于受管理对象、受保护对象、ACL 主体/对象和受保护进程的默认限制，对于大多数系统应该是合适的。因此，请保持原样。
9. 如果您希望 `LIDS` 在用户违反安全规则时断开控制台，请选择 `Hang up console when raising a security alert` 选项。
10. `LIDS` 在启动过程中启用，因此您可能会先运行其他程序。如果您希望在 `LIDS` 保护启用之前执行程序时发出安全警报，请选择 `Security alert when executing unprotected programs before sealing LIDS` 选项。选择此选项后，您可以通过使用 `Do not execute unprotected programs before sealing LIDS` 选项来选择完全禁用未保护程序的执行机会。我不建议在启动期间完全禁止未保护程序，除非您绝对确定您在启动期间想要运行的所有内容（即所有工具、守护进程等）都受保护，并且不会停止正常的启动过程。
11. 启用 `Try not to flood logs (NEW)` 选项，并保持两个相同条目日志记录之间的默认 60 秒延迟，以维护日志文件的理智和大小。
12. （可选）如果您想允许切换 `LIDS` 保护，请选择 `Allow switching LIDS protections` 选项。如果这样做，您可以通过选择 `Number of attempts to submit password`、`Time to wait after a fail (seconds)`、`Allow remote users to switch LIDS protections`、`Allow any program to switch LIDS protections` 或 `Allow reloading config. file` 的值进一步自定义。我的偏好如下所示。

    ```text
    [*]  Allow switching LIDS protections (NEW)
    (3)  Number of attempts to submit password (NEW)
    (3)  Time to wait after a fail (seconds) (NEW)
    [*]  Allow remote users to switch LIDS protections (NEW)
    [ ]  Allow any program to switch LIDS protections (NEW)
    [*]  Allow reloading config. file (NEW)
    ```

13. 您肯定要选择 `Port Scanner Detector in kernel` 选项，以便您可以检测潜在入侵者的端口扫描，以及 `Send security alerts through network` 选项。保持第二个选项的默认值不变。
14. 保存您的内核配置，并运行以下命令来编译新内核及其模块（如果有的话）。

    ```make
    make depend
    make bzImage
    make modules
    make modules_install
    ```

**注意** 如果您编译的内核版本比当前系统运行的版本更新，那么您可能需要备份 `/lib/modules/current-version` 目录，其中 `current-version` 是指当前内核版本。例如，如果您正在编译版本 2.4.1，并且系统已经在运行 2.4.1，那么您应该运行 `cp -r /lib/modules/2.4.1 /lib/modules/2.4.1.bak` 命令来备份当前模块。如果新内核出现问题，您可以删除损坏内核的模块，并将该目录重命名回原始名称。

1. 现在使用 `cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz-lids-1.0.5-2.4.1` 命令，将新创建的 `/usr/src/linux/arch/i386/boot/bzImage` 内核映像复制到 `/boot/vmlinuz-lids-1.0.5-2.4.1`。
2. 向 `/etc/lilo.conf` 文件添加以下内容：

   ```text
   image=/boot/vmlinuz-lids-1.0.5-2.4.1
      label=lids
      read-only
      root=/dev/hda1
   ```
