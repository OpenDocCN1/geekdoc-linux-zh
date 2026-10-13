# The smb.conf File

Samba is configured using the `/etc/smb.conf` file. Before looking at specific Samba configurations for different purposes, we need to consider the basic structure of the smb.conf file. The following is a typical smb.conf file:

```
====================== Global Settings ==================================
[global]
    workgroup = MYGROUP
    server string = Samba Server
    printcap name = /etc/printcap
    load printers = yes
    log file = /var/log/samba/log.%m
    max log size = 50
    security = user
    socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
    dns proxy = no

========================= Share Definitions ===============================
[homes]
    comment = Home Directories
    browseable = no
    writable = yes

[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
    guest ok = no
    writable = no
    printable = yes

[mydir]
    comment = My Directory
    path = /usr/somewhere/private
    valid users = someuser
    public = no
    writable = yes
    printable = no
```

The smb.conf file is divided into sections. Each section starts with a section header such as [global] or [printers] that is followed by one or more directives, one per line. The header specifies the name of the section. Comments, which are ignored when in the smb.conf file, start at a hash mark (#) or a semicolon (;) and continue to the end of the line.

Directives in each section of the smb.conf file take one of two forms:

+   - A value assignment of the form:
+     `<directive name> = <value>`
+   - A simple directive of the form:
+     `<directive name>`