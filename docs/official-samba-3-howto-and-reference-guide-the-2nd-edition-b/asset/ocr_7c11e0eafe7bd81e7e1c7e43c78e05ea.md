```
```
-------          -------
DLORIN          Samba-3.0.20
Workgroup        Master
--------         -------
MIDEARTH         OLORIN
```
```

The following error message indicates that Samba was not running:

```
```
root# smbclient -L olorin -U/
Error connecting to 192.168.1.40 (Connection refused)
Connection to olorin failed.
```
```

8. Connect to OLORIN as maryl:


```
```
root# smbclient //olorin/maryo -Umaryo%secret
OS=[UNIX] Server=[Samba-3.0.20]
smb: \> dir
.			D		0	Sat Jun 21 10:58:16 2003
..			D		0	Sat Jun 21 10:54:32 2003
Documents		D		0	Fri Apr 25 13:23:58 2003
DOCWORK		D		0	Sat Jun 14 15:40:34 2003
OpenOffice.org	D		0	Fri Apr 25 13:55:16 2003
.bashrc		H		1286	Fri Apr 25 13:23:58 2003
.netcnscape6	DH		0	Fri Apr 25 13:55:13 2003
.mozilla		DH		0	Wed Mar 5 11:50:50 2003
.kermsrc		H		164	Fri Apr 25 13:23:58 2003
.acrobats		DH		0	Fri Apr 25 15:41:02 2003

				55817 blocks of size 524288. 34725 blocks available
smb: \> q
```
```

By now you should be getting the hang of configuration basics. Clearly, it is time to explore slightly more complex examples. For the remainder of this chapter we abbreviate instructions, since there are previous examples.

# ## 2.3.2 Domain Member Server

In this instance we consider the simplest server configuration we can get away with to make an accounting department happy. Let’s be warned, the users are accountants and they do have some nasty demands. There is a budget for only one server for this department.

The network is managed by an internal Information Services Group (ISG), to which we belong. Internal policies are typical of a medium-sized organization: Human Resources is