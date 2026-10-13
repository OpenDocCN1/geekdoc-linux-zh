If you remove all the comment lines from the default /etc/smb.conf file, only three special configuration sections are defined in the file. They are discussed next.

# Setting the [global] parameters

The [global] section defines Samba parameters that apply to all other configuration sections (that is, services that they define). The default [global] configuration is as follows:

```
[global]
workgroup = MYGROUP
server string = Samba Server
printcap name = /etc/printcap
load printers = yes
log file = /var/log/samba/log.%m
max log size = 50
security = user
socket options = TCP_NODELAY
dns proxy = no
```

Here is how you configure each of these parameters.

# workgroup

Set this parameter to the Windows workgroup or Windows NT domain name that you want Samba to participate in as a node. For example, I use NITEC as the Windows NT domain name so that I can set workgroup to NITEC. When a Windows 9x or NT system on my network browses the Network Neighborhood, it sees the Samba server under the NITEC Windows NT domain. Set this to whatever workgroup or domain name is appropriate for your LAN.

# server string

Set this parameter to provide a description for your Samba server. This description will be visible to Samba clients (such as a Windows 9x machine.)