
machines and allows an administrator to quickly check these critical files for misconfigurations.

Correct the vulnerability by which the files were obtained.

Was found on the following hosts:
IP Address: 127.0.0.1		Hostname: Could not resolve hostname
Files grabbed from rsh into './127.0.0.1.rsh.files'
Files grabbed via FTP into ./127.0.0.1.anonftp.files

## Anonymous FTP [Low Risk]

Anonymous FTP is enabled on this machine.

Was found on the following hosts:
IP Address: 127.0.0.1		Hostname: Could not resolve hostname

## Netstat [Low Risk]

Netstat gives an intruder information regarding connections, open ports, and trusted hosts.

Disable the netstat daemon by comment it out of /etc/inetd.conf and restarting inetd.

Was found on the following hosts:
IP Address: 127.0.0.1		Hostname: Could not resolve hostname

## Sysstat [Low Risk]

Sysstat gives an intruder information such as who is online and trusted hosts.

Disable the sysstat daemon by comment it out of /etc/inetd.conf and restarting inetd.

Was found on the following hosts:
IP Address: 127.0.0.1		Hostname: Could not resolve hostname

## Verify Account Information About Users with Sendmail [Low Risk]

VRFY allows an intruder to determine if an account exists on a system, providing a significant aid to a brute force attack on user accounts.

If you are running Sendmail, add the line "Opmvrfy" to your Sendmail configuration file, usually located in /etc/sendmail.cf. With other mail servers, contact your vendor for information on how to disable the verify command.

Was found on the following hosts:

IP Address: 127.0.0.1        Hostname: Could not resolve hostname

## Expand Account Information About Users with Sendmail [Low Risk]

EXPN allows an intruder to determine if an account exists on a system, providing a significant aid to a brute force attack on user accounts.

If you are running Sendmail, add the line “O:noexpn” to your Sendmail configuration file, usually located in /etc/sendmail.cf. With other mail servers, contact your vendor for information on how to disable the verify command.

Was found on the following hosts:

IP Address: 127.0.0.1        Hostname: Could not resolve hostname

## Trace Routing of Packets [Low Risk]

Traceroute allows you to determine the path a packet takes between two hosts. This information allows someone to determine network topology and routers on the network.

Was found on the following hosts:

IP Address: 127.0.0.1        Hostname: Could not resolve hostname

127.0.0.1

0

--------- End of Report ---------

Listing 9-5 displays the trusted hosts – those that don’t need password authentication to log in to your system. In effect, your host might as well have the same type of security as the trusted hosts – which may seem convenient at first, but can be a real security problem. From the standpoint of security, the results of this scan were good because they show no trusted hosts.

Listing 9-5: Trusted hosts

```
Internet Security Scanner (C) 1992-1997
ISS SAFEsuite Version 4.3.8
By Internet Security Systems, Inc.
Analysis Report
```

Host Inventory

Summary Information

Hosts Scanned: 1

Hosts with Active Services: 1

Hosts with No Services: 0

Start Time: Tue Jul 7 15:40:21 1998
End Time  : Tue Jul 7 15:44:12 1998
Total Time: 3 minutes 51 seconds

Scan Completed Normally

Alive, Active without Host Names
IP Address: 127.0.0.1  Host Name: Could not resolve hostname

Hosts Trusted by scanned Hosts

No trusted hosts found.

========= End of Report =========

Listing 9-6 shows a report of services, which shows which services were found on your host. It also shows you which services were not found available on your host.

**Listing 9-6: Report of services**

```
Internet Security Scanner (C)1992-1997
ISS SAFESuite Version 4.3.8
By Internet Security Systems, Inc.
Analysis Report

Report of Services
Summary Information
Hosts Scanned: 1
Hosts with Active Services:  1
Hosts with No Services: 0
Start Time: Tue Jul 7 15:40:21 1998
End Time  : Tue Jul 7 15:44:12 1998
Total Time: 3 minutes 51 seconds
Scan Completed Normally

Information by Service

Open Port
Was found on the following hosts:
IP Address: 127.0.0.1   Hostname: Could not resolve hostname
Port 6000 ("X" service) opened.
Port 515 ("printer" service) opened.
Port 514 ("shell" service) opened.
Port 513 ("login" service) opened.
Port 143 ("imap" service) opened.
Port 113 ("ident" service) opened.
Port 111 ("sunrpc" service) opened.
Port 110 ("pop3" service) opened.
Port 37 ("time" service) opened.
Port 25 ("smtp" service) opened.
Port 23 ("telnet" service) opened.
Port 22 ("ssh" service) opened.
Port 21 ("ftp" service) opened.
Port 15 ("netstat" service) opened.
Port 11 ("sysstat" service) opened.
```

Many of these services, including sysstat, netstat, sunrpc, imap, pop3, and printer, can be shut off if they are not being used. They provide information about the host and some possible means of remotely accessing critical files. Listing 9-7 shows the scan for these services on the host.

## Listing 9-7: Scanning for services

```
Port Failure
   Was found on the following hosts:
   IP Address: 127.0.0.1     Hostname: Could not resolve hostname
   Service Failure 13326 ("crossfire(game)" service): Transport endpoint is not connected.
   Service Failure 9000 ("unknown" service): Transport endpoint is not connected.
   Service Failure 8000 ("unknown" service): Transport endpoint is not connected.
   Service Failure 8080 ("httpd" service): Transport endpoint is not connected.
   Service Failure 7002 ("backdoor?" service): Transport endpoint is not connected.
   Service Failure 7001 ("backdoor?" service): Transport endpoint is not connected.
   Service Failure 7000 ("afsserv or dos" service): Transport endpoint is not connected.
   Service Failure 6667 ("irc" service): Transport endpoint is not connected.
   Service Failure 6666 ("irc-serv" service): Transport endpoint is not connected.
   Service Failure 5858 ("netrek(game)" service): Transport endpoint is not connected.
   Service Failure 5000 ("unknown" service): Transport endpoint is not connected.
   Service Failure 4557 ("fax" service): Transport endpoint is not connected.
   Service Failure 4000 ("unknown" service): Transport endpoint is not connected.
   Service Failure 3000 ("unknown" service): Transport endpoint is not connected.
   Service Failure 2592 ("netrek[game]" service): Transport endpoint is not connected.
   Service Failure 2048 ("dls-monitor" service): Transport endpoint is not connected.
   Service Failure 2003 ("cflinger" service): Transport endpoint is not connected.
   Service Failure 2000 ("callbook" service): Transport endpoint is not connected.
   Service Failure 1999 ("tcp-id-port" service): Transport endpoint is not connected.
   Service Failure 1720 ("pptp" service): Transport endpoint is not connected.
   Service Failure 1525 ("oracle" service): Transport endpoint is not connected.
   Service Failure 1524 ("ingreslock" service): Transport endpoint is not connected.
   Service Failure 1080 ("SOCKs" service): Transport endpoint is not connected.
   Service Failure 1024 ("old_finger" service): Transport endpoint is not connected.
   Service Failure 888 ("C0Database" service): Transport endpoint is not connected.
   Service Failure 767 ("phonebook" service): Transport endpoint is not connected.
   Service Failure 765 ("webster" service): Transport endpoint is not connected.
   Service Failure 666 ("doom" service): Transport endpoint is not connected.
   Service Failure 600 ("ipcserver" service): Transport endpoint is not connected.
   Service Failure 566 ("remotefs" service): Transport endpoint is not connected.
   Service Failure 565 ("whoami" service): Transport endpoint is not connected.
   Service Failure 541 ("uucp-rlogin" service): Transport endpoint is not connected.
   Service Failure 540 ("uucp" service) : Transport endpoint is not connected.
   Service Failure 532 ("netnews" service) : Transport endpoint is not connected.
   Service Failure 531 ("conference" service) : Transport endpoint is not connected.
   Service Failure 530 ("courier" service) : Transport endpoint is not connected.
   Service Failure 518 ("ntalk" service) : Transport endpoint is not connected.
   Service Failure 517 ("talk" service) : Transport endpoint is not connected.
   Service Failure 512 ("exec" service) : Transport endpoint is not connected.
   Service Failure 450 ("tserver" service) : Transport endpoint is not connected.
   Service Failure 444 ("snpd" service) : Transport endpoint is not connected.
   Service Failure 443 ("https" service) : Transport endpoint is not connected.
   Service Failure 220 ("imap2" service) : Transport endpoint is not connected.
   Service Failure 177 ("xdmcp" service) : Transport endpoint is not connected.
   Service Failure 170 ("print-srv" service) : Transport endpoint is not connected.
   Service Failure 162 ("SNMPtrAP" service) : Transport endpoint is not connected.
   Service Failure 161 ("SNMP" service) : Transport endpoint is not connected.
   Service Failure 144 ("Nets" service) : Transport endpoint is not connected.
   Service Failure 139 ("netbios-ssn" service) : Transport endpoint is not connected.
   Service Failure 138 ("netbios-dgm" service) : Transport endpoint is not connected.
   Service Failure 137 ("netbios-ns" service) : Transport endpoint is not connected.
   Service Failure 135 ("netbios-rpc" service) : Transport endpoint is not connected.
   Service Failure 133 ("statsrv" service) : Transport endpoint is not connected.
   Service Failure 123 ("ntp" service) : Transport endpoint is not connected.
```
