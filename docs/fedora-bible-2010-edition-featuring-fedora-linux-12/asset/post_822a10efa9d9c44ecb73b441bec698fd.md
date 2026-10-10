
## Security Checklist

protected from each other, as well as from an outsider who takes over one user account. Setting up group accounts can extend the concept of ownership to multiple users. See Chapter 10 for more on setting up user accounts and “Using Password Protection” later in this chapter.

- **Read, write, and execute permissions** — Every item in a Linux file system (including files, directories, applications, and devices) can be restricted by read, write, and execute permissions for that item’s owner and group, as well as by all others. In this way, for example, you can let other users run a command or open a file, allowing them to change *it*. See Chapter 4 for information on setting file and directory permissions.

- **Protect root** — In standard Linux systems, the root users (as well as other administrative user accounts such as apache) have special abilities to use and change your Linux system. Protect the root account’s password and don’t use the root account when you don’t need to. An open shell or desktop owned by the root user can be a target for attack. Running `system-config-*` windows as a regular user (and then entering the root password as prompted) and running administrative commands using `sudo` can reduce exposure to attacks on your root account. See Chapter 9 for information on handling the root user account.

- **Use trusted software** — While there are no guarantees with any open source software, you have a better chance of avoiding compromised software by using an established Linux distribution (such as Fedora). Software repositories where you get add-on packages or updates should likewise be scrutinized. Using valid GPG public keys (which use signatures and encryption), you can ensure that the software you install comes from a valid vendor. And, of course, always be sure of the source of data files you receive before opening them in a Linux application.

- **Get software updates** — As vulnerabilities and bugs are discovered in software packages, every major Linux distribution (including Fedora) offers tools for getting and installing those updates. Be sure to get those updates, especially if you are using Linux as a server. See Chapter 5 for information on using PackageKit and yum to get software updates.

- **Use secure applications** — Even with software that is valid and working, some applications offer better protection from attack or invasion than others. For example, if you want to log in to a computer over the Internet, the secure shell service (SSH) is considered more secure than `rlogin` or `telnet` services. Also, some services that are thought to be insecure if you expose them on the Internet (such as Samba and NFS), can be used more securely over the Internet through virtual private network (VPN) tunnels (such as IPsec or CIPE).

- **Use restrictive firewalls** — A primary job of a firewall is to accept requests for services from a network that you want to allow and turn away requests that you don’t (primarily based on port numbers requested). A desktop system should refuse requests that come in on most ports. A server system should allow requests for a controlled set of ports. This chapter describes how to set up a firewall using iptables.

- **Enable only services you need** — To offer services in Linux (such as Web, file, or mail services), a daemon process will listen on a particular port number. Don't enable services you don't need. In fact, you shouldn't even install server software you don't need. See Chapter 11 for information on using system services. For even better security, don't install any software you don't use, be it server software or any other kind.

> **NOTE:** A program that runs quietly in the background handling service requests (such as sendmail) is called a daemon. Usually, daemons are started automatically when your system boots up, and they keep running until your system is shut down. Daemons may also be started on an as-needed basis by xinetd, a special daemon that listens on a large number of port numbers, and then launches the requested process.

- **Limit access to services** — You can restrict access for a service you want to have on to a particular host computer, domain, or network interface. For example, a computer with interfaces to both the Internet and a local area network (LAN) might limit access to a service such as NFS to computers on the LAN, but not offer those same services to the Internet. Services may limit access in their own configuration files or by using TCP/IP wrappers (described later in this chapter).

- **Check your system** — Linux has tons of tools available for checking the security of your system. After you install Linux, you can check access to its ports using nmap or watch network traffic using Wireshark (formerly called Ethereal). You can also add popular security tools such as Nessus or L0phtCrack (or similar tools) to get a more complete view of your system security.

- **Monitor your system** — You can log almost every type of activity on your Linux system. System log files, using the syslogd and klogd facilities, can be configured to track as much or as little of your system activity as you choose. The logwatch facility provides an easy way to have the potential problem messages forwarded to your administrative e-mail account. Linux logging features are described later in this chapter. You can get add-on packages such as tripwire and portscan tools, to check your system for tampering and deal with someone scanning your ports, respectively.

- **Use SELinux** — SELinux is an extraordinarily rich (and complex) facility for managing the access of nearly every aspect of a Linux system. It addresses the if-I-get-root-access-I-own-your-box shortcomings of Linux and UNIX systems for highly secure environments. Fedora offers a useful, limited set of SELinux policies that are turned on by default. Despite improvements, however, many Linux system administrators still just turn off SELinux because they find it difficult to use. Chapter 9 provides an overview of SELinux, along with explanations of how it is implemented in Fedora.

This checklist should give you a good starting point with many aspects of security in Linux. Each of these topics is covered in greater depth throughout this chapter and in other chapters throughout this book that I have just referenced. However, computer security is an ongoing battle, so I recommend you check out the following Web sites to get a deeper, continuing experience with Linux security:

- **CERT** (*www.cert.org*) — The CERT Coordination center follows computer security issues. Check their home page for the latest vulnerability issues. The site has articles on security practices (http://www.cert.org/search_pubs/search.php). It also has recommendations on what you should do if your computer has been compromised (*www.cert.org/tech tips/win-UNIX-system_compromise.html*), although this is now considered somewhat dated.

- **Red Hat Security Alerts** (*www.redhat.com/security*) — For RHEL security issues (that typically relate to Fedora systems as well), you should check out the resources available from this site. From here you can look for and read about available updates. You can also get information on security training and consulting from Red Hat, Inc.

- **Red Hat Enterprise Linux 4.5 Security Guide** — This older but still relevant guide provides an in-depth look at Linux security, specifically as it relates to Red Hat Enterprise Linux and Fedora. You can access this guide online from the following address:

www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/en-US/Security_Guide/

## Using Password Protection

Passwords are the most fundamental security tool of any modern operating system and consequently, the most commonly attacked security feature. It is natural to want to choose a password that is easy to remember, but very often this means choosing a password that is also easy to guess. Crackers know that on any system with more than a few users, at least one person is likely to have an easily guessed password.

> **NOTE:** The opposite approach, that of requiring all users to select really complicated passwords, may seem much better, but you end up with passwords so complex users write them down. Then, any person that finds the note can get in. Ideally, passwords would lie somewhere in between — easy to remember but hard to crack.

By using the “brute force” method of attempting to log in to every account on the system and trying the most common passwords on each of these accounts, a persistent cracker has a good shot of finding a way in. Remember that a cracker will automate this attack, so thousands of login attempts are not out of the question. Obviously, choosing good passwords is the first and most important step to having a secure system.

Here are some things to avoid when choosing a password:

- Do not use any variation of your login name or your full name. Even if you use varied case, append, or prepend numbers or punctuation, or type it backwards, this will still be an easily guessed password.
- Do not use a dictionary word, even if you add numbers or punctuation to it.
