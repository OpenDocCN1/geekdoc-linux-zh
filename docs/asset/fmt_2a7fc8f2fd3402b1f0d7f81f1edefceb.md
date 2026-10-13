
在之前的章节中，我描述了选择良好密码的重要性。如果你是唯一使用这台 Red Hat Linux 机器的人，验证上面使用的密码强度显然不是大问题。毕竟，你才是分配这些密码的人。

在多用户系统中，确保密码良好的任务更为复杂。如果你的 Red Hat Linux 服务器上有许多账户，某些用户会选择弱密码的概率几乎是肯定的。你如何确定你的用户使用的密码不是容易破解的？最好的方法是使用与破解者类似的工具，并尝试“破解”你系统上的密码。可能最好的工具就是这个名副其实的程序。

## 获取 Crack 包

有关 Crack 软件的通用信息，请阅读位于常见问题解答网页：`http://www.users.dircon.co.uk/~crypto/download/c50-faq.html`。可以通过 FTP 从 `ftp.cerias.purdue.edu` 的 `/pub/tools/unix/pwutils/crack/` 目录下载 Crack。在写作时，5 是 Crack 的当前版本。在这种情况下，需要的文件是 `crack5.tar.gz`。如果你在查看目录时发现了更高的版本号，请下载该新版本。

或者，你可以从服务器 `ftp.cert.dfn` 的 `/pub/tools/password/Crack/` 目录下下载 `Crack_5.0a.tar.gz` 文件。

一旦下载了文件，请使用 `tar` 命令进行解压。在包含下载文件的同一目录下，输入以下命令：

```
tar -xzvf crack5.0.tar.gz
```

来解压 Crack 程序包。它将在当前目录下创建一个名为 `c50a` 的目录。该目录将包含 Crack 程序以及 Crack 软件包运行所需的其他文件和目录。

要使用 Crack 5.0a 软件包，请按照以下步骤操作：

- 1. 使用网络浏览器，访问页面 `http://www.users.diron.co.uk/~crypto/download/c50-linux-util-makefile.txt`，并将该页面保存到你解压 Crack 软件包的目录下的 `c50a/src/util/Makefile` 文件中（如果目录不存在，请先创建）。你的浏览器可能会提示你替换现有的 `Makefile`。
- 2. 点击 yes 以用修复了编译问题的更新版本覆盖 `Makefile`。
- 3. 接下来，编译 Crack 软件包。将当前目录更改到 `c50a` 目录（使用 `cd` 命令），然后输入：

```
./Crack makeonly
```

将 Crack 软件包的源代码转换为可执行代码。
- 4. 接下来，你需要准备 Crack 在尝试破解密码时将使用的字典文件。使用以下命令完成：

```
./Crack -miedict
```

## 运行 Crack 命令

Crack 现在已准备好运行了。但在运行它之前，你必须使你的密码文件符合 Crack 可以读取的格式。实现此最简单的方法是运行 Crack 提供的 `shadmgrg.sv` 脚本。你必须以 root 身份运行脚本，因此请使用 `su` 命令获取 root 权限。`shadmgrg.sv` 脚本位于 Crack 主目录下的 `scripts` 目录。它会将合并后的密码数据打印到屏幕上，因此调用命令时你需要将输出重定向到文件：

```
./scripts/shadmgrg.sv > mypasswd
```

你现在应该回到命令行提示符了。新的 `mypasswd` 文件应该在当前目录下。遗憾的是，它仍然属于 root，除非你计划以 root 身份运行 Crack，否则你需要更改它。输入以下命令，将 `myname` 替换为你的实际登录名：

```
chown myname mypasswd
chmod 600 mypasswd
```

`chmod` 命令修改文件，使其所有者变为你而非 root。（请将 `myname` 替换为你的用户名）。`chmod` 命令更改了文件权限以便你可以读取它。**这极其重要！** 你必须更改此文件的权限，使其仅对你可读；否则，你就在你的系统上留下了一个安全漏洞。如果系统上的其他用户可以读取该文件，他们就可以复制该文件并针对自己运行 Crack。

最后，使用 `exit` 命令退出 root 壳，然后使用以下命令针对合并后的密码文件运行 Crack：

```
./Crack mypassword
```

这将启动密码破解过程，将其放入后台运行，并让你返回到命令行提示符。这并不意味着 Crack 已经完成。取决于文件的大小，破解密码文件可能需要几小时甚至几天。Crack 将在后台处理文件，并在完成后自动退出。你可以随时暂停、停止或检查 Crack 的进度。表 14-3 列出了你可能觉得有用的命令行。

| 表 14-3 | Crack 工具的不同选项 |
|---|---|
| 命令行 | 描述 |
| `./Crack mypassword` | 破解密码文件。 |
| `./Crack -mail mypassword` | 破解密码文件并向使用弱密码的用户发送电子邮件警告。 |
| `./Crack -nice 10 mypassword` | 以较低优先级运行 Crack，以免它拖慢系统。 |
| `./Crack -kill mypassword` | 终止当前的 Crack。 |
| `./Crack -recover mypassword` | 恢复异常中断的 Crack。 |
| `./Reporter` | 显示 Crack 的进度。 |

适用于您的情况。特别是，请将“插入您的系统管理员名称”行替换为相应人员名称、电子邮件和电话号码。

在调用 Crack 时，您可以组合多个参数。因此，如果您想以较低的（nice）优先级运行 Crack 以免拖慢系统，并且还想对使用密码错误的恶劣用户发送电子邮件，可以如下所示调用 Crack：

```
/Crack -nice 10 -email mypasswd
```

请务必阅读在线文档以获取更多关于 Crack 许多功能的信息。文档以文本和 HTML 格式存储在与 Crack 脚本相同的目录（`c50a` 目录）中。请查找 `manual.txt` 和 `manual.html` 文件。

## 通过过滤网络访问保护您的计算机

密码漏洞只是破解者可能利用以获取系统访问权限的潜在弱之一。Red Hat Linux 及其类 Unix 系统提供了多种网络服务，随之而来的是各种破解攻击的途径。了解这些服务以及如何访问它们至关重要。

那么，我说的网络服务是指什么？基本上，我指的是计算机执行的任何需要使用一组预定义的规则通过网络发送和接收的任务的任务路由电子邮件是一项网络服务。提供 Web 页面也是如此。您的 Linux 盒机具有提供数千项服务的潜力。其中许多列在 `/etc/services` 文件中。让我们来看该文件的片段：
