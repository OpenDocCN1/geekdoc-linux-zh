
auth.* |/usr/local/etc/syslog_auth

(You also could choose to handle some of them in other ways such as e-mail to your account, possibly on another system. In a successful cracking, all of your "trip wires" become disabled, but by having them near all the entrances as to get "the warning" beyond the system before it is compromised, you still will get the warning and hopefully in time to stop the cracker).

The raw log message looks like the following:

```
Nov 24 13:13:18 cavu su[426]: - tty2 bob-root
```

The following script will handle this nicely. (It may be invoked from any shell).

```
#!/bin/csh -f
loop:
read x

echo "$x" | grep -q ': invalid password'
if ($status == 0) then
necho "$x"
| sed "s/...........: \([^]*\).*: invalid password for /BAD PW:\1/"
| Mail 1234567@skytel.com
endif

echo "$x" | grep -q 'su[.:* - -'
if ($status == 0) then
necho "$x"
| sed -e "s/^.*........: \([^]*\).*: - /BAD SU:\1/\ "
| Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
endif

goto loop
```

This will generate the following page, where "-" is changed to "->" to indicate that bob is trying to become warmer than the other. It is important to make these pages very easy to understand because you have been woken out of a sound sleep at 3 A.M. and may not be at your mental best.

```
BAD SU:cavu:ttty2 bob-warren
```

In this script you also arranged to receive e-mail on your home and work systems. The truly cautious do not want any evidence of their home system address that a cracker might use to expand his horizons. One solution is to address this e-mail to a third system that should be very secure, which then forwards the e-mail to your home system. There are a number of public re-mailers that could be used.

### Paging telnet and rsh Usage

You can add portions to your script to page yourself when someone initiates a telnet session (whether or not the login is successful) with the following addition to the script. You do not get paged on telnet sessions from cia.com or cavu because you trust these systems. Note that this handles telnet connections that are allowed by TCP Wrappers. The use of TCP Wrappers, a wonderful tool for keeping out crackers, is covered in this chapter and in "TCP Wrappers" on page 109.

```
set y=echo "$x" | sed -e 's/.*' -e 's/.*//'
echo "$x" | grep -q 'telnet\[.*: connect from '
if ("$status == 0) then
  if ("$y" = "cia.com") goto pasttelnet
  if ("$y" = "cavu.com") goto pasttelnet
  echo "$x" \
  | sed -e "s/^...::\([^^]*).*: /telnet\:1;"
  | Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
endif
```

This next example will generate a page when there is an attempt to telnet when it is disallowed by TCP Wrappers. This would be considered a cracking attempt that has been thwarted!

```
echo "$x" | grep -q 'telnet\[.*: refused connect from '
if ("$status == 0) then
  echo "$x" \
  | sed -e "s/^...::\([^^]*).*: /refused connect from/telnet\:1;REFUSED /"
  | refused connect from //"
  | Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
```

The rsh program is quite popular because it allows you to issue a command to a remote system easily. It is a security hole too if someone cracks joe@cia.com and joe@cia.com has permission to issue rsh commands to the bob account on nsa.com (by listing cia.com in ~joe/.rhosts on nsa.com), they "own" joe@nsa.com to too.
The ssh command is much preferred because it is secure. As an alternative (but not as secure), you can use TCP Wrappers to limit which systems can use rsh to issue commands to your system. In any case, if you allow rsh, you will want to be paged (or receive e-mail) when it is used with the following addition to your script.

```
echo "$x" | grep -q 'rsh\[.*: .*cmd='
if ("$status == 0) then
  echo "$x" \
  | sed -e "s/^...::\([^^]*\)\[]:*: /rsh\:1;"
  | Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
```

The e-mail or page you will receive will look like the following:

```
rsh:cavu:root@cracker.com as root: cmd='chown root /bin/csh;
chmod 4777 /bin/csh'
```

## 8.10 Using Arpwatch to Catch ARP and MAC Attacks

On any Ethernet-based Local Area Network (LAN), at the lowest level packet destinations are specified by the machine's Ethernet card's address, more commonly known as the Media Access Control (MAC) address. When a system wants to send a packet to a particular IP address, it sends out an Address Resolution Protocol (ARP) request saying “Who is IP 10.0.0.27” for example. If everyone is playing fair and is properly configured, the intended system will say “I do and my MAC address is 00:87:72:23:7F:AA. The source system sends the packet to MAC address 00:87:72:23:7F:AA. This protocol was designed over 20 years ago, long before the modern Internet existed, when nobody worried about security and only experienced SysAdmins had administrative access to the systems on a LAN.

Now, anyone can plug a laptop into the network and respond to the ARP requests and thoroughly attack the network. Once a network has grown beyond 10 or so systems, management becomes nontrivial. Even well-intentioned users can use conflicting IP addresses unintentionally, forget to change their laptops' IP addresses to the correct one for the organization, and so on.

> Many networks use Dynamic Host Configuration Protocol (DHCP) or ZeroConf to assign IP addresses automatically, but the use of these programs does not completely prevent IP conflicts. There are many ways that a duplicate IP address could be caused by the DHCP server. The most common is system administrator error. However, if the lease file were to be corrupted or removed, duplicate DHCP leases could be handed out.

The best solution for both accidental and intentional problems is to monitor ARP traffic with Arpwatch. This Open Source program was developed by the U.S. government's Lawrence Berkeley Laboratories and runs on Linux and UNIX. In the spring of 2002, I made some major enhancements to it for better tracking of problems on large networks of hostiles with multiple subnets. This enhanced version is available on the CD-ROM or on request via e-mail to book@verysecurelinux.com.

Before going further, I need to introduce the term "bogon" (bo'gon). A packet with an IP address that is incorrect for the subnet it comes from is called a bogon.

To install the enhanced version of Arpwatch on your system, mount the CD-ROM and build from the tarball:

```
cp /mnt/cdrom/book/arpackwatch.bob.tar.gz
zcat arpackwatch.bob.tar.gz | tar -xovf-
cd arpackwatch-bob
./configure
make
make install
make install-man
man arpackwatch
```

Next, add commands similar to the following to the /etc/rc.d/local file so that it will start automatically on reboot:

```
# "-O"          Enhancement to suppress Apple 0.0.0.0 nonsense
# "-m foo"      Enhancement to mail to foo instead of root
# "-w from"      Enhancement to specify from address (include which office)
# "-u MAC"      Enhancement to specify MAC of our upstream router
               to avoid false positives on bogon detection
echo "Starting arpackwatch on each Ethernet interface"
ARPACKET=/usr/local/sbin/arpackwatch
ARPARGS="-O -m sysadmin@pentacorp.com"
# Specify MAC address of upstream router, if any
ARPUPS="-u 00:07:4C:92:76:68"
killall arpackwatch
$ARPARGS -f /var/log/eth0 -i eth0 -w "arpackwatch" (NYC:eth0) " \
  $ARPUPS
$ARPARGS -f /var/log/eth1 -i eth1 -w "arpackwatch" (NYC:eth1) " \
  $ARPUPS
$ARPARGS -f /var/log/eth2 -i eth2 -w "arpackwatch" (NYC:eth2) " \
  $ARPUPS
```

Finally, initialize its human-readable databases and start it for the first time:

```
cd /var/log
touch eth0 eth1 eth2
chmod 600 eth0 eth1 eth2
/etc/rc.d/local
```

This firewall has both an internal network on eth1 and a DMZ on eth2. The argument to the -w flag will show as the "From" address, as "arpackwatch" and indicate which of our firewalls is generating the message and which NIC card the packet originated from. Each running Arpackwatch process builds up an in-memory database
