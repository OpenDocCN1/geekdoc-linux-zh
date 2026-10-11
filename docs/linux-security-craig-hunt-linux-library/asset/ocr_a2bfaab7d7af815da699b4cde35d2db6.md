```
kadmin: ktadd ftp/caldera.hontanon.com
Entry for principal ftp/caldera.hontanon.com with kvno 2, encryption type DES cbc mode with CRC-32 added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal ftp/caldera.hontanon.com with kvno 2, encryption type Triple DES cbc mode raw added to keytab WRFILE:/etc/krb5.keytab.
```

Note that you are running the `kadmin` command on the target server (`caldera.hontanon.com`), which must be configured to point to the `kadmin` daemon on `kerberos.hontanon.com`. This is defined in the `[realms]` section of `/etc/krb5.conf` file, as explained in the previous section, “Configuring the Kerberos Domain Controller (KDC).” You must execute the command as root (using `sudo`), and you use the `-p` `ramon/admin` option to specify which principal you want to use in order to gain administrative permissions to the Kerberos database.

As you can see from its output, the `ktadd` command adds the appropriate keytab entry to the `/etc/krb5.conf` file on the target server. In this case, `caldera.hontanon.com` should be ready to use Kerberos authentication for `ftp`, `telnet`, `rsh`, and `rlogin`.

The next step is to modify the target server’s network setup to use the *Kerberized* versions of the network daemons. If your system is using `/etc/inetd.conf` to spawn off services, add the following lines:

```
ftp stream tcp nowait root /usr/kerberos/sbin/ftpd ftpd -a -l
telnet stream tcp nowait root /usr/kerberos/sbin/telnetd telnetd -a valid
kshell stream tcp nowait root /usr/kerberos/sbin/kshd kshd -ec
eklogin stream tcp nowait root /usr/kerberos/sbin/klogind klogind -ec
```

Note that you may have to add the following Kerberos-specific entry to your server’s `/etc/services` file, depending on your distribution (Red Hat 7.0 and Caldera eServer 2.3 include it, but SuSE 7.0 does not):

```
eklogin 2105/tcp # Kerberos encrypted rlogin
```

If you are using xinetd, use the following format (`ftpd` is shown as an example):

```
[ramon]$ more /etc/xinetd.d/ftp
service ftp
{
    flags = REUSE
    socket_type = stream
```