

```
root# /usr/local/samba/sbin/winbindd -B
```

我通常比较谨慎，喜欢确保守护进程确实在运行。

```
root# ps -ae | grep winbindd
```

如果守护进程正在运行，该命令应产生如下输出。

```
3025 ?       00:00:00 winbindd
```

现在，进行真正的测试，尝试获取关于 PDC 上用户的一些信息：

```
root# /usr/local/samba/bin/wbinfo -u
```

这应该回显您 PDC 上 Windows 用户的列表。例如，我得到以下响应：

- CEO\Administrator
- CEO\burdell
- CEO\Guest
- CEO\jt-ad
- CEO\krtbgt
- CEO\TsInternetUser

显然，我将我的域命名为“CEO”，我的 winbind 分隔符是“\”。你可以做类似的事情来获取 PDC 的组信息：

```
root# /usr/local/samba/bin/wbinfo -g
```

- CEO\Domain Admins
- CEO\Domain Users
- CEO\Domain Guests
- CEO\Domain Computers
- CEO\Domain Controllers
- CEO\Cert Publishers
- CEO\Schema Admins
- CEO\Enterprise Admins
- CEO\Group Policy Creator Owners

现在可以使用函数 `getent` 来获取本地和 PDC 用户及组的统一列表。尝试以下命令：

```
root# getent passwd
```

你应该得到一个列表，看起来像是你的 /etc/passwd 列表，后面跟着具有新 UID、GID、主目录和默认 shell 的域用户。

对组也可以做同样的事情，使用以下命令：

```
root# getent group
```

## 23.5.3.6 修复 init.d 启动脚本

**Linux** winbindd 守护进程需要在 smbd 和 nmbd 守护进程运行后启动。为了完成这项任务，你需要修改系统的启动脚本。在 Red Hat Linux 中，它们位于 /etc/init.d/smb；在 Debian Linux 中，它们位于 /etc/init.d/samba。编辑你的脚本以添加命令，以便按正确的顺序调用此守护进程。我的启动脚本直接从 /usr/local/samba/bin 目录启动 smbd、nmbd 和 winbindd。脚本中的 start 函数如下所示：

```
start() {
    KIND="SMB"
    echo -n "Starting $KIND services: "
    daemon /usr/local/samba/bin/smbd $SMBDOPTIONS
    RETVAL=$?
    echo
    KIND="NMB"
    echo -n "Starting $KIND services: "
    daemon /usr/local/samba/bin/nmbd $NMBDOPTIONS
    RETVAL2=$?
    echo
    KIND="Winbind"
    echo -n "Starting $KIND services: "
    daemon /usr/local/samba/sbin/winbindd
    RETVAL3=$?
    echo
    [ $RETVAL -eq 0 -a $RETVAL2 -eq 0 -a $RETVAL3 -eq 0 ] && \
        touch /var/lock/subsys/smb || RETVAL=1
    return $RETVAL
}
```

如果你想以双守护进程模式运行 winbindd，请将上面的行替换为：

```
daemon /usr/local/samba/sbin/winbindd
```

替换为：

```
daemon /usr/local/samba/sbin/winbindd -B
```

**stop** 函数有一个对应的条目来关闭服务，如下所示：

```
stop() {
KIND="SMB"
echo -n $"Shutting down $KIND services: "
killproc smbd
RETVAL1=$?
echo
KIND="NMB"
echo -n $"Shutting down $KIND services: "
killproc nmbd
RETVAL2=$?
echo
KIND="Winbind"
echo -n $"Shutting down $KIND services: "
killproc winbindd
RETVAL3=$?
[ $RETVAL -eq 0 -a $RETVAL2 -eq 0 -a $RETVAL3 -eq 0 ] && \
rm -f /var/lock/subsys/smb
echo ""
return $RETVAL
}
```

**Solaris** Winbind 在 Solaris 9 上不起作用；详情请参阅第 41.6.2 节。

在 Solaris 上，你需要修改 /etc/init.d/samba.server 启动脚本。它通常只启动 smbd 和 nmbd，但现在也应该启动 winbindd。如果你将 Samba 安装在 /usr/local/samba/bin，该文件可能包含类似以下内容：

```
##
## samba.server
##

if [ ! -d /usr/bin ]
then # /usr not mounted
    exit
fi

killproc() {                # kill the named process(es)
    pid=`/usr/bin/ps -e |
        /usr/bin/grep -w $1 |
        /usr/bin/sed -e 's/^ *//' -e 's/ .*//'`
    [ "$pid" != "" ] && kill $pid
}

# Start/stop processes required for Samba server

case "$1" in
'start')
    #
    # Edit these lines to suit your installation (paths, workgroup, host)
    #
    echo Starting SMBD
    /usr/local/samba/bin/smbd -D -s \\
    /usr/local/samba/smb.conf

    echo Starting NMDB
    /usr/local/samba/bin/nmbd -D -l \\
    /usr/local/samba/var/log -s /usr/local/samba/smb.conf

    echo Starting Winbind Daemon
    /usr/local/samba/sbin/winbindd
    ;;
'stop')
    killproc nmbd
    killproc smbd
    killproc winbindd
    ;;
*)
    echo "Usage: /etc/init.d/samba.server { start | stop }"
    ;;
esac
```

同样，如果你希望以双守护进程模式运行 Samba，请将：

```
/usr/local/samba/sbin/winbindd
```

在上面的脚本中替换为：

```
/usr/local/samba/sbin/winbindd -B
```

**重启** 如果你在此时重启 smbd、nmbd 和 winbindd 守护进程，你应该能够像本地用户一样连接到 Samba 服务器作为域成员。

## 23.5.3.7 配置 Winbind 和 PAM

如果你已经走到这一步，你知道 `winbindd` 和 Samba 正在协同工作。如果你想使用 Winbind 为其他服务提供身份验证，请继续阅读。此步骤需要修改 PAM 配置文件。（你记得备份原始的 `/etc/pam.d` 文件吗？如果没有，请现在执行。）

你需要一个 PAM 模块来使用 winbind 处理这些其他服务。通过调用以下命令，该模块将在 `../source/nsswitch` 目录中编译：

```
root# make nsswitch/pam_winbind.so
```

从 `../source` 目录执行。`pam_winbind.so` 文件应复制到其他 PAM 安全模块的位置。在我的 Red Hat 系统中，这是 `/lib/security` 目录。在 Solaris 上，PAM 安全模块位于 `/usr/lib/security`。

```
root# cp ../samba/source/nsswitch/pam_winbind.so /lib/security
```

**Linux/FreeBSD 特定的 PAM 配置** 不需要修改 `/etc/pam.d/samba` 文件。我只是保持该文件原样：

```
auth required /lib/security/pam_stack.so service=system-auth
account required /lib/security/pam_stack.so service=system-auth
```

我修改以允许使用 Winbind 作为身份验证服务的其他服务包括控制台（或终端会话）上的普通登录、telnet 登录和 ftp 服务。为了启用这些服务，你可能首先需要更改 `/etc/xinetd.d`（或 `/etc/inetd.conf`）中的条目。Red Hat Linux 7.1 及更高版本使用新的 xinetd.d 结构，在这种情况下，你需要将 `/etc/xinetd.d/telnet` 和 `/etc/xinetd.d/ssh` 中的行从

```
enable = no
```

更改为

```
enable = yes
```

为了让 ftp 服务正常工作，你还需要服务器上已经存在域用户的独立目录，或者将主目录模板更改为所有域用户的通用目录。使用 *smb.conf* 全局条目 *template homedir* 可以轻松设置这些。

> **注意**
>
> *template homedir* 中的目录**不会**自动创建！使用 *pam_mkhomedir* 或预先创建用户目录，以确保用户能够以其自己的主目录在 UNIX 上登录。

可以修改 */etc/pam.d/ftp* 文件以允许 Winbind ftp 访问，方式类似于 samba 文件。我的 */etc/pam.d/ftp* 文件被修改为如下所示：

```
auth required /lib/security/pam_listfile.so item=user sense=deny \
file=/etc/ftpusers onerr=succeed
auth sufficient /lib/security/pam_winbind.so
auth required /lib/security/pam_stack.so service=system-auth
auth required /lib/security/pam_shells.so
account sufficient /lib/security/pam_winbind.so
account required /lib/security/pam_stack.so service=system-auth
session required /lib/security/pam_stack.so service=system-auth
```

*/etc/pam.d/login* 文件可以以几乎相同的方式进行修改。现在它看起来像这样：

```
auth required /lib/security/pam_security.so
auth sufficient /lib/security/pam_winbind.so
auth sufficient /lib/security/pam_unix.so use_first_pass
auth required /lib/security/pam_stack.so service=system-auth
auth required /lib/security/pam_nologin.so
account sufficient /lib/security/pam_winbind.so
account required /lib/security/pam_stack.so service=system-auth
password required /lib/security/pam_stack.so service=system-auth
session required /lib/security/pam_stack.so service=system-auth
session optional /lib/security/pam_console.so
```

在这种情况下，我添加了

