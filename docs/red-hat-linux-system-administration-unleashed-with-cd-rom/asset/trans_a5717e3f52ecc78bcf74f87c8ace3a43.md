
-   **主机名 [host-name]**—指定 FTP 服务器要使用的默认主机名。host-name 参数是所要使用 的主机名。此值如果为同一台机器上的虚拟 FTP 服务器设置主机名则可以被覆盖。如果未使用主机名命令字符串，FTP 服务器将默认为其安装所在机器的主机名。

-   **电子邮件 [email-address]**—指定 FTP 站点管理员的电子邮件地址。email-address 参数是所要使用的电子邮件地址。

-   **别名 [alias-name][directory]**—指定 FTP 服务器上目录的别名。别名允许指定逻辑目录，可以从 FTP 服务器上的任何其他目录进入。别名只能由 cwd（更改工作目录）FTP 命令利用。

-   **关闭 [shutdown-file]**—允许定义一个文件来指定 FTP 服务器何时应自动关闭。使用关闭文件可在计划关闭前指定的时间间隔内拒绝服务器的新入站连接，并终止现有连接。关闭文件的格式如下：

[year] [month] [day] [hour] [minute] [deny-offset]
[term-offset [message]]—year 参数可以是 1970 年之后任意年份。month 参数可以是 0 到 11 的任意月份。day 参数可以是 0 到 30 的任意日期。hour 参数可以是 0 到 23 的任意小时。minute 参数可以是 0 到 59 的任意分钟。deny-offset 参数指定在服务器关闭前拒绝新入站连接访问的时间偏移量。其格式为 HHMM（2 位小时，2 位分钟）。term-offset 参数指定在服务器关闭前断开现有 FTP 连接的时间偏移量。其格式为 HHMM（2 位小时，2 位分钟）。message 参数指定在 FTP 服务器关闭时要向用户显示的消息。

wu-ftpd 软件包完全能够在一台主机上支持多个并发的虚拟 FTP 服务器。这可以通过启用 IP 别名（绑定到单个网络设备的额外 IP 地址）来实现。Red Hat Linux 支持多种配置 IP 别名的机制，其中最简单的是 Linuxconf 管理工具。使用此程序，您可以快速为特定网络设备添加 IP 别名。别名也可以通过命令行使用 ifconfig 程序添加。使用 ifconfig 配置别名时，命令的格式如下：

```bash
# ifconfig <interface>:<alias #> <command>
```

示例：ifconfig eth0:1 address 192.168.1.55

一旦您在主机上配置了所需的别名 IP 地址，您就可以通过在 ftpaccess 文件中使用配置指令，在 wu-ftpd 软件包内配置虚拟 FTP 服务器。这些指令允许 FTP 守护进程支持多个虚拟 FTP 站点，每个站点都有自己的横幅和目录层次结构。ftpaccess 文件支持以下与虚拟 FTP 服务器配置相关的选项：

-   **虚拟 [address] 根 [root-dir]**—允许指定特定虚拟 FTP 服务器的根目录。address 参数指定其根目录被设置的虚拟服务器，root-dir 参数是绝对路径名，指向用作虚拟服务器根目录的目录。
-   **虚拟 [address] 横幅 [banner-file]**—允许向连接到特定虚拟 FTP 服务器的客户端显示横幅。横幅在连接到服务器后、用户登录前显示。address 参数指定其横幅被设置的虚拟 FTP 服务器。banner-file 参数指定绝对路径名（相对于 FTP 服务器机器的实际根目录），指向要显示的横幅文件。
-   **虚拟 [address] 日志文件 [log-file]**—指定用于存储特定虚拟 FTP 服务器生成的日志数据的文件。这允许系统上的每个虚拟服务器将其日志数据输出到单独的文件。address 参数指定其日志文件被设置的虚拟 FTP 服务器。log-file 参数指定绝对路径名，指向要记录到的日志文件。
-   **虚拟 [address] 主机名 [host-name]**—指定系统上托管的特定虚拟 FTP 服务器要使用的主机名。address 参数指定其选项被修改的虚拟服务器。host-name 参数是所要使用 的主机名。
-   **虚拟 [address] 电子邮件 [email-address]**—指定系统上托管的特定虚拟 FTP 服务器的 FTP 站点管理员的电子邮件地址。address 参数指定其选项被修改的 FTP 服务器。email-address 参数是所要使用的电子邮件地址。
-   **虚拟 [address] 允许 [username] [...]**—允许将对特定虚拟 FTP 服务器的访问授予系统上的单个真实用户或访客用户。通常，真实用户和访客用户被拒绝访问托管其用户账户的系统上运行的虚拟服务器。当用户被视为访客并且被 chroot 到虚拟服务器的根目录时，或当用户通过 allow 指令被明确允许访问时，则并非如此。username 参数指定被授予虚拟服务器访问权限的用户。可以给出多个 username 参数，或使用用户名 '*' 来授予系统上所有用户的虚拟服务器访问权限。

-   **虚拟 [address] 拒绝 [username] [...]**—允许拒绝系统上单个真实用户或访客用户对特定虚拟 FTP 服务器的访问。此语句通常用于在通过 allow * 语句授予所有用户访问权限后，撤销特定用户的访问权限。username 参数指定被授予虚拟服务器访问权限的用户。如有必要，可以给出多个 username 参数。
-   **虚拟 [address] 私有**—允许禁用对特定虚拟 FTP 服务器的匿名访问。使用此命令字符串不会影响账户和真实用户的访问。

多个 wu-ftpd 相关信息的互联网资源可供 wu-ftpd 社区使用。这些包括电子邮件列表和 WWW 站点。

要订阅 wu-ftpd 邮件列表，请执行以下操作：

1.  向 listproc@mail.wustl.edu 发送电子邮件消息。
2.  此消息的主题字段应为空。
3.  此消息的主体字段应包含以下文本：
    `SUBSCRIBE WU-FTPD your-full-name`

要取消订阅 wu-ftpd 邮件列表，请执行以下操作：

1.  向 listproc@mail.wustl.edu 发送电子邮件消息。
2.  此消息的主题字段应为空。
3.  此消息的主体字段应包含以下文本：
    `UNSUBSCRIBE WU-FTPD`

要向订阅 wu-ftpd 邮件列表的所有用户发送邮件，请执行以下操作：

1.  向 wu-ftpd@mail.wustl.edu 发送电子邮件消息。
2.  此消息的主题和正文字段由用户自行决定。

wu-ftpd 邮件列表也以归档摘要格式通过 FTP 和 WWW 提供。

-   WWW Archive:
    `http://landfield.com/wu-ftpd/mail-archive`
-   WWW Archive Search Engine:
    http://www.landfield.com/wu-ftpd/mail-archive/search.html
-   FTP Archive:
    ftp://ftp.landfield.com/wu-ftpd/mail-archive

还有多个 wu-ftpd 信息的互联网资源。它们是

-   Kent Landfield's wu-ftpd site:
    http://www.landfield.com/wu-ftpd/
-   Academ wu-ftpd page:
    http://www.academ.com/academ/wu-ftpd/
-   CERT (Computer Emergency Response Team) guidelines for systems that allow anonymous FTP access:
    ftp://ftp.cert.org/pub/tech_tips/anonymous_ftp_config

## 使用 WU-FTPD 配置匿名 FTP

您可以通过安装单个 RPM 的简单过程，在 Red Hat 6 Linux 上使用 wu-ftpd 服务器允许匿名 FTP 访问。但是，在投入使用之前，必须正确保护任何新创建的匿名 FTP 服务器。

要配置 FTP 服务器以允许匿名访问，请执行以下操作：

1.  如果尚未成为 root，请成为 root。
2.  安装 anonftp RPM。这可以在 RedHat 安装阶段完成，也可以使用以下命令（从 RedHat 6 CD-ROM 的 RPMS 目录执行）：

```
# rpm -Uvh anonftp-2.8.1-1386.rpm
```

在某些情况下，可能需要一个 incoming 目录，以便用户可以将文件上传到 FTP 服务器。此类可写目录通常不被需要，因为它们可能为 warez 活动（盗版受版权保护的计算机软件）和其他非法软件交易活动提供可能性。如果绝对有必要创建 incoming 目录，建议以这样的方式设置目录权限，即匿名用户即使可以写入目录，也无法查看目录的内容。这有助于防止非法活动的发生，但不是 100% 万无一失的技术。要按上述方式创建 incoming 目录，请执行以下操作：

