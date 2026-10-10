> **NOTE**
> 
> The console terminal method is only used in single-user mode. When you're booting into full multiuser mode, multiple virtual terminals are available at the physical terminal (you can switch between them with Alt+F1, Alt+F2, and so on). These terminals always present a login prompt. The `secure` and `insecure` settings in this case control whether you can log in as root or whether you are required to log in as a regular user and then use `su` to gain root access.

If others have access to the physical terminal (even if you've secured the single-user console), you have a second security hole to plug. This security weakness results from the fact that `Ctrl+Alt+Delete` causes the system to reboot, whether or not you're logged in as root, or even logged in at all. The three-finger-salute works even at the login prompt. Allowing this kind of access is appropriate in some situations (a rack-mounted server in a trusted machine room, for example), but not in others. To disable it, you'll need to add an option to your kernel configuration and rebuild the kernel:

options          SC_DISABLE_REBOOT

For a detailed discussion of kernel options and configuring your kernel, see Chapter 16, "Kernel Configuration."

# What Can Slow Down the Boot Process?

Your system might take longer than a few minutes to boot up. Because of the scripted, serial nature of the boot process, it's fairly simple to see where it's hanging. Two common culprits are `sendmail` and `httpd` (Apache); in both cases, the associated slowness results from a network connectivity problem or misconfiguration.

Both Sendmail and Apache have to figure out your machine's hostname. To do this, they need to perform a reverse lookup against the domain name server (DNS) configured in `/etc/resolv.conf`. (TCP/IP setup will be covered thoroughly in Chapter 22, "Configuring Basic Networking Services.") This lookup will have to time out for every configured name server before it fails and allows the startup process to proceed. Network timeouts are often fairly long, which is why networking is the most common cause of boot hangups. One solution to this problem is to make sure the name server listed first in `/etc/resolv.conf` is reachable from your FreeBSD machine. This ensures that Sendmail and Apache will be able to determine the machine's hostname and start up without delay. If this configuration is not possible, list `127.0.0.1` (localhost) as the first name server and disable the rest.

Incidentally, this potential slowdown is why `init` uses `mount -a -t nofs` when doing its initial "preen" to see whether it can safely go into multiuser mode. NFS has an astonishingly long timeout period, and a process waiting for that timeout to occur can be almost impossible to kill. The `mount` command, which you learned about in Chapter 8, avoids mounting NFS resources until later, in resource configuration, so that it can come up properly in multiuser mode without user intervention.

![](bbox=[0.95, 0.75, 1.0, 0.85])