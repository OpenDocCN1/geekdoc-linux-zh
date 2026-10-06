
# UNIX SYSTEM MANAGEMENT PRIMER PLUS

more time to work on their technical duties, and the users benefited by having people dedicated to handling their complaints and representing them to IT staff, in a business environment, if the IT department does not have the resources, a member of the human resources department often handles these duties, working closely with the IT department for technical guidance.

# Enforcing Your Policies

A policy is useless unless it is not enforced. For example, if your usage policies prohibit running CPU-intensive processes on your login servers, enforce that policy by killing these processes (or lowering their priority) and notifying the user of your usage. Repeated violations should result in some sort of action, such as account suspension. The appropriate punitive action, however, depends on the type of service you are offering and how your management and human resources department want to handle these issues.

If you do not enforce policies consistently, users will consider your policies advisory (if they read them all) and will do as please on your systems. Lack of compliance with usage policies is aggravating to all who use or run the system, and it can even compromise the performance and security of your services. Chapter 16 offers full details about writing and enforcing usage policies.

# Being Paranoid with Security Breaches

As learned in earlier sections of this chapter, if you suspect that a user has compromised the security of your system or is attacking another system, you should disable the account immediately and kill all of that user's processes. Although you need to begin gathering evidence at once, finding and stopping the security breach is even more critical. You must eliminate the holes in your system to minimize existing damage and prevent further damage before spending time on thorough investigation.

![](img/894492738e879267320b8d6f9a044180_465_0.png)

# Give Users of Compromised Accounts a Heads-Up

Many security incidents begin with compromised accounts, so the person using the account you are disabling is likely not the account's rightful owner. If possible, contact the owner of the account by phone or an alternate email account to notify him or her of the situation.

![](img/894492738e879267320b8d6f9a044180_465_1.png)

# Disable Inactive Accounts

Consider disabling the accounts of users who will remain idle for long periods, such as people on long vacations or sabbaticals. This will prevent unauthorized usage of these accounts that would otherwise go unnoticed by the real user's absence.

# Dealing with Remote User Problems

When your Unix system is linked to the Internet, you can experience some interesting user problems. Your publicly available systems have the potential to be reached by millions of people; the chances are great that eventually you'll experience a problem with several of those people; some of the more common problems remote users can cause the following:

- Denial-of-service attacks
- Remote exploits that execute code on your system without an account
- Using a compromised account to store and publish pirated software
- Using your mail hub to send spam

Each of these incidents is covered in more detail in Chapter 13.

Unless you are a tier ISP, remote users will be connecting to your systems through another provider. This makes problems with these users much more difficult to manage since you may not know who they are or where they are located. To fully track, understand, and resolve remote user problems, you must include those in your efforts. In general, the steps involved in resolving remote user problems are as follows:

1. Identify the address from the remote user is connecting.
2. Disable the mechanism used to gain access to your system. This could entail disabling an account, closing a security hole by applying a patch, or denying traffic from the remote address.
3. Identify the administrators of the server at that address.
4. Contact the administrators of the remote server, providing log evidence when available.
5. If the remote administrators do not respond, follow up with the remote responsible for the address space in which that server resides.
6. Follow up with remote administrators until the problem users are found or the accounts used by them are disabled.

The sections that follow provide some general guidelines and practical advice for remote incident management.

# Identifying Remote Site Addresses

If a user has logged into your system, you can use any of a number of simple commands to determine from what address the user has connected to. There are also ways to determine where network traffic is coming from even when users are not actually logged in.

# Back-Tracking Through Multiple Addresses

The address that a user has connected from may be the first in a longer chain of addresses. For example, a user can Telnet from his desktop computer to server1, from server1 to server2, and from server2 to your system. You will need the cooperation of the administrators of each server to trace the connections back to the original user's machine. You should also take into account IP spoofing, which will make tracing this chain of addresses extremely difficult, if not impossible. You can read more about IP spoofing in the section titled "Exploits and Attacks" in Chapter 13.

# Using to Locate Remote Users

The who command displays a list of users who are currently logged in to your system, along with a number of statistics such as the user's remote address. Just filter out the user you are looking for with grep; the remote address is the last field. In this example, the user joeuser has logged in from server4.example.com:

```bash
bash$ who joeuser
joeuser pts/2      Apr 9 08:29 (server4.example.com)
```

# Using to Locate Remote Users

The last command shows all login activity for a system, including current logins. last is the first command you should use to look for historical data. Without arguments, last displays all of the logins recorded on a system's wtmp file. If you supply a username, last displays only logins for particular user; you can also specify the number of logins displayed on the line. The following example shows the response to last command asking for the display of last five logins for joeuser:

```bash
bash$ last -5 joeuser
joeuser pts/2      server4.example.com - Tue 9 08:29
joeuser pts/2      141.158.35 - Mon 8 17:59 (02:18)
joeuser pts/2      141.158.35 - Mon 8 13:37 (04:09)
joeuser pts/2      141.158.35 - Mon 8 13:37 (00:00)
joeuser pts/2      141.158.35 - Mon 8 11:03 (02:08)
```

The remote server is in the third field, but there is a problem with it—the name is limited to 16 characters! This is the major pitfall with last; even today operating systems support longer hostnames, most notable of which is OpenBSD. You may need to rely on other logs to determine the hostname; TCP Wrappers can do this for services like Telnet and SSH.

# Failed Login Attempts

Red Hat Linux has a central database of failed login attempts in /var/log/btmp, which can be viewed with the last command. This can show who is trying to access your system when they are not successful.

# Using tcpdump and sniff to Locate Remote Users

Users do not have to log in to your system to cause problems; a simple denial-service attack or an exploit for a network service vulnerable to buffer overflows are as damaging to your system as any local user. Locating these is much more difficult because they are not actually logged into systems you can control. However, as long as they continue to send traffic to your machine, you can sniff that traffic and identify the remote addresses using tools like tcpdump and sniff (both are discussed in Chapter 13). For example, if someone is repeatedly using Telnet to connect to your server, to log in as a certain user and failing, you can figure out where those connections are coming from by port 23, Telnet's port (output truncated), as follows:

```bash
# tcpdump -n port 23
kernel, protocol ALL, data packet
tcpdump: listening on all devices
20:55:03.008065 eth0 < 192.168.1.21:52136 > 192.168.1.66:telnet: S 3617855084:36 176855084(0) win 24820 <nop,nop,sack> ms 140> (DF)
20:55:03.008017 eth0 > 192.168.1.66:telnet < 192.168.1.21:51236: S 715025216:711 025810(0) ack 3617855085 win 31220 ms 146>nop,nop,sack> (OK)
20:55:03.001118 eth0 < 192.168.1.21:51236 > 192.168.1.66:telnet: . 1:(0) ack 25 win 24820 (DF)
20:55:03.002902 eth0 > 192.168.1.21:51236 > 192.168.1.66:telnet: P 1:(24) ack 25
20:55:03.002963 eth0 > 192.168.1.66:telnet < 192.168.1.21:51236: . 1:(0) ack 25 win 31220
20:55:03.015742 eth0 > 192.168.1.66:telnet > 192.168.1.21:51236: P 1:(13(2) ack 25 win 31220 (DF)
```

Assuming your server is located at 192.168.1.66, you can see where the connection is coming from and can work with the remote administrators to figure out who the culprit is.

# Connections to Popular Services Can Be Difficult to Trace

Tracking down connections for a popular service like Telnet can be a daunting task on a busy server. You may not be able to distinguish one from a swarm of other connections to the same port. In particular you must rely on tools like last and last to identify the addresses from which various users have connected to your system.

# Identifying a Remote User using the IDENT Protocol

The IDENT protocol, specified by RFC 931 and RFC 1413, supports the identification of a remote user to sites that the user connects to. The only requirement for the remote server must be a running server that supports the IDENT protocol, such as ident. A free implementation of identd is available at http://www.lysator.liu.se/~pen/pident—this is the same identd package that is installed on Red Hat Linux.
