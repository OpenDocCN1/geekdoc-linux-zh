
# Listing 12.1 Running the imaps Service from xinetd

```
service imaps
(
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/stunnel
    server_args = -1 /usr/sbin/imap --imapad
    log_on_failure += USERID
)
```

stunnel, however, has nothing specific to POP, IMAP, or e-mail. It can be used to secure a wide variety of daemons. The stunnel map provides for more details about stunnel. Linux Security by Ramon Hontañón (Syex, 2001) for more information about securing a variety of services.

The primary reason for running POP or IMAP through stunnel is to ensure that the user's password cannot be stolen from a POP or IMAP session and then used by the thief to log in to the server. stunnel encrypts everything: the login and the download of mail. This guarantees that the contents of the mail cannot be surreptiously viewed by a snooper during the download, but from the point of view of the system administrator securing the content of the mail is usually unimportant. In all likelihood the mail moved through the Internet to the server. Encrypting as it moves from the server to the reader is a little silly after the worldwide exposure the mail has already received. The password is really the only piece of information you want to protect. Using a stronger form of authentication than simple clear text passwords can protect it. POP provides strong authentication through the optional APOP command of the POP3 protocol.

To offer the APOP command for your POP3 clients, you must install a daemon, such as Qualcomm's Qpopper, which implements the command. Qpopper is available as an RPM from many Linux vendors and can be located through rpmfind.net. Once you install it, make sure that the entry for pop in inet.conf or xinetd.conf points to the new in.qpopper program. The Qpopper package adds a program named popauth that to create passwords for the APOP command. Listing 12.2 shows how an administrator adding an APOP password for the user craig.

# Listing 12.2 Using the popauth command

```
[root]# popauth -user craig
Changing only APOP password for craig.
New password: SecretPassword
Retype password: SecretPassword
```

# Chapter 12 Sendmail Security

All of the things described above—removing logind and telnetd, limiting logins to secure shell, creating POP and IMAP users without login shells, protecting POP and IMAP passwords through encryption or strong authentication—are all done to prevent unauthorized login access. Of course, login access may not be the only network service that you want to protect on your Sendmail server. To control to all services started by inetd, use the wrapper.

# Controlling Network Access with Wrapper

The wrapper daemon, named tcpd, is executed by inetd. It is an integral part of most Linux distributions. Using the wrapper on a Linux system is easier than it is on any other systems because the entries in the inetd.conf file already point to the tcpd program. Listing 12.3 is a few lines from the inetd.conf file on a Caldera system.

# Listing 12.3 Linux Is Pre-configured for Wrapper

```
ftp stream tcp nowait root /usr/sbin/tcpd -l -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
shell stream tcp nowait root /usr/sbin/tcpd in.rshd
login stream tcp nowait root /usr/sbin/tcpd in.logrind
imap stream tcp nowait root /usr/sbin/tcpd imapad
```

In 12.3, bold text is used to highlight the reference to tcpd in each line of the inetd.conf file. The path to tcpd is used in place of the path of each service daemon. Therefore, when inetd receives a request for a service, it starts tcpd. tcpd then logs the service request, checks the access control information, and, if permitted, starts the daemon to handle the request.

The wrapper package performs two basic functions: it logs requests for Internet services and provides an access control mechanism for these services. If the tcpd access control files are not found, tcpd allows every host to have access and simply logs the access request. The wrapper uses the authpriv facility of syslog to log its messages. Look in the /etc/syslog.conf file to find out where your system logs authpriv messages. (On a Caldera system, these messages are logged to /var/log/secure.) Logging requests for specific network services is a useful monitoring function, especially if you are looking for possible intruders. If logging were all it, wrapper would be a useful package. But the real power of wrapper is its ability to control access to network services.

# Basic Security 331

tcpd Access Control Files Two files define access controls for tcpd. The hosts.allow file lists the hosts that are allowed to access the system's services and the hosts.deny file lists the hosts that are denied service. The format of entries in both files is the:

```
services : clients [: shell-command]:
```

services is a comma-separated list of network services or the keyword ALL. Otherwise, each individual service is identified by its process name, which is the name that immediately follows the path to tcpd in the inetd.conf file. For example, the process name in the following inetd.conf file is impad:

imap stream tcp nowait /usr/sbin/tcpd imapd clients is a comma-separated list of hostnames, domain names, Internet addresses, network numbers, and the keyword LOCAL. Alternately it can be the keyword ALL. ALL matches all hostnames and addresses that do not include a domain part. A hostname matches an individual host. An IP address can be defined by itself to match a specific host or with an address mask to match a range of addresses. A domain name starts with a (.) and matches every host within that domain. A network ends with a dot (.) and matches every IP address within the network space.

shell-command is an optional shell command that tcpd executes when a match occurs. If a match occurs, tcpd logs the access, grants or denies access to the service, and then passes the shell command to for execution. The shell command allows you to define additional processing that is triggered by a match in the control list. In all practical examples, this feature is used in the hosts.deny file to get more information about the intruder or to provide immediate notification to the system administrator about a security attack.

tcpd reads hosts.allow file first and then the hosts.deny file. It stops as soon as it finds a match for the host and the service in question. Therefore access granted by hosts.allow cannot be overridden by hosts.deny. For I usually start by inserting an entry in the hosts.deny which blocks access from all remote systems and use hosts.allow to permit only those computers you truly want to give login access through the blockade.

![img/9639113aa446fb8976cb3d77f7aafdd_354.png](img/9639113aa446fb8976cb3d77f7aafdd_354.png)

# Controlling Network Access with xinetd

An alternative to inetd is xinetd. xinetd is configured in the /etc/xinetd.conf file, which provides the same information to xinetd as inetd.conf provides to inetd. Instead of using positional parameters with meanings determined by location on a configuration line, xinetd.conf uses attribute names that identify the purpose of each parameter. Listing 12.4 shows a sample xinetd conf entry.

# 12.4 An xinetd.conf entry from Red Hat 7

```
# default: on
# description: logind is the server for the login(1) program. \
# The server provides a remote login facility with \
# authentication based on privileged port numbers from \
# trusted hosts.
service login {
  socket_type = stream
  wait = no
  user = root
  log_on_success += USERID
  log_on_failure += USERID
  server = /usr/sbin/in.logind
}
```

NOTE The xinetd daemon on Red Hat 7 Linux systems consult the /etc/hosts.allow and /etc/hosts.deny files in addition to the access controls defined in the xinetd.conf file.
