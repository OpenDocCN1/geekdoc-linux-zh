# 22.2.1 SyncBreeze Enterprise

To begin our exploration of exploit modules, we will focus on a service that we’ve abused time and again: SyncBreeze. In this section, we will search for the exploits related to the SyncBreeze Enterprise application installed on the Windows 10 workstation and then exploit it using MSF. To begin, we will use the **search** command:

```
msf5 > **search syncbreeze**
Matching Modules
================

Name                      Disclosure Date   Rank    Description
----                      -----------------   ----    -----------
exploit/windows/fileformat/syncbreeze_xml   2017-03-29        normal  Sync Breeze Enterprise 9.5.16 – Import Command Buffer Overflow
exploit/windows/http/syncbreeze_bof         2017-03-15        great   Sync Breeze Enterprise GET Buffer Overflow
```

![](bbox=[0.35, 0.38, 0.65, 0.4])

The output reveals two specific exploit modules. We will focus on 10.0.28 and request **info** about that particular module.

```
msf5 > **info exploit/windows/http/syncbreeze_bof**
    Name: Sync Breeze Enterprise GET Buffer Overflow
    Module: exploit/windows/http/syncbreeze_bof
    Platform: Windows
    Arch:
    Privileged: Yes
    License: Metasploit Framework License (BSD)
    Rank: Great
    Disclosed: 2017-03-15

Provided by:
    Daniel Teixeira
    Andrew Smith
    Owais Mehtab
    Milton Valencia (wgtw0rk)

Available targets:
    Id  Name
    --  ----
     0   Automatic
     1   Sync Breeze Enterprise v9.4.28
     2   Sync Breeze Enterprise v10.0.28
     3   Sync Breeze Enterprise v10.1.16

Basic options:
    Name  Current Setting  Required  Description
    ----  ---------------  --------  -----------
    Proxies                no        A proxy chain of format type:host:port[,type:host:port]... 
    RHOST                   yes      The target address
    RPORT   80             yes       The target port (TCP)
    SSL     false          no        Negotiate SSL/TLS for outgoing connections
```