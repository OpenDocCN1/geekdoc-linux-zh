
## 9.3 PPP configuration

To be able to use PPP, the kernel must support PPP. In addition, you need the programs pppd and chat. Usually, both programs are part of a separate PPP package.

### Manual configuration

The first step to a PPP connection consists of using a terminal emulator (such as minicom or seyon) to dial your Internet provider's phone number and log in with your PPP login name and the corresponding password. For the sample data in this section, this login process looks more or less like the following. With ATDT the modem is requested to dial the specified number. After some time, the modem answers with the success message CONNECT. Now the Internet provider comes up with your login prompt.

```
ATDT123456
CONNECT 57600/REL
Internet Provider Login: hofer
Password: que44tre
PPP session beginning.... "#!!!!)))***
```

If everything goes right so far, the terminal emulator [will] to display strange characters. The result from the fact that, after your successful login, the Internet provider has started its PPP program and wants to establish a PPP connection with your computer. With some providers, PPP startup is not carried out automatically; instead, you need to enter an additional command (such as ppt). You need to ask your provider for the name of the command.

In order to make this PPP connection actually usable, you must quit the terminal emulator and subsequently start pppd. It is essential that, while doing this, you do not interrupt the established connection. If you work with minicom, com with seyon the CANCEL button and, in the confirmation request that appears, tell the program not to hang.

When calling pppd, you must specify your modem device and the keywords crtscts and defroute. With this, pppd takes control of the serial interface and establishes a PPP connection to exchange IP addresses with the partner program of the Internet provider.

```
#root /usr/lib/ppp/pppd /dev/tty1 crtscts defroute &
```

All examples of this chapter assume that your modem is connected to the second port (that is, /dev/tty1).

Instead of defroute, you can also use the syntax ip:foreignIP, if fixed IP addresses are to be employed. If the IP address of your Internet provider's PPP server is not known, it is sufficient to specify your own IP address.

```
#root /usr/lib/ppp/pppd /dev/tty1 crtscts 199.85.96.166: &
```

If the Internet provider assigns IP addresses dynamically (that is, if you are assigned a different IP address with each login), you must use the keyword noipdefault.

```
#root /usr/lib/ppp/pppd /dev/tty1 crtscts noipdefault &
```

> pppd can only be executed by root. (More precisely, problems do not occur when starting pppd, but only when this program attempts to link the new Internet connection to the TCP/IP system with programs such as ifconfig and route.) However, the PPP connection established by root can subsequently be used by all logged-in users.

Establishment of the connection can be controlled through additional options. These options can be stored either in /etc/ppp/options or in the current working directory in .pprc.

pppd requires that the /etc/ppp/options exists. If this is not the case, simply execute touch /etc/ppp/options.

Most distributions use a preconfigured version of the options file. If pppd does not work, the problem is often caused by the option settings in this file! Try to comment out all the options set.

Instead of the normal PPP, many Internet providers use Van Jacobson compressed PPP. This PPP variation provides additional data reduction (corresponds to CSLIP). Linux recognizes this PPP variation automatically; no special options or settings are required.

## PPP authentication

There are different options for carrying out the PPP login:

- In the above example, the user name and password had to be entered manually in a terminal program, which is, however, suitable for initial testing. On page 313 you will be introduced to the program chat which, besides the dialing process, also automates this simple form of identification. (In many PPP configuration programs, this variation is called script-based, because that utilizes a script-like configuration file.)

- A more elegant form of PPP identification is PAP (Password Authentication Protocol). In the easiest case, this means that login name and password are stored in the file /etc/ppp/pap-secrets, in the following form (for the example of this chapter):

```
# /etc/ppp/pap-secrets
* hofer             * qwe44trE
```

Now, hofer (or whatever the login name may be) must be submitted to pppd as an additional parameter. pppd automatically reads the corresponding password from pap-secrets. This file can contain any number of name/password pairs. The login process can be made more secure by means of further PAP options, that is the password is encoded before transmission, and so on.

- Rather less frequently, CHAP (Challenge/Handshake Authentication Protocol) is used for identification – for example, when Windows NT is used as a PPP server. In this case, the pppd configuration file is etc:/ppp/chap-secrets.

Extensive information about PAP and CHAP can be obtained through man pppd or by looking at the PPP-HOWTO.

## Testing the connection

In order to test whether the PPP connection has been successfully established, the next step is to execute ifconfig. The result should look more or less like the following: besides the loopback device, there is now a PPP connection (device name ppp0) from your IP address 199.85.96.166 to the IP address of the Internet 199.85.37.3. Up to now, no data has been transmitted and therefore all packets are 0.

```
root# ifconfig
Lo Link:Loopback
 addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
 UP BROADCAST LOOPBACK RUNNING MTU:358 Metric:1
 RX packets:14 errors:0 dropped:0 overflows:0 frame:0
 TX packets:14 errors:0 dropped:0 overflows:0 carrier:0 collisions:0
ppp0 Link:Point-to-Point Protocol
 addr:199.85.96.166 P-t:199.85.37.3 Mask:255.255.255.0
 UP POINPOINT RUNNING MTU:1006 frame:0
 RX packets:7 errors:0 dropped:0 overflows:0 carrier:0
 TX packets:7 errors:0 dropped:0 overflows:0 carrier:0 collisions:0
```

Next, you can check whether data transmission works. For this purpose, the pping program which sends small data packets to a specified IP address, in which this case would be the address of the Internet provider known from ifconfig (in the above example, 199.85.37.3).

```
root# ping 199.85.37.3
P 199.85.37.3 (199.85.37.3): 56 data bytes
6 bytes from 199.85.37.3: icmp_seq=0 ttl=255 time=252.2 ms
6 bytes from 199.85.37.3: icmp_seq=1 ttl=255 time=210.3 ms
6 bytes from 199.85.37.3: icmp_seq=2 ttl=255 time=210.3 ms
<Ctrl+C>
----
199.85.37.3 ping statistics
3 packets transmitted, 3 received, 0% packet loss
round-trip min/avg/max/210.3/224.3/252.2 ms
```

## GOING WITH LINUX

If everything functions as it should, you are ready to try out a proper Internet application. Particularly suited for testing is ftp, because larger amounts of data are transmitted, and this allows you to check the stability of the connection. Furthermore, handling ftp is quite straightforward (see also page 335) and, as a rule, it does not assume any further configuration.

## If it does not work

If problems arise at the first step – that is, during connection setup with the terminal emulator – you should contact your Internet provider. After the login, the terminal emulator should display strange characters which result from the PPP communication. The online LED of your modem must still be on after quitting the terminal emulator – the connection has been interrupted.

> pppd uses syslog to log its error messages, warnings, and so on, in a file in the /var/adm/ or /var/log/ directory (depending on the setting in /etc/syslog.conf). When problems occur, you should look at the end of these files. If you specify the optional keyword debug when calling pppd, logging is even more extensive.

Some Internet providers automatically terminate the connection when no more data is transmitted for a given time (usually, 1 and 5 minutes). In principle, this is very useful, because a forgotten PPP connection will not lead to an astronomical phone bill. On the other hand, it can be very irritating when you are reading WWW documents.

If you frequently encounter problems with unwanted interruptions, you can eliminate them by means of the mentioned ping command. The following command transmits a small data packet to the provider every 30 seconds, ensuring some Internet traffic in periods of inactivity.

```
root# ping -i 30 provider.de
```

If you are completely lost, look at the excellent PPP-HOWTO document!

![](img/b30873dd3d753687a59253fb9ad26a0b_339_0.png)
