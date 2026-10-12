
-   `defaultserver private`—允许禁用对 FTP 服务器的匿名访问。使用此命令字符串不会影响访客账户和真实用户的访问。

-   `deny [address-data] [message-file]`—允许拒绝来自与 address-data 参数指定的地址之一匹配的主机连接的客户端访问 FTP 服务器。此参数的格式可能如下：
    -   `[ip_address]`—单个 IP 地址。
    -   `[ip_address]:[netmask]`—带网络掩码的 IP 地址。
    -   `[ip_address]/[cidr]`—带 CIDR 数据的 IP 地址。
    -   `[nameserver]`—一个标识符，用于拒绝无法通过名称服务器解析为有效主机名的任何主机的访问。
    -   `@/[file-name]`—包含更多 address-data 参数的文本文件的绝对路径；每行一个。

    “message-file” 参数是横幅文件的绝对路径，当用户因此命令字符串而被拒绝访问 FTP 服务器时，该文件将被显示给用户。

-   `deny-email [email-address]`—允许 FTP 服务器将与 email-address 参数匹配的电子邮件地址视为无效。如果服务器上启用了 passwd-check 选项，这将阻止具有匹配电子邮件地址的用户登录 FTP 服务器。

-   `deny-gid [gid-range] [...]`—允许特定 GID 或 GID 范围被拒绝访问 FTP 服务器。gid-range 参数可以是单个 GID 或 GID 范围。GID 值可以使用其分配的名称（来自 /etc/group 文件）或其实际数值指定。所有数值 GID 值前面应加上 “%” 字符以标识它们。

-   `deny-uid [uid-range] [...]`—允许特定 UID 或 UID 范围被拒绝访问 FTP 服务器。uid-range 参数可以是单个 UID 或 UID 范围。UID 值可以使用其分配的名称（来自 /etc/passwd 文件）或其实际数值指定。所有数值 UID 值前面应加上 “%” 字符以标识它们。

-   `guestserver [hostname] [...]`—仅允许在此命令字符串中列出的主机进行匿名 FTP 访问。可以指定多个主机名，从而允许对多个主机进行匿名访问。如果未指定 hostname 参数，则拒绝所有连接主机的匿名 FTP 访问。

-   `limit [class-name] [max-users] [times] [message-file]`—允许在一天中的特定时间限制特定访问类中的同时用户数。class-name 参数指定正在限制的访问类。max-users 参数设置给定访问类的最大同时用户数。times 参数使用与 UUCP sys 文件中 times 相同的格式。message-file 将显示给因此命令字符串而被拒绝访问 FTP 服务器的用户。

-   `passwd-check none|trivial|rfc822 enforce|warn`—允许配置 FTP 服务器使用的密码检查级别。此命令字符串中的第一个参数指定应使用的密码检查类型。支持以下密码检查方法：
    -   none—禁用密码检查。
    -   trivial—密码必须包含 “@” 字符。
    -   rfc822—密码必须为符合 RFC822 的电子邮件地址。

    此命令字符串中的第二个参数指定当密码检查机制报告无效密码时应采取的操作。此选项可以设置为 warn，仅通知用户密码使用无效但允许其登录 FTP 服务器，或 enforce，通知用户密码无效并禁止访问服务器。

    ftpaccess 文件支持多种日志机制，在进行事后安全审计时很有用。这些日志机制的输出也可以作为自动化基于主机的入侵检测系统的输入。支持以下日志功能：

-   `loginfails [count]`—允许将重复登录失败消息日志的阈值设置设为用户可定义的值。此阈值值的默认设置是 5。这意味着当 FTP 客户端在一次特定会话中登录 FTP 服务器失败超过四次时，将向系统日志设施记录一条消息。

-   `log commands [keyword-list]`—允许将 FTP 用户发送的命令记录下来以供后续分析。keyword-list 参数是一个逗号分隔的关键字列表，允许为特定类型的 FTP 用户定义日志记录。支持 anonymous、guest 和 real 关键字。anonymous 关键字使此命令字符串仅适用于匿名 FTP 登录，guest 参数仅适用于访客账户，而 real 参数适用于登录 FTP 服务器的实际系统用户。

-   `log transfers [keyword-list] [direction-list]`—允许将 FTP 用户的文件传输记录下来以供后续分析。keyword-list 参数是一个逗号分隔的关键字列表，允许为特定类型的 FTP 用户定义日志记录。支持 anonymous、guest 和 real 关键字。anonymous 关键字使此命令字符串仅适用于匿名 FTP 登录，guest 参数仅适用于访客账户，而 real 参数适用于登录 FTP 服务器的实际系统用户。direction-list 参数是一个逗号分隔的方向关键字列表，允许此命令字符串应用于传入、传出或所有文件传输。支持的方向关键字为 incoming 和 outgoing。

-   `log security [keyword-list]`—允许将 FTP 用户违反系统安全规则的任何行为记录下来以供后续分析。keyword-list 参数是一个逗号分隔的关键字列表，允许为特定类型的 FTP 用户定义日志记录。支持 anonymous、guest 和 real 关键字。anonymous 关键字使此命令字符串仅适用于匿名 FTP 登录，guest 参数仅适用于访客账户，而 real 参数适用于登录 FTP 服务器的实际系统用户。

-   `log syslog`—将文件传输日志消息重定向到 syslog 设施而不是 xferlog 文件。这在尝试进行集中式日志存储以及将日志信息用作基于主机的入侵检测系统的输入时很有用。

    FTP 服务器上的用户访问级别和站点权限可以使用 ftpaccess 文件支持的选项进行控制。这些选项可用于创建用户类，每个用户类都有自己的可定义访问权限、受限文件/目录，甚至受限命令。

    支持以下权限选项：

-   `allowretrieve absolute;relative class=[class-name] [...] [file-name] [...]`—允许在原本会被标记为不可检索时，将 FTP 服务器上的文件指定为可由特定用户检索。此选项可用于允许用户下载特定文件，或与给定 file-name 参数匹配的所有文件。它会覆盖任何会导致指定文件无法访问的先前 noretrieve 语句。此命令字符串中可以指定多个 file-name 参数，格式如下：
    -   `filename`—指定服务器上名称与 filename 匹配的任何文件。
    -   `/path/filename`—使用目录和文件名说明符指定服务器上的特定文件。
    -   `/path/`—指定服务器上特定目录的内容。

    此命令字符串中的 absolute|relative 参数是可选设置，可用于指定指定的路径名应被视为绝对路径，还是相对于连接 FTP 客户端的 chroot 文件系统的路径。

    此命令字符串中的 class= 参数也是可选设置，可用于将文件下载访问权限授予特定用户类，而不是 FTP 服务器上的所有用户。可以给出多个 class= 参数，也可以不给出任何参数（导致所有用户都受 allowretrieve 命令字符串影响）。

-   `anonymous-root [directory] [user-class] [...]`—允许为特定用户类指定根目录。与此命令字符串中列出的任何类匹配的用户在登录 FTP 服务器时将自动被 chroot 到 directory。如果未指定用户类，则命令字符串用于指定未被赋予显式根目录指定的匿名用户的根目录。

-   `autogroup [group-name] [class-name] [...]`—允许在此命令字符串中指定的任何访问类中的用户自动将其有效组 ID 设置为与 group-name 参数匹配的 GID。这在基于组 ID 限制匿名用户的文件访问时很有用。

-   `byte-limit raw|in|out|total [max-bytes] [class-name]`—对 user-class 中的用户可传输的字节数应用限制。此限制可以设置为应用于发送的字节、接收的字节或两者。raw 参数是可选设置，允许使用此命令字符串限制原始流量而不是仅发送/接收的数据文件。如果未指定 user-class 参数，此设置将适用于未明确指定 byte-limit 配置设置的所有用户类。

-   `chmod yes|no [keyword-list]`—允许为特定用户类或用户类组授予或撤销 chmod 命令权限。keyword-list 是一个逗号分隔的关键字列表，允许为特定类型的 FTP 用户控制 chmod 访问。支持 anonymous、guest 和 real 关键字。anonymous 关键字使此命令字符串仅适用于匿名 FTP 登录，guest 参数仅适用于访客账户，而 real 关键字适用于登录 FTP 服务器的实际系统用户。

-   `class [class-name] [type-list] [address-data] [...]`—允许根据登录 FTP 服务器的用户类型和用户的源 IP 地址指定特定用户类。这在定义用户访问级别和权限时提供了高度的可配置性。此命令字符串中的 class-name 参数是用于标识用户类以便进一步应用选项的字母数字文本标识符。keyword-list 参数是一个
