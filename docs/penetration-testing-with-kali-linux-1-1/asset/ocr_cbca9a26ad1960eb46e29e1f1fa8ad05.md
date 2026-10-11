![](bbox=[0.12, 0.035, 0.25, 0.09])

> | Microsoft Windows system vulnerable to remote code execution (MS08-067)
> |   State: VULNERABLE
> |   Ids: CVE:CVE-2008-4250
> |   The Server service in Microsoft Windows 2000 SP4, XP SP2 and SP3, Server 2
> |   Vista Gold and SP1, Server 2008, and 7 Pre-Beta allows remote attackers to
> |   code via a crafted RPC request that triggers the overflow during path cano
> |   Disclosure date: 2008-10-13
> |   References:
> |       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-4250
> |       https://technet.microsoft.com/en-us/library/security/ms08-067.aspx
> | ...

Listing 254 - Determining whether a host is vulnerable to the MS08_067 vulnerability

In this case, Nmap identifies that the specific SMB service is missing at least one critical patch for the MS08-067$^{212}$ vulnerability.

# 7.3.2.1 Exercises

+   1.  Use Nmap to make a list of the SMB servers in the lab that are running Windows.
+   2.  UseNSE scripts to scan these systems for SMB vulnerabilities.
+   3.  Use nbtscan and enum4linux against these systems to identify the types of data you can obtain from different versions of Windows.

# 7.4 NFS Enumeration

Network File System (NFS)$^{213}$ is a distributed file system protocol originally developed by Sun Microsystems in 1984. It allows a user on a client computer to access files over a computer network as if they were on locally-mounted storage.

NFS is often used with UNIX operating systems and is predominantly insecure in its implementation. It can be somewhat difficult to set up securely, so it’s not uncommon to find NFS shares open to the world. This is quite convenient for us as penetration testers, as we might be able to leverage them to collect sensitive information, escalate our privileges, and so forth.

# 7.4.1 Scanning for NFS Shares

Both *Portmapper*$^{214}$ and *RPCbind*$^{215}$ run on TCP port 111. RPCbind maps RPC services to the ports on which they listen. RPC processes notify rpcbind when they start, registering the ports they are listening on and the RPC program numbers they expect to serve.

The client system then contacts rpcbind on the server with a particular RPC program number. The rpcbind service redirects the client to the proper port number (often TCP port 2049) so it can

$^{212}$ (Microsoft, 2008), http://technet.microsoft.com/en-us/security/bulletin/ms08-067
$^{213}$ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Network_File_System
$^{214}$ (Wikipedia, 2017), http://en.wikipedia.org/wiki/Portmap
$^{215}$ (Red Hat, 2019), https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/storage_administration_guide/s2-nfs-methodology-portmap