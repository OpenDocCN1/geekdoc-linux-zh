
## Chapter 3

## Enumeration

+ IN THIS CHAPTER:
- Enumerate Remote Services
- Automated Banner-Grabbing
- Summary

## 36 Part I: Hacking Techniques and Defenses

After performing port scans on target hosts, an intruder will know exactly which hosts are alive and what ports they have. Armed with this information, the logical next step is to enumerate information such as usernames, file shares, and operating system version numbers from services listening on the specific ports. Only after obtaining such information may an attacker move on exploiting particular vulnerabilities as discussed in the next chapter.

Many remote daemons display a banner message when a connection is made to the port they are listening on. Banner messages can give up information about services, such as their identity and version information. The process of obtaining banners from remote services is known as banner grabbing. Since most daemons allow their banners to be changed, you should take advantage of this capability.

Although it is a good idea to change server banners in order to confuse potential intruders, keep in mind that it will not deter the more sophisticated attackers.

## ENUMERATE REMOTE SERVICES

What follows is a list of services that are known to be susceptible to enumeration. They are sorted by the port numbers they usually listen on (see the file /etc/services on your Unix or Linux host for a comprehensive list).

> Any of the services listed here can be configured to listen on a nonstandard port. Some services use non-ASCII characters to communicate, and are difficult to identify. Tools such as Amap, available at http://www.thehackerschoice.com/releases.php, can be used to detect services:

```bash
$ amap -sT intranet.somecompanyasanexample.com 9934
Total amount of tasks to perform: 15
Amap1.2.1b started at Sun Mar 9 09:30:22 2003, stand back and keep the children away.
Protocol on IP 192.168.1.3 port 9934 tcp matches ssl
Protocol on IP 192.168.1.3 port 9934 tcp matches http
Unidentified ports: None.
Amap1.2.1b ended at Sun Mar 9 09:30:59 2003
```

In this example, Amap successfully discovered that host intranet.somecompanyasanexample.com was running HTTPS on port 9934. This is useful information, since the standard port for HTTPS is 443.

## Block and Stop Unnecessary Services

Some services are configured to accept connections from any source IP address. For example, an HTTP server for an e-commerce organization must accept connections from any IP address in order to allow users in all locations to view the organization's web site. In such a case, it is impossible for an organization to hide the fact that they are running an HTTP server.

However, depending on the organization's requirements and network architecture, some services may only expect connections originating from authorized IP addresses. In such cases, firewall rules must be put in place to ensure that connections originating from unauthorized IP addresses are blocked. In addition, unnecessary services must be turned off or blocked by firewall rules. This will prevent the exploitation and identification of services that should not be accessible by unauthorized hosts.

## FTP (File Transfer Protocol): 21 (TCP)

FTP, as the name suggests, is a protocol for transferring files from one host to the other.

## Obtain the FTP Server Banner

FTP servers usually print version information when connected to. An FTP client can be used to connect to an FTP server in order to obtain its banner. For example:

```bash
$ ftp 192.168.1.1
Connected to 192.168.1.1 (192.168.1.1).
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
Name (192.168.1.1:username):
```

The telnet client can also be used to connect to the FTP port directly to obtain the banner information:

```bash
$ telnet 192.168.1.1 21
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^'.
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
```

## Change the FTP Server Banner

If you are running a WU-FTPD server, edit the /etc/ftpaccess file or are using the greeting directive to change the server banner. For example:

```text
greeting text No banner information available. Sorry.
```

## SSH (Secure Shell): 22 (TCP)

SSH is a secure protocol for exchanging data. It can be used to log in to remote machines, execute commands remotely, and transfer files. Since communication with SSH is encrypted, it is a worthy replacement for remote-login solutions such as telnet, rlogin, and FTP.

## Obtain the SSH Server Banner

Although SSH communication is encrypted, the SSH daemons do print version information in clear when connect with a telnet client:

```bash
$ telnet 192.168.1.1 22
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^'.
SSH-1.99-OpenSSH_3.4p1
```

## Change SSH Version Information

The version information displayed by the banner, “OpenSSH_3.4p1”, in the preceding example, may be changed by obtaining and editing the OpenSSH source. Use the grep command to find the version string within the OpenSSH source code. Once this string has been changed, recompile and reinstall OpenSSH.

The banner also displays the protocol version, “SSH-1.99”, in the preceding example. Do not change or remove this information since SSH clients this string to recognize protocol and server information. Changing this value may cause some SSH clients to stop functioning properly.

## Telnet: 23 (TCP)

Telnet is a clear-text protocol used to log in to remote machines.

## Obtain the Telnet Server Banner

Banner information from a telnet daemon can be obtained by simply telnetting to the server:

```bash
$ telnet 192.168.1.1
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'
SunOS 5.8
login:
```

## Change the Telnet Server Banner

In order to change the telnet banner, you will need to write a wrapper around it. Assuming that you are running telnetd in inetd, edit your /etc/inetd.conf, and change

```text
telnet stream tcp nowait root /usr/sbin/in.telnetd in.telnetd
```

to
```text
telnet stream tcp nowait root /usr/sbin/in.telnetdwrapper in.telnetd
```

Now, you must create the file /usr/sbin/in.telnetdwrapper with the following contents:

```sh
#!/bin/sh
/bin/echo "My banner\r"
exec /usr/sbin/in.telnetd
```

> If you are using inetd, edit the telnet file found in your xinetd.d directory appropriately.

You must restart inetd or xinetd in order for changes to take effect.
Note that some versions of telnetd allow you to change banner information by editing the /etc/issue.net file.

## SMTP (Simple Mail Transfer Protocol): 25 (TCP)

SMTP is a protocol used on the Internet to transfer e-mail messages.

## Grab the SMTP Server Banner

SMTP daemon banners can be obtained by telnetting to port 25 of the host SMTP is running on:

```bash
$ telnet 192.168.1.1 25
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^'
220 192.168.1.1 ESMT Sendmail 8.10.2+Sun/8.10.2; Tue,
14 Jan 2003 09:28:02-0500 (EST)
```

## Change the SMTP Server Banner

If you are using Sendmail, you can change the SMTP banner by editing the /etc/sendmail.cf file and changing the value of the SmtpGreeting field.

## Enumerate Users using EXPN and VRFY

EXPN and VRFY are two commands supported by SMTP that allow for username enumeration. EXPN and VRFY can be used to confirm the existence of a particular username. EXPN can be used to enumerate the names and e-mail addresses of all the users on a particular group e-mail alias.

Here is an example of VRFY:

```bash
$ telnet mail.somecompanyexample.com 25
Trying 10.0.0.11...
Connected to mail.somecompanyexample.com.
Escape character is '^'
220 mail.somecompanyexample.com ESMTP Sendmail 8.11.6/
8.11.6; Wed, 15 Jan 2003 22:04:06-0500 (EST)
VRFY smith
250 2.1.5 <smith@sales.somecompanyexample.com>
```

Here is an example using EXPN:

```bash
$ telnet mail.somecompanyexample.com 25
Trying 10.0.0.11...
Connected to mail.somecompanyexample.com.
Escape character is '^'
220 mail.somecompanyexample.com ESMTP Sendmail 8.11.6/
8.11.6; Wed, 15 Jan 2003 22:10:11-0500 (EST)
EXPN marketing-team
250-2.1.5 <bob@marketing.somecompanyexample.com>
```
