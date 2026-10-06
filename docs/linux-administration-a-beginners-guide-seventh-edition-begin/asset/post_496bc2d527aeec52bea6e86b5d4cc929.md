
The Pluggable Authentication Modules (PAM) infrastructure and the name resolution libraries provide a standard of looking up user and group information for applications. It also provides a flexible way of storing that user and group information using a variety of schemes. For administrators looking to Linux, this abstraction layer can seem peculiar at first. However, consider that you can use it from flat files, to Network Information Service (NIS), to Lightweight Directory Access Protocol (LDAP) or Kerberos for authentication. This means you can pick the system that works best for you. For example, if you have an existing UNIX infrastructure that uses NIS, you can simply make your Linux systems plug into that. Or if you have an existing AD infrastructure, you can use PAM with Samba or LDAP to authenticate against the Windows domain model. Use Kerberos? No problem. And, of course, you can make your Linux system not interact with any external authentication system. In addition to being able to tie into multiple authentication systems, Linux can easily use a variety of tools, such as OpenLDAP, to keep directory information centrally available as well.

## Summary

This chapter offered an overview of what Linux is and what it isn’t. We discussed a few of the guiding principles, ideas, and concepts that govern open source software and Linux by extension. We ended the chapter by covering some of the similarities and differences between core technologies in the Linux and Microsoft Windows worlds. Most of these technologies and their practical uses are dealt with in greater detail in the rest of this book.

If you are so inclined and would like to get more detailed information on the internal workings of Linux itself, you might want to start with the source code. The source code can be found at www.kernel.org. It is, after all, open source!

## CHAPTER 2
### Installing Linux in a Server Configuration

The remarkable improvement and polish in the installation tools (and procedures) are partly responsible for the mass adoption of Linux-based distributions. What once was a frightening process many years ago has become almost trivial. Even better, there are many ways to install the software: optical media (CD/DVD-ROMs), USB Flash drives, network, and so on. Network installation options can be a wonderful help when installing a large number of hosts. Another popular method of installing a Linux distribution is installing what is known as a “Live CD”, which simply allows you to tune the software before committing to installing it. Most default configurations in Linux are already capable of becoming servers. It is usually just a question of configuring the proper application to perform the needed task. Proper practice dictates that a server be dedicated to performing only a set of tasks. Any other installed irrelevant services simply take up memory and create a drag on performance, such should be avoided.

### Hardware and Environmental Considerations

As with any operating system, before you get started with the installation process you should determine what hardware configurations will work. Each vendor publishes a hardware compatibility list (HCL) and makes it available on its site. For example, opensuse's HCL can be found at wiki.opensuse.org, Ubuntu's HCL can be found at https://ubuntu.com/support, Red Hat's HCL is at http://hardware.redhat.com (Fedora's HCL can be similar to Red Hat's), and a more generic HCL for most Linux flavors can be found at www.ldp.com/Hardware-HOWTO.

These sites provide a good reference point when you are in doubt concerning a piece of hardware. However, keep in mind that new Linux drivers are being churned out daily around the world, and no single site can keep up with the pace of development in the open source community. In general, most Intel-based and AMD-based configurations work.

### Server Design

By definition, server-grade systems exhibit three important characteristics: stability, availability, and performance. These three factors are usually improved through the purchase of better hardware, which is unfortunate to pay thousands of dollars to get the desired level of performance out of existing hardware with little tuning. With Linux this is not difficult; even better gains are outstanding.

One of the most significant design decisions you must make when managing a server may not be technical but administrative. You must design a server to be unfriendly to casual users. This means no multimedia tools, and no fancy browsers (when possible). In fact, casual use of a server should be strictly prohibited.

Another aspect of designing a server is making sure it resides in the most appropriate environment. As a system administrator, you must ensure the physical safety of your servers by keeping them in a secure room (or the equivalent). The server room itself should be well ventilated and kept cool. Overheating and noisy users can be a great danger to server stability (arguably even more).

Once the system is in a safe place, battery backup is also crucial. Backup power serves two purposes:

- It keeps the system running during a power failure so that it can gracefully shut down, avoiding data corruption or loss.
- It ensures voltage spikes and other electrical noises do not interfere with the health of your system.

Here are some specific things you can do to improve your server performance:

- Take advantage of the fact that the graphical user interface (GUI) is uncoupled from the core operating system, and avoid starting the X Window System (GUI) unless someone needs to sit at the console to run applications. After all, any other application X Window System uses memory and CPU time, both of which are better off gone.
- Determine what functions the server is to perform, and disable all unrelated functions. Not only are unused functions of memory and CPU time, but they are just another security issue to deal with.
- Unlike some operating systems, Linux allows you to pick and choose the features you want in the kernel (You'll learn about this process in Chapter 9). The default kernel is reasonably well tuned, so you won't have to worry about it. But if you need to change a feature or upgrade the kernel, you will be picky about what you add. Make sure you really need a feature before adding it.

> NOTE: You might hear an ideal recommendation to recompile your kernel only to make the most effective use of your system resources. This is no longer entirely true—other reasons to recompile your kernel might be to upgrade or add support for a new device or even remove support for components you don't need.

### Uptime

All of this chatter about server care and making sure silly things don't cause them to crash stems from the long Unix philosophy: Uptime is good. More uptime is better. The UNIX (Linux) uptime command tells the user how long the system has been running since its boot, how many users are currently logged in, and how much load the system is experiencing. The last two are useful measures that are necessary for day-to-day system health and long-term planning (for example, if the server load stays abnormally and consistently high, it might mean it's time to buy a faster/bigger server).

But the important number is how long the server has been running since its last reboot. Uptime is regarded as a sign of care, maintenance, and, from a practical standpoint, system stability. You'll often find UNIX administrators boasting about their server's uptime like you hear boasts about horsepower. This is why you'll hear UNIX administrators cursing at system changes (regardless of operating system) that require a reboot to take effect. You may deny caring about it, but in six months, you'll probably scream at anyone who reboots the system unnecessarily. Don't bother trying to explain this phenomenon to a non-admin, because they'll just look at you oddly. You'll know in your heart that your uptime is better than theirs!

### Methods of Installation

With the improved connectivity and speed of both local area networks (LANs) and Internet connections, it is becoming an increasingly popular option to perform installations over the network rather than using a local optical drive (CD-ROM, DVD-ROM, and so on).

Depending on the Linux distribution and the network infrastructure already in place, you can design network-based installations around several protocols:

- FTP (File Transfer Protocol): This is one of the earliest methods for performing network installations.
- HTTP (Hypertext Transfer Protocol): The installation tree is served from a web server.
- NFS (Network File System): The distribution tree is shared/exported on an NFS server.
- SMB (Server Message Block): This method is relatively uncommon, and not all distributions support it. The installation tree can be shared on a Samba server or shared from a Windows box.
