
# 3.5 R* Services

zoro.com or just the first component of the name zero.

3. Also, it verifies that the source port is less than 1024, which only root can open on a Linux or UNIX system. The only way that the daemon knows which user on the requesting system is making the request is that rsh sets-UID to root and determines the real UID of the account invoking it, looks up this UID in /etc/passwd to find the user name, and sends this to the other system.

In the Linux and UNIX world, only root is allowed to open a port number less than 1024 so the daemon insists that the requesting system be using such a low port number. This might be called the "big system idea." It sounds secure.

## 3.5.2 R* Insecurity

Security can be broken in a number of ways.

1. The cracker can install a bogus .hosts file. This is a classic case where both the ideas presented in "Understanding Linux Security" on page 12 come into play. The cracker is stuck in a maze of twisty little passages. If she wants to break into joe's account she knows she needs to find a series of passages that get her to install a bogus .hosts file.

If Joe's home directory is writable by all (or can be made so) she might be able to find a suitable file. In older versions of rsh it did not care about garbled lines as long as a line matches the invoking system's name.

Suppose joe had a mail folder from a security mailing list showing cracker sites. All the cracker had to do was find any random account to use and mv this folder to .hosts. This random account might be an incorrectly configured FTP anonymous or a badly written Web server CGI script.

2. If the intruder can access the initiating system or if it is not Linux or UNIX, the UNIX/Linux security model (that only root can operate from a port number less than 1024) fails. There is another hole here, which is the security level of remote systems that you are considering granting access to your system.

3. The intruder can configure his system to pretend to be a trusted system, for example, zoro.com, for some techniques for doing this. In many cases this is quite easy.

4. The intruder can compromise the DNS that the server relies on. That DNS may be on a system different from the system serving rsh.

The best solution to rsh is to disable it. The "Host masquerades" cannot be adequately defended if there are any untrusted systems on the LAN and rsh is at risk for suffering the session being sniffed. SSH was created explicitly to solve these problems. Have your users make use of it.

Still, if your LAN is secure from internal attacks and sniffing, then TCP Wrappers around rsh can be secure. The rcp program allows copying files between systems and operates in the same way as rsh and it has the same problems and solutions. Have your users use the scp command in the SSH package. It works like rcp and has all of the rock solid security of SSH. The rexec program works like rsh and has similar problems too. The alternative is ssh.

The login program has all the problems and solutions of rsh and rcp and it has the additional problem that if the client system (the requesting system) is not mentioned in the user's .rhosts file or the /etc/hosts.equiv file on the server system, the invoker will need to supply a password. This password is sent over the network in clear text, allowing a sniffer then to use that password to access that account via login, telnet, ftp, popclient, etc.

The R* services can be disabled by commenting out the lines in /etc/inetd.conf that start with:

```
shell
login
exec
```

The rcp command uses the same remote service as rsh, shell.

# 3.6 DNS (named, a.k.a. BIND)

![](img/7d04225c75a86d3cf4bd6077596f35b2_170_0.png)

The named program, meaning the name daemon or DNS daemon, is the program that converts a fully qualified host name, such as www.realworldlinuxsecurity.com to its numeric IP address like 192.168.57.8.

Without it there would be no www.cute-name.com; there would be harder to deal with and less flamboyant. Many leaf nodes do not need to run it. Instead they simply specify the numeric IP addresses of their name servers in /etc/resolv.conf and any program, such as sendmail, telnet, ftp, and Netscape will read /etc/resolv.conf and make the request for DNS lookup directly to the remote server system's named. Small "internal" networks may not use DNS at all, they will rely on each system's /etc/hosts file being set up.

## 3.6.1 Limiting Consequences of a Named Compromise

| DANGER LEVEL ☠ ☠ ☠ |

Starting in version 8.1.2, named no longer needs to run as root. The only reason it is needed to run as root was to open TCP and UDP ports 53. Now one can use the -u flag to have it do a setuid() call to the specified user after it opens the ports. The argument may be either a user name or a numeric UID. Similarly, there is the -g flag to request a setgid(). Making use of -u and -g is strongly encouraged to eliminate all root vulnerabilities in named in case another buffer overflow is encountered, such as the one in named versions 8.2 and 8.2.1.

The user and group named should be run under should be different from anything else in the system to isolate it; dns is a fine choice. Certainly, an encrypted password of "*" will prevent logins on this account. Specifying /dev/passwd or /dev/null as the user's login shell will further lock down the account.

Recall that named's job is to determine the IP for a host and all it needs to do is to talk on ports 53 and read and write a few of its files. It is an excellent candidate for being in a chroot jail; it cannot harm anything (other than possibly lying about IP addresses). On Red Hat, Mandrake, and other distributions that use the /etc/rc.d/init.d/named file, change the line reading:

```
daemon named
```

to:

```
daemon named -u dns -g dns
```

The user and group dns should be created having a UID and GID that is not otherwise used, with a disabled password, a shell of /dev/null, and its own home directory, for example, /home/dns with mode 700.

The -t flag may be used to specify a directory to have named chroot itself during startup. You will need to copy any dynamic libraries to /home/dns/lib that named will need, as well as the configuration files that it requires, typically /etc/named.conf. Because root can break out of a "prison," it is critical if you also use the -u and -g flags to cause named to switch to an unprivileged user after opening ports 53.

## 3.6.2 To Serve Man

Like the Twilight Zone episode, you need to decide how other systems might use your systems' services. You do not want systems outside your network to be able to see the names and IP addresses of all your internal systems because that would be an invitation for cracking. At the same time you will want all your inside systems to see each other.

The solution is to have two name servers, one for inside use and one for the rest of the world to use. The name servers that you specify to your domain registrar (such as Network Solutions) would be the servers for external use. Their configuration files would list only externally visible systems such as the corporate mail, Web, and FTP servers and any other systems that receive e-mail directly or which allow SSH access.

A useful "implementation detail" is that small requests, such as converting a host name to a numeric IP, are done via UDP and large requests such as dig requests and zone transfers via TCP.

You have never authorized external sites to do zone transfers or dig commands of your site. This is because a zone transfer will allow an external site to learn the names and IP addresses of all your internal systems. This would enable a cracker to know what systems are available for cracking. Additionally, the host names might reveal confidential information.

For example, a host name of afradar.r_d.pentacorp.com might be a Research and Development site for radar systems for the Air Force. Assume that the spying during this cracking reveals that Pentacorp has recently met with Lockheed and that Lockheed is the prime contractor for the Air Force YF22 fighter. This implies that pentacorp.com is the subcontractor for the radar work or is trying to win that contract. That is a whole lot of information that was garnered from just a host name.

All you need to do is to block TCP requests to port 53 of your "external" name server from systems outside your network. For large organizations, such as a Fortune 500 company or large government bureau, a DNS server may hold the names of hundreds or thousands of systems.

One DoS attack is to repeatedly request a zone transfer from your name servers. This ties up your name servers as well as bandwidth. By blocking TCP port 53, you prevent this attack. A better solution is to use the access controls supported by recent versions of named.

The IP addresses that you tell people in your organization to specify in their /etc/resolv.conf would be the name servers for internal use, of course. Access to the internal name server's ports 53 (both TCP and UDP) from outside the organization should be blocked by IP Chains. This blocking is to prevent crackers from "sucking" DNS information from port 53 of every IP in your domain and encountering your internal name server.

Even though your firewall may allow access to these internal systems, there are some recent exploits that allow tunneling through firewalls. Additionally, just knowing the names of systems might allow your competition to learn about your development activities.
