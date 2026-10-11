directory. Because few daemons are started in Single User Mode, most files in this directory start with a K:

```
[root@server1 root]# ls /etc/rc.d/rc1.d
K01yum K20statd K50vsftpd K84ospfd
K03messagesbug K20usersd K50xinetd K84rjpd
K03rhnsd K20wiald K54devcot K84rijngd
K05anacron K20rwhod K56reoute K85zebra
K05atd K20tomcat K56acpid K86ifsqos
K05innnd K24irda K60crond K87rnplance
K05saslauthd K25squid K61hpj3 K87portmap
K09privoxy K25sshd K61ldap K88syslog
K10cups K28amd K65ident K89netplugd
K10dc_server K30sendmail K65admin K90bluetooth
K10psacct K30pamassassin K65kprop K901scom
K10radiusd K34ncrelay K65krb524 K90network
K10xfs K34ypasssswd K65krb5kdc K91lsdn
K12canma K35atalk K68rpcgssd K921ptable
K12dc_client K35cyrus-imapd K692imapd K921ptables
K12FreeWin K35dhcpd K69rpcsvcgssd K921pvsnm
K12mailman K35smb K7000100 K95kduz
K12mysq1d K35vncserver K70bcms820 K96pcmcia
K15kernelmod K361isa K72autofs K99dmodmon
K15pgp K40smartd K74apmd K99dmcpd
K15httpd K44rawdevices K74ntpd K99miscodoc_dctrl
K15postgresql K45erwatch K74ups K99readahead
K16arpd K45named K745pserv K99readahead_early
K1711m K46radvd K74yp K501single
K20bootparam K50netdump K75netfs S011sysd
K201scsi K50smpd K80random S06cpuspeed
K20netdump-server K50smptrapd K840bgpd
K20nfs K501ux K84ospfd
[root@server1 root]#_ 
```

Most daemons that are loaded upon system startup are executed from entries in `/etc/initab` that run the `/etc/rc.d/rc` command at system startup to load daemons from files that start with an S in the appropriate `/etc/rc.d/rc*.d` directory (where `*` refers to the default runlevel). As with the `/etc/rc.d/rc.sysinit` program, a message during boot time indicates whether each file in the `/etc/rc/rc*.d` directory has loaded successfully or unsuccessfully. An excerpt from this list is shown next:

```
Starting up APM daemon: [ OK ]
Starting automount: No Mountpoints Defined [ OK ]
Starting xinetd: [ OK ]
Starting sendmail: [ OK ]
Starting console mouse services: [ OK ]
```