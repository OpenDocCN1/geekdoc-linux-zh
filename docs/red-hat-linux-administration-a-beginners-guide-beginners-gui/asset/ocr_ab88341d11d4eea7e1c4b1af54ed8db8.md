**userlist_deny**  This option is only consulted if the previous option is enabled. It defaults to “yes,” which will deny user accounts that are listed in the file. Changing this option to “no” reverses the meaning of the list so that only those listed can log in.

**userlist_file**  And this option specifies the file referred to by the preceding two options. The default is */etc/vsftpd.user_list*. It is instructive to at least examine the accounts that Red Hat has listed here by default.

# Configuring Host Access

While some FTP daemons will provide direct support for blocking certain hosts, the proper place for that kind of activity is in the access control files **hosts.allow** and **hosts.deny**. Place an entry in either or both of these files to adjust the access according to your needs. An example configuration might be

```
```text
/etc/hosts.allow
vsftpd: LOCAL 10.1.42.0/24 *.my.domain.com
```
```

```
```text
/etc/hosts.deny
vsftpd: ALL
```
```

The access control files are very flexible, but if they don’t quite meet your needs for some reason, you can also adjust the settings in **xinetd.conf**. For more information on the **hosts.allow** and **hosts.deny** files, see Module 8.

# CRITICAL SKILL
**11.4**  Configuring a Virtual FTP Server

Even though the FTP protocol doesn’t support name-based virtual servers the way the Hyperext Transfer Protocol (HTTP) does, you can still set up multiple FTP servers on the same host so long as each server has its own IP address. To distinguish between the different “servers,” we’ll be taking advantage of **xinetd** once again. This section assumes that you have already configured an IP alias and fudged the Address Resolution Protocol (ARP) table correctly. (This is discussed later in this book in Part V, “Advanced Linux Networking.”) This quick jumpstart on the process assumes you have one Ethernet card and want to add a single virtual IP address:

+   1.  Make sure your new IP address exists in both the local host table (**/etc/hosts**) and your DNS table. (In this example, we’ll call the host “earth.”)