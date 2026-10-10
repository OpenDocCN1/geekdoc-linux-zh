
C.ROOT-SERVERS.NET.   3600000 NS   C.ROOT-SERVERS.NET.  
                                         A   192.33.4.12  
; formerly TERP.UMD.EDU

D.ROOT-SERVERS.NET.   3600000 NS   D.ROOT-SERVERS.NET.  
                                         A   128.8.10.90  
; formerly NS.NASA.GOV

E.ROOT-SERVERS.NET.   3600000 NS   E.ROOT-SERVERS.NET.  
                                         A   192.203.230.10  
; formerly NS.ISC.ORG

F.ROOT-SERVERS.NET.   3600000 NS   F.ROOT-SERVERS.NET.  
                                         A   192.5.5.241  
; formerly NS.NIC.DDN.MIL

G.ROOT-SERVERS.NET.   3600000 NS   G.ROOT-SERVERS.NET.  
                                         A   192.112.36.4  
; formerly AOS.ARL.ARMY.MIL

H.ROOT-SERVERS.NET.   3600000 NS   H.ROOT-SERVERS.NET.  
                                         A   128.63.2.53  
; formerly NIC.NORDU.NET

```
3600000 NS i.ROOT-SERVERS.NET.
i.ROOT-SERVERS.NET. 3600000 A 198.32.64.12
;
housed in Japan, operated by WIDE
;
M. 3600000 NS M.ROOT-SERVERS.NET.
M. 3600000 A 202.12.27.33
; End of File
```

Here is the `/var/named/named.local` file:

```
@ IN SOA localhost. root.localhost. (
19970122100 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
IN NS localhost.
1 IN PTR localhost.
```

Here is the `/var/named/named.domain.com` file:

```
@ IN SOA domain.com. hostmaster.domain.com. (
19960422300 ; serial number
10800 ;Refresh every 3 hours
1800 ;Retry every 30 minutes
1209600 ;Expire in 2 weeks
604800 ) ;Minimum 1 week
IN NS ns.domain.com.
IN MX 10 mail1.domains.com.
imp IN A 192.168.1.1 ; Internet gateway
mail IN A 192.168.1.2 ; mail server
technics IN A 192.168.1.3 ; web server
www IN CNAME technics
ns IN A 192.168.1.4 ; name server
peanutbutter IN A 192.168.1.5 ; firewall
```

Here is the `/var/named/named.rev` file:

```
@ IN SOA 1.168.192.in-addr.arpa. hostmaster.domain.com. (
1997010501 ; Serial
10800 ; Refresh rate (3 hours)
1800 ; Retry (30 minutes)
1209600 ; Expire (2 weeks)
604800 ) ; Minimum (1 week)

1 IN NS ns.domain.com.
2 IN PTR imp.domain.com.
3 IN PTR mail.domain.com
4 IN PTR technics.domain.com
5 IN NS ns.domain.com
6 IN PTR peanutbutter.com
```

We don't have to create any files to be secondary for example.com. We only need to add the entries we already have in the /etc/named.conf file.

And that's it: a complete configuration for a primary domain.

## The DNS Toolbox

This section describes a few tools that you'll want to get acquainted with as you work with DNS. They'll help you to troubleshoot problems more quickly.

### nslookup

The **nslookup** tool is really the master of all DNS tools. By learning all of the features nslookup has to offer, you can eliminate the need to learn several of the smaller tools that come with BIND.

In its simplest use, nslookup allows you to resolve host names into IP addresses from the command line. For example:

```
[root@ford root]# nslookup theorw.com
Server: localhost
Address: 127.0.0.1

Name: theorw.com
Address: 209.133.83.16
```

In the output, we see the name of the server that nslookup queried by default, and then the answer returned by that server. This example was run on a name server, so it was configured to look back at itself to resolve host names; thus, the server name is localhost.

We can also use nslookup to perform reverse lookups. For example:

```
[root@ford root]# nslookup 209.133.83.16
Server: localhost
Address: 127.0.0.1

Name: taz.hyperreal.org
Address: 209.133.83.16
```

This can lead to all kinds of interesting discoveries. In this case, we see that theorw.com is the same as taz.hyperreal.org. It's likely that taz.hyperreal.org is also "virtual hosting" other domains, as well.

> One of the goals of this book is to provide a way for NT administrators to become comfortable with Linux by demonstrating system parallels. This section visualizes some of the most important concepts for both operating systems so you can see how their foundations are established.

## Linux Administration Blueprints

## Table of Contents

- Linux vs. Windows NT Authentication....2
- Linux vs. Windows NT Based Network....4
- Linux vs. Windows NT Boot Process....6
- Linux vs. Windows NT Shut Down Process....8

## Linux vs. Windows NT Authentication

### Linux Authentication

![](img/95b125a8bf06051f34d8aba73558b7eb_291_0.png)

- **Step 1:** Application requests a password entry from the user
- **Step 2:** The /etc/nsswitch.conf file is checked to see where the password should be checked from
- **Step 3a:** Check the /etc/passwd (or /etc/shadow if applicable)
- **Step 3b:** Check the NIS Server for the password entry
- **Step 4:** NIS Server responds with the password entry
- **Step 5:** The application compares the two encrypted entries

### Windows NT Authentication

![](img/95b125a8bf06051f34d8aba73558b7eb_292_0.png)

The key difference between Linux and NT is that Linux performs all authentication issues outside of the core operating system. This gives a great deal of flexibility in how the authentication happens, and improves the stability of the system as a whole since it allows the Linux kernel to remain simple. The trade-off is consistency in the user interfaces and the need for application developers to handle their own authentication procedure.

## Linux vs. Windows NT Based Network

### Linux Network

- Any Mix of Windows Based Clients, Unix Clients, and Macintosh Clients
- Linux Based Intranet Server (Apache Web Server)
- Linux File Server (NFS/Samba/Netatalk)
- Linux Print Server (LPR/Samba/Netatalk)
- Linux Database (e.g., IBM DB2)
- Linux Backups (e.g., Legato)
- (Secondary DNS/NIS)
- Linux Based DNS/NIS Service
- Linux Firewall

![](img/95b125a8bf06051f34d8aba73558b7eb_293_0.png)

### Windows NT Based Network

![](img/95b125a8bf06051f34d8aba73558b7eb_294_0.png)

Both networks are functionally equivalent: whatever NT can do, Linux can do as well. However, Linux can typically do this with fewer servers and can support Windows and Macintosh clients as well. This is accomplished with the Samba package for working with Windows clients, and Netatalk for working with Macintosh clients.

## Linux vs. Windows NT Boot Process

### The Linux Boot Process

![](img/95b125a8bf06051f34d8aba73558b7eb_295_0.png)

- Step 1: Hardware reads boot sector
- Step 2: LILO Loads
- Step 3: Kernel loads
- Step 4: Root file system is mounted
- Step 5: Starts init, the "grandfather" of all processes
- Step 6: Read /etc/inittab
- Step 7: Run all scripts pointed to from run level 1
- Step 8: The end of run level 1 tells the system to go to run level 3
- Step 9: Run all scripts pointed to from run level 3
- Step 10: The system is ready

### The NT Boot Process

![](img/95b125a8bf06051f34d8aba73558b7eb_296_0.png)

The NT and Linux boot processes do strike parallels between each other. If you understand the reasoning behind one, you can understand the reasoning behind the other: They both start by reading the MBR, and they both end by providing login: prompts for the user. Noteworthy points of similarity are the NTLDR and LILO. They look different and act different, but in the end they do the exact same thing. NTDETECT, NTKSRNL, and HAL are three components that are all done in the Linux kernel. Although SMSS and init take very different paths, their goal is one and the same: getting the necessary service started.

## Linux vs. Windows NT Shut Down Process

### Linux Shutdown

![](img/95b125a8bf06051f34d8aba73558b7eb_297_0.png)

- Step 1: The shutdown or reboot command is invoked
- Step 2: Init is told to change to runlevel 6
- Step 3: The scripts in /runlevel 6 call init scripts with the parameter “Stop”
- Step 4: Outstanding buffers are written for disk (sync)
- Step 5: The file systems are unmounted
- Step 6: The system is halted

### NT Shutdown

![](img/95b125a8bf06051f34d8aba73558b7eb_297_1.png)

- Step 1: The shutdown command is invoked
- Step 2: The WINS Server is notified that the machine is leaving the network
- Step 3: Disconnections from all network services
- Step 4: The persistent connection to the PDC is closed
- Step 5: “Last Known Good” information is written to the registry
- Step 6: Services are shutdown
- Step 7: The system is halted

Unfortunately, the Linux and NT shutdown procedures don't show the same amount of parallels that their boot processes do. This stems from the nature of Linux's NIS, NFS, and LPR services versus NT's PDC and SMB protocols. Linux doesn't maintain persistent connections for those services; NT does.
