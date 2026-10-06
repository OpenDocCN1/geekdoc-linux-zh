# Linux Administration: A Beginner's Guide

The underlying security issue always goes back to risk: Is the risk of running an application worth the value it brings you? If the value a particular process brings zero because you're not using it, then no amount of risk is worth it. Looking beyond security, there the practical matter of stability and resource consumption. If a process brings zero value, even a benign process that does nothing but sit in an idle loop uses memory, processor time, and kernel resources. If a bug were to be found in process, it could threaten the stability of your server. If you don't need it, don't run it.

If your system is running as a server, you should reduce the number of processes that are run. For example, if there is no reason for the server to connect to a printer, disable the print services. If there is no reason the server should accept or send e-mail, turn off the server component. If no services are run from xinetd, then xineted should be turned off. No printer? Turn off Common UNIX Printing System (CUPS). Not a file server? Turn off Network File System (NFS) and Samba.

Fully thinned, the server should be the bare minimum it needs to provide the services required of it.

# A Real-Life Example: Thinning Down a Server

Let's take a look at a real-life deployment of a Linux server handling web and e-mail access outside of a firewall and a Linux desktop/workstation behind a firewall with a trusted server. The two configurations represent extreme: tight configuration in a environment (the Internet) and a loose configuration in a well-protected and trusted environment (a local area network, or LAN).

The server runs the latest Fedora distribution. With unnecessary processes thinned, the server has 10 programs running, with 18 processes when no one is logged in. Of the 10 programs, all SSH, Apache, and Sendmail are externally visible on the network. The rest handle basic management functions, such as logging (rsyslog) and scheduling (cron). Removing nonessential services used for experimentation only (for example, Squid proxy server), the running program count can be reduced to 7 (init, rsyslog, cron, SSH, Postfix, Getty and Apache), with 13 processes running, 5 of which are Getty to support logins on serial ports and the keyboard.

By comparison, a Fedora system configured for desktop usage by a user that has not been thinned down can have as many as 100 processes that handle everything from the X Window System, printing, to basic system management services.

For desktop systems where the risk is mitigated (for example, where the desktop sits behind a firewall and the users are trusted), the benefits of having a lot of these applications running might well be worth the risk. Users appreciate the ability to print easily and enjoying access to a nice GUI, for example. For a server such as the Linux server, however, the risk would be too great to have unnecessary programs running, and, therefore, any program or process needed should be removed.