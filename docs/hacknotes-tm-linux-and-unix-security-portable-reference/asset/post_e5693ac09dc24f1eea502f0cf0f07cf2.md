
- Do not allow incoming SNMP traffic from your firewall.
- Restrict your SNMP ACLs to allow connections only from specific hosts.

# HTTPS (Secure Hypertext Transfer Protocol): 443 (TCP)

HTTPS is HTTP over SSL (Secure Sockets Layer). HTTPS uses SSL in order to set up and maintain a secure channel, and it therefore provides encrypted communication between the client and the server.

## Obtain the HTTPS Server Banner

The command-line openssl tool can be used to connect to an HTTPS server. Similar to what happens with HTTP (port 80), a request such as

```
HEAD / HTTP/1.0 [enter][enter]
```

or

```
GET / HTTP/1.0 [enter][enter]
```

can be used to obtain banner information.

Example:

```
[bash]$ openssl s_client -connect:192.168.1.1:443
```

[various items of certificate deleted]

```
HEAD / HTTP/1.0[enter]
[enter]
HTTP/1.1 200 OK
Date: Wed, 15 Jan 2003 17:59:12 GMT
Server: Apache/1.3.27 (Unix) PHP/4.2.1 mod_jk/1.2.0 mod_ssl/2.8.12 OpenSSL/0.9.6h
Content-Location: index.html.en
Vary: negotiate,accept-language,accept-charset
TCN: choice
Last-Modified: Thu, 09 May 2002 19:47:31 GMT
Accept-Ranges: bytes
Content-Length: 2673
Connection: close
Content-Type: text/html
Content-Language: en
Expires: Wed, 15 Jan 2003 17:59:12 GMT

Closed
```

## Change the HTTPS Server Banner

Please see “Change the HTTP Server Banner.”

# NNTPS (Secure Network News Transfer Protocol): 563 (TCP)

NNTPS is NNTP over SSL (Secure Sockets Layer). NNTPS uses SSL in order to set up and maintain a secure channel, and therefore provides encrypted communication between the client and the server.

## Grab the NNTPS Server Banner

The command-line `openssl` tool can be used to connect to an NNTPS server in order to obtain banner information:

```
[bash]$ openssl s_client -connect:192.168.1.1:563

[Various items of certificate information deleted]
```

```
200 192.168.1.1 InterNetNews NNRP server INN 1.4 22-Dec-93 ready (posting_ok).
```

OpenSSL is available at http://www.openssl.org.

## Change the NNTPS Server Banner

Please see “Change the NNTP Server Banner.”

# IMAPS (Secure Internet Message Access Protocol): 993 (TCP)

IMAPS is IMAP over SSL (Secure Sockets Layer). IMAPS uses SSL in order to set up and maintain a secure channel, and therefore provides encrypted communication between the client and the server.

## Grab the IMAPS Server Banner

The command-line `openssl` tool can be used to connect to an IMAPS server in order to obtain banner information:

```
[bash]$ openssl s_client -connect:192.168.1.1:993

[Various items of certificate information deleted]
```

> * OK [CAPABILITY IMAP4 IMAP4rev1 LOGIN-REFERRALS AUTH=LOGIN]
> localhost IMAP4rev1 2000.283 at Thu, 16 Jan 2003 03:51:56
> -0500 (EST)

OpenSSL is available at http://www.openssl.org/.

## Change the IMAPS Server Banner

Please see “Change the IMAP Server Banner.”

# POP3S (Secure Post Office Protocol 3): 995 (TCP)

POP3S is POP3 over SSL (Secure Sockets Layer). POP3S uses SSL in order to set up and maintain a secure channel, and therefore provides encrypted communication between the client and the server.

## Obtain the POP3S Server Banner

The command-line openssl tool can be used to connect to a POP3S server in order to obtain banner information:

```
[bash]$ openssl s_client -connect:192.168.1.1:995
```

[Various items of certificate information deleted]

> *OK QPOP (version 2.53) at 192.168.1.1 starting.
> <3413.1213453134@192.168.1.1>

OpenSSL is available at http://www.openssl.org/.

## Change the POP3S Server Banner

Please see “Change the POP3 Server Banner.”

# MySQL: 3306 (TCP)

MySQL is a popular open-source database software package. It is available from http://www.mysql.com/.

## Enumerate MySQL Version Information

It is possible to obtain the version number of the remote MySQL server by connecting to its port using the telnet client:

```
[bash]$ telnet 10.0.0.1 3306
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
3.23.45&/r/3Nod*Connection closed by foreign host.
```

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_108_0.png)

## Allow Only Local Connections

Do not allow hosts outside the intranet to connect to MySQL services. Ensure firewall rules are present to block such connection attempts. Authorized external users should be encouraged to use secure tunneling tools such as SSH to establish remote connections.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_108_1.png)

Although the MySQL source code can be edited to change the version information that is displayed immediately upon connect, it is likely that doing so will break many MySQL clients.

# AUTOMATED BANNER-GRABBING

Ncat is a tool used to read and write data across network connections using TCP or UDP. It can be used to connect to remote servers like the command-line telnet client, or to listen on specific ports for incoming connections. It has a lot of other interesting capabilities, which you will explore in later chapters. Ncat is available at [http://www.atstake.com/research/tools/network_utilities/](http://www.atstake.com/research/tools/network_utilities/).

Ncat can be used to grab the SMTP banner in the following way:

```
$ nc 192.168.1.1 25
220 192.168.1.1 ESMTP Sendmail 8.10.2+Sun/8.10.2; Tue, 14 Jan 2003 09:28:02 -0500 (EST)
```

With a little bit of bash shell programming, you can use Ncat to perform automated banner-grabbing. For example, consider the following script (let us call it grab.bash):

```
#!/bin/bash

if [ $# -lt 1 ]
then
    echo Usage: $0 host
    exit 1
fi

i=21
while [ "$i" -lt 26 ]
do
    nc -v $i < /dev/null
    i=`expr $i + 1`
    echo
done
```

This script consists of a while loop for the values of the variable $i$ ranging from 21 to 25. Within the while loop, a connection to a host (the first parameter passed to the script, i.e., $I$) is made on ports of value $i$ (21 to 25), and /dev/null is given as input to the Netcat connection. Since /dev/null is a special file that contains nothing (null), Netcat will immediately terminate after grabbing the first line of the banner (if any).

Before attempting to execute the preceding script, execute permissions must be granted:

```
[bash]$ chmod u+x ./grab.bash
```

Now run the script:

```
[bash]$ ./grab.bash 192.168.1.1
192.168.1.1 [192.168.1.1] 21 (ftp) open
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
221 You could at least say goodbye.

192.168.1.1 [192.168.1.1] 22 (ssh) open
SSH-1.99-OpenSSH_3.4p1

192.168.1.1 [192.168.1.1] 23 (telnet) : Connection refused

192.168.1.1 [192.168.1.1] 24 (?) : Connection refused

192.168.1.1 [192.168.1.1] 25 (smtp) open
220 192.168.1.1 ESMTP Sendmail 8.9.3/8.9.3; Fri, 17 Jan 2003 14:13:10 -0500 (EST)
```

If the preceding script needs to be executed on various hosts, you can write a wrapper against your grab.bash script like this:

```
#!/bin/bash
for i in `cat hosts.txt`
do
    ./grab.bash $i
    echo
done
```

The preceding script, which could be called wrapper-grab.bash, will execute our original script grab.bash against hosts listed in the file hosts.txt. The hosts.txt file must contain hostnames or IP addresses of target hosts like this:

```
192.168.1.1
10.0.0.1
somecompanyasanexample.com
```

Though the preceding script will work with most services, recall that you need to issue a HEAD request in order to obtain a HTTP banner. In order to do this, Ncat can be used like this, where getrequest.txt is a file containing

```
HEAD / HTTP/1.0[enter]
[enter]
```

Remember to use openssl instead of Ncat for SSL ports such as HTTPS, NNTPS, IMAPS, and POP3S, as described previously.

# SUMMARY

This chapter covered ways to identify services running on nonstandard ports using the Amap tool and how to manually and automatically identify services running on standard ports. You also looked at different ways to remotely enumerate usernames. Now, you are ready to move on to Chapter 4, where you will use the information gained in this chapter to exploit remote services in order to gain access to vulnerable hosts.
