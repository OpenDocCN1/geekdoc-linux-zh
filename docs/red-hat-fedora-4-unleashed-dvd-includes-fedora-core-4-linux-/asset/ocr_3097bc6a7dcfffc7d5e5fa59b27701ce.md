This technique can be used to listen to any messages left by callers (which end up in the /var/spool/voice/incoming directory).

Browse to http://alpha.greenie.net/vgetty/ to download vgetty and its documentation. Also, look at the Linux Answering machine HOWTO at http://linuxindia.virtuallave.net/iamhowto.html.

The next step is to create a user named ppp and then to assign a password to it. Although it is possible to allow remote users to log in and start ppd from the command line (assuming that you have set ppd to SUID root), the ppd daemon can be started automatically by creating a short shell script and then assigning the shell script to the user for the default shell in the user's /etc/passwd entry, like this:

```
ppp:x:500:500::/home/ppp:/usr/local/bin/dopppdoppp
```

(made executable with chmod +x) would contain the following:

```
exec /usr/sbin/pppd -detach
```

Using this approach, pppd will start automatically after the ppp dial-in user connects and logs in (perhaps using the ppp-on scripts or other clients on the remote computer). The file options under the /etc/ppp directory should include general dial-in options for PPP service on your system, and specific options files (such as options.ttyS1 for this example) should be created for each enabled dial-in port. For example, /etc/ppp/options could contain

```
asyncmap 0

netmask 255.255.255.0

proxyarp

lock

crtcts

modem
```

There are many approaches to providing your own PPP service. IP addresses can be assigned dynamically, or a static IP address can be doled out for a user. For example, /etc/ppp/options.ttyS1 could contain

```
IPofPPPserver:assignedIPofdialinuser
```

In this example, the first IP address is for the host computer, whereas the second IP address will be assigned to the remote user. For details about configuring PPP for Linux, read the pppd manual page or documentation under the /usr/share/doc/pppd* directory. If you're a Linux developer, browse the source code files ppp_async.c, ppp_deflate.c, ppp_generic.c, and ppp_synctty.c under the /usr/src/linux-2.6/drivers/net directory.