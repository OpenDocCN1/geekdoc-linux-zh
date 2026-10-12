```
humanresources          D   0 Tue Jul 13 23:57:36 1999
README                  261 Wed Jul 14 00:00:45 1999

33521 blocks of size 32768. 27022 blocks available
smb: \> quit
```

As you can see, we were able to connect to the public shared directory using the smbclient command and were able to view the directories and files contained there.

Now let's suppose that the user tschenk wants to mount his home directory on the server onto his local Linux client. To do this, he will use the smbmount and smbumount commands.

```
[tschenk@nomad tschenk]$ smbmount //quicksilver/tschenk -c 'mount -samba \
-u 500 -g 500'
Added interface ip=192.168.50.25 bcast=192.168.50.255 netmask=255.255.255.0
Server time is Wed Jul 14 00:14:57 1999
Timezone is UTC-5.0
Password:
Domain=[ALCHEMY] OS=[Unix] Server=[Samba 2.0.3]
security=user
```

```
[tschenk@nomad tschenk]$ cd samba
```

```
[tschenk@nomad samba]$ ls -l*
lilo-colors.tar.gz  limp_penguin_ai.zip  linux-1.3.0.tar.gz  ljf.quote
limp_penguin.ai    linux-1.0.tar.gz     linux-2.0.tar.gz    lodlin16.tgz
limp_penguin.eps   linux-1.1.0.tar.gz   linux-2.1.0.tar.gz
limp_penguin.jpg   linux-1.2.0.tar.gz   linux-2.2.0.tar.gz
```

```
[tschenk@nomad samba]$ cd ..

[tschenk@nomad tschenk]$ smbumount samba

[tschenk@nomad tschenk]$ ls samba
```

As you can see, the user tschenk was able to mount his shared home directory from the server onto a directory called samba and then unmount it again.

# Caution

In order for a regular user to mount and unmount shares in this fashion, the smbmount and smbumount commands must be made setuid root. They are not installed this way for the Red Hat RPM for Samba.