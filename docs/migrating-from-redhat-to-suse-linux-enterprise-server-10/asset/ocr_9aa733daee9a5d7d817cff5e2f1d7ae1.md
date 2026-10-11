# Figure C-16

| Red Hat Enterprise Linux | | SUSE Linux Enterprise Server |
|---|---|---|
| | BIND/DNS | |
| Chrooted Directory | /var/named/chroot | /var/lib/named |
| Files | /etc/named.conf (symlinked to /var/named/chroot/etc/named.conf) | /etc/named.conf (copied from /var/lib/named/etc every time named is started) |
| | /etc/named.custom | /var/lib/named/etc/named.conf.incl<br>ude<br>(copied from<br>/etc/named.conf.incl<br>ude) |
| | /etc/rndc.key (symlinked to /var/named/chroot/etc/rndc.key) | /etc/rndc.conf.incl<br>ude<br>(copied from /var/lib/named/etc)<br>/var/lib/named/*<br>(copied from /var/lib/named/*)<br>/var/lib/named/etc/named.d<br>/var/lib/named/etc/rndc.key |
| Zone Files | /var/named/chroot/var/named/** | /var/lib/named/master<br>/var/lib/named/slave |
| Config Files | /etc/nisypd.conf (not chrooted by default) | /etc/nisypd.conf (copied from<br>/var/lib/nisypd/etc/nisypd.conf)<br>(chrooted to /var/lib/nisypd) |
| | DHCPD | |
| Config Files | /etc/dhcpd.conf | /var/lib/dhcp/etc/dhcpd.conf<br>(copied from<br>/etc/dhcpd.conf every time dh<sup>2</sup>clientpd is started) |
| Client | dhcp<sup>2</sup>client | Dhcpd |

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**