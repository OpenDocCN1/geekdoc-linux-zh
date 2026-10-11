username to use for all other hosts. Take a look at a typical sequence of commands involving a Kerberized ftp client in Listing 13.13.

# Listing 13.13 Obtaining a Kerberos ticket for use with the Kerberized ftp client

```
[ramon]$ hostname  
atlantis.hontanon.com
[ramon]$ kinit ramon@HONTANON.COM
Password for ramon@HONTANON.COM:  
[ramon]$ klist  
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

	Valid starting		Expires		Service principal
02/24/01 21:20:59	02/25/01 07:20:59	htgrp@HONTANON.COM

Kerberos 4 ticket cache: /tmp/tkt501
klist: You have no tickets cached
[ramon]$ ftp -x challenger
Connected to challenger.
220 challenger.hontanon.com FTP server (Version 5.60) ready.
334 Using authentication type GSSAPI; ADAT must follow
GSSAPI accepted as authentication type
GSSAPI authentication succeeded
200 Data channel protection level set to private.
232 GSSAPI user ramon@HONTANON.COM is authorized as ramon
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> pwd
257 "/home/ramon" is current directory.
ftp> bye
221 Goodbye.
[ramon]$ klist  
Ticket cache: FILE:/tmp/krb5cc_501
Default principal: ramon@HONTANON.COM

	Valid starting		Expires		Service principal
02/24/01 21:20:59	02/25/01 07:20:59	http@HONTANON.COM

```