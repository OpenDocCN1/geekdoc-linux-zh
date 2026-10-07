# Configuring a Dial-in PPP Server

The next step is to create a user named ppp and then to assign a password. Although it is possible to allow remote users to log in and start pppd from the command line (assuming you've set pppd to SUID), the pppd daemon can be started automatically by creating a short script and then assigning the shell in the user's /etc/passwd entry, like this:
ppp:x:500:500::/home/ppp:/usr/local/bin/dopp

In this instance, the script doppt (made executable with chmod +x) would contain the following:
exec /usr/sbin/pppd -detach

Using this approach, pppd will start automatically after the ppp dial-in user connects and logs in (perhaps using the ppp-on scripts or other clients on the remote computer). The file options under the /etc/ppp directory should include global dial-in for PPP service on your system, and specific options (such as options.tty1 for this example) should be

```
asyncmap 0
netmask 255.255.255.0
proxyarp
lock
crtscts
modem
```

created for each enabled dial-in port. For example, /etc/ppp/options could contain

There are many approaches to providing your own PPP service. IP addresses can be assigned dynamically, or a static IP address can be doled out for a user. For example,
/etc/ppp/options.tty1 could contain

```
IPofserver=assignedIPofdialuser
```

In this example, the first IP address for the host computer, whereas the second IP address will be assigned to the remote user. For details about configuring PPP Linux, read the ppp manual page or documentation under the /usr/share/doc/pppd/ directory. If you're a Linux developer, browse the files ppp_async.c, ppp_deflate.c, ppp_generic.c, and ppp_synctty.c under the /usr/src/linux/drivers/network.

# Relevant Red Hat and Linux Commands

Here are some of the most useful commands for managing Internet connections in Red Hat Linux:
internet-druid—Red Hat's command-line name for its graphical Internet Connection Wizard (also symbolic link to redhat-config-network client).

mgetty—An advanced serial port monitoring tool that supports data and fax modem operations with Linux.

neat—Red Hat's command-line name for the graphical Network Configuration tool.