
# Anonymous access, and no incoming

```apache
<VirtualHost ftp.site1.org>
    ServerAdmin             ftpmaster@site1.org
    ServerName              "Site1 FTP Server"
    TransferLog             /var/spool/syslog/xfer/ftp.site1.org
    MaxLoginAttempts        3
    RequireValidShell       no
    DefaultRoot             /home/ftp/ftp.site1.org
    User                    site1
    Group                   site1
    AllowOverwrite          yes
    # Auth files...
    AuthUserFile       /var/conf/ftp/authfiles/passwd.ftp.site1.org
    AuthGroupFile      /var/conf/ftp/authfiles/group.ftp.site1.org
    <Anonymous /home/ftp/ftp.site1.org>
        User                  ftp
        Group                 ftp
        UserAlias             anonymous ftp
        RequireValidShell     no
        MaxClients            10
        <Limit WRITE>
            DenyAll
        </Limit>
    </Anonymous>
</VirtualHost>
```

# ftp.site2.org

# Anonymous ftp, and no incoming

```apache
<VirtualHost ftp.site2.org>
    ServerAdmin            ftpmaster@site2.org
    ServerName             "Site 2 FTP Server"
    TransferLog            /var/spool/syslog/xfer/ftp.site2.org
    MaxLoginAttempts       3
    RequireValidShell      no
    DefaultRoot            /home/ftp/ftp.site2.org
    User                   site2
    Group                  site2
    AllowOverwrite         yes
    # Auth files....
    AuthUserFile       /var/conf/ftp/authfiles/passwd.ftp.site2.org
    AuthGroupFile      /var/conf/ftp/authfiles/group.ftp.site2.org
    <Anonymous /home/ftp/ftp.site2.org>
        User                  ftp
        Group                 ftp
        UserAlias             anonymous ftp
        RequireValidShell     no
        MaxClients            10
        <Limit WRITE>
            DenyAll
        </Limit>
    </Anonymous>
</VirtualHost>
```

以井号（`#`）开头的行是注释行，ProFTPD 守护进程会忽略这些行。该文件可分析如下：

- 第2至25行定义了一个名为 `ftp.site1.org` 的虚拟主机。
- 第26至51行定义了第二个名为 `ftp.site2.org` 的虚拟主机。
- 第3行指定了第一个站点管理员的电子邮件地址。第3行还指定了当您连接到该服务器时横幅页面所显示的服务器名称。
- 第5行指定了第一个站点虚拟主机的传输日志文件的位置。
- 第8行指定了第一个站点的根目录。

> **注意：** 每个虚拟主机都有其私有的根目录和独立的传输日志文件。

- 第9行和第10行指定为这个虚拟主机服务的 ProFTPD 守护进程将以用户 `site1` 和组 `site1` 的身份运行。不用说，在设置虚拟站点时，必须定义所指定的用户和组。
- 第13行和第14行指定了 `AuthUserFile` 和 `AuthGroupFile` 的位置。`AuthUserFile` 指定一个备用密码文件，其格式与系统 `/etc/passwd` 文件相同。当指定该文件时，它用于身份验证和目录访问控制。

> **注意：** 备用密码文件不必位于 chroot 的目录结构中，即可用于匿名或普通登录。

- 第15至24行使用我们在上一节已经讨论过的指令定义了一个匿名 FTP 访问。
- 第25至51行定义了名为 `ftp.site2.org` 的第二个虚拟主机，并使用与定义 `ftp.site1.org` 时类似的指令。

有关 ProFTPD 配置选项的更多详细信息，请使用 `/usr/local/src/proftpd-1.2.0pre10/doc` 目录中的在线文档，或访问 ProFTPD 网站 `http://www.proftpd.net`。

### 有用的脚本

通常保存在 `xferlog` 文件中的数据很有价值，但难以使用。因为每次单独传输的文件都会按时间顺序记录在该文件中，所以仅通过阅读日志文件很难掌握服务器的使用情况。

WU-FTPD 包含一个名为 `xferstats` 的实用工具，用于分析和汇总存储在 `xferlog` 文件中的日志信息。`xferstats` 的输出包括以下信息：

- 传输的总字节数和日均字节数
- 每日统计
- 按每个服务器目录发送的文件和字节数的明细
- 每小时流量统计

`xferstats` 程序接受多个参数，包括 `-f filename` 用于指定 `xferlog` 文件的完整路径和文件名；`-r` 用于在统计中包含真实用户；`-a` 用于在统计中包含匿名用户；`-h` 用于生成每小时流量报告；`-d` 用于生成特定域名的流量报告；`-t` 用于按部分生成总流量报告。

以下是 `xferstats` 的示例输出：

```text
# xferstats -f /var/log/xferlog -r -a -h -t

TOTALS FOR SUMMARY PERIOD Sun Nov 7 1999 To Sat Nov 13 1999

Files Transmitted During Summary Period                  107

Bytes Transmitted During Summary Period                8217300

Systems Using Archiving                                  43

Average Files Transmitted Daily                          15

Average Bytes Transmitted Daily                      1173900
```
