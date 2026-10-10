
## Turn Off EXPN and VRFY

Configure your SMTP server not to support EXPN and VRFY. To do this in Sendmail, edit /etc/sendmail.cf and set PrivacyOptions to authwarnings,noexpn,novrfy.

## DNS (Domain Name System): 53 (TCP/UDP)

DNS is a protocol used to translate between domain names and IP addresses.

### Obtain BIND Version Information

The most widely used DNS server software on Linux and Unix is BIND (Berkeley Internet Name Domain). The `dig` tool can be used to query for the version of BIND running on a particular host.

As an example, if the IP address of the host running BIND is 192.168.1.1:

```bash
$ dig -t txt -c chaos VERSION.BIND @192.168.1.1
; <<>> DiG 9.2.1 <<> -t txt -c chaos VERSION.BIND @192.168.1.1
; global options: printcmd
; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22464
; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL:0

; QUESTION SECTION:
;VERSION.BIND.                CH      TXT

; ANSWER SECTION:
VERSION.BIND.                 0   CH  TXT   "8.3.3-REL"

; Query time: 40 msec
; SERVER: 192.168.1.1#53(192.168.1.1)
; WHEN: Wed Jan 15 09:46:22 2003
; MSG SIZE  rcvd: 64
```

### Enumerate Remote Services

## Configure BIND to Not Display Version Information

Edit the BIND configuration file, named.conf, and override the version number:

```
options { version "Not available"; }
```

You might also want to configure BIND with specific ACLs and limit queries from specific hosts. See the BIND documentation for details. More information about BIND can be found at http://www.isc.org/products/BIND/.

## Finger: 79 (TCP)

Finger is a user information lookup program. Fingering a remote host will provide information such as usernames, IP addresses, idle time, and real names of the individuals logged on the host at the time.

### Enumerate Remote Users by Using the Finger Command

If the remote host is running a finger daemon, the command-line finger tool can be used to query the host:

```
finger @host
```

Example:

```
$ finger @192.168.1.1
Login    Name          TTY     Idle   When     Where
bob      Bob             pts/1    8     Wed 14:26   bobaddress.bobsisp.org
rob      Robert Smith    pts/4   51     Wed 12:46   dhcp.robshomeisp.org
tang     Thomas Tang     pts/3   1:08   Wed 10:07   somecasanexample.com
```

It is also possible to finger a specific username. Querying for a specific username will yield some information about the user even if the user is not logged on at the time:

```
finger username@host
```

Example:

```
$ finger root@192.168.1.1
Login name:  root        In real life: Sys Admin
Directory: /        Shell: /usr/local/bin/tcsh
Last login Jan 11 14:26:51 on tty2
```

New mail received Wed Jan 15 14:36:29 2003;
unread since Wed Jan 11 14:29:54 2003
No Plan.

An old finger (finger daemon) version of Solaris has been known to contain a vulnerability that discloses the list of all usernames on the host if queried with a string such as “`a b c d e f g h`”:

```
`finger 'a b c d e f g h'@host`
```

See [http://www.securityfocus.com/bid/3457/info/](http://www.securityfocus.com/bid/3457/info/) for more information about this vulnerability.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_97_0.png)

### Disable Finger

If you are running the finger server, it is strongly recommended that you consider the following suggestions:

- Consider disabling the finger service if possible. It provides far too much information about your system to local users and intruders. If you use inetd, finger can be disabled by commenting out the appropriate line in `/etc/inetd.conf`. If you use xinetd, edit the file named finger in the xinetd.d directory and make sure the following line exists:
  `disable = yes`

You must restart inetd or xinetd in order for changes to take effect.

- If you must run the finger server, configure your firewall to drop incoming connections to port 79. This will prevent users on external networks from querying your hosts.

## HTTP (Hypertext Transfer Protocol): 80 (TCP)

HTTP is a stateless protocol used to distribute various hypermedia. It is most widely used to serve WWW (World Wide Web) content.

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_97_1.png)

### Obtain the HTTP Server Banner

In order to grab banner information from HTTP servers, telnet to the port they are listening on and issue the following request:

```
`HEAD / HTTP/1.0[enter][enter]`
```

For example:

```
`(bash)$ telnet www.somecompanyasanexample.com 80`
`Trying 10.0.0.100...`
`Connected to www.somecompanyasanexample.com.`
```

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_97_2.png)

Escaped character is '^"'.
HEAD / HTTP/1.0 [enter]
[enter]
HTTP/1.1 200 OK
Date: Wed, 15 Jan 2003 17:59:12 GMT
Server: Apache/1.3.27 (Unix) PHP/4.2.1 mod_jk/1.2.0 mod_ssl/2.8.12 OpenSSL/0.9.6b
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
Connection closed by foreign host.

Some web servers do not allow HEAD requests. In this case, we must perform a GET query:
GET / HTTP/1.0[enter][enter]

This query will return to you the banner information, along with the default index page (such as index.html).

If you want to request a particular web page, say contact.html, you will need to append its name and path along with the GET request:
GET /contact.html HTTP/1.0[enter][enter]

> Sometimes, a single web server can be used to serve content for multiple domain names. In such cases, the specific domain name must be specified in the request. This can be done by typing `Host: domain-name` after the GET request. For example:
> GET / HTTP/1.0[enter]
> Host: www.domainname.com[enter][enter]

## Change the HTTP Server Banner

If you are running Apache, edit your httpd.conf file and make sure the following directives are present:

ServerSignature Off
ServerTokens Prod

Disabling the `ServerSignature` token instructs Apache to not print version information when an error page such as a “404-Not Found” is displayed. The `ServerTokens` directive, when set to `Prod`, instructs Apache to only display “Server: Apache” in the banner. If you do not want to display “Apache” in the Server tag but want to display fake information such as “Server: Not-allowed,” you will need to:

1. Download the Apache source code.
2. Edit the file `httpd.h` and change the value of the string “Apache” in the line
   ```c
   #define SERVER_BASEPRODUCT "Apache"
   ```
   to something else:
   ```c
   #define SERVER_BASEPRODUCT "Not-allowed"
   ```
3. Recompile, reinstall, and restart Apache.

## POP3 (Post Office Protocol 3): 110 (TCP)

POP3 is a protocol used to access e-mail from a mailbox server.

### Obtain the POP3 Server Banner

Telnet to port 110 to get the POP3 server banner information:

```bash
$ telnet 10.0.1.1 110
+OK POP3 10.0.1.1 v4.39 server ready
```

### Change the POP3 Server Banner

Many POP3 servers require their source code to be edited in order to change the server banner. In these cases, you must obtain the source code to your POP3 server and search for the version string by using the `grep` command. Once you have edited the source code to reflect the new banner information, recompile and reinstall the POP3 server. Some POP3 servers allow for banner information to be changed by editing appropriate configuration files. Please see your POP3 server documentation for details.

## Portmapper: 111 (TCP)

RPC (remote procedure call)–based services such as NIS (Network Information Service) do not listen on static ports. These services register their port numbers with the Portmapper.
