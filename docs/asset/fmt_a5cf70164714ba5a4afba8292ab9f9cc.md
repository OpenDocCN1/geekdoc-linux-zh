
```
Oct 21 04:02:00 flyingpenguin CROND[11790]: (root) CMD (run-parts /etc/cron.daily)
Oct 21 04:02:00 flyingpenguin anacron[11794]: Updated timestamp for 'cron.daily' to 2020-10-21
Oct 21 04:02:26 flyingpenguin PAM_unix[11954]: (system-auth) session opened for user news by (uid=0)
Oct 21 04:02:29 flyingpenguin PAM_unix[11954]: (system-auth) session closed for user news
Oct 21 04:02:48 flyingpenguin sendmail[12018]: e9L82mE12018: from-root, size=440, cc=0, ncpts=1, msgid=<20010210248.e9L82mE2018@localhost>
```

`Dec 16 16:30:35 burgessmeredith login: LOGIN FAILURE ON /dev/ttyp5 FROM localhost`

`Dec 16 16:36:44 burgessmeredith deny host=tweety.cardinalconsulting.com/service=ipop3d`

异常系统事件 -----------

`Dec 16 16:32:40 burgessmeredith sshd[21624]: log: Connection from`

`Dec 16 16:32:44 burgessmeredith sshd[21624]: log: Password authentication for candace accepted.`

`Dec 16 16:32:48 burgessmeredith sshd[21624]: log: Closing connection to`

## 入侵后的损害控制与修复

一旦你检测到系统或网络被入侵，有几项措施是你需要立即采取。

### 关闭漏洞

完全将受损的系统从网络中断开连接。如果你让受损的系统留在网络上，入侵者可能仍然在那里，撤销你为修复损害所执行的所有操作。

寻找嗅探器程序的证据。黑客经常闯入并安装嗅探器来窃取用户账户和密码信息。

要确定你的系统上是否安装了嗅探器，请查看是否存在混杂模式的网络接口。通常情况下，你的网卡（NIC）只对发送给它的数据包感兴趣——它忽略所有其他数据包。然而，某些网络监控和管理软件能够将网卡设置为混杂模式，使其保留并显示每一个数据包。这类工具对于调试网络问题很有用，但它们应该仅供授权的网络管理员获取和使用。如果任何接口处于混杂模式，则你的系统上可能被安装了嗅探器。请注意，如果你在发现此类入侵后重启了机器，或在单用户模式下运行系统，你将无法检测到混杂接口。

使用 `ifstat` 程序检查系统上的所有网络接口，并报告所有接口是否处于调试或混杂模式。侧边栏“获取 ifstat 程序”显示了如何设置 `ifstat`，从在你还没有该程序时下载它开始。

### 获取 ifstat 程序

此示例使用终端窗口界面通过 FTP 下载 `ifstat` 程序。

```
root@flyingpenguin~# ftp ftp.cerias.purdue.edu
Connected to ftp.cerias.purdue.edu.
220-ftp.cerias.purdue.edu NcFTPd Server (free educational
license) ready.
220-    Welcome to the CERIAS Security FTP Archive
220-
220-Users must provide their e-mail addresses as passwords. All
activity
220-is logged and may be monitored. If you object to this, do not
log into
220-thisservice. Before downloading any tools, tips, tricks or other bits
220-of information from this site, please read and understand all
of the
220-implications of the information provided located in the root
directory.
220-    Limitation of Liability - README.liability
220-    Export Restrictions - README.export
220-    Copyright Notice - README.export
220-
KERBEROS_V4 rejected as an authentication type
Name (ftp.cerias.purdue.edu:miss_scarlet): anonymous
331 Guest login ok, send your complete e-mail address as
password:
230-
230-\            Purdue University
230-\            CERIAS Security Archive
230-
230-\            Center for Education and Research in
230-\            Information Assurance and Security
230-
230-\            Local time is Mon Oct 23 09:40:21 2000. User 15 of
100.
230-\            All transfers are logged with your host name and email
address. If you
230-\            don't like this policy, disconnect now!
230-\            For more information on CERIAS go to
http://www.cerias.purdue.edu
```

# 第 29 章 Linux 系统安全

匿名登录。

远程系统类型为 UNIX。

使用二进制模式传输文件。

`ftp > cd pub/tools/unix`

`"/pub/tools/unix"` 是新的工作目录。

Purdue University

CERIAS Security Archive

Center for Education and Research in

Information Assurance And Security

向 `security-archive@cerias.purdue.edu` 发送反馈

- crypto - 加密软件
- daemons - 守护进程。
- firewalls - 防火墙和防火墙配置工具
- ids - 入侵检测系统
- libs - 安全库
- logutils - 日志记录和日志管理工具
- netutils - 网络工具
- pwdutils - 密码工具
- scanners - 网络和主机扫描器
- sysutils - 系统工具

```
ftp > cd sysutils
"/pub/tools/unix/sysutils" 是新的工作目录。
ftp > cd ifstatus
"/pub/tools/unix/sysutils/ifstatus" 是新的工作目录。
ftp > ls
-rw-r--r-- 1 ftuser Jun 14 17:40 README.local
-rw-r--r-- 1 ftuser Jun 14 17:40 ifstatus.tar.gz
```

## 高级系统与网络管理

列表完成。

`ftp > mget *`

`mget README.local`

`mget ifstatus.tar.gz`

`ftp > close`

`ftp > bye`

`root@flyingpenguin# ls`

`ifstatus/`

- `Makefile`
- `generic.c`
- `ifstatus.c`
- `install.sh`
- `ifstatus.h`
- `ifsolaris.c`
- `ifsolaris.h`
- `ifstatus`
- `status`

`root@flyingpenguin#`

-- TCP/IP --

Time: Tue 15

Path: `/`

`.com`

`.edu`

`.org`

`.net`

`at.com`
