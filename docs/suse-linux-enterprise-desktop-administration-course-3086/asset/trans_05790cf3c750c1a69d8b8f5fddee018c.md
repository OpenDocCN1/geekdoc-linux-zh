

+   c. 使用密码 nove11 以 geeko 身份登录。
+     Geeko Novell 的 Novell iFolder 页面出现，其中列出了 OES Documents iFolder。
+   d. 从列表中选择 OES Documents；然后选择 Marketing Documents。
+   e. 选择 oes_intro.sxi 文件。
+     出现 Opening oes_intro.sxi 对话框。
+   f. 确保已选择 Open with oooimpress (default)；然后选择 OK。
+   g. 关闭 Downloads 对话框。
+     经过片刻，Novell Open Enterprise Server: Adding Value to Open Source 幻灯片演示在 OpenOffice.org Impress 演示软件中出现。
+   h. （可选）通过选择 Slide Show > Slide Show 显示幻灯片（按 Esc 返回 Impress）。
+   i. 通过选择 File > Exit 关闭 OpenOffice.org Impress。
+   j. 通过选择 Log Out（右上角）退出 Novell iFolder。
+     你将被返回到 Novell iFolder 登录屏幕。
+   k. 关闭 Firefox Web 浏览器窗口。

## Summary

-   跨平台 LDAP 目录服务允许网络用户查询用于各种用途的信息，包括用户身份验证和信息存储。SUSE Linux 使用 OpenLDAP 提供 LDAP 服务。
-   LDAP 资源组织成层次树结构。每个资源（叶对象）存储在一系列容器对象中，可以使用 DN 或 RDN 访问。
-   YaST 可用于配置客户端连接到 LDAP 服务。
-   NFS 服务器使用 RPC 和 portmapper 服务将目录共享给 NFS 客户端。然后 NFS 客户端将共享的 NFS 目录挂载到远程计算机上的本地目录。
-   你可以使用 YaST 或通过编辑 /etc/fstab 文件来配置计算机连接到远程 NFS 共享目录。
-   Automounter 服务可用于自动将远程 NFS 服务器上的主目录挂载到本地目录。你可以将 Automounter 配置存储在 LDAP 目录服务中。
-   Windows 网络通常使用 Active Directory 服务通过 LDAP 和 Kerberos 提供集中身份验证和资源访问。
-   Winbind 守护进程用于将 SUSE Linux 与 Active Directory 环境集成。Active Directory Kerberos 票证由 SUSE Linux 客户端上的 PAM 模块处理。
-   你可以使用 YaST 配置 SUSE Linux 系统以使用 Active Directory。你还应确保系统使用 NTP 具有正确的时间，转发到 Active Directory DNS 服务器，并且没有活动的防火墙。然后你可以使用 GDM、KDM 或 `ssh` 命令登录到 Active Directory 域。
-   你可以使用 Samba 与 Windows 计算机共享文件和打印机资源。Samba 使用 `smbd` 和 `nmbd` 守护进程以及 `/etc/samba/smb.conf` 文件中的条目来模拟 Windows 网络上使用的 SMB 和 NetBIOS 协议。
-   Windows 计算机上大多数共享资源都使用 NetBIOS 名称通过 UNC 访问。`nmblookup` 命令可用于测试 NetBIOS 名称解析。
-   Nautilus 可用于创建 Samba 共享以及访问网络上的 Windows 共享。你还可以使用 `mount` 和 `smbclient` 命令连接到 Windows 或 Samba 共享。
-   Novell 网络通常使用 eDirectory 服务通过 LDAP 提供集中身份验证和资源访问。eDirectory 用户帐户可以使用 LUM 或 Novell iManager 管理。你可以在 SUSE Linux 安装期间或使用 YaST 配置 LUM。Novell iManager 必须使用 Web 浏览器访问。
-   要访问所有 eDirectory 服务，必须在 SUSE Linux 系统上配置 Novell Client for Linux。你可以使用 YaST 或使用自定义配置文件配置 Novell Client for Linux。
-   你可以通过在图形桌面环境中单击 Novell Client 系统托盘应用程序来访问 Novell Client for Linux。
-   Novell iFolder 可用于在安装了 iFolder 客户端并创建了 iFolder 帐户的 Linux 和 Windows 系统之间共享文件。你可以轻松加密并控制对 iFolder 共享文件的访问。

## Key Terms

-   **/etc/auto.master** Automounter 配置文件。
-   **/etc/fstab** 一个用于在系统初始化时自动挂载文件系统的文件。
-   **/etc/nsswitch.conf** 一个列出服务在 Linux 系统上访问信息所使用的方法的文件。
-   **/etc/opt/novell/ncl** 存储 Novell Client 配置文件的一个目录。
-   **/etc/samba/smb.conf** Samba 主配置文件。
-   **/etc/samba/smbfs tab** 一个包含 Samba 文件系统挂载选项的文件。
-   **/opt/novell/ifolder3/bin/ifolder** iFolder 客户端程序。
-   **/opt/novell/ncl/bin/ncl_tray** Novell Client 系统托盘应用程序。
-   **/usr/sbin/automount** SUSE Linux 中的 Automounter 程序。
-   **Active Directory (AD)** Windows 网络上使用的目录服务。
-   **attributes** LDAP 对象中包含的属性。
-   **autofs** SUSE Linux 中的 Automounter 软件包。
-   **autofs daemon** SUSE Linux 中的 Automounter 守护进程。
-   **Automounter** 一个自动将远程资源连接到本地目录的系统服务。
-   **container object** 用于组织叶对象的 LDAP 对象。
-   **directory** 包含有关资源（如用户帐户）的信息的数据库。
-   **Directory Information Tree (DIT)** LDAP 数据库的层次结构。
-   **directory service** 可用于查询目录获取信息的服务。
-   **distinguished name (DN)** LDAP 叶对象的完整路径名。
-   **Domain Name System (DNS)** 互联网上使用的命名系统。每个主机由主机名和域名标识。
-   **Dynamic Host Configuration Protocol (DHCP)** 用于在网络上向主机分配 TCP/IP 配置信息的协议。
-   **eDirectory** Novell 网络上使用的目录服务。
-   **entry** LDAP 对象的引用。
-   **firewall** 限制主机计算机上某些网络流量的服务。
-   **GNOME Display Manager (GDM)** GNOME 桌面环境使用的登录屏幕。
-   **iFolder** 参见 Novell iFolder。
-   **iFolder Client** 安装在 iFolder 客户端上的软件组件，可用于连接和管理共享文件。
-   **iManager** 参见 Novell iManager。
-   **insserv command** 用于在系统初始化时配置守护进程启动的命令。
-   **K Display Manager (KDM)** KDE 桌面环境使用的登录屏幕。
-   **Kerberos** UNIX、Linux 和 Windows 目录服务使用的安全身份验证协议。Kerberos 使用票证来识别已身份验证的计算机和服务。
-   **Key Distribution Center (KDC)** 用于签发 Kerberos 票证的计算机。
-   **Konqueror** KDE 桌面中使用的图形文件管理实用程序。
-   **leaf object** 表示网络资源的 LDAP 对象。
-   **Lightweight Directory Access Protocol (LDAP)** 用于提供中央身份验证并将信息分发到网络计算机的协议。
-   **Lightweight Directory Interchange Format (LDIF)** 用于创建、修改和查询 LDAP 数据库中对象的文件的格式。
-   **Linux User Management (LUM)** 一种管理套件，旨在管理 SUSE Linux 计算机上的本地和基于目录的用户帐户。
-   **Name Service Switch (NSS)** 提供 Linux 系统上名称服务信息的软件组件。
-   **Nautilus** SUSE Linux 中使用的默认图形文件管理实用程序。
-   **NetBIOS** 使用唯一的 15 字符计算机名来标识网络主机的 Windows 协议。
-   **NetWare Core Protocol (NCP)** Novell NetWare 系统在网络上使用的应用层协议。
-   **Network File System (NFS)** UNIX 和 Linux 系统使用的文件共享协议。
-   **Network Information Service (NIS)** 允许 Linux 和 UNIX 配置集中的服务。
-   **Network Time Protocol (NTP)** 用于从互联网上的时间服务器获取时间信息的协议。
-   **NFS client** 使用 NFS 协议访问 NFS 服务器上导出文件的计算机。
-   **NFS Lock Manager (NLM)** 提供 NFS 文件锁定的内核模块。
-   **NFS server** 使用 NFS 协议托管（导出）文件的计算机。
-   **nmbd** Samba 软件包中的 NetBIOS 守护进程。
-   **nmblookup command** 显示主机 NetBIOS 计算机名的命令。
-   **Novell Client for Linux** 可用于访问 Novell 网络服务的 SUSE Linux 软件组件。
-   **Novell iFolder** 可由 Windows 和 Linux 系统使用的安全文件共享系统。
-   **Novell iManager** 可用于管理目录用户帐户的基于 Web 的实用程序。
-   **Novell Modular Authentication Services (NMAS)** Novell 网络使用的安全分布式身份验证系统。
-   **novfs.ko** Novell Client for Linux 使用的内核模块。
-   **novfsd** Novell Client for Linux 使用的守护进程。
-   **object** LDAP 数据库的组件。两种主要对象类型是容器对象和叶对象。
-   **object class** LDAP 数据库中对象的一种类型。
-   **OpenLDAP** SLES 中使用的 LDAP 服务。
-   **OpenSLP** SUSE Linux 系统使用的 SLP 实现。
-   **passwd command** 用于更改 Linux 和 AD 密码的命令。
-   **Pluggable Authentication Modules (PAM)** 处理应用程序身份验证访问系统的 Linux 软件组件。PAM 还可以与 Kerberos 协议一起工作。
-   **portmapper** 提供 Linux 中 RPC 的服务。
-   **relative distinguished name (RDN)** LDAP 中对象的简单名称。
-   **Remote Procedure Call (RPC)** 在远程计算机上执行的例程。
-   **rpcinfo command** 显示 RPC 端口及其关联服务的命令。
-   **Samba** Linux 中的一组服务，提供 SMB 和 NetBIOS 协议以便与 Windows 计算机进行文件和打印机共享。
-   **schema** LDAP 数据库的对象和对象属性列表。
-   **Secure Shell (SSH)** 提供到远程计算机的加密 shell 会话的软件服务。
-   **Server Message Block (SMB)** Windows 系统使用的文件和打印机共享协议。
-   **Service Location Protocol (SLP)** Novell 网络使用的网络浏览协议。
-   **shares** Windows 或 Samba 计算机上的共享目录或打印机。
-   **smbclient command** 用于查看和访问 Windows 和 Samba 文件和打印机共享的命令。
-   **smbd** Samba 守护进程。
-   **ssh command** 用于从远程 SSH 服务器获取 shell 的命令。
-   **ticket granting ticket (TGT)** 在成功身份验证请求后授予已身份验证计算机的 Kerberos 票证。

