
- Figure out how critical and important your computer and network are and identify who or what resources can help you protect your system.
- Take steps to prevent and minimize potential damage and interruption.
- Develop and document a comprehensive contingency plan.
- Periodically test the contingency plan and revise the procedures as appropriate.

## Network security review

*Network security review focuses on assessing the security mechanisms in each of the following areas:*

- **Prevention:** Set up a firewall, enable packet filtering, disable unnecessary `xinetd` services, turn off unneeded Internet services, use TCP wrappers for access control, and use SSH for secure remote logins.
- **Detection:** Use network intrusion detection and capture system logs.
- **Response:** Develop incident response procedures.

I briefly describe some key steps in assessing the network security.

### Services started by xinetd

Many Internet services such as TELNET and `sgi_fam` (`sgi_fam` monitors changes to files) are started by the `xinetd` server. The decision to turn on some of these services depends on factors such as how the system is connected to the Internet and how the system is being used. You can usually turn off most `xinetd` services.

Check which `xinetd` services are turned on by using one of the following ways:

- Check the configuration files in the `/etc/xinetd.d` directory for all the services that `xinetd` can start. If a service is turned off, the configuration file has a line like this:
  
  ```
  disable = yes
  ```
  
  Remember that the `disable = yes` line doesn't count if it's commented out by placing a `#` at the beginning of the line.
- Type the following command to disable a service that `xinetd` can start:
  
  ```
  chkconfig servicename off
  ```
  
  where `servicename` is the name of the service (such as `telnet` or `sgi_fam`). To check the names of the services that `xinetd` can start, type the following command:

```
chkconfig --list | more
```

In the output, look for the lines that follow:

```
xinetd based services:
```

These lines list all the services that xinetd can start and whether they are on or off. For example, here are a few lines showing the status of xinetd services on a system:

```
chargen-udp: off
rsync: off
chargen: off
daytime-udp: off
daytime: off
echo-udp: off
echo: off
services: off
servers: off
time-udp: off
time: off
cups-lpd: off
sgi_fam: on
ktalk: off
imap: off
... lines deleted ...
```

In this case, the sgi_fam (a server that reports changes to any file) service is on, but everything else is off.

Also check the following files for any access controls used with the xinetd services:

- `/etc/hosts.allow` lists hosts allowed to access specific services.
- `/etc/hosts.deny` lists hosts that should be denied access to services.

### Standalone services

Many services such as the httpd (Web server) and sendmail (mail server) start automatically at boot time, assuming they are configured to start that way. You can use the chkconfig command to check which of these standalone servers are set to start at various run levels (see Book VI, Chapter 1 for more about run levels). Typically, your Red Hat Linux system starts up at run level 3 (for text login) or 5 (for graphical login). Therefore, what matters is the setting for the servers in levels 3 and 5. To view the list of servers, type the following command:

```
chkconfig --list | more
```

Here's a partial listing of what you might see:

gpm 0:off 1:off 2:on 3:on 4:on 5:on 6:off
kudzu 0:off 1:off 2:off 3:on 4:on 5:on 6:off
syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
rawdevices 0:off 1:off 2:off 3:on 4:on 5:on 6:off
netfs 0:off 1:off 2:on 3:on 4:on 5:on 6:off
network 0:off 1:off 2:on 3:on 4:on 5:on 6:off
random 0:off 1:off 2:on 3:on 4:on 5:on 6:off
saslauthd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
pcmcia 0:off 1:off 2:on 3:on 4:on 5:on 6:off
keytable 0:off 1:on 2:on 3:on 4:on 5:on 6:off
apmd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
atd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
autofs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
iptables 0:off 1:off 2:on 3:on 4:on 5:on 6:off
irda 0:off 1:off 2:off 3:off 4:off 5:off 6:off
isdn 0:off 1:off 2:on 3:on 4:on 5:on 6:off
sshd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
portmap 0:off 1:off 2:off 3:on 4:on 5:on 6:off
nfs 0:off 1:off 2:off 3:off 4:off 5:off 6:off
nfslock 0:off 1:off 2:off 3:on 4:on 5:on 6:off
sendmail 0:off 1:off 2:on 3:on 4:on 5:on 6:off
xfs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
...lines deleted...

The first column shows the names of the servers. Look at the column of entries that begin with 3: and the ones that begin with 5:. These are the ones that show the status of the server for run levels 3 and 5. The ones that appear as on are automatically started when your Red Hat Linux system starts.

If you're doing a self-assessment of your network security and you find that some servers should not be running, you can turn them off for run levels 3 and 5 with the chkconfig command like this:

```
chkconfig --level 35 servicename off
```

Replace servicename with the name of the server you want to turn off.

If you're auditing network security, make a note of all the servers that are turned on — and then try to determine whether they should really be on, according to what you know about the system. The decision to turn a particular service on depends on how your system is used (for example, as a Web server or as a desktop system) and how it's connected to the Internet (say, through a firewall or directly).

### Penetration test

A penetration test is the best way to tell what services are really running on a Red Hat Linux system. Penetration testing involves trying to get access to your system from an attacker's perspective. Typically, you perform this test from a system on the Internet and try to see if you can break in or, at a minimum, get access to services running on your Red Hat Linux system.

One aspect of penetration testing is to see what ports are open on your Red Hat Linux system. The port number is simply a number that identifies specific TCP/IP network connections to the system. The attempt to connect to a port succeeds only if a server is running on that port (or put another way, if a server is "listening on that port"). A port is considered to be open if a server responds when a connection request for that port arrives.

The first step in penetration testing is to perform a port scan. The term port scan is used to describe the automated process of trying to connect to each port number to see if a valid response comes back. Many available automated tools can perform port scanning — Red Hat Linux comes with a popular port-scanning tool called nmap (which I describe later in this chapter).

After performing a port scan, you know the potential vulnerabilities that could be exploited. Not all servers have security problems, but many servers have well-known vulnerabilities, and an open port provides a cracker a way to attack your system through one of the servers. In fact, you can use automated tools called vulnerability scanners to identify vulnerabilities that exist in your system. (I describe some vulnerability scanners next.) Whether your Red Hat Linux system is connected to the Internet directly (through DSL or cable modem) or through a firewall, use the port-scanning and vulnerability-scanning tools to figure out if you have any holes in your defenses. Better you than them!

### Exploring Security Testing Tools

Many automated tools are available to perform security testing. Some of these tools are meant for finding the open ports on every system in a range of IP addresses. Others look for the vulnerabilities associated with open ports. Yet other tools can capture (or sniff) those weaknesses and help you analyze them so you can glean useful information about what's going on in your network.

You can browse a list of the top 50 security tools (based on an informal poll of nmap users) at www.insecure.org/tools.html. Table 4-4 lists a number of these tools by category. I describe a few of the freely available vulnerability scanners in the next sections.

Table 4-4 Some Popular Computer Security Tools

| Type | Names of Tools |
|---|---|
| Port scanners | nmap, Strobe |
| Vulnerability scanners | Nessus Security Scanner, SAINT, SARA, Whisker (CGI scanner), ISS Internet Scanner, CyberCop Scanner, Vetescan, Retina Network Security Scanner |
