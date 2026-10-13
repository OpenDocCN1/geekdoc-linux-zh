A sample of the standard proftpd.conf file installed as part of the ProFTPD software package is shown here. It establishes a single server and a single anonymous login. Notice the default ServerType is standalone. If you want to use xinetd to run your server, you must change this entry to inetd. Detailed examples of proftpd.conf files, showing various anonymous FTP and virtual host configurations, can be found with the ProFTPD documentation, located in /usr/share/doc, and on the ProFTPD Web site at www.proftpd.net.

```
ServerName           "ProFTPD Default Installation"
ServerType           standalone
DefaultServer        on
Port                 21
Umask                022
MaxInstances         30
User                 nobody
Group                nobody
<Directory />
    AllowOverwrite     on
</Directory>

# A basic anonymous configuration, with one incoming directory.
<Anonymous ~ftp>
User                 ftp
Group                ftp
RequireValidShell   off
MaxClients           10
UserAlias            anonymous ftp
DisplayLogin         welcome.msg
DisplayFirstChdir    .message
# Limit WRITE everywhere in the anonymous chroot except incoming
<Directory *>
    <Limit WRITE>
        DenyAll
    </Limit>
</Directory>
<Directory incoming>
    <Limit WRITE>
        AllowAll
    </Limit>
    <Limit READ>
        DenyAll
    </Limit>
</Directory>
</Anonymous>
```

# Authentication

Authentication of users in ProFTPD can be implemented either in PAM, LDAP, or SQL. For LDAP or SQL, you need to load the corresponding ProFTPD module. PAM authentication is the default (see Chapter 28 for more information on LDAP and PAM). Be sure that a /etc/pam.d/ftp file has been installed to provide PAM