
The TCP wrappers, or simply *wrappers*, control access to network daemons. While the program must be written to support TCP wrappers, most modern software has supported wrappers for many years. Wrappers are fairly simple to configure and don't require much networking knowledge. As access controls go, however, wrappers are fairly limited. Wrappers do let you do interesting things with connections and with daemons offering connections, though, which is why we'll discuss it.

*Packet filtering* controls which traffic the system allows to pass through it and which traffic it rejects. Most firewalls are packet filters with a pretty GUI on top, but you can use FreeBSD packet filtering and proxy software to build a solid firewall in and of itself. A rejected connection request never reaches any userland program; it's blocked in the network stack. Packet filtering can control access to any program, service, or network port but does require more networking knowledge.

*Blacklisting* is useful when you want a program to be able to decide to stop listening to a remote host. The most common tool for blacklisting is fail2ban (*https://www.fail2ban.org/*), which is flexible but requires much special configuration. FreeBSD includes blacklistd, an easier-to-configure blacklisting tool that requires integration with programs that use it.

Which should you use? For basic TCP/IP access control, I recommend always using a packet filter. Only use TCP wrappers if you need their specific features. I discuss blocking and allowing connections with TCP wrappers only as a prerequisite to those advanced features. If you want a service to block clients after a certain number of failed connection attempts, consider blacklistd.

With wrappers or packet filtering, you must decide whether you want a default accept or default deny traffic control policy.

## Default Accept vs. Default Deny

One of the essential decisions in any security policy is between default accept and default deny. A *default accept* security stance means that you allow any type of connection except what you specifically disallow. A *default deny* stance means that you allow connections only from specified parts of the internet and/or to specified services and that you refuse all other connections. The default is used unless you make a specific rule dictating otherwise. Once you've chosen your default security stance, you create exceptions one way or another to either provide or block services as necessary. The choice is really between whether you offer services to the world (default accept) or only to a select few (default deny).

For example, company policy might dictate that the intranet web server must be accessible only from within the company. If so, adopt a default deny stance and explicitly list who may access the server. Alternatively, if you have a public website but want to block certain parts of the internet from accessing it for whatever reason, adopt a default accept stance.

I always recommend a default deny stance. If you don't make a choice, however, you've chosen default accept.

Choosing a default doesn't mean that the default must be implemented without exceptions. My public web servers have a default deny security stance, but I specifically allow the world to access the websites. The machine rejects attempts to connect to other programs unless they come from one of a few specified IP addresses. This is a perfectly acceptable default deny stance.

Different security tools implement these stances in different ways. For example, with TCP wrappers, the *first* matching rule is applied. If your last rule denies everything, you've established a policy that says, “Unless I've specifically created a rule earlier to permit this traffic, block it.” On the other hand, with the PF packet filter, the *last* matching rule applies. If your first rule says, “Block all traffic,” you've implemented a policy that says, “Unless I specifically create a later rule to permit this traffic, block it.”

Both default accept and default deny annoy the sysadmin. If you have a default accept policy, you'll spend your time continually plugging holes. If you choose a default deny policy, you'll spend your time opening access for people. You'll repeatedly apologize for either choice.

With default deny, you'll say things like, “I've just activated service for you. I apologize for the inconvenience.” With default accept, you'll say things like, “. . . and that's why the intruders were able to access our internal accounting database and why we lost millions of dollars.” In the latter case, “I apologize for the inconvenience” *really* doesn't suffice.

# TCP Wrappers

Remember from Chapter 7 that network connections are made to various programs that listen for connection requests. When a program is built with TCP wrappers support, the program checks the incoming request against the wrappers configuration. If the wrappers configuration says to reject the connection, the program immediately drops the request. Despite the name, TCP wrappers work with both TCP and UDP connections. Wrappers are a long-running Unix standard that have been incorporated into FreeBSD. Individual programs might or might not work with wrappers; while just about everything in the base FreeBSD system does, some third-party software doesn't.

TCP wrappers are implemented as a shared library, called *libwrap*. As seen in Chapter 17, shared libraries are small chunks of code that can be shared between programs. Any program that links with libwrap may use the TCP wrappers functions.

Wrappers most commonly protect *inetd(8)*, the super server that handles network requests for smaller programs. We'll discuss inetd in Chapter 20. While our examples cover *inetd(8)*, you can protect any other program that supports wrappers in exactly the same way. While wrappers help protect *inetd(8)*, make sure *inetd(8)* doesn’t offer any unnecessary services, just as you do for the main system.

# Configuring Wrappers

Wrappers check each incoming connection request against the rules in /etc/*hosts.allow*, in order. The first matching rule is applied, and processing stops immediately. This makes rule order very important.

Each rule is on a separate line and is made up of three parts separated by colons: a daemon name, a client list, and a list of options. Here's a sample rule:

```
ftpd : all : deny
```

The daemon name is **ftpd**; the client list is **all**, meaning all hosts; and the option is **deny**, telling wrappers to reject all connections. Nobody can connect to the FTP server on this host unless an earlier rule explicitly grants access.

In the early examples, I refer to only two options: **accept** and **deny**. They allow and reject connections, respectively. We'll discuss the additional options later.

## Daemon Name

The daemon name is the program's name as it appears on the command line. For example, **inetd(8)** starts the **ftpd(8)** program when it receives an incoming FTP request. The Apache web server starts a program called *httpd*, so if your version of Apache supports wrappers, give the daemon name as **httpd**. (Note that Apache doesn't run out of **inetd**, but it can support wrappers anyway.) One special daemon name, **ALL**, matches all daemons that support wrappers.

If your system has multiple IP addresses, you can specify, as part of the daemon name, different wrapper rules for each IP address that a daemon listens on:

```
ftpd@203.0.113.1 : ALL : deny
ftpd@203.0.113.2 : ALL : accept
```

In this example, we have two daemon names, **ftpd@203.0.113.1** and **ftpd@203.0.113.2**. Each has a separate TCP wrapper rule.

## The Client List

The client list is a list of specific IP addresses, network address blocks, hostnames, domain names, and keywords, separated by spaces. Hostnames and IP addresses are simple: just list them.

```
ALL : netmanager.absolutefreebsd.com 203.0.113.5 : allow
```

With this rule at the top of `/etc/hosts.allow`, wrappers allow my netmanager machine and any host with an IP address of 203.0.113.5 to connect to any service on this host. (I could block this access by other means, mind you.)

Specify network numbers in the client list with a slash between the IP address and the netmask, as discussed in Chapter 7. For example, if script kiddies attack your server from a bunch of addresses that begin with 192.0.2, you could block them like this:

```
ALL : 192.0.2.0/255.255.255.0 : deny
```

You can also use domain names in client lists by prefixing them with a dot. This works through reverse DNS, which means that anyone who controls the DNS server for a block of addresses can evade this restriction.

```
ALL : .mycompany.com : allow
```

If you have a long list of clients, you can even list them in a file and put the full path to the file in the client space in `/etc/hosts.allow`. I've been on networks with large numbers of widely scattered hosts, such as an ISP or corporate network environment with network management workstations scattered across the world. Each workstation shared the same wrapper rules as every other workstation and appeared on half a dozen lines in `hosts.allow`. By maintaining a single file with a workstation list, I could centralize all changes.

In addition to specifically listing client addresses and names, wrappers provide several special client keywords to add groups of clients to your list. Table 19-1 shows the keywords and their usage.

Most of the client keywords listed in Table 19-1 require a working DNS server. If you use these keywords, you must have a very reliable DNS service, and you must remember the vital link between DNS and the rest of your programs. If your DNS server fails, daemons that use wrappers and those keywords can't identify any hosts. This means that
