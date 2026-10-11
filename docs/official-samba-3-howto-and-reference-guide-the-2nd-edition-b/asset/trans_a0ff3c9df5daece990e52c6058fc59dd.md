

你的 UNIX 打印子系统！该路径通常指向一个目录，该目录对所有人可写，并设置了 *sticky*（粘滞）位。

- **browseable = no**：如果 *printable* = yes，则始终设置为 *no*。它使 *[printer]* 共享本身在 **net view** 命令或资源管理器浏览列表中的可用共享列表中不可见。（当然，你仍能看到各个单独的打印机。）

- **guest ok = yes**：如果此参数设置为 *yes*，则连接打印机服务时无需密码。将授予以 *guest*（来宾）*account*（账户）权限进行访问。在许多系统中，*guest* 账户将映射到名为 "nobody" 的用户。通常，该用户会在 UNIX passwd 文件中以空密码出现，但没有有效的 UNIX 登录权限。在某些系统中，*guest* 账户可能没有打印权限。你可以通过使用 **su - guest** 以 *guest* 用户身份登录并运行系统打印命令（例如）来测试此权限：
  ```
  lpr -P printname /etc/motd
  ```

- **public = yes**：是 *guest ok* = yes 的同义词。由于我们已经设置了 *guest ok* = yes，因此实际上不需要在此处重复设置。（这引出了一个有趣的问题：“如果我无意中为同一个共享设置了两个相互矛盾的选项怎么办？”答案是，Samba 采纳最后遇到的那个设置。**testparm** 不会抱怨同一个共享中同一参数的不同设置。你可以通过为 *guest* *account* 参数设置多行不同的用户名，然后运行 testparm 来查看 Samba 实际使用的是哪一个，从而测试这一点。）

- **read only = yes**：通常（对于其他类型的共享）阻止用户在共享目录中创建或修改文件。然而，在 *printable* 服务中，如果用户权限允许连接，则*始终*允许向该目录写入（仅通过打印暂存操作）。不允许普通的写入操作。

- **writable = no**：是 *read only* = yes 的同义词。

### 20.4.1.3 任何 [*my_printer_name*] 部分

如果在 **smb.conf** 文件中出现了一个包含参数 *printable* = yes 的 [*my_printer_name*] 部分，Samba 会将其配置为打印机共享。如果共享名称超过八个字符，Windows 9x/Me 客户端在连接或加载打印机驱动程序时可能会遇到问题。不要将打印机共享命名为可能与现有用户或文件共享名称冲突的名称。在客户端连接请求中，Samba 总是先尝试查找具有该名称的文件共享。如果找到了，它将连接到该文件共享，而不会连接到同名打印机！

- **comment = Printer with Restricted Access**：注释说明了一切。
- **path = /var/spool/samba_my_printer**：将此打印机的暂存区域设置为除默认目录之外的其他目录。设置不同路径并非必需，但提供了此选项。
- **printer admin = kurt**：与此明确定义的打印机共享相比，一般 *[printers]* 共享中的打印机管理员定义有所不同。这并非要求，我们这样做只是为了展示这是可能的。
- **browseable = yes**：这使得打印机可被浏览，以便客户端在浏览 **Network Neighborhood**（网络邻居）时可以方便地找到它。
- **printable = yes**：参见第 20.4.1.2 节。
- **writable = no**：参见第 20.4.1.2 节。
- **hosts allow = 10.160.50., 10.160.51.**：这里我们通过使用 *hosts allow* 和 *hosts deny* 参数来实施一定程度的访问控制。这绝不是一个安全的赌注。这不是保护打印机的方法。该行在访问控制的第一阶段评估中接受来自特定子网的所有客户端。
- **hosts deny = turbo_xp, 10.160.50.23, 10.160.51.60**：列出的所有主机均不被允许（即使它们属于被允许的子网）。正如你所见，你可以在此处使用 IP 地址或 NetBIOS 主机名。
- **guest ok = no**：此打印机不对来宾账户开放。

### 20.4.1.4 打印命令

在每个定义打印机的部分（或在 *[printers]* 部分）中，可以定义一个 *print command* 参数。它设置了一个命令，用于处理放置在 Samba 该打印机打印暂存目录中的文件。（如果你还记得，该暂存目录是通过 *path* 参数设置的）。通常，此命令将使用合适的系统打印命令将暂存文件提交到 Samba 主机的打印子系统中。但这并非强制要求。出于调试或其他原因，你可能希望执行与打印文件完全不同的操作。一个例子是一个命令，它将打印文件复制到临时位置以便在需要调试打印时进一步调查。如果你自己创建打印命令（甚至开发打印命令 shell 脚本），请确保注意从 Samba 暂存目录中删除文件的需求。否则，你的硬盘可能会很快因空闲空间不足而受到影响。

### 20.4.1.5 默认 UNIX 系统打印命令

你之前了解到，如果 Samba 在其配置文件中找不到明确陈述的设置，它在大多数情况下会针对许多参数使用其内置设置。*print command* 也是如此。默认打印命令取决于 *printing* 参数设置的变化。在表 20.1 列出的命令中，你会注意到一些形式为 `%X` 的参数，其中 `X` 是 *p, s, J* 等。这些字母分别代表打印机名称、暂存文件和作业 ID。它们在表 20.1 中得到了更详细的解释，该表概述了主要打印选项，但排除了 CUPS 的特殊情况，CUPS 支持在第 21 章 “CUPS Printing Support” 中讨论。

表 20.1 默认打印设置

| 设置 | 默认打印命令 |
| :--- | :--- |
| *printing = bsd, aix, q, p* | 打印命令为 *lpr -r -P%p %s* |
| *printing = svsv, hpx* | 打印命令为 *lp -c -P%p %s; rm %s* |
| *printing = qnx* | 打印命令为 *lp -P%p -s %gs* |
| *printing = bsd, aix, p, q* | lpq 命令为 *lpq -P%p* |
| *printing = svsv, hpx* | lpq 命令为 *lps -o%p* |
| *printing = qnx* | lpq 命令为 *lpq -P%p* |
| *printing = bsd, aix, p, q* | lprm 命令为 *lprm -P%p %c* |
| *printing = svsv, hpx* | lprm 命令为 *cancel %p-%j* |
| *printing = qnx* | lprm 命令为 *cancel %p-%j* |
| *printing = bsd, aix, p, q* | lpause 命令为 *lp -i %c -p %j -H hold* |
| *printing = svsv, hpx* | lpause 命令 (...为空) |
| *printing = qnx* | lpause 命令 (...为空) |
| *printing = bsd, aix, p, q* | lpresume 命令为 *lp -i %c -p %j -H resume* |
| *printing = svsv, hpx* | lpresume 命令 (...为空) |
| *printing = qnx* | lpresume 命令 (...为空) |

对于 *printing = CUPS*，如果 Samba 是针对 libcups 编译的，它将使用 CUPS API 来提交作业。（如果你的 *cupsd.conf* 被设置为将其自动生成的 printcap 文件写入不寻常的位置，也建议设置 *printcap = cups*）。否则，Samba 映射到 System V 打印命令，带有 -oraw 选项用于打印；也就是说，它使用 *lp -c -d%p -oraw; rm %s*。如果使用 *printing = cups*，并且 Samba 是针对 libcups 编译的，那么任何手动设置的打印命令都将被忽略！

### 20.4.1.6 自定义打印命令

在打印作业完成向服务暂存后，Samba 将通过 *system()* 调用使用 *print command* 来处理暂存文件。通常，指定的命令将把暂存文件提交到主机的打印子系统中。但并没有要求必须如此。打印子系统可能不会自行删除暂存文件，因此无论你指定什么命令，都应确保在处理完暂存文件后将其删除。

在传统打印系统中使用自定义打印命令没有困难。然而，如果你不想自己编写，你应该充分了解 Samba 为每个打印子系统使用的默认内置命令（参见表 20.1）。在最后几段列出的所有命令中，查看形式为 %X 的参数。这些是宏或快捷方式，用作实际对象名称的占位符。在运行带有此类占位符的命令时，Samba 会自动插入适当的值。打印命令可以处理所有 Samba 宏替换。就打印而言，以下这些具有特殊相关性：

- %s, %f — 暂存文件名的路径。
- %p — 相应的打印机名称。
- %J — 客户端传输的作业名称。
- %c — 暂存作业的已打印页数（如果已知）。
- %z — 暂存打印作业的大小（以字节为单位）。

打印命令必须至少包含一次 %s 或 %f。%p 是可选的。如果未提供打印机名称，%p 将从打印命令中静默删除。在这种情况下，作业将发送到默认打印机。

如果在 [global] 部分中指定，给定的打印命令将用于任何未指定自身打印命令的可打印服务。如果既没有为可打印服务指定打印命令，也没有全局打印命令，则暂存文件将被创建但不会被处理！最重要的是，打印文件将不会被删除，因此它们将占用磁盘空间。

在使用 nobody 账户时，某些 UNIX 系统上的打印可能会失败。如果发生这种情况，请创建一个替代的来宾账户并赋予其打印权限。在 [global] 部分中使用 guest account 参数设置此来宾账户。

你可以形成相当复杂的打印命令。你需要意识到，打印命令只是传递给 UNIX shell。shell 能够像往常一样展开包含的环境变量。（在 Samba 打印命令中包含 UNIX 环境变量 Variable 的语法是 %$Variable。）为了给你一个可用的打印命令示例，以下命令会将打印作业记录到 /tmp/print.log，打印该文件，然后将其删除。分号 (";") 是 shell 脚本中命令的常用分隔符：

```
print command = echo Printing %s >> /tmp/print.log; lpr -P %f -z %p %s; rm %s
```

根据你通常在系统上如何打印文件，你可能需要使你的命令与此示例有很大不同。print command 参数的默认值取决于 printing 参数的设置。另一个例子是：

```
print command = /usr/local/samba/bin/myprintscript %p %s
```

