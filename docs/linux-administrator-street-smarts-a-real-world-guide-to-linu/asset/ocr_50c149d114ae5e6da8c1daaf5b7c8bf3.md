# Configuring xinetd

The **xinetd** program is an extended super server. It provides the functionality of **inetd** plus security options that are similar to those of TCP Wrappers. Modern versions of Fedora, Mandriva, Red Hat, openSUSE, and a few other distributions use **xinetd** by default. Other distributions may use it in the future. If you like, you can replace **inetd** with **xinetd** on any distribution.

The `/etc/xinetd.conf` file controls **xinetd**. On distributions that use **xinetd** by default, though, this file contains only global default options and a directive to include files stored in `/etc/xinetd.d`. Each server that should run via **xinetd** then installs a file in `/etc/xinetd.d` with its own configuration options. Look for a file called `ftp`, `ftpd`, `in.ftpd`, or something similar in the `/etc/xinetd.d` directory. If it's present, you can edit this file to activate your FTP server. If not, you can either create this file and add an FTP entry as described shortly or add such an entry to your `/etc/xinetd.conf` file.

Whether the entry for a service goes in `/etc/xinetd.conf` or a file in `/etc/xinetd.d`, it contains information similar to that in the `inetd.conf` file. The **xinetd** configuration file, though, spreads the information across multiple lines and labels it more explicitly. Listing 6.2 shows an example that's equivalent to the earlier `inetd.conf` entry. This entry provides precisely the same information as the `inetd.conf` entry except that it doesn't include a reference to `/usr/sbin/tcpd`, the TCP Wrappers binary. Because **xinetd** includes similar functionality, it's generally not used with TCP Wrappers.

# Listing 6.2: Sample xinetd Configuration Entry

```
service ftp
{
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/in.ftpd
    server_args     = -l
}
```

![](bbox=[0.13, 0.71, 0.24, 0.81])

Your existing **xinetd** configuration file for your FTP server may not be identical to Listing 6.2. If it's not, it's probably best to leave the configuration as you found it, with the exception of the `disable` option (described next) and any other options you research and that you know you want to modify.

One additional **xinetd** parameter is important: `disable`. If you include the line `disable = yes` in a service definition, **xinetd** ignores the entry. Some servers install startup files in `/etc/xinetd.d` that have this option set by default; you must edit the file and change the entry to read `disable = no` to enable the server. You can also disable a set of servers by listing their names in the `default` section of the main `xinetd.conf` file on a line called `disabled`, as in `disabled = ftp shell`.