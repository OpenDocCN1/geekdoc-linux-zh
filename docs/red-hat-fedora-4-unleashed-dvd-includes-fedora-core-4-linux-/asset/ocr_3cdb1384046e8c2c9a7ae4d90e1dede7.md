K12canna  K20rusersd  K35dhcpd  K50tux  K65krb5kdc
K84rippd  S12syslog  S44acpid  S95anacron  K12aiman
K20rwalld  K35smb  K50svftpd  K70aeip1000  K82zebra
S13irqbalance  S55cups  S95atd  K12mysqld  K20rwhod
K35vncserver  K54dovecot  K70bcm5820  K90isicom  S13portmap
S55sshd  S97messagebus  K15httpd  K20spamassassin  K35winbind
K54pxe  K74ntpd  K91isdn  S14nfslcok  S56rawdevices
S97rhnsd  K15postgresql  K24irda  K40mars-nwe  K55routed
K74ups  K95firstboot  S17keytable  S56xinetd  S991ocal
K16rarpd  K25squid  K45arpwatch  K61hp0j  K74ypserv
S0microcode_ctl  S20random  S84privoxy  S99mdmonitor

These scripts are actually symbolic links to system service scripts under the /etc/rc.d/init.d directory (yours might look different, depending on whether you are working with a workstation or server installation and the services or software packages installed on your system):

```
# ls /etc/rc.d/init.d/
acpid bgpd firstboot iptables keytable mars-nwe nfs
postgresql ripd smartd vncserver zebra aep1000 bluetooth
FreeWnn ipchains killall mdmonitor nfslcok privoxy
rippd smb svftpd amd bootparam functions iptables
krop messagebus nsd psacct routed snoopd winbind
anacron canna gkre1imd irda krb524 microcode_ctl ntpd
pxe rstat snmptrapd xfs apmd cpqarrayd gpm
irqbalance krb5kdc mysqlid ospf6d radiusd rusersd
spamassassin xinetd arpwatch crond halt iccsi kudzu
named ospfd radvd rwalld squid ypbind
atak cups hp0j isdn ldap netdump pand
random rwhod sshd yppasswd atd dhchpd
httpd isicom lisa netdump-server pcmcia rarpd
saslauthd syslog ypserv autofs dhcrelay ident kadmiin
lm_sensors netfs portmap rawdevices sendmail tux
ypxfrd bcm5820 dovecot innd kdccrotate mailman
network postfix rhnsd single ups yum
```

The rc5. d links are prefixed with a letter and number, such as K15 or S10. The (K) or (S) in these prefixes indicate whether or not a particular service should be killed (K) or started (S) and pass a value of stop or start to the appropriate /etc/rc.d/init.d script. The number in the prefix executes the specific /etc/rc.d/init.d script in a particular order. The symlinks have numbers to delinate the order in which they are started. Nothing is sacred about a specific number, but some services need to be running before others are started. You wouldn't want your Fedora Core Linux system to attempt, for example, to mount a remote Network File System (NFS) volume without first starting networking and NFS services.