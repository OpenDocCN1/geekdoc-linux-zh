
*TCP* (*atcp*) and *stealth UDP* (*sudp*) and *advanced stealth UDP* (*audp*). Only run one TCP service and one UDP service. So, if you uncomment a stealth or advanced stealth service, be sure to add a comment in front of the appropriate basic service.

To activate the new services, you would then execute the following command:

```
# /etc/init.d/portsentry restart
```

The new PortSentry modes will take effect immediately. Those new modes will also be in effect when your computer reboots.

## Testing PortSentry

You can test that your ports are properly protected in different ways. What you want to do is run a program that a potential intruder would run and see if it trips the appropriate response from PortSentry. For example, you could use a port scanner to see how your ports appear to the outside world. You could also use a command, such as `telnet`, to try and set off a particular port to see if PortSentry catches it.

`nmap` is a popular tool for scanning TCP and UDP ports. You can give the `nmap` command a host name or IP address, and it will scan about 1500 ports on computer to see which ports are open (and presumably offering services that could potentially be cracked).

An RPM of `nmap` is also available. You can download the `nmap-frontend` package, which contains a simple graphical interface to `nmap` called `xnmap`. I suggest that you install the packages on the system running PortSentry as well as on another system on your LAN (if one is available). Then run the following procedure on the PortSentry system to test it:

- 1. If PortSentry is running, shut it down by typing the following:
  # /etc/init.d/portsentry stop

- 2. Type the following `nmap` commands to see which ports are open on the local system:
  # nmap -sS -O 127.0.0.1
  # nmap -sU -O 127.0.0.1
  
  The output shows you which ports are currently offering services on your computer for TCP and UDP protocols, respectively.

- 3. If there are any services that you don't want open, you should turn off those services by using `chkconfig service off` (replacing `service` with the service name), by editing the configuration file in the `/etc/xinetd.d` directory that represents the service and changing `disable = no` to `disable = yes`, or by changing your firewall setup.

- 4. If there are services that you want to be available from your computer, make sure that the port numbers representing those services are not being monitored by PortSentry. Remove the port number from the `TCP_PORTS` and/or `UDP_PORTS` options in the `/etc/portsentry/portsentry.conf` file, or PortSentry will report that there is a possible stealth scan on the port.

- 5. Restart PortSentry as follows:
  ```
  # /etc/init.d/portsentry start
  ```
- 6. Run nmap again, as described previously. The ports offering legitimate services, as well as the ports being monitored by PortSentry, should all appear to be open.
- 7. Check the /var/log/messages file to make sure that PortSentry is not trying to monitor any ports on which you are offering services.

When you have determined that PortSentry is set up the way you would like it to be, run the nmap command from another computer on your network. This time, replace 127.0.0.1 with the name or IP address of the PortSentry computer. If everything is working, the first port that the remote computer scans on your PortSentry computer should block all subsequent scans.

## Tracking PortSentry intrusions

Besides taking action against intruders, PortSentry logs its activities using the syslog utility. PortSentry's start-up, shutdown, and scan-detection activities are logged to your /var/log/messages file. The following are examples of PortSentry output in that file.

```
portsentry[13259]: adminalert: Psionic PortSentry 1.0 is starting.
portsentry[13260]: adminalert: Going into listen mode on TCP port: 1
portsentry[13260]: adminalert: Going into listen mode on TCP port: 11
...
portsentry[13260]: adminalert: PortSentry is active and listening.
portsentry[]: attackalert:Connect from host:10.0.0.4 to TCP port: 31337
portsentry[]: attackalert: Connect from host: 10.0.0.4 to TCP port: 11
portsentry[]: attackalert: Host: 10.0.0.4 is already blocked. Ignoring
...
portsentry[13371]: securityalert: Psionic PortSentry is shutting down
portsentry[13371]: adminalert: Psionic PortSentry is shutting down
```

The first part of the output shows PortSentry starting up. As PortSentry begins listening to each port, that port is noted in a separate log message. The next messages show the computer being scanned. Someone from host 10.0.0.4 ran nmap to scan the ports on the computer. PortSentry caught the scan of port 31337 and blocked attempts to scan other ports.

Finally, the last set of messages shows PortSentry being shut down. This is a security alert because someone besides you could shut down PortSentry to hide that they had broken in.

> **NOTE:** If you have been running the LogSentry package (described earlier), these messages show up in the e-mail messages you receive each hour from Logcheck.

## Restoring access

If access was cut off to a computer that you wanted to have access, there are several things you can check to correct that problem:

- **/etc/hosts.deny:** See if the computer's IP address was mistakenly added to this file. This would cause network services to be denied to the host at that IP address.
- **/var/portsentry/portsentry.blocked:** Check that an entry for the computer's IP address wasn't added to the portsentry.blocked.udp or portsentry.blocked.tcp files.
- **route:** Run the /sbin/route command to see if messages from the computer are being rerouted to a dead host (probably the localhost).
- **ipchains:** Run the ipchains -L command to see if a new firewall was created to block access from the computer. (If you had created an iptables rule instead, type iptables -L to see the new firewall entry.)

> TIP: To make sure that access isn't cut off again, you can add the IP address of the remote computer to the /etc/portsentry/portsentry.ignore file. Future improper scans or requests for services won't cause the remote computer to be blocked.

## Summary

With the rise of the Internet, security has become a critical issue for nearly all computer users. Properly using passwords, securely configuring network services, and monitoring log files are critical ways of keeping your computer secure.

Using encryption keys you can help verify the authenticity of those you communicate with, as well as make the data you transmit more secure. With tools such as LogSentry and PortSentry, you can protect your Red Hat Linux system from intrusions.

## Part IV

## Red Hat Linux Network and Server Setup

- Chapter 15: Setting Up a Local Area Network
- Chapter 16: Connecting to the Internet
- Chapter 17: Setting Up a Print Server
- Chapter 18: Setting Up a File Server
- Chapter 19: Setting Up a Mail Server
- Chapter 20: Setting Up an FTP Server
- Chapter 21: Setting Up a Web Server
- Chapter 22: Setting Up a News Server
- Chapter 23: Setting Up Boot Servers: DHCP and NIS
- Chapter 24: Setting Up a MySQL Database Server
- Chapter 25: Making Servers Public with DNS
- Chapter 26: Using Linux Servers from a Mac

## Chapter 15

### Setting Up a Local Area Network

- In This Chapter
- Understanding local area networks
- Setting up a wired Ethernet LAN
- Setting up a wireless LAN
- Troubleshooting your LAN

In the home or in a small business, Red Hat Linux can help you connect to other Linux, Windows, and Macintosh computers so that you can share your computing equipment (files, printers, and devices). Add a connection to the Internet and routing among multiple LANs (described in Chapter 16), and Red Hat Linux can serve as a focal point for network computing in a larger enterprise.

This chapter helps you set up your own local area network (LAN). The procedures described here provide a foundation for sharing the computing resources in your home or organization. In particular, the chapter describes how to use Ethernet cards, wiring, and protocols to connect computers. It then tells you specifically how to configure your Red Hat Linux computer so that it can communicate with other computers.

### Understanding Local Area Networks

Connecting the computers in your organization via a LAN can save you a lot of time and money. The amount of money you put into networking hardware, even in a small configuration (less than five or six users), can save you from buying multiple printers, backup media, and other hardware. Add a single, shared Internet connection and you no longer need multiple modems and Internet accounts.

With a LAN, you don’t have to run down the hall anymore with your file on a disk to print it on your friend’s printer. Information that had to wait for the mailroom to make the rounds can be sent in an instant to anyone (or everyone) on your LAN.

With a LAN, you begin to open the greatest potential of Red Hat Linux — its ability to act as a server on a network. Because Red Hat Linux is more robust and feature-rich than other computing systems (certainly for the price), adding it to your LAN can provide a focal point to
