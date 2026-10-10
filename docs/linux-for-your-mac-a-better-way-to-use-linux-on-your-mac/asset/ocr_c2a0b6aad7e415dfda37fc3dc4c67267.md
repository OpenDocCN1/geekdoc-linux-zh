```
writable = yes
path = /home/bball
```

In this example, the home directory of the user bball is published (and the hostname of the computer is green). On the host, next restart the Samba daemon (as root) to read in the new configuration:

```
# /etc/rc.d/init.d/smb restart
Restarting SMB services:            [ OK ]
Restarting NMB services:            [ OK ]
```

The smbmount can then be used to mount the remote directory. However, you can also use the smbclient command, which mimics the FTP client, to access files and upload or download files to and from the remote share:

```
$ smbclient //green/bball
added interface ip=192.168.2.99 bcast=192.168.2.255 nmask=255.255.255.0

Password:

Domain=[LINUX_SSERVER] OS=[Unix] Server=[Samba 2.0.5a]
smb: \> ls *.pcx
04fig01.pcx          1077841  Wed May  2 13:57:39 2001
04fig02.pcx          1085118  Wed May  2 13:57:41 2001
04fig03.pcx          1085360  Wed May  2 13:57:43 2001

                    63643 blocks of size 16384, 12262 blocks available
smb: \> ?
ls	dir	du	lcd	cd
pwd	get	mget	put	mput
rename	more	mask	del	open
rm	mkdir	md	mrd	cd
prompt	recurse	translate	lowercase	print
printmode	queue	cancel	quit	q
exit	never	archive	tar .	blocksize

smb: \> mget *.pcx
Get file 04fig01.pcx? y
getting file 04fig01.pcx of size 1077841 as 04fig01.pcx (1045.26 kb/s) (average 1045.26 kb/s)

Get file 04fig02.pcx? n
Get file 04fig03.pcx? n
smb: \> exit
$
```